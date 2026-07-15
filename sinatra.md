### Starting a Modular Sinatra App with run!

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to start a modular Sinatra application directly by using the `run!` method, typically guarded by `if app_file == $0`. This allows the application to be run as a standalone server.

```ruby
# my_app.rb
require 'sinatra/base

class MyApp < Sinatra::Base
  # ... app code here ...

  # start the server if ruby file executed directly
  run! if app_file == $0
end
```

--------------------------------

### Installing Sinatra and Dependencies

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Installs the necessary gems for running a Sinatra application, including Sinatra itself, rackup, and the Puma web server.

```shell
gem install sinatra rackup puma
```

--------------------------------

### Install Sinatra Pre-release Gems

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Provides instructions on how to install pre-release versions of the Sinatra gem using the `gem install` command, allowing users to access the latest features before official releases.

```shell
gem install sinatra --pre
```

--------------------------------

### Sinatra Testing with Rack::Test

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to write tests for Sinatra applications using the Rack::Test library. It includes examples for basic GET requests, requests with parameters, and requests with custom headers.

```ruby
require 'my_sinatra_app'
require 'minitest/autorun'
require 'rack/test'

class MyAppTest < Minitest::Test
  include Rack::Test::Methods

  def app
    Sinatra::Application
  end

  def test_my_default
    get '/'
    assert_equal 'Hello World!', last_response.body
  end

  def test_with_params
    get '/meet', :name => 'Frank'
    assert_equal 'Hello Frank!', last_response.body
  end

  def test_with_user_agent
    get '/', {}, 'HTTP_USER_AGENT' => 'Songbird'
    assert_equal "You're using Songbird!", last_response.body
  end
end
```

--------------------------------

### Basic Sinatra Application

Source: https://github.com/sinatra/sinatra/blob/main/README.md

A simple 'Hello World' application using Sinatra. Requires the Sinatra gem to be installed.

```ruby
require 'sinatra'

get '/' do
  'Hello world!'
end
```

--------------------------------

### Installing Pre-release Sinatra Gem

Source: https://github.com/sinatra/sinatra/blob/main/README.md

This command shows how to install the latest pre-release version of the Sinatra gem, allowing users to test the bleeding-edge code.

```shell
gem install sinatra --pre
```

--------------------------------

### Application Scope Example

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to define and access options within the application scope in Sinatra. The `set` method is used to define options, which are then accessible as methods at the class level. The example contrasts this with the request scope where `request` and `session` objects are available.

```ruby
class MyApp < Sinatra::Base
  # Hey, I'm in the application scope!
  set :foo, 42
  foo # => 42

  get '/foo' do
    # Hey, I'm no longer in the application scope!
  end
end
```

--------------------------------

### Running a Sinatra Application

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Starts a Sinatra application using the Ruby interpreter. The application will be accessible via a local web server.

```shell
ruby myapp.rb
```

--------------------------------

### Using Classic Style Sinatra App with config.ru

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates how to deploy a classic style Sinatra application using a `config.ru` file. This setup directs the `rackup` command to run the top-level Sinatra application.

```ruby
# app.rb
require 'sinatra'

get '/' do
  'Hello world!'
end

# config.ru
require './app'
run Sinatra::Application
```

--------------------------------

### Using Sinatra with Bundler (Gemfile)

Source: https://github.com/sinatra/sinatra/blob/main/README.md

This code demonstrates how to specify Sinatra and its dependencies in a Gemfile for use with Bundler. It shows how to install Bundler, create a Gemfile, and run an application using `bundle exec`.

```ruby
gem install bundler

source 'https://rubygems.org'
gem 'sinatra', :github => 'sinatra/sinatra'

# other dependencies
gem 'haml'                    # for instance, if you use haml
```

```shell
bundle exec ruby myapp.rb
```

--------------------------------

### Yajl Template Example

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to use Yajl templates in Sinatra, including passing local variables and using callbacks for rendering.

```ruby
yajl :index,
     :locals => { :key => 'qux' },
     :callback => 'present',
     :variable => 'resource'
```

--------------------------------

### Sinatra as Middleware Example

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to use one Sinatra application (LoginScreen) as middleware for another (MyApp). The middleware runs before filters, controlling access based on session data.

```Ruby
require 'sinatra/base

class LoginScreen < Sinatra::Base
  enable :sessions

  get('/login') { haml :login }

  post('/login') do
    if params['name'] == 'admin' && params['password'] == 'admin'
      session['user_name'] = params['name']
    else
      redirect '/login'
    end
  end
end

class MyApp < Sinatra::Base
  # middleware will run before filters
  use LoginScreen

  before do
    unless session['user_name']
      halt "Access denied, please <a href='/login'>login</a>."
    end
  end

  get('/') { "Hello #{session['user_name']}." }
end
```

--------------------------------

### Sinatra::Base for Modular Applications

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates how to define a Sinatra application using Sinatra::Base, which is recommended for reusable components like middleware or libraries. This example shows setting options and defining a basic route.

```ruby
require 'sinatra/base

class MyApp < Sinatra::Base
  set :sessions, true
  set :foo, 'bar'

  get '/' do
    'Hello world!'
  end
end
```

--------------------------------

### Install Sinatra::Contrib from Git

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/README.md

Illustrates how to add the Sinatra::Contrib gem directly from a Git repository, including specifying other gems from the same repository.

```ruby
github 'sinatra/sinatra' do
  gem 'sinatra-contrib'
end
```

--------------------------------

### Request Scope Example

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates accessing the application scope (`settings`) from within the request scope in Sinatra. The example defines a route that dynamically defines another route. It shows how instance variables (`@value`) are not shared between requests, highlighting the difference between application and request scopes.

```ruby
class MyApp < Sinatra::Base
  # Hey, I'm in the application scope!
  get '/define_route/:name' do
    # Request scope for '/define_route/:name'
    @value = 42

    settings.get("/#{params['name']}") do
      # Request scope for "/#{params['name']}"
      @value # => nil (not the same request)
    end

    "Route defined!"
  end
end
```

--------------------------------

### Integrating Rack-Cache with Sinatra

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to integrate the `rack-cache` gem with Sinatra for reverse-proxy caching. This example demonstrates setting cache control and simulating a delayed response.

```ruby
require "rack/cache"
require "sinatra"

use Rack::Cache

get '/' do
  cache_control :public, :max_age => 36000
  sleep 5
  "hello"
end
```

--------------------------------

### Using Sinatra as Middleware

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to use one Sinatra application as middleware for another. This involves defining separate Sinatra::Base subclasses and using the `use` keyword to stack them. The example shows a `LoginScreen` middleware that checks user credentials before allowing access to the main application.

```ruby
require 'sinatra/base'

class LoginScreen < Sinatra::Base
  enable :sessions

  get('/login') { haml :login }

  post('/login') do
    if params['name'] == 'admin' && params['password'] == 'admin'
      session['user_name'] = params['name']
    else
      redirect '/login'
    end
  end
end

class MyApp < Sinatra::Base
  # middleware will run before filters
  use LoginScreen

  before do
    unless session['user_name']
      halt "Access denied, please <a href='/login'>login</a>."
    end
  end

  get('/') { "Hello #{session['user_name']}." }
end
```

--------------------------------

### Rack::Protection Instrumentation

Source: https://github.com/sinatra/sinatra/blob/main/rack-protection/README.md

This example demonstrates how to enable instrumentation for Rack::Protection by passing an instrumenter, like ActiveSupport::Notifications. It explains how the instrumenter receives namespace and environment details for monitoring.

```ruby
use Rack::Protection, instrumenter: ActiveSupport::Notifications
```

--------------------------------

### Yajl Callback Example

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates the JavaScript code that handles the data processed by a Yajl template with a callback.

```javascript
var resource = {"foo":"bar","baz":"qux"};
present(resource);
```

--------------------------------

### Package and Install Sinatra Gems Locally

Source: https://github.com/sinatra/sinatra/blob/main/RELEASING.md

Packages all specified Sinatra gems and installs them locally on the system.

