# RSpec Rails

RSpec Rails brings the RSpec testing framework to Ruby on Rails as a drop-in alternative to Minitest. It provides a behavior-driven development (BDD) approach where tests are not just scripts but detailed specifications of how the application should behave, expressed in plain English. The gem integrates seamlessly with Rails' built-in components and provides specialized testing capabilities for models, controllers, views, routing, mailers, jobs, and system tests.

The framework follows Rails versioning closely, supporting Rails 7.2+ in version 8.x. It extends RSpec's core functionality with Rails-specific matchers, helpers, and example groups that make testing Rails applications intuitive and efficient. The gem automatically hooks into Rails generators to create spec files alongside application code, and provides a comprehensive testing DSL that works with all major Rails components including ActiveRecord, ActionController, ActionView, ActionMailer, ActiveJob, and ActionCable.

## Installation and Setup

Generate RSpec configuration files in a Rails project

```ruby
# In Gemfile
group :development, :test do
  gem 'rspec-rails', '~> 8.0.0'
end
```

```bash
# Install the gem
bundle install

# Generate configuration files
rails generate rspec:install
# Creates:
#   .rspec
#   spec/
#   spec/spec_helper.rb
#   spec/rails_helper.rb

# Run all specs
bundle exec rspec

# Run specific spec file
bundle exec rspec spec/models/user_spec.rb

# Run specific example by line number
bundle exec rspec spec/models/user_spec.rb:42
```

## Configuration

Configure RSpec Rails behavior in rails_helper.rb

```ruby
# spec/rails_helper.rb
require 'spec_helper'
ENV['RAILS_ENV'] ||= 'test'
require_relative '../config/environment'
abort("The Rails environment is running in production mode!") if Rails.env.production?
require 'rspec/rails'

RSpec.configure do |config|
  # Use transactional fixtures for database cleanup
  config.use_transactional_fixtures = true

  # Set fixture path
  config.fixture_paths = [Rails.root.join('spec/fixtures')]

  # Automatically infer spec type from file location
  # spec/models -> type: :model, spec/controllers -> type: :controller
  config.infer_spec_type_from_file_location!

  # Filter Rails framework from backtraces
  config.filter_rails_from_backtrace!

  # Filter specific gems from backtraces
  config.filter_gems_from_backtrace("factory_bot", "database_cleaner")

  # Disable ActiveRecord (for API-only apps)
  # config.use_active_record = false
end
```

## Model Specs

Test ActiveRecord models with validations and business logic

```ruby
# spec/models/user_spec.rb
require 'rails_helper'

RSpec.describe User, type: :model do
  describe 'validations' do
    it 'validates presence of email' do
      user = User.new(email: nil)
      expect(user).not_to be_valid
      expect(user.errors[:email]).to include("can't be blank")
    end

    it 'validates uniqueness of email' do
      User.create!(email: 'test@example.com', name: 'John')
      duplicate = User.new(email: 'test@example.com', name: 'Jane')
      expect(duplicate).not_to be_valid
      expect(duplicate.errors[:email]).to include('has already been taken')
    end

    it 'is valid with all required attributes' do
      user = User.new(email: 'user@example.com', name: 'John Doe')
      expect(user).to be_valid
    end
  end

  describe 'associations' do
    it 'has many posts' do
      user = User.create!(email: 'user@example.com', name: 'John')
      post1 = user.posts.create!(title: 'First Post', body: 'Content')
      post2 = user.posts.create!(title: 'Second Post', body: 'More content')
      expect(user.posts).to match_array([post1, post2])
    end
  end

  describe '#full_name' do
    it 'returns first and last name combined' do
      user = User.new(first_name: 'John', last_name: 'Doe')
      expect(user.full_name).to eq('John Doe')
    end
  end
end
```

## Request Specs

Test HTTP endpoints from a client perspective

```ruby
# spec/requests/posts_spec.rb
require 'rails_helper'

RSpec.describe 'Posts API', type: :request do
  describe 'GET /posts' do
    it 'returns all posts as JSON' do
      Post.create!(title: 'First', body: 'Content 1')
      Post.create!(title: 'Second', body: 'Content 2')

      get '/posts', headers: { 'Accept' => 'application/json' }

      expect(response).to have_http_status(:ok)
      expect(response.content_type).to match(a_string_including('application/json'))

      json = JSON.parse(response.body)
      expect(json.length).to eq(2)
      expect(json[0]['title']).to eq('First')
    end
  end

  describe 'POST /posts' do
    it 'creates a new post with valid parameters' do
      post_params = { post: { title: 'New Post', body: 'Content' } }

      expect {
        post '/posts', params: post_params
      }.to change(Post, :count).by(1)

      expect(response).to have_http_status(:created)
      expect(response).to redirect_to(post_path(Post.last))
    end

    it 'returns unprocessable entity with invalid parameters' do
      post '/posts', params: { post: { title: '' } }

      expect(response).to have_http_status(:unprocessable_entity)
    end
  end

  describe 'GET /posts/:id' do
    it 'returns a specific post' do
      post = Post.create!(title: 'Test', body: 'Content')

      get "/posts/#{post.id}"

      expect(response).to have_http_status(:success)
      expect(response.body).to include('Test')
    end

    it 'returns not found for non-existent post' do
      get '/posts/99999'
      expect(response).to have_http_status(:not_found)
    end
  end
end
```

