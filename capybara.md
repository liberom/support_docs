# Capybara

Capybara is a Ruby integration testing framework that simulates how real users interact with web applications. It provides an intuitive DSL (Domain Specific Language) for automating browser interactions such as clicking links, filling forms, and verifying page content. Capybara works with any Rack-based web application including Rails, Sinatra, and Merb, making it a versatile choice for acceptance testing.

The library abstracts away driver-specific implementations, allowing developers to write tests once and run them against different backends. By default, Capybara uses Rack::Test for fast headless testing, but can seamlessly switch to Selenium WebDriver for JavaScript-enabled testing. It features powerful synchronization capabilities that automatically wait for asynchronous processes to complete, eliminating the need for manual sleep statements and reducing test flakiness.

## APIs and Functions

### Visiting Pages

Navigate to URLs within your application or external websites.

```ruby
require 'capybara/dsl'

# Visit a relative path (requires Capybara.app to be set)
visit '/users/sign_in'

# Visit an absolute URL
visit 'https://example.com'

# Check current location
expect(page).to have_current_path('/dashboard')
current_path # => '/dashboard'
current_url  # => 'http://www.example.com/dashboard'
```

### Finding Elements

Locate elements on the page using CSS selectors, XPath, or semantic locators.

```ruby
# Find by CSS selector
element = find('div.user-profile')
element = find('#main-content')

# Find by XPath
element = find(:xpath, './/div[@id="content"]')

# Find with filters
element = find('a', text: 'Sign Out', visible: true)
element = find('input', id: 'email', disabled: false)

# Find specific element types
find_field('Username')      # Locates input/textarea by label, name, or id
find_link('Read More')      # Locates links by text, id, or title
find_button('Submit')       # Locates buttons by text, value, or id
find_by_id('user-email')   # Locates by id attribute

# Find all matching elements
all('table tbody tr').each do |row|
  puts row.text
end

# Find with waiting behavior (waits up to default_max_wait_time)
begin
  element = find('.async-loaded-content', wait: 10)
rescue Capybara::ElementNotFound => e
  puts "Element not found: #{e.message}"
end
```

### Clicking Links and Buttons

Interact with clickable elements on the page.

```ruby
# Click a link by text, id, or title
click_link('About Us')
click_link('navigation-home')

# Click a button by text, value, name, or id
click_button('Save Changes')
click_button('submit-btn')

# Click either a link or button
click_on('Continue')

# Click with options
click_link('Profile', match: :first)
click_button('Delete', wait: 5)

# Direct element click with coordinates offset
element = find('#draggable')
element.click(x: 10, y: 10)
```

### Filling Forms

Enter data into form fields including text inputs, textareas, and file uploads.

```ruby
# Fill in text field by label, name, id, or placeholder
fill_in 'Email', with: 'user@example.com'
fill_in 'Password', with: 'secret123', currently_with: ''

# Fill in with special options
fill_in 'search', with: 'Capybara', fill_options: { clear: :backspace }

# Attach files to file input fields
attach_file('profile_picture', '/path/to/photo.jpg')
attach_file('documents', ['/path/to/doc1.pdf', '/path/to/doc2.pdf'])

# Attach with make_visible option for hidden file inputs
attach_file('avatar', '/path/to/image.png', make_visible: true)

# Block form for attaching files
attach_file('/path/to/file.pdf') do
  click_button('Upload Document')
end
```

### Selecting Options

Select and unselect options from dropdowns, radio buttons, and checkboxes.

```ruby
# Select from dropdown by visible text
select 'United States', from: 'Country'
select '2024', from: 'year_select'

# Unselect from multi-select
unselect 'Python', from: 'Languages'

# Choose radio button
choose('payment_method_credit_card')
choose('Male')

# Check checkbox
check('terms_and_conditions')
check('Subscribe to newsletter')

# Uncheck checkbox
uncheck('marketing_emails')

# With options and error handling
begin
  choose('option_value', wait: 5, allow_label_click: true)
rescue Capybara::ElementNotFound => e
  puts "Radio button not found: #{e.message}"
end
```

### Querying Page Content

Check for the presence or absence of content, elements, and attributes.