```sh
# Build and install sinatra-contrib gem locally
$ bundle exec rake install:sinatra-contrib

# Build and install rack-protection gem locally
$ bundle exec rake install:rack-protection

# Build and install sinatra gem locally
$ bundle exec rake install:sinatra

# Build and install all gems locally
$ bundle exec rake install:all
```

--------------------------------

### Sinatra Before Filter Example

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates a 'before' filter that modifies instance variables and the request path before a route is executed. Instance variables set in filters are accessible by routes.

```ruby
before do
  @note = 'Hi!'
  request.path_info = '/foo/bar/baz'
end

get '/foo/*' do
  @note #=> 'Hi!'
  params['splat'] #=> 'bar/baz'
end
```

--------------------------------

### Conditional Layout Rendering

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows an example of conditionally rendering a layout based on a request condition, such as an AJAX request.

```ruby
erb :index, :layout => !request.xhr?
```

--------------------------------

### Sinatra Lifecycle Events

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Defines callbacks for server startup and shutdown events. These callbacks are executed when Sinatra starts or stops the web server. They are only functional when Sinatra itself is initiating the server process.

```ruby
on_start do
  puts "===== Booting up ====="
end

on_stop do
  puts "===== Shutting down ====="
end
```

--------------------------------

### Custom Template Lookup

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Provides an example of implementing a custom `#find_template` method to control how Sinatra locates templates.

```ruby
configure do
  set :views, [ './views/a', './views/b' ]
end

def find_template(views, name, engine, &block)
  Array(views).each do |v|
    super(v, name, engine, &block)
  end
end
```

--------------------------------

### Skipping a Specific Protection

Source: https://github.com/sinatra/sinatra/blob/main/rack-protection/README.md

This example shows how to exclude a particular protection middleware, such as 'path_traversal', when initializing Rack::Protection. This allows for granular control over the applied security measures.

```ruby
require 'rack/protection'
use Rack::Protection, :except => :path_traversal
run MyApp
```

--------------------------------

### Customizing Template File Lookup

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Provides examples of how to customize the `find_template` helper in Sinatra to manage template file locations, including using multiple view directories or different directories for different template engines.

```ruby
find_template settings.views, 'foo', Tilt[:haml] do |file|
  puts "could be #{file}"
end

# Using multiple view directories
set :views, ['views', 'templates']
helpers do
  def find_template(views, name, engine, &block)
    Array(views).each { |v| super(v, name, engine, &block) }
  end
end

# Using different directories for different engines
set :views, :haml => 'templates', :default => 'views'
helpers do
  def find_template(views, name, engine, &block)
    _, folder = views.detect { |k,v| engine == Tilt[k] }
    folder ||= views[:default]
    super(folder, name, engine, &block)
  end
end
```

--------------------------------

### Setting Cache Control Headers in Sinatra

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to set Cache-Control headers for HTTP caching in Sinatra routes and filters. Includes examples for basic caching, revalidation, and setting max age.

```ruby
get '/' do
  cache_control :public
  "cache it!"
end
```

```ruby
before do
  cache_control :public, :must_revalidate, :max_age => 60
end
```

```ruby
before do
  expires 500, :public, :must_revalidate
end
```

--------------------------------

### Sinatra HTTP Methods

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Defines routes for different HTTP methods (GET, POST, PUT, PATCH, DELETE, OPTIONS, LINK, UNLINK) in Sinatra. Each route is associated with a block that handles the request.

```ruby
get '/' do
  .. show something ..
end

post '/' do
  .. create something ..
end

put '/' do
  .. replace something ..
end

patch '/' do
  .. modify something ..
end

delete '/' do
  .. annihilate something ..
end

options '/' do
  .. appease something ..
end

link '/' do
  .. affiliate something ..
end

unlink '/' do
  .. separate something ..
end
```

--------------------------------

### Finding Tasks and Contributing

Source: https://github.com/sinatra/sinatra/blob/main/CONTRIBUTING.md

This section guides contributors on how to find tasks to work on within the Sinatra project. It highlights specific GitHub issue labels like 'Help Wanted', 'Good First Issue', and 'Wishlist' to help contributors find suitable tasks.

```Markdown
## Looking for something to do?

If you'd like to help out but aren't sure how, pick something that looks
interesting from the [issues][ghi] list and hack on. Make sure to leave a
comment on the ticket noting that you're investigating (a simple "Taking…" is
fine).

* ["Help Wanted"](https://github.com/sinatra/sinatra/labels/help%20wanted):  Anyone willing to pitch in is open to contribute to this ticket as they see fit (will try to add context / summarize or ask for requirements)

* ["Good First Issue"](https://github.com/sinatra/sinatra/labels/good%20first%20issue): Potential first time contributors should start here

* ["Wishlist"](https://github.com/sinatra/sinatra/labels/Wishlist): All the things I wish we had but have no time for
```

--------------------------------

### Sinatra After Filter Example

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates an 'after' filter that executes after a request and can access response status. Note that the response body might not be available in 'after' filters if not explicitly handled.

```ruby
after do
  puts response.status
end
```

--------------------------------

### Sinatra Custom Route Matchers

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Explains how to define custom route matching logic in Sinatra by creating classes that implement `to_pattern` and `params` methods. It provides an example of a matcher that excludes a specific path.

```ruby
class AllButPattern
  def initialize(except)
    @except = except
  end

  def to_pattern(options)
    return self
  end

  def params(route)
    return {} unless @except === route
  end
end

def all_but(pattern)
  AllButPattern.new(pattern)
end

get all_but("/index") do
  # ...
end
```

```ruby
get /.*/ do
  pass if request.path_info == "/index"
  # ...
end
```

--------------------------------

### Sinatra Halting Requests

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates how to immediately stop request processing in Sinatra filters or routes using the `halt` method. It shows examples of halting with no arguments, a status code, a body, or both, including custom headers.

```ruby
halt
```

```ruby
halt 410
```

```ruby
halt 'this will be the body'
```

```ruby
halt 401, 'go away!'
```

```ruby
halt 402, {'Content-Type' => 'text/plain'}, 'revenge'
```

```ruby
halt erb(:error)
```

--------------------------------

### Sinatra Calling Another Route

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to trigger and get the result of another route in Sinatra using the `call` or `call!` methods. `call` sends the request to a new environment, while `call!` sends it to the same application instance.

```ruby
get '/foo' do
  status, headers, body = call env.merge("PATH_INFO" => '/bar')
  [status, headers, body.map(&:upcase)]
end

get '/bar' do
  "bar"
end
```

--------------------------------

### Dynamic Application Creation with Sinatra.new

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to create new Sinatra applications at runtime using Sinatra.new. This is useful for testing extensions or embedding Sinatra within libraries.

```Ruby
require 'sinatra/base
my_app = Sinatra.new { get('/') { "hi" } }
my_app.run!
```

--------------------------------

### Dynamic App Creation with Inheritance and Mapping

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates dynamic application creation using Sinatra.new with an inherited controller configuration. This pattern is useful for routing different paths to distinct Sinatra applications, often used with Rackup.

```Ruby
# config.ru (run with rackup)
require 'sinatra/base

controller = Sinatra.new do
  enable :logging
  helpers MyHelpers
end

map('/a') do
  run Sinatra.new(controller) { get('/') { 'a' } }
end

map('/b') do
  run Sinatra.new(controller) { get('/') { 'b' } }
end
```

--------------------------------

### Configuring a Modular Sinatra App with config.ru

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to configure and run a modular Sinatra application using a `config.ru` file. This approach allows leveraging any Rack-compatible server for deployment.

```ruby
# config.ru (run with rackup)
require './my_app'
run MyApp
```

--------------------------------

### Dynamic Application Creation with Sinatra.new

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates how to create Sinatra applications dynamically at runtime using `Sinatra.new`. This method can be used to create new application instances without assigning them to a constant, and it accepts an optional argument to specify a parent application class for inheritance. This is useful for testing extensions or integrating Sinatra into libraries.

```ruby
require 'sinatra/base'
my_app = Sinatra.new { get('/') { "hi" } }
my_app.run!
```