## Controller Specs

Test controller actions and their effects

```ruby
# spec/controllers/posts_controller_spec.rb
require 'rails_helper'

RSpec.describe PostsController, type: :controller do
  describe 'GET #index' do
    it 'assigns all posts to @posts' do
      post1 = Post.create!(title: 'First', body: 'Content')
      post2 = Post.create!(title: 'Second', body: 'Content')

      get :index

      expect(assigns(:posts)).to match_array([post1, post2])
      expect(response).to have_http_status(:success)
      expect(response).to render_template('index')
    end
  end

  describe 'GET #show' do
    it 'assigns the requested post to @post' do
      post = Post.create!(title: 'Test', body: 'Content')

      get :show, params: { id: post.id }

      expect(assigns(:post)).to eq(post)
    end
  end

  describe 'POST #create' do
    context 'with valid parameters' do
      it 'creates a new post' do
        expect {
          post :create, params: { post: { title: 'New', body: 'Content' } }
        }.to change(Post, :count).by(1)
      end

      it 'redirects to the created post' do
        post :create, params: { post: { title: 'New', body: 'Content' } }
        expect(response).to redirect_to(post_path(Post.last))
      end
    end

    context 'with invalid parameters' do
      it 'does not create a new post' do
        expect {
          post :create, params: { post: { title: '' } }
        }.not_to change(Post, :count)
      end

      it 'renders the new template' do
        post :create, params: { post: { title: '' } }
        expect(response).to render_template('new')
      end
    end
  end

  describe 'testing anonymous controllers' do
    controller(ApplicationController) do
      def custom_action
        raise StandardError, 'Error occurred'
      end
    end

    it 'handles exceptions' do
      routes.draw { get 'custom_action' => 'anonymous#custom_action' }

      expect {
        bypass_rescue
        get :custom_action
      }.to raise_error(StandardError, 'Error occurred')
    end
  end
end
```

## System Specs

Test complete user workflows with browser automation

```ruby
# spec/system/user_authentication_spec.rb
require 'rails_helper'

RSpec.describe 'User Authentication', type: :system do
  before do
    driven_by(:selenium_chrome_headless)
  end

  it 'allows a user to sign up and log in' do
    visit root_path

    click_link 'Sign Up'

    fill_in 'Email', with: 'user@example.com'
    fill_in 'Password', with: 'password123'
    fill_in 'Password confirmation', with: 'password123'

    expect {
      click_button 'Create Account'
    }.to change(User, :count).by(1)

    expect(page).to have_content('Welcome!')
    expect(page).to have_current_path(dashboard_path)
  end

  it 'prevents login with invalid credentials' do
    User.create!(email: 'user@example.com', password: 'correct_password')

    visit login_path

    fill_in 'Email', with: 'user@example.com'
    fill_in 'Password', with: 'wrong_password'
    click_button 'Log In'

    expect(page).to have_content('Invalid email or password')
    expect(page).to have_current_path(login_path)
  end

  it 'allows user to create a post after logging in', js: true do
    user = User.create!(email: 'user@example.com', password: 'password123')

    login_as(user)

    visit new_post_path

    fill_in 'Title', with: 'My First Post'
    fill_in 'Body', with: 'This is the content of my post'

    click_button 'Publish'

    expect(page).to have_content('Post was successfully created')
    expect(page).to have_content('My First Post')
  end
end
```

## Feature Specs

Alternative to system specs for end-to-end testing

```ruby
# spec/features/shopping_cart_spec.rb
require 'rails_helper'

RSpec.feature 'Shopping Cart', type: :feature do
  scenario 'user adds items to cart and checks out' do
    product1 = Product.create!(name: 'Widget', price: 10.00)
    product2 = Product.create!(name: 'Gadget', price: 25.00)

    visit products_path

    within("#product_#{product1.id}") do
      click_button 'Add to Cart'
    end

    within("#product_#{product2.id}") do
      click_button 'Add to Cart'
    end

    click_link 'Cart'

    expect(page).to have_content('Widget')
    expect(page).to have_content('Gadget')
    expect(page).to have_content('Total: $35.00')

    click_button 'Checkout'

    fill_in 'Name', with: 'John Doe'
    fill_in 'Email', with: 'john@example.com'
    fill_in 'Card Number', with: '4242424242424242'

    click_button 'Complete Purchase'

    expect(page).to have_content('Order complete!')
  end
end
```