```ruby
# Check for text content
page.has_content?('Welcome back!')        # => true
page.has_text?('Error', wait: 3)         # => false
page.has_no_content?('Logged out')       # => true

# Check for CSS selectors
page.has_css?('div.alert-success')       # => true
page.has_no_css?('.error-message')       # => true

# Check for XPath
page.has_xpath?('.//table//tr', count: 5) # => true

# Check for specific elements
page.has_link?('Sign In')                 # => true
page.has_button?('Submit', disabled: false) # => true
page.has_field?('email', with: 'test@example.com') # => true
page.has_checked_field?('remember_me')    # => true
page.has_select?('country', selected: 'USA') # => true

# RSpec matchers (recommended)
expect(page).to have_content('Dashboard')
expect(page).to have_css('.user-profile', count: 1)
expect(page).to have_selector('table tr', minimum: 1)
expect(page).to have_link('Logout', href: '/logout')
expect(page).not_to have_button('Delete', visible: true)
```

### Scoping Interactions

Restrict actions to specific sections of the page using within blocks.

```ruby
# Scope by CSS selector
within('#sidebar') do
  click_link('Settings')
  expect(page).to have_content('Account')
end

# Scope by XPath
within(:xpath, './/div[@id="comments"]') do
  all('.comment').each do |comment|
    puts comment.find('.author').text
  end
end

# Scope to fieldset by legend text
within_fieldset('Personal Information') do
  fill_in 'First Name', with: 'John'
  fill_in 'Last Name', with: 'Doe'
end

# Scope to table by caption text
within_table('Users') do
  expect(page).to have_selector('tr', count: 10)
end

# Nested scoping
within('.content') do
  within('.article') do
    click_link('Read More')
  end
end
```

### Working with Windows

Manage multiple browser windows and tabs.

```ruby
# Open a new window
new_window = open_new_window
within_window(new_window) do
  visit '/terms'
  expect(page).to have_content('Terms of Service')
end

# Track window opened by an action
popup = window_opened_by do
  click_button('Share')
end

within_window(popup) do
  fill_in 'email', with: 'friend@example.com'
  click_button('Send')
end

# Switch between windows
windows = page.windows
original_window = windows.first
new_window = windows.last

switch_to_window(new_window)
# ... perform actions in new window
switch_to_window(original_window)

# Get current window
current_window.maximize
current_window.resize_to(1024, 768)
current_window.close
```

### JavaScript Execution

Execute and evaluate JavaScript code in browser drivers that support it.

```ruby
# Execute JavaScript (no return value expected)
page.execute_script("document.getElementById('hidden').style.display = 'block'")
page.execute_script("$('button').trigger('click')")

# Evaluate JavaScript and get result
result = page.evaluate_script('4 + 4')  # => 8
title = page.evaluate_script('document.title')

# Pass arguments to JavaScript
element = find('#calculator')
result = page.evaluate_script(<<~JS, 5, element)
  (function(num, el) {
    var currentValue = parseInt(el.value, 10);
    return num + currentValue;
  })(arguments[0], arguments[1])
JS

# Async JavaScript evaluation
page.evaluate_async_script(<<~JS)
  var callback = arguments[0];
  setTimeout(function() {
    callback('Async result');
  }, 1000);
JS
```

### Modal Dialogs

Handle JavaScript alerts, confirms, and prompts.

```ruby
# Accept alert
message = accept_alert do
  click_button('Delete Account')
end
expect(message).to eq('Are you sure?')

# Accept alert with specific message
accept_alert('Data will be lost') do
  click_link('Reset')
end

# Accept confirmation
accept_confirm do
  click_button('Proceed')
end

# Dismiss confirmation
dismiss_confirm do
  click_button('Cancel')
end

# Accept prompt with input
accept_prompt(with: 'New Project') do
  click_button('Create')
end

# Dismiss prompt
dismiss_prompt do
  click_button('Rename')
end

# Handle with error checking
begin
  accept_confirm(wait: 5) do
    click_button('Submit')
  end
rescue Capybara::ModalNotFound => e
  puts "No modal appeared: #{e.message}"
end
```

### Sessions and Drivers

Manage multiple sessions and switch between different drivers.

```ruby
# Configure default driver
Capybara.default_driver = :selenium_chrome

# Use a different driver temporarily
Capybara.using_driver(:selenium_headless) do
  visit '/admin'
  expect(page).to have_content('Admin Panel')
end

# Switch driver for current session
Capybara.current_driver = :selenium
visit '/dashboard'
Capybara.use_default_driver

# Named sessions for multiple simultaneous users
Capybara.using_session('admin') do
  visit '/login'
  fill_in 'username', with: 'admin'
  fill_in 'password', with: 'admin123'
  click_button 'Login'
end

Capybara.using_session('user') do
  visit '/login'
  fill_in 'username', with: 'user'
  fill_in 'password', with: 'user123'
  click_button 'Login'
end

# Manual session management
session = Capybara::Session.new(:selenium, MyRackApp)
session.visit('/posts')
session.fill_in 'title', with: 'New Post'
session.click_button('Publish')
```