```ruby
# config.ru (run with rackup)
require 'sinatra/base

controller = Sinatra.new do
  enable :logging
  helpers MyHelpers
end

map('/a') do
  run Sinatra.new(controller) { get('/') { 'a' } }
end

map('/b') do
  run Sinatra.new(controller) { get('/') { 'b' } }
end
```

```ruby
require 'sinatra/base

use Sinatra do
  get('/') { ... }
end

run RailsProject::Application
```

--------------------------------

### Sinatra Command Line Options

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Details the command-line arguments available when running a Sinatra application directly. It outlines options for help, port, host, environment, server handler, quiet mode, and mutex locking.

```APIDOC
ruby myapp.rb [-h] [-x] [-q] [-e ENVIRONMENT] [-p PORT] [-o HOST] [-s HANDLER]

Options are:
-h # help
-p # set the port (default is 4567)
-o # set the host (default is 0.0.0.0)
-e # set the environment (default is development)
-s # specify rack server/handler (default is puma)
-q # turn on quiet mode for server (default is off)
-x # turn on the mutex lock (default is off)
```

--------------------------------

### Environment-Specific Sinatra Configurations

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to apply configurations based on the application's environment. Configurations can be run for specific environments (e.g., :production) or multiple environments (e.g., :production, :test).

```ruby
configure :production do
  ...
end

configure :production, :test do
  ...
end
```

--------------------------------

### Integrating Rack Middleware in Sinatra

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to use the `use` method in Sinatra to integrate Rack middleware, such as `Rack::Lint` or custom middleware, into the application's request/response pipeline. It also shows how to use blocks with `use` for configuration.

```ruby
require 'sinatra'
require 'my_custom_middleware'

use Rack::Lint
use MyCustomMiddleware

get '/hello' do
  'Hello World'
end

use Rack::Auth::Basic do |username, password|
  username == 'admin' && password == 'secret'
end
```

--------------------------------

### Sinatra::Application for Modular Style

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to subclass Sinatra::Application, which provides behavior similar to the classic style but within a modular framework. This is useful when you need multiple Sinatra applications in a single process.

```ruby
require 'sinatra/base

class MyApp < Sinatra::Application
  get '/' do
    'Hello world!'
  end
end
```

--------------------------------

### Rendering Haml Templates with Options

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates rendering a Haml template and passing engine-specific options, such as `:format => :html5`. Options passed directly to the render method override those set globally.

```ruby
get '/' do
  haml :index, :format => :html5
end
```

--------------------------------

### Sinatra Configuration Options

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Provides an overview of Sinatra's configuration options related to static file serving, including setting the public folder, cache control, and custom headers.

```APIDOC
Sinatra Configuration Options:

set :public_folder, path
  - Sets the directory for serving static files.
  - Default: './public'

set :static_cache_control, options
  - Adds Cache-Control headers to static files.
  - Example: `set :static_cache_control, { max_age: 3600 }`

set :static_headers, headers_hash
  - Adds custom headers to all static file responses.
  - Example: `set :static_headers, { 'X-Custom-Header' => 'value' }`
```

--------------------------------

### Registering Custom Template Engine

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Explains how to register a custom template engine with Tilt and create a corresponding rendering method in Sinatra.

```ruby
Tilt.register MyAwesomeTemplateEngine, :myat

helpers do
  def myat(*args)
    render(:myat, *args)
  end
end

get '/' do
  myat :index
end
```

--------------------------------

### Customizing Layout Options

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates how to pass specific options to the layout rendering process, such as specifying a different directory for layout files.

```ruby
set :rdoc, :layout_options => { :views => 'views/layouts' }
```

--------------------------------

### Sinatra Configuration Options

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to set and access configuration options within a Sinatra application. This includes setting single or multiple options, enabling/disabling features, and using blocks for dynamic settings. Options can be accessed via the `settings` object.

```ruby
configure do
  # setting one option
  set :option, 'value'

  # setting multiple options
  set :a => 1, :b => 2

  # same as `set :option, true`
  enable :option

  # same as `set :option, false`
  disable :option

  # you can also have dynamic settings with blocks
  set(:css_dir) { File.join(views, 'css') }
end

configure do
  set :foo, 'bar'
end

get '/' do
  settings.foo? # => true
  settings.foo  # => 'bar'
  ...
end
```

--------------------------------

### Specifying Layout Engine

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to specify a different template engine for rendering the layout, which is useful for languages that don't natively support layouts.

```ruby
set :rdoc, :layout_engine => :erb
```

--------------------------------

### Basic Rack::Protection Usage

Source: https://github.com/sinatra/sinatra/blob/main/rack-protection/README.md

This snippet demonstrates the basic usage of Rack::Protection middleware in a Rack application's configuration file (config.ru). It includes the gem and applies all protections.

```ruby
require 'rack/protection'
use Rack::Protection
run MyApp
```

--------------------------------

### Associating File Extensions with Tilt

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to register a file extension with a specific Tilt template engine.

```ruby
Tilt.register Tilt[:haml], :tt
```

--------------------------------

### Sending Files with Sinatra's send_file Helper

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates the usage of the `send_file` helper in Sinatra to serve file contents as responses. Covers basic usage, options for content type, disposition, and status codes.

```ruby
get '/' do
  send_file 'foo.png'
end
```

```ruby
send_file 'foo.png', :type => :jpg
```

--------------------------------

### Sinatra Conditions: Host Name and Provides

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates using `host_name` and `provides` conditions to route requests based on the request's host or the `Accept` header, respectively. `provides` can match single or multiple content types.

```ruby
get '/', :host_name => /^admin\./ do
  "Admin Area, Access denied!"
end

get '/', :provides => 'html' do
  haml :index
end

get '/', :provides => ['rss', 'atom', 'xml'] do
  builder :feed
end
```

--------------------------------

### Sinatra as Middleware in Rackup

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates embedding a Sinatra application directly as middleware within a Rackup configuration, preceding another Rack-based application like Rails.

```Ruby
require 'sinatra/base

use Sinatra do
  get('/') { ... }
end

run RailsProject::Application
```

--------------------------------

### Handling Conditional Requests with ETag

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Explains how to use the `etag` helper with options like `:new_resource` and `:kind` to manage conditional requests based on `If-Match` or `If-None-Match` headers.

```ruby
get '/create' do
  etag '', :new_resource => true
  Article.create
  erb :new_article
end
```

```ruby
etag '', :new_resource => true, :kind => :weak
```

--------------------------------

### Sinatra Environment Configuration

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to check the current application environment and how to set it using the APP_ENV environment variable. Sinatra has predefined environments: 'development', 'production', and 'test'.

```ruby
get '/' do
  if settings.development?
    "development!"
  else
    "not development!"
  end
end
```

```shell
APP_ENV=production ruby my_app.rb
```

--------------------------------

### Using Markdown Templates

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Explains how to use the Markdown template engine by requiring the necessary gem (`rdiscount`) and then calling the `markdown` rendering method.

```ruby
require 'rdiscount'
get('/') { markdown :index }
```

--------------------------------

### Sinatra Command Line Arguments

Source: https://github.com/sinatra/sinatra/blob/main/README.md

This snippet details the command-line options available when running a Sinatra application directly. It includes flags for help, port, host, environment, handler, quiet mode, and mutex lock.

```shell
ruby myapp.rb [-h] [-x] [-q] [-e ENVIRONMENT] [-p PORT] [-o HOST] [-s HANDLER]

Options are:

-h # help
-p # set the port (default is 4567)
-o # set the host (default is 0.0.0.0)
-e # set the environment (default is development)
-s # specify rack server/handler (default is puma)
-q # turn on quiet mode for server (default is off)
-x # turn on the mutex lock (default is off)
```

--------------------------------

### Sinatra Gemfile Configuration

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to configure a Bundler Gemfile to use the latest Sinatra from its GitHub repository, along with other project dependencies like Haml.

```ruby
source 'https://rubygems.org'
gem 'sinatra', :github => 'sinatra/sinatra'

# other dependencies
gem 'haml'                    # for instance, if you use haml
```