## Mailer Specs

Test email delivery and content

```ruby
# spec/mailers/user_mailer_spec.rb
require 'rails_helper'

RSpec.describe UserMailer, type: :mailer do
  describe 'welcome_email' do
    let(:user) { User.create!(email: 'user@example.com', name: 'John') }
    let(:mail) { UserMailer.welcome_email(user) }

    it 'renders the headers' do
      expect(mail.subject).to eq('Welcome to My App')
      expect(mail.to).to eq(['user@example.com'])
      expect(mail.from).to eq(['noreply@myapp.com'])
    end

    it 'renders the body' do
      expect(mail.body.encoded).to match('Welcome John')
      expect(mail.body.encoded).to include('Thanks for signing up')
    end

    it 'sends the email' do
      expect {
        mail.deliver_now
      }.to change { ActionMailer::Base.deliveries.count }.by(1)
    end
  end

  describe 'password_reset' do
    it 'includes reset token in email' do
      user = User.create!(email: 'user@example.com', reset_token: 'abc123')
      mail = UserMailer.password_reset(user)

      expect(mail.body.encoded).to include('abc123')
      expect(mail.body.encoded).to include(reset_password_url(token: 'abc123'))
    end
  end
end
```

## Job Specs

Test ActiveJob background jobs

```ruby
# spec/jobs/process_payment_job_spec.rb
require 'rails_helper'

RSpec.describe ProcessPaymentJob, type: :job do
  describe '#perform' do
    it 'processes payment for order' do
      order = Order.create!(total: 100.00, status: 'pending')

      expect {
        ProcessPaymentJob.perform_now(order.id)
      }.to change { order.reload.status }.from('pending').to('paid')
    end

    it 'enqueues the job' do
      order = Order.create!(total: 100.00)

      expect {
        ProcessPaymentJob.perform_later(order.id)
      }.to have_enqueued_job(ProcessPaymentJob).with(order.id)
    end

    it 'enqueues with specific queue and delay' do
      ActiveJob::Base.queue_adapter = :test

      expect {
        ProcessPaymentJob.set(queue: :critical, wait: 5.minutes).perform_later(123)
      }.to have_enqueued_job(ProcessPaymentJob)
        .with(123)
        .on_queue('critical')
        .at(5.minutes.from_now)
    end
  end

  describe 'job execution tracking' do
    it 'tracks that job was enqueued and performed' do
      order = Order.create!(total: 50.00)

      expect {
        ProcessPaymentJob.perform_later(order.id)
      }.to have_enqueued_job

      expect {
        perform_enqueued_jobs
      }.to change { order.reload.status }
    end
  end
end
```

## Routing Specs

Test route definitions and URL generation

```ruby
# spec/routing/posts_routing_spec.rb
require 'rails_helper'

RSpec.describe 'Posts routing', type: :routing do
  it 'routes GET /posts to posts#index' do
    expect(get: '/posts').to route_to('posts#index')
  end

  it 'routes POST /posts to posts#create' do
    expect(post: '/posts').to route_to('posts#create')
  end

  it 'routes GET /posts/:id to posts#show' do
    expect(get: '/posts/1').to route_to('posts#show', id: '1')
  end

  it 'routes PUT /posts/:id to posts#update' do
    expect(put: '/posts/1').to route_to('posts#update', id: '1')
  end

  it 'does not route to unknown action' do
    expect(get: '/posts/archive').not_to be_routable
  end

  it 'routes nested resources' do
    expect(get: '/posts/1/comments/2')
      .to route_to('comments#show', post_id: '1', id: '2')
  end

  it 'generates correct path' do
    expect(post_path(1)).to eq('/posts/1')
    expect(posts_path).to eq('/posts')
  end
end
```

## View Specs

Test view templates in isolation

```ruby
# spec/views/posts/show.html.erb_spec.rb
require 'rails_helper'

RSpec.describe 'posts/show', type: :view do
  it 'displays post title and body' do
    post = assign(:post, Post.new(
      title: 'Test Title',
      body: 'Test body content',
      author: 'John Doe'
    ))

    render

    expect(rendered).to match(/Test Title/)
    expect(rendered).to match(/Test body content/)
    expect(rendered).to match(/John Doe/)
  end

  it 'shows edit link when user is author' do
    user = User.create!(email: 'user@example.com')
    post = assign(:post, Post.create!(title: 'Test', user: user))
    assign(:current_user, user)

    render

    expect(rendered).to have_link('Edit', href: edit_post_path(post))
  end

  it 'renders partial for comments' do
    post = assign(:post, Post.create!(title: 'Test'))
    post.comments.create!(body: 'Great post!', author: 'Jane')

    render

    expect(view).to render_template(partial: '_comment')
    expect(rendered).to match(/Great post!/)
  end
end
```