### Configuration

Customize Capybara's behavior through configuration options.

```ruby
Capybara.configure do |config|
  # Server configuration
  config.run_server = true
  config.server = :puma
  config.server_port = 3000
  config.app_host = 'http://localhost:3000'

  # Waiting and timing
  config.default_max_wait_time = 5
  config.default_retry_interval = 0.05

  # Selector and matching
  config.default_selector = :css
  config.match = :smart  # :one, :first, :prefer_exact, :smart
  config.exact = false
  config.exact_text = false

  # Element visibility
  config.ignore_hidden_elements = true
  config.automatic_reload = true

  # Paths and debugging
  config.save_path = 'tmp/capybara'
  config.automatic_label_click = false

  # Testing behavior
  config.raise_server_errors = true
  config.predicates_wait = true
end

# Register custom driver
Capybara.register_driver :selenium_custom do |app|
  options = Selenium::WebDriver::Chrome::Options.new
  options.add_argument('--headless')
  options.add_argument('--disable-gpu')
  options.add_argument('--window-size=1920,1080')

  Capybara::Selenium::Driver.new(
    app,
    browser: :chrome,
    options: options
  )
end
```

### Custom Selectors

Define custom selectors for frequently used element patterns.

```ruby
# Add a custom selector
Capybara.add_selector(:data_id) do
  xpath { |id| XPath.descendant[XPath.attr(:'data-id') == id.to_s] }
end

# Use custom selector
find(:data_id, 'user-123')
page.has_selector?(:data_id, 'product-456')

# Add selector with filters
Capybara.add_selector(:row) do
  xpath { |num| ".//tbody/tr[#{num}]" }

  filter(:status) do |node, status|
    node.has_css?(".status-#{status}")
  end
end

# Use with filters
find(:row, 3, status: 'active')

# Modify existing selector
Capybara.modify_selector(:button) do
  filter(:data_action) { |node, action| node['data-action'] == action }
end

find(:button, 'Submit', data_action: 'create')
```

### RSpec Integration

Integrate Capybara with RSpec for feature testing.

```ruby
# spec_helper.rb or rails_helper.rb
require 'capybara/rspec'

RSpec.configure do |config|
  config.include Capybara::DSL
end

# Feature spec example
RSpec.describe 'User authentication', type: :feature do
  before do
    User.create(email: 'user@example.com', password: 'password123')
  end

  scenario 'successful login' do
    visit '/login'

    within('#login-form') do
      fill_in 'Email', with: 'user@example.com'
      fill_in 'Password', with: 'password123'
      click_button 'Sign In'
    end

    expect(page).to have_content('Welcome back!')
    expect(page).to have_current_path('/dashboard')
    expect(page).to have_link('Logout')
  end

  scenario 'failed login with invalid credentials', js: true do
    visit '/login'

    fill_in 'Email', with: 'wrong@example.com'
    fill_in 'Password', with: 'wrongpassword'
    click_button 'Sign In'

    expect(page).to have_css('.alert-error', text: 'Invalid credentials')
    expect(page).to have_current_path('/login')
  end

  scenario 'password reset flow', driver: :selenium_headless do
    visit '/login'
    click_link 'Forgot password?'

    expect(page).to have_content('Reset your password')

    fill_in 'Email', with: 'user@example.com'
    click_button 'Send reset link'

    expect(page).to have_content('Check your email')
  end
end

# Using feature/scenario DSL
feature 'Shopping cart' do
  background do
    @product = Product.create(name: 'Ruby Book', price: 29.99)
  end

  scenario 'adding items to cart' do
    visit "/products/#{@product.id}"
    click_button 'Add to Cart'

    expect(page).to have_content('Item added to cart')

    visit '/cart'
    expect(page).to have_content('Ruby Book')
    expect(page).to have_content('$29.99')
  end
end
```

### Debugging

Debug failing tests by inspecting page state.

```ruby
# Save and open HTML snapshot
save_and_open_page

# Save HTML to file
save_page('debug.html')

# Print current HTML
puts page.html

# Take screenshot (for drivers that support it)
save_screenshot('error.png')
save_and_open_screenshot

# Take screenshot with full page
save_screenshot('full_page.png', full: true)

# Get page source
page_source = page.source

# Debug information
puts "Current URL: #{current_url}"
puts "Current path: #{current_path}"
puts "Page title: #{page.title}"

# Using debugger in test
scenario 'debug example' do
  visit '/complex-page'

  # Pause and inspect
  binding.pry  # or debugger

  # Continue test
  click_button('Submit')
end
```

### Minitest Integration

Use Capybara with Minitest for integration testing.