--------------------------------

### Sinatra Content-For Extension with Multiple Template Engines

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/ideas.md

This extension enhances `sinatra-content-for` to support various template engines including Liquid, Radius, Markaby, Nokogiri, and Builder. Integration with Liquid and Radius may require patching the Tilt library.

```ruby
# Extend `sinatra-content-for` to support Liquid, Radius, Markaby, Nokogiri and
# Builder. At least the first two probably involve patching Tilt.
```

--------------------------------

### Setting Global Template Options

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to set default options for a specific template engine globally using `set`. These options can be overridden by options passed directly to the rendering method.

```ruby
set :haml, :format => :html5

get '/' do
  haml :index
end
```

--------------------------------

### Generating URLs in Sinatra

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates the use of the `url` helper method for generating URLs, which correctly handles reverse proxies and Rack routers. It also mentions that `url` is aliased to `to`.

```ruby
%a{:href => url('/foo')} foo
```

--------------------------------

### Require Sinatra::Contrib Extensions (Classic Style)

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/README.md

Demonstrates how to require individual extensions or all common extensions for classic Sinatra applications.

```ruby
require 'sinatra'
require 'sinatra/content_for'

# Or for common extensions:
require 'sinatra'
require 'sinatra/contrib'
```

```ruby
require 'sinatra'
require 'sinatra/contrib/all'
```

--------------------------------

### Named Templates

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to define templates using the top-level `template` method and how layouts are applied.

```ruby
template :layout do
  "%html\n  =yield\n"
end

template :index do
  '%div.title Hello World!'
end

get '/' do
  haml :index
end
```

```ruby
get '/' do
  haml :index, :layout => !request.xhr?
end
```

--------------------------------

### Contributing to Sinatra Documentation and Website

Source: https://github.com/sinatra/sinatra/blob/main/CONTRIBUTING.md

This section outlines how to contribute to Sinatra's website, documentation, and book. It details the use of Git and GitHub for managing contributions and points to specific repositories for different aspects of the documentation.

```Markdown
## Want to write docs?

The process for contributing to Sinatra's website, documentation or the book
is the same as contributing code. We use Git for versions control and GitHub to
track patch requests.

* [The sinatra.github.com repo](http://github.com/sinatra/sinatra.github.com/)
  is where the website sources are managed. There are almost always people in
  `#sinatra` that are happy to discuss, apply, and publish website patches.