## Helper Specs

Test view helper methods

```ruby
# spec/helpers/application_helper_spec.rb
require 'rails_helper'

RSpec.describe ApplicationHelper, type: :helper do
  describe '#format_date' do
    it 'formats date in readable format' do
      date = Date.new(2024, 1, 15)
      expect(helper.format_date(date)).to eq('January 15, 2024')
    end

    it 'returns empty string for nil date' do
      expect(helper.format_date(nil)).to eq('')
    end
  end

  describe '#user_avatar' do
    it 'returns image tag with avatar URL' do
      user = User.new(avatar_url: 'http://example.com/avatar.jpg')
      result = helper.user_avatar(user)

      expect(result).to have_css('img[src="http://example.com/avatar.jpg"]')
    end

    it 'returns default avatar when user has none' do
      user = User.new(avatar_url: nil)
      result = helper.user_avatar(user)

      expect(result).to include('default-avatar.png')
    end
  end
end
```

## Custom Matchers

Use Rails-specific matchers for cleaner specs

```ruby
# Using have_http_status matcher
expect(response).to have_http_status(:ok)
expect(response).to have_http_status(200)
expect(response).to have_http_status(:success)  # Any 2xx status
expect(response).to have_http_status(:error)    # Any 5xx status
expect(response).to have_http_status(:redirect) # Any 3xx status
expect(response).to have_http_status(:missing)  # 404

# Using redirect_to matcher
expect(response).to redirect_to(root_path)
expect(response).to redirect_to(action: 'index')
expect(response).to redirect_to('http://example.com')

# Using render_template matcher
expect(response).to render_template('index')
expect(response).to render_template('posts/show')
expect(response).to render_template(partial: '_form')
expect(response).to render_template(layout: 'application')

# Using be_valid matcher
user = User.new(email: 'test@example.com')
expect(user).to be_valid
expect(user).not_to be_valid

# Using be_a_new matcher
post = Post.new(title: 'Test')
expect(post).to be_a_new(Post)
expect(post).to be_a_new(Post).with(title: 'Test')

# Using match_array for ActiveRecord relations
user = User.create!(email: 'test@example.com')
post1 = user.posts.create!(title: 'First')
post2 = user.posts.create!(title: 'Second')
expect(user.posts).to match_array([post1, post2])

# Using job matchers
expect {
  ProcessPaymentJob.perform_later(order_id)
}.to have_enqueued_job(ProcessPaymentJob).with(order_id)

expect {
  UserMailer.welcome_email(user).deliver_later
}.to have_enqueued_mail(UserMailer, :welcome_email).with(user)
```

## Generators

Generate spec files using Rails generators

```bash
# Generate model with spec
rails generate model User email:string name:string
# Creates: spec/models/user_spec.rb

# Generate controller with specs
rails generate controller Posts index show create
# Creates: spec/controllers/posts_controller_spec.rb
#          spec/requests/posts_spec.rb
#          spec/routing/posts_routing_spec.rb
#          spec/views/posts/index.html.erb_spec.rb

# Generate specific spec types
rails generate rspec:model User
rails generate rspec:controller Posts
rails generate rspec:request Posts
rails generate rspec:feature UserLogin
rails generate rspec:system Shopping
rails generate rspec:mailer UserMailer
rails generate rspec:job ProcessPayment
rails generate rspec:helper Application

# List all RSpec generators
rails generate --help | grep rspec
```

## Summary

RSpec Rails transforms Rails testing by providing a comprehensive BDD framework that makes specs readable, maintainable, and expressive. The primary use cases include writing model specs for business logic validation, request specs for API testing, system specs for end-to-end user workflows, and controller specs for testing application flow. Job specs verify background processing, mailer specs ensure correct email delivery, and routing specs validate URL structure. The framework excels at testing Rails applications of any size, from small APIs to large monoliths with complex user interactions.

Integration with Rails is seamless through automatic generator hooks, transactional fixtures for database cleanup, and Rails-aware matchers that understand HTTP status codes, redirects, and template rendering. The configuration system allows fine-tuning of test behavior including fixture management, database strategies, and metadata-driven spec types. RSpec Rails supports testing engines, API-only applications, and traditional full-stack Rails apps equally well, making it the standard choice for Rails testing in the Ruby community. Combined with tools like FactoryBot for test data and Capybara for browser automation, it provides a complete testing solution.