```ruby
# test_helper.rb
require 'capybara/minitest'

class ActionDispatch::IntegrationTest
  include Capybara::DSL
  include Capybara::Minitest::Assertions

  teardown do
    Capybara.reset_sessions!
    Capybara.use_default_driver
  end
end

# Integration test example
class UserFlowsTest < ActionDispatch::IntegrationTest
  test 'user can sign up' do
    visit '/signup'

    fill_in 'user[email]', with: 'newuser@example.com'
    fill_in 'user[password]', with: 'secure_password'
    fill_in 'user[password_confirmation]', with: 'secure_password'

    click_button 'Create Account'

    assert_content 'Welcome!'
    assert_current_path '/dashboard'
    assert_selector 'h1', text: 'Dashboard'
    refute_selector '.error'
  end

  test 'displays validation errors' do
    visit '/signup'
    click_button 'Create Account'

    assert_content 'Email can\'t be blank'
    assert_selector '.field_with_errors', count: 2
  end
end

# Using Minitest::Spec style
describe 'Posts feature' do
  it 'creates a new post' do
    visit '/posts/new'

    fill_in 'Title', with: 'Test Post'
    fill_in 'Body', with: 'This is a test post'
    click_button 'Publish'

    page.must_have_content 'Post published'
    page.must_have_current_path '/posts/1'
  end
end
```

### Cucumber Integration

Write BDD-style feature tests with Cucumber and Capybara.

```ruby
# features/support/env.rb
require 'capybara/cucumber'

Capybara.default_driver = :selenium_chrome
Capybara.app = MyRackApp

# features/step_definitions/user_steps.rb
Given('a user exists with email {string}') do |email|
  User.create(email: email, password: 'password123')
end

When('I sign in as {string}') do |email|
  visit '/login'
  fill_in 'Email', with: email
  fill_in 'Password', with: 'password123'
  click_button 'Sign In'
end

Then('I should see the dashboard') do
  expect(page).to have_content('Dashboard')
  expect(page).to have_current_path('/dashboard')
end

When('I fill in the search form with {string}') do |query|
  within('#search-form') do
    fill_in 'q', with: query
    click_button 'Search'
  end
end

Then('I should see {int} search results') do |count|
  expect(page).to have_selector('.search-result', count: count)
end

# features/user_authentication.feature
@javascript
Feature: User Authentication
  As a user
  I want to sign in to my account
  So that I can access my dashboard

  Scenario: Successful login
    Given a user exists with email "user@example.com"
    When I sign in as "user@example.com"
    Then I should see the dashboard
    And I should see "Welcome back!"
```

### Query String HTML

Parse and query HTML strings without a full browser session.

```ruby
# Parse HTML string
node = Capybara.string('<div class="user"><span>John Doe</span></div>')

# Query the parsed HTML
node.has_selector?('div.user')  # => true
node.find('span').text          # => "John Doe"

# Complex HTML parsing
html = <<-HTML
  <ul id="users">
    <li class="user" data-id="1">Alice</li>
    <li class="user" data-id="2">Bob</li>
    <li class="user" data-id="3">Charlie</li>
  </ul>
HTML

doc = Capybara.string(html)

# Query parsed document
doc.has_css?('#users')                           # => true
doc.all('.user').count                           # => 3
doc.find('.user[data-id="2"]').text             # => "Bob"
doc.has_selector?('li.user', count: 3)          # => true

# Extract data
users = doc.all('.user').map { |li|
  { id: li['data-id'], name: li.text }
}
# => [{id: "1", name: "Alice"}, {id: "2", name: "Bob"}, {id: "3", name: "Charlie"}]
```

## Summary

Capybara excels at integration testing for web applications by providing a high-level DSL that mirrors user interactions. Common use cases include end-to-end testing of user workflows (registration, login, checkout), form validation testing, JavaScript-heavy interface testing, and cross-browser compatibility testing. The framework's automatic waiting behavior makes it particularly effective for testing modern single-page applications with asynchronous content loading, while its driver-agnostic design allows tests to run in fast headless mode during development and switch to real browsers in CI environments.

Integration patterns typically involve combining Capybara with testing frameworks like RSpec, Minitest, or Cucumber for structured test organization. Tests can be written using the DSL directly by including `Capybara::DSL`, or accessed through the `page` object in supported frameworks. For Rails applications, Capybara integrates seamlessly with system tests and feature specs, automatically managing the application server and database transactions. The library also supports advanced scenarios like testing multiple concurrent sessions, custom driver configuration for specialized browsers, and extending functionality through custom selectors and matchers, making it adaptable to diverse testing requirements.