* [The Book](http://sinatra-org-book.herokuapp.com/) has its own [Git
  repository](http://github.com/sinatra/sinatra-book/) and build process but is
  managed the same as the website and project codebase.

* [Sinatra Recipes](http://recipes.sinatrarb.com/) is a community
  project where anyone is free to contribute ideas, recipes and tutorials. Which
  also has its own [Git repository](http://github.com/sinatra/sinatra-recipes).

* [The Introduction](http://www.sinatrarb.com/intro.html) is generated from
  Sinatra's [README file](http://github.com/sinatra/sinatra/blob/main/README.md).

* If you want to help translating the documentation, the README is already
  available in
  [Japanese](http://github.com/sinatra/sinatra/blob/main/README.ja.md),
  [German](http://github.com/sinatra/sinatra/blob/main/README.de.md),
  [Chinese](https://github.com/sinatra/sinatra/blob/main/README.zh.md),
  [Russian](https://github.com/sinatra/sinatra/blob/main/README.ru.md),
  [European](https://github.com/sinatra/sinatra/blob/main/README.pt-pt.md) and
  [Brazilian](https://github.com/sinatra/sinatra/blob/main/README.pt-br.md)
  Portuguese,
  [French](https://github.com/sinatra/sinatra/blob/main/README.fr.md),
  [Spanish](https://github.com/sinatra/sinatra/blob/main/README.es.md),
  [Korean](https://github.com/sinatra/sinatra/blob/main/README.ko.md), and
  [Hungarian](https://github.com/sinatra/sinatra/blob/main/README.hu.md).
  The translations tend to fall behind the English version. Translations into
  other languages would also be appreciated.
```

--------------------------------

### Inline Templates

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates defining Sinatra templates directly within the source file using the @@ syntax.

```ruby
require 'sinatra'

get '/' do
  haml :index
end

__END__

@@ layout
%html
  != yield

@@ index
%div.title Hello world.
```

--------------------------------

### Setting Response Attachment

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates using the `attachment` helper in Sinatra to prompt the browser to download the response as a file. It shows how to set a default filename or specify a custom one.

```ruby
get '/' do
  attachment
  "store it!"
end

get '/' do
  attachment "info.txt"
  "store it!"
end
```

--------------------------------

### Use All Sinatra Extensions (Modular Style)

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/README.md

Demonstrates how to register all available Sinatra extensions with a modular Sinatra application.

```ruby
require 'sinatra/base'
require 'sinatra/contrib/all'

class MyApp < Sinatra::Base
  register Sinatra::Contrib
end
```

--------------------------------

### Sinatra Session Options Configuration

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates how to configure additional session options, such as the domain for sharing sessions across subdomains.

```ruby
set :sessions, :domain => 'foo.com'
# For subdomains:
# set :sessions, :domain => '.foo.com'
```

--------------------------------

### Browser Redirects in Sinatra

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates how to perform browser redirects using the `redirect` helper method. It covers redirecting to a specific path, passing additional parameters like HTTP status codes or messages, redirecting to the previous page with `redirect back`, and passing data via query parameters or sessions.

```ruby
get '/foo' do
  redirect to('/bar')
end
```

```ruby
redirect to('/bar'), 303
```

```ruby
redirect 'http://www.google.com/', 'wrong place, buddy'
```

```ruby
get '/foo' do
  "<a href='/bar'>do something</a>"
end

get '/bar' do
  do_something
  redirect back
end
```

```ruby
redirect to('/bar?sum=42')
```

```ruby
enable :sessions

get '/foo' do
  session[:secret] = 'foo'
  redirect to('/bar')
end

get '/bar' do
  session[:secret]
end
```

--------------------------------

### Sinatra Static File Serving

Source: https://github.com/sinatra/sinatra/blob/main/test/public/hello+world.txt

Demonstrates how Sinatra serves static files and the default behavior regarding URL decoding, specifically for the '+' character.

```Ruby
require 'sinatra'

# Sinatra by default decodes '+' as spaces for static files.
# For example, a URL like '/images/my+file.jpg' will be treated as '/images/my file.jpg'.
```

--------------------------------

### Sinatra Passing Control to Next Route

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Explains how to use the `pass` method in Sinatra to punt processing to the next matching route. If no subsequent route matches, a 404 error is returned.

```ruby
get '/guess/:who' do
  pass unless params['who'] == 'Frank'
  'You got me!'
end

get '/guess/*' do
  'You missed!'
end
```

--------------------------------

### Package Sinatra Gems

Source: https://github.com/sinatra/sinatra/blob/main/RELEASING.md

Builds .gem and .tar.gz package files for specified Sinatra gems or all gems.

```sh
# Build sinatra-contrib package
$ bundle exec rake package:sinatra-contrib

# Build rack-protection package
$ bundle exec rake package:rack-protection

# Build sinatra package
$ bundle exec rake package:sinatra

# Build all packages
$ bundle exec rake package:all
```

--------------------------------

### Rendering Literal Haml Templates

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates rendering a Haml template directly from a string. You can also provide `:path` and `:line` options for better error reporting.

```ruby
get '/' do
  haml '%div.title Hello World'
end
```

```ruby
get '/' do
  haml '%div.title Hello World', :path => 'examples/file.haml', :line => 3
end
```

--------------------------------

### Sinatra Static File Serving Configuration

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Details how Sinatra serves static files from the `./public` directory by default. It shows how to configure a different directory using `set :public_folder` and how to add `Cache-Control` headers using `static_cache_control` and custom headers with `static_headers`.

```ruby
set :public_folder, __dir__ + '/static'
```

```ruby
set :static_headers, {
  'access-control-allow-origin' => '*',
  'x-static-asset' => 'served-by-sinatra'
}
```

--------------------------------

### Slim Template Rendering

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Renders Slim templates using the Slim Lang dependency. Supports .slim files.

```ruby
slim :index
```

--------------------------------

### Sinatra Application Settings

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Details various configuration options for a Sinatra application, including how they affect behavior like redirects, content handling, logging, and security. These settings can be modified to customize the application's runtime behavior.

```APIDOC
absolute_redirects:
  If disabled, Sinatra will allow relative redirects, however, Sinatra will no longer conform with RFC 2616 (HTTP 1.1), which only allows absolute redirects.
  Enable if your app is running behind a reverse proxy that has not been set up properly. Note that the url helper will still produce absolute URLs, unless you pass in false as the second parameter.
  Disabled by default.

add_charset:
  Mime types the content_type helper will automatically add the charset info to. You should add to it rather than overriding this option: settings.add_charset << "application/foobar"

app_file:
  Path to the main application file, used to detect project root, views and public folder and inline templates.

bind:
  IP address to bind to (default: 0.0.0.0 or localhost if your environment is set to development). Only used for built-in server.

default_content_type:
  Content-Type to assume if unknown (defaults to "text/html"). Set to nil to not set a default Content-Type on every response; when configured so, you must set the Content-Type manually when emitting content or the user-agent will have to sniff it (or, if nosniff is enabled in Rack::Protection::XSSHeader, assume application/octet-stream).

default_encoding:
  Encoding to assume if unknown (defaults to "utf-8").

dump_errors:
  Display errors in the log. Enabled by default unless environment is "test".

environment:
  Current environment. Defaults to ENV['APP_ENV'], or "development" if not available.

host_authorization:
  You can pass a hash of options to host_authorization, to be used by the Rack::Protection::HostAuthorization middleware.
  The middleware can block requests with unrecognized hostnames, to prevent DNS rebinding and other host header attacks. It checks the Host, X-Forwarded-Host and Forwarded headers.
  Useful options are:
    permitted_hosts – an array of hostnames (and IPAddr objects) your app recognizes
      in the development environment, it is set to .localhost, .test and any IPv4/IPv6 address
      if empty, any hostname is permitted (the default for any other environment)
    status – the HTTP status code used in the response when a request is blocked (defaults to 403)
    message – the body used in the response when a request is blocked (defaults to Host not permitted)
    allow_if – supply a Proc to use custom allow/deny logic, the proc is passed the request environment

logging:
  Use the logger.

lock:
  Places a lock around every request, only running processing on request per Ruby process concurrently.
  Enabled if your app is not thread-safe. Disabled by default.

method_override:
  Use _method magic to allow put/delete forms in browsers that don't support it.

mustermann_opts:
  A default hash of options to pass to Mustermann.new when compiling routing paths.

port:
  Port to listen on. Only used for built-in server.

prefixed_redirects:
  Whether or not to insert request.script_name into redirects if no absolute path is given. That way redirect '/foo' would behave like redirect to('/foo'). Disabled by default.

protection:
  Whether or not to enable web attack protections. See protection section above.

public_dir:
  Alias for public_folder. See below.

public_folder:
  Path to the folder public files are served from. Only used if static file serving is enabled (see static setting below). Inferred from app_file setting if not set.

quiet:
  Disables logs generated by Sinatra's start and stop commands. false by default.

reload_templates:
  Whether or not to reload templates between requests. Enabled in development mode.

root:
  
```

--------------------------------

### Sinatra Setting Response Body, Status, and Headers

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to set the response body, status code, and headers in Sinatra using helper methods like `body`, `status`, and `headers`. These can be set within a route or using `after` filters.

```ruby
get '/foo' do
  body "bar"
end

after do
  puts body
end
```

```ruby
get '/foo' do
  status 418
  headers \
    "Allow"   => "BREW, POST, GET, PROPFIND, WHEN",
    "Refresh" => "Refresh: 20; https://ietf.org/rfc/rfc2324.txt"
  body "I\'m a teapot!"
end
```

--------------------------------

### Streaming Responses in Sinatra

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to use the `stream` helper to send data incrementally to the client. This is useful for streaming APIs, Server-Sent Events, and WebSockets. It also notes that streaming behavior depends on the webserver and provides an option to keep the stream open.

```ruby
get '/' do
  stream do |out|
    out << "It's gonna be legen -\n"
    sleep 0.5
    out << " (wait for it) \n"
    sleep 1
    out << "- dary!\n"
  end
end
```

--------------------------------

### Sinatra Extensions Documentation

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/README.md

This section lists various Sinatra extensions and provides links to their official documentation. These extensions add extra features and capabilities to the Sinatra web framework.

```APIDOC
Sinatra Extensions:

- Sinatra::Reloader: http://www.sinatrarb.com/contrib/reloader
- Sinatra::Namespace: http://www.sinatrarb.com/contrib/namespace
- Sinatra::ContentFor: http://www.sinatrarb.com/contrib/content_for
- Sinatra::Cookies: http://www.sinatrarb.com/contrib/cookies
- Sinatra::Streaming: http://www.sinatrarb.com/contrib/streaming
- Sinatra::WebDAV: http://www.sinatrarb.com/contrib/webdav
- Sinatra::Runner: http://www.sinatrarb.com/contrib/runner
- Sinatra::Extension: http://www.sinatrarb.com/contrib/extension
- Sinatra::TestHelpers: https://github.com/sinatra/sinatra/blob/main/SINATRA-contrib/lib/sinatra/test_helpers.rb
- Sinatra::RequiredParams: http://www.sinatrarb.com/contrib/required_params
- Sinatra::CustomLogger: http://www.sinatrarb.com/contrib/custom_logger
- Sinatra::MultiRoute: http://www.sinatrarb.com/contrib/multi_route
- Sinatra::JSON: http://www.sinatrarb.com/contrib/json
- Sinatra::RespondWith: http://www.sinatrarb.com/contrib/respond_with
- Sinatra::ConfigFile: http://www.sinatrarb.com/contrib/config_file
- Sinatra::LinkHeader: http://www.sinatrarb.com/contrib/link_header
- Sinatra::Capture: http://www.sinatrarb.com/contrib/capture
- Sinatra::EngineTracking: https://github.com/sinatra/SINATRA/blob/main/SINATRA-contrib/lib/sinatra/engine_tracking.rb
```

--------------------------------

### Sinatra Session Middleware Configuration

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to enable sessions in Sinatra and configure session storage using Rack::Session::Pool. It shows two methods: enabling sessions directly and manually using `use` for middleware.

```ruby
enable :sessions
set :session_store, Rack::Session::Pool
```

```ruby
set :sessions, :expire_after => 2592000
set :session_store, Rack::Session::Pool
```

```ruby
use Rack::Session::Pool, :expire_after => 2592000
use Rack::Protection::RemoteToken
use Rack::Protection::SessionHijacking
```

--------------------------------

### Using a Single Protection Middleware

Source: https://github.com/sinatra/sinatra/blob/main/rack-protection/README.md

This snippet illustrates how to use a single, specific protection middleware from the Rack::Protection gem, such as 'AuthenticityToken', by explicitly requiring and using it.

```ruby
require 'rack/protection'
use Rack::Protection::AuthenticityToken
run MyApp
```

--------------------------------

### Sinatra Route Matching Order

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates that routes are matched in the order they are defined. The first route that matches the request is invoked. Routes with trailing slashes are distinct from those without.

```ruby
get '/foo' do
  # Does not match "GET /foo/"
end
```

--------------------------------

### Using ETag and Last-Modified for Caching

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates the use of `last_modified` and `etag` helpers in Sinatra to provide caching information to clients. It explains their placement and behavior, including handling weak ETags.

```ruby
get "/article/:id" do
  @article = Article.find params['id']
  last_modified @article.updated_at
  etag @article.sha1
  erb :article
end
```

```ruby
etag @article.sha1, :weak
```

--------------------------------

### Use Common Sinatra Extensions (Modular Style)

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/README.md

Illustrates how to register all common Sinatra extensions with a modular Sinatra application.

```ruby
require 'sinatra/base'
require 'sinatra/contrib'

class MyApp < Sinatra::Base
  register Sinatra::Contrib
end
```

--------------------------------

### Sinatra Conditions: User Agent

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to define routes with conditions, specifically matching based on the User-Agent header. This allows for targeted responses based on the client's browser or application.

```ruby
get '/foo', :agent => /Songbird (\d\.\d)[\d\/]*/? do
  "You're using Songbird version #{params['agent'][0]}"
end

get '/foo' do
  # Matches non-songbird browsers
end
```

--------------------------------

### Require Sinatra::Contrib Extensions (Modular Style)

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/README.md

Shows how to integrate Sinatra::Contrib extensions into modular Sinatra applications using `Sinatra::Base`.

```ruby
require 'sinatra/base'
require 'sinatra/content_for'
require 'sinatra/namespace'

class MyApp < Sinatra::Base
  helpers Sinatra::ContentFor
  register Sinatra::Namespace
end
```

```ruby
require 'sinatra/base'
require 'sinatra/contrib'

class MyApp < Sinatra::Base
  register Sinatra::Contrib
end
```

```ruby
require 'sinatra/base'
require 'sinatra/contrib/all'

class MyApp < Sinatra::Base
  register Sinatra::Contrib
end
```

--------------------------------

### Use Single Sinatra Extension (Modular Style)

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/README.md

Shows how to integrate a single Sinatra extension, such as sinatra/content_for and sinatra/namespace, into a modular Sinatra application.

```ruby
require 'sinatra/base'
require 'sinatra/content_for'
require 'sinatra/namespace'

class MyApp < Sinatra::Base
  helpers Sinatra::ContentFor
  register Sinatra::Namespace
end
```

--------------------------------

### HTML Escaping Helpers for Sinatra

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/ideas.md

This section mentions the availability of helper methods for HTML escaping and similar utilities within the Sinatra framework, aimed at improving security and proper rendering of HTML content.

```ruby
# Helpers for HTML escaping and such.
```

--------------------------------

### Liquid Template Rendering

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Renders Liquid templates using the liquid dependency. Supports .liquid files and requires locals to be passed due to limitations in calling Ruby methods.

```ruby
liquid :index, :locals => { :key => 'value' }
```

--------------------------------

### Contributing to Sinatra Project

Source: https://github.com/sinatra/sinatra/blob/main/CONTRIBUTING.md

This section details the process for contributing to the Sinatra project, including reporting bugs, seeking help, and submitting code patches. It emphasizes using Git and GitHub, writing unit tests, and updating the README.

```Markdown
## Found a bug?

Log it in our [issue tracker][ghi] or send a note to the [mailing list][ml].
Be sure to include all relevant information, like the versions of Sinatra and
Ruby you're using. A [gist](http://gist.github.com/) of the code that caused
the issue as well as any error messages are also very helpful.

## Need help?

The [Sinatra mailing list][ml] has over 900 subscribers, many of which are happy
to help out newbies or talk about potential feature additions. You can also
drop by the [#sinatra](irc://chat.freenode.net/#sinatra) channel on
[irc.freenode.net](http://freenode.net).

## Have a patch?

Bugs and feature requests that include patches are much more likely to
get attention. Here are some guidelines that will help ensure your patch
can be applied as quickly as possible:

1. **Use [Git](http://git-scm.com) and [GitHub](http://github.com):**
   The easiest way to get setup is to fork the
   [sinatra/sinatra repo](http://github.com/sinatra/sinatra/).
   Or, the [sinatra.github.com repo](http://github.com/sinatra/sinatra.github.com/),
   if the patch is doc related.

2. **Write unit tests:** If you add or modify functionality, it must
   include unit tests. If you don't write tests, we have to, and this
   can hold up acceptance of the patch.

3. **Mind the `README`:** If the patch adds or modifies a major feature,
   modify the `README.md` file to reflect that. Again, if you don't
   update the `README`, we have to, and this holds up acceptance.

4. **Push it:** Once you're ready, push your changes to a topic branch
   and add a note to the ticket with the URL to your branch. Or, say
   something like, "you can find the patch on johndoe/foobranch". We also
   gladly accept GitHub [pull requests](http://help.github.com/pull-requests/). 

__NOTE:__ _We will take whatever we can get._ If you prefer to attach diffs in
emails to the mailing list, that's fine; but do know that _someone_ will need
to take the diff through the process described above and this can hold things
up considerably.

[ghi]: http://github.com/sinatra/sinatra/issues
[ml]: http://groups.google.com/group/sinatrarb/topics "Sinatra Mailing List"
```

--------------------------------

### Application Scope: Setting Options

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates how to define and access settings (options) within the application scope (class level) of a Sinatra application. These settings are available via the `settings` object in the request scope.

```Ruby
class MyApp < Sinatra::Base
  # Hey, I'm in the application scope!
  set :foo, 42
  foo # => 42

  get '/foo' do
    # Hey, I'm no longer in the application scope!
    # Accessing settings from request scope:
    settings.foo # => 42
  end
end
```

--------------------------------

### Verbose Logging Extension for Sinatra

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/ideas.md

This extension provides verbose logging for Sinatra applications. It logs the usage of filters, routes, error handlers, templates, and other components, offering detailed insights into application flow.

```ruby
# Some verbose logging extension: Log what filters, routes, error handlers,
# templates, and so on is used.
```

--------------------------------

### Rendering ERB Templates

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to render an ERB template named 'index'. Sinatra looks for templates in the 'views' directory by default. You can also pass template content directly as a string.

```ruby
get '/' do
  erb :index
end
```

```ruby
get '/' do
  code = "<%= Time.now %>"
  erb code
end
```

--------------------------------

### Sinatra Route Return Values

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates the various types of return values accepted by Sinatra route blocks, including strings, Rack-compatible arrays, objects responding to #each, and integer status codes. It also shows how to implement streaming responses.

```ruby
class Stream
  def each
    100.times { |i| yield "#{i}\n" }
  end
end

get('/') { Stream.new }
```

--------------------------------

### Sinatra Regular Expression Routes

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to use regular expressions to define route matching patterns. Captured groups from the regex are available in `params['captures']` or as block parameters.

```ruby
get //hello/([w]+)/ do
  "Hello, #{params['captures'].first}!"
end

get %r{/hello/([w]+)} do |c|
  # Matches "GET /meta/hello/world", "GET /hello/world/1234" etc.
  "Hello, #{c}!"
end
```

--------------------------------

### Nokogiri Template Usage

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Describes how to use the Nokogiri template engine, which is suitable for generating HTML or XML. It also supports inline templates via a block.

```ruby
nokogiri { |xml| xml.em "hi" }
```

--------------------------------

### Sinatra Helper Method Definition

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates defining helper methods within a 'helpers' block for use in route handlers and templates. Helper methods can also be defined in separate modules and then included.

```ruby
helpers do
  def bar(name)
    "#{name}bar"
  end
end

get '/:name' do
  bar(params['name'])
end

module FooUtils
  def foo(name) "#{name}foo" end
end

module BarUtils
  def bar(name) "#{name}bar" end
end

helpers FooUtils, BarUtils
```

--------------------------------

### ERB with Nested Layouts

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates how to use ERB templates with nested layouts by passing blocks to rendering methods.

```ruby
erb :main_layout, :layout => false do
  erb :admin_layout do
    erb :user
  end
end
```

```ruby
erb :admin_layout, :layout => :main_layout do
  erb :user
end
```

--------------------------------

### Sinatra Named Parameters

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to define routes with named parameters in the URL pattern. These parameters are accessible via the `params` hash or directly as block parameters.

```ruby
get '/hello/:name' do
  # matches "GET /hello/foo" and "GET /hello/bar"
  # params['name'] is 'foo' or 'bar'
  "Hello #{params['name']}!"
end

get '/hello/:name' do |n|
  # matches "GET /hello/foo" and "GET /hello/bar"
  # params['name'] is 'foo' or 'bar'
  # n stores params['name']
  "Hello #{n}!"
end
```

--------------------------------

### Markaby Template Rendering

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Renders Markaby templates using the Markaby dependency. Supports .mab files and can accept blocks for inline templates.

```ruby
markaby { h1 "Welcome!" }
```

--------------------------------

### Changing the Views Directory

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to configure Sinatra to look for templates in a directory other than the default './views'.

```ruby
set :views, settings.root + '/templates'
```

--------------------------------

### Sinatra Custom Route Matching Options

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how to customize route matching behavior by passing `:mustermann_opts` to a route. This allows fine-grained control over pattern matching, such as explicit anchoring.

```ruby
get '\A/posts\z', :mustermann_opts => { :type => :regexp, :check_anchors => false } do
  # matches /posts exactly, with explicit anchoring
  "If you match an anchored pattern clap your hands!"
end
```

--------------------------------

### Sinatra Optional Route Parameters

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to define routes with optional parameters using a question mark after the parameter name. This allows the route to match with or without the parameter.

```ruby
get '/posts/:format?' do
  # matches "GET /posts/" and any extension "GET /posts/json", "GET /posts/xml" etc
end
```

--------------------------------

### Sinatra Logger Usage

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to use the `logger` helper in Sinatra to log messages within routes. It explains that the logger respects Rack handler settings and returns a dummy object if logging is disabled. It also covers enabling logging for `Sinatra::Base` subclasses and disabling it.

```ruby
get '/' do
  logger.info "loading data"
  # ...
end
```

```ruby
class MyApp < Sinatra::Base
  configure :production, :development do
    enable :logging
  end
end
```

--------------------------------

### AsciiDoc Template Rendering

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Renders AsciiDoc templates using the Asciidoctor dependency. Supports .asciidoc, .adoc, and .ad files. Locals are typically passed to AsciiDoc templates as Ruby methods cannot be called directly.

```ruby
asciidoc :README, :layout_engine => :erb
```

--------------------------------

### Registering Mime Types in Sinatra

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Explains how to register custom mime types using the `mime_type` method within a `configure` block. It also shows how to use the registered mime type with the `content_type` helper.

```ruby
configure do
  mime_type :foo, 'text/foo'
end
```

```ruby
get '/' do
  content_type :foo
  "foo foo foo"
end
```

--------------------------------

### Sinatra Query Parameters

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Explains how routes can utilize query parameters from the request URL. These parameters are accessed through the `params` hash.

```ruby
get '/posts' do
  # matches "GET /posts?title=foo&author=bar"
  title = params['title']
  author = params['author']
  # uses title and author variables; query is optional to the /posts route
end
```

--------------------------------

### Sinatra Error Handling

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Defines various ways to handle errors in Sinatra applications, including catch-all handlers, custom error classes, status codes, and ranges. It also shows how to access the exception object.

```ruby
set :show_exceptions, :after_handler

error do
  'Sorry there was a nasty error'
end

error do
  'Sorry there was a nasty error - ' + env['sinatra.error'].message
end

error MyCustomError do
  'So what happened was...' + env['sinatra.error'].message
end

get '/' do
  raise MyCustomError, 'something bad'
end

error 403 do
  'Access forbidden'
end

get '/secret' do
  403
end

error 400..510 do
  'Boom'
end
```

--------------------------------

### Sinatra Conditional Filters

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to apply filters based on request path patterns or conditions like user-agent or host name.

```ruby
before '/protected/*' do
  authenticate!
end

after '/create/:slug' do |slug|
  session[:last_slug] = slug
end

before :agent => /Songbird/ do
  # ...
end

after '/blog/*', :host_name => 'example.com' do
  # ...
end
```

--------------------------------

### Scss Template Rendering

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Renders Scss templates using the sass-embedded dependency. Supports .scss files and allows for style expansion.

```ruby
scss :stylesheet, :style => :expanded
```

--------------------------------

### Sinatra Splat Parameters

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates the use of splat (wildcard) parameters in route patterns. These capture multiple URL segments and are available in the `params['splat']` array or as block parameters.

```ruby
get '/say/*/to/*' do
  # matches /say/hello/to/world
  params['splat'] # => ["hello", "world"]
end

get '/download/*.*' do
  # matches /download/path/to/file.xml
  params['splat'] # => ["path/to/file", "xml"]
end

get '/download/*.*' do |path, ext|
  [path, ext] # => ["path/to/file", "xml"]
end
```

--------------------------------

### Passing Local Variables to Templates

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Explains how to pass local variables to templates using the `:locals` option, which is particularly useful when working with partials.

```ruby
erb "<%= foo %>", :locals => {:foo => "bar"}
```

--------------------------------

### RABL Template Rendering

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Renders Rabl templates using the Rabl dependency. Supports .rabl files.

```ruby
rabl :index
```

--------------------------------

### Builder Template Usage

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Details the usage of the Builder template engine for generating XML or other structured data. It can be used with a block for inline templates.

```ruby
builder { |xml| xml.em "hi" }
```

--------------------------------

### Sinatra Not Found Error Handling

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Provides a custom handler for 'not_found' errors. This block is executed when a Sinatra::NotFound exception is raised or when the response status code is 404, allowing for custom responses to missing resources.

```ruby
not_found do
  'This is nowhere to be found.'
end
```

--------------------------------

### Sinatra Attack Protection Configuration

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Details how to manage Sinatra's built-in attack protection, which uses Rack::Protection. This includes disabling all protection, disabling specific layers using an options hash or an array, and enabling session-based protection.

```ruby
disable :protection

set :protection, :except => :path_traversal

set :protection, :except => [:path_traversal, :remote_token]

set :protection, :session => true
```

--------------------------------

### ERB Template with Custom Layout

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to specify a custom layout template for ERB rendering. If a layout is not specified, Sinatra uses 'views/layout.erb' by default.

```ruby
get '/' do
  erb :index, :layout => :post
end
```

--------------------------------

### Sinatra Form Helpers with ActiveModel Integration

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/ideas.md

This describes an extension for form helpers in Sinatra, treating forms as first-class objects. It allows forms to accept hashes and use their metadata for JSON APIs or route definitions, strictly adhering to the ActiveModel API.

```ruby
# Form helpers, with forms as first class objects that accepts hashes or
# something, so the form meta data can also be used to expose a JSON API or
# similar, possibly defining routes (like "Sinatra's Hat"), strictly using
# the ActiveModel API.
```

--------------------------------

### Sinatra Time Helpers

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Explains the `time_for` helper in Sinatra for converting various date and time formats into Time objects. It also shows how to override `time_for` to customize date handling for helpers like `last_modified` and `expires`.

```ruby
get '/' do
  pass if Time.now > time_for('Dec 23, 2016')
  "still time"
end

helpers do
  def time_for(value)
    case value
    when :yesterday then Time.now - 24*60*60
    when :tomorrow  then Time.now + 24*60*60
    else super
    end
  end
end

get '/' do
  last_modified :yesterday
  expires :tomorrow
  "hello"
end
```

--------------------------------

### Sinatra Request Object Attributes

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates accessing various attributes of the Sinatra request object to retrieve information about the incoming HTTP request, such as headers, query parameters, request method, URL components, and client IP.

```ruby
get '/foo' do
  t = %w[text/css text/html application/javascript]
  request.accept              # ['text/html', '*/*']
  request.accept? 'text/xml'  # true
  request.preferred_type(t)   # 'text/html'
  request.body                # request body sent by the client (see below)
  request.scheme              # "http"
  request.script_name         # "/example"
  request.path_info           # "/foo"
  request.port                # 80
  request.request_method      # "GET"
  request.query_string        # ""
  request.content_length      # length of request.body
  request.media_type          # media type of request.body
  request.host                # "example.com"
  request.get?                # true (similar methods for other verbs)
  request.form_data?          # false
  request["some_param"]       # value of some_param parameter. [] is a shortcut to the params hash.
  request.referrer            # the referrer of the client or '/'
  request.user_agent          # user agent (used by :agent condition)
  request.cookies             # hash of browser cookies
  request.xhr?                # is this an ajax request?
  request.url                 # "http://example.com/example/foo"
  request.path                # "/example/foo"
  request.ip                  # client IP address
  request.secure?             # false (would be true over ssl)
  request.forwarded?          # true (if running behind a reverse proxy)
  request.env                 # raw env hash handed in by Rack
end
```

--------------------------------

### Handling Request Body

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates how to read and parse the raw request body in a Sinatra POST request. It emphasizes rewinding the body to ensure it can be read and then parsing it as JSON.

```ruby
post "/api" do
  request.body.rewind  # in case someone already read it
  data = JSON.parse request.body.read
  "Hello #{data['name']}!"
end
```

--------------------------------

### Sinatra Error Handling with raise_errors Option

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates the behavior of Sinatra's error handling when the `raise_errors` option is true or false, detailing how custom and catch-all handlers are invoked or bypassed, and the impact on response bodies and error propagation.

```ruby
# First handler
error MyCustomError do
  'A custom message'
end

# Second handler
error do
  'A catch-all message'
end

# Example behavior when raise_errors is false:
# When MyCustomError or descendant is raised, the first handler is invoked.
# When any other error is raised, the second handler is invoked.

# Example behavior when raise_errors is true:
# When MyCustomError or descendant is raised, the first handler is invoked.
# When any other error is raised, the second handler is not invoked, and the error is raised outside the application.

# In the test environment, raise_errors is true by default.
# To test a catch-all error handler, set raise_errors to false for the test.
```

--------------------------------

### Sinatra Session Management

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to enable and use sessions in Sinatra to maintain state across requests. Session data is stored in a hash accessible via the 'session' object.

```ruby
enable :sessions

get '/' do
  "value = " << session[:value].inspect
end

get '/:value' do
  session['value'] = params['value']
end
```

--------------------------------

### Passing Local Variables to Haml

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to explicitly pass local variables to Haml templates, useful for partials or when instance variables are not desired.

```ruby
get '/:id' do
  foo = Foo.find(params['id'])
  haml '%h1= bar.name', :locals => { :bar => foo }
end
```

--------------------------------

### Markdown Template Rendering

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Renders Markdown templates using various dependencies like RDiscount, RedCarpet, kramdown, commonmarker, or pandoc. Supports .markdown, .mkd, and .md files. Markdown templates cannot call Ruby methods or use layouts written in Markdown, but can be combined with other rendering engines.

```ruby
markdown :index, :layout_engine => :erb
```

```ruby
erb :overview, :locals => { :text => markdown(:introduction) }
```

```ruby
%h1 Hello From Haml!
%p= markdown(:greetings)
```

--------------------------------

### Sinatra Smart Cache Extension

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/ideas.md

The `sinatra-smart-cache` extension updates cache headers intelligently. It ensures that caching headers are set only when the new arguments are more restrictive than the current ones, optimizing caching for helper methods like `send_file`.

```ruby
# sinatra-smart-cache: update cache header only if arguments are more
# restrictive than current value, set caching headers that way for most helper
# methods (i.e. `send_file`)
```

--------------------------------

### Sinatra Compass Rewrite Consideration

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/ideas.md

This entry discusses the possibility of a rewrite for the `sinatra-compass` component, suggesting potential improvements or modernization of its functionality.

```ruby
# Rewrite of `sinatra-compass`?
```

--------------------------------

### Sinatra Custom Static File Headers

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Allows defining custom HTTP headers for responses when serving static files. This is useful for setting cross-origin resource sharing (CORS) headers or other custom metadata.

```ruby
set :static_headers, {'access-control-allow-origin' => '*', 'x-static-asset' => 'served-by-sinatra'}
```

--------------------------------

### RDoc Template Rendering

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Renders RDoc templates using the RDoc dependency. Supports .rdoc files. RDoc templates cannot call Ruby methods or use layouts written in RDoc, but can be combined with other rendering engines.

```ruby
rdoc :README, :layout_engine => :erb
```

```ruby
erb :overview, :locals => { :text => rdoc(:introduction) }
```

```ruby
%h1 Hello From Haml!
%p= rdoc(:greetings)
```

--------------------------------

### Memcached Integration in Sinatra

Source: https://github.com/sinatra/sinatra/blob/main/sinatra-contrib/ideas.md

This snippet demonstrates how to integrate Memcached for caching and session management within a Sinatra application. It checks if Memcached is enabled via settings and applies the corresponding Rack middleware.

```ruby
def build(*)
  if settings.memcached?
    use Rack::Cache, :backend => :memcached
    use Rack::Session::Memcached
    # ...
  end
  super
end
```

--------------------------------

### Accessing Instance Variables in Haml

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Demonstrates how instance variables set in a Sinatra route handler are accessible within Haml templates.

```ruby
get '/:id' do
  @foo = Foo.find(params['id'])
  haml '%h1= @foo.name'
end
```

--------------------------------

### Sinatra Custom Conditions with Block Parameters

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Explains how to define custom conditions using `set` with a block that accepts arguments. These arguments can be used to parameterize the condition logic, and splats can handle multiple values.

```ruby
set(:probability) { |value| condition { rand <= value } }

get '/win_a_car', :probability => 0.1 do
  "You won!"
end

get '/win_a_car' do
  "Sorry, you lost."
end

set(:auth) do |*roles|
  condition do
    unless logged_in? && roles.any? {|role| current_user.in_role? role }
      redirect "/login/", 303
    end
  end
end

get "/my/account/", :auth => [:user, :admin] do
  "Your Account Details"
end

get "/only/admin/", :auth => :admin do
  "Only admins are allowed here!"
end
```

--------------------------------

### Modifying Request Path Info

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to use the `before` filter in Sinatra to modify the `request.path_info` before a route is processed, allowing all requests to be funneled to a single handler.

```ruby
before { request.path_info = "/" }

get "/" do
  "all requests end up here"
end
```

--------------------------------

### Sass Template Rendering

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Renders Sass templates using the sass-embedded dependency. Supports .sass files and allows for style expansion.

```ruby
sass :stylesheet, :style => :expanded
```

--------------------------------

### Sinatra Delegation Scope

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Illustrates how to explicitly add method delegations to Sinatra's delegator scope using `Sinatra::Delegator.delegate :method_name`.

```ruby
Sinatra::Delegator.delegate :method_name
```

--------------------------------

### Request Scope: Dynamic Route Definition

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to define new routes dynamically within the request scope of a Sinatra application. It highlights how instance variables set in one request scope are not available in dynamically defined routes for subsequent requests.

```Ruby
class MyApp < Sinatra::Base
  # Hey, I'm in the application scope!
  get '/define_route/:name' do
    # Request scope for '/define_route/:name'
    @value = 42

    settings.get("/#{params['name']}") do
      # Request scope for "/#{params['name']}"
      # @value is nil here because it's a different request context
      @value # => nil (not the same request)
    end

    "Route defined!"
  end
end
```

--------------------------------

### Sinatra Session Secret Configuration

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Details how to configure the session secret for security. It's recommended to use a strong, randomly generated secret stored in an environment variable.

```ruby
require 'securerandom'
set :session_secret, ENV.fetch('SESSION_SECRET') { SecureRandom.hex(64) }
```

--------------------------------

### Accessing the Request Object in Sinatra

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows how to access the incoming request object within Sinatra's filters, routes, and error handlers using the `request` method.

```ruby
get '/' do
  request.env['HTTP_USER_AGENT']
end
```

--------------------------------

### Sinatra Static File Cache Control

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Configures Cache-Control headers for static files served by Sinatra. This setting uses the 'cache_control' helper and can accept single values or an array for multiple directives.

```ruby
set :static_cache_control, [:public, :max_age => 300]
```

--------------------------------

### Yajl JSON Conversion

Source: https://github.com/sinatra/sinatra/blob/main/README.md

Shows the Ruby code used to generate JSON data that can be processed by Yajl templates.

```ruby
json = { :foo => 'bar' }
json[:baz] = key
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.