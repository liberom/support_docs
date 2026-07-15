### Generate Rails Guides Documentation Locally

Source: https://guides.rubyonrails.org/v4.0/getting_started

This command-line snippet shows how to generate local copies of the Rails Guides. It requires the RedCloth gem to be installed and added to your `Gemfile`. After installation, running this command populates the `doc/guides` folder.

```shell
rake doc:guides
```

--------------------------------

### Kamal Setup and Deploy Commands (Shell)

Source: https://guides.rubyonrails.org/getting_started

Shell commands to initiate the Kamal setup process for the first-time deployment and to deploy subsequent changes to the production environment.

```shell
$ bin/kamal setup

```

```shell
$ bin/kamal deploy

```

--------------------------------

### Verify Rails Installation

Source: https://guides.rubyonrails.org/v5.0/getting_started

Confirms that the Rails framework has been successfully installed and is available in the system's PATH. This command outputs the installed Rails version.

```bash
$ rails --version
```

--------------------------------

### Install RedCloth Gem for Rake Task

Source: https://guides.rubyonrails.org/v4.1/getting_started

To use the `rake doc:guides` task, the RedCloth gem is required. This snippet shows how to add the gem to the application's Gemfile and then install it using Bundler. This is a common setup step for Rails projects that need to generate documentation.

```ruby
gem 'redcloth'
# Then run: bundle install
```

--------------------------------

### Verify Ruby Installation

Source: https://guides.rubyonrails.org/v5.0/getting_started

Checks if a compatible version of Ruby is installed on the system. This is a prerequisite for installing and using Ruby on Rails. No specific inputs or outputs are required beyond the command itself.

```bash
$ ruby -v
```

--------------------------------

### Example View for a Rails Action

Source: https://guides.rubyonrails.org/getting_started

This is the HTML content rendered by the `index` action of the `ProductsController`. Rails automatically looks for a view file matching the action's name in the controller's view directory.

```html
<h1>Products#index</h1>
<p>Find me in app/views/products/index.html.erb</p>
```

--------------------------------

### Install and Start Redis on Arch Linux

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Commands to install the Redis package and start the Redis service on Arch Linux. This setup is necessary for Action Cable.

```shell
sudo pacman -S redis
sudo systemctl start redis
```

--------------------------------

### Start Rails Development Server

Source: https://guides.rubyonrails.org/v6.0/getting_started

Starts the default Puma web server for the Rails application. This command assumes you are in the application's root directory. Changes made to files are usually picked up automatically without restarting the server.

```bash
$ rails server
```

```bash
ruby bin\rails server
```

--------------------------------

### Verify Ruby Installation

Source: https://guides.rubyonrails.org/v7.2/getting_started

Checks if a compatible version of Ruby is installed on the system. Rails requires Ruby version 3.1.0 or later. This command is essential before proceeding with Rails installation.

```bash
$ ruby --version
ruby 3.1.0

```

--------------------------------

### Verify SQLite3 Installation

Source: https://guides.rubyonrails.org/v7.2/getting_started

Confirms that SQLite3 is installed and accessible in the system's load PATH. This database is a prerequisite for many Rails applications.

```bash
$ sqlite3 --version

```

--------------------------------

### Create New Rails Application

Source: https://guides.rubyonrails.org/getting_started

Generates the foundational structure for a new Rails application. This command requires the Rails gem to be installed. It creates a new directory with the specified application name and populates it with the necessary files and subdirectories.

```bash
$ rails new store

```

--------------------------------

### Basic Rails Template Example

Source: https://guides.rubyonrails.org/v4.1/rails_application_templates

A simple example of a Rails application template. It demonstrates generating a scaffold, setting the root route, and running database migrations. This template automates common initial setup tasks.

```ruby
# template.rb
generate(:scaffold, "person name:string")
route "root to: 'people#index'"
rake("db:migrate")
git :init
git add: "."
git commit: "-m 'Initial commit'"
```

--------------------------------

### Install MySQL and PostgreSQL Development Files (Ubuntu)

Source: https://guides.rubyonrails.org/v3.1/contributing_to_ruby_on_rails

Installs necessary packages for MySQL and PostgreSQL development on Ubuntu systems, including servers, client libraries, and development files required for gem installation and database interaction.

```bash
$ sudo apt-get install mysql-server libmysqlclient15-dev
$ sudo apt-get install postgresql postgresql-client postgresql-contrib libpq-dev
```

--------------------------------

### Start Ruby on Rails Server

Source: https://guides.rubyonrails.org/v6.1/getting_started

Starts the Puma web server for a Rails application. Ensure you are in the application's root directory. On Windows, use 'ruby bin\rails server'. The server runs on http://localhost:3000 by default. Stop it with Ctrl+C.

```bash
$ bin/rails server

```

```powershell
ruby bin\rails server

```

--------------------------------

### Start Rails Development Server

Source: https://guides.rubyonrails.org/getting_started

This command initiates the Rails development server, typically Puma, which serves your application on localhost. It ensures the application's specific Rails version is utilized. The output shows server configuration and the URL to access the application.

```bash
$ bin/rails server

```

--------------------------------

### Running rackup command (Shell)

Source: https://guides.rubyonrails.org/v6.0/rails_on_rack

Demonstrates how to start a Rails application using the `rackup` command with a `config.ru` file. Also shows how to get help for `rackup` options.

```bash
$ rackup config.ru
```

```bash
$ rackup --help
```

--------------------------------

### Markdown: Configuration Guide Table Example

Source: https://guides.rubyonrails.org/v7.2/contributing_to_ruby_on_rails

An example of a Markdown table used in a configuration guide to document framework defaults. This table clearly shows the starting version for a configuration option and its default value, facilitating understanding for upgrades.

```markdown
```markdown
#### `config.active_job.existing_behavior

| Starting with version |
| --------------------- |
| (original)            |
| 7.1                   |

| The default value is |
| `true`               |
| `false`              |

```
```

--------------------------------

### Install and Run Rails Server with Mongrel

Source: https://guides.rubyonrails.org/v3.1/command_line

This snippet demonstrates how to install the Mongrel gem and then start the Rails server using Mongrel as the backend. It shows the command-line interface for installation and server startup, along with the expected output indicating the server is booting.

```bash
$ sudo gem install mongrel
Building native extensions.  This could take a while...
Building native extensions.  This could take a while...
Successfully installed gem_plugin-0.2.3
Successfully installed fastthread-1.0.1
Successfully installed cgi_multipart_eof_fix-2.5.0
Successfully installed mongrel-1.1.5
...
...
Installing RDoc documentation for mongrel-1.1.5...
$ rails server mongrel
=> Booting Mongrel (use 'rails server webrick' to force WEBrick)
=> Rails 3.1.0 application starting on http://0.0.0.0:3000
...
```

--------------------------------

### Install Action Text Gem (Rails CLI)

Source: https://guides.rubyonrails.org/getting_started

This sequence of commands installs the Action Text gem, a feature in Rails for handling rich text content. It involves running the Action Text installer, bundling the new gem, and migrating the database to set up the necessary tables for storing rich text data.

```bash
$ bin/rails action_text:install
$ bundle install
$ bin/rails db:migrate
```

--------------------------------

### Verify SQLite3 Installation

Source: https://guides.rubyonrails.org/v5.0/getting_started

Verifies that SQLite3 is correctly installed and accessible in the system's PATH. This is important as Rails often uses SQLite3 for database management. The command outputs the installed version if successful.

```bash
$ sqlite3 --version
```

--------------------------------

### Instantiate and Create Product Record in Ruby

Source: https://guides.rubyonrails.org/getting_started

Demonstrates how to instantiate a new Product record with specific attributes and then save it to the database using the .save method. It also shows the shortcut .create method for instantiating and saving in one step.

```ruby
product = Product.new(name: "T-Shirt")
product.save
```

```ruby
Product.create(name: "Pants")
```

--------------------------------

### Generate Rails Controller and Action

Source: https://guides.rubyonrails.org/v4.1/getting_started

This command generates a new controller named 'welcome' with an 'index' action. It also creates associated view, test, helper, and asset files. The command also defines a route for this action.

```bash
$ bin/rails generate controller welcome index
```

--------------------------------

### Generate Rails Controller and View

Source: https://guides.rubyonrails.org/v4.0/getting_started

Creates a new controller named 'welcome' with an 'index' action, along with its associated view file and other generated assets. This command sets up the basic structure for handling incoming requests and rendering responses.

```bash
$ rails generate controller welcome index
```

--------------------------------

### View Generated Routes with `rake routes` in Rails

Source: https://guides.rubyonrails.org/v4.0/getting_started

This example shows the expected output after running the `rake routes` command in a Rails application where `resources :posts` has been defined. It lists all the available routes, including those for the 'posts' resource and the application's root.

```shell
$ rake routes
      posts GET    /posts(.:format)          posts#index
            POST   /posts(.:format)          posts#create
  new_post GET    /posts/new(.:format)      posts#new
 edit_post GET    /posts/:id/edit(.:format) posts#edit
   post GET    /posts/:id(.:format)      posts#show
        PATCH  /posts/:id(.:format)      posts#update
        PUT    /posts/:id(.:format)      posts#update
        DELETE /posts/:id(.:format)      posts#destroy
   root        /                       welcome#index
```

--------------------------------

### Rails Development Server Output Example

Source: https://guides.rubyonrails.org/getting_started

This output provides details about the running Rails server, including the web server being used (Puma), the Rails version, environment, PID, and the local network addresses and ports it's listening on. It also indicates how to stop the server.

```text
=> Booting Puma
=> Rails 8.0.0 application starting in development
=> Run `bin/rails server --help` for more startup options
Puma starting in single mode...
* Puma version: 6.4.3 (ruby 3.3.5-p100) ("The Eagle of Durango")
*  Min threads: 3
*  Max threads: 3
*  Environment: development
*          PID: 12345
* Listening on http://127.0.0.1:3000
* Listening on http://[::1]:3000
Use Ctrl-C to stop

```

--------------------------------

### Check Rails Version

Source: https://guides.rubyonrails.org/getting_started

Verifies the installed version of Rails. This command requires Rails to be installed and accessible in the system's PATH. It outputs the current Rails version number.

```bash
$ rails --version
Rails 8.0.0

```

--------------------------------

### Create New Rails Application

Source: https://guides.rubyonrails.org/v5.0/getting_started

Generates a new Rails application with the specified name ('blog' in this case). It sets up the basic directory structure, configuration files, and installs necessary gem dependencies using Bundler. Optional flags like `--skip-spring` and `--skip-listen` can be used for specific environments.

```bash
$ rails new blog
```

```bash
$ rails new blog --skip-spring --skip-listen
```

--------------------------------

### Generate Rails Controller and Action

Source: https://guides.rubyonrails.org/v6.0/getting_started

Generates a new controller named 'Welcome' with an 'index' action. This command also creates associated view files, routes, tests, and helper files, setting up the basic structure for handling requests to '/welcome/index'.

```bash
$ rails generate controller Welcome index
```

--------------------------------

### Install MySQL and PostgreSQL on Ubuntu

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Commands to install MySQL and PostgreSQL client libraries and development files on Ubuntu systems. These packages are necessary for compiling and running database-related applications.

```shell
sudo apt-get install mysql-server libmysqlclient-dev
sudo apt-get install postgresql postgresql-client postgresql-contrib libpq-dev
```

--------------------------------

### Install MySQL and PostgreSQL on macOS

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Commands to install MySQL and PostgreSQL using Homebrew on macOS. These are prerequisites for running database-specific tests.

```shell
brew install mysql
brew install postgresql
```

--------------------------------

### Create User in Rails Console

Source: https://guides.rubyonrails.org/getting_started

This example demonstrates creating a new User record directly within the Rails console using the `create!` method. It requires providing an email address and password, which will be securely hashed using bcrypt. This is useful for initial setup or testing.

```ruby
store(dev)> User.create! email_address: "you@example.org", password: "s3cr3t", password_confirmation: "s3cr3t"
```

--------------------------------

### Setting Up the Database in Rails

Source: https://guides.rubyonrails.org/v7.1/active_record_migrations

Describes the `bin/rails db:setup` command, which creates the database, loads the schema, and populates it with seed data. This is typically used for initial project setup.

```bash
bin/rails db:setup
```

--------------------------------

### Ruby on Rails View for Product List with New Product Link

Source: https://guides.rubyonrails.org/getting_started

Renders a list of products and includes a link to a 'New product' page. It iterates over the @products collection to display each product's name.

```erb
<h1>Products</h1>

<%= link_to "New product", new_product_path %>

<div id="products">
  <% @products.each do |product| %>
    <div>
      <%= link_to product.name, product %>
    </div>
  <% end %>
</div>
```

--------------------------------

### Rackup Server Start Logic

Source: https://guides.rubyonrails.org/initialization

The `Rackup::Server#start` method handles Rack application initialization, including setting up load paths, requiring specified libraries, and managing daemonization. It ultimately calls `server.run` to start the application.

```ruby
module Rackup
  class Server
    def start(&block)
      if options[:warn]
        $-w = true
      end

      if includes = options[:include]
        $LOAD_PATH.unshift(*includes)
      end

      Array(options[:require]).each do |library|
        require library
      end

      if options[:debug]
        $DEBUG = true
        require "pp"
        p options[:server]
        pp wrapped_app
        pp app
      end

      check_pid! if options[:pid]

      # Touch the wrapped app, so that the config.ru is loaded before
      # daemonization (i.e. before chdir, etc).
      handle_profiling(options[:heapfile], options[:profile_mode], options[:profile_file]) do
        wrapped_app
      end

      daemonize_app if options[:daemonize]

      write_pid if options[:pid]

      trap(:INT) do
        if server.respond_to?(:shutdown)
          server.shutdown
        else
          exit
        end
      end

      server.run(wrapped_app, **options, &block)
    end
  end
end
```

--------------------------------

### Install Rails Plugin

Source: https://guides.rubyonrails.org/v2.3/command_line

This command installs a Rails plugin from a given URL. The example shows installing the 'acts_as_paranoid' plugin, which adds soft-delete functionality to models.

```bash
$ ./script/plugin install http://svn.techno-weenie.net/projects/plugins/acts_as_paranoid
```

--------------------------------

### Install Redis from Package Manager

Source: https://guides.rubyonrails.org/v5.1/development_dependencies_install

Installs the Redis server using the system's package manager. This is a straightforward method for getting Redis up and running, though installing from source is often recommended for the latest versions.

```bash
$ brew install redis
```

```bash
$ sudo apt-get install redis-server
```

```bash
$ sudo yum install redis
```

```bash
$ sudo pacman -S redis
$ systemctl start redis
```

```bash
# portmaster databases/redis
```

--------------------------------

### Install MySQL and PostgreSQL on FreeBSD

Source: https://guides.rubyonrails.org/v4.2/development_dependencies_install

Installs MySQL and PostgreSQL client and server packages on FreeBSD using pkg. This enables Rails applications to connect to and utilize these database systems on FreeBSD.

```bash
# pkg install mysql56-client mysql56-server
# pkg install postgresql93-client postgresql93-server
```

--------------------------------

### Install MySQL and PostgreSQL on OS X

Source: https://guides.rubyonrails.org/v4.2/development_dependencies_install

Installs MySQL and PostgreSQL servers and their client libraries on macOS using Homebrew. This is a prerequisite for running Rails tests with these databases.

```bash
$ brew install mysql
$ brew install postgresql
```

--------------------------------

### Starting Rails Server with Rack::Server

Source: https://guides.rubyonrails.org/v7.1/rails_on_rack

Demonstrates how `bin/rails server` initializes and starts a Rack::Server instance to serve a Rails application. It inherits from Rack::Server and invokes its start method.

```ruby
Rails::Server.new.tap do |server|
  require APP_PATH
  Dir.chdir(Rails.application.root)
  server.start
end

class Server < ::Rack::Server
  def start
    # ...
    super
  end
end
```

--------------------------------

### Ruby on Rails Controller Actions with Create and Strong Parameters

Source: https://guides.rubyonrails.org/getting_started

Extends the ProductsController to include a `create` action for handling new product submissions and a `product_params` private method for strong parameter filtering to ensure security.

```ruby
class ProductsController < ApplicationController
  def index
    @products = Product.all
  end

  def show
    @product = Product.find(params[:id])
  end

  def new
    @product = Product.new
  end

  def create
    @product = Product.new(product_params)
    if @product.save
      redirect_to @product
    else
      render :new, status: :unprocessable_entity
    end
  end

  private
    def product_params
      params.expect(product: [ :name ])
    end
end
```

--------------------------------

### Generate Rails Controller

Source: https://guides.rubyonrails.org/v6.0/getting_started

This command generates a new controller named ArticlesController. This controller will handle requests related to articles. It sets up the basic controller file structure.

```bash
$ rails generate controller Articles
```

--------------------------------

### Display All Rails Routes

Source: https://guides.rubyonrails.org/getting_started

This command lists all the routes your Rails application currently responds to. It's useful for understanding routing patterns and debugging.

```bash
bin/rails routes
```

--------------------------------

### Define Rails Route with String Parameter

Source: https://guides.rubyonrails.org/getting_started

This Rails route example uses a string parameter ':title' to capture parts of the URL. It allows routing based on non-numeric identifiers, such as '/blog/hello-world', making the captured 'hello-world' part available in the controller.

```ruby
get "/blog/:title", to: "blog#show"

```

--------------------------------

### Rails 3 Application Bootstrapping Example

Source: https://guides.rubyonrails.org/v4.0/3_0_release_notes

Demonstrates how to start an application in Rails 3 using its own namespace. This approach simplifies interaction with other applications and ensures a clearer structure. It assumes the application is named 'YourAppName'.

```ruby
YourAppName.boot
```

--------------------------------

### Install Redis on FreeBSD

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Command to install Redis on FreeBSD systems using portmaster. This is a prerequisite for Action Cable's testing.

```shell
# portmaster databases/redis
```

--------------------------------

### Install Redis on Ubuntu

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Command to install the Redis server package on Ubuntu systems. This is required for Action Cable's testing environment.

```shell
sudo apt-get install redis-server
```

--------------------------------

### Setup Rails Database

Source: https://guides.rubyonrails.org/v7.0/active_record_migrations

Creates the database, loads the schema, and initializes it with seed data using the `db:setup` command.

```bash
$ bin/rails db:setup

```

--------------------------------

### Example Rails Application Template

Source: https://guides.rubyonrails.org/v6.0/rails_application_templates

A sample Rails template demonstrating common API calls like generating scaffolds, defining routes, running migrations, and executing git commands after bundle installation.

```ruby
# template.rb
generate(:scaffold, "person name:string")
route "root to: 'people#index'"
rails_command("db:migrate")
after_bundle do 
  git :init 
  git add: "." 
  git commit: "Q"{"-m 'Initial commit'"}
end
```

--------------------------------

### Rack Server Start Method and Application Setup

Source: https://guides.rubyonrails.org/v4.0/initialization

This Ruby method, `Rack::Server#start`, is the core of the Rack server's startup process. It handles options like warnings and library includes, checks for PID files, prepares the application by calling `wrapped_app`, handles daemonization, writes the PID file, sets up an interrupt trap, and finally runs the application.

```ruby
def start &blk
  if options[:warn]
    $-w = true
  end
  if includes = options[:include]
    $LOAD_PATH.unshift(*includes)
  end
  if library = options[:require]
    require library
  end
  if options[:debug]
    $DEBUG = true
    require 'pp'
    p options[:server]
    pp wrapped_app
    pp app
  end
  check_pid! if options[:pid]
  # Touch the wrapped app, so that the config.ru is loaded before
  # daemonization (i.e. before chdir, etc).
  wrapped_app
  daemonize_app if options[:daemonize]
  write_pid if options[:pid]
  trap(:INT) do
    if server.respond_to?(:shutdown)
      server.shutdown
    else
      exit
    end
  end
  server.run wrapped_app, options, &blk
end
```

--------------------------------

### Install Rails 3

Source: https://guides.rubyonrails.org/v6.1/3_0_release_notes

This command installs the Rails 3 gem. Use sudo if your system requires administrator privileges for gem installation. This is the primary method to get started with Rails 3.

```shell
# Use sudo if your setup requires it
$ gem install rails

```

--------------------------------

### Install Bundler

Source: https://guides.rubyonrails.org/v4.1/ruby_on_rails_guides_guidelines

Installs the latest version of Bundler, a dependency manager for Ruby projects. Ensure you have Bundler installed before generating guides.

```bash
gem install bundler
```

--------------------------------

### Install Redis on macOS

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Command to install Redis using Homebrew on macOS. Redis is the default subscriptions adapter for Action Cable.

```shell
brew install redis
```

--------------------------------

### Kamal Deployment Configuration (YAML)

Source: https://guides.rubyonrails.org/getting_started

Configuration file for Kamal deployment. Specifies service name, Docker image, target servers, registry credentials, and proxy settings for SSL.

```yaml
# Name of your application. Used to uniquely configure containers.
service: store

# Name of the container image.
image: your-user/store

# Deploy to these servers.
servers:
  web:
    - 192.168.0.1

# Credentials for your image host.
registry:
  # Specify the registry server, if you're not using Docker Hub
  # server: registry.digitalocean.com / ghcr.io / ...
  username: your-user

proxy:
  ssl: true
  host: app.example.com

```

--------------------------------

### Ruby on Rails Controller Actions for Products

Source: https://guides.rubyonrails.org/getting_started

Defines basic controller actions (index, show, new) for managing products in a Ruby on Rails application. It sets up instance variables to hold product data for views.

```ruby
class ProductsController < ApplicationController
  def index
    @products = Product.all
  end

  def show
    @product = Product.find(params[:id])
  end

  def new
    @product = Product.new
  end
end
```

--------------------------------

### Example Rails Application Template - Ruby

Source: https://guides.rubyonrails.org/v4.2/rails_application_templates

A sample Rails application template demonstrating common DSL commands. It includes generating a scaffold, setting a root route, running migrations, and initializing a Git repository with an initial commit.

```ruby
# template.rb
generate(:scaffold, "person name:string")
route "root to: 'people#index'"
rake("db:migrate")
after_bundle do 
  git :init
  git add: "."
  git commit: "-m 'Initial commit'"
end
```

--------------------------------

### Generate All HTML Guides (Bundler)

Source: https://guides.rubyonrails.org/v7.1/ruby_on_rails_guides_guidelines

Command to generate all HTML guides using Bundler. Requires navigating to the 'guides' directory and ensuring Bundler is installed.

```bash
$ bundle exec rake guides:generate
```

```bash
$ bundle exec rake guides:generate:html
```

--------------------------------

### Verify Yarn Installation

Source: https://guides.rubyonrails.org/v7.1/working_with_javascript_in_rails

This command checks if Yarn, a JavaScript package manager, is installed and accessible in your system's PATH. It prints the installed version of Yarn, which is required for some bundling setups.

```bash
yarn --version
```

--------------------------------

### Install a Rails Plugin

Source: https://guides.rubyonrails.org/v3.0/command_line

This command installs a specified Ruby on Rails plugin from a given URL. Plugins extend Rails functionality. The example shows installing the 'acts_as_paranoid' plugin, which adds soft-delete capabilities to models.

```bash
$ rails plugin install http://svn.techno-weenie.net/projects/plugins/acts_as_paranoid
```

--------------------------------

### Rack::Server Startup and Options Handling

Source: https://guides.rubyonrails.org/v4.1/initialization

The Rack::Server#start method handles server startup, including setting debugging flags, managing the load path, requiring libraries, and setting up signal traps. It also prepares the Rack application for running.

```ruby
def start &blk
  if options[:warn]
    $-w = true
  end
  if includes = options[:include]
    $LOAD_PATH.unshift(*includes)
  end
  if library = options[:require]
    require library
  end
  if options[:debug]
    $DEBUG = true
    require 'pp'
    pp options[:server]
    pp wrapped_app
    pp app
  end
  check_pid! if options[:pid]
  # Touch the wrapped app, so that the config.ru is loaded before
  # daemonization (i.e. before chdir, etc).
  wrapped_app
  daemonize_app if options[:daemonize]
  write_pid if options[:pid]
  trap(:INT) do
    if server.respond_to?(:shutdown)
      server.shutdown
    else
      exit
    end
  end
  server.run wrapped_app, options, &blk
end
```

--------------------------------

### Install MySQL and PostgreSQL on Fedora/CentOS

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Commands to install MySQL and PostgreSQL server and development packages on Fedora or CentOS systems. These are required for database operations and testing.

```shell
sudo yum install mysql-server mysql-devel
sudo yum install postgresql-server postgresql-devel
```

--------------------------------

### Bundle Install after Removing Config

Source: https://guides.rubyonrails.org/v3.1/contributing_to_ruby_on_rails

Resets Bundler's configuration to allow installation of all gems, particularly those in the 'db' group, by removing the existing .bundle/config file before running 'bundle install'.

```bash
$ rm .bundle/config
$ bundle install
```

--------------------------------

### Starting Rails Server with Rack::Server

Source: https://guides.rubyonrails.org/v7.2/rails_on_rack

This snippet demonstrates how bin/rails server creates and starts a Rack::Server instance to serve a Rails application. It involves requiring the application and changing the directory before starting the server.

```ruby
Rails::Server.new.tap do |server|
  require APP_PATH
  Dir.chdir(Rails.application.root)
  server.start
end

```

```ruby
class Server < ::Rack::Server
  def start
    # ...
    super
  end
end

```

--------------------------------

### Install MariaDB and PostgreSQL on Arch Linux

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Commands to install MariaDB (as MySQL is no longer supported) and PostgreSQL on Arch Linux. This includes necessary client libraries and development files.

```shell
sudo pacman -S mariadb libmariadbclient mariadb-clients
sudo pacman -S postgresql postgresql-libs
```

--------------------------------

### Set Starting ID for find_in_batches in Ruby

Source: https://guides.rubyonrails.org/active_record_querying

Configures the starting ID for record selection in `find_in_batches`. This example fetches customers starting from ID 5000 in batches of 2500.

```ruby
Customer.find_in_batches(batch_size: 2500, start: 5000) do |customers|
  export.add_customers(customers)
end

```

--------------------------------

### Generate Rails Controller

Source: https://guides.rubyonrails.org/v4.0/getting_started

This command generates a new controller file for the application. It creates a basic controller class that inherits from ApplicationController, providing a foundation for defining actions.

```bash
$ rails g controller posts
```

--------------------------------

### Install SQLite3 Development Files (Shell)

Source: https://guides.rubyonrails.org/v4.2/development_dependencies_install

These commands install SQLite3 and its development files, which are necessary for running the Rails test suite against the SQLite3 database adapter. The commands vary by operating system.

```bash
# macOS
$ brew install sqlite3
```

```bash
# Ubuntu
$ sudo apt-get install sqlite3 libsqlite3-dev
```

```bash
# Fedora/CentOS
$ sudo yum install sqlite3 sqlite3-devel
```

```bash
# Arch Linux
$ sudo pacman -S sqlite
```

```bash
# FreeBSD
# pkg install sqlite3
```

--------------------------------

### Generate Rails Controller

Source: https://guides.rubyonrails.org/v4.1/getting_started

This command uses the Rails generator to create a new controller file and associated test file. It also generates view, helper, and asset files for the controller.

```bash
$ bin/rails generate controller Comments
```

--------------------------------

### Rails Routes Output

Source: https://guides.rubyonrails.org/v6.0/getting_started

This is the output of the `rails routes` command, illustrating the available routes for an articles resource. It shows the HTTP verbs, URI patterns, and corresponding Controller#Action mappings, which are essential for configuring form submissions and understanding routing in Rails.

```bash
Prefix Verb      URI Pattern                Controller#Action
welcome_index GET       /welcome/index(.:format)   welcome#index
articles      GET       /articles(.:format)        articles#index
              POST      /articles(.:format)        articles#create
new_article   GET       /articles/new(.:format)    articles#new
edit_article  GET       /articles/:id/edit(.:format) articles#edit
article       GET       /articles/:id(.:format)    articles#show
              PATCH     /articles/:id(.:format)    articles#update
              PUT       /articles/:id(.:format)    articles#update
              DELETE    /articles/:id(.:format)    articles#destroy
root          GET       /                          welcome#index
```

--------------------------------

### Install Redis on Fedora/CentOS

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Command to install Redis on Fedora or CentOS systems, assuming the EPEL repository is enabled. Redis is needed for Action Cable.

```shell
sudo yum install redis
```

--------------------------------

### Update Product View with Rails ERB and Hotwire

Source: https://guides.rubyonrails.org/getting_started

This ERB template snippet renders product details and includes links for navigation and actions. It utilizes Rails' caching and Hotwire components (Turbo) for efficient updates and dynamic content.

```erb
<p><%= link_to "Back", products_path %></p>

<section class="product">
  <%= image_tag @product.featured_image if @product.featured_image.attached? %>

  <section class="product-info">
    <% cache @product do %>
      <h1><%= @product.name %></h1>
      <%= @product.description %>
    <% end %>

    <%= render "inventory", product: @product %>

    <% if authenticated? %>
      <%= link_to "Edit", edit_product_path(@product) %>
      <%= button_to "Delete", @product, method: :delete, data: { turbo_confirm: "Are you sure?" } %>
    <% end %>
  </section>
</section>
```

--------------------------------

### Rails Routes: Configuration for Product Index and Show

Source: https://guides.rubyonrails.org/getting_started

This output from 'bin/rails routes' displays the configured routes for the products resource. It shows the HTTP methods, URI patterns, and the corresponding controller actions ('products#index' and 'products#show'). This is crucial for understanding how URLs map to controller logic.

```text
Prefix Verb   URI Pattern                                                                                       Controller#Action
products GET    /products(.:format)                                                                               products#index
 product GET    /products/:id(.:format)                                                                           products#show
```

--------------------------------

### Install Development Dependencies on macOS with Homebrew

Source: https://guides.rubyonrails.org/v7.0/development_dependencies_install

This command uses Homebrew's bundle feature to install all specified development dependencies for Ruby on Rails on macOS. Ensure Homebrew is installed and configured. It also shows how to list and start services managed by Homebrew.

```bash
$ brew bundle
$ brew services list
$ brew services start mysql

```

--------------------------------

### Ruby on Rails Redirect to Show Action

Source: https://guides.rubyonrails.org/getting_started

Demonstrates how to redirect to a product's show page after successful creation. Rails automatically generates the correct URL based on the Active Record object.

```ruby
redirect_to @product
```

--------------------------------

### Rails Route Generation for Articles Resource

Source: https://guides.rubyonrails.org/v4.1/getting_started

This output shows the routes automatically generated by Rails after declaring the ':articles' resource. It lists the HTTP verbs, URI patterns, and corresponding Controller#Action mappings for various article-related operations.

```bash
$ bin/rake routes
       Prefix Verb   URI Pattern                  Controller#Action
     articles GET    /articles(.:format)          articles#index
              POST   /articles(.:format)          articles#create
  new_article GET    /articles/new(.:format)      articles#new
 edit_article GET    /articles/:id/edit(.:format) articles#edit
      article GET    /articles/:id(.:format)      articles#show
              PATCH  /articles/:id(.:format)      articles#update
              PUT    /articles/:id(.:format)      articles#update
              DELETE /articles/:id(.:format)      articles#destroy
        root GET    /                            welcome#index
```

--------------------------------

### Rails Server Startup and Configuration

Source: https://guides.rubyonrails.org/initialization

Defines the `ServerCommand` class for initiating the Rails server. It prepares the environment, sets up the server options, requires the application, and starts the server process. It handles cases where the server might not be directly serveable.

```ruby
module Rails
  module Command
    class ServerCommand < Base # :nodoc:
      def perform
        set_application_directory!
        prepare_restart

        Rails::Server.new(server_options).tap do |server|
          # Require application after server sets environment to propagate
          # the --environment option.
          require APP_PATH
          Dir.chdir(Rails.application.root)

          if server.serveable?
            print_boot_information(server.server, server.served_url)
            after_stop_callback = -> { say "Exiting" unless options[:daemon] }
            server.start(after_stop_callback)
          else
            say rack_server_suggestion(options[:using])
          end
        end
      end
    end
  end
end

```

--------------------------------

### Configure Nested Routes (Rails)

Source: https://guides.rubyonrails.org/getting_started

Sets up nested routes in `config/routes.rb` so that subscriber creation is associated with a specific product. This allows for `POST /products/:product_id/subscribers`.

```ruby
resources :products do
  resources :subscribers, only: [ :create ]
end
```

--------------------------------

### Generate All HTML Guides

Source: https://guides.rubyonrails.org/v4.1/ruby_on_rails_guides_guidelines

Generates all HTML guides by navigating to the 'guides' directory, installing dependencies, and running the rake task. It can also be configured to generate specific guides or all guides even if unmodified.

```bash
cd guides
bundle install
bundle exec rake guides:generate
```

```bash
bundle exec rake guides:generate:html
```

```bash
bundle exec rake guides:generate ONLY=my_guide.md
```

```bash
bundle exec rake guides:generate ALL=1
```

```bash
bundle exec rake guides:generate GUIDES_LANGUAGE=es
```

```bash
rake
```

--------------------------------

### Install MySQL and PostgreSQL (Ubuntu)

Source: https://guides.rubyonrails.org/v5.0/development_dependencies_install

Installs MySQL and PostgreSQL servers, client libraries, and development files on Ubuntu using apt-get.

```bash
$ sudo apt-get install mysql-server libmysqlclient-dev
$ sudo apt-get install postgresql postgresql-client postgresql-contrib libpq-dev
```

--------------------------------

### Example Rails Application Template

Source: https://guides.rubyonrails.org/v5.1/rails_application_templates

A sample Rails application template demonstrating common API calls. It includes generating a scaffold, setting a root route, running database migrations, and initializing a Git repository with an initial commit.

```ruby
# template.rb
generate(:scaffold, "person name:string")
route "root to: 'people#index'"
rails_command("db:migrate")
after_bundle do
  git :init
  git add: "."
  git commit: "-m 'Initial commit'"
end
```

--------------------------------

### List All Configuration Options (Ruby on Rails)

Source: https://guides.rubyonrails.org/ruby_on_rails_guides_guidelines

Command to display all available environment variables for configuring the guide generation script in a Ruby on Rails project.

```bash
rake
```

--------------------------------

### Run EXPLAIN on Rails Queries (PostgreSQL Example)

Source: https://guides.rubyonrails.org/v4.2/active_record_querying

This example demonstrates the output of the `explain` method for a query involving a join, when using the PostgreSQL adapter. Active Record pretty-prints the query plan.

```ruby
User.where(id: 1).joins(:articles).explain
```

```sql
EXPLAIN for: SELECT "users".* FROM "users" INNER JOIN "articles" ON "articles"."user_id" = "users"."id" WHERE "users"."id" = 1
                                                 QUERY PLAN                                                 
-------------------------------------------------------------------------------------------------------------
 Nested Loop Left Join  (cost=0.00..37.24 rows=8 width=0)
   Join Filter: (articles.user_id = users.id)
   ->  Index Scan using users_pkey on users  (cost=0.00..8.27 rows=1 width=4)
         Index Cond: (id = 1)
   ->  Seq Scan on articles  (cost=0.00..28.88 rows=8 width=4)
         Filter: (articles.user_id = 1)
(6 rows)
```

--------------------------------

### Starting Batch Processing from a Specific ID with `find_in_batches`

Source: https://guides.rubyonrails.org/v4.1/active_record_querying

The `:start` option can also be used with `find_in_batches` to begin processing from a specific record ID. This example starts from ID 10000 with a batch size of 500.

```ruby
Invoice.find_in_batches(start: 10000, batch_size: 500) do |invoices|
  export.add_invoices(invoices)
end
```

--------------------------------

### Example Rails Application Template

Source: https://guides.rubyonrails.org/v6.1/rails_application_templates

A comprehensive example of a Rails application template (`template.rb`) demonstrating the use of various template API methods. It includes generating scaffolds, setting root routes, running migrations, and initializing a Git repository with an initial commit.

```ruby
# template.rb
generate(:scaffold, "person name:string")
route "root to: 'people#index'"
rails_command("db:migrate")

after_bundle do
  git :init
  git add: "."
  git commit: %Q{ -m 'Initial commit' }
end
```

--------------------------------

### Install MariaDB and PostgreSQL Gems (Arch Linux)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs MariaDB (as MySQL is no longer supported) and its client utilities, along with PostgreSQL and its client libraries on Arch Linux. This setup is required for testing Active Record with these databases on Arch.

```bash
$ sudo pacman -S mariadb libmariadbclient mariadb-clients
$ sudo pacman -S postgresql postgresql-libs
```

--------------------------------

### Add Navigation Link to Welcome Index (Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This snippet demonstrates how to add a link to the 'posts' controller on the welcome index page using Rails' `link_to` helper. It requires the Rails framework to be set up.

```erb
<h1>Hello, Rails!</h1>
<%= link_to "My Blog", controller: "posts" %>
```

--------------------------------

### Render Inventory Partial (ERB)

Source: https://guides.rubyonrails.org/getting_started

Renders the `_inventory` partial within the `app/views/products/show.html.erb` file. This displays the inventory status and subscription form for a specific product.

```erb
<%= render "inventory", product: @product %>
```

--------------------------------

### Basic Rails Controller Implementation

Source: https://guides.rubyonrails.org/getting_started

Defines a simple controller named `ProductsController` inheriting from `ApplicationController` with an `index` action. Rails automatically loads this controller based on its filename convention.

```ruby
class ProductsController < ApplicationController
  def index
  end
end
```

--------------------------------

### Accessing Production Rails Console (Shell)

Source: https://guides.rubyonrails.org/getting_started

Command to open a Rails console session connected to the production environment, allowing for database interactions.

```shell
$ bin/kamal console

```

--------------------------------

### Rails Migration Execution Output

Source: https://guides.rubyonrails.org/v4.0/getting_started

This is a typical output from running a Rails database migration command. It indicates the start and completion of the migration process, including the time taken for specific actions like table creation.

```text
== CreatePosts: migrating ====================================================
-- create_table(:posts)
   -> 0.0019s
== CreatePosts: migrated (0.0020s) ===========================================

```

--------------------------------

### Set Start and Finish IDs for find_each in Ruby

Source: https://guides.rubyonrails.org/active_record_querying

Defines both the starting and ending primary key for `find_each`. This example fetches records from ID 2000 up to 10000.

```ruby
Customer.find_each(start: 2000, finish: 10000) do |customer|
  NewsMailer.weekly(customer).deliver_now
end

```

--------------------------------

### Verify Ruby Installation

Source: https://guides.rubyonrails.org/v6.1/getting_started

Checks if a compatible version of Ruby (2.5.0 or later) is installed on the system. This is a prerequisite for installing Rails.

```bash
$
ruby --version
```

--------------------------------

### Generate All HTML Guides with Rake

Source: https://guides.rubyonrails.org/v4.2/ruby_on_rails_guides_guidelines

This command generates all HTML guides. It requires Bundler to be installed. It can be configured using environment variables for specific guides, forcing all guides, or specifying a language.

```bash
cd guides
bundle install
bundle exec rake guides:generate
```

```bash
bundle exec rake guides:generate:html
```

--------------------------------

### Create and Manage Rails Applications with Rails CLI

Source: https://context7.com/context7/guides_rubyonrails/llms.txt

Learn to generate new Rails applications, navigate directories, start the development server, generate scaffolded resources (model, controller, views), and run database migrations using the Rails command-line interface.

```bash
# Create a new Rails application
$ rails new store
      create
      create  README.md
      create  Rakefile
      create  .ruby-version
      create  config.ru
      create  .gitignore
      create  .gitattributes
      create  Gemfile
      ...

# Navigate into the application directory
$ cd store

# Start the Rails development server
$ bin/rails server
=> Booting Puma
=> Rails 8.0.0 application starting in development
=> Run `bin/rails server --help` for more startup options
Puma starting in single mode...
* Listening on http://127.0.0.1:3000

# Generate a resource with model, controller, and views
$ bin/rails generate scaffold Product name:string price:decimal description:text
      invoke  active_record
      create    db/migrate/20240502100843_create_products.rb
      create    app/models/product.rb
      invoke  resource_route
       route    resources :products
      invoke  scaffold_controller
      create    app/controllers/products_controller.rb
      invoke    erb
      create      app/views/products
      create      app/views/products/index.html.erb
      create      app/views/products/edit.html.erb
      create      app/views/products/show.html.erb
      create      app/views/products/new.html.erb
      create      app/views/products/_form.html.erb

# Run database migrations
$ bin/rails db:migrate
== 20240502100843 CreateProducts: migrating ==================================
-- create_table(:products)
   -> 0.0019s
== 20240502100843 CreateProducts: migrated (0.0020s) =========================

```

--------------------------------

### Create Subscribers Controller (Ruby)

Source: https://guides.rubyonrails.org/getting_started

Defines a Subscribers controller with a `create` action to handle new subscriber submissions. It finds the product, creates or finds a subscriber with the provided email, and redirects.

```ruby
class SubscribersController < ApplicationController
  allow_unauthenticated_access
  before_action :set_product

  def create
    @product.subscribers.where(subscriber_params).first_or_create
    redirect_to @product, notice: "You are now subscribed."
  end

  private

  def set_product
    @product = Product.find(params[:product_id])
  end

  def subscriber_params
    params.expect(subscriber: [ :email ])
  end
end
```

--------------------------------

### Install Action Mailbox

Source: https://guides.rubyonrails.org/v7.2/action_mailbox_basics

Installs the Action Mailbox gem and its associated migrations. This command generates the necessary files and sets up the database schema for handling incoming emails.

```bash
bin/rails action_mailbox:install

```

--------------------------------

### Generate New Rails App with Dev Container

Source: https://guides.rubyonrails.org/v7.2/getting_started_with_devcontainer

Creates a new Rails application named 'blog' and configures it for use within a development container. This command automates the setup of Ruby, Rails, and other dependencies within a containerized environment, simplifying the development workflow.

```bash
$ rails-new blog --devcontainer

```

--------------------------------

### Preparing the Database in Rails

Source: https://guides.rubyonrails.org/v7.1/active_record_migrations

Explains the `bin/rails db:prepare` command, which idempotently sets up the database. It creates the database, loads the schema, runs pending migrations, and loads seed data if they don't already exist.

```bash
bin/rails db:prepare
```

--------------------------------

### Starting the Rails Development Server

Source: https://guides.rubyonrails.org/v4.2/getting_started

This command starts the WEBrick web server for your Rails application. It allows you to view your application in a web browser. On Windows, you need to invoke the script directly using the Ruby interpreter. Changes to files are usually automatically picked up by the server in development mode.

```bash
$ bin/rails server
```

```bash
ruby bin\rails server
```

--------------------------------

### Incoming HTTP Request Example

Source: https://guides.rubyonrails.org/v2.3/routing

An example of an incoming HTTP GET request to a specific URL path. Rails routing is responsible for interpreting this request and dispatching it to the appropriate controller action.

```text
GET /patients/17
```

--------------------------------

### Setting Up Development Environment with Dev Container CLI

Source: https://guides.rubyonrails.org/v7.1/contributing_to_ruby_on_rails

This example illustrates how to set up a Ruby on Rails development environment using the Dev Container CLI. It involves installing the CLI globally, navigating to the Rails project directory, and then using commands to build and execute the development container. This method utilizes the .devcontainer configuration for consistent development setups.

```bash
$ npm install -g @devcontainers/cli
$ cd rails
$ devcontainer up --workspace-folder .
$ devcontainer exec --workspace-folder . bash
```

--------------------------------

### Install MySQL/MariaDB Client Libraries and Development Files

Source: https://guides.rubyonrails.org/v5.1/development_dependencies_install

Installs MySQL or MariaDB server, client libraries, and development files required for database operations. Commands are provided for various operating systems.

```bash
$ brew install mysql
$ brew install postgresql
```

```bash
$ sudo apt-get install mysql-server libmysqlclient-dev
$ sudo apt-get install postgresql postgresql-client postgresql-contrib libpq-dev
```

```bash
$ sudo yum install mysql-server mysql-devel
$ sudo yum install postgresql-server postgresql-devel
```

```bash
$ sudo pacman -S mariadb libmariadbclient mariadb-clients
$ sudo pacman -S postgresql postgresql-libs
```

```bash
# pkg install mysql56-client mysql56-server
# pkg install postgresql94-client postgresql94-server
```

--------------------------------

### Implement HTTP Basic Authentication in Rails PostsController

Source: https://guides.rubyonrails.org/v4.0/getting_started

This snippet demonstrates how to use Rails' `http_basic_authenticate_with` method in the `PostsController`. It allows access to the `index` and `show` actions without authentication while requiring it for all other actions. Ensure you have a `Post` model and related setup.

```ruby
class PostsController < ApplicationController
  http_basic_authenticate_with name: "dhh", password: "secret", except: [:index, :show]

  def index
    @posts = Post.all
  end
  # snipped for brevity
```

--------------------------------

### Initialize Rails App with Git and PostgreSQL

Source: https://guides.rubyonrails.org/v7.0/command_line

This snippet demonstrates initializing a new Rails application with Git version control and PostgreSQL as the database. It requires creating a directory, initializing Git, and then running the `rails new` command with specific options. The output shows the files created by Rails and files added to the Git repository.

```bash
$ mkdir gitapp
$ cd gitapp
$ git init
Initialized empty Git repository in .git/
$ rails new . --git --database=postgresql
      exists
      create  app/controllers
      create  app/helpers
...
...
      create  tmp/cache
      create  tmp/pids
      create  Rakefile
add 'Rakefile'
      create  README.md
add 'README.md'
      create  app/controllers/application_controller.rb
add 'app/controllers/application_controller.rb'
      create  app/helpers/application_helper.rb
...
      create  log/test.log
add 'log/test.log'

```

--------------------------------

### Install Dependencies for Rails Tests

Source: https://guides.rubyonrails.org/v3.1/contributing_to_ruby_on_rails

These commands install essential development libraries and Ruby gems required for running the Ruby on Rails test suite. It includes system packages for XML and SQLite, and uses Bundler to manage Ruby gem dependencies, excluding database drivers initially.

```bash
sudo apt-get install libxml2 libxml2-dev libxslt1-dev
sudo apt-get install sqlite3 libsqlite3-dev
gem install bundler
bundle install --without db
```

--------------------------------

### Install Memcached (Shell)

Source: https://guides.rubyonrails.org/v4.2/development_dependencies_install

These commands install Memcached, a distributed memory object caching system, which may be required for certain parts of the Rails test suite. The commands differ based on the operating system.

```bash
# macOS
$ brew install memcached
```

```bash
# Ubuntu
$ sudo apt-get install memcached
```

```bash
# Fedora/CentOS
$ sudo yum install memcached
```

```bash
# Arch Linux
$ sudo pacman -S memcached
```

```bash
# FreeBSD
# pkg install memcached
```

--------------------------------

### Install Action Mailbox and Database Migrations (Ruby on Rails)

Source: https://guides.rubyonrails.org/v6.1/action_mailbox_basics

Installs the necessary files for Action Mailbox and applies database migrations to support inbound email records. Requires Active Storage to be set up.

```bash
$ bin/rails action_mailbox:install
$ bin/rails db:migrate
```

--------------------------------

### Implement Basic HTTP Authentication in Rails Controllers

Source: https://guides.rubyonrails.org/v6.0/getting_started

This Ruby code shows how to implement basic HTTP authentication in Rails controllers using the `http_basic_authenticate_with` method. It allows specifying which actions should be protected and provides credentials. The `ArticlesController` example protects all actions except `index` and `show`, while the `CommentsController` example protects only the `destroy` action.

```ruby
class ArticlesController < ApplicationController
  http_basic_authenticate_with name: "dhh", password: "secret", except: [:index, :show]
  
  def index
    @articles = Article.all
  end
  # snippet for brevity
```

```ruby
class CommentsController < ApplicationController
  http_basic_authenticate_with name: "dhh", password: "secret", only: :destroy
  
  def create
    @article = Article.find(params[:article_id])
    # ...
  end
  # snippet for brevity
```

--------------------------------

### Rails Functional Test: Simulating GET Request with Options

Source: https://guides.rubyonrails.org/v5.0/testing

This example demonstrates how to simulate a GET request in Rails functional tests, including passing parameters, headers, and other options. It shows flexibility in testing various request scenarios.

```ruby
# Simulating GET request to the :show action with params and headers
get article_url, params: { id: 12 }, headers: { "HTTP_REFERER" => "http://example.com/home" }
```

--------------------------------

### Set Starting ID for find_each in Ruby

Source: https://guides.rubyonrails.org/active_record_querying

Configures the first ID of the sequence for `find_each`, useful for resuming interrupted processes. This example starts fetching from ID 2000.

```ruby
Customer.find_each(start: 2000) do |customer|
  NewsMailer.weekly(customer).deliver_now
end

```

--------------------------------

### Rack Server Startup Logic

Source: https://guides.rubyonrails.org/v7.2/initialization

The `Rack::Server#start` method handles various server configurations including load path adjustments, library requirements, debugging options, PID file management, daemonization, and signal handling. It ultimately runs the application using `server.run`.

```ruby
module Rack
  class Server
    def start(&blk)
      if options[:warn]
        $-w = true
      end

      if includes = options[:include]
        $LOAD_PATH.unshift(*includes)
      end

      if library = options[:require]
        require library
      end

      if options[:debug]
        $DEBUG = true
        require "pp"
        p options[:server]
        pp wrapped_app
        pp app
      end

      check_pid! if options[:pid]

      # Touch the wrapped app, so that the config.ru is loaded before
      # daemonization (i.e. before chdir, etc).
      handle_profiling(options[:heapfile], options[:profile_mode], options[:profile_file]) do
        wrapped_app
      end

      daemonize_app if options[:daemonize]

      write_pid if options[:pid]

      trap(:INT) do
        if server.respond_to?(:shutdown)
          server.shutdown
        else
          exit
        end
      end

      server.run wrapped_app, options, &blk
    end
  end
end

```

--------------------------------

### Generate All Ruby on Rails Guides

Source: https://guides.rubyonrails.org/v3.2/ruby_on_rails_guides_guidelines

This command generates all Ruby on Rails guides. It requires Bundler to be installed and may need a `bundle install` beforehand. The `ONLY` environment variable can be used to process specific files, and `ALL=1` forces processing of all guides. `WARNINGS=1` is recommended for detecting issues like duplicate IDs and broken links.

```shell
bundle exec rake generate_guides
```

```shell
bundle exec rake generate_guides ONLY=my_guide
```

```shell
bundle exec rake generate_guides ALL=1 WARNINGS=1
```

--------------------------------

### Generate Rails API Documentation Locally

Source: https://guides.rubyonrails.org/v4.0/getting_started

This command-line snippet demonstrates how to generate local API documentation for Rails. Running this command will place the documentation files in the `doc/api` folder of your application, allowing you to explore the API offline.

```shell
rake doc:rails
```

--------------------------------

### Install MySQL and PostgreSQL (FreeBSD)

Source: https://guides.rubyonrails.org/v5.0/development_dependencies_install

Installs MySQL and PostgreSQL client and server packages on FreeBSD using pkg.

```bash
# pkg install mysql56-client mysql56-server
# pkg install postgresql94-client postgresql94-server
```

--------------------------------

### Generate Inventory Migration (Rails)

Source: https://guides.rubyonrails.org/getting_started

Generates a Rails migration to add an 'inventory_count' integer column to the Products table. This is the first step in tracking product stock.

```bash
$ bin/rails generate migration AddInventoryCountToProducts inventory_count:integer
```

--------------------------------

### Install Rails Gem

Source: https://guides.rubyonrails.org/v6.1/getting_started

Installs the Rails gem using RubyGems, which is the standard package manager for Ruby. This command makes the Rails framework available for creating and managing applications.

```bash
$
gem install rails
```

--------------------------------

### Define Basic Rails Route

Source: https://guides.rubyonrails.org/getting_started

This code snippet defines a basic route in Rails. It maps GET requests to the '/products' URL to the 'index' action within the 'ProductsController'. This is a fundamental way to direct incoming web traffic to the appropriate controller logic.

```ruby
Rails.application.routes.draw do
  get "/products", to: "products#index"
end

```

--------------------------------

### Map Route to Controller Action with Symbol in Rails

Source: https://guides.rubyonrails.org/v4.0/routing

This example demonstrates mapping a GET request for a specific path directly to an action using a symbol. This is a more concise way to specify the target action when using `match` or `get` with a `to:` option.

```ruby
get 'profile', to: :show
```

--------------------------------

### Get Substring from Position - Ruby

Source: https://guides.rubyonrails.org/v6.0/active_support_core_extensions

Extracts a substring starting from a specified position to the end of the string. Handles positive, negative, and out-of-bounds indices, returning `nil` if the starting position is invalid.

```ruby
"hello".from(0)  # => "hello"
"hello".from(2)  # => "llo"
"hello".from(-2) # => "lo"
"hello".from(10) # => nil
```

--------------------------------

### Ruby on Rails View for New Product Form

Source: https://guides.rubyonrails.org/getting_started

Generates an HTML form for creating a new product using Rails' `form_with` helper. It includes input fields for the product's name and a submit button.

```erb
<h1>New product</h1>

<%= form_with model: @product do |form| %>
  <div>
    <%= form.label :name %>
    <%= form.text_field :name %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```

--------------------------------

### Rack::Server#start Method - Ruby

Source: https://guides.rubyonrails.org/v5.2/initialization

The `start` method from `Rack::Server` is called via `super` from `Rails::Server#start`. It handles various startup options such as warnings, load path manipulation, requiring specific libraries, and debugging. It also manages PID file creation, daemonization, and sets up signal traps before running the Rack application.

```ruby
def start &blk
  if options[:warn]
    $-w = true
  end
  if includes = options[:include]
    $LOAD_PATH.unshift(*includes)
  end
  if library = options[:require]
    require library
  end
  if options[:debug]
    $DEBUG = true
    require 'pp'
    p options[:server]
    pp wrapped_app
    pp app
  end
  check_pid! if options[:pid]
  wrapped_app
  daemonize_app if options[:daemonize]
  write_pid if options[:pid]
  trap(:INT) do
    if server.respond_to?(:shutdown)
      server.shutdown
    else
      exit
    end
  end
  server.run wrapped_app, options, &blk
end
```

--------------------------------

### Generate Subscriber Model (Rails)

Source: https://guides.rubyonrails.org/getting_started

Generates a new Rails model named 'Subscriber' with a belongs-to association to Product and an 'email' attribute. This sets up the database table for subscribers.

```bash
$ bin/rails generate model Subscriber product:belongs_to email
```

--------------------------------

### Generate Basic Rails Application

Source: https://guides.rubyonrails.org/v2.3/plugins

Installs the Rails gem and creates a new Rails application named 'yaffle_guide'. It then generates a scaffold for a 'bird' resource, migrates the database, and starts the development server. This is a prerequisite for plugin development.

```bash
gem install rails
rails yaffle_guide
cd yaffle_guide
script/generate scaffold bird name:string
rake db:migrate
script/server
```

--------------------------------

### Define Root Route in Rails

Source: https://guides.rubyonrails.org/getting_started

Configures the root URL of the application to render the `index` action of the `ProductsController`. This is done by modifying the `config/routes.rb` file.

```ruby
root "products#index"
```

--------------------------------

### Example Rails Middleware Stack Output (Text)

Source: https://guides.rubyonrails.org/v3.1/rails_on_rack

An example output of the `rake middleware` task, showing the sequence of Rack middlewares applied to a typical Rails application. Each line indicates a middleware and its configuration.

```text
use Rack::Lock
use ActionController::Failsafe
use ActionController::Session::CookieStore, , {
  :secret=>"<secret>",
  :session_key=>"<_app>_session"
}
use Rails::Rack::Metal
use ActionDispatch::RewindableInput
use ActionController::ParamsParser
use Rack::MethodOverride
use Rack::Head
use ActiveRecord::QueryCache
run ActionController::Dispatcher.new
```

--------------------------------

### Index Action and View for Listing Articles in Rails

Source: https://guides.rubyonrails.org/v4.2/getting_started

Implements the 'index' action in the ArticlesController to fetch all articles using Article.all and prepares them for display. The corresponding ERB view then iterates over the articles to create an HTML table listing their titles and text.

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end
  
  def show
    @article = Article.find(params[:id])
  end
  
  def new
  end
  
  # snippet for brevity
```

```html+erb
<h1>Listing articles</h1>
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
  </tr>
  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
    </tr>
  <% end %>
</table>
```

--------------------------------

### Run Rails App with Mongrel Server (Ruby)

Source: https://guides.rubyonrails.org/v4.0/initialization

This Ruby code demonstrates how the Mongrel server integrates with Rack to run a Rails application. It initializes a `Mongrel::HttpServer` instance with various options like host, port, and processors. The code then registers the application with the server, potentially handling multiple paths or a `Rack::URLMap`, before starting the server and joining its run thread.

```ruby
server = ::Mongrel::HttpServer.new(
  options[:Host]        || '0.0.0.0',
  options[:Port]        || 8080,
  options[:num_processors] || 950,
  options[:throttle]      || 0,
  options[:timeout]       || 60
)

# Acts like Rack::URLMap, utilizing Mongrel's own path finding methods.
# Use is similar to #run, replacing the app argument with a hash of
# { path=>app, ... } or an instance of Rack::URLMap.
if options[:map]
  if app.is_a? Hash
    app.each do |path, appl|
      path = '/' + path unless path[/^\//]
      server.register(path, Rack::Handler::Mongrel.new(appl))
    end
  elsif app.is_a? URLMap
    app.instance_variable_get(:@mapping).each do |(host, path, appl)|
          next if !host.nil? && !options[:Host].nil? && options[:Host] != host
          path = '/' + path unless path[/^\//]
          server.register(path, Rack::Handler::Mongrel.new(appl))
        end
  else
    raise ArgumentError, "first argument should be a Hash or URLMap"
  end
else
  server.register('/', Rack::Handler::Mongrel.new(app))
end

yield server if block_given?
server.run.join
```

--------------------------------

### Define Routes for Articles (Ruby on Rails)

Source: https://guides.rubyonrails.org/v6.1/getting_started

Configures routes for the Articles resource, specifically mapping GET requests for '/articles' to the index action and '/articles/:id' to the show action. The ':id' in the path is a route parameter.

```ruby
Rails.application.routes.draw do
  root "articles#index"

  get "/articles", to: "articles#index"
  get "/articles/:id", to: "articles#show"
end

```

--------------------------------

### Generate All HTML Guides with Rake

Source: https://guides.rubyonrails.org/v7.0/ruby_on_rails_guides_guidelines

Command to generate all HTML versions of the Ruby on Rails Guides using Bundler and Rake. Ensure Bundler is installed and updated before running.

```bash
$ bundle exec rake guides:generate:html
```

--------------------------------

### Exporting Docker Registry Password (Shell)

Source: https://guides.rubyonrails.org/getting_started

Environment variable command to export the Docker Hub access token for Kamal to use during image push operations.

```shell
export KAMAL_REGISTRY_PASSWORD=your-access-token
```

--------------------------------

### Navigate to Application Directory

Source: https://guides.rubyonrails.org/getting_started

Changes the current working directory to the newly created Rails application directory. This is a standard shell command used after generating a new application to work within its context.

```bash
$ cd store

```

--------------------------------

### Generate a Model in Rails

Source: https://guides.rubyonrails.org/v6.1/getting_started

Use the Rails command-line interface to generate a new model. This command creates the model file, database migration, and test files. The example generates an `Article` model with `title` (string) and `body` (text) attributes.

```bash
$ bin/rails generate model Article title:string body:text

```

--------------------------------

### Install and Migrate Active Storage

Source: https://guides.rubyonrails.org/active_storage_overview

These commands install Active Storage and create the necessary database tables. This is a crucial step for setting up Active Storage in your Rails application.

```bash
$ bin/rails active_storage:install
$ bin/rails db:migrate
```

--------------------------------

### Output of a Successful Ruby on Rails Migration

Source: https://guides.rubyonrails.org/v6.0/getting_started

This output shows the result of running a database migration in Ruby on Rails. It indicates the migration being applied (`CreateArticles`), the specific database operation performed (`create_table(:articles)`), the execution time, and confirmation of successful migration.

```bash
== CreateArticles: migrating ===============
-- create_table(:articles)
 -> 0.0019s
== CreateArticles: migrated (0.0020s) ================
```

--------------------------------

### Rails Server Initialization in Ruby

Source: https://guides.rubyonrails.org/v4.2/rails_on_rack

Demonstrates how `rails server` creates and starts a `Rack::Server` object. It requires the application path, changes the directory to the Rails application root, and then initiates the server.

```ruby
Rails::Server.new.tap do |server|
  require APP_PATH
  Dir.chdir(Rails.application.root)
  server.start
end
```

--------------------------------

### Execute Rails Server Script

Source: https://guides.rubyonrails.org/v4.0/initialization

This Ruby script is the entry point for starting a Rails application. It sets the application path, loads the boot configuration, and requires the necessary Rails commands to run the server.

```ruby
#!/usr/bin/env ruby
APP_PATH = File.expand_path('../../config/application', __FILE__)
require File.expand_path('../../config/boot', __FILE__)
require 'rails/commands'
```

--------------------------------

### Rack Server App Builder

Source: https://guides.rubyonrails.org/initialization

Builds the Rack application instance, either from a configuration string using `build_app_from_string` or from a configuration file using `build_app_and_options_from_config`. It handles the creation of the Rack::Builder instance.

```ruby
module Rackup
  class Server
    def app
      @app ||= options[:builder] ? build_app_from_string : build_app_and_options_from_config
    end

    # ...

    private
      def build_app_and_options_from_config
        if !::File.exist? options[:config]
          abort "configuration #{options[:config]} not found"
        end

        Rack::Builder.parse_file(self.options[:config])
      end

      def build_app_from_string
        Rack::Builder.new_from_string(self.options[:builder])
      end
  end
end

```

--------------------------------

### Get Beginning of Day in Ruby

Source: https://guides.rubyonrails.org/v5.1/active_support_core_extensions

Calculates the timestamp at the very start of the day (00:00:00). This method is also aliased as `at_beginning_of_day`, `midnight`, and `at_midnight`.

```ruby
date = Date.new(2010, 6, 7)
date.beginning_of_day
# => Mon Jun 07 00:00:00 +0200 2010
```

--------------------------------

### Installing Bundler with RubyGems

Source: https://guides.rubyonrails.org/v4.0/ruby_on_rails_guides_guidelines

This command installs the latest version of Bundler, a dependency management tool for Ruby projects. It's a prerequisite for generating Ruby on Rails guides.

```Shell
gem install bundler

```

--------------------------------

### Generate HTML Rails Guides in a Specific Language

Source: https://guides.rubyonrails.org/v6.1/contributing_to_ruby_on_rails

This command installs necessary gems for generating HTML guides, navigates to the guides directory, and then executes a Rake task to generate the HTML output for a specified language (e.g., Italian). Ensure you have Bundler installed and are in the root of the Rails project.

```bash
bundle install --without job cable storage ujs test db
cd guides/
bundle exec rake guides:generate:html GUIDES_LANGUAGE=it-IT
```

--------------------------------

### Article Model Association in Rails

Source: https://guides.rubyonrails.org/v4.1/getting_started

Defines the association for the Article model. It has many comments, establishing the other side of the one-to-many relationship. Includes basic title validation.

```ruby
class Article < ActiveRecord::Base
  has_many :comments
  validates :title, presence: true,
                    length: { minimum: 5 }
end
```

--------------------------------

### Example Rails Middleware Stack Output

Source: https://guides.rubyonrails.org/v7.0/rails_on_rack

An example output from the `bin/rails middleware` command, illustrating a typical middleware stack for a freshly generated Rails application. This includes standard middlewares for request handling, session management, and more.

```text
use Rack::Sendfile
use ActionDispatch::Static
use ActionDispatch::Executor
use ActiveSupport::Cache::Strategy::LocalCache::Middleware
use Rack::Runtime
use Rack::MethodOverride
use ActionDispatch::RequestId
use ActionDispatch::RemoteIp
use Sprockets::Rails::QuietAssets
use Rails::Rack::Logger
use ActionDispatch::ShowExceptions
use WebConsole::Middleware
use ActionDispatch::DebugExceptions
use ActionDispatch::ActionableExceptions
use ActionDispatch::Reloader
use ActionDispatch::Callbacks
use ActiveRecord::Migration::CheckPending
use ActionDispatch::Cookies
use ActionDispatch::Session::CookieStore
use ActionDispatch::Flash
use ActionDispatch::ContentSecurityPolicy::Middleware
use Rack::Head
use Rack::ConditionalGet
use Rack::ETag
use Rack::TempfileReaper
run MyApp::Application.routes
```

--------------------------------

### Creating a Production User (Rails Console)

Source: https://guides.rubyonrails.org/getting_started

Ruby code executed within the Rails console to create a new user record in the production database, including email and password.

```ruby
store(prod)> User.create!(email_address: "you@example.org", password: "s3cr3t", password_confirmation: "s3cr3t")

```

--------------------------------

### Define Route for Articles Index in Rails

Source: https://guides.rubyonrails.org/v6.1/getting_started

Adds a route to the Rails application's `config/routes.rb` file. This route maps GET requests to '/articles' to the 'index' action of the 'ArticlesController'. Requires Ruby.

```ruby
Rails.application.routes.draw do
  get "/articles", to: "articles#index"

  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end

```

--------------------------------

### Verify Rails Installation

Source: https://guides.rubyonrails.org/install_ruby_on_rails

Confirms that Rails has been installed successfully by displaying its version number.

```shell
$ rails --version

```

--------------------------------

### Generate Rails Controller and View

Source: https://guides.rubyonrails.org/v5.0/getting_started

This command uses the Rails generator to create a new controller named 'Welcome' with an 'index' action. It also generates associated view files, routes, tests, and assets. The primary files created are the controller logic and the HTML view template.

```bash
$ bin/rails generate controller Welcome index
```

--------------------------------

### Add Subscribers Association (Ruby)

Source: https://guides.rubyonrails.org/getting_started

Updates the Product model to include a `has_many` association with Subscribers, specifying dependent destroy. This defines the relationship between products and their subscribers.

```ruby
class Product < ApplicationRecord
  has_many :subscribers, dependent: :destroy
  has_one_attached :featured_image
  has_rich_text :description

  validates :name, presence: true
  validates :inventory_count, numericality: { greater_than_or_equal_to: 0 }
end
```

--------------------------------

### Display Flash Notice (ERB)

Source: https://guides.rubyonrails.org/getting_started

Includes a div to display flash messages, specifically the 'notice' set after subscribing. This is typically placed in the application layout to show feedback to the user.

```erb
<html>
  <!-- ... -->
  <body>
    <div class="notice"><%= notice %></div>
    <!-- ... -->
  </body>
</html>
```

--------------------------------

### Text Email Template for In Stock Notification

Source: https://guides.rubyonrails.org/getting_started

The plain text template for the 'in_stock' email. It includes a clear message indicating the product is back in stock and provides the full product URL for easy access.

```erb
Good news!

<%= @product.name %> is back in stock.
<%= product_url(@product) %>
```

--------------------------------

### Define Rails Controller Class

Source: https://guides.rubyonrails.org/v4.0/getting_started

This Ruby code defines a controller class named PostsController that inherits from ApplicationController. This is the basic structure for a controller in a Rails application.

```ruby
class PostsController < ApplicationController
end
```

--------------------------------

### Verify Rails Installation

Source: https://guides.rubyonrails.org/v6.1/getting_started

Confirms that the Rails gem has been successfully installed and is accessible. This command should output the installed Rails version.

```bash
$
rails --version
```

--------------------------------

### Index Article View in Rails ERB

Source: https://guides.rubyonrails.org/v4.1/getting_started

An ERB template for listing all articles in a table format. It iterates over the '@articles' collection passed from the controller, displaying the title and text for each article. Includes table headers for clarity.

```html
<h1>Listing articles</h1>
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
  </tr>
  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
    </tr>
  <% end %>
</table>
```

--------------------------------

### Install Rails Gem

Source: https://guides.rubyonrails.org/v2.3/getting_started

This command installs the Rails framework using RubyGems, the Ruby package manager. Ensure Ruby and RubyGems are installed on your system before running this command.

```bash
$ gem install rails
```

--------------------------------

### Get Substring from Position (Ruby)

Source: https://guides.rubyonrails.org/v4.2/active_support_core_extensions

Extracts a substring starting from a given position to the end of the string. Handles positive, negative, and out-of-bounds indices.

```Ruby
"hello".from(0)   # => "hello"
"hello".from(2)   # => "llo"
"hello".from(-2)  # => "lo"
"hello".from(10)  # => "" if < 1.9, nil in 1.9
```

--------------------------------

### Show Post View in ERB

Source: https://guides.rubyonrails.org/v4.0/getting_started

This ERB template file displays the details of a single post, including its title and text. It accesses the post object through the @post instance variable passed from the controller.

```erb
<p>
  <strong>Title:</strong>
  <%= @post.title %>
</p>
<p>
  <strong>Text:</strong>
  <%= @post.text %>
</p>
```

--------------------------------

### Product Inventory Partial (ERB)

Source: https://guides.rubyonrails.org/getting_started

A Rails partial that displays the product's inventory count if available, or an 'Out of stock' message along with a subscription form. This partial is rendered on the product show page.

```erb
<% if product.inventory_count? %>
  <p><%= product.inventory_count %> in stock</p>
<% else %>
  <p>Out of stock</p>
  <p>Email me when available.</p>

  <%= form_with model: [product, Subscriber.new] do |form| %>
    <%= form.email_field :email, placeholder: "you@example.com", required: true %>
    <%= form.submit "Submit" %>
  <% end %>
<% end %>
```

--------------------------------

### Add 'Back' Link to Show Post View (Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This code adds a 'Back' link to the show post view, enabling users to navigate back to the list of all posts. It employs the `posts_path` helper.

```erb
<p>  <strong>Title:</strong>  <%= @post.title %></p>
<p>  <strong>Text:</strong>  <%= @post.text %></p>
<%= link_to 'Back', posts_path %>
```

--------------------------------

### Rails Article Show View with Comments

Source: https://guides.rubyonrails.org/v4.1/getting_started

This ERB code displays an article's details, followed by a list of existing comments. It then includes a form for adding new comments and links to edit the article or return to the articles list.

```erb
<p><strong>Title:</strong> <%= @article.title %></p>
<p><strong>Text:</strong> <%= @article.text %></p>

<h2>Comments</h2>
<% @article.comments.each do |comment| %>
  <p>
    <strong>Commenter:</strong>
    <%= comment.commenter %>
  </p>
  <p>
    <strong>Comment:</strong>
    <%= comment.body %>
  </p>
<% end %>

<h2>Add a comment:</h2>
<%= form_for([@article, @article.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br>
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br>
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>

<%= link_to 'Edit Article', edit_article_path(@article) %> |
<%= link_to 'Back to Articles', articles_path %>
```

--------------------------------

### Running Rails Application with rackup

Source: https://guides.rubyonrails.org/v5.0/rails_on_rack

Shows how to configure and run a Rails application using `rackup` by creating a `config.ru` file. It specifies the required setup to load the Rails environment and run the application.

```ruby
# Rails.root/config.ru
require ::File.expand_path('../config/environment', __FILE__)
run Rails.application
```

--------------------------------

### Verify Ruby Installation

Source: https://guides.rubyonrails.org/install_ruby_on_rails

Checks if Ruby is installed correctly by displaying its version number.

```shell
$ ruby --version

```

--------------------------------

### Install Ruby on Windows (WSL) using Mise

Source: https://guides.rubyonrails.org/install_ruby_on_rails

Installs build dependencies, Mise version manager, and Ruby globally within an Ubuntu WSL environment on Windows. Assumes Ubuntu is already installed.

```shell
# Install dependencies with apt
$ sudo apt update
$ sudo apt install build-essential rustc libssl-dev libyaml-dev zlib1g-dev libgmp-dev

# Install Mise version manager
$ curl https://mise.run | sh
$ echo 'eval "$(~/.local/bin/mise activate bash)"' >> ~/.bashrc
$ source ~/.bashrc

# Install Ruby globally with Mise
$ mise use -g ruby@3

```

--------------------------------

### Start Services on macOS

Source: https://guides.rubyonrails.org/v6.0/development_dependencies_install

This command lists all available Homebrew services and is used to start individual services like MySQL, PostgreSQL, or Redis on macOS. You need to replace 'mysql' with the specific service name you wish to start.

```bash
brew services list
brew services start mysql
```

--------------------------------

### Add Inventory Validation (Ruby)

Source: https://guides.rubyonrails.org/getting_started

Adds a validation to the Product model to ensure that the `inventory_count` is never negative. This helps maintain data integrity for stock levels.

```ruby
class Product < ApplicationRecord
  has_one_attached :featured_image
  has_rich_text :description

  validates :name, presence: true
  validates :inventory_count, numericality: { greater_than_or_equal_to: 0 }
end
```

--------------------------------

### Start a Homebrew Service on macOS

Source: https://guides.rubyonrails.org/v6.1/development_dependencies_install

Starts a specific service managed by Homebrew on macOS. Replace 'mysql' with the actual service name you wish to start, such as postgresql, redis, etc.

```shell
brew services start mysql
```

--------------------------------

### Ruby on Rails: Start Development Server

Source: https://guides.rubyonrails.org/v6.0/command_line

Starts the built-in web server for development. This allows you to test your Rails application locally in a browser.

```bash
rails server
```

--------------------------------

### Rails Server Start Logic

Source: https://guides.rubyonrails.org/initialization

The `Rails::Server#start` method initializes server-specific configurations like signal traps, temporary directories, and development caching before calling the parent `Rackup::Server#start` method. It ensures necessary directories are created and logging is set up.

```ruby
module Rails
  class Server < ::Rackup::Server
    def start(after_stop_callback = nil)
      trap(:INT) { exit }
      create_tmp_directories
      setup_dev_caching
      log_to_stdout if options[:log_stdout]

      super()
      # ...
    end

    private
      def setup_dev_caching
        if options[:environment] == "development"
          Rails::DevCaching.enable_by_argument(options[:caching])
        end
      end

      def create_tmp_directories
        %w(cache pids sockets).each do |dir_to_make|
          FileUtils.mkdir_p(File.join(Rails.root, "tmp", dir_to_make))
        end
      end

      def log_to_stdout
        wrapped_app # touch the app so the logger is set up

        console = ActiveSupport::Logger.new(STDOUT)
        console.formatter = Rails.logger.formatter
        console.level = Rails.logger.level

        unless ActiveSupport::Logger.logger_outputs_to?(Rails.logger, STDERR, STDOUT)
          Rails.logger.broadcast_to(console)
        end
      end
  end
end
```

--------------------------------

### Output of Rails Routes Command

Source: https://guides.rubyonrails.org/v6.0/getting_started

This is the output generated by running the `rails routes` command in a Rails application. It lists all defined routes, including their associated HTTP verbs, URI patterns, and the controller#action pairs they map to. This output helps in understanding the available endpoints and how they are configured.

```bash
$ rails routes
      Prefix Verb      URI Pattern               Controller#Action
   welcome_index GET       /welcome/index(.:format)  welcome#index
        articles GET       /articles(.:format)       articles#index
                POST      /articles(.:format)       articles#create
     new_article GET       /articles/new(.:format)   articles#new
    edit_article GET       /articles/:id/edit(.:format) articles#edit
         article GET       /articles/:id(.:format)   articles#show
                PATCH     /articles/:id(.:format)   articles#update
                PUT       /articles/:id(.:format)   articles#update
                DELETE    /articles/:id(.:format)   articles#destroy
          root GET       /                         welcome#index
```

--------------------------------

### Generate Article model with attributes (Bash)

Source: https://guides.rubyonrails.org/v4.1/getting_started

This Bash command utilizes the Rails generator to create a new model named `Article`. It specifies two attributes: `title` as a string and `text` as a text type. This command also sets up the corresponding database migration.

```bash
$ bin/rails generate model Article title:string text:text
```

--------------------------------

### Database Configuration for PostgreSQL

Source: https://guides.rubyonrails.org/command_line

Example `config/database.yml` snippet for a Rails application configured to use PostgreSQL. It outlines adapter settings, connection pooling, and development environment configuration. Assumes the `pg` gem is installed.

```yaml
# PostgreSQL. Versions 9.3 and up are supported.
#
# Install the pg driver:
#   gem install pg
# On macOS with Homebrew:
#   gem install pg -- --with-pg-config=/usr/local/bin/pg_config
# On Windows:
#   gem install pg
#       Choose the win32 build.
#       Install PostgreSQL and put its /bin directory on your path.
#
# Configure Using Gemfile
# gem "pg"
#
default: &default
  adapter: postgresql
  encoding: unicode

  # For details on connection pooling, see Rails configuration guide
  # https://guides.rubyonrails.org/configuring.html#database-pooling
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

development:
  <<: *default
  database: petstore_development
...

```

--------------------------------

### Permit Inventory Count Parameter (Ruby)

Source: https://guides.rubyonrails.org/getting_started

Modifies the `product_params` method in a Rails controller to permit the `:inventory_count` attribute. This is necessary for strong parameters to allow the update.

```ruby
def product_params
  params.expect(product: [ :name, :description, :featured_image, :inventory_count ])
end
```

--------------------------------

### Start Rails Development Server

Source: https://guides.rubyonrails.org/v7.0/command_line

Command to start the Rails development server. This command boots up the application, making it accessible via a local web server, typically on `http://localhost:3000`.

```bash
$ bin/rails server
=> Booting Puma...


```

--------------------------------

### Create New Article View Template in Rails

Source: https://guides.rubyonrails.org/v4.1/getting_started

This ERB template is responsible for rendering the 'New Article' page. It defines the HTML structure for the page, including a heading. This file should be placed in `app/views/articles/new.html.erb` to be rendered by the `new` action in ArticlesController.

```html
<h1>New Article</h1>
```

--------------------------------

### Update Product Form (ERB)

Source: https://guides.rubyonrails.org/getting_started

Adds an inventory count input field to the product form in the Rails view. This allows users to input or update the stock quantity.

```erb
<%= form_with model: product do |form| %>
  <%# ... %>

  <div>
    <%= form.label :inventory_count, style: "display: block" %>
    <%= form.number_field :inventory_count %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```

--------------------------------

### Declare Article Resource in Rails Routes

Source: https://guides.rubyonrails.org/v4.1/getting_started

This snippet demonstrates how to declare a RESTful resource, specifically ':articles', within the routes.rb file. This automatically generates routes for standard CRUD operations on articles.

```ruby
Rails.application.routes.draw do
  resources :articles
  root 'welcome#index'
end
```

--------------------------------

### Rails Database Migration for Creating a Table

Source: https://guides.rubyonrails.org/v6.1/getting_started

Define the structure of a database table using a Rails migration file. This example shows how to create an `articles` table with `title` and `text` columns, along with `created_at` and `updated_at` timestamps managed by `t.timestamps`.

```ruby
class CreateArticles < ActiveRecord::Migration[6.0]
  def change
    create_table :articles do |t|
      t.string :title
      t.text :body

      t.timestamps
    end
  end
end

```

--------------------------------

### Server Integration: Mongrel's `run` Method

Source: https://guides.rubyonrails.org/v4.1/initialization

This Ruby code demonstrates how a server like Mongrel integrates with Rack. The `run` method initializes the Mongrel HTTP server with various options and registers the Rack application, handling different mapping strategies for URLs.

```ruby
def self.run(app, options={})
  server = ::Mongrel::HttpServer.new(
    options[:Host]          || '0.0.0.0',
    options[:Port]          || 8080,
    options[:num_processors] || 950,
    options[:throttle]      || 0,
    options[:timeout]       || 60
  )
  # Acts like Rack::URLMap, utilizing Mongrel's own path finding methods.
  # Use is similar to #run, replacing the app argument with a hash of
  # { path=>app, ... } or an instance of Rack::URLMap.
  if options[:map]
    if app.is_a? Hash
      app.each do |path, appl|
        path = '/' + path unless path[0] == ?/
        server.register(path, Rack::Handler::Mongrel.new(appl))
      end
    elsif app.is_a? URLMap
      app.instance_variable_get(:@mapping).each do |(host, path, appl)||
        next if !host.nil? && !options[:Host].nil? && options[:Host] != host
        path = '/' + path unless path[0] == ?/
        server.register(path, Rack::Handler::Mongrel.new(appl))
      end
    else
      raise ArgumentError, "first argument should be a Hash or URLMap"
    end
  else
    server.register('/', Rack::Handler::Mongrel.new(app))
  end
  yield server if block_given?
  server.run.join
end
```

--------------------------------

### Generating HTML Guides with Rake

Source: https://guides.rubyonrails.org/v4.0/ruby_on_rails_guides_guidelines

This snippet shows how to generate HTML versions of the Ruby on Rails guides. It requires Bundler to be installed and utilizes rake tasks for the generation process. Environment variables like `ONLY`, `ALL`, `WARNINGS`, and `GUIDES_LANGUAGE` can be used to customize the generation.

```Shell
bundle exec rake guides:generate

```

```Shell
bundle exec rake guides:generate:html

```

```Shell
touch my_guide.md
bundle exec rake guides:generate ONLY=my_guide

```

```Shell
bundle exec rake guides:generate ALL=1 WARNINGS=1

```

```Shell
bundle exec rake guides:generate GUIDES_LANGUAGE=es

```

```Shell
rake

```

--------------------------------

### Create Basic ERB View Template

Source: https://guides.rubyonrails.org/v4.0/getting_started

This ERB (Embedded Ruby) code creates a simple HTML view. It defines an H1 heading that will be displayed when the 'new' action of the PostsController is rendered.

```html+erb
<h1>New Post</h1>
```

--------------------------------

### Basic Rails Application Template Example

Source: https://guides.rubyonrails.org/v4.0/rails_application_templates

A simple Rails application template demonstrating the use of `generate`, `route`, `rake`, and `git` commands within a template file. This template scaffolds a 'person' resource, sets a root route, runs database migrations, and initializes a Git repository.

```ruby
generate(:scaffold, "person name:string")
route "root to: 'people#index'"
rake("db:migrate")
git :init
git add: "."
git commit: %Q{"-m 'Initial commit'"}
```

--------------------------------

### Segment Constraints for Sharing Root Namespace in Rails

Source: https://guides.rubyonrails.org/v3.1/routing

Shows how segment constraints can be used to allow different route patterns to share the root namespace. This example allows ':id' to start with a number and ':username' not to.

```ruby
match '/:id' => 'posts#show', :constraints => { :id => /\d.+/ }
match '/:username' => 'users#show'
```

--------------------------------

### Configure Action Cable Log Tags

Source: https://guides.rubyonrails.org/v6.0/action_cable_overview

Defines log tags for the per-connection logger. This example includes user account ID (or 'no-account'), the string 'action_cable', and the request UUID.

```ruby
config.action_cable.log_tags = [
  -> request { request.env['user_account_id'] || 'no-account' },
  :action_cable,
  -> request { request.uuid }
]
```

--------------------------------

### Example Rails Application Template

Source: https://guides.rubyonrails.org/v5.2/rails_application_templates

An example of a typical Ruby on Rails application template (`template.rb`) demonstrating the use of core Template API methods like `generate`, `route`, `rails_command`, and `after_bundle` for Git initialization.

```ruby
# template.rb
generate(:scaffold, "person name:string")
route "root to: 'people#index'"
rails_command("db:migrate")

after_bundle do
  git :init
  git add: "."
  git commit: "-m 'Initial commit'"
end
```

--------------------------------

### Generate Articles Controller in Rails

Source: https://guides.rubyonrails.org/v4.1/getting_started

This command generates a new controller named ArticlesController in a Ruby on Rails application. It sets up the basic file structure for the controller, making it ready to define actions for handling article-related requests.

```bash
bin/rails g controller articles
```

--------------------------------

### Markdown Headings Example

Source: https://guides.rubyonrails.org/v5.1/ruby_on_rails_guides_guidelines

Examples of Markdown heading syntax used in Ruby on Rails Guides. This includes `h1` for the guide title, `h2` for sections, `h3` for subsections, and demonstrates proper capitalization and inline formatting.

```markdown
Guide Title
===========

Section
-------

### Sub Section

```

```markdown
#### Middleware Stack is an Array

```

```markdown
#### When are Objects Saved?

```

```markdown
##### The `:content_type` Option

```

--------------------------------

### Rails Application Update Task Example

Source: https://guides.rubyonrails.org/v7.2/upgrading_ruby_on_rails

Demonstrates the usage of the `bin/rails app:update` command after changing the Rails version in the Gemfile. It shows an example of the interactive prompt for handling configuration file updates.

```bash
$ bin/rails app:update
       exist  config
    conflict  config/application.rb
Overwrite /myapp/config/application.rb? (enter "h" for help) [Ynaqdh]
       force  config/application.rb
      create  config/initializers/new_framework_defaults_7_2.rb
...
```

--------------------------------

### API Linking Examples

Source: https://guides.rubyonrails.org/v5.1/ruby_on_rails_guides_guidelines

Illustrates how to correctly link to the Ruby on Rails API documentation. It shows the format for links with release tags (which remain untouched) and without release tags (which are modified based on whether edge or release guides are being generated).

```http
http://api.rubyonrails.org/v5.0.1/classes/ActiveRecord/Attributes/ClassMethods.html

```

```http
http://api.rubyonrails.org/classes/ActionDispatch/Response.html

```

```http
http://edgeapi.rubyonrails.org/classes/ActionDispatch/Response.html

```

```http
http://api.rubyonrails.org/v5.1.0/classes/ActionDispatch/Response.html

```

--------------------------------

### Start and Use Rails Console

Source: https://guides.rubyonrails.org/getting_started

This command launches the interactive Rails console, which allows developers to execute Ruby code within the context of their Rails application. It's useful for testing code, inspecting data, and debugging. The console provides a prompt to enter commands and see immediate results.

```bash
$ bin/rails console

```

```ruby
store(dev)> Rails.version
=> "8.0.0"

```

--------------------------------

### Set Root Path in Rails Routing

Source: https://guides.rubyonrails.org/v6.1/getting_started

Configure the `config/routes.rb` file to set the application's root path to a specific controller and action. This example maps the root URL to the `index` action of the `ArticlesController`.

```ruby
Rails.application.routes.draw do
  root "articles#index"

  get "/articles", to: "articles#index"
end

```

--------------------------------

### Rails Server Start Method and Initialization

Source: https://guides.rubyonrails.org/v4.0/initialization

This Ruby method, `Rails::Server#start`, is responsible for initiating the Rails server. It sets up the server URL, displays startup information, handles interrupt signals (Ctrl+C), creates necessary temporary directories, and configures logging before calling the parent `Rack::Server.start` method.

```ruby
def start
  url = "#{options[:SSLEnable] ? 'https' : 'http'}://#{options[:Host]}:#{options[:Port]}"
  puts "=> Booting #{ActiveSupport::Inflector.demodulize(server)}"
  puts "=> Rails #{Rails.version} application starting in #{Rails.env} on #{url}"
  puts "=> Run `rails server -h` for more startup options"
  trap(:INT) { exit }
  puts "=> Ctrl-C to shutdown server" unless options[:daemonize]
  #Create required tmp directories if not found
  %w(cache pids sessions sockets).each do |dir_to_make|
    FileUtils.mkdir_p(Rails.root.join('tmp', dir_to_make))
  end
  unless options[:daemonize]
    wrapped_app # touch the app so the logger is set up
    console = ActiveSupport::Logger.new($stdout)
    console.formatter = Rails.logger.formatter
    Rails.logger.extend(ActiveSupport::Logger.broadcast(console))
  end
  super
ensure
  # The '-h' option calls exit before @options is set.
  # If we call 'options' with it unset, we get double help banners.
  puts 'Exiting' unless @options && options[:daemonize]
end
```

--------------------------------

### Starting Rails Server with Rack::Server

Source: https://guides.rubyonrails.org/rails_on_rack

Demonstrates how the `bin/rails server` command initializes a `Rack::Server` object and starts the web server. This involves requiring the application path, changing the directory, and then calling the server's start method.

```ruby
Rails::Server.new.tap do |server|
  require APP_PATH
  Dir.chdir(Rails.application.root)
  server.start
end
```

```ruby
class Server < ::Rack::Server
  def start
    # ...
    super
  end
end
```

--------------------------------

### Get Module Parent Chain with module_parents (Ruby)

Source: https://guides.rubyonrails.org/active_support_core_extensions

The `module_parents` method returns an array of all parent modules, starting from the immediate parent up to `Object`, for a given module.

```ruby
module X
  module Y
    module Z
    end
  end
end
M = X::Y::Z

X::Y::Z.module_parents # => [X::Y, X, Object]
M.module_parents       # => [X::Y, X, Object]
```

--------------------------------

### Comment Model Association in Rails

Source: https://guides.rubyonrails.org/v4.1/getting_started

Defines the association for the Comment model. It belongs to an Article, establishing a one-to-many relationship from the Article's perspective. This is a core part of Active Record associations.

```ruby
class Comment < ActiveRecord::Base
  belongs_to :article
end
```

--------------------------------

### Initialize Rails App with PostgreSQL and Git

Source: https://guides.rubyonrails.org/v6.0/command_line

This snippet demonstrates the command-line process for creating a new Rails application. It includes initializing a Git repository and specifying PostgreSQL as the database. The output shows the files created by the Rails generator.

```bash
$ mkdir gitapp
$ cd gitapp
$ git init
Initialized empty Git repository in .git/
$ rails new . --git --database=postgresql
     exists  app/controllers
     exists  app/helpers
... 
     create  tmp/cache
     create  tmp/pids
     create  Rakefile
add 'Rakefile'
     create  README.md
add 'README.md'
     create  app/controllers/application_controller.rb
add 'app/controllers/application_controller.rb'
     create  app/helpers/application_helper.rb
... 
     create  log/test.log
add 'log/test.log'
```

--------------------------------

### Install Action Mailbox and Migrate Database in Rails

Source: https://guides.rubyonrails.org/v7.0/action_mailbox_basics

This snippet shows the commands to install the necessary migrations for Action Mailbox's InboundEmail records and then apply those migrations to the database. Ensure Active Storage is set up prior to running these commands.

```bash
$ bin/rails action_mailbox:install
$ bin/rails db:migrate

```

--------------------------------

### Running Database Migrations in Ruby on Rails

Source: https://guides.rubyonrails.org/v6.0/getting_started

These commands demonstrate how to execute database migrations in Ruby on Rails. The primary command is `rails db:migrate`, which applies pending migrations. You can also specify a target environment, such as production, using `RAILS_ENV=production`.

```bash
$ rails db:migrate
```

```bash
rails db:migrate RAILS_ENV=production
```

--------------------------------

### Ruby on Rails: Create Database Table Migration

Source: https://guides.rubyonrails.org/v4.1/getting_started

This Ruby code defines a database migration for creating an 'articles' table. It specifies columns for 'title' (string) and 'text' (text), and includes timestamps for tracking creation and update times. This migration is reversible.

```ruby
class CreateArticles < ActiveRecord::Migration
  def change
    create_table :articles do |t|
      t.string :title
      t.text :text
      t.timestamps
    end
  end
end
```

--------------------------------

### Rails Routes Output Example

Source: https://guides.rubyonrails.org/v5.2/getting_started

This is an example output from the `bin/rails routes` command, illustrating how different URI patterns are mapped to specific controller actions. It shows the `articles` resource routes, including the `POST /articles` route used for creating new articles.

```text
$ bin/rails routes
       Prefix Verb   URI Pattern                  Controller#Action
    welcome_index GET    /welcome/index(.:format)     welcome#index
         articles GET    /articles(.:format)          articles#index
                  POST   /articles(.:format)          articles#create
      new_article GET    /articles/new(.:format)      articles#new
     edit_article GET    /articles/:id/edit(.:format) articles#edit
          article GET    /articles/:id(.:format)      articles#show
                  PATCH  /articles/:id(.:format)      articles#update
                  PUT    /articles/:id(.:format)      articles#update
                  DELETE /articles/:id(.:format)      articles#destroy
           root GET    /                            welcome#index
```

--------------------------------

### Install and Migrate Active Storage - Ruby

Source: https://guides.rubyonrails.org/v7.2/active_storage_overview

Installs Active Storage by creating necessary configuration files and migrating the database to add the required tables: `active_storage_blobs`, `active_storage_attachments`, and `active_storage_variant_records`.

```bash
$ bin/rails active_storage:install
$ bin/rails db:migrate

```

--------------------------------

### Create Comments Migration in Rails

Source: https://guides.rubyonrails.org/v6.0/getting_started

This migration defines the 'comments' table schema. It includes columns for 'commenter' (string), 'body' (text), and 'article_id' (integer with foreign key constraint), along with timestamps.

```ruby
class CreateComments < ActiveRecord::Migration[6.0]
  def change
    create_table :comments do |t|
      t.string :commenter
      t.text :body
      t.references :article, null: false, foreign_key: true
      t.timestamps
    end
  end
end
```

--------------------------------

### Rails 3 Railties Application Namespacing and Loading

Source: https://guides.rubyonrails.org/v4.1/3_0_release_notes

In Rails 3, each application gets its own namespace, started with `YourAppName.boot`. Files under `Rails.root/app` are automatically added to the load path, simplifying application interaction and file loading.

```ruby
YourAppName.boot
app/observers/user_observer.rb
```

--------------------------------

### Index View for Listing Posts in ERB

Source: https://guides.rubyonrails.org/v4.0/getting_started

This ERB template file generates an HTML table to list all posts. It iterates over the @posts collection passed from the controller, displaying the title and text for each post in a table row.

```erb
<h1>Listing posts</h1>
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
  </tr>
  <% @posts.each do |post| %>
    <tr>
      <td><%= post.title %></td>
      <td><%= post.text %></td>
    </tr>
  <% end %>
</table>
```

--------------------------------

### Dev Container CLI Setup and Execution

Source: https://guides.rubyonrails.org/contributing_to_ruby_on_rails

This sequence sets up and utilizes the Dev Container CLI for a Rails development environment. It involves global npm installation, navigating to the Rails directory, and then starting and executing commands within the development container.

```bash
$ npm install -g @devcontainers/cli
$ cd rails
$ devcontainer up --workspace-folder .
$ devcontainer exec --workspace-folder . bash

```

--------------------------------

### Inspect Product Model Columns in Ruby

Source: https://guides.rubyonrails.org/getting_started

Illustrates how to inspect the column names detected by Rails for the Product model by calling the .column_names method. This helps in understanding the attributes Rails has dynamically generated.

```ruby
Product.column_names
```

--------------------------------

### Generate Product Mailer in Rails

Source: https://guides.rubyonrails.org/getting_started

Generates a mailer class for handling product-related emails, specifically an 'in_stock' method to notify subscribers. This command creates the necessary file structure for the mailer and its associated views.

```bash
bin/rails g mailer Product in_stock
```

--------------------------------

### Securely Store Passwords with ActiveModel::SecurePassword

Source: https://guides.rubyonrails.org/v7.1/active_model_basics

Provides an example of using ActiveModel::SecurePassword to securely hash and authenticate passwords. It includes setup, validations, and usage of `has_secure_password` and authentication methods.

```ruby
class Person
  include ActiveModel::SecurePassword
  has_secure_password
  has_secure_password :recovery_password, validations: false

  attr_accessor :password_digest, :recovery_password_digest
end

# Example Usage:
irb> person = Person.new

# Validations:
irb> person.valid?
=> false
irb> person.password = 'aditya'
irb> person.password_confirmation = 'nomatch'
irb> person.valid?
=> false
irb> person.password = person.password_confirmation = 'a' * 100
irb> person.valid?
=> false
irb> person.password = person.password_confirmation = 'aditya'
irb> person.valid?
=> true

irb> person.recovery_password = "42password"

# Authentication:
irb> person.authenticate('aditya')
=> #<Person>
irb> person.authenticate('notright')
=> false
irb> person.authenticate_password('aditya')
=> #<Person>
irb> person.authenticate_password('notright')
=> false
irb> person.authenticate_recovery_password('42password')
=> #<Person>
irb> person.authenticate_recovery_password('notright')
=> false

# Digests:
irb> person.password_digest
=> "$2a$04$gF8RfZdoXHvyTjHhiU4ZsO.kQqV9oonYZu31PRE4hLQn3xM2qkpIy"
irb> person.recovery_password_digest
=> "$2a$04$iOfhwahFymCs5weB3BNH/uXkTG65HR.qpW.bNhEjFP3ftli3o5DQC"

```

--------------------------------

### Example Functional Test for 'index' Action (Rails)

Source: https://guides.rubyonrails.org/v6.1/testing

A basic functional test for the 'index' action of a Rails controller. It asserts that a GET request to the articles URL results in a successful response.

```ruby
# articles_controller_test.rb
class ArticlesControllerTest < ActionDispatch::IntegrationTest
  test "should get index" do
    get articles_url
    assert_response :success
  end
end

```

--------------------------------

### Configure HTML Guide Generation with Rake

Source: https://guides.rubyonrails.org/v4.2/ruby_on_rails_guides_guidelines

Demonstrates configuring HTML guide generation using environment variables. `ALL=1` forces processing of all guides, and `WARNINGS=1` enables duplicate ID and broken link detection. `GUIDES_LANGUAGE` specifies the output language.

```bash
bundle exec rake guides:generate ALL=1 WARNINGS=1
```

```bash
bundle exec rake guides:generate GUIDES_LANGUAGE=es
```

--------------------------------

### Generate Ruby on Rails Post Model

Source: https://guides.rubyonrails.org/v4.0/getting_started

This command generates a new Post model in a Ruby on Rails application, defining 'title' as a string and 'text' as a text attribute. It also creates a corresponding database migration file.

```bash
$ rails generate model Post title:string text:text
```

--------------------------------

### Create Action in CommentsController (Ruby on Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

The `create` action in the `CommentsController` handles the submission of new comments. It finds the associated post, creates a new comment using the permitted parameters, and then redirects the user back to the post's show page.

```ruby
class CommentsController < ApplicationController
  def create
    @post = Post.find(params[:post_id])
    @comment = @post.comments.create(params[:comment].permit(:commenter, :body))
    redirect_to post_path(@post)
  end
end
```

--------------------------------

### Map Route to Controller Action with String in Rails

Source: https://guides.rubyonrails.org/v4.0/routing

This example shows how to map a GET request for a specific path to a controller action using a string format. The string specifies the controller and action separated by a '#'.

```ruby
get 'profile', to: 'users#show'
```

--------------------------------

### Rails render_to_string Example - Ruby

Source: https://guides.rubyonrails.org/v2.3/layouts_and_rendering

Illustrates how to use `render_to_string` in Rails to get the rendered output as a string without sending it as a browser response. This method accepts the same options as the `render` method.

```ruby
render_to_string :action => "show", :layout => false
```

--------------------------------

### Define Rails Controller Action

Source: https://guides.rubyonrails.org/v4.0/getting_started

This Ruby code defines a 'new' action within the PostsController. Public methods defined in a controller serve as actions, responding to specific routes and potentially rendering views.

```ruby
def new
end
```

--------------------------------

### Rails Server Initialization (Ruby)

Source: https://guides.rubyonrails.org/v4.0/rails_on_rack

Demonstrates how `rails server` creates and starts a `Rack::Server` object for a Rails application. It shows the inheritance from `Rack::Server` and the call to `super` within the `start` method.

```ruby
Rails::Server.new.tap do |server|
  require APP_PATH
  Dir.chdir(Rails.application.root)
  server.start
end
```

```ruby
class Server < ::Rack::Server
  def start
    ...
    super
  end
end
```

--------------------------------

### Start Rails Development Server with `bin/rails server`

Source: https://guides.rubyonrails.org/v6.1/command_line

The `bin/rails server` command starts the Puma web server for your Rails application, making it accessible via a web browser. You can customize the environment, port, IP binding, and run it as a daemon.

```bash
$ cd commandsapp
$ bin/rails server
=> Booting Puma
=> Rails 6.0.0 application starting in development
=> Run `bin/rails server --help` for more startup options
Puma starting in single mode...
* Version 3.12.1 (ruby 2.5.7-p206), codename: Llamas in Pajamas
* Min threads: 5, max threads: 5
* Environment: development
* Listening on tcp://localhost:3000
Use Ctrl-C to stop

```

```bash
$ bin/rails server -e production -p 4000
```

```bash
$ bin/rails server -d
```

--------------------------------

### Define Rails Resource Routes

Source: https://guides.rubyonrails.org/getting_started

This Rails code snippet uses the 'resources' helper to automatically define all standard CRUD routes for the 'products' resource. It's a concise way to set up common routes, reducing boilerplate code and ensuring consistency.

```ruby
resources :products

```

--------------------------------

### Install Project Dependencies and Run Tests

Source: https://guides.rubyonrails.org/v4.0/development_dependencies_install

Installs all project dependencies using Bundler, excluding MySQL and PostgreSQL drivers. It then runs the full test suite for the Ruby on Rails project using the Rake task.

```bash
$ bundle install --without db
$ bundle exec rake test
```

--------------------------------

### Generate Comment Model in Rails

Source: https://guides.rubyonrails.org/v4.1/getting_started

This command generates a new Comment model with specified attributes (commenter, body) and a reference to the Article model. It also creates associated migration, test files, and fixture data.

```bash
$ bin/rails generate model Comment commenter:string body:text article:references
```

--------------------------------

### Define Basic Active Record Model in Ruby

Source: https://guides.rubyonrails.org/getting_started

Defines a basic Active Record model named 'Product' that inherits from 'ApplicationRecord'. Rails automatically infers database columns and types from the 'products' table.

```ruby
class Product < ApplicationRecord
end
```

--------------------------------

### Rails Seed Data for Initial Products

Source: https://guides.rubyonrails.org/v4.0/migrations

This Ruby code snippet demonstrates how to use Rails' `db/seeds.rb` file to populate the database with initial product data. It's a straightforward way to set up a blank application's database.

```ruby
5.times do |i|
  Product.create(name: "Product ##{i}", description: "A product.")
end
```

--------------------------------

### Generate All Rails Guides (Ruby)

Source: https://guides.rubyonrails.org/v6.1/ruby_on_rails_guides_guidelines

This rake task generates all the guides in HTML format. It requires running 'bundle install' first. The generated HTML files are placed in the './output' directory.

```ruby
bundle exec rake guides:generate

```

--------------------------------

### Get Module Hierarchy with module_parents

Source: https://guides.rubyonrails.org/v6.0/active_support_core_extensions

The `module_parents` method returns an array of a module's ancestors, starting from its immediate parent up to `Object`. This is useful for understanding the inheritance chain of a module.

```ruby
module X
  module Y
    module Z
    end
  end
end
M = X::Y::Z
puts M.module_parents # => [X::Y, X, Object]
puts M.module_parents # => [X::Y, X, Object]
```

--------------------------------

### Test Sending an In Stock Email in Rails Console

Source: https://guides.rubyonrails.org/getting_started

Demonstrates how to manually trigger an 'in_stock' email from the Rails console. It involves fetching a product, finding or creating a subscriber, and then delivering the email asynchronously using `deliver_later`.

```ruby
store(dev)> product = Product.first
store(dev)> subscriber = product.subscribers.find_or_create_by(email: "subscriber@example.org")
store(dev)> ProductMailer.with(product: product, subscriber: subscriber).in_stock.deliver_later
```

--------------------------------

### Get All Parent Modules with parents (Ruby)

Source: https://guides.rubyonrails.org/v3.1/active_support_core_extensions

The `parents` method returns an array of all ancestor modules, starting from the immediate parent up to `Object`. This provides a complete chain of module containment.

```ruby
module X
  module Y
    module Z
    end
  end
end
M = X::Y::Z

X::Y::Z.parents  # => [X::Y, X, Object]
M.parents        # => [X::Y, X, Object]
```

--------------------------------

### Preconfigure Database with `rails new`

Source: https://guides.rubyonrails.org/command_line

Creates a new Rails application while preconfiguring the database adapter. For example, `--database=postgresql` sets up the application to use PostgreSQL. This requires the corresponding database driver gem to be installed.

```shell
$ rails new petstore --database=postgresql
      create
      create  app/controllers
      create  app/helpers
...

```

--------------------------------

### Plugin Test Helper Setup

Source: https://guides.rubyonrails.org/v3.0/plugins

This Ruby file sets up the testing environment for a Rails plugin. It configures the `RAILS_ENV`, loads the environment, establishes a database connection based on the `database.yml` and `DB` environment variable, and loads the schema.

```ruby
# vendor/plugins/yaffle/test/test_helper.rb
ENV['RAILS_ENV'] = 'test'
ENV['RAILS_ROOT'] ||= File.dirname(__FILE__) + '/../../../..'
require 'test/unit'
require File.expand_path(File.join(ENV['RAILS_ROOT'], 'config/environment.rb'))

def load_schema
  config = YAML::load(IO.read(File.dirname(__FILE__) + '/database.yml'))
  ActiveRecord::Base.logger = Logger.new(File.dirname(__FILE__) + "/debug.log")
  db_adapter = ENV['DB']
  # no db passed, try one of these fine config-free DBs before bombing.
  db_adapter ||= 
    begin
      require 'rubygems'
      require 'sqlite'
      'sqlite'
    rescue MissingSourceFile
      begin
        require 'sqlite3'
        'sqlite3'
      rescue MissingSourceFile
      end
    end
  if db_adapter.nil?
    raise "No DB Adapter selected. Pass the DB= option to pick one, or install Sqlite or Sqlite3."
  end
  ActiveRecord::Base.establish_connection(config[db_adapter])
  load(File.dirname(__FILE__) + "/schema.rb")
  require File.dirname(__FILE__) + '/../rails/init'
end
```

--------------------------------

### Ruby on Rails: Create a New Application

Source: https://guides.rubyonrails.org/v6.0/command_line

Initializes a new Ruby on Rails application with a standard directory structure and essential configuration files. Requires the Rails gem to be installed.

```bash
$ rails new commandsapp
```

--------------------------------

### List Available Services with Homebrew on macOS

Source: https://guides.rubyonrails.org/v6.1/development_dependencies_install

Lists all services managed by Homebrew on macOS. This is useful for identifying the names of services like databases or caches that need to be started for Rails development.

```shell
brew services list
```

--------------------------------

### Rackup::Server Initialize Method in Ruby

Source: https://guides.rubyonrails.org/initialization

The initialize method of Rackup::Server sets up instance variables based on provided options or parses command-line arguments if no options are given. It handles the application instance and default option behavior.

```ruby
module Rackup
  class Server
    def initialize(options = nil)
      @ignore_options = []

      if options
        @use_default_options = false
        @options = options
        @app = options[:app] if options[:app]
      else
        @use_default_options = true
        @options = parse_options(ARGV)
      end
    end
  end
end
```

--------------------------------

### Generate HTML Rails Guides (Ruby)

Source: https://guides.rubyonrails.org/v6.1/ruby_on_rails_guides_guidelines

This rake task specifically generates the guides in HTML format. It's an alternative to the general 'guides:generate' task. Ensure 'bundle install' has been executed prior to running.

```ruby
bundle exec rake guides:generate:html

```

--------------------------------

### Create New Rails App with Git and PostgreSQL

Source: https://guides.rubyonrails.org/v3.2/command_line

This example demonstrates creating a new Rails application (`rails new .`) with Git source control management and PostgreSQL as the database. It requires initializing a Git repository beforehand.

```bash
$ mkdir gitapp
$ cd gitapp
$ git init
Initialized empty Git repository in .git/
$ rails new . --git --database=postgresql
      exist
      create  app/controllers
      create  app/helpers
...
      create  tmp/cache
      create  tmp/pids
      create  Rakefile
add 'Rakefile'
      create  README.rdoc
add 'README.rdoc'
      create  app/controllers/application_controller.rb
add 'app/controllers/application_controller.rb'
      create  app/helpers/application_helper.rb
...
      create  log/test.log
add 'log/test.log'
```

--------------------------------

### Rails Routes Output for Article Management

Source: https://guides.rubyonrails.org/v5.1/getting_started

This output from `bin/rails routes` displays the defined routes for article management. It shows the HTTP verbs, URI patterns, and the corresponding Controller#Action for various operations like index, create, new, show, edit, update, and destroy.

```bash
$ bin/rails routes
      Prefix Verb   URI Pattern                  Controller#Action
    articles GET    /articles(.:format)          articles#index
             POST   /articles(.:format)          articles#create
 new_article GET    /articles/new(.:format)      articles#new
edit_article GET    /articles/:id/edit(.:format) articles#edit
     article GET    /articles/:id(.:format)      articles#show
             PATCH  /articles/:id(.:format)      articles#update
             PUT    /articles/:id(.:format)      articles#update
             DELETE /articles/:id(.:format)      articles#destroy
       root GET    /                            welcome#index
```

--------------------------------

### Rack Server Start (`Rack::Server#start`)

Source: https://guides.rubyonrails.org/v7.1/initialization

The core `Rack::Server` startup logic. It configures load paths, requires specified libraries, enables debugging and pretty-printing if requested, checks for PID files, handles daemonization, writes the PID file, sets up an `INT` signal trap for server shutdown, and finally runs the wrapped application.

```ruby
module Rack
  class Server
    def start(&blk)
      if options[:warn]
        $-w = true
      end

      if includes = options[:include]
        $LOAD_PATH.unshift(*includes)
      end

      if library = options[:require]
        require library
      end

      if options[:debug]
        $DEBUG = true
        require "pp"
        p options[:server]
        pp wrapped_app
        pp app
      end

      check_pid! if options[:pid]

      # Touch the wrapped app, so that the config.ru is loaded before
      # daemonization (i.e. before chdir, etc).
      handle_profiling(options[:heapfile], options[:profile_mode], options[:profile_file]) do
        wrapped_app
      end

      daemonize_app if options[:daemonize]

      write_pid if options[:pid]

      trap(:INT) do
        if server.respond_to?(:shutdown)
          server.shutdown
        else
          exit
        end
      end

      server.run wrapped_app, options, &blk
    end
  end
end
```

--------------------------------

### Delete Record with `destroy` in Ruby on Rails

Source: https://guides.rubyonrails.org/getting_started

Demonstrates deleting a product record from the database using the `destroy` method in the Rails console. It shows the SQL query executed and the returned object, confirming the deletion.

```ruby
store(dev)> product.destroy
  TRANSACTION (0.1ms)  BEGIN immediate TRANSACTION /*application='Store'*/
  Product Destroy (0.4ms)  DELETE FROM "products" WHERE "products"."id" = 1 /*application='Store'*/
  TRANSACTION (0.1ms)  COMMIT TRANSACTION /*application='Store'*/
=> #<Product:0x0000000125813d48 id: 1, name: "T-Shirt", created_at: "2024-11-09 22:39:38.498730000 +0000", updated_at: "2024-11-09 22:39:38.498730000 +0000">

```

```ruby
store(dev)> Product.all
  Product Load (1.9ms)  SELECT "products".* FROM "products" /* loading for pp */ LIMIT 11 /*application='Store'*/
=>
[#<Product:0x000000012abde4c8
  id: 2,
  name: "Pants",
  created_at: "2024-11-09 22:33:19.638912000 +0000",
  updated_at: "2024-11-09 22:33:19.638912000 +0000">
]

```

--------------------------------

### Start Rails Development Server

Source: https://guides.rubyonrails.org/v2.3/getting_started

Starts the default Mongrel web server for the Rails application. This command allows you to view your application in a web browser. To stop the server, press Ctrl+C in the terminal. Changes to files are usually auto-reloaded.

```bash
$ script/server
```

--------------------------------

### PostgreSQL EXPLAIN Output Example

Source: https://guides.rubyonrails.org/v5.2/active_record_querying

An example of the output generated by `EXPLAIN` for a Ruby on Rails query when using the PostgreSQL database adapter. It presents the query plan with costs, row estimates, and join strategies.

```text
EXPLAIN for: SELECT "users".* FROM "users" INNER JOIN "articles" ON "articles"."user_id" = "users"."id" WHERE "users"."id" = 1
                  QUERY PLAN
------------------------------------------------------------------------------
 Nested Loop Left Join  (cost=0.00..37.24 rows=8 width=0)
   Join Filter: (articles.user_id = users.id)
   ->  Index Scan using users_pkey on users  (cost=0.00..8.27 rows=1 width=4)
         Index Cond: (id = 1)
   ->  Seq Scan on articles  (cost=0.00..28.88 rows=8 width=4)
         Filter: (articles.user_id = 1)
(6 rows)
```

--------------------------------

### PostgreSQL EXPLAIN Output Example

Source: https://guides.rubyonrails.org/v7.1/active_record_querying

An example of the `EXPLAIN` output for a simple query on PostgreSQL, illustrating the query plan details.

```sql
EXPLAIN SELECT "customers".* FROM "customers" INNER JOIN "orders" ON "orders"."customer_id" = "customers"."id" WHERE "customers"."id" = $1 [["id", 1]]
                                  QUERY PLAN
------------------------------------------------------------------------------
 Nested Loop  (cost=4.33..20.85 rows=4 width=164)
    ->  Index Scan using customers_pkey on customers  (cost=0.15..8.17 rows=1 width=164)
          Index Cond: (id = '1'::bigint)
    ->  Bitmap Heap Scan on orders  (cost=4.18..12.64 rows=4 width=8)
          Recheck Cond: (customer_id = '1'::bigint)
          ->  Bitmap Index Scan on index_orders_on_customer_id  (cost=0.00..4.18 rows=4 width=0)
                Index Cond: (customer_id = '1'::bigint)
(7 rows)

```

--------------------------------

### Basic Articles Controller Structure in Rails

Source: https://guides.rubyonrails.org/v4.1/getting_started

This is the fundamental structure of a Rails controller, inheriting from ApplicationController. Public methods defined within this class will serve as actions, capable of responding to web requests and performing operations.

```ruby
class ArticlesController < ApplicationController
end
```

--------------------------------

### Create Comments Table Migration in Rails

Source: https://guides.rubyonrails.org/v4.1/getting_started

This Rails migration file defines the schema for the 'comments' table. It includes columns for 'commenter', 'body', 'article_id' (with an index for the association), and timestamps. This is automatically generated when a model is created.

```ruby
class CreateComments < ActiveRecord::Migration
  def change
    create_table :comments do |t|
      t.string :commenter
      t.text :body
      # this line adds an integer column called `article_id`.
      t.references :article, index: true
      t.timestamps
    end
  end
end
```

--------------------------------

### Initialize and Save Article in Rails Controller

Source: https://guides.rubyonrails.org/v4.2/getting_started

Initializes a new Article model with parameters and saves it to the database. It then redirects to the article's show page. This is a fundamental step in creating new records.

```ruby
def create
  @article = Article.new(params[:article])
  @article.save
  redirect_to @article
end
```

--------------------------------

### Action Cable Configuration Example

Source: https://guides.rubyonrails.org/v5.1/action_cable_overview

Defines the subscription adapter configuration for different Rails environments. Specifies 'async' for development/test and 'redis' for production.

```yaml
development:
  adapter: async
test:
  adapter: async
production:
  adapter: redis
  url: redis://10.10.3.153:6381
  channel_prefix: appname_production
```

--------------------------------

### Test Helper for Database Setup in Rails Plugin (Ruby)

Source: https://guides.rubyonrails.org/v2.3/plugins

This Ruby script sets up the Rails environment for plugin testing. It configures the database connection based on the `DB` environment variable, loads the schema, and initializes the Rails environment.

```ruby
ENV['RAILS_ENV'] = 'test'
ENV['RAILS_ROOT'] ||= File.dirname(__FILE__) + '/../../../..'

require 'test/unit'
require File.expand_path(File.join(ENV['RAILS_ROOT'], 'config/environment.rb'))

def load_schema
  config = YAML::load(IO.read(File.dirname(__FILE__) + '/database.yml'))
  ActiveRecord::Base.logger = Logger.new(File.dirname(__FILE__) + "/debug.log")

  db_adapter = ENV['DB']

  # no db passed, try one of these fine config-free DBs before bombing.
  db_adapter ||= 
    begin
      require 'rubygems'
      require 'sqlite'
      'sqlite'
    rescue MissingSourceFile
      begin
        require 'sqlite3'
        'sqlite3'
      rescue MissingSourceFile
      end
    end

  raise "No DB Adapter selected. Pass the DB= option to pick one, or install Sqlite or Sqlite3." if db_adapter.nil?

  ActiveRecord::Base.establish_connection(config[db_adapter])
  load(File.dirname(__FILE__) + "/schema.rb")
  require File.dirname(__FILE__) + '/../rails/init.rb'
end

```

--------------------------------

### Generate a Rails Controller with an Action

Source: https://guides.rubyonrails.org/getting_started

This command generates a new controller, its associated view files, and test files. The `--skip-routes` flag prevents the generator from adding new routes, assuming they are already defined.

```bash
bin/rails generate controller Products index --skip-routes
```

--------------------------------

### Building Rack Application

Source: https://guides.rubyonrails.org/v6.0/initialization

This Ruby code demonstrates how the Rack application is built. The `wrapped_app` method memoizes the application instance, which is then built using `build_app`. The `build_app_and_options_from_config` method is responsible for parsing the `config.ru` file to construct the application and merge any options defined within it. If a builder string is provided, `build_app_from_string` is used.

```ruby
@wrapped_app ||= build_app app

def app
  @app ||= options[:builder] ? build_app_from_string : build_app_and_options_from_config
end

private

def build_app_and_options_from_config
  if !::File.exist? options[:config]
    abort "configuration #{options[:config]} not found"
  end
  app, options = Rack::Builder.parse_file(self.options[:config], opt_parser)
  self.options.merge! options
  app
end

def build_app_from_string
  Rack::Builder.new_from_string(self.options[:builder])
end
```

--------------------------------

### Ruby: Get Beginning/End of Hour

Source: https://guides.rubyonrails.org/v5.2/active_support_core_extensions

These Ruby methods return timestamps at the start (hh:00:00) or end (hh:59:59) of a specific hour. They work with `Time` and `DateTime` objects. `beginning_of_hour` is aliased to `at_beginning_of_hour`.

```ruby
date = DateTime.new(2010, 6, 7, 19, 55, 25)
date.beginning_of_hour # => Mon Jun 07 19:00:00 +0200 2010
date.end_of_hour     # => Mon Jun 07 19:59:59 +0200 2010
```

--------------------------------

### Example Rails Middleware Stack

Source: https://guides.rubyonrails.org/v4.1/rails_on_rack

Presents a typical output from the `bin/rake middleware` command for a freshly generated Rails application. It lists various Rack and Action Dispatch middlewares used by default.

```shell
use Rack::Sendfile
use ActionDispatch::Static
use Rack::Lock
use #<ActiveSupport::Cache::Strategy::LocalCache::Middleware:0x000000029a0838>
use Rack::Runtime
use Rack::MethodOverride
use ActionDispatch::RequestId
use Rails::Rack::Logger
use ActionDispatch::ShowExceptions
use ActionDispatch::DebugExceptions
use ActionDispatch::RemoteIp
use ActionDispatch::Reloader
use ActionDispatch::Callbacks
use ActiveRecord::Migration::CheckPending
use ActiveRecord::ConnectionAdapters::ConnectionManagement
use ActiveRecord::QueryCache
use ActionDispatch::Cookies
use ActionDispatch::Session::CookieStore
use ActionDispatch::Flash
use ActionDispatch::ParamsParser
use Rack::Head
use Rack::ConditionalGet
use Rack::ETag
run Rails.application.routes
```

--------------------------------

### Product Model with In Stock Notification Callback (Ruby)

Source: https://guides.rubyonrails.org/getting_started

Extends the `Product` model to include an `after_update_commit` callback that triggers the `notify_subscribers` method. This method checks if a product is back in stock using `inventory_count_previously_was` and sends emails to subscribers.

```ruby
class Product < ApplicationRecord
  has_many :subscribers, dependent: :destroy
  has_one_attached :featured_image
  has_rich_text :description

  validates :name, presence: true
  validates :inventory_count, numericality: { greater_than_or_equal_to: 0 }

  after_update_commit :notify_subscribers, if: :back_in_stock?

  def back_in_stock?
    inventory_count_previously_was.zero? && inventory_count > 0
  end

  def notify_subscribers
    subscribers.each do |subscriber|
      ProductMailer.with(product: self, subscriber: subscriber).in_stock.deliver_later
    end
  end
end
```

--------------------------------

### View Generated Rails Routes

Source: https://guides.rubyonrails.org/v4.2/getting_started

This command displays all the routes defined in a Rails application, including those generated by `resources` and custom routes. It helps in understanding how URLs are mapped to controller actions and provides insights into the available endpoints and their associated HTTP verbs.

```bash
$ bin/rake routes
    Prefix Verb      URI Pattern                  Controller#Action
  articles GET       /articles(.:format)          articles#index
           POST      /articles(.:format)          articles#create
new_article GET      /articles/new(.:format)      articles#new
edit_article GET     /articles/:id/edit(.:format) articles#edit
 article GET       /articles/:id(.:format)      articles#show
           PATCH     /articles/:id(.:format)      articles#update
           PUT       /articles/:id(.:format)      articles#update
           DELETE    /articles/:id(.:format)      articles#destroy
    root GET       /                            welcome#index
```

--------------------------------

### Define create action in ArticlesController (Ruby)

Source: https://guides.rubyonrails.org/v4.1/getting_started

This Ruby code snippet defines the `create` action within the `ArticlesController` class. It is intended to handle incoming article data from a form submission. Currently, it displays the submitted article parameters.

```ruby
class ArticlesController < ApplicationController
  def new
  end

  def create
    render plain: params[:article].inspect
  end
end
```

--------------------------------

### Display Application Information

Source: https://guides.rubyonrails.org/v6.1/command_line

Shows general information about the Rails application, including dependency versions. This command is helpful for troubleshooting and understanding the application's setup.

```bash
bin/rails about
```

--------------------------------

### Index Action for Listing Articles in Rails Controller

Source: https://guides.rubyonrails.org/v4.1/getting_started

Defines the 'index' action in the ArticlesController to fetch all articles from the database. It assigns the collection of articles to an instance variable '@articles', making them available for display in the corresponding view. Assumes an 'Article' model exists.

```ruby
def index
  @articles = Article.all
end
```

--------------------------------

### Create a New Rails Application

Source: https://guides.rubyonrails.org/v5.2/command_line

The `rails new` command initializes a new Rails application with a standard directory structure and necessary configuration files. It requires the Rails gem to be installed (`gem install rails`). It outputs a list of created files and runs `bundle install` to set up dependencies.

```bash
$ rails new commandsapp
      create
      create  README.md
      create  Rakefile
      create  config.ru
      create  .gitignore
      create  Gemfile
      create  app
      ... 
      create  tmp/cache
      ...
      run  bundle install
```

--------------------------------

### Ruby: Get beginning of day timestamp

Source: https://guides.rubyonrails.org/v3.2/active_support_core_extensions

The `beginning_of_day` method returns a timestamp representing the start of the day (00:00:00) for a given date. This method is also aliased as `at_beginning_of_day`, `midnight`, and `at_midnight`.

```ruby
date = Date.new(2010, 6, 7)
date.beginning_of_day # => Sun Jun 07 00:00:00 +0200 2010
```

--------------------------------

### Example Rails Middleware Stack Output

Source: https://guides.rubyonrails.org/v7.2/rails_on_rack

This is an example output from the `bin/rails middleware` command, illustrating a typical middleware stack for a freshly generated Rails application. It shows various Action Dispatch and Rack middlewares, ending with the application's routes.

```bash
use ActionDispatch::HostAuthorization
use Rack::Sendfile
use ActionDispatch::Static
use ActionDispatch::Executor
use ActionDispatch::ServerTiming
use ActiveSupport::Cache::Strategy::LocalCache::Middleware
use Rack::Runtime
use Rack::MethodOverride
use ActionDispatch::RequestId
use ActionDispatch::RemoteIp
use Sprockets::Rails::QuietAssets
use Rails::Rack::Logger
use ActionDispatch::ShowExceptions
use WebConsole::Middleware
use ActionDispatch::DebugExceptions
use ActionDispatch::ActionableExceptions
use ActionDispatch::Reloader
use ActionDispatch::Callbacks
use ActiveRecord::Migration::CheckPending
use ActionDispatch::Cookies
use ActionDispatch::Session::CookieStore
use ActionDispatch::Flash
use ActionDispatch::ContentSecurityPolicy::Middleware
use Rack::Head
use Rack::ConditionalGet
use Rack::ETag
use Rack::TempfileReaper
run MyApp::Application.routes

```

--------------------------------

### Navigation Link to Articles Index in Rails View

Source: https://guides.rubyonrails.org/v4.1/getting_started

Demonstrates how to create a hyperlink to the main articles listing page using the Rails 'link_to' helper. This is typically placed in a view to provide navigation to the articles section of the site.

```html
<h1>Hello, Rails!</h1>
<%= link_to 'My Blog', controller: 'articles' %>
```

--------------------------------

### PostgreSQL Database Configuration for Rails

Source: https://guides.rubyonrails.org/v6.0/command_line

This code snippet shows the content of the `config/database.yml` file generated by Rails when PostgreSQL is selected as the database. It includes default settings and an example for the development environment, with comments on driver installation and configuration.

```yaml
# PostgreSQL. Versions 9.1 and up are supported.
#
# Install the pg driver:
#  gem install pg
# On macOS with Homebrew:
#  gem install pg -- --with-pg-config=/usr/local/bin/pg_config
# On macOS with MacPorts:
#  gem install pg -- --with-pg-config=/opt/local/lib/postgresql84/bin/pg_config
# On Windows:
#  gem install pg
#      Choose the win32 build.
#      Install PostgreSQL and put its /bin directory on your path.
#
# Configure Using Gemfile
# gem 'pg'
#
default: &default
  adapter: postgresql
  encoding: unicode
  # For details on connection pooling, see Rails configuration guide
  # https://guides.rubyonrails.org/configuring.html#database-pooling
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

development:
  <<: *default
  database: gitapp_development
...
```

--------------------------------

### Configuration Guide Table for Framework Default

Source: https://guides.rubyonrails.org/v2.3/contributing_to_rails

Shows the format for documenting a new framework default in the configuration guide. This table clearly outlines the starting version and the default value change.

```html
#### `config.active_job.existing_behavior

| Starting with version | The default value is |
| --------------------- | -------------------- |
| (original)            | `true`               |
| 7.1                   | `false`              |

```

--------------------------------

### Get Help for a Specific Rails Generator (Controller)

Source: https://guides.rubyonrails.org/v7.2/command_line

This command provides detailed usage information for the 'controller' generator, including expected arguments, options, and examples. It's useful for understanding how to properly invoke the generator for specific tasks.

```bash
$ bin/rails generate controller
Usage:
  bin/rails generate controller NAME [action action] [options]

...
...

Description:
    ...

    To create a controller within a module, specify the controller name as a path like 'parent_module/controller_name'.

    ...

Example:
    `bin/rails generate controller CreditCards open debit credit close`

    Credit card controller with URLs like /credit_cards/debit.
        Controller: app/controllers/credit_cards_controller.rb
        Test:       test/controllers/credit_cards_controller_test.rb
        Views:      app/views/credit_cards/debit.html.erb [...]
        Helper:     app/helpers/credit_cards_helper.rb

```

--------------------------------

### Rails Generate Model Command

Source: https://guides.rubyonrails.org/v6.0/getting_started

This command-line snippet uses the Rails generator to create a new model named 'Article'. It specifies two attributes: 'title' of type string and 'text' of type text. This command generates the model file and the database migration file.

```bash
$ rails generate model Article title:string text:text
```

--------------------------------

### Index Action for Listing Posts in Rails Controller

Source: https://guides.rubyonrails.org/v4.0/getting_started

This Ruby code defines the 'index' action in a Rails controller. It retrieves all posts from the database using Post.all and assigns them to an instance variable @posts for display in a view.

```ruby
def index
  @posts = Post.all
end
```

--------------------------------

### Create MySQL Test Databases

Source: https://guides.rubyonrails.org/v3.1/contributing_to_ruby_on_rails

Navigates to the 'activerecord' directory and executes a rake task to build the necessary test databases for MySQL.

```bash
$ cd activerecord
$ rake mysql:build_databases
```

--------------------------------

### Create Rails Application with Git and PostgreSQL

Source: https://guides.rubyonrails.org/v3.1/command_line

This demonstrates creating a new Rails application with specific database and source code management (SCM) configurations. It involves creating a directory, initializing Git, and then running `rails new` with options like `--git` and `--database=postgresql`. The output shows the files created and the structure of the generated `config/database.yml`.

```bash
$ mkdir gitapp
$ cd gitapp
$ git init
Initialized empty Git repository in .git/
$ rails new . --git --database=postgresql
    exists  app/controllers
    exists  app/helpers
... 
    create  tmp/cache
    create  tmp/pids
    create  Rakefile
add 'Rakefile'
    create  README
add 'README'
    create  app/controllers/application_controller.rb
add 'app/controllers/application_controller.rb'
... 
    create  log/test.log
add 'log/test.log'
```

```yaml
cat config/database.yml
# PostgreSQL. Versions 7.4 and 8.x are supported.
#
# Install the ruby-postgres driver:
#   gem install ruby-postgres
# On Mac OS X:
#   gem install ruby-postgres -- --include=/usr/local/pgsql
# On Windows:
#   gem install ruby-postgres
#     Choose the win32 build.
#     Install PostgreSQL and put its /bin directory on your path.
development:
  adapter: postgresql
  encoding: unicode
  database: gitapp_development
  pool: 5
  username: gitapp
  password:
...
```

--------------------------------

### Query All Product Records in Ruby

Source: https://guides.rubyonrails.org/getting_started

Shows how to retrieve all records from the 'products' database table using the .all class method on the Product model. This method returns an ActiveRecord::Relation object, which is an Array-like collection.

```ruby
Product.all
```

--------------------------------

### I18n: Spanish Locale Configuration (YAML)

Source: https://guides.rubyonrails.org/getting_started

This YAML snippet provides translations for the Spanish locale. It includes translations for "hello" and a nested translation for "products.index.title", mirroring the structure of the English locale file.

```yaml
es:
  hello: "Hola mundo"
  products:
    index:
      title: "Productos"
```

--------------------------------

### API Link Formatting Examples

Source: https://guides.rubyonrails.org/ruby_on_rails_guides_guidelines

Shows how direct links to the Ruby on Rails API documentation are handled by the guides generator, including how version tags affect URL modification and the preferred method for linking to API resources.

```text
https://api.rubyonrails.org/v5.0.1/classes/ActiveRecord/Attributes/ClassMethods.html
```

```text
https://api.rubyonrails.org/classes/ActionDispatch/Response.html
```

```text
https://edgeapi.rubyonrails.org/classes/ActionDispatch/Response.html
```

```text
https://api.rubyonrails.org/v5.1.0/classes/ActionDispatch/Response.html
```

--------------------------------

### Start Rails Server

Source: https://guides.rubyonrails.org/command_line

Command to start the Rails development server. This command boots up the application, making it accessible via a local URL, typically http://localhost:3000.

```bash
$ bin/rails server
=> Booting Puma...

```

--------------------------------

### Define RESTful Resources in Rails

Source: https://guides.rubyonrails.org/v4.0/getting_started

This code demonstrates how to declare a standard RESTful resource, such as `:posts`, within the `config/routes.rb` file. This automatically generates routes for common CRUD operations (index, create, new, show, edit, update, destroy).

```ruby
Blog::Application.routes.draw do
  resources :posts
  root to: "welcome#index"
end
```

--------------------------------

### MySQL/MariaDB EXPLAIN Output Example

Source: https://guides.rubyonrails.org/v7.1/active_record_querying

An example of the `EXPLAIN` output for a simple query on MySQL or MariaDB, showing the query plan details.

```sql
EXPLAIN SELECT `customers`.* FROM `customers` INNER JOIN `orders` ON `orders`.`customer_id` = `customers`.`id` WHERE `customers`.`id` = 1
+----+-------------+------------+-------+---------------+-----------------+---------+---------+-------+------+-------------+
| id | select_type | table      | type  | possible_keys | key             | key_len | ref     | rows  | Extra       |
+----+-------------+------------+-------+---------------+-----------------+---------+---------+-------+-------------+
|  1 | SIMPLE      | customers  | const | PRIMARY       | PRIMARY         | 4       | const   | 1     |             |
|  1 | SIMPLE      | orders     | ALL   | NULL          | NULL            | NULL    | NULL    | 1     | Using where |
+----+-------------+------------+-------+---------------+-----------------+---------+---------+-------+-------------+

```

--------------------------------

### Rails Form for Nested Comments

Source: https://guides.rubyonrails.org/v4.1/getting_started

This ERB code snippet demonstrates how to build a form for creating new comments nested under an article. It uses the `form_for` helper with an array to define the nested route for the comment submission.

```erb
<%= form_for([@article, @article.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br>
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br>
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
```

--------------------------------

### Display Rails Environment Information with bin/rails about

Source: https://guides.rubyonrails.org/v5.1/command_line

The `bin/rails about` command provides a detailed overview of your Rails application's environment. This includes version numbers for Ruby, Rails, and other components, as well as database adapter information and the application root.

```bash
$ bin/rails about
About your application's environment
Rails version                5.1.0
Ruby version                 2.2.2 (x86_64-linux)
RubyGems version           2.4.6
Rack version                 2.0.1
JavaScript Runtime       Node.js (V8)
Middleware:                Rack::Sendfile, ActionDispatch::Static, ActionDispatch::Executor, ActiveSupport::Cache::Strategy::LocalCache::Middleware, Rack::Runtime, Rack::MethodOverride, ActionDispatch::RequestId, ActionDispatch::RemoteIp, Sprockets::Rails::QuietAssets, Rails::Rack::Logger, ActionDispatch::ShowExceptions, WebConsole::Middleware, ActionDispatch::DebugExceptions, ActionDispatch::Reloader, ActionDispatch::Callbacks, ActiveRecord::Migration::CheckPending, ActionDispatch::Cookies, ActionDispatch::Session::CookieStore, ActionDispatch::Flash, Rack::Head, Rack::ConditionalGet, Rack::ETag
Application root           /home/foobar/commandsapp
Environment                development
Database adapter           sqlite3
Database schema version    20110805173523

```

--------------------------------

### Install Action Text Gem

Source: https://guides.rubyonrails.org/action_text_overview

Installs Action Text and its JavaScript dependencies, adds the image_processing gem, creates necessary database migrations, and sets up CSS and view partials for rendering rich text content and attachments.

```bash
$ bin/rails action_text:install

```

--------------------------------

### Show Article View in Rails ERB

Source: https://guides.rubyonrails.org/v4.1/getting_started

An ERB template for displaying a single article's title and text. It accesses the article data passed from the controller via the '@article' instance variable. This view is intended to be rendered by the 'show' action.

```html
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>
<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>
```

--------------------------------

### Show Post Action in Rails Controller

Source: https://guides.rubyonrails.org/v4.0/getting_started

This Ruby code implements the 'show' action in a Rails controller. It finds a specific post by its ID from the database using the Post model and makes it available to the view via an instance variable.

```ruby
def show
  @post = Post.find(params[:id])
end
```

--------------------------------

### Link Back to Articles Index from Show Article View in Rails

Source: https://guides.rubyonrails.org/v4.1/getting_started

Adds a 'Back' link to the 'show' article view. This allows users viewing a single article to easily return to the list of all articles using the 'link_to' helper and the 'articles_path' route helper.

```html
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>
<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>
<%= link_to 'Back', articles_path %>
```

--------------------------------

### Execute Rails Server Command

Source: https://guides.rubyonrails.org/initialization

This Ruby script is the entry point for executing Rails commands, specifically `bin/rails server`. It sets the application path and requires the necessary boot and command files.

```ruby
#!/usr/bin/env ruby
APP_PATH = File.expand_path("../config/application", __dir__)
require_relative "../config/boot"
require "rails/commands"

```

--------------------------------

### Set Root URL in Rails Routes

Source: https://guides.rubyonrails.org/v4.1/getting_started

This snippet shows how to configure the root URL of your Rails application by uncommenting and setting the 'root' route in the routes.rb file. This directs traffic to the 'welcome' controller's 'index' action.

```ruby
Rails.application.routes.draw do
  get 'welcome/index'
  # The priority is based upon order of creation:
  # first created -> highest priority.
  #
  # You can have the root of your site routed with "root"
  root 'welcome#index'
  #
  # ...
end
```

--------------------------------

### Display Comments on Article Show Page (Rails)

Source: https://guides.rubyonrails.org/v6.0/getting_started

This ERB template snippet demonstrates how to display a list of comments associated with an article on its show page. It iterates through the comments collection for the article and displays the 'commenter' and 'body' for each comment.

```erb
<p>  <strong>Title:</strong>  <%= @article.title %> </p>
<p>  <strong>Text:</strong>  <%= @article.text %> </p>
<h2>Comments</h2>
<% @article.comments.each do |comment| %>
  <p>
    <strong>Commenter:</strong>
    <%= comment.commenter %>
  </p>
  <p>
    <strong>Comment:</strong>
    <%= comment.body %>
  </p>
<% end %>
<h2>Add a comment:</h2>
<%= form_with(model: [ @article, @article.comments.build ], local: true) do |form| %>
  <p>
    <%= form.label :commenter %><br>
    <%= form.text_field :commenter %>
  </p>
  <p>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
  </p>
  <p>
    <%= form.submit %>
  </p>
<% end %>
<%= link_to 'Edit', edit_article_path(@article) %> |<%= link_to 'Back', articles_path %>
```

--------------------------------

### Install SQLite3 (Arch Linux)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs the SQLite3 package on Arch Linux, a prerequisite for the sqlite3-ruby gem.

```bash
$ sudo pacman -S sqlite
```

--------------------------------

### Web Console Gem Installation and Usage (Ruby)

Source: https://guides.rubyonrails.org/v6.0/upgrading_ruby_on_rails

Instructions for adding the 'web-console' gem to a Rails development environment. It details how to install the gem and then includes the console helper in views or relies on it appearing on error pages.

```ruby
gem 'web-console', '~> 2.0'
```

```erb
<%= console %>
```

--------------------------------

### Example of Ruby on Rails Configuration Hook

Source: https://guides.rubyonrails.org/v5.1/engines

This snippet demonstrates how to use the `before_configuration` hook in Ruby on Rails. This hook is executed very early in the application's boot process, before any initializers are run. It's useful for setting up configurations that need to be available globally from the start.

```ruby
config.before_configuration { puts 'I am called before any initializers' }
```

--------------------------------

### Ruby on Rails Console: Model Interaction and Database Operations

Source: https://guides.rubyonrails.org/v7.2/getting_started

This snippet shows how to use the Rails console to create, save, and retrieve Article records from the database. It demonstrates initializing a new object, persisting it with `save`, and fetching records using `find` and `all`.

```ruby
bin/rails console
```

```ruby
article = Article.new(title: "Hello Rails", body: "I am on Rails!")
```

```ruby
article.save
```

```ruby
Article.find(1)
```

```ruby
Article.all
```

--------------------------------

### Install Ruby on Ubuntu using Mise

Source: https://guides.rubyonrails.org/install_ruby_on_rails

Installs build dependencies, Mise version manager, and Ruby globally on Ubuntu. Requires Ubuntu Jammy 22.04 or newer.

```shell
# Install dependencies with apt
$ sudo apt update
$ sudo apt install build-essential rustc libssl-dev libyaml-dev zlib1g-dev libgmp-dev git

# Install Mise version manager
$ curl https://mise.run | sh
$ echo 'eval "$(~/.local/bin/mise activate)"' >> ~/.bashrc
$ source ~/.bashrc

# Install Ruby globally with Mise
$ mise use -g ruby@3

```

--------------------------------

### Get Parent Module Chain (Ruby)

Source: https://guides.rubyonrails.org/v6.1/active_support_core_extensions

The `module_parents` method returns an array of parent modules, starting from the immediate parent up to `Object`. This method is useful for understanding the hierarchy of a module. Defined in `active_support/core_ext/module/introspection.rb`.

```ruby
module X
  module Y
    module Z
    end
  end
end
M = X::Y::Z

X::Y::Z.module_parents # => [X::Y, X, Object]
M.module_parents       # => [X::Y, X, Object]

```

--------------------------------

### Install Ubuntu on Windows using WSL

Source: https://guides.rubyonrails.org/install_ruby_on_rails

Installs the Ubuntu 24.04 distribution on Windows using the Windows Subsystem for Linux. Requires Windows 11 or Windows 10 version 2004 or higher.

```shell
$ wsl --install --distribution Ubuntu-24.04

```

--------------------------------

### I18n: Basic Translation Helper in View (ERB)

Source: https://guides.rubyonrails.org/getting_started

This ERB snippet shows the basic usage of the `t` helper for internationalization in a Rails view. It looks up a translation for the key "hello" in the current locale.

```erb
<h1><%= t "hello" %></h1>
```

--------------------------------

### Generate Comment Model in Rails

Source: https://guides.rubyonrails.org/v6.0/getting_started

Generates a new Comment model with specified attributes (commenter, body, article reference) and creates associated migration and test files. The ':references' keyword creates an '_id' column for database relationships.

```bash
$ rails generate model Comment commenter:string body:text article:references
```

--------------------------------

### Add 'New Post' Link to Post Index (Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This code adds a 'New post' link to the posts index page, which navigates to the form for creating a new post. It utilizes the `new_post_path` helper provided by Rails.

```erb
<%= link_to 'New post', new_post_path %>
```

--------------------------------

### Start Rails Server with Alias

Source: https://guides.rubyonrails.org/v6.0/command_line

Demonstrates the shorthand alias 's' for the `rails server` command, providing a quicker way to launch the Puma web server.

```bash
rails s
```

--------------------------------

### Rails Server Initialization (`Rails::Server#start`)

Source: https://guides.rubyonrails.org/v5.0/initialization

The `start` method in `Rails::Server` handles initial server setup, including setting up interrupt signal handling, creating temporary directories, and logging to standard output. It then calls the superclass's `start` method.

```ruby
def start
  print_boot_information
  trap(:INT) { exit }
  create_tmp_directories
  log_to_stdout if options[:log_stdout]
  super
  ...
end

private

def print_boot_information
  ...
  puts "=> Run `rails server -h` for more startup options"
end

def create_tmp_directories
  %w(cache pids sockets).each do |dir_to_make|
    FileUtils.mkdir_p(File.join(Rails.root, 'tmp', dir_to_make))
  end
end

def log_to_stdout
  wrapped_app # touch the app so the logger is set up
  console = ActiveSupport::Logger.new($stdout)
  console.formatter = Rails.logger.formatter
  console.level = Rails.logger.level
  Rails.logger.extend(ActiveSupport::Logger.broadcast(console))
end
```

--------------------------------

### Get All Parent Modules in Ruby

Source: https://guides.rubyonrails.org/v3.0/active_support_core_extensions

The `parents` method returns an array containing all ancestor modules, starting from the immediate parent up to `Object`. This provides a complete view of the module's nesting hierarchy.

```ruby
module X
  module Y
    module Z
    end
  end
end
M = X::Y::Z
X::Y::Z.parents  # => [X::Y, X, Object]
M.parents        # => [X::Y, X, Object]
```

--------------------------------

### Install Rails Dependencies with Bundler

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs all project dependencies defined in the Gemfile using Bundler, excluding MySQL and PostgreSQL Ruby drivers.

```bash
$ bundle install --without db
```

--------------------------------

### Generate Authentication in Rails

Source: https://guides.rubyonrails.org/getting_started

This command uses the Rails generator to set up authentication for the application. It typically creates User and Session models, along with necessary controllers and views for login and logout functionality. This is a foundational step for securing the application.

```bash
$ bin/rails generate authentication
```

--------------------------------

### Rails Database Configuration Example

Source: https://guides.rubyonrails.org/v3.0/testing

This is an excerpt from a Rails database configuration file (config/database.yml) demonstrating the separation of database settings for different environments: production, development, and test. Each environment has its own unique database setup, allowing for isolated data management during development and testing.

```yaml
production:
  adapter: postgresql
  encoding: unicode
  database: myapp_production
  pool: 5
  username: myapp
  password:

development:
  adapter: postgresql
  encoding: unicode
  database: myapp_development
  pool: 5
  username: myapp
  password:

test:
  adapter: postgresql
  encoding: unicode
  database: myapp_test
  pool: 5
  username: myapp
  password:
```

--------------------------------

### Render Comment Partial in Rails

Source: https://guides.rubyonrails.org/v4.1/getting_started

This ERB code snippet demonstrates how to render a partial for each comment in a collection. The `render @article.comments` call iterates through the comments and applies the `_comment.html.erb` partial to each one, assigning it to a local `comment` variable.

```erb
<p>    <strong>Commenter:</strong>    <%= comment.commenter %></p><p>    <strong>Comment:</strong>    <%= comment.body %></p>
```

```erb
<p>    <strong>Title:</strong>    <%= @article.title %></p><p>    <strong>Text:</strong>    <%= @article.text %></p><h2>Comments</h2><%= render @article.comments %><h2>Add a comment:</h2><%= form_for([@article, @article.comments.build]) do |f| %>    <p>        <%= f.label :commenter %><br>        <%= f.text_field :commenter %>    </p>    <p>        <%= f.label :body %><br>        <%= f.text_area :body %>    </p>    <p>        <%= f.submit %>    </p><% end %> <%= link_to 'Edit Article', edit_article_path(@article) %> |<%= link_to 'Back to Articles', articles_path %>
```

--------------------------------

### Example CHANGELOG Entry

Source: https://guides.rubyonrails.org/v5.2/contributing_to_ruby_on_rails

This illustrates the format for a CHANGELOG entry, including a summary of the change, optional multi-line descriptions, code examples indented with four spaces, and the author's name or issue number.

```text
*  Summary of a change that briefly describes what was changed. You can use multiple
   lines and wrap them at around 80 characters. Code examples are ok, too, if needed:
         class Foo
           def bar
             puts 'baz'
           end
         end
     You can continue after the code example and you can attach issue number. GH#1234
    *Your Name*
```

--------------------------------

### Configure Bundler Setup

Source: https://guides.rubyonrails.org/v4.0/initialization

This Ruby script configures Bundler for a Rails application by locating the Gemfile and setting up the environment to load the specified gems. It ensures all application dependencies are met before proceeding with initialization.

```ruby
# Set up gems listed in the Gemfile.
ENV['BUNDLE_GEMFILE'] ||= File.expand_path('../../Gemfile', __FILE__)
require 'bundler/setup' if File.exist?(ENV['BUNDLE_GEMFILE'])
```

--------------------------------

### Get Error Count with errors.size

Source: https://guides.rubyonrails.org/v4.0/active_record_validations

Shows how to retrieve the total number of validation error messages associated with an object using the `errors.size` method. The examples illustrate the error count for both invalid and valid objects.

```ruby
class Person < ActiveRecord::Base
  validates :name, presence: true, length: { minimum: 3 }
end
person = Person.new
person.valid? # => false
person.errors.size # => 2
person = Person.new(name: "Andrea", email: "andrea@example.com")
person.valid? # => true
person.errors.size # => 0
```

--------------------------------

### Update Article Show View with Form Partial in Rails

Source: https://guides.rubyonrails.org/v6.0/getting_started

This ERB template demonstrates how to render the comment form partial within the article's show view. It replaces the inline form with a call to `render 'comments/form'`, simplifying the main view.

```erb
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>
<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>
<h2>Comments</h2>
<%= render @article.comments %>
<h2>Add a comment:</h2>
<%= render 'comments/form' %>
<%= link_to 'Edit', edit_article_path(@article) %> | <%= link_to 'Back', articles_path %>
```

--------------------------------

### Rails Action Cable Connection Setup

Source: https://guides.rubyonrails.org/v7.1/action_cable_overview

This Ruby code demonstrates the setup for an Action Cable connection in a Rails application. It extends `ActionCable::Connection::Base` and includes logic for authorizing incoming WebSocket connections based on user identification.

```ruby
module ApplicationCable
  class Connection < ActionCable::Connection::Base
    identified_by :current_user

    def connect
      self.current_user = find_verified_user
    end

    private
      def find_verified_user
        # Identify and authorize the user. Return nil if not authorized.
      end
  end
end
```

--------------------------------

### Rails Server Initialization and Logging

Source: https://guides.rubyonrails.org/v4.1/initialization

The start method in Rails::Server initializes the server, sets up signal traps for graceful shutdown, creates temporary directories, and configures logging to stdout if specified. It then calls the superclass's start method.

```ruby
def start
  print_boot_information
  trap(:INT) { exit }
  create_tmp_directories
  log_to_stdout if options[:log_stdout]
  super
  ...
end

private

def print_boot_information
  ...
  puts "=> Run `rails server -h` for more startup options"
  puts "=> Ctrl-C to shutdown server" unless options[:daemonize]
end

def create_tmp_directories
  %w(cache pids sessions sockets).each do |dir_to_make|
    FileUtils.mkdir_p(File.join(Rails.root, 'tmp', dir_to_make))
  end
end

def log_to_stdout
  wrapped_app # touch the app so the logger is set up
  console = ActiveSupport::Logger.new($stdout)
  console.formatter = Rails.logger.formatter
  console.level = Rails.logger.level
  Rails.logger.extend(ActiveSupport::Logger.broadcast(console))
end
```

--------------------------------

### Ruby on Rails Post Model Migration File

Source: https://guides.rubyonrails.org/v4.0/getting_started

This Ruby code defines a database migration for creating a 'posts' table. It includes 'title' (string) and 'text' (text) columns, along with timestamps for creation and update tracking. The `change` method is designed to be reversible.

```ruby
class CreatePosts < ActiveRecord::Migration
  def change
    create_table :posts do |t|
      t.string :title
      t.text :text
      t.timestamps
    end
  end
end
```

--------------------------------

### Ruby on Rails: Execute Database Migration Command

Source: https://guides.rubyonrails.org/v4.1/getting_started

This command-line instruction executes database migrations in a Ruby on Rails application. By default, it runs migrations for the development environment. To run migrations in a different environment, such as production, specify the RAILS_ENV variable.

```bash
$ bin/rake db:migrate
```

```bash
rake db:migrate RAILS_ENV=production
```

--------------------------------

### Example Rails Middleware Stack Output

Source: https://guides.rubyonrails.org/v7.1/rails_on_rack

Illustrates a typical output from the `bin/rails middleware` command for a new Rails application, showcasing the sequence of Rack middlewares used in request processing.

```shell
use ActionDispatch::HostAuthorization
use Rack::Sendfile
use ActionDispatch::Static
use ActionDispatch::Executor
use ActionDispatch::ServerTiming
use ActiveSupport::Cache::Strategy::LocalCache::Middleware
use Rack::Runtime
use Rack::MethodOverride
use ActionDispatch::RequestId
use ActionDispatch::RemoteIp
use Sprockets::Rails::QuietAssets
use Rails::Rack::Logger
use ActionDispatch::ShowExceptions
use WebConsole::Middleware
use ActionDispatch::DebugExceptions
use ActionDispatch::ActionableExceptions
use ActionDispatch::Reloader
use ActionDispatch::Callbacks
use ActiveRecord::Migration::CheckPending
use ActionDispatch::Cookies
use ActionDispatch::Session::CookieStore
use ActionDispatch::Flash
use ActionDispatch::ContentSecurityPolicy::Middleware
use Rack::Head
use Rack::ConditionalGet
use Rack::ETag
use Rack::TempfileReaper
run MyApp::Application.routes
```

--------------------------------

### Build PostgreSQL Test Databases with Rake

Source: https://guides.rubyonrails.org/v4.2/development_dependencies_install

Builds the required test databases for PostgreSQL using a Rake task within the 'activerecord' directory. This command sets up the databases with appropriate configurations for testing.

```bash
$ cd activerecord
$ bundle exec rake db:postgresql:build
```

--------------------------------

### PostgreSQL Database Configuration in Rails (YAML)

Source: https://guides.rubyonrails.org/v4.2/command_line

This is an example of the `database.yml` configuration file for a PostgreSQL database in a Rails application. It shows settings for development, including adapter, encoding, database name, and connection pool. Instructions for installing the `pg` gem are also included.

```yaml
# PostgreSQL. Versions 8.2 and up are supported.
#
# Install the pg driver:
#   gem install pg
# On OS X with Homebrew:
#   gem install pg -- --with-pg-config=/usr/local/bin/pg_config
# On OS X with MacPorts:
#   gem install pg -- --with-pg-config=/opt/local/lib/postgresql84/bin/pg_config
# On Windows:
#   gem install pg
#     Choose the win32 build.
#     Install PostgreSQL and put its /bin directory on your path.
#
# Configure Using Gemfile
# gem 'pg'
#
development:
  adapter: postgresql
  encoding: unicode
  database: gitapp_development
  pool: 5
  username: gitapp
  password:
...
```

--------------------------------

### Define new and create actions in PostsController (Ruby on Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This snippet shows the structure of a `PostsController` in Rails, defining `new` and `create` actions. The `new` action is typically responsible for rendering the form, while the `create` action handles the submission of form data.

```ruby
class PostsController < ApplicationController
  def new
  end

  def create
  end
end
```

--------------------------------

### Generate HTML Guides (Ruby on Rails)

Source: https://guides.rubyonrails.org/ruby_on_rails_guides_guidelines

Rake tasks for generating HTML versions of the guides within a Ruby on Rails project. This process involves navigating to the 'guides' directory, installing dependencies, and executing the generation task.

```bash
bundle exec rake guides:generate
# or
bundle exec rake guides:generate:html
```

--------------------------------

### Install SQLite3 (FreeBSD)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs the sqlite3 package on FreeBSD using pkg_add, required for the sqlite3-ruby gem.

```bash
# pkg_add -r sqlite3
```

--------------------------------

### Example Rails Application Template

Source: https://guides.rubyonrails.org/v5.0/rails_application_templates

A sample Rails template file (`template.rb`) demonstrating the use of DSL methods like `generate`, `route`, `rails_command`, and `after_bundle` to customize a Rails application.

```ruby
# template.rb
generate(:scaffold, "person name:string")
route "root to: 'people#index'"
rails_command("db:migrate")
after_bundle do 
  git :init
  git add: "."
  git commit: "Q{ -m 'Initial commit' }
end
```

--------------------------------

### Example CHANGELOG Entry Format

Source: https://guides.rubyonrails.org/v4.2/contributing_to_ruby_on_rails

Illustrates the standard format for entries in the CHANGELOG file. Includes guidelines for describing changes, adding code examples, and referencing GitHub issues.

```markdown
*  Summary of a change that briefly describes what was changed. You can use multiple
    lines and wrap them at around 80 characters. Code examples are ok, too, if needed:
          class Foo
              def bar
                  puts 'baz'
              end
          end
    You can continue after the code example and you can attach issue number. GH#1234
    *Your Name*
```

--------------------------------

### Access Application Root Path in Console

Source: https://guides.rubyonrails.org/v5.1/command_line

Within the Rails console, the 'app' object provides access to various application helpers, including URL and path helpers. This example demonstrates how to get the root path of the application.

```ruby
>> app.root_path
=> "/"
```

--------------------------------

### Rackup Server App Construction

Source: https://guides.rubyonrails.org/initialization

The `Rackup::Server#app` method determines the application to be built, either from a string using `build_app_from_string` or from a configuration file (defaulting to `config.ru`) using `build_app_and_options_from_config`.

```ruby
module Rackup
  class Server
    def app
      @app ||= options[:builder] ? build_app_from_string : build_app_and_options_from_config
    end

    # ...

    private
      def build_app_and_options_from_config
        if !::File.exist? options[:config]
          abort "configuration #{options[:config]} not found"
        end

        Rack::Builder.parse_file(self.options[:config])
      end

      def build_app_from_string
        Rack::Builder.new_from_string(self.options[:builder])
      end
  end
end
```

--------------------------------

### Rails View to Display 'Hello, Rails!'

Source: https://guides.rubyonrails.org/v6.1/getting_started

An ERB template for a Rails view. This file, typically located at `app/views/articles/index.html.erb`, displays a simple 'Hello, Rails!' heading when rendered by the corresponding controller action.

```html
<h1>Hello, Rails!</h1>

```

--------------------------------

### Implement Presence Validation in Ruby on Rails

Source: https://guides.rubyonrails.org/getting_started

Shows how to add a `presence: true` validation to the `name` attribute of a `Product` model in Ruby on Rails. It demonstrates the effect of this validation when attempting to save a product without a name.

```ruby
class Product < ApplicationRecord
  validates :name, presence: true
end

```

```ruby
store(dev)> reload!
Reloading...


```

```ruby
store(dev)> product = Product.new
store(dev)> product.save
=> false

```

```ruby
store(dev)> product.errors
=> #<ActiveModel::Errors [#<ActiveModel::Error attribute=name, type=blank, options={}>]>

```

```ruby
store(dev)> product.errors.full_messages
=> ["Name can't be blank"]

```

--------------------------------

### HTML Email Template for In Stock Notification

Source: https://guides.rubyonrails.org/getting_started

The HTML template for the 'in_stock' email. It displays a "Good news!" message and provides a clickable link to the product using `product_url`, ensuring the link is fully qualified for email clients.

```erb
<h1>Good news!</h1>

<p><%= link_to @product.name, product_url(@product) %> is back in stock.</p>
```

--------------------------------

### Rails Project Initialization with Git

Source: https://guides.rubyonrails.org/v6.1/upgrading_ruby_on_rails

This snippet demonstrates how to initialize a Rails project, generate a scaffold, set the root route, migrate the database, and commit initial changes using Git. It can be wrapped in an `after_bundle` block to ensure execution after dependencies are installed.

```ruby
generate(:scaffold, "person name:string")
route "root to: 'people#index'"
rake("db:migrate")

git :init
git add: "."
git commit: %Q{ -m 'Initial commit' }
```

```ruby
generate(:scaffold, "person name:string")
route "root to: 'people#index'"
rake("db:migrate")

after_bundle do
  git :init
  git add: "."
  git commit: %Q{ -m 'Initial commit' }
end
```

--------------------------------

### I18n: Default English Locale Configuration (YAML)

Source: https://guides.rubyonrails.org/getting_started

This YAML snippet defines the default English translations for a Rails application. It includes a basic "hello" translation and a nested translation for "products.index.title".

```yaml
en:
  hello: "Hello world"
  products:
    index:
      title: "Products"
```

--------------------------------

### Generate New Rails App with Dev Container

Source: https://guides.rubyonrails.org/getting_started_with_devcontainer

This command uses the `rails-new` tool to generate a new Rails application named 'store' with dev container support. It automates the setup of a containerized development environment, ensuring all necessary Ruby and Rails versions and dependencies are managed within Docker.

```bash
#!/bin/bash
rails-new store --devcontainer

```

--------------------------------

### Rails: Display About Information

Source: https://guides.rubyonrails.org/v7.2/command_line

The `bin/rails about` command provides a comprehensive overview of the Rails application's environment. It includes versions of Ruby, RubyGems, Rails, Rack, middleware stack, application root, environment name, database adapter, and schema version. This is useful for debugging and seeking support.

```bash
$ bin/rails about
About your application's environment
Rails version             7.2.0
Ruby version              3.1.0 (x86_64-linux)
RubyGems version          3.3.7
Rack version              3.0.8
JavaScript Runtime        Node.js (V8)
Middleware:               ActionDispatch::HostAuthorization, Rack::Sendfile, ActionDispatch::Static, ActionDispatch::Executor, ActionDispatch::ServerTiming, ActiveSupport::Cache::Strategy::LocalCache::Middleware, Rack::Runtime, Rack::MethodOverride, ActionDispatch::RequestId, ActionDispatch::RemoteIp, Sprockets::Rails::QuietAssets, Rails::Rack::Logger, ActionDispatch::ShowExceptions, WebConsole::Middleware, ActionDispatch::DebugExceptions, ActionDispatch::ActionableExceptions, ActionDispatch::Reloader, ActionDispatch::Callbacks, ActiveRecord::Migration::CheckPending, ActionDispatch::Cookies, ActionDispatch::Session::CookieStore, ActionDispatch::Flash, ActionDispatch::ContentSecurityPolicy::Middleware, ActionDispatch::PermissionsPolicy::Middleware, Rack::Head, Rack::ConditionalGet, Rack::ETag, Rack::TempfileReaper
Application root          /home/foobar/my_app
Environment               development
Database adapter          sqlite3
Database schema version   20180205173523


```

--------------------------------

### Define Product Fixture Data for Rails Tests

Source: https://guides.rubyonrails.org/getting_started

This YAML snippet defines fixture data for the 'Product' model in Rails. It specifies product attributes like 'name' and 'inventory_count', used to populate the test database.

```yaml
tshirt:
  name: T-Shirt
  inventory_count: 15
```

--------------------------------

### Configure Rails Server Port and Environment

Source: https://guides.rubyonrails.org/v6.0/command_line

Shows how to start the Rails server on a custom port and specify a different environment (e.g., production) using command-line options.

```bash
rails server -e production -p 4000
```

--------------------------------

### Rackup Server Wrapped App Logic

Source: https://guides.rubyonrails.org/initialization

The `Rackup::Server#wrapped_app` method memoizes and returns the Rack application. It calls `build_app` with the result of the `app` method, which determines how the application is constructed.

```ruby
module Rackup
  class Server
    def wrapped_app
      @wrapped_app ||= build_app app
    end
  end
end
```

--------------------------------

### Setup Database (Ruby on Rails)

Source: https://guides.rubyonrails.org/v7.0/active_record_multiple_databases

Command to create all databases, load all schemas, and initialize with seed data. This command is useful for setting up a new development environment. It can be used for all databases or specific ones like 'animals' or 'primary'.

```bash
rails db:setup
rails db:setup:animals
rails db:setup:primary
```

--------------------------------

### Rails Server Initialization and Startup

Source: https://guides.rubyonrails.org/v7.0/initialization

This snippet shows the `start` method of `Rails::Server`, which is responsible for setting up the server environment. It includes signal trapping, directory creation, development caching setup, and logging configuration before invoking the parent `Rack::Server.start` method.

```ruby
module Rails
  class Server < ::Rack::Server
    def start(after_stop_callback = nil)
      trap(:INT) { exit }
      create_tmp_directories
      setup_dev_caching
      log_to_stdout if options[:log_stdout]

      super()
      # ...
    end

    private
      def setup_dev_caching
        if options[:environment] == "development"
          Rails::DevCaching.enable_by_argument(options[:caching])
        end
      end

      def create_tmp_directories
        %w(cache pids sockets).each do |dir_to_make|
          FileUtils.mkdir_p(File.join(Rails.root, "tmp", dir_to_make))
        end
      end

      def log_to_stdout
        wrapped_app # touch the app so the logger is set up

        console = ActiveSupport::Logger.new(STDOUT)
        console.formatter = Rails.logger.formatter
        console.level = Rails.logger.level

        unless ActiveSupport::Logger.logger_outputs_to?(Rails.logger, STDOUT)
          Rails.logger.extend(ActiveSupport::Logger.broadcast(console))
        end
      end
  end
end

```

--------------------------------

### Constrain Rails Routes by HTTP Verb

Source: https://guides.rubyonrails.org/v4.1/routing

This example demonstrates how to constrain routes to specific HTTP verbs using methods like get, post, etc., or by using the match method with the :via option for multiple verbs or all verbs.

```ruby
match 'photos', to: 'photos#show', via: [:get, :post]
```

```ruby
match 'photos', to: 'photos#show', via: :all
```

--------------------------------

### Install and Update Bundler Gem

Source: https://guides.rubyonrails.org/v6.0/development_dependencies_install

Installs or updates the Bundler gem, a dependency manager for Ruby projects. It also shows how to run `bundle install` to install project dependencies, with an option to skip database setup.

```shell
gem install bundler
gem update bundler
bundle install
bundle install --without db
```

--------------------------------

### HTML: Example HTTP header response with 201 Created

Source: https://guides.rubyonrails.org/v6.0/layouts_and_rendering

This is an example HTTP header response indicating a successful creation (201 Created). It includes standard headers and a 'Location' header pointing to the resource's URL.

```http
HTTP/1.1 201 Created
Connection: close
Date: Sun, 24 Jan 2010 12:16:44 GMT
Transfer-Encoding: chunked
Location: /photos/1
Content-Type: text/html; charset=utf-8
X-Runtime: 0.083496
Set-Cookie: _blog_session=...snip...; path=/; HttpOnly
Cache-Control: no-cache
```

--------------------------------

### Install Rails Gem

Source: https://guides.rubyonrails.org/install_ruby_on_rails

Installs the latest version of the Rails framework and its dependencies using Ruby's gem package manager.

```shell
$ gem install rails

```

--------------------------------

### Add 'Back' Link to New Post Form (Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This snippet shows how to add a 'Back' link below the form on the new post page, allowing users to return to the main posts index. It uses the `posts_path` helper.

```erb
<%= form_for :post do |f| %> 
  ... 
<% end %> 
<%= link_to 'Back', posts_path %>
```

--------------------------------

### Rails Routes Output for Articles

Source: https://guides.rubyonrails.org/v5.0/getting_started

This is the output from the `bin/rails routes` command, showing the defined routes for the `articles` resource. It lists the HTTP verbs, URI patterns, and the corresponding Controller#Action. This is crucial for understanding where forms and other requests will be directed.

```bash
$ bin/rails routes
      Prefix Verb      URI Pattern              Controller#Action
    articles GET       /articles(.:format)      articles#index
             POST      /articles(.:format)      articles#create
 new_article GET       /articles/new(.:format)  articles#new
edit_article GET      /articles/:id/edit(.:format) articles#edit
     article GET       /articles/:id(.:format)  articles#show
             PATCH     /articles/:id(.:format)  articles#update
             PUT       /articles/:id(.:format)  articles#update
             DELETE    /articles/:id(.:format)  articles#destroy
        root GET       /                        welcome#index
```

--------------------------------

### Get All Parents with parents in Ruby

Source: https://guides.rubyonrails.org/v5.0/active_support_core_extensions

The `parents` method, available through Active Support, returns an array of all containing modules starting from the immediate parent up to the top-level `Object`. The array is ordered from the nearest parent to the furthest.

```Ruby
module X
  module Y
    module Z
    end
  end
end
M = X::Y::Z

X::Y::Z.parents # => [X::Y, X, Object]
M.parents       # => [X::Y, X, Object]
```

--------------------------------

### Setup Database with Schema and Seed Data in Rails

Source: https://guides.rubyonrails.org/v4.1/migrations

Creates the database, loads the schema from schema.rb, and initializes it with seed data. This task is useful for setting up a new development environment.

```bash
rake db:setup
```

--------------------------------

### Inspecting Generated Rails Routes

Source: https://guides.rubyonrails.org/v7.2/getting_started

Command to display all routes generated by the Rails application, including prefixes, HTTP verbs, URI patterns, and corresponding controller actions.

```bash
$ bin/rails routes

```

--------------------------------

### Render Partial in Rails New Article View

Source: https://guides.rubyonrails.org/v6.0/getting_started

This ERB template renders the shared article form partial in the 'new article' view. It includes a page title and a link back to the articles index. The render call assumes the '_form.html.erb' partial is located in the same directory.

```erb
<%# app/views/articles/new.html.erb %>
<h1>New Article</h1>
<%= render 'form' %>
<%= link_to 'Back', articles_path %>
```

--------------------------------

### Install Memcached (Ubuntu)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs Memcached on Ubuntu using apt-get, a caching system used for some Rails tests.

```bash
$ sudo apt-get install memcached
```

--------------------------------

### Generate HTML Rails Guides in a Specific Language

Source: https://guides.rubyonrails.org/v7.0/contributing_to_ruby_on_rails

This command generates the Ruby on Rails guides in HTML format for a specified language (e.g., Italian). It requires installing necessary gems, navigating to the guides directory, and executing a rake task with the language code. Ensure you have the correct dependencies installed.

```bash
$ bundle install --without job cable storage ujs test db
$ cd guides/
$ bundle exec rake guides:generate:html GUIDES_LANGUAGE=it-IT
```

--------------------------------

### Get Beginning and End of Year in Ruby

Source: https://guides.rubyonrails.org/v5.0/active_support_core_extensions

The `beginning_of_year` and `end_of_year` methods return the dates corresponding to the start and end of a given year. These methods are useful for setting date ranges or performing yearly calculations.

```ruby
d = Date.new(2010, 5, 9) 
puts d.beginning_of_year
puts d.end_of_year
```

--------------------------------

### Start Rails Server

Source: https://guides.rubyonrails.org/v3.0/command_line

Starts the WEBrick web server for a Rails application. This command is used to run the application locally and access it via a web browser. Ensure no backup files are present in the views directory to avoid rendering issues.

```bash
$ rails server
=> Booting WEBrick...
```

--------------------------------

### Install SQLite3 Ruby Gem

Source: https://guides.rubyonrails.org/v2.3/getting_started

This command installs the sqlite3-ruby gem, which provides Ruby bindings for the SQLite3 database. This is necessary if SQLite is not pre-installed on your system.

```bash
$ gem install sqlite3-ruby

```

--------------------------------

### Render Collection of Comments in Rails

Source: https://guides.rubyonrails.org/v6.0/getting_started

This ERB template shows how to render a collection of comments using a partial. The `render @article.comments` call iterates through the comments and renders the '_comment.html.erb' partial for each one, assigning the current comment to a local 'comment' variable.

```erb
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>
<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>
<h2>Comments</h2>
<%= render @article.comments %>
<h2>Add a comment:</h2>
<%= form_with(model: [@article, @article.comments.build], local: true) do |form| %>
  <p>
    <%= form.label :commenter %><br>
    <%= form.text_field :commenter %>
  </p>
  <p>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
  </p>
  <p>
    <%= form.submit %>
  </p>
<% end %>
<%= link_to 'Edit', edit_article_path(@article) %> | <%= link_to 'Back', articles_path %>
```

--------------------------------

### Running Plugin Tests with Rake (Shell)

Source: https://guides.rubyonrails.org/v2.3/plugins

This command demonstrates how to navigate to a plugin directory and execute tests using `rake`. It shows the basic command to run tests and how to specify a database adapter using the `DB` environment variable.

```shell
cd vendor/plugins/yaffle
rake

rake DB=sqlite
rake DB=sqlite3
rake DB=mysql
rake DB=postgresql

```

--------------------------------

### Implement Basic Rails Integration Test for Welcome Page

Source: https://guides.rubyonrails.org/v7.0/testing

This Ruby code defines an integration test for a blog application's welcome page. It uses `get "/"` to simulate a request to the root path and `assert_select "h1", "Welcome#index"` to verify that the expected HTML heading is present in the response. This test relies on Rails' integration testing helpers.

```ruby
require "test_helper"

class BlogFlowTest < ActionDispatch::IntegrationTest
  test "can see the welcome page" do
    get "/"
    assert_select "h1", "Welcome#index"
  end
end

```

--------------------------------

### Render Partial in Rails Edit Article View

Source: https://guides.rubyonrails.org/v6.0/getting_started

This ERB template renders the shared article form partial in the 'edit article' view. It includes a page title and a link back to the articles index. The render call assumes the '_form.html.erb' partial is located in the same directory.

```erb
<%# app/views/articles/edit.html.erb %>
<h1>Edit Article</h1>
<%= render 'form' %>
<%= link_to 'Back', articles_path %>
```

--------------------------------

### Install MySQL and PostgreSQL Gems (FreeBSD)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs MySQL 5.6 client and server, and PostgreSQL 9.2 client and server on FreeBSD using pkg_add. Alternatively, these can be installed via ports under the 'databases' folder.

```bash
# pkg_add -r mysql56-client mysql56-server
# pkg_add -r postgresql92-client postgresql92-server
```

--------------------------------

### Display Application Environment with bin/rails about

Source: https://guides.rubyonrails.org/v6.1/command_line

The bin/rails about command provides a summary of your Rails application's environment, including versions of Ruby, Rails, and its subcomponents, as well as application root, environment name, database adapter, and schema version.

```bash
$ bin/rails about
About your application's environment
Rails version             6.0.0
Ruby version              2.5.0 (x86_64-linux)
RubyGems version          2.7.3
Rack version              2.0.4
JavaScript Runtime        Node.js (V8)
Middleware:               Rack::Sendfile, ActionDispatch::Static, ActionDispatch::Executor, ActiveSupport::Cache::Strategy::LocalCache::Middleware, Rack::Runtime, Rack::MethodOverride, ActionDispatch::RequestId, ActionDispatch::RemoteIp, Sprockets::Rails::QuietAssets, Rails::Rack::Logger, ActionDispatch::ShowExceptions, WebConsole::Middleware, ActionDispatch::DebugExceptions, ActionDispatch::Reloader, ActionDispatch::Callbacks, ActiveRecord::Migration::CheckPending, ActionDispatch::Cookies, ActionDispatch::Session::CookieStore, ActionDispatch::Flash, Rack::Head, Rack::ConditionalGet, Rack::ETag
Application root          /home/foobar/commandsapp
Environment               development
Database adapter          sqlite3
Database schema version   20180205173523
```

--------------------------------

### Verify SQLite3 Installation

Source: https://guides.rubyonrails.org/v6.1/getting_started

Checks if SQLite3 is installed and available in the system's load path. SQLite3 is a database commonly used with Rails applications.

```bash
$
sqlite3 --version
```

--------------------------------

### Rails System Tests for Product Creation and Update

Source: https://context7.com/context7/guides_rubyonrails/llms.txt

System tests for the Products feature, simulating user interactions like visiting pages, filling forms, and clicking buttons to create and update products. These tests ensure the front-end behaves as expected.

```ruby
require "application_system_test_case"

class ProductsTest < ApplicationSystemTestCase
  test "creating a product" do
    visit products_path
    click_on "New Product"

    fill_in "Name", with: "Test Product"
    fill_in "Price", with: "29.99"
    fill_in "Description", with: "A test product"

    click_on "Create Product"

    assert_text "Product was successfully created"
    assert_text "Test Product"
  end

  test "updating a product" do
    product = products(:one)

    visit product_path(product)
    click_on "Edit"

    fill_in "Name", with: "Updated Product Name"
    click_on "Update Product"

    assert_text "Product was successfully updated"
    assert_text "Updated Product Name"
  endend
```

--------------------------------

### Example CHANGELOG Entry for Rails Contributions

Source: https://guides.rubyonrails.org/v4.1/contributing_to_ruby_on_rails

This snippet demonstrates the recommended format for a CHANGELOG entry in Rails. It includes a summary of the change, optional multi-line descriptions, code examples, issue references, and the author's name.

```markdown
*  Summary of a change that briefly describes what was changed. You can use multiple
     lines and wrap them at around 80 characters. Code examples are ok, too, if needed:
         class Foo
           def bar
             puts 'baz'
           end
         end
    You can continue after the code example and you can attach issue number. GH#1234
    *Your Name*
```

--------------------------------

### Basic HTTP Authentication in Rails ArticlesController

Source: https://guides.rubyonrails.org/v4.2/getting_started

This snippet demonstrates how to implement basic HTTP authentication for all actions in the ArticlesController except for 'index' and 'show', using the http_basic_authenticate_with method. It requires a name and password for authentication.

```ruby
class ArticlesController < ApplicationController
  http_basic_authenticate_with name: "dhh", password: "secret", except: [:index, :show]

  def index
    @articles = Article.all
  end
  # snippet for brevity
```

--------------------------------

### Example CHANGELOG Entry Format

Source: https://guides.rubyonrails.org/v5.1/contributing_to_ruby_on_rails

This illustrates the expected format for a CHANGELOG entry, including a summary of the change, optional multi-line descriptions, code examples indented with 4 spaces, and the author's name. Issue numbers can also be referenced.

```markdown
*  Summary of a change that briefly describes what was changed. You can use multiple
    lines and wrap them at around 80 characters. Code examples are ok, too, if needed:
          class Foo
            def bar
              puts 'baz'
            end
          end
    You can continue after the code example and you can attach issue number. GH#1234
    *Your Name*
```

--------------------------------

### Install Memcached (OSX)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs Memcached on macOS using Homebrew, a caching system used for some Rails tests.

```bash
$ brew install memcached
```

--------------------------------

### Rackup Configuration for Rails

Source: https://guides.rubyonrails.org/v4.1/rails_on_rack

Provides a sample `config.ru` file for a Rails application, demonstrating how to configure Rackup to use Rails. It includes requiring the Rails environment and running the Rails application with specified middlewares.

```ruby
# Rails.root/config.ru
require ::File.expand_path('../config/environment', __FILE__)
use Rails::Rack::Debugger
use Rack::ContentLength
run Rails.application
```

--------------------------------

### Start Rails Server with Puma

Source: https://guides.rubyonrails.org/v6.0/command_line

Launches the Puma web server for a Rails application in the development environment. This is the standard command to make your application accessible via a web browser.

```bash
cd commandsapp
rails server
```

--------------------------------

### Create New Rails App with Git and PostgreSQL

Source: https://guides.rubyonrails.org/v4.0/command_line

This command initializes a new Rails application in the current directory, enabling Git integration and configuring PostgreSQL as the database. It requires the `rails` gem and assumes PostgreSQL is installed.

```bash
$ mkdir gitapp
$ cd gitapp
$ git init
Initialized empty Git repository in .git/
$ rails new . --git --database=postgresql
```

--------------------------------

### Create Post Action in Rails Controller

Source: https://guides.rubyonrails.org/v4.0/getting_started

This Ruby code defines the 'create' action in a Rails controller to initialize a new Post object with permitted parameters and save it to the database. It requires the 'post' parameters to permit 'title' and 'text' attributes.

```ruby
def create
  @post = Post.new(post_params)
  @post.save
  redirect_to @post
end

private

def post_params
  params.require(:post).permit(:title, :text)
end
```

--------------------------------

### Example Rails Metal Application Code

Source: https://guides.rubyonrails.org/v2.3/rails_on_rack

Provides an example of the code generated for a Rails Metal application. This code defines a simple Rack application that responds to specific paths.

```ruby
# Allow the metal piece to run in isolation
require(File.dirname(__FILE__) + "/../../config/environment") unless defined?(Rails)

class Poller
  def self.call(env)
    if env["PATH_INFO"] =~ /\/poller/
      [200, {"Content-Type" => "text/html"}, ["Hello, World!"]]
    else
      [404, {"Content-Type" => "text/html"}, ["Not Found"]]
    end
  end
end
```

--------------------------------

### Configure Action Cable with Connection Options

Source: https://guides.rubyonrails.org/v6.0/5_2_release_notes

Demonstrates how to configure Action Cable's `cable.yml` file to include host, port, database, and password options for establishing connections.

```yaml
development:
  adapter: redis
  url: redis://localhost:6379/1
  host: localhost
  port: 6379
  db: 1
  password: your_redis_password
```

--------------------------------

### Create New Rails Application

Source: https://guides.rubyonrails.org/v4.1/command_line

The `rails new` command scaffolds a new Rails application, setting up the directory structure and necessary files. It requires the Rails gem to be installed. The command outputs a list of created files and runs `bundle install` to set up dependencies.

```bash
$ rails new commandsapp
create  README.rdoc
create  Rakefile
create  config.ru
create  .gitignore
create  Gemfile
create  app
...
create  tmp/cache
...
run bundle install
```

--------------------------------

### Display Comments in Post Show View (Rails ERB)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This ERB code snippet shows how to display a list of comments associated with a post on its show page. It iterates through the `@post.comments` collection and displays the commenter and body of each comment.

```erb
<h2>Comments</h2>
<% @post.comments.each do |comment| %>
  <p>
    <strong>Commenter:</strong>
    <%= comment.commenter %>
  </p>
  <p>
    <strong>Comment:</strong>
    <%= comment.body %>
  </p>
<% end %>
```

--------------------------------

### Install Development Dependencies on Arch Linux

Source: https://guides.rubyonrails.org/v6.0/development_dependencies_install

This command installs required development tools and services for Ruby on Rails on Arch Linux using pacman. It includes MariaDB (as MySQL is not supported), PostgreSQL, Redis, Memcached, and other utilities. Note that it also initializes the MariaDB database and starts services.

```bash
sudo pacman -S sqlite mariadb libmariadbclient mariadb-clients postgresql postgresql-libs redis memcached imagemagick ffmpeg mupdf mupdf-tools poppler yarn libxml2
sudo mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
sudo systemctl start redis mariadb memcached
```

--------------------------------

### Install Webpacker in Rails

Source: https://guides.rubyonrails.org/v6.0/upgrading_ruby_on_rails

Instructions to install Webpacker, the default JavaScript compiler for Rails 6, by adding it to the Gemfile and running the installation command.

```ruby
gem "webpacker"
```

```bash
bin/rails webpacker:install
```

--------------------------------

### Ruby on Rails Migration Execution Output

Source: https://guides.rubyonrails.org/v5.0/getting_started

This output indicates the successful execution of a database migration in Ruby on Rails. It shows the migration process starting (`migrating`), the specific action being performed (e.g., `create_table(:articles)`), the time taken for the operation, and confirmation that the migration has been completed (`migrated`).

```text
== CreateArticles: migrating ===============
-- create_table(:articles)
  -> 0.0019s
== CreateArticles: migrated (0.0020s) =======
```

--------------------------------

### Rails Update Task Example Output

Source: https://guides.rubyonrails.org/v6.0/upgrading_ruby_on_rails

Example output from the `rails app:update` task, showing file status such as 'identical', 'exist', and 'conflict' during the update process.

```bash
identical  config/boot.rb
exist      config
conflict   config/routes.rb
Overwrite /myapp/config/routes.rb? (enter "h" for help) [Ynaqdh]
force      config/routes.rb
conflict   config/application.rb
Overwrite /myapp/config/application.rb? (enter "h" for help) [Ynaqdh]
force      config/application.rb
conflict   config/environment.rb
...
```

--------------------------------

### Link Back to Articles Index from New Article Form in Rails View

Source: https://guides.rubyonrails.org/v4.1/getting_started

Includes a 'Back' link below the article creation form. This link uses the 'link_to' helper and the 'articles_path' route helper to navigate the user back to the main articles listing page after interacting with the new article form.

```html
<%= form_for :article, url: articles_path do |f| %>
  ...
<% end %>
<%= link_to 'Back', articles_path %>
```

--------------------------------

### Install/Update Bundler

Source: https://guides.rubyonrails.org/ruby_on_rails_guides_guidelines

Commands to install or update Bundler, a dependency manager for Ruby projects. Bundler ensures you have the correct versions of gems for your project.

```bash
gem install bundler
gem update bundler
```

--------------------------------

### Configure Bundler and Bootsnap

Source: https://guides.rubyonrails.org/initialization

The `config/boot.rb` script initializes Bundler by setting the `BUNDLE_GEMFILE` environment variable and then requires `bundler/setup` to configure the load path for application dependencies. It also requires `bootsnap/setup` to speed up boot time by caching operations.

```ruby
ENV["BUNDLE_GEMFILE"] ||= File.expand_path("../Gemfile", __dir__)

require "bundler/setup" # Set up gems listed in the Gemfile.
require "bootsnap/setup" # Speed up boot time by caching expensive operations.

```

--------------------------------

### Rails Controller: Test AJAX Request

Source: https://guides.rubyonrails.org/v6.1/testing

Tests an AJAX GET request to retrieve an article and asserts the response body and media type. This example demonstrates how to specifically test asynchronous requests and their expected JavaScript responses.

```ruby
test "ajax request" do
  article = articles(:one)
  get article_url(article), xhr: true

  assert_equal "hello world", @response.body
  assert_equal "text/javascript", @response.media_type
end
```

--------------------------------

### Install and Use Mongrel Server with Rails

Source: https://guides.rubyonrails.org/v3.0/command_line

This snippet demonstrates how to install the Mongrel gem and then configure the Rails server to use Mongrel as its backend. This allows for using alternative web servers beyond the default WEBrick.

```shell
$ sudo gem install mongrel
$ rails server mongrel
```

--------------------------------

### Get String Substring from Position with Ruby

Source: https://guides.rubyonrails.org/active_support_core_extensions

The `from` method extracts a substring starting from a given `position` to the end of the string. It handles positive and negative indices. If the position is beyond the string length, it returns `nil`.

```ruby
defined in `active_support/core_ext/string/access.rb`.
"hello".from(0)  # => "hello"
"hello".from(2)  # => "llo"
"hello".from(-2) # => "lo"
"hello".from(10) # => nil
```

--------------------------------

### Install Ruby Gem Dependencies with Bundler

Source: https://guides.rubyonrails.org/v7.0/development_dependencies_install

Installs all Ruby gem dependencies specified in the project's Gemfile using Bundler. An optional flag can be used to exclude database-related gems.

```bash
$ bundle install
$ bundle install --without db
```

--------------------------------

### Ruby Method Documentation with Examples Section

Source: https://guides.rubyonrails.org/v7.1/api_documentation_guidelines

Illustrates documenting Ruby methods with a dedicated 'Examples' section for larger or more complex code snippets. It shows how to include multiple example calls and their corresponding outputs.

```Ruby
# ==== Examples
#
#   Person.exists?(5)
#   Person.exists?('5')
#   Person.exists?(name: "David")
#   Person.exists?(name: '5')
#   Person.exists?(name: "David")
#   Person.exists?(['name LIKE ?', "%#{query}%"])

```

--------------------------------

### Wording Style Guide for Rails Documentation

Source: https://guides.rubyonrails.org/v7.1/api_documentation_guidelines

Provides examples of preferred wording for Ruby on Rails API documentation, emphasizing brevity, clarity, and present tense. It illustrates how to write concise and direct sentences, start comments with uppercase letters, and follow punctuation rules.

```ruby
# BAD
# Caching may interfere with being able to see the results
# of code changes.

# GOOD
# Caching interferes with seeing the results of code changes.

# BAD
# Returned a hash that...
# Will return a hash that...
# Return a hash that...

# GOOD
# Returns a hash that...

# BAD
# declares an attribute reader backed by an internally-named
# instance variable

# GOOD
# Declares an attribute reader backed by an internally-named
# instance variable.

```

--------------------------------

### Rails Server Initialization and Signal Handling (Ruby)

Source: https://guides.rubyonrails.org/v4.2/initialization

The `Rails::Server#start` method initializes the server, sets up signal traps for graceful shutdown (e.g., Ctrl+C), creates necessary temporary directories, and configures logging to stdout if specified. It then calls `super` to continue the startup process.

```ruby
def start
  print_boot_information
  trap(:INT) { exit }
  create_tmp_directories
  log_to_stdout if options[:log_stdout]
  super
  ...
end

private

def print_boot_information
  ...
  puts "=> Run `rails server -h` for more startup options"
  ...
  puts "=> Ctrl-C to shutdown server" unless options[:daemonize]
end

def create_tmp_directories
  %w(cache pids sessions sockets).each do |dir_to_make|
    FileUtils.mkdir_p(File.join(Rails.root, 'tmp', dir_to_make))
  end
end

def log_to_stdout
  wrapped_app # touch the app so the logger is set up
  console = ActiveSupport::Logger.new($stdout)
  console.formatter = Rails.logger.formatter
  console.level = Rails.logger.level
  Rails.logger.extend(ActiveSupport::Logger.broadcast(console))
end
```

--------------------------------

### Rails Controller: Implement Show Action for Products

Source: https://guides.rubyonrails.org/getting_started

This snippet demonstrates how to add the 'show' action to the Products controller in a Rails application. It fetches a single product from the database using its ID from the request parameters. Dependencies include the Product model and Rails routing.

```ruby
class ProductsController < ApplicationController
  def index
    @products = Product.all
  end

  def show
    @product = Product.find(params[:id])
  end
end
```

--------------------------------

### Create Initial Products Migration (Ruby)

Source: https://guides.rubyonrails.org/v7.1/active_record_migrations

An example of a Rails ActiveRecord migration to create initial product data. The `up` method creates 5 products, and the `down` method deletes all products. This migration is written in Ruby.

```ruby
class AddInitialProducts < ActiveRecord::Migration[7.1]
  def up
    5.times do |i|
      Product.create(name: "Product ##{i}", description: "A product.")
    end
  end

  def down
    Product.delete_all
  end
end
```

--------------------------------

### Define Rails Route with Parameter

Source: https://guides.rubyonrails.org/getting_started

This route definition in Rails includes a dynamic parameter ':id'. It captures a segment of the URL, such as '/products/1', and makes it available as an 'id' parameter within the controller action. This is essential for fetching specific records.

```ruby
get "/products/:id", to: "products#show"

```

--------------------------------

### Ruby on Rails: Migration for belongs_to/has_one Setup

Source: https://guides.rubyonrails.org/v6.1/association_basics

Provides an example of a Rails migration to create the suppliers and accounts tables, including the foreign key constraint for the one-to-one relationship. It shows both explicit bigint foreign key and the shorthand t.references.

```ruby
class CreateSuppliers < ActiveRecord::Migration[6.0]
  def change
    create_table :suppliers do |t|
      t.string :name
      t.timestamps
    end

    create_table :accounts do |t|
      t.bigint  :supplier_id
      t.string  :account_number
      t.timestamps
    end

    add_index :accounts, :supplier_id
  end
end
```

--------------------------------

### Example CHANGELOG Entry (Ruby)

Source: https://guides.rubyonrails.org/v6.1/contributing_to_ruby_on_rails

Illustrates the format for adding entries to the CHANGELOG file in Rails. It shows how to summarize changes, include multi-line descriptions, embed code examples with indentation, and reference issue numbers. This format helps maintain a clear and informative history of framework modifications.

```text
*   Summary of a change that briefly describes what was changed. You can use multiple
    lines and wrap them at around 80 characters. Code examples are ok, too, if needed:

        class Foo
          def bar
            puts 'baz'
          end
        end

    You can continue after the code example and you can attach issue number.

    Fixes #1234.

    *Your Name*

```

--------------------------------

### Verify Yarn Installation

Source: https://guides.rubyonrails.org/v6.1/getting_started

Confirms that Yarn, a JavaScript package manager, is installed correctly. Yarn is used for managing application dependencies, particularly JavaScript packages.

```bash
$
yarn --version
```

--------------------------------

### Install Development Dependencies on Arch Linux

Source: https://guides.rubyonrails.org/v7.0/development_dependencies_install

This command installs required packages for Ruby on Rails development on Arch Linux using pacman. It includes MariaDB (as MySQL is not supported), PostgreSQL, Redis, Memcached, and other multimedia tools. It also shows how to initialize the database and start services.

```bash
$ sudo pacman -S sqlite mariadb libmariadbclient mariadb-clients postgresql postgresql-libs redis memcached imagemagick ffmpeg mupdf mupdf-tools poppler yarn libxml2
$ sudo mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
$ sudo systemctl start redis mariadb memcached

```

--------------------------------

### Git: Clone Rails Repository

Source: https://guides.rubyonrails.org/v3.1/contributing_to_ruby_on_rails

Command to clone the Ruby on Rails source code repository from GitHub. This is the first step to contributing code.

```bash
git clone git://github.com/rails/rails.git
```

--------------------------------

### Product Mailer Class Definition (Ruby)

Source: https://guides.rubyonrails.org/getting_started

Defines the `ProductMailer` class inheriting from `ApplicationMailer`. The `in_stock` method sets the recipient's email address and assigns the product object for use in the email templates. It uses `params` to pass data to the mailer.

```ruby
class ProductMailer < ApplicationMailer
  # Subject can be set in your I18n file at config/locales/en.yml
  # with the following lookup:
  #
  #   en.product_mailer.in_stock.subject
  #
  def in_stock
    @product = params[:product]
    mail to: params[:subscriber].email
  end
end
```

--------------------------------

### Create Article Form Partial (_form.html.erb) in Rails

Source: https://guides.rubyonrails.org/v4.1/getting_started

This ERB code defines a reusable form partial for creating and editing articles. It handles displaying errors, form fields for title and text, and a submit button. It relies on the @article instance variable being present.

```erb
<%= form_for @article do |f| %>
  <% if @article.errors.any? %>
    <div id="error_explanation">
      <h2><%= pluralize(@article.errors.count, "error") %> prohibited
        this article from being saved:</h2>
      <ul>
        <% @article.errors.full_messages.each do |msg| %>  
          <li><%= msg %></li>
        <% end %>
      </ul>
    </div>
  <% end %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>  
  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>  
  <p>
    <%= f.submit %>
  </p>
<% end %>
```

--------------------------------

### Rails Route Matching GET Request

Source: https://guides.rubyonrails.org/v4.0/routing

Demonstrates how Rails routes incoming GET requests to a controller action. It shows a sample URL and a corresponding route definition that maps the URL to a controller and action, including parameters.

```erb
GET /patients/17
get '/patients/:id', to: 'patients#show'
```

--------------------------------

### Install SQLite3 Development Files (Ubuntu)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs SQLite3 and its development files on Ubuntu, required for the sqlite3-ruby gem used in Rails.

```bash
$ sudo apt-get install sqlite3 libsqlite3-dev
```

--------------------------------

### Start Rails Development Server

Source: https://guides.rubyonrails.org/v6.1/command_line

Starts the embedded web server for local development. This command allows developers to view and test their Rails application in a browser during the development phase.

```bash
bin/rails server
```

--------------------------------

### Rails Server Start Command

Source: https://guides.rubyonrails.org/v4.0/command_line

This command starts the Rails development server. It typically uses WEBrick by default to serve the application locally, allowing developers to test changes in a web browser.

```bash
$ rails server
=> Booting WEBrick...

```

--------------------------------

### Get Ancestry Chain of Ruby Modules

Source: https://guides.rubyonrails.org/v5.1/active_support_core_extensions

The `parents` method returns an array representing the chain of parent modules, starting from the immediate parent up to `Object`. This allows for a complete traversal of a module's containing hierarchy.

```ruby
module X
  module Y
    module Z
    end
  end
end
m = X::Y::Z
X::Y::Z.parents # => [X::Y, X, Object]
m.parents       # => [X::Y, X, Object]
```

--------------------------------

### Create a New Rails Application

Source: https://guides.rubyonrails.org/v4.0/command_line

The `rails new` command initializes a new Rails application with a standard directory structure and essential files. It requires the Rails gem to be installed. It outputs a list of created files and runs `bundle install`.

```shell
$ rails new commandsapp
create  README.rdoc
create  Rakefile
create  config.ru
create  .gitignore
create  Gemfile
create  app
...
create  tmp/cache
...
run  bundle install
```

--------------------------------

### Install Development Libraries for Nokogiri (Arch Linux)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs the libxml2 and libxslt packages on Arch Linux, which are prerequisites for the Nokogiri gem.

```bash
$ sudo pacman -S libxml2 libxslt
```

--------------------------------

### Create Rails App with Git and PostgreSQL

Source: https://guides.rubyonrails.org/v4.1/command_line

This snippet demonstrates creating a new Rails application with Git SCM and PostgreSQL database support. It involves creating a directory, initializing a Git repository, and then running the `rails new` command with specific options. The output shows the files created by Rails and added to Git.

```bash
$ mkdir gitapp
$ cd gitapp
$ git init
Initialized empty Git repository in .git/
$ rails new . --git --database=postgresql
     exist
     create  app/controllers
     create  app/helpers
...
     create  tmp/cache
     create  tmp/pids
     create  Rakefile
add 'Rakefile'
     create  README.rdoc
add 'README.rdoc'
     create  app/controllers/application_controller.rb
add 'app/controllers/application_controller.rb'
     create  app/helpers/application_helper.rb
...
     create  log/test.log
add 'log/test.log'
```

--------------------------------

### Define Rails POST Route

Source: https://guides.rubyonrails.org/getting_started

This snippet demonstrates how to define a route for POST requests in Rails. It directs POST requests to the '/products' path to the 'create' action of the 'ProductsController'. This is commonly used for form submissions that create new data records.

```ruby
post "/products", to: "products#create"

```

--------------------------------

### Start a Homebrew Service on macOS

Source: https://guides.rubyonrails.org/v7.1/development_dependencies_install

Starts a specific service managed by Homebrew on macOS, such as MySQL. Replace 'mysql' with the desired service name.

```bash
$ brew services start mysql
```

--------------------------------

### Navigation Links in Rails Views

Source: https://guides.rubyonrails.org/v4.2/getting_started

Demonstrates the use of Rails' built-in `link_to` helper and path helpers to create navigation links within different views. These links allow users to navigate to the articles index, create new articles, and go back to the list from show or new article pages.

```html+erb
<h1>Hello, Rails!</h1>
<%= link_to 'My Blog', controller: 'articles' %>
```

```html+erb
<%= link_to 'New article', new_article_path %>
```

```html+erb
<%= form_for :article, url: articles_path do |f| %> 
  ...
<% end %>
<%= link_to 'Back', articles_path %>
```

```html+erb
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>
<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>
<%= link_to 'Back', articles_path %>
```

--------------------------------

### Install MySQL and PostgreSQL Development Files (Fedora/CentOS)

Source: https://guides.rubyonrails.org/v4.0/development_dependencies_install

Installs MySQL server and development packages, along with PostgreSQL server and development packages, essential for Rails database testing on Fedora or CentOS systems.

```bash
$ sudo yum install mysql-server mysql-devel
$ sudo yum install postgresql-server postgresql-devel
```

--------------------------------

### Rails Controller Test: AJAX Request Example

Source: https://guides.rubyonrails.org/testing

Tests an AJAX request to fetch an article. It simulates a GET request with the `xhr: true` option and asserts the response body and media type, verifying that the server responds with JavaScript.

```ruby
test "AJAX request" do
  article = articles(:one)
  get article_url(article), xhr: true

  assert_equal "hello world", @response.body
  assert_equal "text/javascript", @response.media_type
end
```

--------------------------------

### Specify Request Method for Match Routes in Rails

Source: https://guides.rubyonrails.org/v7.1/upgrading_ruby_on_rails

This example shows the requirement in Rails 4.0 to specify the request method when using `match` in routes. It contrasts the Rails 3.x syntax with the updated Rails 4.x syntax, which includes `via: :get`.

```ruby
# Rails 3.x
match '/' => 'root#index'
```

```ruby
# becomes
match '/' => 'root#index', via: :get
```

--------------------------------

### Run EXPLAIN on Rails Queries (MySQL Example)

Source: https://guides.rubyonrails.org/v3.2/active_record_querying

Executes an SQL EXPLAIN on a Rails query to analyze its performance, specifically shown with a MySQL example involving a join. The `.explain` method executes the query and fetches the query plan from the database.

```ruby
User.where(:id => 1).joins(:posts).explain
```

--------------------------------

### Install Ruby Gem

Source: https://guides.rubyonrails.org/v2.3/command_line

This command installs the sqlite3-ruby gem, which is necessary for interacting with the SQLite3 database in Rails applications. It requires RubyGems to be installed.

```bash
gem install sqlite3-ruby
```

--------------------------------

### Create a New Rails Application via Command-line

Source: https://guides.rubyonrails.org/api_documentation_guidelines

Shows the command-line instruction to create a new Ruby on Rails project named 'zomg'. This is a foundational command for starting new Rails applications.

```bash
# Run the following command:
#   $ bin/rails new zomg
#   ...

```

--------------------------------

### Rails View: Refactored Link to Product Show Page with Link_to Helper

Source: https://guides.rubyonrails.org/getting_started

This refactored ERB view uses the Rails 'link_to' helper and the 'product_path' helper (implicitly via passing the product object) to generate links to individual product show pages. This approach is cleaner and more idiomatic Rails compared to manual URL construction.

```html
<h1>Products</h1>

<div id="products">
  <% @products.each do |product| %>
    <div>
      <%= link_to product.name, product %>
    </div>
  <% end %>
</div>
```

--------------------------------

### Install Dependencies on FreeBSD

Source: https://guides.rubyonrails.org/v6.1/development_dependencies_install

Installs necessary packages for Rails development on FreeBSD, including database clients, caching services, and media processing tools. Redis is installed via ports.

```bash
pkg install sqlite3 mysql80-client mysql80-server postgresql11-client postgresql11-server memcached imagemagick ffmpeg mupdf yarn libxml2
# portmaster databases/redis
```

--------------------------------

### Ruby on Rails: Querying has_many Collection Methods

Source: https://guides.rubyonrails.org/association_basics

Shows how to query a `has_many` association collection in Ruby on Rails. Examples include checking if the collection is empty, getting its size, finding specific records, and performing conditional queries.

```ruby
@book_ids = @author.book_ids

# In ERB template:
<% if @author.books.empty? %>
  No Books Found
<% end %>

@book_count = @author.books.size

@available_book = @author.books.find(1)

@available_books = @author.books.where(available: true)
@available_book = @available_books.first

@author.books.exists?(id: 1)
```

--------------------------------

### Install Development Libraries for Nokogiri (FreeBSD)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs the libxml2 and libxslt packages on FreeBSD using pkg_add, which are dependencies for the Nokogiri gem.

```bash
# pkg_add -r libxml2 libxslt
```

--------------------------------

### Example of button_to rendering (Ruby)

Source: https://guides.rubyonrails.org/configuring

Demonstrates how `button_to` renders different HTML tags based on its content and the `button_to_generates_button_tag` configuration. This example shows the default behavior when the config is false.

```ruby
<%= button_to "Content", "/" %>
# => <input type="submit" value="Content">

<%= button_to "/" do %>
  Content
<% end %>
# => <button type="submit">Content</button>
```

--------------------------------

### Rails Controller for Article Creation and Updates

Source: https://guides.rubyonrails.org/v5.1/getting_started

This Ruby code defines the `new` and `create` actions for an `ArticlesController` in Rails. The `new` action initializes an `@article` instance, while the `create` action attempts to save a new article, rendering the 'new' template with errors if saving fails. It also includes a private `article_params` method for strong parameter handling.

```ruby
def new
  @article = Article.new
end

def create
  @article = Article.new(article_params)
  if @article.save
    redirect_to @article
  else
    render 'new'
  end
end

private

def article_params
    params.require(:article).permit(:title, :text)
  end
```

--------------------------------

### Define Regular Routes with Bound Parameters (Ruby on Rails)

Source: https://guides.rubyonrails.org/v5.1/routing

Illustrates how to define non-resourceful routes in Rails using `get` with optional parameters. This example shows how a URL like `/photos/1` can be mapped to a controller action, with parameters like `:id` being bound.

```ruby
get 'photos(/:id)', to: :display
```

--------------------------------

### Rails Migration File Example

Source: https://guides.rubyonrails.org/v7.2/active_record_migrations

An example of a standalone migration file in Rails, demonstrating the naming convention and basic structure of a migration class. It includes the timestamp and the class definition.

```ruby
# db/migrate/20240502101659_add_part_number_to_products.rb
class AddPartNumberToProducts < ActiveRecord::Migration[7.2]
  def change
  end
end
```

--------------------------------

### View Generated Rails Routes

Source: https://guides.rubyonrails.org/v5.0/getting_started

This command displays all the routes defined in your Rails application, including those generated by `resources` and custom routes. It's useful for verifying route configurations and understanding how requests are mapped to controllers and actions.

```bash
$ bin/rails routes
```

--------------------------------

### Example Middleware Stack Output

Source: https://guides.rubyonrails.org/v3.2/rails_on_rack

Presents a sample output from the `rake middleware` task for a typical Rails application. It lists various middlewares, including ActionDispatch, Rack, ActiveSupport, and application-specific runners.

```shell
use ActionDispatch::Static
use Rack::Lock
use ActiveSupport::Cache::Strategy::LocalCache
use Rack::Runtime
use Rails::Rack::Logger
use ActionDispatch::ShowExceptions
use ActionDispatch::DebugExceptions
use ActionDispatch::RemoteIp
use Rack::Sendfile
use ActionDispatch::Callbacks
use ActiveRecord::ConnectionAdapters::ConnectionManagement
use ActiveRecord::QueryCache
use ActionDispatch::Cookies
use ActionDispatch::Session::CookieStore
use ActionDispatch::Flash
use ActionDispatch::ParamsParser
use Rack::MethodOverride
use ActionDispatch::Head
use ActionDispatch::BestStandardsSupport
run Blog::Application.routes
```

--------------------------------

### Rack Server Option Parser Setup (Ruby)

Source: https://guides.rubyonrails.org/v3.2/initialization

Initializes an `OptionParser` for Rack server command-line arguments. This example shows the banner and a port option, with a note that it's often overridden in subclasses like `Rails::Server`.

```ruby
def opt_parser
  Options.new
end

# In Rails::Server, this is often overridden:
def parse!(args)
  args, options = args.dup, {}
  opt_parser = OptionParser.new do |opts|
    opts.banner = "Usage: rails server [mongrel, thin, etc] [options]"
    opts.on("-p", "--port=port", Integer,
            "Runs Rails on the specified port.",
            "Default: 3000") { |v| options[:Port] = v }
    # ... other options
  end
  # ... rest of the method
end
```

--------------------------------

### Install SQLite3 Development Files (Fedora/CentOS)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs SQLite3 and its development files on Fedora or CentOS systems, needed for the sqlite3-ruby gem.

```bash
$ sudo yum install sqlite3 sqlite3-devel
```

--------------------------------

### Run EXPLAIN on Rails Queries (MySQL Example)

Source: https://guides.rubyonrails.org/v4.2/active_record_querying

The `explain` method allows you to analyze the execution plan of a database query generated by Active Record. This example shows the output for a query with a join on MySQL.

```ruby
User.where(id: 1).joins(:articles).explain
```

```sql
EXPLAIN for: SELECT `users`.* FROM `users` INNER JOIN `articles` ON `articles`.`user_id` = `users`.`id` WHERE `users`.`id` = 1
+----+-------------+----------+-------+---------------+------------------------------------------------------+
| id | select_type | table    | type  | possible_keys | key                                                  |
+----+-------------+----------+-------+---------------+------------------------------------------------------+
|  1 | SIMPLE      | users    | const | PRIMARY       | PRIMARY                                              |
|  1 | SIMPLE      | articles | ALL   | NULL          | NULL                                                 |
+----+-------------+----------+-------+---------------+------------------------------------------------------+
+---------+---------+-------+------+-------------+
| key_len | ref     | rows  | Extra |             |
+---------+---------+-------+------+-------------+
| 4       | const   |     1 |      |
| NULL    | NULL    |     1 | Using where |
+---------+---------+-------+------+-------------+
```

--------------------------------

### Create a New Rails App with Git and PostgreSQL (Shell)

Source: https://guides.rubyonrails.org/v4.2/command_line

This command sequence shows how to create a new Rails application, specifying Git for source code management and PostgreSQL as the database. It includes directory creation, Git initialization, and the `rails new` command with options.

```shell
mkdir gitapp
cd gitapp
git init
rails new . --git --database=postgresql
```

--------------------------------

### Set Application Root Route in Rails

Source: https://guides.rubyonrails.org/v4.0/getting_started

This snippet shows how to uncomment and modify the `root` route in `config/routes.rb` to direct requests to the application's root URL to a specific controller action. This is essential for defining your application's home page.

```ruby
Blog::Application.routes.draw do
  get "welcome/index"
  # The priority is based upon order of creation:
  # first created -> highest priority.
  # ...
  # You can have the root of your site routed with "root"
  root to: "welcome#index"
end
```

--------------------------------

### Starting the Rails Development Server

Source: https://guides.rubyonrails.org/asset_pipeline

This command starts the Ruby on Rails development server. It allows you to preview your application in a web browser and observe how assets are served, particularly in development mode where caching is bypassed.

```shell
$ bin/rails server
```

--------------------------------

### Install Ruby on macOS using Mise

Source: https://guides.rubyonrails.org/install_ruby_on_rails

Installs Xcode Command Line Tools, Homebrew with necessary dependencies, Mise version manager, and Ruby globally on macOS. Requires macOS Catalina 10.15 or newer.

```shell
# Install Xcode Command Line Tools
$ xcode-select --install

# Install Homebrew and dependencies
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
$ echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zshrc
$ source ~/.zshrc
$ brew install openssl@3 libyaml gmp rust

# Install Mise version manager
$ curl https://mise.run | sh
$ echo 'eval "$(~/.local/bin/mise activate)"' >> ~/.zshrc
$ source ~/.zshrc

# Install Ruby globally with Mise
$ mise use -g ruby@3

```

--------------------------------

### Ruby on Rails Coding Conventions

Source: https://guides.rubyonrails.org/v3.1/contributing_to_ruby_on_rails

A list of coding style conventions followed by the Ruby on Rails project. Adhering to these ensures consistency and readability.

```text
Two spaces, no tabs.
No trailing whitespace. Blank lines should not have any space.
Indent after private/protected.
Prefer &&/|| over and/or.
Prefer class << self block over self.method for class methods.
MyClass.my_method(my_arg) not my_method( my_arg ) or my_method my_arg.
a = b and not a=b.
```

--------------------------------

### Full-Text Search Setup in Rails (PostgreSQL)

Source: https://guides.rubyonrails.org/v7.1/active_record_postgresql

Provides code examples for setting up full-text search using PostgreSQL's `to_tsvector` and `to_tsquery` functions within a Rails application. It covers both immediate index creation and storing generated vectors as virtual columns.

```ruby
# db/migrate/20131220144913_create_documents.rb
create_table :documents do |t|
  t.string :title
  t.string :body
end

add_index :documents, "to_tsvector('english', title || ' ' || body)", using: :gin, name: 'documents_idx'
```

```ruby
# app/models/document.rb
class Document < ApplicationRecord
end
```

```ruby
# Usage
Document.create(title: "Cats and Dogs", body: "are nice!")

## all documents matching 'cat & dog'
Document.where("to_tsvector('english', title || ' ' || body) @@ to_tsquery(?)",
                 "cat & dog")
```

```ruby
# db/migrate/20131220144913_create_documents.rb
create_table :documents do |t|
  t.string :title
  t.string :body

  t.virtual :textsearchable_index_col,
            type: :tsvector, as: "to_tsvector('english', title || ' ' || body)", stored: true
end

add_index :documents, :textsearchable_index_col, using: :gin, name: 'documents_idx'

# Usage
Document.create(title: "Cats and Dogs", body: "are nice!")

## all documents matching 'cat & dog'
Document.where("textsearchable_index_col @@ to_tsquery(?)", "cat & dog")
```

--------------------------------

### Verify Bun Installation

Source: https://guides.rubyonrails.org/v7.1/working_with_javascript_in_rails

This command checks if the Bun JavaScript runtime and bundler is correctly installed and accessible in your system's PATH. It prints the installed version of Bun.

```bash
bun --version
```

--------------------------------

### Rails Plugin Installation with Revision Control

Source: https://guides.rubyonrails.org/v4.2/2_2_release_notes

Shows how to install Rails plugins using git or subversion (svn) and specify a particular revision or commit hash.

```bash
# Install a plugin from a git repository at a specific revision
$ script/plugin install git://github.com/user/repo.git -r <commit_hash>

# Install a plugin from an svn repository at a specific revision
$ script/plugin install http://svn.example.com/repo/trunk -r <revision_number>
```

--------------------------------

### Rails Route Definitions

Source: https://guides.rubyonrails.org/v4.2/getting_started

This output displays the available routes defined in a Rails application, as generated by the `rake routes` command. It maps HTTP verbs and URI patterns to their corresponding controller actions, useful for understanding where form submissions will be directed.

```bash
$ bin/rake routes
       Prefix Verb      URI Pattern                  Controller#Action
     articles GET       /articles(.:format)          articles#index
              POST      /articles(.:format)          articles#create
  new_article GET       /articles/new(.:format)      articles#new
 edit_article GET      /articles/:id/edit(.:format) articles#edit
      article GET       /articles/:id(.:format)      articles#show
              PATCH     /articles/:id(.:format)      articles#update
              PUT       /articles/:id(.:format)      articles#update
              DELETE    /articles/:id(.:format)      articles#destroy
        root GET       /                            welcome#index
```

--------------------------------

### Create a New Post Form with form_for (Ruby on Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This snippet demonstrates the basic usage of the `form_for` helper to generate an HTML form for creating a new post. It includes fields for title and text, and a submit button. The form is configured to submit to the 'new' action by default.

```erb
<%= form_for :post do |f| %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
```

--------------------------------

### Ruby: Initialize Rails application and boot

Source: https://guides.rubyonrails.org/v4.1/initialization

This Ruby code represents the 'bin/rails' file in a Rails application. It sets the application path, requires the 'config/boot' script, and then loads the main Rails commands.

```ruby
#!/usr/bin/env ruby
APP_PATH = File.expand_path('../../config/application', __FILE__)
require_relative '../config/boot'
require 'rails/commands'
```

--------------------------------

### Create PostgreSQL Test Databases

Source: https://guides.rubyonrails.org/v3.1/contributing_to_ruby_on_rails

Navigates to the 'activerecord' directory and executes a rake task to build the necessary test databases for PostgreSQL, ensuring correct character set and collation.

```bash
$ cd activerecord
$ rake postgresql:build_databases
```

--------------------------------

### Initialize and Save a New Article Record (Rails Console)

Source: https://guides.rubyonrails.org/v6.1/getting_started

Demonstrates how to create a new `Article` object with specified attributes and then persist it to the database using the `save` method. The `save` method triggers an SQL INSERT statement.

```ruby
irb> article = Article.new(title: "Hello Rails", body: "I am on Rails!")
irb> article.save
```

--------------------------------

### Rack Server Start Method

Source: https://guides.rubyonrails.org/v3.2/initialization

The `start` method in `Rack::Server` handles initial server setup. It can enable warnings, modify the load path, require specific libraries, and enable debug mode with pretty-printing of application details if the 'debug' option is set.

```ruby
def start
  if options[:warn]
    $-w = true
  end
  if includes = options[:include]
    $LOAD_PATH.unshift(*includes)
  end
  if library = options[:require]
    require library
  end
  if options[:debug]
    $DEBUG = true
    require 'pp'
    p options[:server]
    pp wrapped_app
    pp app
  end
end
```

--------------------------------

### Install SQLite3 Development Files (Shell)

Source: https://guides.rubyonrails.org/v5.1/development_dependencies_install

Installs SQLite3 and its development files, required for the sqlite3 gem. Provides commands for macOS, Ubuntu, Fedora/CentOS, Arch Linux, and FreeBSD.

```shell
# macOS
$ brew install sqlite3

# Ubuntu
$ sudo apt-get install sqlite3 libsqlite3-dev

# Fedora/CentOS
$ sudo yum install sqlite3 sqlite3-devel

# Arch Linux
$ sudo pacman -S sqlite

# FreeBSD
# pkg install sqlite3
# Or compile the databases/sqlite3 port.
```

--------------------------------

### Install Rails Plugin from Git Repository

Source: https://guides.rubyonrails.org/v3.1/command_line

This command installs a Rails plugin from a specified Git repository URL. It fetches the plugin's code and integrates it into your application's plugin directory. Git must be installed locally.

```bash
$ rails plugin install https://github.com/technoweenie/acts_as_paranoid.git
+ ./CHANGELOG
+ ./MIT-LICENSE
...
```

--------------------------------

### Install Development Dependencies on Ubuntu

Source: https://guides.rubyonrails.org/v6.1/development_dependencies_install

Installs essential development tools and libraries on Ubuntu using the apt package manager. This includes databases (SQLite, MySQL, PostgreSQL), Redis, Memcached, ImageMagick, FFmpeg, muPDF, and Yarn.

```shell
sudo apt-get update
sudo apt-get install sqlite3 libsqlite3-dev mysql-server libmysqlclient-dev postgresql postgresql-client postgresql-contrib libpq-dev redis-server memcached imagemagick ffmpeg mupdf mupdf-tools libxml2-dev

# Install Yarn
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get install yarn
```

--------------------------------

### Rackup Configuration for Rails Application (Ruby)

Source: https://guides.rubyonrails.org/v3.0/rails_on_rack

Shows how to configure a Rails application to be served using `rackup` by defining a `config.ru` file. This file specifies required environment setup and lists the Rack middlewares to be used before running the Rails application.

```ruby
require "config/environment"
use Rails::Rack::LogTailer
use ActionDispatch::Static
run ActionController::Dispatcher.new
```

--------------------------------

### Start Rails Development Server with `rails server`

Source: https://guides.rubyonrails.org/v4.2/command_line

Launches the WEBrick web server to run the Rails application in the development environment. This command makes the application accessible through a web browser. It listens on `http://localhost:3000` by default.

```bash
$ cd commandsapp
$ bin/rails server
=> Booting WEBrick
=> Rails 4.2.0 application starting in development on http://localhost:3000
=> Call with -d to detach
=> Ctrl-C to shutdown server
[2013-08-07 02:00:01] INFO  WEBrick 1.3.1
[2013-08-07 02:00:01] INFO  ruby 2.0.0 (2013-06-27) [x86_64-darwin11.2.0]
[2013-08-07 02:00:01] INFO  WEBrick::HTTPServer#start: pid=69680 port=3000
```

--------------------------------

### Verify Node.js Installation

Source: https://guides.rubyonrails.org/v6.1/getting_started

Verifies that Node.js is installed and meets the minimum version requirement (greater than 8.16.0). Node.js is required for managing JavaScript assets in Rails applications.

```bash
$
node --version
```

--------------------------------

### Example CHANGELOG Entry Format

Source: https://guides.rubyonrails.org/v5.0/contributing_to_ruby_on_rails

This example demonstrates the standard format for adding an entry to the CHANGELOG file. It includes a summary of the change, optional multi-line descriptions, code examples, issue references, and the author's name.

```text
*  Summary of a change that briefly describes what was changed. You can use multiple
     lines and wrap them at around 80 characters. Code examples are ok, too, if needed:
         class Foo
           def bar
             puts 'baz'
           end
         end
     You can continue after the code example and you can attach issue number. GH#1234
    *Your Name*
```

--------------------------------

### Implement Basic HTTP Auth in Rails ArticlesController

Source: https://guides.rubyonrails.org/v4.1/getting_started

This code snippet demonstrates how to use `http_basic_authenticate_with` in a Rails controller to protect actions. It allows access to 'index' and 'show' actions without authentication, while requiring authentication for all other actions. This is useful for protecting administrative or sensitive content.

```ruby
class ArticlesController < ApplicationController
  http_basic_authenticate_with name: "dhh", password: "secret", except: [:index, :show]
  def index
    @articles = Article.all
  end
  # snipped for brevity
```

--------------------------------

### Ruby on Rails Model Object Initialization Example

Source: https://guides.rubyonrails.org/v7.1/form_helpers

Shows how to initialize a model object in Ruby on Rails for use with form builders. This example demonstrates finding an existing record and its attributes.

```ruby
@article = Article.find(42)
# => #<Article id: 42, title: "My Title", body: "My Body">
```

--------------------------------

### Build MySQL Test Databases

Source: https://guides.rubyonrails.org/v4.0/development_dependencies_install

Navigates to the 'activerecord' directory and then uses the 'bundle exec rake mysql:build_databases' command to create the necessary test databases for MySQL.

```bash
$ cd activerecord
$ bundle exec rake mysql:build_databases
```

--------------------------------

### Running Rails Notes Command

Source: https://guides.rubyonrails.org/v7.0/command_line

This is an example output of the `bin/rails notes` command, which lists annotations found in the project's code. It shows file paths and the annotations within them.

```shell
$ bin/rails notes
app/controllers/admin/users_controller.rb:
  * [ 20] [TODO] any other way to do this?
  * [132] [FIXME] high priority for next deploy

lib/school.rb:
  * [ 13] [OPTIMIZE] Refactor this code to make it faster
  * [ 17] [FIXME] 

spec/models/user_spec.rb:
  * [122] [TODO] Verify the user that has a subscription works

vendor/tools.rb:
  * [ 56] [TODO] Get rid of this dependency

```

--------------------------------

### Active Storage: Permit Featured Image Parameter (Ruby)

Source: https://guides.rubyonrails.org/getting_started

This Ruby code snippet shows how to permit the 'featured_image' parameter within the product controller's strong parameters. This is crucial for allowing file uploads to be processed correctly by the controller.

```ruby
# Only allow a list of trusted parameters through.
def product_params
  params.expect(product: [ :name, :description, :featured_image ])
end
```

--------------------------------

### Rails 3 Application Namespace and Booting

Source: https://guides.rubyonrails.org/v5.2/3_0_release_notes

Illustrates how Rails 3 applications now have their own namespace, allowing for easier interaction with other applications. The example shows the syntax for booting an application.

```ruby
# Example: Booting an application
YourAppName.boot
```

--------------------------------

### Ruby: Post has_many Comments Association and Validation

Source: https://guides.rubyonrails.org/v4.0/getting_started

Defines a has_many association in the Post model, indicating that a post can have multiple comments. It also includes a presence validation for the post's title with a minimum length of 5 characters.

```ruby
class Post < ActiveRecord::Base
  has_many :comments
  validates :title, presence: true,
                    length: { minimum: 5 }
  [...]
end
```

--------------------------------

### Setup Testing Database for Rails Plugin

Source: https://guides.rubyonrails.org/plugins

Navigates to the dummy Rails application within the plugin and creates its testing database using the `db:create` Rake task. This prepares the environment for running integration tests for the plugin.

```bash
$ cd test/dummy
$ bin/rails db:create

```

--------------------------------

### Get Beginning and End of Day Timestamps in Ruby

Source: https://guides.rubyonrails.org/v5.0/active_support_core_extensions

The `beginning_of_day` and `end_of_day` methods return `Time` or `DateTime` objects representing the start (00:00:00) and end (23:59:59) of a given day, respectively. These are useful for timestamp-based operations and logging.

```ruby
date = Date.new(2010, 6, 7)
puts date.beginning_of_day
puts date.end_of_day
```

--------------------------------

### Ruby on Rails: Controller Actions for New and Create Article

Source: https://guides.rubyonrails.org/v6.1/getting_started

Implements the `new` and `create` actions in a Rails controller to handle article creation. The `new` action initializes a new article instance, while `create` attempts to save it and redirects on success or re-renders the form on failure. It uses `Article.new` and `@article.save`.

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def create
    @article = Article.new(title: "...", body: "...")

    if @article.save
      redirect_to @article
    else
      render :new
    end
  end
end
```

--------------------------------

### Install Memcached (Fedora/CentOS)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs Memcached on Fedora or CentOS using yum, a caching system used for some Rails tests.

```bash
$ sudo yum install memcached
```

--------------------------------

### Order Records by Name in Ruby on Rails

Source: https://guides.rubyonrails.org/getting_started

Sort database records alphabetically using the `order` method. Pass a hash with the column name and the desired order (e.g., `:asc` for ascending). This generates a SQL `SELECT` query with an `ORDER BY` clause.

```ruby
store(dev)> Product.order(name: :asc)
  Product Load (0.3ms)  SELECT "products".* FROM "products" /* loading for pp */ ORDER BY "products"."name" ASC LIMIT 11 /*application='Store'*/
=> [#<Product:0x0000000120e02a88 id: 2, name: "Pants", created_at: "2024-11-09 16:36:01.856751000 +0000", updated_at: "2024-11-09 16:36:01.856751000 +0000">
 #<Product:0x0000000120e02948 id: 1, name: "T-Shirt", created_at: "2024-11-09 16:35:01.117836000 +0000", updated_at: "2024-11-09 16:35:01.117836000 +0000">]
```

--------------------------------

### Create 'index' view for listing articles in Rails

Source: https://guides.rubyonrails.org/v6.0/getting_started

Defines the ERB view for the 'index' action in Rails, which lists all articles. It creates an HTML table to display the title and text of each article, along with a 'Show' link for each item using `link_to` and `article_path`. The view iterates over the `@articles` instance variable.

```html
<h1>Listing Articles</h1>
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th></th>
  </tr>
  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
      <td><%= link_to 'Show', article_path(article) %></td>
    </tr>
  <% end %>
</table>
```

--------------------------------

### List Available Rails Database Commands

Source: https://guides.rubyonrails.org/v7.1/active_record_multiple_databases

This shell command lists all available database-related tasks provided by Rails. Running `bin/rails -T` shows commands for database creation, migration, setup, and more, which are essential for managing multiple databases.

```bash
$ bin/rails -T
bin/rails db:create                          # Create the database from DATABASE_URL or config/database.yml for the ...

```

--------------------------------

### Install Ruby Gems with Bundler

Source: https://guides.rubyonrails.org/v6.1/development_dependencies_install

Installs all the Ruby gems specified in the project's Gemfile. The `--without db` option can be used to skip database-related gems, often for running tests.

```bash
bundle install
bundle install --without db
```

--------------------------------

### Rails Controller: Handling Post Creation with Validation

Source: https://guides.rubyonrails.org/v4.0/getting_started

This Ruby code demonstrates how to handle the creation of a new post in a Rails controller. It includes logic to create a new post object, attempt to save it, and then either redirect to the post's page on success or re-render the 'new' form with validation errors on failure. It permits strong parameters for the post attributes.

```ruby
def new
  @post = Post.new
end

def create
  @post = Post.new(params[:post].permit(:title, :text))
  if @post.save
    redirect_to @post
  else
    render 'new'
  end
end
```

--------------------------------

### Rack Configuration File Content

Source: https://guides.rubyonrails.org/v4.0/initialization

This is a typical content of a `config.ru` file used by Rack-based servers to start a Ruby on Rails application. It first requires the Rails environment and then uses the `run` command to specify the main application constant.

```ruby
# This file is used by Rack-based servers to start the application.
require ::File.expand_path('../config/environment', __FILE__)
run <%= app_const %>
```

--------------------------------

### Rails View Code Example

Source: https://guides.rubyonrails.org/command_line

Example of a Rails view file corresponding to the 'hello' action. This ERB template displays a heading and renders the `@message` instance variable set in the controller.

```erb
<h1>A Greeting for You!</h1>
<p><%= @message %></p>

```

--------------------------------

### Markdown for Link Formatting Examples

Source: https://guides.rubyonrails.org/ruby_on_rails_guides_guidelines

Provides examples of incorrect ('BAD') and correct ('GOOD') Markdown syntax for creating descriptive links, emphasizing the importance of clear link text for both external and internal references.

```markdown
# BAD
See the Rails Internationalization (I18n) API documentation for [more
details](i18n.html).

# GOOD
See the [Rails Internationalization (I18n) API documentation](i18n.html) for
more details.
```

```markdown
# BAD
We will cover this [below](#multiple-callback-conditions).

# GOOD
We will cover this in the [multiple callback conditions
section](#multiple-callback-conditions) shown below.
```

--------------------------------

### Rails Script Server and Plugin Installation

Source: https://guides.rubyonrails.org/v4.0/2_2_release_notes

Shows how to use the `script/server` command with direct Thin web server support and the updated `script/plugin install` command that supports both Git and SVN repositories. These commands streamline application serving and plugin management.

```shell
# Start server with Thin
# script/server thin

# Install a git-based plugin
# script/plugin install git://github.com/user/repo.git

# Install an svn-based plugin
# script/plugin install http://svn.example.com/repo/trunk
```

--------------------------------

### Generate HTML Rails Guides

Source: https://guides.rubyonrails.org/contributing_to_ruby_on_rails

This command generates the Rails guides in HTML format for a specified language. It requires installing dependencies and executing a rake task within the guides directory. Note that the Redcarpet Gem is not compatible with JRuby.

```bash
$ BUNDLE_ONLY=default:doc bundle install
$ cd guides/
$ BUNDLE_ONLY=default:doc bundle exec rake guides:generate:html GUIDES_LANGUAGE=it-IT

```

--------------------------------

### Allow Unauthenticated Access in Rails Controller

Source: https://guides.rubyonrails.org/getting_started

This Ruby code configures the `ProductsController` to allow unauthenticated users to access the `index` and `show` actions. The `allow_unauthenticated_access` method, likely provided by an authentication gem, specifies which controller actions are publicly accessible.

```ruby
class ProductsController < ApplicationController
  allow_unauthenticated_access only: %i[ index show ]
  # ...
end
```

--------------------------------

### Ruby on Rails Database Migration for Creating Articles Table

Source: https://guides.rubyonrails.org/v7.2/getting_started

Defines a database migration to create the 'articles' table. It includes 'title' (string) and 'body' (text) columns, along with 'created_at' and 'updated_at' timestamps managed by Rails.

```ruby
class CreateArticles < ActiveRecord::Migration[7.2]
  def change
    create_table :articles do |t|
      t.string :title
      t.text :body

      t.timestamps
    end
  end
end
```

--------------------------------

### Generate HTML Rails Guides (Ruby)

Source: https://guides.rubyonrails.org/v7.2/contributing_to_ruby_on_rails

This Ruby command generates HTML versions of the Rails guides for a specified language. It requires installing guide dependencies and navigating to the guides directory. The Redcarpet Gem is not compatible with JRuby.

```shell
# only install gems necessary for the guides. To undo run: bundle config --delete without
$ bundle install --without job cable storage test db
$ cd guides/
$ bundle exec rake guides:generate:html GUIDES_LANGUAGE=it-IT
```

--------------------------------

### Build MySQL Test Databases with Rake

Source: https://guides.rubyonrails.org/v4.2/development_dependencies_install

Builds the necessary test databases for MySQL using a Rake task within the 'activerecord' directory. This command ensures that the databases are created with the correct configurations for testing.

```bash
$ cd activerecord
$ bundle exec rake db:mysql:build
```

--------------------------------

### Ruby: Execute bin/rails script

Source: https://guides.rubyonrails.org/v6.1/initialization

The `bin/rails` script is the entry point for running Rails commands. It sets the `APP_PATH` constant, requires `config/boot.rb` to set up Bundler and dependencies, and then requires `rails/commands` to handle command execution.

```ruby
#!/usr/bin/env ruby
APP_PATH = File.expand_path('../config/application', __dir__)
require_relative "../config/boot"
require "rails/commands"

```

--------------------------------

### Rails database.yml Configuration Example (YAML)

Source: https://guides.rubyonrails.org/v4.1/configuring

An example of the config/database.yml file structure for specifying database connection details for different Rails environments. It shows the adapter, database name, and connection pool size.

```yaml
development:
  adapter: postgresql
  database: blog_development
  pool: 5
```

--------------------------------

### Client-Server: Create Consumer and Subscribe to Appearance Channel (JavaScript)

Source: https://guides.rubyonrails.org/v6.0/action_cable_overview

Establishes a WebSocket connection to the Action Cable server and subscribes to the 'AppearanceChannel'. This is the initial setup for real-time client-server communication for appearance updates.

```javascript
App.cable = ActionCable.createConsumer("ws://cable.example.com")
consumer.subscriptions.create({ channel: "AppearanceChannel" })
```

--------------------------------

### Track User Appearances with Ruby on Rails and JavaScript

Source: https://guides.rubyonrails.org/v6.0/action_cable_overview

This example shows how to implement a user appearance tracking system using Action Cable. The Ruby code defines methods to mark users as appeared or disappeared, which can be backed by Redis or a database. The JavaScript code subscribes to the AppearanceChannel, handles connection events, and sends appear/away actions based on document activity.

```ruby
class AppearanceChannel < ApplicationCable::Channel
  def subscribed
    current_user.appear
  end

  def unsubscribed
    current_user.disappear
  end

  def appear(data)
    current_user.appear(on: data['appearing_on'])
  end

  def away
    current_user.away
  end
end
```

```javascript
import consumer from "./consumer"

consumer.subscriptions.create("AppearanceChannel", {
  // Called once when the subscription is created.
  initialized() {
    this.update = this.update.bind(this)
  },
  // Called when the subscription is ready for use on the server.
  connected() {
    this.install()
    this.update()
  },
  // Called when the WebSocket connection is closed.
  disconnected() {
    this.uninstall()
  },
  // Called when the subscription is rejected by the server.
  rejected() {
    this.uninstall()
  },
  update() {
    this.documentIsActive ? this.appear() : this.away()
  },
  appear() {
    // Calls `AppearanceChannel#appear(data)` on the server.
    this.perform("appear", { appearing_on: this.appearingOn })
  },
  away() {
    // Calls `AppearanceChannel#away` on the server.
    this.perform("away")
  },
  install() {
    window.addEventListener("focus", this.update)
    window.addEventListener("blur", this.update)
    document.addEventListener("turbolinks:load", this.update)
    document.addEventListener("visibilitychange", this.update)
  },
  uninstall() {
    window.removeEventListener("focus", this.update)
    window.removeEventListener("blur", this.update)
    document.removeEventListener("turbolinks:load", this.update)
    document.removeEventListener("visibilitychange", this.update)
  },
  get documentIsActive() {
    return document.visibilityState == "visible" && document.hasFocus()
  },
  get appearingOn() {
    const element = document.querySelector("[data-appearing-on]")
    return element ? element.getAttribute("data-appearing-on") : null
  }
})
```

--------------------------------

### Require Rails Core and Frameworks (Ruby)

Source: https://guides.rubyonrails.org/v5.2/initialization

This snippet demonstrates the loading of the main Rails application and its individual frameworks. It ensures that all necessary components like ActiveRecord, ActionController, and others are made available to the application. Error handling for missing railtie files is included.

```ruby
require "rails/all"
%w(active_record/railtie action_controller/railtie action_view/railtie action_mailer/railtie active_job/railtie action_cable/engine active_storage/engine rails/test_unit/railtie sprockets/railtie).each do |railtie|
  begin
    require railtie
  rescue LoadError
  end
end
```

--------------------------------

### Ruby on Rails Manifest File Example

Source: https://guides.rubyonrails.org/v6.1/asset_pipeline

Example of an application.js manifest file and the resulting HTML output in development mode. The `body` parameter is required by Sprockets.

```javascript
//= require core
//= require projects
//= require tickets

```

```html
<script src="/assets/core.js?body=1"></script>
<script src="/assets/projects.js?body=1"></script>
<script src="/assets/tickets.js?body=1"></script>

```

--------------------------------

### Start Solid Queue Jobs (Bash)

Source: https://guides.rubyonrails.org/active_job_basics

Command to start the Solid Queue job processor. This command initiates the system to begin picking up and processing jobs from the queue.

```bash
bin/jobs start
```

--------------------------------

### Rails Controller Test Setup and Teardown

Source: https://guides.rubyonrails.org/v3.0/testing

Demonstrates how to use `setup` and `teardown` callbacks in Rails controller tests. The `setup` method is called before each test to initialize instance variables, and `teardown` is called after each test, often used for cleanup. This ensures a clean state for every test.

```ruby
require 'test_helper'

class PostsControllerTest < ActionController::TestCase
  # called before every single test
  def setup
    @post = posts(:one)
  end

  # called after every single test
  def teardown
    # as we are re-initializing @post before every test
    # setting it to nil here is not essential but I hope
    # you understand how you can use the teardown method
    @post = nil
  end

  test "should show post" do
    get :show, id: @post.id
    assert_response :success
  end

  test "should destroy post" do
    assert_difference('Post.count', -1) do
      delete :destroy, id: @post.id
    end
    assert_redirected_to posts_path
  end
end
```

--------------------------------

### Install FreeBSD Packages for Rails

Source: https://guides.rubyonrails.org/v7.0/development_dependencies_install

Installs common packages required for Ruby on Rails development on FreeBSD, including database clients, image manipulation tools, and JavaScript package managers. It also suggests using portmaster for Redis.

```bash
$ pkg install sqlite3 mysql80-client mysql80-server postgresql11-client postgresql11-server memcached imagemagick ffmpeg mupdf yarn libxml2
# portmaster databases/redis
```

--------------------------------

### Install Development Libraries for Nokogiri (Ubuntu)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs the libxml2 and libxslt libraries along with their development files on Ubuntu, which are necessary for the Nokogiri gem used in Rails development.

```bash
$ sudo apt-get install libxml2 libxml2-dev libxslt1-dev
```

--------------------------------

### Define Article Model with Validations (Ruby)

Source: https://guides.rubyonrails.org/v4.1/getting_started

This Ruby code defines the Article model, inheriting from ActiveRecord::Base. It includes validations to ensure the 'title' attribute is present and has a minimum length of 5 characters. This is a core part of data integrity in Rails applications.

```ruby
class Article < ActiveRecord::Base
  validates :title, presence: true,
                    length: { minimum: 5 }
end
```

--------------------------------

### Configure form_with Submission URL (Rails)

Source: https://guides.rubyonrails.org/v6.0/getting_started

This snippet shows how to configure the submission URL for a form created with `form_with`. By passing `url: articles_path`, the form will submit to the route defined by the `articles_path` helper, which typically maps to the `create` action in the `ArticlesController` using a POST request.

```erb
<%= form_with scope: :article, url: articles_path, local: true do |form| %>
  <p>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </p>
  <p>
    <%= form.label :text %><br>
    <%= form.text_area :text %>
  </p>
  <p>
    <%= form.submit %>
  </p>
<% end %>
```

--------------------------------

### Rails Fingerprinting Example

Source: https://guides.rubyonrails.org/v3.1/asset_pipeline

Demonstrates how Rails uses fingerprinting to create unique filenames for static assets, incorporating a hash of the content for effective cache busting. This ensures that updated content gets new URLs, forcing caches to retrieve the latest version.

```html
global-908e25f4bf641868d8683022a5b62f54.css
```

--------------------------------

### Install Action Text Rails Generator

Source: https://guides.rubyonrails.org/v7.2/action_text_overview

This command installs Action Text, including Trix editor JavaScript, Active Storage for attachments, database migrations, and necessary CSS and view partials.

```bash
bin/rails action_text:install
```

--------------------------------

### Markdown Title Formatting Examples

Source: https://guides.rubyonrails.org/v4.0/ruby_on_rails_guides_guidelines

These examples illustrate the Markdown syntax for different heading levels (h1, h2, h3, etc.) as used in Ruby on Rails Guides. It also shows specific conventions for capitalizing titles and using inline code formatting.

```Markdown
`Guide Title`
===========

```

```Markdown
`Section`
-------

```

```Markdown
### Sub Section

```

```Markdown
#### Middleware Stack is an Array

```

```Markdown
#### When are Objects Saved?

```

```Markdown
##### The `:content_type` Option

```

--------------------------------

### Configuring Rails Application with rackup

Source: https://guides.rubyonrails.org/v6.1/rails_on_rack

Shows how to configure a Rails application to be served using `rackup` by creating a `config.ru` file. This file requires the Rails environment and then runs the `Rails.application` object.

```ruby
# Rails.root/config.ru
require_relative "config/environment"
run Rails.application
```

--------------------------------

### Install Action Text - Shell

Source: https://guides.rubyonrails.org/v6.0/action_text_overview

This command installs Action Text by adding the necessary Yarn package and generating migration files. It's the first step in integrating Action Text into your Rails application.

```bash
rails action_text:install
```

--------------------------------

### Generate Basic Rails Application

Source: https://guides.rubyonrails.org/v3.0/plugins

This command installs the Rails gem, creates a new Rails application named 'yaffle_guide', generates a scaffold for a 'bird' resource with a 'name' string attribute, migrates the database, and starts the Rails server. It's a prerequisite for developing Rails plugins.

```bash
gem install rails
rails new yaffle_guide
cd yaffle_guide
rails generate scaffold bird name:string
rake db:migrate
rails server
```

--------------------------------

### Install Development Libraries for Nokogiri (Fedora/CentOS)

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Installs the libxml2 and libxslt libraries along with their development files on Fedora or CentOS systems, required for the Nokogiri gem.

```bash
$ sudo yum install libxml2 libxml2-devel libxslt libxslt-devel
```

--------------------------------

### Generate HTML Rails Guides in a Specific Language

Source: https://guides.rubyonrails.org/v5.2/contributing_to_ruby_on_rails

This command generates HTML versions of the Rails guides for a specified language. It requires installing bundle dependencies and then executing a rake task with the language code. The output is placed in an 'output' directory.

```ruby
bundle install
bundle exec rake guides:generate:html GUIDES_LANGUAGE=it-IT
```

--------------------------------

### Render reusable form partial in edit post view (ERB)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This ERB code updates the 'edit post' view to incorporate the '_form.html.erb' partial. This refactoring consolidates the form's HTML structure into a single partial, making the edit view cleaner and promoting code reuse between the new and edit post functionalities.

```erb
<h1>Edit post</h1>
<%= render 'form' %>
<%= link_to 'Back', posts_path %>
```

--------------------------------

### Defining RESTful Resources

Source: https://guides.rubyonrails.org/v4.2/getting_started

This section details how to use the `resources` method in `config/routes.rb` to automatically generate routes for standard RESTful CRUD (Create, Read, Update, Delete) operations for a given resource. It also shows how to view the generated routes using `bin/rake routes`.

```APIDOC
## Resource Routes

### Description
Defines a set of standard RESTful routes for a given resource, enabling CRUD operations.

### Method
Various (GET, POST, PATCH, PUT, DELETE)

### Endpoint
- `/articles` (for index and create)
- `/articles/new` (for new)
- `/articles/:id/edit` (for edit)
- `/articles/:id` (for show, update, destroy)

### Parameters
#### Path Parameters
- **id** (integer) - Required - The unique identifier for an article.

#### Query Parameters
None

#### Request Body
- **article** (object) - Required - Contains the data for creating or updating an article.
  - **title** (string) - Optional - The title of the article.
  - **body** (text) - Optional - The content of the article.

### Request Example
```json
{
  "article": {
    "title": "My First Article",
    "body": "This is the content of my first article."
  }
}
```

### Response
#### Success Response (200/201)
- **id** (integer) - The unique identifier of the article.
- **title** (string) - The title of the article.
- **body** (text) - The content of the article.

#### Response Example
```json
{
  "id": 1,
  "title": "My First Article",
  "body": "This is the content of my first article."
}
```
```

--------------------------------

### Install macOS Dependencies with Homebrew

Source: https://guides.rubyonrails.org/development_dependencies_install

Installs all required development dependencies on macOS using Homebrew. This command assumes Homebrew is already installed. It also shows how to list and start services.

```bash
$ brew bundle
$ brew services list
$ brew services start mysql
```

--------------------------------

### Generating HTML Rails Guides in a Specific Language

Source: https://guides.rubyonrails.org/v7.1/contributing_to_ruby_on_rails

This command shows how to generate HTML versions of the Rails guides for a specific language (e.g., Italian). It requires installing necessary gems, navigating to the guides directory, and then executing a rake task with the language code. Ensure that you do not translate the HTML files directly as they are auto-generated.

```bash
# only install gems necessary for the guides. To undo run: bundle config --delete without
$ bundle install --without job cable storage ujs test db
$ cd guides/
$ bundle exec rake guides:generate:html GUIDES_LANGUAGE=it-IT
```

--------------------------------

### Start the Rails Development Server

Source: https://guides.rubyonrails.org/v4.0/command_line

The `rails server` command starts the WEBrick web server, allowing you to access your Rails application through a web browser. You can specify the environment and port, or run it as a daemon. The alias `rails s` can also be used.

```shell
$ cd commandsapp
$ rails server
=> Booting WEBrick
=> Rails 4.0.0 application starting in development on http://0.0.0.0:3000
=> Call with -d to detach
=> Ctrl-C to shutdown server
[2012-05-28 00:39:41] INFO  WEBrick 1.3.1
[2012-05-28 00:39:41] INFO  ruby 1.9.2 (2011-02-18) [x86_64-darwin11.2.0]
[2012-05-28 00:39:41] INFO  WEBrick::HTTPServer#start: pid=69680 port=3000
```

```shell
$ rails server -e production -p 4000
```

```shell
$ rails server -d
```

--------------------------------

### Configure Form Submission URL with posts_path (Ruby on Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This snippet modifies the `form_for` helper to specify the submission URL using the `posts_path` helper. This directs the form data to the 'create' action of the PostsController, typically handling the creation of a new post record.

```erb
<%= form_for :post, url: posts_path do |f| %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
```

--------------------------------

### Active Storage: Display Featured Image in Show View (ERB)

Source: https://guides.rubyonrails.org/getting_started

This ERB snippet demonstrates how to conditionally display an attached 'featured_image' for a product on its show page. It uses an `if` condition to check if the image is attached before rendering it using `image_tag`.

```erb
<%= image_tag @product.featured_image if @product.featured_image.attached? %>
```

--------------------------------

### Install SQLite3 Dependencies on Ubuntu

Source: https://guides.rubyonrails.org/v3.2/contributing_to_ruby_on_rails

Installs SQLite3 and its development files, required for the 'sqlite3-ruby' gem. This command is specific to Ubuntu-based systems.

```shell
sudo apt-get install sqlite3 libsqlite3-dev
```

--------------------------------

### Destroy Link in Post Index View (Ruby on Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

Adds a 'Destroy' link to the posts index view, utilizing the `link_to` helper with the `:delete` method and a data-confirm option for user confirmation. This leverages `jquery_ujs` for client-side confirmation before submission.

```erb
<h1>Listing Posts</h1>
<%= link_to 'New post', new_post_path %>
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th></th>
    <th></th>
    <th></th>
  </tr>
<% @posts.each do |post| %>
  <tr>
    <td><%= post.title %></td>
    <td><%= post.text %></td>
    <td><%= link_to 'Show', post_path(post) %></td>
    <td><%= link_to 'Edit', edit_post_path(post) %></td>
    <td><%= link_to 'Destroy', post_path(post),
                    method: :delete, data: { confirm: 'Are you sure?' } %></td>
  </tr>
<% end %>
</table>
```

--------------------------------

### Example Commit Message - Plain Text

Source: https://guides.rubyonrails.org/v3.2/contributing_to_ruby_on_rails

Demonstrates the recommended format for Git commit messages. It includes a concise summary line and a more detailed description, with support for multiline content and indented code examples.

```plaintext
Short summary (ideally 50 characters or less)

More detailed description, if necessary. It should be wrapped to 72
characters. Try to be as descriptive as you can, even if you think that
the commit content is obvious, it may not be obvious to others. You
should add such description also if it's already present in bug tracker,
it should not be necessary to visit a webpage to check the history.

Description can have multiple paragraps and you can use code examples
inside, just indent it with 4 spaces:

    class PostsController
      def index
        respond_with Post.limit(10)
      end
    end

You can also add bullet points:
- you can use dashes or asterisks
- also, try to indent next line of a point for readability, if it's too
  long to fit in 72 characters
```

--------------------------------

### Show Article Action in Rails Controller

Source: https://guides.rubyonrails.org/v4.1/getting_started

Defines the 'show' action in the ArticlesController to retrieve a single article by its ID from the request parameters. It makes the found article available to the view via an instance variable. Assumes an 'Article' model exists and the route expects an ':id' parameter.

```ruby
def show
  @article = Article.find(params[:id])
end
```

--------------------------------

### script/plugin Install with Git Revision (Shell)

Source: https://guides.rubyonrails.org/v3.0/2_2_release_notes

The `script/plugin install` command now supports specifying a revision (`-r`) for Git-based plugins, in addition to SVN. This allows for precise version control of installed plugins.

```shell
# Installing a git-based plugin with a specific revision:
script/plugin install my_plugin -r abcdef12345
```

--------------------------------

### Example Rails Middleware Stack Output

Source: https://guides.rubyonrails.org/v5.0/rails_on_rack

Illustrates a typical output when inspecting the middleware stack of a Rails application. It lists various Rack and Action Dispatch middlewares in their execution order.

```shell
use Rack::Sendfile
use ActionDispatch::Static
use ActionDispatch::Executor
use #<ActiveSupport::Cache::Strategy::LocalCache::Middleware:0x000000029a0838>
use Rack::Runtime
use Rack::MethodOverride
use ActionDispatch::RequestId
use Rails::Rack::Logger
use ActionDispatch::ShowExceptions
use ActionDispatch::DebugExceptions
use ActionDispatch::RemoteIp
use ActionDispatch::Reloader
use ActionDispatch::Callbacks
use ActiveRecord::Migration::CheckPending
use ActiveRecord::ConnectionAdapters::ConnectionManagement
use ActiveRecord::QueryCache
use ActionDispatch::Cookies
use ActionDispatch::Session::CookieStore
use ActionDispatch::Flash
use Rack::Head
use Rack::ConditionalGet
use Rack::ETag
run Rails.application.routes
```

--------------------------------

### Enable Polymorphic Association in Rails belongs_to

Source: https://guides.rubyonrails.org/v6.0/association_basics

Setting the `:polymorphic` option to `true` indicates that this is a polymorphic association. Polymorphic associations allow a model to belong to multiple different types of models. This example shows the basic setup for a polymorphic belongs_to.

```ruby
class Comment < ApplicationRecord
  belongs_to :commentable, polymorphic: true
end
```

--------------------------------

### Generating HTML Rails Guides in a Specific Language

Source: https://guides.rubyonrails.org/v5.0/contributing_to_ruby_on_rails

This command generates HTML versions of the Rails guides for a specified language. It requires RubyGems and Bundler to be installed and assumes you are in the '_guides' directory.

```bash
$ bundle install
$ bundle exec rake guides:generate:html GUIDES_LANGUAGE=it-IT
```

--------------------------------

### Ruby: Setup and Teardown Callbacks in Rails Tests

Source: https://guides.rubyonrails.org/v4.0/testing

Demonstrates the use of `setup` and `teardown` callbacks within Rails controller tests. These methods are executed before and after each test, respectively, to prepare the test environment or clean up resources. The example shows initializing an instance variable in `setup` and clearing it in `teardown`.

```ruby
require 'test_helper'
class PostsControllerTest < ActionController::TestCase
  # called before every single test
  def setup
    @post = posts(:one)
  end

  # called after every single test
  def teardown
    # as we are re-initializing @post before every test
    # setting it to nil here is not essential but I hope
    # you understand how you can use the teardown method
    @post = nil
  end

  test "should show post"
    get :show, id: @post.id
    assert_response :success
  end

  test "should destroy post"
    assert_difference('Post.count', -1) do
      delete :destroy, id: @post.id
    end
    assert_redirected_to posts_path
  end
end
```

--------------------------------

### Install Memcached for Various Operating Systems

Source: https://guides.rubyonrails.org/v5.0/development_dependencies_install

Installs Memcached, a distributed memory caching system, required for tests that use memcached. Installation commands are provided for OS X (Homebrew), Ubuntu, Fedora/CentOS, Arch Linux, and FreeBSD.

```bash
# OS X
$ brew install memcached

# Ubuntu
$ sudo apt-get install memcached

# Fedora or CentOS
$ sudo yum install memcached

# Arch Linux
$ sudo pacman -S memcached

# FreeBSD
# pkg install memcached
# Alternatively, compile the databases/memcached port.
```

--------------------------------

### Show Article Action in Rails Controller

Source: https://guides.rubyonrails.org/v4.2/getting_started

Defines the 'show' action within the ArticlesController to find and display a single article based on its ID. It uses the Article.find method with a parameter from the request and makes the article instance available to the view.

```ruby
class ArticlesController < ApplicationController
  def show
    @article = Article.find(params[:id])
  end
  
  def new
  end
  
  # snippet for brevity
```

--------------------------------

### Ruby: STI Query Example with Subclass Constraint

Source: https://guides.rubyonrails.org/v4.2/autoloading_and_reloading_constants

Demonstrates how Active Record adds a type constraint to SQL queries when querying a subclass in a Single Table Inheritance (STI) setup. This ensures that only records of the specified subclass (and its descendants) are retrieved.

```ruby
Rectangle.all
# SELECT "polygons".* FROM "polygons" WHERE "polygons"."type" IN ('Rectangle')
```

--------------------------------

### Example CHANGELOG Entry - Ruby

Source: https://guides.rubyonrails.org/v3.2/contributing_to_ruby_on_rails

Illustrates the structure and content of a CHANGELOG entry for Ruby on Rails. Includes a summary, optional multiline descriptions, code examples, and issue references. It should end with the author's name.

```plaintext
*  Summary of a change that briefly describes what was changed. You can use multiple
     lines and wrap them at around 80 characters. Code examples are ok, too, if needed:
          class Foo
            def bar
              puts 'baz'
            end
          end
     You can continue after the code example and you can attach issue number. GH#1234
* Your Name *
```

--------------------------------

### Start the Rails Development Server

Source: https://guides.rubyonrails.org/v5.1/command_line

The `rails server` command starts the Puma web server, which is bundled with Rails. This command is used to run the application in a development environment and make it accessible via a web browser. The server defaults to port 3000 and listens on localhost.

```bash
$ cd commandsapp
$ bin/rails server
=> Booting Puma
=> Rails 5.1.0 application starting in development on http://0.0.0.0:3000
=> Run `rails server -h` for more startup options
Puma starting in single mode...
* Version 3.0.2 (ruby 2.3.0-p0), codename: Plethora of Penguin Pinatas
* Min threads: 5, max threads: 5
* Environment: development
* Listening on tcp://localhost:3000
Use Ctrl-C to stop
```

```bash
$ bin/rails server -e production -p 4000
```

```bash
$ bin/rails server -d
```

--------------------------------

### Run a Single Rails Test from a File

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Executes a single, specific test case within a file in the Rails project by providing the file path and the test name using Bundler and Ruby.

```bash
$ cd actionpack
$ bundle exec ruby -Itest path/to/test.rb -n test_name
```

--------------------------------

### Create All Test Databases

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Rake command to build test databases for both PostgreSQL and MySQL. This is a convenient task for environments supporting multiple database types.

```shell
cd activerecord
bundle exec rake db:create
```

--------------------------------

### Configuring Rails Environment

Source: https://guides.rubyonrails.org/v7.2/initialization

The `config/environment.rb` file is required early in the Rails startup process. It typically sets up the Rails application instance, which is then passed to the Rack server.

```ruby
# This file is used by Rack-based servers to start the application.

require_relative "config/environment"

run Rails.application

```

--------------------------------

### MySQL EXPLAIN Output Example

Source: https://guides.rubyonrails.org/v5.2/active_record_querying

An example of the output generated by `EXPLAIN` for a Ruby on Rails query when using the MySQL or MariaDB database adapter. It shows the query execution plan, including table access, join types, and index usage.

```text
EXPLAIN for: SELECT `users`.* FROM `users` INNER JOIN `articles` ON `articles`.`user_id` = `users`.`id` WHERE `users`.`id` = 1
+----+-------------+----------+-------+---------------+-----------+---------+---------+------+------+----------+
| id | select_type | table    | type  | possible_keys | key       | key_len | ref     | rows | Extra|
+----+-------------+----------+-------+---------------+-----------+---------+---------+------+------+
|  1 | SIMPLE      | users    | const | PRIMARY       | PRIMARY   | 4       | const   |    1 |      |
|  1 | SIMPLE      | articles | ALL   | NULL          | NULL      | NULL    | NULL    |    1 | Using where |
+----+-------------+----------+-------+---------------+-----------+---------+---------+------+------+
1 row in set (0.00 sec)
```

--------------------------------

### Ruby on Rails: Controller Action to Save Article Data

Source: https://guides.rubyonrails.org/v4.1/getting_started

This Ruby code demonstrates a controller action in Rails for creating and saving a new article. It initializes an Article model with permitted parameters and then attempts to save it to the database. If successful, it redirects to the article's show page.

```ruby
def create
  @article = Article.new(article_params)
  @article.save
  redirect_to @article
end

private

def article_params
  params.require(:article).permit(:title, :text)
end
```

--------------------------------

### Build Rack Application from Configuration or String - Ruby

Source: https://guides.rubyonrails.org/v6.1/initialization

Demonstrates how Rack::Server builds the application, either from a configuration file using Rack::Builder.parse_file or directly from a string using Rack::Builder.new_from_string. It handles options merging and file existence checks.

```Ruby
module Rack
  class Server
    def app
      @app ||= options[:builder] ? build_app_from_string : build_app_and_options_from_config
    end

    # ...

    private
      def build_app_and_options_from_config
        if !::File.exist? options[:config]
          abort "configuration #{options[:config]} not found"
        end

        app, options = Rack::Builder.parse_file(self.options[:config], opt_parser)
        @options.merge!(options) { |key, old, new| old }
        app
      end

      def build_app_from_string
        Rack::Builder.new_from_string(self.options[:builder])
      end

  end
end

```

--------------------------------

### Delete Post Route and Controller Action (Ruby on Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

Defines the route for deleting posts using the DELETE HTTP method and the corresponding controller action to find and destroy a post, then redirects to the posts index. This follows REST conventions for resource destruction.

```Ruby
config/routes.rb:
DELETE /posts/:id(. :format) posts#destroy

app/controllers/posts_controller.rb:
def destroy
  @post = Post.find(params[:id])
  @post.destroy
  redirect_to posts_path
end
```

--------------------------------

### JavaScript: Action Cable Consumer Setup

Source: https://guides.rubyonrails.org/v6.0/action_cable_overview

Initializes an Action Cable consumer in the browser using the `createConsumer` function. This consumer connects to the `/cable` endpoint by default and can be configured with custom URLs or dynamic URL generation.

```javascript
import { createConsumer } from "@rails/actioncable"
export default createConsumer()
```

```javascript
createConsumer('https://ws.example.com/cable')
```

```javascript
createConsumer(getWebSocketURL)
function getWebSocketURL {
  const token = localStorage.get('auth-token')
  return `https://ws.example.com/cable?token=${token}`
}
```

--------------------------------

### Puma Handler: Running the Rack Application

Source: https://guides.rubyonrails.org/v7.1/initialization

Shows how the Puma Rack handler starts the server. It configures Puma with application details and options, then runs the launcher, handling interrupts for graceful shutdown.

```ruby
module Rack
  module Handler
    module Puma
      # ...
      def self.run(app, options = {})
        conf   = self.config(app, options)

        events = options.delete(:Silent) ? ::Puma::Events.strings : ::Puma::Events.stdio

        launcher = ::Puma::Launcher.new(conf, events: events)

        yield launcher if block_given?
        begin
          launcher.run
        rescue Interrupt
          puts "* Gracefully stopping, waiting for requests to finish"
          launcher.stop
          puts "* Goodbye!"
        end
      end
      # ...
    end
  end
end

```

--------------------------------

### Start Rails Development Server

Source: https://guides.rubyonrails.org/v3.0/command_line

This command starts the Rails development server, making the application accessible via a web browser. Typically, you would access it at http://localhost:3000. It's used for testing and viewing the application during development.

```bash
$ rails server
```

--------------------------------

### Implementing Strong Parameters for Article Creation

Source: https://guides.rubyonrails.org/v4.2/getting_started

Enhances the article creation process by using strong parameters to explicitly permit 'title' and 'text' attributes. This is a security measure to prevent unauthorized data from being mass-assigned.

```ruby
@article = Article.new(params.require(:article).permit(:title, :text))
```

--------------------------------

### Ruby Rails Migration: Create Articles Table

Source: https://guides.rubyonrails.org/v4.2/getting_started

This Ruby code defines a database migration for creating an 'articles' table. It uses `create_table` to define columns like 'title' (string) and 'text' (text), along with timestamps for tracking creation and update times. The `change` method ensures the migration is reversible.

```ruby
class CreateArticles < ActiveRecord::Migration
  def change
    create_table :articles do |t|
      t.string :title
      t.text :text
      t.timestamps null: false
    end
  end
end
```

--------------------------------

### Install Yarn on Fedora/CentOS/RHEL

Source: https://guides.rubyonrails.org/v6.1/development_dependencies_install

Installs Yarn package manager on Fedora, CentOS, or RHEL systems. This command adds the Yarn repository and then installs the Yarn package using dnf.

```bash
curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
sudo dnf install yarn
```

--------------------------------

### Build PostgreSQL Test Databases

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Rake command to build the necessary test databases for PostgreSQL within the Active Record gem directory. This ensures proper setup for PostgreSQL testing.

```shell
cd activerecord
bundle exec rake db:postgresql:build
```

--------------------------------

### Installing Webpacker via Rails CLI

Source: https://guides.rubyonrails.org/v6.1/upgrading_ruby_on_rails

Command to run after adding the `webpacker` gem to the Gemfile, used to install and configure Webpacker within a Rails application.

```bash
$ bin/rails webpacker:install
```

```bash
bin/rails webpacker:install
```

--------------------------------

### Render Partial Collection in Rails

Source: https://guides.rubyonrails.org/v4.0/getting_started

This snippet demonstrates how to render a partial for each item in a collection. It assumes a partial named `_comment.html.erb` exists and will be rendered for each comment in the `@post.comments` collection. The `render` method automatically assigns each item to a local variable named after the partial (e.g., `comment`).

```erb
<p>  <strong>Commenter:</strong>  <%= comment.commenter %></p> <p>  <strong>Comment:</strong>  <%= comment.body %></p>
```

```erb
<p>  <strong>Title:</strong>  <%= @post.title %></p> <p>  <strong>Text:</strong>  <%= @post.text %></p> <h2>Comments</h2><%= render @post.comments %> <h2>Add a comment:</h2><%= form_for([@post, @post.comments.build]) do |f| %>  <p>    <%= f.label :commenter %><br />    <%= f.text_field :commenter %>  </p>  <p>    <%= f.label :body %><br />    <%= f.text_area :body %>  </p>  <p>    <%= f.submit %>  </p><% end %> <%= link_to 'Edit Post', edit_post_path(@post) %> |<%= link_to 'Back to Posts', posts_path %>
```

--------------------------------

### Define Subscriber Fixture Data for Rails Tests

Source: https://guides.rubyonrails.org/getting_started

This YAML snippet defines fixture data for the 'Subscriber' model in Rails, including associations to products and email addresses. These fixtures are used to set up the test database for testing email sending functionality.

```yaml
david:
  product: tshirt
  email: david@example.org

chris:
  product: tshirt
  email: chris@example.org
```

--------------------------------

### Install Git Dependencies on Ubuntu

Source: https://guides.rubyonrails.org/v3.2/contributing_to_ruby_on_rails

Installs necessary development libraries for libxml2 and libxslt, which are required for the Nokogiri gem. This command is specific to Ubuntu-based systems.

```shell
sudo apt-get install libxml2 libxml2-dev libxslt1-dev
```

--------------------------------

### Configure and Install Ruby from Source

Source: https://guides.rubyonrails.org/v3.1/performance_testing

Configures the Ruby build to install in a specified directory and then compiles and installs it. Ensure `<homedir>` is replaced with your actual home directory path.

```shell
$ ./configure --prefix=/<homedir>/rubygc
$ make && make install
```

--------------------------------

### Template Inheritance Lookup Order in Rails

Source: https://guides.rubyonrails.org/v5.1/layouts_and_rendering

Explains how Rails searches for templates and partials within the controller and its inheritance chain if not found in the conventional path. This example details the lookup order for an `admin/products#index` action, starting from the specific view path and moving up to the application-level views.

```ruby
class ApplicationController < ActionController::Base
end
```

```ruby
class AdminController < ApplicationController
end
```

```ruby
class Admin::ProductsController < AdminController
  def index
  end
end
```

--------------------------------

### View Generated Rails Routes

Source: https://guides.rubyonrails.org/v5.1/getting_started

This command displays all the routes defined in the Rails application, including those generated by the `resources` method. It helps in understanding how requests are mapped to controllers and actions. The output shows prefixes, HTTP verbs, URI patterns, and corresponding controller#action pairs.

```Shell
$ bin/rails routes
      Prefix Verb      URI Pattern                Controller#Action
    articles GET      /articles(.:format)        articles#index
             POST     /articles(.:format)        articles#create
 new_article GET      /articles/new(.:format)    articles#new
edit_article GET      /articles/:id/edit(.:format) articles#edit
     article GET      /articles/:id(.:format)    articles#show
             PATCH    /articles/:id(.:format)    articles#update
             PUT      /articles/:id(.:format)    articles#update
             DELETE   /articles/:id(.:format)    articles#destroy
        root GET      /                          welcome#index
```

--------------------------------

### Install Development Dependencies on macOS

Source: https://guides.rubyonrails.org/v6.0/development_dependencies_install

This command uses Homebrew to install all the necessary additional tools and services required for Ruby on Rails core development on macOS. After installation, you'll need to start the services.

```bash
brew bundle
```

--------------------------------

### Unicode Character Routes in Rails

Source: https://guides.rubyonrails.org/v4.0/routing

This snippet illustrates how to define routes that directly use Unicode characters in their paths. This allows for internationalized URL structures. The example shows a GET request to a path with Japanese characters being routed to the `welcome` controller's `index` action.

```ruby
get 'こんにちは', to: 'welcome#index'
```

--------------------------------

### Deduplicate Product Fetching with before_action in Rails

Source: https://guides.rubyonrails.org/getting_started

This Ruby on Rails controller demonstrates the use of 'before_action' to define a 'set_product' method that runs before specific actions ('show', 'edit', 'update'). This method fetches the product by ID, reducing code duplication and adhering to the DRY principle. The rest of the controller actions remain similar, but the explicit product fetching is removed from 'show', 'edit', and 'update'.

```ruby
class ProductsController < ApplicationController
  before_action :set_product, only: %i[ show edit update ]

  def index
    @products = Product.all
  end

  def show
  end

  def new
    @product = Product.new
  end

  def create
    @product = Product.new(product_params)
    if @product.save
      redirect_to @product
    else
      render :new, status: :unprocessable_entity
    end
  end

  def edit
  end

  def update
    if @product.update(product_params)
      redirect_to @product
    else
      render :edit, status: :unprocessable_entity
    end
  end

  private
    def set_product
      @product = Product.find(params[:id])
    end

    def product_params
      params.expect(product: [ :name ])
    end
end
```

--------------------------------

### Rails 5.1: Parameterized Mailers Example

Source: https://guides.rubyonrails.org/v5.2/5_1_release_notes

Illustrates the usage of parameterized mailers in Rails 5.1, allowing common parameters to be specified for all methods within a mailer class. This facilitates sharing instance variables and common setup across mailer methods. The example shows how to define a mailer with before_action callbacks for parameter setup and how to invoke it.

```ruby
class InvitationsMailer < ApplicationMailer
  before_action { @inviter, @invitee = params[:inviter], params[:invitee] }
  before_action { @account = @inviter.account }

  def account_invitation
    mail subject: "#{@inviter.name} invited you to their Basecamp (#{@account.name})"
  end
end

InvitationsMailer.with(inviter: person_a, invitee: person_b)
                 .account_invitation.deliver_later
```

--------------------------------

### Install Dependencies on Arch Linux

Source: https://guides.rubyonrails.org/v7.1/development_dependencies_install

Installs various development packages including SQLite, MariaDB, PostgreSQL, Redis, Memcached, ImageMagick, FFmpeg, and Yarn using pacman. Also initializes and starts services.

```shell
$ sudo pacman -S sqlite mariadb libmariadbclient mariadb-clients postgresql postgresql-libs redis memcached imagemagick ffmpeg mupdf mupdf-tools poppler yarn libxml2 libvips poppler
$ sudo mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
$ sudo systemctl start redis mariadb memcached
```

--------------------------------

### Install importmap-rails in Rails

Source: https://guides.rubyonrails.org/v7.1/working_with_javascript_in_rails

This command runs the installation task for the importmap-rails gem, setting up the necessary configurations and files for import map functionality in your Rails application.

```bash
bin/rails importmap:install
```

--------------------------------

### Inspect Generated Routes with `bin/rails routes` (Shell)

Source: https://guides.rubyonrails.org/v6.1/getting_started

This command-line snippet demonstrates how to inspect the routes that have been generated by Rails, typically after defining resources. It displays the HTTP verb, URI pattern, and corresponding controller#action for each route.

```shell
$ bin/rails routes
      Prefix Verb   URI Pattern                  Controller#Action
        root GET    /                            articles#index
    articles GET    /articles(.:format)          articles#index
 new_article GET    /articles/new(.:format)      articles#new
     article GET    /articles/:id(.:format)      articles#show
             POST   /articles(.:format)          articles#create
edit_article GET    /articles/:id/edit(.:format) articles#edit
             PATCH  /articles/:id(.:format)      articles#update
             DELETE /articles/:id(.:format)      articles#destroy

```

--------------------------------

### Apply CSS Styles with Propshaft in Rails

Source: https://guides.rubyonrails.org/getting_started

This CSS code snippet modifies the styling for body, navigation, and product sections. It sets font families, padding, alignment, and image display properties, intended for use with Rails' Propshaft asset pipeline.

```css
body {
  font-family: Arial, Helvetica, sans-serif;
  padding: 1rem;
}

nav {
  justify-content: flex-end;
  display: flex;
  font-size: 0.875em;
  gap: 0.5rem;
  max-width: 1024px;
  margin: 0 auto;
  padding: 1rem;
}

nav a {
  display: inline-block;
}

main {
  max-width: 1024px;
  margin: 0 auto;
}

.notice {
  color: green;
}

section.product {
  display: flex;
  gap: 1rem;
  flex-direction: row;
}

section.product img {
  border-radius: 8px;
  flex-basis: 50%;
  max-width: 50%;
}
```

--------------------------------

### Rails Path Helper Examples

Source: https://guides.rubyonrails.org/v6.1/routing

Shows examples of path helpers generated by Rails for resourceful routes. These helpers simplify the creation of URLs for various actions related to the 'photos' resource, such as accessing the index, new form, edit form, or a specific photo.

```ruby
photos_path returns /photos
new_photo_path returns /photos/new
edit_photo_path(:id) returns /photos/:id/edit (for instance, edit_photo_path(10) returns /photos/10/edit)
photo_path(:id) returns /photos/:id (for instance, photo_path(10) returns /photos/10)
```

--------------------------------

### Active Model API Compliance Test Setup

Source: https://guides.rubyonrails.org/active_model_basics

Shows how to set up tests for Active Model API compliance using `ActiveModel::Lint::Tests`. It includes including the module in a test case and initializing the model instance for testing.

```ruby
class Person
  include ActiveModel::API
end
```

```ruby
require "test_helper"

class PersonTest < ActiveSupport::TestCase
  include ActiveModel::Lint::Tests

  setup do
    @model = Person.new
  end
end
```

--------------------------------

### Rails: Script/Server Support for Thin Web Server

Source: https://guides.rubyonrails.org/v5.1/2_2_release_notes

Highlights the integration of the Thin web server with the `script/server` command. This allows developers to easily start their Rails applications using the Thin server directly from the command line.

```bash
script/server thin
```

--------------------------------

### Ruby: New Framework Defaults Template Example

Source: https://guides.rubyonrails.org/v7.2/contributing_to_ruby_on_rails

Presents an example of a new framework defaults template file (`new_framework_defaults_7_2.rb.tt`) in Ruby. It shows how to include a commented-out section for setting a new configuration value, allowing developers to opt into the new behavior during upgrades.

```ruby
# new_framework_defaults_7_2.rb.tt

# Rails.application.config.active_job.existing_behavior = false

```

--------------------------------

### Default Rails Middleware Stack Example

Source: https://guides.rubyonrails.org/v5.2/rails_on_rack

Illustrates a typical middleware stack output for a freshly generated Rails application. Each line represents a middleware component, showing the sequence of operations applied to requests and responses.

```bash
use Rack::Sendfile
use ActionDispatch::Static
use ActionDispatch::Executor
use ActiveSupport::Cache::Strategy::LocalCache::Middleware
use Rack::Runtime
use Rack::MethodOverride
use ActionDispatch::RequestId
use ActionDispatch::RemoteIp
use Sprockets::Rails::QuietAssets
use Rails::Rack::Logger
use ActionDispatch::ShowExceptions
use WebConsole::Middleware
use ActionDispatch::DebugExceptions
use ActionDispatch::Reloader
use ActionDispatch::Callbacks
use ActiveRecord::Migration::CheckPending
use ActionDispatch::Cookies
use ActionDispatch::Session::CookieStore
use ActionDispatch::Flash
use ActionDispatch::ContentSecurityPolicy::Middleware
use Rack::Head
use Rack::ConditionalGet
use Rack::ETag
use Rack::TempfileReaper
run MyApp::Application.routes
```

--------------------------------

### Install SQLite3 for Various Linux Distributions and FreeBSD

Source: https://guides.rubyonrails.org/v5.0/development_dependencies_install

Installs SQLite3 and its development files, which are required for running the Rails test suite. Commands are provided for Mac OS X (using Homebrew), Ubuntu, Fedora/CentOS, Arch Linux, and FreeBSD.

```bash
# Mac OS X
$ brew install sqlite3

# Ubuntu
$ sudo apt-get install sqlite3 libsqlite3-dev

# Fedora or CentOS
$ sudo yum install sqlite3 sqlite3-devel

# Arch Linux
$ sudo pacman -S sqlite

# FreeBSD
# pkg install sqlite3
# Or compile the databases/sqlite3 port.
```

--------------------------------

### Generate Rails Controller

Source: https://guides.rubyonrails.org/v4.2/getting_started

This command generates a new controller named ArticlesController in your Rails application. This controller will handle requests related to articles.

```bash
bin/rails generate controller articles
```

--------------------------------

### Start Standalone Action Cable Server with Puma (Shell)

Source: https://guides.rubyonrails.org/v7.2/action_cable_overview

This command demonstrates how to start the standalone Action Cable server using Puma. It specifies the port (28080) and the `config.ru` file to use. This allows Action Cable to run independently on a dedicated port.

```bash
$ bundle exec puma -p 28080 cable/config.ru

```

--------------------------------

### Ruby: Get Beginning/End of Minute

Source: https://guides.rubyonrails.org/v5.2/active_support_core_extensions

These Ruby methods return timestamps at the start (hh:mm:00) or end (hh:mm:59) of a specific minute. They are applicable to `Time` and `DateTime` objects. `beginning_of_minute` is aliased to `at_beginning_of_minute`. These methods are not implemented for `Date` objects.

```ruby
date = DateTime.new(2010, 6, 7, 19, 55, 25)
date.beginning_of_minute # => Mon Jun 07 19:55:00 +0200 2010
date.end_of_minute     # => Mon Jun 07 19:55:59 +0200 2010
```

--------------------------------

### Run Tests for a Specific Rails Component

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Navigates to a specific component's directory (e.g., Action Pack) and runs its associated tests using Bundler and Rake.

```bash
$ cd actionpack
$ bundle exec rake test
```

--------------------------------

### Form for Building a Comment in Rails View

Source: https://guides.rubyonrails.org/v4.0/getting_started

This ERB code snippet demonstrates how to create a form for a new comment within a post's show page. It utilizes `form_for` with a nested route structure (`[@post, @post.comments.build]`) to associate comments with specific posts.

```erb
<%= form_for([@post, @post.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br />
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br />
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
```

--------------------------------

### Migrate Database for Dummy App

Source: https://guides.rubyonrails.org/v5.1/plugins

This command navigates to the dummy Rails application directory and executes the database migration. This step is crucial to create the necessary tables in the test database that correspond to the generated `Hickwall` and `Wickwall` models.

```bash
cd test/dummy
bin/rails db:migrate
```

--------------------------------

### Install Development Packages on FreeBSD

Source: https://guides.rubyonrails.org/v6.0/development_dependencies_install

Installs essential development packages on FreeBSD, including database clients and servers, caching services, media tools, and a package manager. It uses the `pkg` command for package installation and `portmaster` for ports-based installations.

```shell
# pkg install sqlite3 mysql80-client mysql80-server postgresql11-client postgresql11-server memcached imagemagick ffmpeg mupdf yarn
# portmaster databases/redis
```

--------------------------------

### Start Rails Development Server

Source: https://guides.rubyonrails.org/v7.2/command_line

The `bin/rails server` command starts the Puma web server, which is bundled with Rails. This command is used to run your Rails application and access it through a web browser. It defaults to the development environment and listens on port 3000.

```shell
$ cd my_app
$ bin/rails server
=> Booting Puma
=> Rails 7.2.0 application starting in development
=> Run `bin/rails server --help` for more startup options
Puma starting in single mode...
* Puma version: 6.4.0 (ruby 3.1.3-p185) ("The Eagle of Durango")
*  Min threads: 5
*  Max threads: 5
*  Environment: development
*          PID: 5295
* Listening on http://127.0.0.1:3000
* Listening on http://[::1]:3000
Use Ctrl-C to stop

```

--------------------------------

### Active Record Transaction Start Example

Source: https://guides.rubyonrails.org/v7.2/active_support_instrumentation

Demonstrates how Active Record starts a database transaction. The event is fired when the transaction is actually initiated, not necessarily when `ActiveRecord::Base.transaction` is called.

```ruby
ActiveRecord::Base.transaction do
  # We are inside the block, but no event has been triggered yet.

  # The following line makes Active Record start the transaction.
  User.count # Event fired here.
end
```

--------------------------------

### Start find_each from a Specific ID in Ruby

Source: https://guides.rubyonrails.org/v4.2/active_record_querying

Enables resuming interrupted batch processes or starting from a specific record ID. The `start` option combined with `batch_size` allows for efficient processing of large, segmented datasets. Example starts from ID 2000 with a batch size of 5000.

```ruby
User.find_each(start: 2000, batch_size: 5000) do |user|
  NewsMailer.weekly(user).deliver_now
end
```

--------------------------------

### Puma Server Handler Run Method

Source: https://guides.rubyonrails.org/initialization

The `run` method from the Puma Rack handler, responsible for launching the Puma server. It configures Puma with the application and options, sets up logging, and starts the server. It includes graceful shutdown handling for `Interrupt` signals. Dependencies include `Puma::Launcher` and `Puma::LogWriter`.

```ruby
module Rack
  module Handler
    module Puma
      # ...
      def self.run(app, options = {})
        conf = self.config(app, options)

        log_writer = options.delete(:Silent) ? ::Puma::LogWriter.strings : ::Puma::LogWriter.stdio

        launcher = ::Puma::Launcher.new(conf, log_writer: log_writer, events: @events)

        yield launcher if block_given?
        begin
          launcher.run
        rescue Interrupt
          puts "* Gracefully stopping, waiting for requests to finish"
          launcher.stop
          puts "* Goodbye!"
        end
      end
      # ...
    end
  end
end

```

--------------------------------

### Install Action Mailbox - Ruby on Rails

Source: https://guides.rubyonrails.org/action_mailbox_basics

Installs the Action Mailbox gem, creating necessary files and migrations for email processing within a Rails application. It generates an `application_mailbox.rb` file and prepares the database schema.

```bash
bin/rails action_mailbox:install
```

--------------------------------

### EXPLAIN Output Example - PostgreSQL

Source: https://guides.rubyonrails.org/v5.1/active_record_querying

This is an example of the `EXPLAIN` output for a Ruby on Rails query executed on PostgreSQL. It presents the query plan using PostgreSQL's specific format, detailing join methods, costs, and row estimates for performance tuning.

```sql
EXPLAIN for: SELECT "users".* FROM "users" INNER JOIN "articles" ON "articles"."user_id" = "users"."id" WHERE "users"."id" = 1
               
QUERY PLAN
------------------------------------------------------------------------------
 Nested Loop Left Join  (cost=0.00..37.24 rows=8 width=0) 
   Join Filter: (articles.user_id = users.id) 
   ->  Index Scan using users_pkey on users  (cost=0.00..8.27 rows=1 width=4) 
     Index Cond: (id = 1) 
   ->  Seq Scan on articles  (cost=0.00..28.88 rows=8 width=4) 
     Filter: (articles.user_id = 1) 
(6 rows)
```

--------------------------------

### Get Beginning and End of Minute with Rails Methods

Source: https://guides.rubyonrails.org/v4.0/active_support_core_extensions

The `beginning_of_minute` and `end_of_minute` methods return a `Time` or `DateTime` object representing the start (hh:mm:00) or end (hh:mm:59) of a given minute. These methods are available for `Time` and `DateTime` objects.

```ruby
date = DateTime.new(2010, 6, 7, 19, 55, 25)
date.beginning_of_minute # => Mon Jun 07 19:55:00 +0200 2010
date.end_of_minute # => Mon Jun 07 19:55:59 +0200 2010
```

--------------------------------

### Start Rails Server

Source: https://guides.rubyonrails.org/v6.0/command_line

The `rails server` command starts the development web server for a Rails application. This allows you to access your application locally in a web browser. The server typically runs on `http://localhost:3000` by default.

```bash
$ rails server
=> Booting Puma...
```

--------------------------------

### Action Controller Page Instrumentation Examples

Source: https://guides.rubyonrails.org/v5.0/active_support_instrumentation

Examples showcasing instrumentation hooks for managing page caching in Action Controller. These events provide the path associated with page operations like writing or expiring.

```ruby
write_page.action_controller
# Example data:
# {"path": "/users/1"}
```

```ruby
expire_page.action_controller
# Example data:
# {"path": "/users/1"}
```

--------------------------------

### Install and Update Bundler

Source: https://guides.rubyonrails.org/v4.0/development_dependencies_install

Installs or updates the Bundler gem, a dependency manager for Ruby projects. It ensures you have a recent version of Bundler, which is crucial for managing project dependencies.

```bash
$ gem install bundler
$ gem update bundler
```

--------------------------------

### Define Nested Comment Routes in Rails

Source: https://guides.rubyonrails.org/v6.1/getting_started

This Ruby code snippet defines nested routes for comments within articles using Rails' resource routing. It establishes a hierarchical relationship in the application's navigation. No external dependencies are required beyond a standard Rails setup.

```ruby
Rails.application.routes.draw do
  root "articles#index"

  resources :articles do
    resources :comments
  end
end
```

--------------------------------

### Install Development Dependencies on Fedora or CentOS

Source: https://guides.rubyonrails.org/v6.1/development_dependencies_install

Installs necessary development packages on Fedora or CentOS using the DNF package manager. This includes database clients and servers, caching services, media tools, and preparation for Yarn installation.

```shell
sudo dnf install sqlite-devel sqlite-libs mysql-server mysql-devel postgresql-server postgresql-devel redis memcached imagemagick ffmpeg mupdf libxml2-devel

# Install Yarn
# Use this command if you do not have Node.js installed
curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo bash -
```

--------------------------------

### Ruby Schema Dump Example (db/schema.rb)

Source: https://guides.rubyonrails.org/v6.1/active_record_migrations

An example of a database schema definition in Ruby format, as generated by `db/schema.rb`. This file represents the current state of the database schema and is used for loading.

```ruby
ActiveRecord::Schema.define(version: 2008_09_06_171750) do
  create_table "authors", force: true do |t|
    t.string   "name"
    t.datetime "created_at"
    t.datetime "updated_at"
  end

  create_table "products", force: true do |t|
    t.string   "name"
    t.text     "description"
    t.datetime "created_at"
    t.datetime "updated_at"
    t.string   "part_number"
  end
end
```

--------------------------------

### Rack::Server Default Options

Source: https://guides.rubyonrails.org/v4.1/initialization

Defines the default configuration options for the Rack server, including environment, PID file, port, host, access log, and configuration file path.

```ruby
def default_options
  {
    environment: ENV['RACK_ENV'] || "development",
    pid:         nil,
    Port:        9292,
    Host:        "0.0.0.0",
    AccessLog:   [],
    config:      "config.ru"
  }
end
```

--------------------------------

### Rails Server Start Method (`Rails::Server#start`)

Source: https://guides.rubyonrails.org/v5.1/initialization

Initiates the Rails server by setting up signal traps, creating temporary directories, configuring development caching, setting up stdout logging, and then invoking the superclass's start method. It's the primary entry point for server execution after application configuration is loaded.

```ruby
def start
  print_boot_information
  trap(:INT) { exit }
  create_tmp_directories
  setup_dev_caching
  log_to_stdout if options[:log_stdout]
  super
  ...
end
```

--------------------------------

### Constrain Route to Multiple HTTP Verbs in Ruby

Source: https://guides.rubyonrails.org/v3.0/routing

This Ruby code shows how to define a route that can be accessed using multiple HTTP verbs (GET and POST in this example). The `:via` option accepts an array of symbols representing the allowed HTTP methods.

```Ruby
match 'photos/show' => 'photos#show', :via => [:get, :post]
```

--------------------------------

### Start find_each from Specific Primary Key (Ruby on Rails)

Source: https://guides.rubyonrails.org/v3.1/active_record_querying

Enables resuming interrupted batch processes or starting iteration from a specific primary key using the `:start` option. Records are processed in ascending order of primary keys.

```ruby
User.find_each(:batch_size => 5000, :start => 2000) do |user|
  NewsLetter.weekly_deliver(user)
end
```

--------------------------------

### Ruby on Rails: Action Cable Channel Setup

Source: https://guides.rubyonrails.org/v6.0/action_cable_overview

Defines the parent `ApplicationCable::Channel` class for encapsulating shared logic among custom channels. It serves as a base class for creating specific channels like `ChatChannel` and `AppearanceChannel`.

```ruby
module ApplicationCable
  class Channel < ActionCable::Channel::Base
  end
end
```

```ruby
class ChatChannel < ApplicationCable::Channel
end
```

```ruby
class AppearanceChannel < ApplicationCable::Channel
end
```

--------------------------------

### SecurePassword Authentication Examples

Source: https://guides.rubyonrails.org/active_model_basics

These IRB examples illustrate the usage of ActiveModel::SecurePassword's authentication methods. They show how to validate passwords, password confirmations, and authenticate using both primary and recovery passwords.

```irb
irb> person = Person.new

# When password is blank.
irb> person.valid?
=> false

# When the confirmation doesn't match the password.
irb> person.password = "aditya"
irb> person.password_confirmation = "nomatch"
irb> person.valid?
=> false

# When the length of password exceeds 72.
irb> person.password = person.password_confirmation = "a" * 100
irb> person.valid?
=> false

# When only password is supplied with no password_confirmation.
irb> person.password = "aditya"
irb> person.valid?
=> true

# When all validations are passed.
irb> person.password = person.password_confirmation = "aditya"
irb> person.valid?
=> true

irb> person.recovery_password = "42password"

# `authenticate` is an alias for `authenticate_password`
irb> person.authenticate("aditya")
=> #<Person> # == person
irb> person.authenticate("notright")
=> false
irb> person.authenticate_password("aditya")
=> #<Person> # == person
irb> person.authenticate_password("notright")
=> false

irb> person.authenticate_recovery_password("aditya")
=> false
irb> person.authenticate_recovery_password("42password")
=> #<Person> # == person
irb> person.authenticate_recovery_password("notright")
=> false

irb> person.password_digest
=> "$2a$04$gF8RfZdoXHvyTjHhiU4ZsO.kQqV9oonYZu31PRE4hLQn3xM2qkpIy"
irb> person.recovery_password_digest
=> "$2a$04$iOfhwahFymCs5weB3BNH/uXkTG65HR.qpW.bNhEjFP3ftli3o5DQC"

```

--------------------------------

### Rails Server Middleware Configuration (Ruby)

Source: https://guides.rubyonrails.org/v3.1/rails_on_rack

Demonstrates how `rails server` constructs a `Rack::Builder` object by using various middleware components before running the main Rails application.

```ruby
app = Rack::Builder.new {
  use Rails::Rack::LogTailer unless options[:detach]
  use Rails::Rack::Debugger if options[:debugger]
  use ActionDispatch::Static
  run ActionController::Dispatcher.new
}.to_app
```

--------------------------------

### List Available bin/rails Tasks

Source: https://guides.rubyonrails.org/v5.2/command_line

The `bin/rails --help` or `bin/rails -T` command displays a list of all available tasks for the Rails application. This helps users discover and understand the various commands they can execute, such as generating code, managing the console, or starting the server.

```bash
$ bin/rails --help
$ bin/rails -T
```

--------------------------------

### Git: Checkout and Create Branch

Source: https://guides.rubyonrails.org/v3.1/contributing_to_ruby_on_rails

Commands to create a new Git branch for testing or development. This isolates your changes from the main codebase.

```bash
git checkout -b testing_branch
```

```bash
git checkout -b my_new_branch
```

--------------------------------

### Rails Server Initialization and Setup

Source: https://guides.rubyonrails.org/v4.2/initialization

This Ruby code prepares the environment for the Rails server by changing the directory and requiring necessary components. It initializes the `Rails::Server` class, which inherits from `Rack::Server`, and starts the server after setting the application environment.

```ruby
def set_application_directory!
  Dir.chdir(File.expand_path('../../', APP_PATH)) unless File.exist?(File.expand_path("config.ru"))
end
def server
  set_application_directory!
  require_command!("server")
  Rails::Server.new.tap do |server|
    # We need to require application after the server sets environment,
    # otherwise the --environment option given to the server won't propagate.
    require APP_PATH
    Dir.chdir(Rails.application.root)
    server.start
  end
end
def require_command!(command)
  require "rails/commands/#{command}"
end
```

--------------------------------

### Initialize Rails Server Environment

Source: https://guides.rubyonrails.org/v4.1/initialization

This Ruby code prepares the Rails application environment for the server. It changes the directory to the Rails root if `config.ru` is not found, requires the server command, and then instantiates and starts `Rails::Server`.

```ruby
def set_application_directory!
  Dir.chdir(File.expand_path('../../', APP_PATH)) unless
    File.exist?(File.expand_path("config.ru"))
end
def server
  set_application_directory!
  require_command!("server")
  Rails::Server.new.tap do |server|
    require APP_PATH
    Dir.chdir(Rails.application.root)
    server.start
  end
end
def require_command!(command)
  require "rails/commands/#{command}"
end
```

--------------------------------

### Rails Controller Test with Setup and Teardown

Source: https://guides.rubyonrails.org/v5.0/testing

Refactored controller tests using setup and teardown to manage the '@article' instance variable and clear cache, reducing code duplication.

```ruby
require 'test_helper'
class ArticlesControllerTest < ActionDispatch::IntegrationTest
  # called before every single test
  setup do
    @article = articles(:one)
  end

  # called after every single test
  teardown do
    # when controller is using cache it may be a good idea to reset it afterwards
    Rails.cache.clear
  end

  test "should show article" do
    # Reuse the @article instance variable from setup
    get article_url(@article)
    assert_response :success
  end

  test "should destroy article" do
    assert_difference('Article.count', -1) do
      delete article_url(@article)
    end
    assert_redirected_to articles_path
  end

  test "should update article" do
    patch article_url(@article), params: { article: { title: "updated" } }
    assert_redirected_to article_path(@article)
    # Reload association to fetch updated data and assert that title is updated.
    @article.reload
    assert_equal "updated", @article.title
  end
end
```

--------------------------------

### Render submitted form parameters in create action (Ruby on Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This snippet modifies the `create` action in the `PostsController` to render the submitted form parameters using `params[:post].inspect`. This is useful for inspecting the data sent from the form before it's processed or saved.

```ruby
def create
  render text: params[:post].inspect
end
```

--------------------------------

### Rails Controller Create Action

Source: https://guides.rubyonrails.org/v4.1/getting_started

This Ruby code defines the `create` action for the `CommentsController`. It finds the associated article, creates a new comment using permitted parameters, and redirects to the article's show page. It also includes a private method for strong parameter validation.

```ruby
class CommentsController < ApplicationController
  def create
    @article = Article.find(params[:article_id])
    @comment = @article.comments.create(comment_params)
    redirect_to article_path(@article)
  end

  private
    def comment_params
      params.require(:comment).permit(:commenter, :body)
    end
end
```

--------------------------------

### Generate Ruby on Rails Controller

Source: https://guides.rubyonrails.org/v5.0/getting_started

Command to generate a new controller named ArticlesController in a Rails application. This command creates the controller file and sets up basic routing if needed.

```bash
bin/rails generate controller Articles
```

--------------------------------

### Filter Records by Name in Ruby on Rails

Source: https://guides.rubyonrails.org/getting_started

Use the `where` method to filter database records based on a specific column's value. This method returns an `ActiveRecord::Relation`, allowing for further chaining of query methods. It translates to a SQL `SELECT` statement with a `WHERE` clause.

```ruby
store(dev)> Product.where(name: "Pants")
  Product Load (1.5ms)  SELECT "products".* FROM "products" WHERE "products"."name" = 'Pants' /* loading for pp */ LIMIT 11 /*application='Store'*/
=> [#<Product:0x000000012184d858 id: 2, name: "Pants", created_at: "2024-11-09 16:36:01.856751000 +0000", updated_at: "2024-11-09 16:36:01.856751000 +0000">]
```

--------------------------------

### Verify Node.js Installation

Source: https://guides.rubyonrails.org/v7.1/working_with_javascript_in_rails

This command checks if Node.js is installed and accessible in your system's PATH. It prints the installed version of Node.js, ensuring it meets the minimum requirement for certain JavaScript bundlers.

```bash
node --version
```

--------------------------------

### Rails Controller Code Example

Source: https://guides.rubyonrails.org/command_line

Example of a generated Rails controller action. This code defines a 'hello' action within the GreetingsController, sets an instance variable `@message`, which can then be used in the corresponding view.

```ruby
class GreetingsController < ApplicationController
  def hello
    @message = "Hello, how are you today?"
  end
end

```

--------------------------------

### Navigate to Application Directory

Source: https://guides.rubyonrails.org/v5.0/getting_started

Changes the current directory to the newly created Rails application's root folder. This is a standard command-line operation required before running application-specific commands.

```bash
$ cd blog
```

--------------------------------

### Render Form Partial in Rails

Source: https://guides.rubyonrails.org/v4.0/getting_started

This snippet shows how to render a specific form partial, `_form.html.erb`, to be used for creating or editing comments. The `@post` instance variable is accessible within the partial, allowing the form to be correctly associated with the post. This promotes code reuse and organization.

```erb
<%= form_for([@post, @post.comments.build]) do |f| %>  <p>    <%= f.label :commenter %><br />    <%= f.text_field :commenter %>  </p>  <p>    <%= f.label :body %><br />    <%= f.text_area :body %>  </p>  <p>    <%= f.submit %>  </p><% end %>
```

```erb
<p>  <strong>Title:</strong>  <%= @post.title %></p> <p>  <strong>Text:</strong>  <%= @post.text %></p> <h2>Comments</h2><%= render @post.comments %> <h2>Add a comment:</h2><%= render "comments/form" %> <%= link_to 'Edit Post', edit_post_path(@post) %> |<%= link_to 'Back to Posts', posts_path %>
```

--------------------------------

### Action Controller Fragment Instrumentation Examples

Source: https://guides.rubyonrails.org/v5.0/active_support_instrumentation

Examples demonstrating instrumentation hooks for managing fragments in Action Controller. These events provide details about the cache key used for operations like writing, reading, expiring, or checking the existence of fragments.

```ruby
write_fragment.action_controller
# Example data:
# {"key": "posts/1-dashboard-view"}
```

```ruby
read_fragment.action_controller
# Example data:
# {"key": "posts/1-dashboard-view"}
```

```ruby
expire_fragment.action_controller
# Example data:
# {"key": "posts/1-dashboard-view"}
```

```ruby
exist_fragment?.action_controller
# Example data:
# {"key": "posts/1-dashboard-view"}
```

--------------------------------

### Example Git Commit Message

Source: https://guides.rubyonrails.org/v5.2/contributing_to_ruby_on_rails

This demonstrates a well-formatted Git commit message, including a concise subject line, a detailed description wrapped at 72 characters, multiple paragraphs, indented code examples, and bullet points.

```text
Short summary (ideally 50 characters or less)
More detailed description, if necessary. It should be wrapped to
72 characters. Try to be as descriptive as you can. Even if you
think that the commit content is obvious, it may not be obvious
to others. Add any description that is already present in the
relevant issues; it should not be necessary to visit a webpage
to check the history.
The description section can have multiple paragraphs.
Code examples can be embedded by indenting them with 4 spaces:
    class ArticlesController
      def index
        render json: Article.limit(10)
      end
    end
You can also add bullet points:
- make a bullet point by starting a line with either a dash (-)
  or an asterisk (*)
- wrap lines at 72 characters, and indent any additional lines
  with 2 spaces for readability
```

--------------------------------

### Custom Validation Logic with `validates_each` in Rails

Source: https://guides.rubyonrails.org/active_record_validations

Defines custom validation logic for attributes using a block. This example enforces that 'name' and 'surname' must start with an uppercase letter. Errors are added to the record's error collection if the validation fails.

```ruby
class Person < ApplicationRecord
  validates_each :name, :surname do |record, attr, value|
    record.errors.add(attr, "must start with upper case") if /\A[[:lower:]]/.match?(value)
  end
end
```

--------------------------------

### Ruby Schema Dump Example

Source: https://guides.rubyonrails.org/v7.0/active_record_migrations

An example of a database schema dump in Ruby format (`db/schema.rb`). This file represents the database structure using Rails' DSL.

```ruby
ActiveRecord::Schema[7.0].define(version: 2008_09_06_171750) do
  create_table "authors", force: true do |t|
    t.string   "name"
    t.datetime "created_at"
    t.datetime "updated_at"
  end

  create_table "products", force: true do |t|
    t.string   "name"
    t.text     "description"
    t.datetime "created_at"
    t.datetime "updated_at"
    t.string   "part_number"
  end
end

```

--------------------------------

### List Available Services on macOS

Source: https://guides.rubyonrails.org/v7.1/development_dependencies_install

Lists all services managed by Homebrew on macOS. This command is used to identify the names of services that can be started, stopped, or restarted.

```bash
$ brew services list
```

--------------------------------

### Configuration Guide Entry for `config.active_job.existing_behavior`

Source: https://guides.rubyonrails.org/v7.1/contributing_to_ruby_on_rails

Illustrates how to document a framework default in the configuration guide (`configuration.md`). It shows the default value for previous versions and the new default value starting from a specific Rails version (7.1).

```markdown
#### `config.active_job.existing_behavior

| Starting with version | The default value is |
| --------------------- | -------------------- |
| (original)            | `true`               |
| 7.1                   | `false`              |


```

--------------------------------

### Action Cable Connection Setup - Ruby

Source: https://guides.rubyonrails.org/action_cable_overview

Demonstrates the basic setup for an Action Cable connection in a Rails application. This involves defining the connection class, which extends `ActionCable::Connection::Base`, and implementing authorization logic to identify and allow incoming WebSocket connections.

```ruby
module ApplicationCable
  class Connection < ActionCable::Connection::Base
    identified_by :current_user

    def connect
      self.current_user = find_verified_user
      reject_unauthorized_connection unless current_user
    end

    private

    def find_verified_user
      # Implement your user identification logic here, e.g., using cookies or tokens
      # Example: User.find(cookies.encrypted[:user_id])
      verified_user = env['warden']&.user
    end
  end
end
```

--------------------------------

### Ruby: Documenting Framework Behavior with Asset Pipeline Example

Source: https://guides.rubyonrails.org/v6.0/api_documentation_guidelines

Shows an example of documenting the behavior of a method (`image_tag`) within the context of the full Rails stack, specifically considering the Asset Pipeline's influence on the output.

```ruby
# image_tag("icon.png")#   # => <img src="/assets/icon.png" />
```

--------------------------------

### Enable Development Caching (Rails CLI)

Source: https://guides.rubyonrails.org/getting_started

This command enables caching features in a Rails development environment. Running this command allows developers to test and debug caching mechanisms locally before deploying to production. It typically involves starting a local server with caching enabled.

```bash
$ bin/rails dev:cache
```

--------------------------------

### Install Development Dependencies on Ubuntu

Source: https://guides.rubyonrails.org/v4.0/development_dependencies_install

Installs necessary libraries for Nokogiri (libxml2, libxslt) and SQLite3, including their development files, on Ubuntu systems. These are required for running tests and building certain Ruby gems.

```bash
$ sudo apt-get install libxml2 libxml2-dev libxslt1-dev
$ sudo apt-get install sqlite3 libsqlite3-dev
```

--------------------------------

### Controller Actions for Creating Articles in Rails

Source: https://guides.rubyonrails.org/v7.2/getting_started

Implements the `new` and `create` actions in a Rails controller to handle article creation. The `create` action attempts to save the article and renders the `new` view with errors if validation fails.

```ruby
  def new
    @article = Article.new
  end

  def create
    @article = Article.new(article_params)

    if @article.save
      redirect_to @article
    else
      render :new, status: :unprocessable_entity
    end
  end


```

--------------------------------

### Create a New Rails Application

Source: https://guides.rubyonrails.org/v3.1/command_line

The `rails new` command initializes a new Rails application with a complete directory structure and default code. It requires Ruby and the Rails gem to be installed.

```bash
$ rails new commandsapp
create  README
create  .gitignore
create  Rakefile
create  config.ru
create  Gemfile
create  app
...
create  tmp/cache
create  tmp/pids
create  vendor/plugins
create  vendor/plugins/.gitkeep
```

--------------------------------

### Restrict Comment Deletion with HTTP Basic Authentication in Rails

Source: https://guides.rubyonrails.org/v4.0/getting_started

This Ruby snippet shows how to apply HTTP basic authentication specifically to the `destroy` action in the `CommentsController`. This ensures only authenticated users can delete comments. It assumes a `Post` model and a `comments` resource are set up.

```ruby
class CommentsController < ApplicationController
  http_basic_authenticate_with name: "dhh", password: "secret", only: :destroy

  def create
    @post = Post.find(params[:post_id])
    ...
  end
  # snipped for brevity
```

--------------------------------

### Shorthand for GET HTTP Verb Constraint in Rails

Source: https://guides.rubyonrails.org/v3.1/routing

Presents a shorthand syntax for constraining a route to GET requests.

```ruby
get 'photos/show'
```

--------------------------------

### Create a New Rails Application with `rails new`

Source: https://guides.rubyonrails.org/v3.0/command_line

The `rails new` command initializes a new Ruby on Rails application. It sets up the standard directory structure and essential files needed for a Rails project. Ensure the rails gem is installed first.

```bash
$ rails new commandsapp
create
create  README
create  .gitignore
create  Rakefile
create  config.ru
create  Gemfile
create  app
...
create  tmp/cache
create  tmp/pids
create  vendor/plugins
create  vendor/plugins/.gitkeep
```

--------------------------------

### Railties Script Server and Plugin Installation

Source: https://guides.rubyonrails.org/v6.0/2_2_release_notes

Describes updates to Rails' command-line scripts. `script/server` now includes direct support for the Thin web server. `script/plugin install` has been improved to work seamlessly with both Git and SVN-based plugins, allowing specification of a revision.

```bash
# Install a plugin from Git at a specific revision
script/plugin install git://github.com/user/repo.git -r abc123def

# Install a plugin from SVN at a specific revision
script/plugin install http://svn.example.com/repo/trunk -r 123
```

--------------------------------

### Rails Model Validation: Presence and Length

Source: https://guides.rubyonrails.org/v4.0/getting_started

This Ruby code snippet defines validation rules for a Rails model. It ensures that the 'title' attribute is present and has a minimum length of 5 characters. This is a common pattern for ensuring data integrity before saving to the database.

```ruby
class Post < ActiveRecord::Base
  validates :title, presence: true,
                  length: { minimum: 5 }
end
```

--------------------------------

### Specifying a Starting Point with find_each in Rails

Source: https://guides.rubyonrails.org/v4.0/active_record_querying

Use the `:start` option with `find_each` to begin processing records from a specific primary key ID. This is useful for resuming interrupted batch jobs or distributing work among multiple workers. This example starts from ID 2000 with a batch size of 5000.

```ruby
User.find_each(start: 2000, batch_size: 5000) do |user|
  NewsLetter.weekly_deliver(user)
end
```

--------------------------------

### Display Rails Application Environment Information

Source: https://guides.rubyonrails.org/v6.0/command_line

The `rails about` command provides a summary of the application's environment, including Rails version, Ruby version, database adapter, and other key details. This information is valuable for debugging, seeking support, or understanding the application's setup.

```bash
$ rails about
About your application's environment
Rails version                   6.0.0
Ruby version                   2.5.0 (x86_64-linux)
RubyGems version                2.7.3
Rack version                   2.0.4
JavaScript Runtime         Node.js (V8)
Middleware:               Rack::Sendfile, ActionDispatch::Static, ActionDispatch::Executor, ActiveSupport::Cache::Strategy::LocalCache::Middleware, Rack::Runtime, Rack::MethodOverride, ActionDispatch::RequestId, ActionDispatch::RemoteIp, Sprockets::Rails::QuietAssets, Rails::Rack::Logger, ActionDispatch::ShowExceptions, WebConsole::Middleware, ActionDispatch::DebugExceptions, ActionDispatch::Reloader, ActionDispatch::Callbacks, ActiveRecord::Migration::CheckPending, ActionDispatch::Cookies, ActionDispatch::Session::CookieStore, ActionDispatch::Flash, Rack::Head, Rack::ConditionalGet, Rack::ETag
Application root                 /home/foobar/commandsapp
Environment                     development
Database adapter                sqlite3
Database schema version       20180205173523

```

--------------------------------

### Rails Controller: Complete ArticlesController with Destroy Action

Source: https://guides.rubyonrails.org/v5.0/getting_started

The complete `ArticlesController` including index, show, new, edit, create, update, and the newly added destroy actions, along with the private `article_params` method for strong parameters. This provides the full CRUD functionality for articles.

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end 
  def show
    @article = Article.find(params[:id])
  end 
  def new
    @article = Article.new
  end 
  def edit
    @article = Article.find(params[:id])
  end 
  def create
    @article = Article.new(article_params)
    if @article.save
      redirect_to @article
    else
      render 'new'
    end
  end 
  def update
    @article = Article.find(params[:id])
    if @article.update(article_params)
      redirect_to @article
    else
      render 'edit'
    end
  end 
  def destroy
    @article = Article.find(params[:id])
    @article.destroy
    redirect_to articles_path
  end 
  private
    def article_params
      params.require(:article).permit(:title, :text)
    end
end
```

--------------------------------

### Example Migration Script (Ruby)

Source: https://guides.rubyonrails.org/v2.3/plugins

This is an example of a Ruby on Rails migration file, `db/migrate/20081116181115_create_birdhouses.rb`, that defines the `up` and `down` methods for creating birdhouses. It utilizes `ActiveRecord::Migration` and calls into a `Yaffle::CreateBirdhouses` class for the actual schema changes. It depends on ActiveRecord.

```ruby
class CreateBirdhouses < ActiveRecord::Migration
  def self.up
    Yaffle::CreateBirdhouses.up
  end

  def self.down
    Yaffle::CreateBirdhouses.down
  end
end
```

--------------------------------

### Run Rails Server with Mongrel Backend (Ruby)

Source: https://guides.rubyonrails.org/v2.3/command_line

This command demonstrates how to run the Rails development server using the Mongrel backend. First, the `mongrel` gem needs to be installed. Then, `script/server mongrel` is used to start the server, indicating Rails will boot using Mongrel. This leverages Rack integration, allowing various web servers to host Rails applications.

```shell
# Install the mongrel gem
$ sudo gem install mongrel
Building native extensions.  This could take a while...
Building native extensions.  This could take a while...
Successfully installed gem_plugin-0.2.3
Successfully installed fastthread-1.0.1
Successfully installed cgi_multipart_eof_fix-2.5.0
Successfully installed mongrel-1.1.5
...
...
Installing RDoc documentation for mongrel-1.1.5...

# Start the Rails server with the mongrel backend
$ script/server mongrel
=> Booting Mongrel (use 'script/server webrick' to force WEBrick)
=> Rails 2.2.0 application starting on http://0.0.0.0:3000
...
```

--------------------------------

### Create Rails Blog Application

Source: https://guides.rubyonrails.org/v2.3/getting_started

This command creates a new Ruby on Rails application. By default, it uses SQLite for data storage. You can specify other databases like MySQL or PostgreSQL using the -d flag.

```bash
$ rails blog

```

```bash
$ rails blog -d mysql

```

```bash
$ rails blog -d postgresql

```

--------------------------------

### JavaScript Manifest Example

Source: https://guides.rubyonrails.org/v5.1/asset_pipeline

Example of a JavaScript manifest file that includes other JavaScript files. The 'body=1' parameter is required by Sprockets for proper asset handling.

```html
<script src="/assets/core.js?body=1"></script>
<script src="/assets/projects.js?body=1"></script>
<script src="/assets/tickets.js?body=1"></script>
```

--------------------------------

### Deeply Nested Resources Example

Source: https://guides.rubyonrails.org/v7.0/routing

Illustrates a deeply nested resource structure and discusses the recommended limits for nesting.

```APIDOC
## Deeply Nested Resources Example

This section demonstrates an example of deeply nested resources and discusses the limitations and best practices.

### Example Structure

```ruby
resources :publishers do
  resources :magazines do
    resources :photos
  end
end
```

This structure would recognize paths such as `/publishers/1/magazines/2/photos/3`.

### Recommendation

Resources should ideally not be nested more than one level deep to avoid cumbersome URLs and routing helpers.
```

--------------------------------

### Create All Databases

Source: https://guides.rubyonrails.org/v6.1/active_record_multiple_databases

Creates all databases defined in the `config/database.yml` file for the current environment. This is a convenient way to set up all necessary databases for your application.

```bash
bin/rails db:create
```

--------------------------------

### Active Storage JavaScript npm Package Initialization

Source: https://guides.rubyonrails.org/active_storage_overview

Imports and starts the Active Storage JavaScript library when using it via the npm package for direct uploads.

```javascript
import * as ActiveStorage from "@rails/activestorage"
ActiveStorage.start()
```

--------------------------------

### Rackup Configuration for Rails Application

Source: https://guides.rubyonrails.org/v3.2/rails_on_rack

Shows how to configure a Rails application to be served using `rackup` by creating a `config.ru` file. This file specifies the necessary middleware and the main Rails application object.

```ruby
# Rails.root/config.ru
require "config/environment"
use Rails::Rack::LogTailer
use ActionDispatch::Static
run ActionController::Dispatcher.new
```

--------------------------------

### Documenting Options with Examples in Rails

Source: https://guides.rubyonrails.org/api_documentation_guidelines

Provides detailed documentation for options, including explanations, examples, and potential usage scenarios. This style is useful for complex options like expiration times.

```ruby
# ==== Options
#
# [+:expires_at+]
#   The datetime at which the message expires. After this datetime,
#   verification of the message will fail.
#
#     message = encryptor.encrypt_and_sign("hello", expires_at: Time.now.tomorrow)
#     encryptor.decrypt_and_verify(message) # => "hello"
#     # 24 hours later...
#     encryptor.decrypt_and_verify(message) # => nil
```

--------------------------------

### Generate Rails Controller and Action

Source: https://guides.rubyonrails.org/v6.1/getting_started

Generates a new controller named 'ArticlesController' with an 'index' action and associated view files. The `--skip-routes` option is used because the route has already been manually defined. Requires Ruby.

```bash
$ bin/rails generate controller Articles index --skip-routes

```

--------------------------------

### Copy Migrations from Multiple Engines (Ruby on Rails)

Source: https://guides.rubyonrails.org/v7.1/engines

Installs migrations from all installed Rails engines into the application's database. Use this command when you have multiple engines requiring migration setup. It's a more general version of `blorgh:install:migrations`.

```bash
bin/rails railties:install:migrations
```

--------------------------------

### Require Rails Application Configuration

Source: https://guides.rubyonrails.org/initialization

This code snippet demonstrates the initial step in loading the Rails application configuration by requiring the `config/application.rb` file. This is a fundamental part of the Rails boot process.

```ruby
require_relative "application"

```

--------------------------------

### Rackup Configuration for Rails in Ruby

Source: https://guides.rubyonrails.org/v4.2/rails_on_rack

Provides the content for a `config.ru` file, enabling a Rails application to be served using `rackup`. It requires the Rails environment and runs the application.

```ruby
# Rails.root/config.ru
require ::File.expand_path('../config/environment', __FILE__)
use Rack::ContentLength
run Rails.application
```

--------------------------------

### Add Comment Destroy Link in Rails View

Source: https://guides.rubyonrails.org/v4.0/getting_started

This code adds a 'Destroy Comment' link to the `_comment.html.erb` partial. When clicked, it sends a DELETE request to the appropriate controller action, including the necessary parameters to identify the comment to be destroyed. It also includes a confirmation dialog.

```erb
<p>  <strong>Commenter:</strong>  <%= comment.commenter %></p> <p>  <strong>Comment:</strong>  <%= comment.body %></p> <p>  <%= link_to 'Destroy Comment', [comment.post, comment],        method: :delete,        data: { confirm: 'Are you sure?' } %>  </p>
```

--------------------------------

### Find Each Starting from a Specific ID in Ruby on Rails

Source: https://guides.rubyonrails.org/v7.1/active_record_querying

This example shows how to use the `find_each` method with the `:start` option to begin fetching records from a specified primary key ID. This is beneficial for resuming interrupted processes or targeting a subset of records based on their ID. Here, it starts processing customers from ID 2000.

```ruby
Customer.find_each(start: 2000) do |customer|
  NewsMailer.weekly(customer).deliver_now
end
```

--------------------------------

### Active Record Data Access Examples in Ruby

Source: https://guides.rubyonrails.org/v5.1/active_record_basics

Demonstrates various methods for reading data from a database using Active Record in Ruby. Includes fetching all records, the first record, specific records by attribute, and filtered/ordered records. No external dependencies beyond Active Record itself are required.

```Ruby
```ruby
# return a collection with all users
users = User.all

# return the first user
user = User.first

# return the first user named David
david = User.find_by(name: 'David')

# find all users named David who are Code Artists and sort by created_at in reverse chronological order
users = User.where(name: 'David', occupation: 'Code Artist').order(created_at: :desc)
```
```

--------------------------------

### Creating Rails Controllers for HTTP Request Handling

Source: https://context7.com/context7/guides_rubyonrails/llms.txt

This snippet shows how to create controllers in Ruby on Rails to handle HTTP requests and render responses. It includes examples of setting up before actions, defining actions for common CRUD operations (index, show, new, create, edit, update, destroy), using strong parameters for security, and handling different response formats (HTML and JSON). It also includes an example of an API-only controller.

```ruby
# app/controllers/products_controller.rb
class ProductsController < ApplicationController
  before_action :set_product, only: [:show, :edit, :update, :destroy]
  before_action :authenticate_user!, except: [:index, :show]

  # GET /products
  def index
    @products = Product.all.order(created_at: :desc)

    respond_to do |format|
      format.html  # Renders app/views/products/index.html.erb
      format.json { render json: @products }
    end
  end

  # GET /products/1
  def show
    respond_to do |format|
      format.html
      format.json { render json: @product }
    end
  end

  # GET /products/new
  def new
    @product = Product.new
  end

  # POST /products
  def create
    @product = Product.new(product_params)

    if @product.save
      redirect_to @product, notice: "Product was successfully created."
    else
      render :new, status: :unprocessable_entity
    end
  end

  # GET /products/1/edit
  def edit
  end

  # PATCH/PUT /products/1
  def update
    if @product.update(product_params)
      redirect_to @product, notice: "Product was successfully updated."
    else
      render :edit, status: :unprocessable_entity
    end
  end

  # DELETE /products/1
  def destroy
    @product.destroy
    redirect_to products_url, notice: "Product was successfully destroyed."
  end

  private

  def set_product
    @product = Product.find(params[:id])
  rescue ActiveRecord::RecordNotFound
    redirect_to products_path, alert: "Product not found"
  end

  # Strong parameters for security
  def product_params
    params.require(:product).permit(:name, :description, :price, :stock_quantity)
  end

  def authenticate_user!
    redirect_to login_path, alert: "Please sign in" unless current_user
  end
end

# API-only controller
class Api::V1::ProductsController < ApplicationController
  skip_before_action :verify_authenticity_token

  def index
    @products = Product.all
    render json: @products, status: :ok
  end

  def create
    @product = Product.new(product_params)

    if @product.save
      render json: @product, status: :created, location: api_v1_product_url(@product)
    else
      render json: { errors: @product.errors }, status: :unprocessable_entity
    end
  end
end

```

--------------------------------

### Set Dependent Destroy for Article Comments in Rails Model

Source: https://guides.rubyonrails.org/v4.1/getting_started

This Ruby code modifies the `Article` model to ensure that all associated comments are automatically deleted when an article is deleted. This is achieved by adding `dependent: :destroy` to the `has_many` association for comments, preventing orphaned records in the database.

```ruby
class Article < ActiveRecord::Base
  has_many :comments, dependent: :destroy
  validates :title, presence: true,
                    length: { minimum: 5 }
end
```

--------------------------------

### Counting Total Validation Errors in Ruby on Rails

Source: https://guides.rubyonrails.org/v3.2/active_record_validations_callbacks

This example demonstrates how to get the total count of validation error messages for a Rails model object using the `errors.size` method. It shows that `errors.size` returns the number of messages in the `errors` collection. A valid object will have an `errors.size` of 0.

```Ruby
class Person < ActiveRecord::Base
  validates :name, :presence => true, :length => { :minimum => 3 }
end

person = Person.new
person.valid?
# => false
person.errors.size
# => 2

person = Person.new(:name => "Andrea", :email => "andrea@example.com")
person.valid?
# => true
person.errors.size
# => 0
```

--------------------------------

### Ruby Integration Test: Making GET Requests

Source: https://guides.rubyonrails.org/4_2_release_notes

Provides an example of how to perform a GET request within an integration test in Rails. It shows the correct usage of the `get` helper, emphasizing the requirement for a leading slash in the path.

```ruby
test "list all posts" do
  get "/posts"
  assert_response :success
end
```

--------------------------------

### Generate Kindle Guides with Rake

Source: https://guides.rubyonrails.org/v7.0/ruby_on_rails_guides_guidelines

Command to generate the Ruby on Rails Guides in a format suitable for Kindle devices using the Rake build tool.

```bash
$ bundle exec rake guides:generate:kindle
```

--------------------------------

### Example Action Mailbox Processing with Callbacks and Action Mailer

Source: https://guides.rubyonrails.org/v7.2/action_mailbox_basics

An example Action Mailbox demonstrating the use of `before_processing` callback to check user project availability. It processes email subjects and decoded bodies to create records or sends Action Mailer emails to prompt project selection.

```ruby
# Example: Mailbox to process forwards
class ForwardsMailbox < ApplicationMailbox
  before_processing :ensure_user_has_projects

  def process
    record_forward
  end

  private

  def ensure_user_has_projects
    user = User.find_by(email: mail.from)
    if user.projects.empty?
      bounced_with :no_projects_for_forwarder
      mail(to: user.email, subject: 'Please choose a project').deliver_later
    end
  end

  def record_forward
    user = User.find_by(email: mail.from)
    user.projects.create!(
      subject: mail.subject,
      body: mail.decoded
    )
  end
end

```

--------------------------------

### Rack::Server Default Options

Source: https://guides.rubyonrails.org/v5.2/initialization

Defines the default configuration options for the Rack server, including port, host, environment, daemonization, caching, PID path, and restart command. It fetches port and host from environment variables if available.

```ruby
def default_options
  super.merge(
    Port: ENV.fetch("PORT", 3000).to_i,
    Host: ENV.fetch("HOST", "localhost").dup,
    DoNotReverseLookup: true,
    environment: (ENV["RAILS_ENV"] || ENV["RACK_ENV"] || "development").dup,
    daemonize: false,
    caching: nil,
    pid: Options::DEFAULT_PID_PATH,
    restart_cmd: restart_command
  )
end
```

--------------------------------

### Example Rails Middleware Stack Output

Source: https://guides.rubyonrails.org/v5.1/rails_on_rack

This is an example output from the `bin/rails middleware` command for a standard Rails application. It lists various Rack middlewares that are configured by default, such as `Rack::Sendfile`, `ActionDispatch::Static`, and `Rails::Rack::Logger`, culminating in `run MyApp.application.routes`. This provides insight into the request processing pipeline.

```shell
use Rack::Sendfile
use ActionDispatch::Static
use ActionDispatch::Executor
use ActiveSupport::Cache::Strategy::LocalCache::Middleware
use Rack::Runtime
use Rack::MethodOverride
use ActionDispatch::RequestId
use ActionDispatch::RemoteIp
use Sprockets::Rails::QuietAssets
use Rails::Rack::Logger
use ActionDispatch::ShowExceptions
use WebConsole::Middleware
use ActionDispatch::DebugExceptions
use ActionDispatch::Reloader
use ActionDispatch::Callbacks
use ActiveRecord::Migration::CheckPending
use ActionDispatch::Cookies
use ActionDispatch::Session::CookieStore
use ActionDispatch::Flash
use Rack::Head
use Rack::ConditionalGet
use Rack::ETag
run MyApp.application.routes
```

--------------------------------

### Install Webpacker in Rails 6

Source: https://guides.rubyonrails.org/v7.1/upgrading_ruby_on_rails

Provides instructions for installing Webpacker, the default JavaScript compiler in Rails 6, for applications upgrading from Rails 5.2. It includes adding the `webpacker` gem to the Gemfile and running the installation generator.

```ruby
gem "webpacker"


```

```bash
$ bin/rails webpacker:install


```

--------------------------------

### HTML: Example HTTP header response

Source: https://guides.rubyonrails.org/v6.0/layouts_and_rendering

This is an example of an HTTP header response, likely generated by a Rails application. It includes status codes, connection information, date, content type, and other relevant headers.

```http
HTTP/1.1 400 Bad Request
Connection: close
Date: Sun, 24 Jan 2010 12:15:53 GMT
Transfer-Encoding: chunked
Content-Type: text/html; charset=utf-8
X-Runtime: 0.013483
Set-Cookie: _blog_session=...snip...; path=/; HttpOnly
Cache-Control: no-cache
```

--------------------------------

### Ruby on Rails: Enqueuing and Executing Active Jobs

Source: https://context7.com/context7/guides_rubyonrails/llms.txt

Provides examples of how to enqueue Active Jobs for background processing, including options for immediate execution, delayed execution, and scheduling at a specific time. Also covers overriding queues and passing multiple arguments.

```ruby
# Enqueue jobs
GuestsCleanupJob.perform_later(guest)
# Executes when queue is free

GuestsCleanupJob.set(wait: 1.week).perform_later(guest)
# Executes 1 week from now

GuestsCleanupJob.set(wait_until: Date.tomorrow.noon).perform_later(guest)
# Executes at specific time

ProcessOrderJob.set(queue: :high_priority).perform_later(order)
# Override queue

# Passing multiple arguments
GuestsCleanupJob.perform_later(guest1, guest2, filter: "inactive")

# Execute immediately (not recommended for production)
GuestsCleanupJob.perform_now(guest)
```

```ruby
# Bulk enqueuing (Rails 7+)
ActiveJob.perform_all_later(
  GuestsCleanupJob.new(guest1),
  GuestsCleanupJob.new(guest2),
  ProcessOrderJob.new(order)
)
```

--------------------------------

### Rails Server Command

Source: https://guides.rubyonrails.org/v3.2/command_line

Shows the command to start the Rails development server. This command is used to run the application locally for testing and development purposes. It typically outputs information about the server booting process.

```bash
$ rails server
#=> Booting WEBrick...
```

--------------------------------

### Create reusable post form partial (ERB)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This ERB code defines a reusable form partial for post creation and editing. It contains the form structure, error handling, and input fields for 'title' and 'text', abstracting away the common elements of the new and edit forms. The form_for helper is used without explicit URL or method, allowing it to adapt based on the context it's rendered in.

```erb
<%= form_for @post do |f| %>
  <% if @post.errors.any? %>
  <div id="error_explanation">
    <h2><%= pluralize(@post.errors.count, "error") %> prohibited
      this post from being saved:</h2>
    <ul>
      <% @post.errors.full_messages.each do |msg| %>
        <li><%= msg %></li>
      <% end %>
    </ul>
  </div>
  <% end %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
```

--------------------------------

### Run Specific Component Tests in Rails

Source: https://guides.rubyonrails.org/v3.1/contributing_to_ruby_on_rails

This demonstrates how to run tests for a specific component of the Ruby on Rails framework, such as Action Pack. It involves navigating into the component's directory and then executing the test suite using Bundler and Rake.

```bash
cd actionpack
bundle exec rake test
```

--------------------------------

### Ruby on Rails: has_one :through Migration Example

Source: https://guides.rubyonrails.org/v6.1/association_basics

Provides an example of database migrations for setting up tables required for a has_one :through association. This includes creating tables for the supplier, account, and account_history models, establishing the necessary foreign key relationships.

```ruby
class CreateAccountHistories < ActiveRecord::Migration[6.0]
  def change
    create_table :suppliers do |t|
      t.string :name
      t.timestamps
    end

    create_table :accounts do |t|
      t.belongs_to :supplier
      t.string :account_number
      t.timestamps
    end

    create_table :account_histories do |t|
      t.belongs_to :account
      t.integer :credit_rating
      t.timestamps
    end
  end
end

```

--------------------------------

### Manifest File Example (JSON)

Source: https://guides.rubyonrails.org/asset_pipeline

An example of a .manifest.json file generated during Rails asset precompilation. This file maps original asset filenames to their fingerprinted versions, crucial for cache invalidation and runtime asset resolution.

```json
{
  "application.css": "application-6d58c9e6e3b5d4a7c9a8e3.css",
  "application.js": "application-2d4b9f6c5a7c8e2b8d9e6.js",
  "logo.png": "logo-f3e8c9b2a6e5d4c8.png",
  "favicon.ico": "favicon-d6c8e5a9f3b2c7.ico"
}
```

--------------------------------

### Install Ruby on Rails 3

Source: https://guides.rubyonrails.org/v3.0/3_0_release_notes

Command to install Ruby on Rails version 3 using the RubyGems package manager. It may require sudo privileges depending on your system setup.

```shell
# Use sudo if your setup requires it
gem install rails
```

--------------------------------

### Using Setup Callback by Method Name in Rails

Source: https://guides.rubyonrails.org/v4.2/testing

This code example shows how to define a `setup` callback in a Rails test class by specifying a method name as a symbol. This method (`initialize_article`) is executed before each test, ensuring the necessary instance variables are set up. The `teardown` method is also demonstrated for cleanup.

```ruby
require 'test_helper'

class ArticlesControllerTest < ActionController::TestCase
  # called before every single test
  setup :initialize_article

  # called after every single test
  def teardown
    @article = nil
  end

  test "should show article" do
    get :show, id: @article.id
    assert_response :success
  end

  test "should update article" do
    patch :update, id: @article.id, article: {}
    assert_redirected_to article_path(assigns(:article))
  end

  test "should destroy article" do
    assert_difference('Article.count', -1) do
      delete :destroy, id: @article.id
    end
    assert_redirected_to articles_path
  end

  private

  def initialize_article
    @article = articles(:one)
  end
end
```

--------------------------------

### Print Autoload Paths using Rails Runner (Ruby)

Source: https://guides.rubyonrails.org/upgrading_ruby_on_rails

A command-line example using `rails runner` to inspect the currently configured autoload paths in a Rails application. This is useful for verifying whether directories like `lib` are included in the autoloaders.

```ruby
# Print autoload paths.
$ bin/rails runner 'pp Rails.autoloaders.main.dirs'
```

--------------------------------

### Example Application Template Logic

Source: https://guides.rubyonrails.org/v3.1/generators

An example of a Ruby on Rails application template that conditionally installs gems like `rspec-rails`, `cucumber-rails`, and `devise`. It prompts the user for input and generates necessary files.

```ruby
gem("rspec-rails", :group => "test")
gem("cucumber-rails", :group => "test")
if yes?("Would you like to install Devise?")
  gem("devise")
  generate("devise:install")
  model_name = ask("What would you like the user model to be called? [user]")
  model_name = "user" if model_name.blank?
  generate("devise", model_name)
end
```

--------------------------------

### Start a Rails Development Server with `rails server`

Source: https://guides.rubyonrails.org/v3.0/command_line

The `rails server` command starts a development web server (WEBrick by default) for your Rails application. This allows you to view your application in a web browser. The server typically runs on port 3000. Use Ctrl-C to shut it down.

```bash
$ cd commandsapp
$ rails server
=> Booting WEBrick
=> Rails 3.0.0 application starting in development on http://0.0.0.0:3000
=> Call with -d to detach
=> Ctrl-C to shutdown server
[2010-04-18 03:20:33] INFO  WEBrick 1.3.1
[2010-04-18 03:20:33] INFO  ruby 1.8.7 (2010-01-10) [x86_64-linux]
[2010-04-18 03:20:33] INFO  WEBrick::HTTPServer#start: pid=26086 port=3000
```

--------------------------------

### Start a Rails Development Server

Source: https://guides.rubyonrails.org/v3.1/command_line

The `rails server` command launches a development web server (WEBrick by default) to run your Rails application. It allows access through a web browser on a specified port. Options include changing the environment (`-e`) or port (`-p`).

```bash
$ cd commandsapp
$ rails server
=> Booting WEBrick
=> Rails 3.1.0 application starting in development on http://0.0.0.0:3000
=> Call with -d to detach
=> Ctrl-C to shutdown server
[2010-04-18 03:20:33] INFO  WEBrick 1.3.1
[2010-04-18 03:20:33] INFO  ruby 1.8.7 (2010-01-10) [x86_64-linux]
[2010-04-18 03:20:33] INFO  WEBrick::HTTPServer#start: pid=26086 port=3000
```

```bash
$ rails server -e production -p 4000
```

```bash
$ rails s
```

--------------------------------

### SQL: Example of Limit and Offset

Source: https://guides.rubyonrails.org/v5.1/active_record_querying

These show the SQL generated by the Ruby code for limiting and offsetting records.

```sql
SELECT * FROM clients LIMIT 5
SELECT * FROM clients LIMIT 5 OFFSET 30
```

--------------------------------

### Install MySQL and PostgreSQL Gems and Libraries (Ubuntu)

Source: https://guides.rubyonrails.org/v3.0/contributing_to_ruby_on_rails

Installs the MySQL and PostgreSQL servers, client libraries, and development files required for Ruby on Rails testing on Ubuntu systems.

```bash
sudo apt-get install mysql-server libmysqlclient15-dev
sudo apt-get install postgresql postgresql-client postgresql-contrib libpq-dev
```

--------------------------------

### Define 'update' action in Posts Controller (Ruby on Rails)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This Ruby code defines the 'update' action in the Posts controller. It finds the post by ID, attempts to update it with permitted parameters (:title, :text), and redirects to the post's page on success or re-renders the 'edit' form on failure. It uses Rails' strong parameters to prevent mass assignment vulnerabilities.

```ruby
def update
  @post = Post.find(params[:id])
  if @post.update(params[:post].permit(:title, :text))
    redirect_to @post
  else
    render 'edit'
  end
end
```

--------------------------------

### Generate New Rails Application

Source: https://guides.rubyonrails.org/v6.1/command_line

Creates a new Ruby on Rails application with a specified name. This is the foundational command for starting any new Rails project, setting up the directory structure and initial configuration.

```bash
rails new app_name
```

--------------------------------

### SQL: Example IN Statement from Subset Condition

Source: https://guides.rubyonrails.org/v4.1/active_record_querying

This is the SQL generated by the Ruby subset condition example, demonstrating the `IN` clause for checking against a list of values.

```sql
SELECT * FROM clients WHERE (clients.orders_count IN (1,3,5))
```

--------------------------------

### Install Memcached (Shell)

Source: https://guides.rubyonrails.org/v5.1/development_dependencies_install

Installs Memcached, a distributed memory object caching system, required for tests that use memcached. Provides commands for OS X, Ubuntu, Fedora/CentOS, Arch Linux, and FreeBSD.

```shell
# OS X
$ brew install memcached

# Ubuntu
$ sudo apt-get install memcached

# Fedora/CentOS
$ sudo yum install memcached

# Arch Linux
$ sudo pacman -S memcached

# FreeBSD
# pkg install memcached
# Alternatively, compile the databases/memcached port.
```

--------------------------------

### SQL: Range Condition Example

Source: https://guides.rubyonrails.org/v6.1/active_record_querying

Provides an example of the SQL query generated for range conditions in Active Record, demonstrating the use of the `BETWEEN` operator.

```sql
SELECT * FROM books WHERE (books.created_at BETWEEN '2008-12-21 00:00:00' AND '2008-12-22 00:00:00')
```

--------------------------------

### Ruby on Rails: Link Back to Articles Index

Source: https://guides.rubyonrails.org/v5.1/getting_started

Provides a link to navigate back to the main articles index page from the 'new article' form or a 'show' article view. It uses the `link_to` helper and the `articles_path`, which represents the path to the index action for the articles resource.

```erb
<%= link_to 'Back', articles_path %>
```

--------------------------------

### Rails Route Definitions

Source: https://guides.rubyonrails.org/v4.1/getting_started

This output from the `rake routes` command displays the defined routes for a Rails application, specifically showing the patterns, HTTP verbs, and corresponding controller#action pairs. It is crucial for understanding how route helpers like `articles_path` map to specific URL patterns and actions, which is used to configure form submissions.

```bash
$ bin/rake routes
       Prefix Verb      URI Pattern                  Controller#Action
     articles GET       /articles(.:format)          articles#index
              POST      /articles(.:format)          articles#create
  new_article GET       /articles/new(.:format)      articles#new
 edit_article GET       /articles/:id/edit(.:format) articles#edit
      article GET       /articles/:id(.:format)      articles#show
              PATCH     /articles/:id(.:format)      articles#update
              PUT       /articles/:id(.:format)      articles#update
              DELETE    /articles/:id(.:format)      articles#destroy
        root GET       /                            welcome#index
```

--------------------------------

### Add 'Edit' link to posts show view (ERB)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This ERB snippet demonstrates adding an 'Edit' link to the posts show view. It appends a link using link_to with edit_post_path(@post), providing easy access to edit the currently displayed post. This improves the user experience by offering direct editing capabilities from the show page.

```erb
... 
<%= link_to 'Back', posts_path %>
| <%= link_to 'Edit', edit_post_path(@post) %>
```

--------------------------------

### Action Controller: start_processing Event Example

Source: https://guides.rubyonrails.org/v7.0/active_support_instrumentation

This snippet demonstrates the payload for the `start_processing.action_controller` hook, which is triggered at the beginning of an Action Controller action. It includes details about the controller, action, parameters, headers, format, method, and path of the request.

```ruby
{
  controller: "PostsController",
  action: "new",
  params: { "action" => "new", "controller" => "posts" },
  headers: #<ActionDispatch::Http::Headers:0x0055a67a519b88>,
  format: :html,
  method: "GET",
  path: "/posts/new"
}

```

--------------------------------

### Running Rails Tests Command

Source: https://guides.rubyonrails.org/active_model_basics

Illustrates the command to run tests in a Rails application and provides an example of the output, showing the number of runs, assertions, and any failures or errors.

```bash
$ bin/rails test

Run options: --seed 14596

# Running:

......

Finished in 0.024899s, 240.9735 runs/s, 1204.8677 assertions/s.

6 runs, 30 assertions, 0 failures, 0 errors, 0 skips
```

--------------------------------

### Rails Controller Test Setup and Teardown

Source: https://guides.rubyonrails.org/v3.1/testing

Demonstrates using `setup` and `teardown` callbacks in a Rails controller test to initialize and clean up an instance variable before and after each test. This ensures tests are isolated and have a consistent starting state.

```ruby
require 'test_helper'
class PostsControllerTest < ActionController::TestCase
  # called before every single test
  def setup
    @post = posts(:one)
  end

  # called after every single test
  def teardown
    # as we are re-initializing @post before every test
    # setting it to nil here is not essential but I hope
    # you understand how you can use the teardown method
    @post = nil
  end

  test "should show post" do
    get :show, :id => @post.id
    assert_response :success
  end

  test "should destroy post" do
    assert_difference('Post.count', -1) do
      delete :destroy, :id => @post.id
    end
    assert_redirected_to posts_path
  end
end
```

--------------------------------

### Define create action in ArticlesController

Source: https://guides.rubyonrails.org/v4.2/getting_started

Adds a 'create' action to the ArticlesController, intended to handle article creation. This is a basic structure before parameter processing is implemented. It's part of the ApplicationController inheritance.

```ruby
class ArticlesController < ApplicationController
  def new
  end

  def create
  end
end
```

--------------------------------

### Define Rich Text Field in Model (Ruby)

Source: https://guides.rubyonrails.org/getting_started

This Ruby code defines a Product model in Rails and uses the `has_rich_text` macro to associate a rich text field named 'description' with the model. It also includes a presence validation for the 'name' attribute. This setup enables the product to store and manage rich text content.

```ruby
class Product < ApplicationRecord
  has_rich_text :description
  validates :name, presence: true
end
```

--------------------------------

### Run Component or Specific Tests

Source: https://guides.rubyonrails.org/v4.0/development_dependencies_install

Demonstrates how to run tests for a specific component (e.g., Action Pack) by navigating to its directory, or how to run tests within a particular directory using the TEST_DIR environment variable. It also shows how to execute a single test file.

```bash
$ cd actionpack
$ bundle exec rake test
```

```bash
$ cd railties
$ TEST_DIR=generators bundle exec rake test
```

```bash
$ cd actionpack
$ bundle exec ruby -Itest test/template/form_helper_test.rb
```

--------------------------------

### Rails Database URL Example (Ruby)

Source: https://guides.rubyonrails.org/v4.1/configuring

Demonstrates how to retrieve a database connection URL from an environment variable in Ruby. This URL typically includes the adapter, host, database name, and connection pool.

```ruby
puts ENV['DATABASE_URL']
# Example Output: postgresql://localhost/blog_development?pool=5
```

--------------------------------

### Rails Secrets Configuration: secrets.yml Example

Source: https://guides.rubyonrails.org/upgrading_ruby_on_rails

Provides an example structure for the `config/secrets.yml` file, used for managing application secrets across different environments. It shows how to define `secret_key_base` for development, test, and production, with production leveraging environment variables.

```yaml
development:
  secret_key_base:

test:
  secret_key_base:

production:
  secret_key_base: <%= ENV["SECRET_KEY_BASE"] %>
```

--------------------------------

### Deeply-Nested Resources Example

Source: https://guides.rubyonrails.org/v6.1/routing

Demonstrates how deeply nested resources are defined and the resulting URL structure.

```APIDOC
## Deeply-Nested Resources

### Description
This section illustrates the definition and path generation for deeply nested resources in Rails.

### Method
N/A (DSL definition)

### Endpoint
N/A (DSL definition)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

## Resource Nesting Example (DSL)
```ruby
resources :publishers do
  resources :magazines do
    resources :photos
  end
end
```

## Resulting Path Example
```
/publishers/:publisher_id/magazines/:magazine_id/photos/:id
```

## Route Helper Example
`publisher_magazine_photo_url`
```

--------------------------------

### Link to New Article Form in Rails View

Source: https://guides.rubyonrails.org/v4.1/getting_started

Adds a link to the 'new article' form within the articles index view. It utilizes the 'link_to' helper with a route helper 'new_article_path' to generate the correct URL for creating a new article. This link is placed above the article listing table.

```html
<%= link_to 'New article', new_article_path %>
```

--------------------------------

### Configuring the Rails Application - Ruby

Source: https://guides.rubyonrails.org/v5.2/initialization

The `app` method defines how the Rails application is constructed. It prioritizes building the app from a string if specified in options, otherwise it calls `build_app_and_options_from_config` to load the application and its options from the configuration file.

```ruby
def app
  @app ||= options[:builder] ? build_app_from_string : build_app_and_options_from_config
end
```

--------------------------------

### SQL: Example BETWEEN Statement from Range Condition

Source: https://guides.rubyonrails.org/v4.1/active_record_querying

This is the SQL generated by the Ruby range condition example, demonstrating the `BETWEEN` clause for date filtering.

```sql
SELECT * FROM clients WHERE (clients.created_at BETWEEN '2008-12-21 00:00:00' AND '2008-12-22 00:00:00')
```

--------------------------------

### Start Rails Development Server (Windows)

Source: https://guides.rubyonrails.org/v5.2/getting_started

On Windows, you need to explicitly pass the Rails script to the Ruby interpreter to start the development server. Navigate to your application's directory first. The server will be accessible at http://localhost:3000. Stop the server by pressing Ctrl+C.

```bash
ruby bin\rails server
```

--------------------------------

### Ruby: Example Code with Output

Source: https://guides.rubyonrails.org/v3.1/api_documentation_guidelines

Illustrates how to present example code snippets in documentation, including the expected output. This format is used for methods that return values, with the output clearly aligned and introduced by '# => '.

```ruby
# Converts a collection of elements into a formatted string by calling
# <tt>to_s</tt> on all elements and joining them.
#
#   Blog.all.to_formatted_s # => "First PostSecond PostThird Post"
```

```ruby
# ==== Examples
#
#   Person.exists?(5)
#   Person.exists?('5')
#   Person.exists?(:name => "David")
#   Person.exists?(['name LIKE ?', "%#{query}%"])
```

```ruby
# For checking if a fixnum is even or odd.
#
#   1.even? # => false
#   1.odd?  # => true
#   2.even? # => true
#   2.odd?  # => false
```

```ruby
#   label(:post, :title)
#   # => <label for="post_title">Title</label>
#
#   label(:post, :title, "A short title")
#   # => <label for="post_title">A short title</label>
#
#   label(:post, :title, "A short title", :class => "title_label")
#   # => <label for="post_title" class="title_label">A short title</label>
```

```ruby
#   polymorphic_url(record)  # same as comment_url(record)
```

--------------------------------

### ERB Template Example with Loop and Output

Source: https://guides.rubyonrails.org/v4.2/action_view_overview

Demonstrates how to use ERB (Embedded Ruby) templates to embed Ruby code within HTML. It shows the use of <% %> for executing Ruby code and <%= %> for outputting values, including an example of iterating over a collection.

```erb
<h1>Names of all the people</h1>
<% @people.each do |person| %>
  
Name: <%= person.name %><br>
<% end %>

```

--------------------------------

### Rails Layout: Basic Application Layout Example

Source: https://guides.rubyonrails.org/action_view_overview

An example of a basic `application.html.erb` layout file in Ruby on Rails. It includes essential elements like head, navigation, CSRF meta tags, stylesheets, JavaScript imports, and a footer, with a `yield` statement to render the main view content.

```erb
<!DOCTYPE html>
<html>
<head>
  <title><%= "Your Rails App" %></title>
  <%= csrf_meta_tags %>
  <%= csp_meta_tag %>
  <%= stylesheet_link_tag "application", "data-turbo-track": "reload" %>
  <%= javascript_importmap_tags %>
</head>
<body>

<nav>
  <ul>
    <li><%= link_to "Home", root_path %></li>
    <li><%= link_to "Products", products_path %></li>
    <!-- Additional navigation links here -->
  </ul>
</nav>

<%= yield %>

<footer>
  <p>&copy; <%= Date.current.year %> Your Company</p>
</footer>


```

--------------------------------

### Clone Ruby on Rails Repository using Git

Source: https://guides.rubyonrails.org/v4.0/development_dependencies_install

This command clones the official Ruby on Rails repository from GitHub to your local machine. It requires Git to be installed on your system. After cloning, you navigate into the created 'rails' directory.

```bash
$ git clone git://github.com/rails/rails.git
$ cd rails
```

--------------------------------

### Main Rails Script Entry Point (Ruby)

Source: https://guides.rubyonrails.org/v3.2/initialization

This Ruby file, `script/rails`, serves as the main entry point for the Rails command-line interface. It defines the `APP_PATH` constant, which points to the application's configuration, and then loads the `config/boot.rb` file to initialize Bundler and the Rails environment.

```ruby
APP_PATH = File.expand_path('../../config/application', __FILE__)
require File.expand_path('../../config/boot', __FILE__)
require 'rails/commands'
```

--------------------------------

### Rails Test Runner Command Examples

Source: https://guides.rubyonrails.org/testing

Demonstrates how to execute tests using the Rails test runner. This includes commands for running all tests, a specific test file, and a particular test method using the `-n` or `--name` flag.

```bash
$ bin/rails test test/models/article_test.rb
Running 1 tests in a single process (parallelization threshold is 50)
Run options: --seed 1559

# Running:

..

Finished in 0.027034s, 73.9810 runs/s, 110.9715 assertions/s.

2 runs, 3 assertions, 0 failures, 0 errors, 0 skips

```

```bash
$ bin/rails test test/models/article_test.rb -n test_the_truth
Running 1 tests in a single process (parallelization threshold is 50)
Run options: -n test_the_truth --seed 43583


```

--------------------------------

### Add 'Edit' link to posts index view (ERB)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This ERB snippet shows how to add an 'Edit' link next to each post in the index view. It uses the link_to helper with the 'edit_post_path' route, passing the individual post object to generate the correct URL for editing that specific post. This enhances navigation for updating records.

```erb
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th></th>
    <th></th>
  </tr>
<% @posts.each do |post| %>
  <tr>
    <td><%= post.title %></td>
    <td><%= post.text %></td>
    <td><%= link_to 'Show', post %></td>
    <td><%= link_to 'Edit', edit_post_path(post) %></td>
  </tr>
<% end %>
</table>
```

--------------------------------

### Configure Dependent Destroy Association in Rails Model

Source: https://guides.rubyonrails.org/v4.0/getting_started

This Ruby code modifies the `Post` model to ensure that all associated comments are automatically deleted when a post is deleted. This is achieved by using the `dependent: :destroy` option within the `has_many` association, preventing orphaned comment records in the database.

```ruby
class Post < ActiveRecord::Base
  has_many :comments, dependent: :destroy
  validates :title, presence: true,
                    length: { minimum: 5 }
  [...]
end
```

--------------------------------

### Action Mailer Example Configuration

Source: https://guides.rubyonrails.org/v2.3/action_mailer_basics

This snippet demonstrates a general configuration for Action Mailer, setting the delivery method to sendmail and configuring its associated settings. It also enables delivery performances and error raising, and sets a default character set.

```ruby
ActionMailer::Base.delivery_method = :sendmail
ActionMailer::Base.sendmail_settings = {
  :location => '/usr/sbin/sendmail',
  :arguments => '-i -t'
}
ActionMailer::Base.perform_deliveries = true
ActionMailer::Base.raise_delivery_errors = true
ActionMailer::Base.default_charset = "iso-8859-1"
```

--------------------------------

### Ruby on Rails Mailer Fixture Content Example

Source: https://guides.rubyonrails.org/testing

This is an example of a mailer fixture file content for the 'invite' action in Ruby on Rails. It represents the expected plain text body of the invitation email.

```text
Hi friend@example.com,

You have been invited.

Cheers!


```

--------------------------------

### SQL: Ordering Example

Source: https://guides.rubyonrails.org/v6.1/active_record_querying

Presents the SQL generated for ordering results, showing how `ORDER BY` clauses are constructed for single and multiple fields, with ASC/DESC specifiers.

```sql
SELECT * FROM customers ORDER BY orders_count ASC, created_at DESC
```

--------------------------------

### Default Server Options

Source: https://guides.rubyonrails.org/v4.0/initialization

The `default_options` method defines the default configuration settings for the Rack server. This includes the default environment, PID file path, host, port, access log settings, and the configuration file path.

```ruby
def default_options
  {
    :environment => ENV['RACK_ENV'] || "development",
    :pid         => nil,
    :Port        => 9292,
    :Host        => "0.0.0.0",
    :AccessLog   => [],
    :config      => "config.ru"
  }
end
```

--------------------------------

### PostgreSQL EXPLAIN Output with Eager Loading

Source: https://guides.rubyonrails.org/v7.1/active_record_querying

Example of `EXPLAIN` output with eager loading (`includes`) on PostgreSQL, showing the SQL queries and their respective query plans.

```sql
  Customer Load (0.3ms)  SELECT "customers".* FROM "customers" WHERE "customers"."id" = $1  [["id", 1]]
  Order Load (0.3ms)  SELECT "orders".* FROM "orders" WHERE "orders"."customer_id" = $1  [["customer_id", 1]]
=> EXPLAIN SELECT "customers".* FROM "customers" WHERE "customers"."id" = $1 [["id", 1]]
                                    QUERY PLAN
----------------------------------------------------------------------------------
 Index Scan using customers_pkey on customers  (cost=0.15..8.17 rows=1 width=164)
   Index Cond: (id = '1'::bigint)
(2 rows)

```

--------------------------------

### Rails Server Logs for Caching (Log Output)

Source: https://guides.rubyonrails.org/getting_started

This is an example of output from a Rails server log indicating cache read and write operations. The 'Read fragment' line shows Rails attempting to retrieve cached content, while 'Write fragment' indicates that the content was generated and stored in the cache. These logs help in understanding caching behavior and performance.

```log
Read fragment views/products/show:a5a585f985894cd27c8b3d49bb81de3a/products/1-20240918154439539125 (1.6ms)
Write fragment views/products/show:a5a585f985894cd27c8b3d49bb81de3a/products/1-20240918154439539125 (4.0ms)
```

--------------------------------

### Add Edit Link to Rails Show View

Source: https://guides.rubyonrails.org/getting_started

This ERB template for a Ruby on Rails 'show' view displays the product's name and provides links to navigate back to the product list or to edit the current product. The 'link_to' helper is used to generate these navigation links.

```erb
<h1><%= @product.name %></h1>

<%= link_to "Back", products_path %>
<%= link_to "Edit", edit_product_path(@product) %>
```

--------------------------------

### Database Migration for Creating Products Table

Source: https://guides.rubyonrails.org/getting_started

This Ruby code defines a database migration to create a 'products' table. It includes a 'name' column of type string and automatically adds 'created_at' and 'updated_at' timestamps. This script is part of Active Record's database management system.

```ruby
class CreateProducts < ActiveRecord::Migration[8.0]
  def change
    create_table :products do |t|
      t.string :name

      t.timestamps
    end
  end
end

```

--------------------------------

### Rails Performance Test Example

Source: https://guides.rubyonrails.org/v3.0/performance_testing

An example of performance tests for HomeController#dashboard and PostsController#create. It demonstrates using 'get' and 'post' methods within performance tests. Assumes application routes and models are defined.

```ruby
require 'test_helper'
require 'rails/performance_test_help'

class PostPerformanceTest < ActionController::PerformanceTest
  def setup
    # Application requires logged-in user
    login_as(:lifo)
  end

  def test_homepage
    get '/dashboard'
  end

  def test_creating_new_post
    post '/posts', :post => { :body => 'lifo is fooling you' }
  end
end
```

--------------------------------

### Start a Rails Development Server using './script/server'

Source: https://guides.rubyonrails.org/v2.3/command_line

The `server` command launches WEBrick, a bundled web server for Ruby, to host your Rails application. This allows you to view your application in a web browser. It starts the server on port 3000 by default. You can stop the server by pressing Ctrl-C.

```bash
$ cd myapp
$ ./script/server
=> Booting WEBrick...
=> Rails 2.2.0 application started on http://0.0.0.0:3000
=> Ctrl-C to shutdown server; call with --help for options
[2008-11-04 10:11:38] INFO  WEBrick 1.3.1
[2008-11-04 10:11:38] INFO  ruby 1.8.5 (2006-12-04) [i486-linux]
[2008-11-04 10:11:38] INFO  WEBrick::HTTPServer#start: pid=18994 port=3000
```

--------------------------------

### List Available bin/rails Tasks

Source: https://guides.rubyonrails.org/v5.1/command_line

The `bin/rails --help` command displays a list of all available tasks and their descriptions within the Rails application. This is useful for discovering and understanding the various commands at your disposal.

```bash
$ bin/rails --help
Usage: rails COMMAND [ARGS]
The most common rails commands are:
generate      Generate new code (short-cut alias: "g")
console      Start the Rails console (short-cut alias: "c")
server      Start the Rails server (short-cut alias: "s")
...
All commands can be run with -h (or --help) for more information.
In addition to those commands, there are:
about                 List versions of all Rails ...
assets:clean[keep]       Remove old compiled assets
assets:clobber           Remove compiled assets
assets:environment       Load asset compile environment
assets:precompile       Compile all the assets ...
...
db:fixtures:load         Loads fixtures into the ...
db:migrate              Migrate the database ...
db:migrate:status       Display status of migrations
db:rollback             Rolls the schema back to ...
db:schema:cache:clear           Clears a db/schema_cache.yml file
db:schema:cache:dump           Creates a db/schema_cache.yml file
db:schema:dump           Creates a db/schema.rb file ...
db:schema:load           Loads a schema.rb file ...
db:seed               Loads the seed data ...
db:structure:dump           Dumps the database structure ...
db:structure:load           Recreates the databases ...
db:version             Retrieves the current schema ...
...
restart               Restart app by touching ...
tmp:create             Creates tmp directories ...

```

--------------------------------

### Nested Layout Example (HTML ERB)

Source: https://guides.rubyonrails.org/v5.0/layouts_and_rendering

Provides an example of a nested layout structure in Rails. The `application.html.erb` serves as the base layout, and `news.html.erb` extends it with specific modifications for the NewsController, demonstrating how to override or add content blocks.

```erb
<!DOCTYPE html>
<html>
<head>
  <title><%= @page_title or "Page Title" %></title>
  <%= stylesheet_link_tag "layout" %>
  <style><%= yield :stylesheets %></style>
</head>
<body>
  <div id="top_menu">Top menu items here</div>
  <div id="menu">Menu items here</div>
  <div id="content">
    <%= content_for?( :content ) ? yield( :content ) : yield %>
  </div>
</body>
</html>
```

```erb
<% content_for :stylesheets do %>
  #top_menu {display: none}
  #right_menu {float: right; background-color: yellow; color: black}
<% end %>
<% content_for :content do %>
  <div id="right_menu">Right menu items here</div>
  <%= content_for?( :news_content ) ? yield( :news_content ) : yield %>
<% end %>
<%= render template: "layouts/application" %>
```

--------------------------------

### Install Development Dependencies on Fedora/CentOS

Source: https://guides.rubyonrails.org/v4.0/development_dependencies_install

Installs necessary libraries for Nokogiri (libxml2, libxslt) and SQLite3, including their development files, on Fedora or CentOS systems. These are required for running tests and building certain Ruby gems.

```bash
$ sudo yum install libxml2 libxml2-devel libxslt libxslt-devel
$ sudo yum install sqlite3 sqlite3-devel
```

--------------------------------

### Rails Controller: Complete ArticlesController with Destroy Action

Source: https://guides.rubyonrails.org/v4.2/getting_started

This Ruby code represents the full ArticlesController, including all CRUD actions (index, show, new, edit, create, update, destroy) and a private method for strong parameters. The 'destroy' action is included to handle article deletion.

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end
  def show
    @article = Article.find(params[:id])
  end
  def new
    @article = Article.new
  end
  def edit
    @article = Article.find(params[:id])
  end
  def create
    @article = Article.new(article_params)
    if @article.save
      redirect_to @article
    else
      render 'new'
    end
  end
  def update
    @article = Article.find(params[:id])
    if @article.update(article_params)
      redirect_to @article
    else
      render 'edit'
    end
  end
  def destroy
    @article = Article.find(params[:id])
    @article.destroy
    redirect_to articles_path
  end
  private
    def article_params
      params.require(:article).permit(:title, :text)
    end
end
```

--------------------------------

### Running Rails Notes with Custom Extensions

Source: https://guides.rubyonrails.org/v7.0/command_line

This is an example output of the `bin/rails notes` command after registering custom extensions. It shows annotations found in files with the newly registered extensions like `.sass` and `.scss`.

```shell
$ bin/rails notes
app/controllers/admin/users_controller.rb:
  * [ 20] [TODO] any other way to do this?
  * [132] [FIXME] high priority for next deploy

app/assets/stylesheets/application.css.sass:
  * [ 34] [TODO] Use pseudo element for this class

app/assets/stylesheets/application.css.scss:
  * [  1] [TODO] Split into multiple components

lib/school.rb:
  * [ 13] [OPTIMIZE] Refactor this code to make it faster
  * [ 17] [FIXME] 

spec/models/user_spec.rb:
  * [122] [TODO] Verify the user that has a subscription works

vendor/tools.rb:
  * [ 56] [TODO] Get rid of this dependency

```

--------------------------------

### Constrain Route to HTTP GET Verb in Ruby

Source: https://guides.rubyonrails.org/v3.0/routing

This Ruby code restricts a route to only respond to GET requests using the `:via` option. It also shows the shorthand `get` method for the same purpose.

```Ruby
match 'photos/show' => 'photos#show', :via => :get
```

```Ruby
get 'photos/show'
```

--------------------------------

### Action Cable Channel Subscription Example in Ruby

Source: https://guides.rubyonrails.org/action_cable_overview

Illustrates a basic channel setup where the `subscribed` callback is defined. This callback is invoked when a consumer successfully subscribes to the channel.

```ruby
class ChatChannel < ApplicationCable::Channel
  # Called when the consumer has successfully
  # become a subscriber to this channel.
  def subscribed
  end
end
```

--------------------------------

### Ruby: `belongs_to` Association with Options Example

Source: https://guides.rubyonrails.org/v2.3/association_basics

Provides an example of a `belongs_to` association declaration using multiple options like `:counter_cache` and `:conditions`. This showcases how to customize the default behavior of the association.

```ruby
class Order < ActiveRecord::Base
  belongs_to :customer, :counter_cache => true, :conditions => "active = 1"
end
```

--------------------------------

### Create Database (Ruby on Rails)

Source: https://guides.rubyonrails.org/v7.0/active_record_multiple_databases

Command to create databases. It can create all databases defined in the configuration or specific ones like 'animals' or 'primary'. Database users must be created manually.

```bash
rails db:create
rails db:create:animals
rails db:create:primary
```

--------------------------------

### Example Date Format Translations in YAML

Source: https://guides.rubyonrails.org/i18n

An example of how date format translations can be stored in a YAML file. It defines 'default', 'short', and 'long' formats for the 'en' locale.

```yaml
en:
  date:
    formats:
      default: "%Y-%m-%d"
      short: "%b %d"
      long: "%B %d, %Y"
```

--------------------------------

### Rails Server Class Rack::Server Inheritance in Ruby

Source: https://guides.rubyonrails.org/v4.2/rails_on_rack

Shows the inheritance structure of the `Rails::Server` class from `Rack::Server`, highlighting the `start` method override.

```ruby
class Server < ::Rack::Server
  def start
    ...
    super
  end
end
```

--------------------------------

### Ruby: Complete ArticlesController with Destroy Action

Source: https://guides.rubyonrails.org/v6.0/getting_started

This Ruby code represents the complete `ArticlesController` class, incorporating all CRUD actions including `index`, `show`, `new`, `edit`, `create`, `update`, and `destroy`. It also includes a private method `article_params` for strong parameters. The `destroy` action is implemented to handle the deletion of articles.

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def edit
    @article = Article.find(params[:id])
  end

  def create
    @article = Article.new(article_params)
    if @article.save
      redirect_to @article
    else
      render 'new'
    end
  end

  def update
    @article = Article.find(params[:id])
    if @article.update(article_params)
      redirect_to @article
    else
      render 'edit'
    end
  end

  def destroy
    @article = Article.find(params[:id])
    @article.destroy
    redirect_to articles_path
  end

  private

  def article_params
    params.require(:article).permit(:title, :text)
  end
end
```

--------------------------------

### Action Cable Broadcast Job Example

Source: https://guides.rubyonrails.org/v6.1/testing

This Ruby snippet shows an example of an Application Job in Rails that broadcasts messages using `ChatChannel.broadcast_to`. This is useful for sending real-time updates to connected clients subscribed to specific channels.

```ruby
# app/jobs/chat_relay_job.rb
class ChatRelayJob < ApplicationJob
  def perform_later(room, message)
    ChatChannel.broadcast_to room, text: message
  end
end
```

--------------------------------

### ERb Fixture Example with Ruby Code

Source: https://guides.rubyonrails.org/v3.0/testing

An example of an ERb fixture file that embeds Ruby code within templates. ERb allows dynamic data generation by executing Ruby code within <% %> tags and outputting results with <%= %>.

```erb
<% earth_size = 20 %>
mercury:
  size: <%= earth_size / 50 %>
  brightest_on: <%= 113.days.ago.to_s(:db) %>
venus:
  size: <%= earth_size / 2 %>
  brightest_on: <%= 67.days.ago.to_s(:db) %>
mars:
  size: <%= earth_size - 69 %>
  brightest_on: <%= 13.days.from_now.to_s(:db) %>
```

--------------------------------

### Build PostgreSQL Test Databases

Source: https://guides.rubyonrails.org/v4.0/development_dependencies_install

Navigates to the 'activerecord' directory and executes the 'bundle exec rake postgresql:build_databases' command to create the required test databases for PostgreSQL.

```bash
$ cd activerecord
$ bundle exec rake postgresql:build_databases
```

--------------------------------

### Basic Assertion Example

Source: https://guides.rubyonrails.org/testing

A fundamental example of an assertion within a Rails test. Assertions are used to check for expected results and determine if a test passes or fails.

```ruby
assert true
```

--------------------------------

### Rack Server Start Method

Source: https://guides.rubyonrails.org/v7.0/initialization

This Ruby code defines the `start` method within `Rack::Server`. It handles various server options such as warnings, load path adjustments, required libraries, debugging, PID file management, daemonization, and signal trapping before running the application.

```ruby
module Rack
  class Server
    def start &blk
      if options[:warn]
        $-w = true
      end

      if includes = options[:include]
        $LOAD_PATH.unshift(*includes)
      end

      if library = options[:require]
        require library
      end

      if options[:debug]
        $DEBUG = true
        require "pp"
        p options[:server]
        pp wrapped_app
        pp app
      end

      check_pid! if options[:pid]

      # Touch the wrapped app, so that the config.ru is loaded before
      # daemonization (i.e. before chdir, etc).
      handle_profiling(options[:heapfile], options[:profile_mode], options[:profile_file]) do
        wrapped_app
      end

      daemonize_app if options[:daemonize]

      write_pid if options[:pid]

      trap(:INT) do
        if server.respond_to?(:shutdown)
          server.shutdown
        else
          exit
        end
      end

      server.run wrapped_app, options, &blk
    end
  end
end

```

--------------------------------

### Switch Database Adapter in Rails Application

Source: https://guides.rubyonrails.org/command_line

Allows changing the primary database adapter for a Rails application. After running the command, it prompts for configuration file overwrites and requires a `bundle install` to install new gems. Uses `config/database.yml` for configuration.

```bash
$ rails db:system:change --to=postgresql
    conflict  config/database.yml
Overwrite config/database.yml? (enter "h" for help) [Ynaqdhm] Y
       force  config/database.yml
        gsub  Gemfile
        gsub  Gemfile
...

```

```bash
$ bundle install
...

```

--------------------------------

### Rails Server Class Inheriting from Rack::Server

Source: https://guides.rubyonrails.org/v6.1/rails_on_rack

Illustrates the `Rails::Server` class, which inherits from `Rack::Server`. It shows how the `start` method in `Rails::Server` ultimately calls the `start` method of its parent class, `Rack::Server`.

```ruby
class Server < ::Rack::Server
  def start
    # ...
    super
  end
end
```

--------------------------------

### Running Rails Commands (Ruby)

Source: https://guides.rubyonrails.org/v4.1/3_0_release_notes

Demonstrates the new way to run Rails commands using the `rails` command instead of direct script execution. This simplifies common tasks like accessing the console or generating scaffolds.

```shell
$ rails console
$ rails g scaffold post title:string
```

--------------------------------

### Run Action Text Database Migrations

Source: https://guides.rubyonrails.org/action_text_overview

Executes the database migrations generated during the Action Text installation to create tables for storing rich text content and attachments.

```bash
$ bin/rails db:migrate

```

--------------------------------

### Check Zeitwerk Autoloading Compatibility

Source: https://guides.rubyonrails.org/upgrading_ruby_on_rails

This command-line example demonstrates how to use the `zeitwerk:check` Rake task to verify if your project's structure is compatible with Zeitwerk's autoloading conventions. It provides feedback on whether autoloading is functioning correctly.

```bash
$ bin/rails zeitwerk:check
Hold on, I am eager loading the application.
All is good!

```

--------------------------------

### Install Webpacker in Rails 6

Source: https://guides.rubyonrails.org/upgrading_ruby_on_rails

Provides instructions for integrating Webpacker, the default JavaScript compiler in Rails 6, into an existing application. This involves adding the 'webpacker' gem to the Gemfile and running the installation generator.

```ruby
gem "webpacker"
```

```shell
$ bin/rails webpacker:install
```

--------------------------------

### Ruby on Rails: Model Testing with ActiveSupport::TestCase

Source: https://context7.com/context7/guides_rubyonrails/llms.txt

Shows how to write unit tests for models in Ruby on Rails using the `ActiveSupport::TestCase`. Includes examples of testing validations (e.g., ensuring a book is not saved without a title) and business logic (e.g., calculating a discount price).

```ruby
# test/models/book_test.rb
require "test_helper"

class BookTest < ActiveSupport::TestCase
  test "should not save book without title" do
    book = Book.new
    assert_not book.save, "Saved the book without a title"
  end

  test "should save valid book" do
    book = Book.new(title: "Rails Guide", author: "DHH", price: 29.99)
    assert book.save, "Failed to save valid book"
  end

  test "should calculate discount price" do
    book = books(:rails_guide)  # Uses fixture
    assert_equal 26.99, book.discount_price(0.1)
  end
end
```

--------------------------------

### Define 'new' Action in Rails Controller

Source: https://guides.rubyonrails.org/v4.2/getting_started

This Ruby code adds a 'new' action to the ArticlesController. This action will be invoked when a request is made to the '/articles/new' route and is responsible for preparing data for the new article view.

```ruby
class ArticlesController < ApplicationController
  def new
  end
end
```

--------------------------------

### Example Rails Secret Key Base

Source: https://guides.rubyonrails.org/security

This snippet shows an example of a `secret_key_base` value. In production environments, this key should be securely stored in `config/credentials.yml.enc` and kept confidential to maintain the security of encrypted cookies and other sensitive data.

```yaml
secret_key_base: 492f...

```

--------------------------------

### Default config.ru Content - Ruby

Source: https://guides.rubyonrails.org/v5.2/initialization

This is the standard content of a `config.ru` file used by Rack-based servers to initialize the application. It requires the Rails environment configuration and then specifies the main application constant to run.

```ruby
# This file is used by Rack-based servers to start the application.
require_relative 'config/environment'
run <%= app_const %>
```

--------------------------------

### Rails Server Start Method

Source: https://guides.rubyonrails.org/v3.2/initialization

The `start` method in `Rails::Server` initiates the server process. It prints startup information, sets up an interrupt handler for graceful shutdown (Ctrl+C), ensures necessary temporary directories exist, and then calls the parent `start` method.

```ruby
def start
  puts "=> Booting #{ActiveSupport::Inflector.demodulize(server)}"
  puts "=> Rails #{Rails.version} application starting in #{Rails.env} on http://#{options[:Host]}:#{options[:Port]}"
  puts "=> Call with -d to detach" unless options[:daemonize]
  trap(:INT) { exit }
  puts "=> Ctrl-C to shutdown server" unless options[:daemonize]
  #Create required tmp directories if not found
  %w(cache pids sessions sockets).each do |dir_to_make|
    FileUtils.mkdir_p(Rails.root.join('tmp', dir_to_make))
  end
  super
ensure
  # The '-h' option calls exit before @options is set.
  # If we call 'options' with it unset, we get double help banners.
  puts 'Exiting' unless @options && options[:daemonize]
end
```

--------------------------------

### Define Resourceful Routes with `resources` (Ruby)

Source: https://guides.rubyonrails.org/v6.1/getting_started

This snippet shows how to use the `resources` method in `config/routes.rb` to automatically map conventional routes for a resource, such as articles. It simplifies route definitions for CRUD operations.

```ruby
Rails.application.routes.draw do
  root "articles#index"

  resources :articles
end

```

--------------------------------

### Rails Route Scope Path Example

Source: https://guides.rubyonrails.org/v4.0/routing

Assigns a specific URL path prefix to resources without changing the controller's namespace. For example, `/admin/posts` can be routed to `PostsController`.

```ruby
scope '/admin' do
  resources :posts, :comments
end
```

--------------------------------

### Environment Configuration Entry Point - Ruby

Source: https://guides.rubyonrails.org/v5.2/initialization

The `config/environment.rb` file serves as the central point for configuring the Rails application. It is required by both `config.ru` (for `rails server`) and Passenger, ensuring a consistent setup across different deployment methods. It begins by requiring `config/application.rb`.

```ruby
require_relative 'application'
```

--------------------------------

### Rack Server Start Method

Source: https://guides.rubyonrails.org/v6.1/initialization

The core start method for Rack servers. It handles load path adjustments, required libraries, debugging options, PID file management, daemonization, and signal trapping for graceful shutdown before running the application.

```ruby
module Rack
  class Server
    def start &blk
      if options[:warn]
        $-w = true
      end

      if includes = options[:include]
        $LOAD_PATH.unshift(*includes)
      end

      if library = options[:require]
        require library
      end

      if options[:debug]
        $DEBUG = true
        require "pp"
        p options[:server]
        pp wrapped_app
        pp app
      end

      check_pid! if options[:pid]

      # Touch the wrapped app, so that the config.ru is loaded before
      # daemonization (i.e. before chdir, etc).
      handle_profiling(options[:heapfile], options[:profile_mode], options[:profile_file]) do
        wrapped_app
      end

      daemonize_app if options[:daemonize]

      write_pid if options[:pid]

      trap(:INT) do
        if server.respond_to?(:shutdown)
          server.shutdown
        else
          exit
        end
      end

      server.run wrapped_app, options, &blk
    end
  end
end
```

--------------------------------

### Defer Action Controller Initialization with Load Hooks (Ruby)

Source: https://guides.rubyonrails.org/configuring

This snippet shows how to use `ActiveSupport.on_load` to defer prepending a helper module to `ActionController::Base` until the Action Controller framework is loaded. This is a best practice to avoid slow boot times and potential load order conflicts.

```ruby
ActiveSupport.on_load(:action_controller_base) do
  prepend MyActionControllerHelper
end
```

--------------------------------

### ActiveModel::Serialization Usage Examples

Source: https://guides.rubyonrails.org/active_model_basics

These IRB examples show how to use ActiveModel::Serialization to serialize an object into a hash. It demonstrates basic serialization, including methods, and filtering attributes using `:only` and `:except` options.

```irb
irb> person = Person.new

irb> person.serializable_hash
=> {"name" => nil, "age" => nil}

# Set the name and age attributes and serialize the object
irb> person.name = "bob"
irb> person.age = 22
irb> person.serializable_hash
=> {"name" => "bob", "age" => 22}

# Use the methods option to include the capitalized_name method
irb>  person.serializable_hash(methods: :capitalized_name)
=> {"name" => "bob", "age" => 22, "capitalized_name" => "Bob"}

# Use the only method to include only the name attribute
irb> person.serializable_hash(only: :name)
=> {"name" => "bob"}

```

--------------------------------

### Build MySQL Test Databases

Source: https://guides.rubyonrails.org/v5.2/development_dependencies_install

Rake command to build the necessary test databases for MySQL within the Active Record gem directory. This task sets up the databases with the correct configurations.

```shell
cd activerecord
bundle exec rake db:mysql:build
```

--------------------------------

### YAML Fixture Example

Source: https://guides.rubyonrails.org/v3.0/testing

A sample YAML fixture file demonstrating the human-friendly format for describing sample data. Records are separated by blank lines, and comments can be added using the '#' character.

```yaml
# lo & behold!  I am a YAML comment!
david:
  name: David Heinemeier Hansson
  birthday: 1979-10-15
  profession: Systems development
steve:
  name: Steve Ross Kellock
  birthday: 1974-09-27
  profession: guy with keyboard
```

--------------------------------

### Article Creation Example (Ruby)

Source: https://guides.rubyonrails.org/v7.0/action_view_overview

A simple Ruby code snippet demonstrating how to create a new Article instance with a specified body. This is used in the context of explaining partial layouts.

```ruby
Article.create(body: 'Partial Layouts are cool!')

```

--------------------------------

### Generate Ruby on Rails Guides

Source: https://guides.rubyonrails.org/v3.1/ruby_on_rails_guides_guidelines

Command to generate all Ruby on Rails guides. It requires navigating to the 'railties' directory and running a rake task. Optional environment variables can be used to process specific files, force processing of all files, enable warnings, or specify a language.

```bash
cd railties
bundle exec rake generate_guides
```

```bash
bundle exec rake generate_guides ONLY=my_guide
```

```bash
bundle exec rake generate_guides ALL=1 WARNINGS=1
```

```bash
bundle exec rake generate_guides GUIDES_LANGUAGE=es
```

--------------------------------

### Generate Rails Guides and API Documentation (Ruby on Rails)

Source: https://guides.rubyonrails.org/v2.3/getting_started

These Rake tasks are used within a Rails application to generate local copies of the Rails Guides and API documentation. `rake doc:guides` places the guides in the `/doc/guides` directory, while `rake doc:rails` generates API documentation in the `/doc/api` directory.

```bash
rake doc:guides
rake doc:rails
```

--------------------------------

### Rack Server: Building the Application Stack (`build_app` method)

Source: https://guides.rubyonrails.org/v4.1/initialization

This Ruby code implements the `build_app` method, which constructs the middleware stack for the Rack application. It iterates through defined middleware, instantiates them, and applies them to the application in reverse order.

```ruby
def build_app(app)
  middleware[options[:environment]].reverse_each do |middleware|
    middleware = middleware.call(self) if middleware.respond_to?(:call)
    next unless middleware
    klass = middleware.shift
    app = klass.new(app, *middleware)
  end
  app
end
```

--------------------------------

### Create 'edit' post form view (ERB)

Source: https://guides.rubyonrails.org/v4.0/getting_started

This ERB code generates an HTML form for editing an existing post. It uses the form_for helper to target the 'update' action and 'patch' method for submission. The form includes fields for 'title' and 'text', displays validation errors if any, and a submit button. It relies on the @post instance variable being set in the controller.

```erb
<h1>Editing post</h1>
<%= form_for :post, url: post_path(@post), method: :patch do |f| %>
  <% if @post.errors.any? %>
  <div id="error_explanation">
    <h2><%= pluralize(@post.errors.count, "error") %> prohibited
      this post from being saved:</h2>
    <ul>
      <% @post.errors.full_messages.each do |msg| %>
        <li><%= msg %></li>
      <% end %>
    </ul>
  </div>
  <% end %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
<%= link_to 'Back', posts_path %>
```

--------------------------------

### Run Rails Tests for a Specific File

Source: https://guides.rubyonrails.org/v4.1/development_dependencies_install

Executes tests for a particular file within the Rails project, specifying the file path and using Bundler and Ruby.

```bash
$ cd actionpack
$ bundle exec ruby -Itest test/template/form_helper_test.rb
```

--------------------------------

### Calculate Week Boundaries in Ruby

Source: https://guides.rubyonrails.org/v6.0/active_support_core_extensions

These Ruby methods calculate the start and end dates of a week, with Monday as the default start day. An optional argument can specify a different starting day for the week. Aliases `at_beginning_of_week` and `at_end_of_week` are also available.

```ruby
d = Date.new(2010, 5, 8) # => Sat, 08 May 2010
d.beginning_of_week # => Mon, 03 May 2010
d.beginning_of_week(:sunday) # => Sun, 02 May 2010
d.end_of_week # => Sun, 09 May 2010
d.end_of_week(:sunday) # => Sat, 08 May 2010
```

--------------------------------

### Railties - `script/plugin install` with Git Support

Source: https://guides.rubyonrails.org/v5.0/2_2_release_notes

Modifies `script/plugin install` to work with both Subversion (SVN) and Git-based plugins. This enhances flexibility when managing plugins by supporting the prevalent Git version control system.

```bash
# Install a plugin from a git repository
./script/plugin install git://github.com/user/repo.git
```

```bash
# Install a specific revision of a git-based plugin
./script/plugin install git://github.com/user/repo.git -r <commit_hash>
```

--------------------------------

### Build Rack Middleware Stack (Ruby)

Source: https://guides.rubyonrails.org/v4.0/initialization

The `build_app` method in `Rack::Server` constructs the middleware stack for the Rails application. It iterates through a list of configured middlewares, instantiating each one and wrapping it around the application. This process ensures that all specified middlewares are applied in the correct order.

```ruby
middleware[options[:environment]].reverse_each do |middleware|
  middleware = middleware.call(self) if middleware.respond_to?(:call)
  next unless middleware
  klass = middleware.shift
  app = klass.new(app, *middleware)
end
app
```

--------------------------------

### Generate Rails Controller and View

Source: https://guides.rubyonrails.org/v2.3/getting_started

Generates a controller named 'home' with an 'index' action and its corresponding view file. This is the foundational step for creating a new page in a Rails application. Ensure Ruby and Rails are installed and configured correctly.

```bash
$ script/generate controller home index
```

```bash
ruby script/generate controller home index
```

--------------------------------

### Configure Spring Application Preloader

Source: https://guides.rubyonrails.org/v4.2/upgrading_ruby_on_rails

To use Spring as an application preloader in development, add the `spring` gem to your Gemfile, install it with `bundle install`, and then springify your binstubs. User-defined rake tasks will run in the development environment by default.

```ruby
gem 'spring', group: :development
```

```bash
bundle install
bundle exec spring binstub --all
```

--------------------------------

### Rack Server Middleware Integration

Source: https://guides.rubyonrails.org/initialization

Applies middleware to the Rack application in reverse order of definition. It iterates through the configured middleware, instantiates them with the application, and updates the application reference. Dependencies include the `middleware` configuration and the ability for middleware to respond to `:call`.

```ruby
module Rackup
  class Server
    private
      def build_app(app)
        middleware[options[:environment]].reverse_each do |middleware|
          middleware = middleware.call(self) if middleware.respond_to?(:call)
          next unless middleware
          klass, *args = middleware
          app = klass.new(app, *args)
        end
        app
      end
  end
end

```

--------------------------------

### List Rails Initializers with bin/rails initializers

Source: https://guides.rubyonrails.org/command_line

The `bin/rails initializers` command displays all the initializers defined in your Rails application and the order in which they are executed during the boot process. This is useful for understanding application startup sequencing.

```shell
bin/rails initializers

```

--------------------------------

### Shallow Nesting Example 1 (Specific Actions)

Source: https://guides.rubyonrails.org/v6.1/routing

Shows how to achieve shallow nesting by specifying allowed actions for nested resources.

```APIDOC
## Shallow Nesting (Specific Actions)

### Description
This example demonstrates shallow nesting by explicitly defining the actions for nested resources, balancing hierarchy with concise routes.

### Method
N/A (DSL definition)

### Endpoint
N/A (DSL definition)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

## Shallow Nesting DSL Example
```ruby
resources :articles do
  resources :comments, only: [:index, :new, :create]
end
resources :comments, only: [:show, :edit, :update, :destroy]
```

## Generated Routes (Conceptual)
- `GET /articles/:article_id/comments` (index)
- `POST /articles/:article_id/comments` (create)
- `GET /articles/:article_id/comments/new` (new)
- `GET /comments/:id` (show)
- `GET /comments/:id/edit` (edit)
- `PATCH/PUT /comments/:id` (update)
- `DELETE /comments/:id` (destroy)
```

--------------------------------

### Ruby on Rails: Miscellaneous Commands

Source: https://guides.rubyonrails.org/v6.0/command_line

Includes various other useful commands for Rails development, such as managing notes, testing, and more.

```bash
rails notes
```

```bash
rails test
```

--------------------------------

### SQL: Example of Grouping Records

Source: https://guides.rubyonrails.org/v5.1/active_record_querying

This shows the SQL generated by the Ruby code for grouping records.

```sql
SELECT date(created_at) as ordered_date, sum(price) as total_price FROM orders GROUP BY date(created_at)
```

--------------------------------

### Clone Ruby on Rails Repository

Source: https://guides.rubyonrails.org/v6.0/development_dependencies_install

This command clones the official Ruby on Rails repository from GitHub to your local machine. It is a fundamental step for contributing to the Rails core. Ensure you have Git installed before running this command.

```bash
git clone https://github.com/rails/rails.git
cd rails
```

--------------------------------

### Ruby on Rails: has_many :through Association Example

Source: https://guides.rubyonrails.org/v7.0/association_basics

Demonstrates the has_many :through association for establishing many-to-many relationships between models. This is useful when a direct join table is needed. The example shows Physicians, Patients, and Appointments.

```ruby
class Physician < ApplicationRecord
  has_many :appointments
  has_many :patients, through: :appointments
end

class Appointment < ApplicationRecord
  belongs_to :physician
  belongs_to :patient
end

class Patient < ApplicationRecord
  has_many :appointments
  has_many :physicians, through: :appointments
end
```

```ruby
class CreateAppointments < ActiveRecord::Migration[7.0]
  def change
    create_table :physicians do |t|
      t.string :name
      t.timestamps
    end

    create_table :patients do |t|
      t.string :name
      t.timestamps
    end

    create_table :appointments do |t|
      t.belongs_to :physician
      t.belongs_to :patient
      t.datetime :appointment_date
      t.timestamps
    end
  end
end
```

```ruby
physician.patients = patients
```

```ruby
class Document < ApplicationRecord
  has_many :sections
  has_many :paragraphs, through: :sections
end

class Section < ApplicationRecord
  belongs_to :document
  has_many :paragraphs
end

class Paragraph < ApplicationRecord
  belongs_to :section
end
```

```ruby
@document.paragraphs
```

--------------------------------

### Build Active Record Databases (Ruby)

Source: https://guides.rubyonrails.org/v2.3/contribute

Commands to build the necessary databases for testing Active Record with different adapters like MySQL and PostgreSQL. Refer to 'activerecord/test/config.example.yml' for configuration details. SQLite3 does not require this step.

```shell
$ cd activerecord
$ bundle exec rake db:mysql:build
```

```shell
$ cd activerecord
$ bundle exec rake db:postgresql:build
```

--------------------------------

### Rails View: Displaying Form and Validation Errors

Source: https://guides.rubyonrails.org/v4.0/getting_started

This ERB (Embedded Ruby) code snippet shows how to render a form for creating or editing a post in a Rails application. It includes conditional logic to display validation error messages if the `@post` object has any errors, using `@post.errors.any?` and `@post.errors.full_messages`. It also includes fields for title and text, and a submit button.

```html.erb
<%= form_for :post, url: posts_path do |f| %>
  <% if @post.errors.any? %>
  <div id="error_explanation">
    <h2><%= pluralize(@post.errors.count, "error") %> prohibited
      this post from being saved:</h2>
    <ul>
      <% @post.errors.full_messages.each do |msg| %>
        <li><%= msg %></li>
      <% end %>
    </ul>
  </div>
  <% end %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
<%= link_to 'Back', posts_path %>
```

--------------------------------

### Example Rails Asset Manifest JSON

Source: https://guides.rubyonrails.org/v7.0/asset_pipeline

This is an example of a `.sprockets-manifest-randomhex.json` file generated during asset precompilation. It maps logical asset paths to their fingerprinted filenames, including metadata like modification time, size, digest, and integrity.

```json
{"files":{"application-aee4be71f1288037ae78b997df388332edfd246471b533dcedaa8f9fe156442b.js":{"logical_path":"application.js","mtime":"2016-12-23T20:12:03-05:00","size":412383,
"digest":"aee4be71f1288037ae78b997df388332edfd246471b533dcedaa8f9fe156442b","integrity":"sha256-ruS+cfEogDeueLmX3ziDMu39JGRxtTPc7aqPn+FWRCs="},
"application-86a292b5070793c37e2c0e5f39f73bb387644eaeada7f96e6fc040a028b16c18.css":{"logical_path":"application.css","mtime":"2016-12-23T19:12:20-05:00","size":2994,
"digest":"86a292b5070793c37e2c0e5f39f73bb387644eaeada7f96e6fc040a028b16c18","integrity":"sha256-hqKStQcHk8N+LA5fOfc7s4dkTq6tp/lub8BAoCixbBg="},
"favicon-8d2387b8d4d32cecd93fa3900df0e9ff89d01aacd84f50e780c17c9f6b3d0eda.ico":{"logical_path":"favicon.ico","mtime":"2016-12-23T20:11:00-05:00","size":8629,
"digest":"8d2387b8d4d32cecd93fa3900df0e9ff89d01aacd84f50e780c17c9f6b3d0eda","integrity":"sha256-jSOHuNTTLOzZP6OQDfDp/4nQGqzYT1DngMF8n2s9Dto="},
"my_image-f4028156fd7eca03584d5f2fc0470df1e0dbc7369eaae638b2ff033f988ec493.png":{"logical_path":"my_image.png","mtime":"2016-12-23T20:10:54-05:00","size":23414,
"digest":"f4028156fd7eca03584d5f2fc0470df1e0dbc7369eaae638b2ff033f988ec493","integrity":"sha256-9AKBVv1+ygNYTV8vwEcN8eDbxzaequY4sv8DP5iOxJM="}},
"assets":{"application.js":"application-aee4be71f1288037ae78b997df388332edfd246471b533dcedaa8f9fe156442b.js",
"application.css":"application-86a292b5070793c37e2c0e5f39f73bb387644eaeada7f96e6fc040a028b16c18.css",
"favicon.ico":"favicon-8d2387b8d4d32cecd93fa3900df0e9ff89d01aacd84f50e780c17c9f6b3d0eda.ico",
"my_image.png":"my_image-f4028156fd7eca03584d5f2fc0470df1e0dbc7369eaae638b2ff033f988ec493.png"}}

```

--------------------------------

### Manage Temporary Directories

Source: https://guides.rubyonrails.org/v6.1/command_line

Ensures that necessary temporary directories for the Rails application are created. This command is often run during deployment or initial setup.

```bash
bin/rails tmp:create
```

--------------------------------

### Testing Remote JavaScript with XHR

Source: https://guides.rubyonrails.org/v4.2/upgrading_ruby_on_rails

When testing remote JavaScript responses in Rails 4.1, CSRF protection is now enabled for GET requests. To explicitly test an `XmlHttpRequest`, use `xhr :get`, `:index`, `format: :js` instead of `get :index`, `format: :js`.

```ruby
xhr :get, :index, format: :js
```

--------------------------------

### Rails Helper for Asset Inclusion with Debugging

Source: https://guides.rubyonrails.org/v4.0/asset_pipeline

Example of using Rails helper methods to include stylesheets and JavaScripts, with an option to enable debugging.

```html+ruby
<%= stylesheet_link_tag "application", debug: true %>
<%= javascript_include_tag "application", debug: true %>
```

--------------------------------

### Rails Server Command

Source: https://guides.rubyonrails.org/v4.2/command_line

This command starts the Rails development server, typically WEBrick, allowing you to view your application in a web browser. The server listens on a default port, usually 3000.

```bash
$ bin/rails server
=> Booting WEBrick...

```

--------------------------------

### Generate a New Rails Application

Source: https://guides.rubyonrails.org/v7.0/getting_started

Uses the `rails new` generator to create a fresh Rails application. This command sets up the project directory, installs gem dependencies, and configures the basic structure for a new application.

```bash
$ rails new blog

```

--------------------------------

### Ruby on Rails: ETag Format Examples

Source: https://guides.rubyonrails.org/v7.1/caching_with_rails

This snippet provides examples of how weak and strong ETags are represented in Ruby on Rails. Weak ETags are prefixed with 'W/', while strong ETags are represented by their hash value directly.

```text
W/"618bbc92e2d35ea1945008b42799b0e7" → Weak ETag
"618bbc92e2d35ea1945008b42799b0e7" → Strong ETag
```

--------------------------------

### Applying Rails Application Templates

Source: https://guides.rubyonrails.org/v5.1/rails_application_templates

Demonstrates how to apply a Rails application template using the 'rails new' command with the -m option, specifying a local file path or a URL. It also shows how to apply a template to an existing application using the 'app:template' Rake task.

```bash
# Applying a template during new application generation
$ rails new blog -m ~/template.rb
$ rails new blog -m http://example.com/template.rb

# Applying a template to an existing application
$ bin/rails app:template LOCATION=~/template.rb
$ bin/rails app:template LOCATION=http://example.com/template.rb
```

--------------------------------

### Initial Action Controller Framework Loading (Ruby)

Source: https://guides.rubyonrails.org/configuring

This code snippet, shown as an example to be modified, directly prepends a module to `ActionController::Base`. This action forces the Action Controller framework to load early in the application's boot process, which is generally discouraged.

```ruby
ActionController::Base.prepend(MyActionControllerHelper)
```

--------------------------------

### Simulate GET Request with Params and Headers in Rails

Source: https://guides.rubyonrails.org/v5.1/testing

This example shows how to simulate a GET request to the 'show' action of a controller, passing an ID as a parameter and setting a custom HTTP_REFERER header. This is useful for testing actions that require specific parameters or context.

```ruby
get article_url, params: { id: 12 }, headers: { "HTTP_REFERER" => "http://example.com/home" }
```

--------------------------------

### Rails database.yml Configuration with URL (YAML)

Source: https://guides.rubyonrails.org/v4.1/configuring

An example of how to specify a database connection using a URL directly within the config/database.yml file for a specific environment.

```yaml
development:
  url: postgresql://localhost/blog_development?pool=5
```

--------------------------------

### Generate Comment Model with References

Source: https://guides.rubyonrails.org/v7.2/getting_started

This command generates a Comment model, its migration file, and associated test files. The `article:references` option automatically sets up a foreign key column for associating comments with articles.

```bash
$ bin/rails generate model Comment commenter:string body:text article:references

```

--------------------------------

### Start the Rails Development Server

Source: https://guides.rubyonrails.org/command_line

This command launches the Puma web server, bundled with Rails, to run your application. It's essential for accessing your application through a web browser during development. The default port is 3000.

```bash
$ cd my_app
$ bin/rails server
=> Booting Puma
=> Rails 8.0.0 application starting in development
=> Run `bin/rails server --help` for more startup options
Puma starting in single mode...
* Puma version: 6.4.0 (ruby 3.1.3-p185) ("The Eagle of Durango")
*  Min threads: 5
*  Max threads: 5
*  Environment: development
*          PID: 5295
* Listening on http://127.0.0.1:3000
* Listening on http://[::1]:3000
Use Ctrl-C to stop
```

--------------------------------

### Rails Route Testing Example

Source: https://guides.rubyonrails.org/v3.0/testing

Provides an example of how to test routes in a Rails application. This test verifies that a given URL path correctly maps to the intended controller action and parameters, ensuring proper routing configuration. The `assert_routing` method is used for this purpose.

```ruby
test "should route to post" do
  assert_routing '/posts/1', { controller: "posts", action: "show", id: "1" }
end
```

--------------------------------

### Generate Rails Model and Database Table

Source: https://guides.rubyonrails.org/getting_started

This command generates a new Active Record model named 'Product' with a 'name' column of type string. It also creates the corresponding database migration file, model file, and test files. The model name is singular, while the database table name will be plural.

```bash
$ bin/rails generate model Product name:string

```

--------------------------------

### Ruby: Execute Rails executable

Source: https://guides.rubyonrails.org/v4.1/initialization

This Ruby code snippet demonstrates how the 'rails' command executable is invoked. It determines the version and loads the appropriate 'rails' gem executable from the load path.

```ruby
version = ">= 0"
load Gem.bin_path('railties', 'rails', version)
```

--------------------------------

### Apply Rails Template via Command Line

Source: https://guides.rubyonrails.org/v5.2/rails_application_templates

Demonstrates how to apply a Ruby on Rails application template to a new project using the `rails new` command with the `-m` option, specifying either a local file path or a URL for the template.

```bash
# Apply a local template file
$ rails new blog -m ~/template.rb

# Apply a template from a URL
$ rails new blog -m http://example.com/template.rb
```

--------------------------------

### Generate Kindle Guides (Ruby on Rails)

Source: https://guides.rubyonrails.org/ruby_on_rails_guides_guidelines

Rake task for generating guides specifically formatted for Kindle devices within a Ruby on Rails project.

```bash
bundle exec rake guides:generate:kindle
```

--------------------------------

### Ruby: Article Model Including Visible Concern

Source: https://guides.rubyonrails.org/v6.1/getting_started

This Ruby code demonstrates how the `Article` model includes the `Visible` concern, inheriting its status validations and methods. It simplifies the model by removing duplicated logic.

```ruby
class Article < ApplicationRecord
  include Visible
  has_many :comments

  validates :title, presence: true
  validates :body, presence: true, length: { minimum: 10 }
end
```

--------------------------------

### Load All Active Support Core Extensions

Source: https://guides.rubyonrails.org/v3.0/active_support_core_extensions

This snippet demonstrates how to load all core extensions provided by Active Support. This is the most comprehensive way to enable all enhancements.

```ruby
require 'active_support/all'
```

--------------------------------

### Rake Commands for Documentation Generation

Source: https://guides.rubyonrails.org/v3.1/command_line

The `doc:` Rake namespace provides tasks for generating various types of documentation. `rake doc:app` generates documentation for the application, `rake doc:guides` generates Rails guides, `rake doc:rails` generates API documentation for Rails, and `rake doc:plugins` generates documentation for installed plugins. `rake doc:clobber_plugins` removes plugin documentation.

```shell
rake doc:app
rake doc:guides
rake doc:rails
rake doc:plugins
rake doc:clobber_plugins
```

--------------------------------

### Define Routes with Controller and Action

Source: https://guides.rubyonrails.org/v4.0/routing

This example demonstrates how to define a route that maps incoming requests to a specific controller and action. It shows how Rails parses path segments into controller, action, and optional parameters like 'id'.

```ruby
get ":controller(/:action(/:id))"
```

--------------------------------

### Configure Rails Server Port and Environment

Source: https://guides.rubyonrails.org/v4.2/command_line

Demonstrates how to start the Rails server on a specific port, in a different environment, or bind to a particular IP address. The `-p` option sets the port, `-e` sets the environment (e.g., 'production'), and `-b` binds to an IP. The `-d` option runs the server as a daemon.

```bash
$ bin/rails server -e production -p 4000
```

```bash
$ bin/rails server -d -p 5000 -b 0.0.0.0
```

--------------------------------

### Bundler Rake Tasks for Gem Publishing in Shell

Source: https://guides.rubyonrails.org/v6.1/plugins

Shell commands utilizing Bundler's Rake tasks for building, installing, and releasing a Ruby gem. These tasks automate the packaging and distribution process.

```bash
$ bundle exec rake build
# Build yaffle-0.1.0.gem into the pkg directory
```

```bash
$ bundle exec rake install
# Build and install yaffle-0.1.0.gem into system gems
```

```bash
$ bundle exec rake release
# Create tag v0.1.0 and build and push yaffle-0.1.0.gem to Rubygems
```

--------------------------------

### Create Database Migrations in Rails (Create Table)

Source: https://context7.com/context7/guides_rubyonrails/llms.txt

Provides examples of generating and defining database migrations to create new tables with various column types, default values, and indexes. This uses Rails' migration DSL.

```ruby
# db/migrate/YYYYMMDDHHMMSS_create_products.rb
class CreateProducts < ActiveRecord::Migration[8.0]
  def change
    create_table :products do |t|
      t.string :name
      t.text :description
      t.decimal :price, precision: 8, scale: 2
      t.integer :stock_quantity, default: 0
      t.boolean :available, default: true

      t.timestamps
    end

    add_index :products, :name
  end
end
```

--------------------------------

### Rails Server Initialization

Source: https://guides.rubyonrails.org/initialization

Initializes the `Rails::Server` class, inheriting from `Rackup::Server`. It sets default options and calls the parent `Rackup::Server`'s initialize method, followed by setting the Rails environment.

```ruby
module Rails
  class Server < Rackup::Server
    def initialize(options = nil)
      @default_options = options || {}
      super(@default_options)
      set_environment
    end
  end
end

```

--------------------------------

### Generate HTML Guides in Different Language (Ruby on Rails)

Source: https://guides.rubyonrails.org/ruby_on_rails_guides_guidelines

Command to generate HTML guides in a language other than English by specifying the 'GUIDES_LANGUAGE' environment variable. Guides should be placed in a language-specific subdirectory under 'source'.

```bash
bundle exec rake guides:generate GUIDES_LANGUAGE=es
```

--------------------------------

### Action Mailer Delivery Example

Source: https://guides.rubyonrails.org/v7.1/active_support_instrumentation

This example shows the payload for the `deliver.action_mailer` event, detailing the parameters involved in sending an email. It includes information such as the mailer class, message ID, subject, recipients, sender, and date. The actual mail content is omitted for brevity.

```json
{
  mailer: "Notification",
  message_id: "4f5b5491f1774_181b23fc3d4434d38138e5@mba.local.mail",
  subject: "Rails Guides",
  to: ["users@rails.com", "dhh@rails.com"],
  from: ["me@rails.com"],
  date: "Sat, 10 Mar 2012 14:18:09 +0100",
  mail: "...",
  perform_deliveries: true
}
```

--------------------------------

### Default Solid Queue Configuration (YAML)

Source: https://guides.rubyonrails.org/active_job_basics

An example of the default configuration file for Solid Queue, specifying settings for dispatchers and workers. This file allows fine-tuning of job processing behavior.

```yaml
default: &default
  dispatchers:
    - polling_interval: 1
      batch_size: 500
  workers:
    - queues: "*"
      threads: 3
      processes: <%= ENV.fetch("JOB_CONCURRENCY", 1) %>
      polling_interval: 0.1
```

--------------------------------

### Rails Action Cable Connection Setup

Source: https://guides.rubyonrails.org/v7.0/action_cable_overview

This snippet demonstrates the basic setup for an Action Cable connection in a Rails application. It shows how to extend `ActionCable::Connection::Base` and handle connection authorization. This is crucial for establishing the WebSocket connection and identifying the user.

```ruby
module ApplicationCable
  class Connection < ActionCable::Connection::Base
    identified_by :current_user

    def connect
      self.current_user = find_verified_user
    end

    private

    def find_verified_user
      # Replace with your actual user authentication logic
      if current_user = User.find_by(id: cookies.encrypted[:user_id])
        current_user
      else
        reject_unauthorized_connection
      end
    end
  end
end
```

--------------------------------

### Rails Controller with Empty Index Action

Source: https://guides.rubyonrails.org/v6.1/getting_started

Defines a basic 'ArticlesController' in Ruby. The 'index' action is currently empty, which by convention in Rails will automatically render the corresponding view file ('app/views/articles/index.html.erb').

```ruby
class ArticlesController < ApplicationController
  def index
  end
end

```

--------------------------------

### Basic Article Form with `form_for` (Rails)

Source: https://guides.rubyonrails.org/v4.1/getting_started

This snippet demonstrates the basic usage of the `form_for` helper in a Rails ERB template to create an article form. It includes fields for title and text, along with a submit button. The form is initially configured to submit to a default URL. Dependencies include the Rails framework and a corresponding controller action.

```erb
<%= form_for :article do |f| %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
```

--------------------------------

### Config.ru File Content

Source: https://guides.rubyonrails.org/v3.2/initialization

This is a typical `config.ru` file content for a Rails application. It sets up the environment by requiring `config/environment.rb` and then runs the main application defined in `YourApp::Application`.

```ruby
# This file is used by Rack-based servers to start the application.
require ::File.expand_path('../config/environment', __FILE__)
run YourApp::Application
```

--------------------------------

### Active Record Store Custom Coder Example

Source: https://guides.rubyonrails.org/v5.1/4_0_release_notes

Illustrates how to use custom coders with `ActiveRecord::Store` for serializing and deserializing attributes. This example shows setting the `coder` option to `JSON` for the `settings` attribute.

```ruby
class User < ActiveRecord::Base
  store :settings, accessors: [ :color, :homepage ], coder: JSON
end
```

--------------------------------

### PostgreSQL Database Configuration in YAML

Source: https://guides.rubyonrails.org/v5.2/command_line

This YAML snippet shows the database configuration for a PostgreSQL adapter in a Rails application. It includes default settings and an example for a development environment, highlighting connection pooling and adapter specifics.

```yaml
# PostgreSQL. Versions 9.1 and up are supported.
#
# Install the pg driver:
#   gem install pg
# On OS X with Homebrew:
#   gem install pg -- --with-pg-config=/usr/local/bin/pg_config
# On OS X with MacPorts:
#   gem install pg -- --with-pg-config=/opt/local/lib/postgresql84/bin/pg_config
# On Windows:
#   gem install pg
#     Choose the win32 build.
#     Install PostgreSQL and put its /bin directory on your path.
#
# Configure Using Gemfile
# gem 'pg'
#
default: &default
  adapter: postgresql
  encoding: unicode
  # For details on connection pooling, see Rails configuration guide
  # http://guides.rubyonrails.org/configuring.html#database-pooling
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

development:
  <<: *default
  database: gitapp_development
```

--------------------------------

### Rails Asset Pipeline: Manifest File Example

Source: https://guides.rubyonrails.org/v7.0/asset_pipeline

An example of a JavaScript manifest file (`application.js`) that includes other JavaScript assets using Sprockets' require directives. This file dictates which JavaScript files are concatenated and served in development mode.

```javascript
//= require core
//= require projects
//= require tickets

```

--------------------------------

### Generate Specific Rails Guide (Ruby)

Source: https://guides.rubyonrails.org/v6.1/ruby_on_rails_guides_guidelines

This command allows for the generation of a single, specified guide file (e.g., 'my_guide.md') by using the 'ONLY' environment variable. This is useful for targeted updates or testing. Note that you may need to 'touch' the file first if it does not exist.

```ruby
touch my_guide.md
bundle exec rake guides:generate ONLY=my_guide

```

--------------------------------

### Ruby on Rails: Action Cable Channel Subscription

Source: https://guides.rubyonrails.org/v6.0/action_cable_overview

Implements the `subscribed` callback within a channel to handle consumer subscriptions. This method is called when a consumer successfully becomes a subscriber to the channel, allowing for setup or data broadcasting.

```ruby
class ChatChannel < ApplicationCable::Channel
  def subscribed
    # Called when the consumer has successfully
    # become a subscriber to this channel.
  end
end
```

--------------------------------

### Define Example Route with Specific HTTP Method (Ruby)

Source: https://guides.rubyonrails.org/v4.2/upgrading_ruby_on_rails

This Ruby code demonstrates how to define a route in Rails 4.0 using the `match` method, requiring explicit specification of the HTTP method (e.g., `:get`). This is a change from Rails 3.x where the method was often implied. Alternatively, using specific HTTP method helpers like `get` is recommended.

```ruby
# Rails 3.x
# match '/'
#   => 'root#index'

# Rails 4.x
match '/', to: 'root#index', via: :get
# or
get '/', to: 'root#index'
```

--------------------------------

### Track and Checkout Older Rails Branch

Source: https://guides.rubyonrails.org/v3.1/contributing_to_ruby_on_rails

Sets up a local Git branch to track an older version of the Ruby on Rails repository (e.g., '2-3-stable') and then checks out that branch for development or contribution purposes.

```bash
$ git branch --track 2-3-stable origin/2-3-stable
$ git checkout 2-3-stable
```

--------------------------------

### MySQL/MariaDB EXPLAIN Output with Eager Loading

Source: https://guides.rubyonrails.org/v7.1/active_record_querying

Example of `EXPLAIN` output when using eager loading (`includes`) on MySQL or MariaDB, showing separate plans for the primary and associated tables.

```sql
EXPLAIN SELECT `customers`.* FROM `customers`  WHERE `customers`.`id` = 1
+----+-------------+-----------+-------+---------------+---------+---------+-------+------+------+
| id | select_type | table     | type  | possible_keys | key     | key_len | ref   | rows | Extra |
+----+-------------+-----------+-------+---------------+---------+---------+-------+------+------+
|  1 | SIMPLE      | customers | const | PRIMARY       | PRIMARY | 4       | const | 1    |      |
+----+-------------+-----------+-------+---------------+---------+---------+-------+------+------+

EXPLAIN SELECT `orders`.* FROM `orders`  WHERE `orders`.`customer_id` IN (1)
+----+-------------+--------+------+---------------+------+---------+------+------+-------------+
| id | select_type | table  | type | possible_keys | key  | key_len | ref  | rows | Extra       |
+----+-------------+--------+------+---------------+------+---------+------+------+-------------+
|  1 | SIMPLE      | orders | ALL  | NULL          | NULL | NULL    | NULL | 1    | Using where |
+----+-------------+--------+------+---------------+------+---------+------+------+-------------+

```

--------------------------------

### Boot Rails Application with bin/rails boot

Source: https://guides.rubyonrails.org/command_line

The `bin/rails boot` command initiates the Rails application's boot process and then exits. It's primarily used for testing or verifying that the application can start up correctly without performing any further actions.

```shell
bin/rails boot

```

--------------------------------

### Setup Databases (Rails)

Source: https://guides.rubyonrails.org/v7.1/active_record_multiple_databases

Creates all databases, loads all schemas, and initializes with seed data. This command is available for the general setup, and specific setups for 'animals' and 'primary' databases are also provided. It's recommended to use `db:reset` to drop databases first.

```bash
bin/rails db:setup
bin/rails db:setup:animals
bin/rails db:setup:primary
```

--------------------------------

### Building App from Configuration File (`config.ru`)

Source: https://guides.rubyonrails.org/v5.1/initialization

Parses the `config.ru` file to construct the Rack application and merges any options defined within it. It first checks for the existence of the configuration file and aborts if not found. This is the standard way Rails applications are configured for Rack servers.

```ruby
def build_app_and_options_from_config
  if !::File.exist? options[:config]
    abort "configuration #{options[:config]} not found"
  end
  app, options = Rack::Builder.parse_file(self.options[:config], opt_parser)
  self.options.merge! options
  app
end
```

--------------------------------

### Define Custom Rack Stack with config.ru

Source: https://guides.rubyonrails.org/v4.0/rails_on_rack

This example shows how to set up a custom Rack middleware stack using a `config.ru` file in a Rails application. It specifies a custom middleware stack and then runs the Rails application.

```ruby
# config.ru
use MyOwnStackFromScratch
run Rails.application
```

--------------------------------

### Rails Controller Generator Help

Source: https://guides.rubyonrails.org/v7.1/command_line

Shows detailed usage information for the `bin/rails generate controller` command. It explains how to specify the controller name, actions, and options for creating controller files, views, tests, and helpers. It also provides an example of how to create a controller with specific actions.

```bash
$ bin/rails generate controller
Usage:
  bin/rails generate controller NAME [action action] [options]

...
...

Description:
    ...

    To create a controller within a module, specify the controller name as a path like 'parent_module/controller_name'.

    ...

Example:
    `bin/rails generate controller CreditCards open debit credit close`

    Credit card controller with URLs like /credit_cards/debit.
        Controller: app/controllers/credit_cards_controller.rb
        Test:       test/controllers/credit_cards_controller_test.rb
        Views:      app/views/credit_cards/debit.html.erb [...]
        Helper:     app/helpers/credit_cards_helper.rb


```

--------------------------------

### Refactor Rails Controller Tests with Setup and Teardown

Source: https://guides.rubyonrails.org/v6.1/testing

Demonstrates refactoring multiple controller tests by using `setup` to define an instance variable (`@article`) accessible to all tests and `teardown` to clear Rails cache. This reduces code duplication and improves test maintainability.

```ruby
require "test_helper"

class ArticlesControllerTest < ActionDispatch::IntegrationTest
  # called before every single test
  setup do
    @article = articles(:one)
  end

  # called after every single test
  teardown do
    # when controller is using cache it may be a good idea to reset it afterwards
    Rails.cache.clear
  end

  test "should show article" do
    # Reuse the @article instance variable from setup
    get article_url(@article)
    assert_response :success
  end

  test "should destroy article" do
    assert_difference("Article.count", -1) do
      delete article_url(@article)
    end

    assert_redirected_to articles_path
  end

  test "should update article" do
    patch article_url(@article), params: { article: { title: "updated" } }

    assert_redirected_to article_path(@article)
    # Reload association to fetch updated data and assert that title is updated.
    @article.reload
    assert_equal "updated", @article.title
  end
end

```

--------------------------------

### Install Development Dependencies on Ubuntu

Source: https://guides.rubyonrails.org/v7.0/development_dependencies_install

This script installs essential development tools and libraries for Ruby on Rails on Ubuntu systems using apt-get. It includes databases, caching services, image and video processing tools, and sets up the Yarn package manager. Ensure you have sudo privileges.

```bash
$ sudo apt-get update
$ sudo apt-get install sqlite3 libsqlite3-dev mysql-server libmysqlclient-dev postgresql postgresql-client postgresql-contrib libpq-dev redis-server memcached imagemagick ffmpeg mupdf mupdf-tools libxml2-dev

# Install Yarn
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
$ sudo apt-get install yarn

```

--------------------------------

### Use `link_to` Helper with Resource Object (HTML/Ruby)

Source: https://guides.rubyonrails.org/v6.1/getting_started

This ERB template snippet demonstrates a more concise way to create links using the `link_to` helper. When passed a resource object, `link_to` automatically uses the appropriate path helper (e.g., `article_path`) to generate the URL.

```erb
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <%= link_to article.title, article %>
    </li>
  <% end %>
</ul>

```

--------------------------------

### SQL: Example of Select Specific Fields

Source: https://guides.rubyonrails.org/v5.1/active_record_querying

This shows the SQL generated by the Ruby code for selecting specific fields.

```sql
SELECT viewable_by, locked FROM clients
```

--------------------------------

### Basic Integration Test for Welcome Page in Rails

Source: https://guides.rubyonrails.org/v5.0/testing

An example of a simple integration test for a Ruby on Rails application. It checks if the welcome page can be accessed and if a specific HTML element with expected content is present in the response.

```ruby
require 'test_helper'

class BlogFlowTest < ActionDispatch::IntegrationTest
  test "can see the welcome page" do
    get "/"
    assert_select "h1", "Welcome#index"
  end
end
```

--------------------------------

### Define Rails Route for Articles

Source: https://guides.rubyonrails.org/v7.1/getting_started

Adds a GET route for '/articles' that maps to the 'index' action of the 'ArticlesController' within a Rails application. This is configured in the 'config/routes.rb' file.

```ruby
Rails.application.routes.draw do
  get "/articles", to: "articles#index"

  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end
```

--------------------------------

### Rails 4.0 Gemfile Configuration

Source: https://guides.rubyonrails.org/v7.1/upgrading_ruby_on_rails

Example of how to include gems in the Gemfile for Rails 4.0. This assumes you are using Bundler to manage your dependencies.

```ruby
Bundler.require(*Rails.groups)
```

--------------------------------

### Rails Destroy Command - Model Example

Source: https://guides.rubyonrails.org/v4.1/command_line

Demonstrates the 'rails destroy' command, which reverses actions performed by the 'rails generate' command. This example shows the removal of files associated with a generated model named 'Oops'.

```shell
$ bin/rails destroy model Oops
     invoke  active_record
     remove   db/migrate/20120528062523_create_oops.rb
     remove   app/models/oops.rb
     invoke   test_unit
     remove    test/models/oops_test.rb
     remove    test/fixtures/oops.yml
```

--------------------------------

### Create Executable Test Case with Ruby

Source: https://guides.rubyonrails.org/v5.1/contributing_to_ruby_on_rails

Provides a template for creating executable test cases in Ruby to reproduce issues. This involves copying boilerplate code into a .rb file, modifying it to demonstrate the problem, and executing it with `ruby <filename>.rb`. The goal is to see the test case failing.

```ruby
# Example of a generic test case template

require 'rails'

# Set up a minimal Rails environment (e.g., Active Record)
# This part would be filled with specific setup based on the template used.

class MyTest < Minitest::Test
  def test_something_fails
    # Code to demonstrate the bug
    assert false, "This is expected to fail"
  end
end

# To run this test, save it as a .rb file (e.g., test_bug.rb)
# and execute: ruby test_bug.rb

```

--------------------------------

### Create Articles Table Migration in Ruby on Rails

Source: https://guides.rubyonrails.org/v6.0/getting_started

This Ruby code defines a database migration for creating an 'articles' table. It uses ActiveRecord::Migration to specify columns like 'title' (string) and 'text' (text), along with automatic timestamp fields. The `change` method makes the migration reversible.

```ruby
class CreateArticles < ActiveRecord::Migration[6.0]
  def change
    create_table :articles do |t|
      t.string :title
      t.text :text
      t.timestamps
    end
  end
end
```

--------------------------------

### Run Active Record Tests for MySQL2 and PostgreSQL

Source: https://guides.rubyonrails.org/v5.1/contributing_to_ruby_on_rails

These commands run the Active Record test suite for MySQL2 and PostgreSQL database adapters, respectively. Similar to SQLite3, ensure you are in the 'activerecord' directory and have dependencies managed by Bundler.

```bash
bundle exec rake test:mysql2
```

```bash
bundle exec rake test:postgresql
```

--------------------------------

### Rails Default Controller Rendering Example

Source: https://guides.rubyonrails.org/v4.2/layouts_and_rendering

Demonstrates how Rails automatically renders views based on controller actions and routes, following the 'convention over configuration' principle. It shows a basic controller and a corresponding ERB view file.

```ruby
class BooksController < ApplicationController
  def index
    @books = Book.all
  end
end
```

```erb
<h1>Listing Books</h1>
<table>
  <tr>
    <th>Title</th>
    <th>Summary</th>
    <th></th>
    <th></th>
    <th></th>
  </tr>
<% @books.each do |book| %>
  <tr>
    <td><%= book.title %></td>
    <td><%= book.content %></td>
    <td><%= link_to "Show", book %></td>
    <td><%= link_to "Edit", edit_book_path(book) %></td>
    <td><%= link_to "Remove", book, method: :delete, data: { confirm: "Are you sure?" } %></td>
  </tr>
<% end %>
</table>
<br>
<%= link_to "New book", new_book_path %>
```

--------------------------------

### Navigate to Rails Application Directory

Source: https://guides.rubyonrails.org/getting_started_with_devcontainer

After generating the Rails application, this command changes the current directory to the newly created 'store' application folder. This is necessary to access the application's files and run subsequent commands within the project context.

```bash
#!/bin/bash
cd store

```

--------------------------------

### Example Nested Attributes Parameters in Rails

Source: https://guides.rubyonrails.org/v6.1/form_helpers

Provides an example of the expected structure for parameters submitted from a form handling nested attributes in Rails. The `addresses_attributes` key is used to group attributes for each associated address record.

```json
{
  'person' => {
    'name' => 'John Doe',
    'addresses_attributes' => {
      '0' => {
        'kind' => 'Home',
        'street' => '221b Baker Street'
      },
      '1' => {
        'kind' => 'Office',
        'street' => '31 Spooner Street'
      }
    }
  }
}

```

--------------------------------

### PostgreSQL Query Explanation with Analyze and Verbose

Source: https://guides.rubyonrails.org/v7.1/active_record_querying

Demonstrates how to use the `.explain` method with `:analyze` and `:verbose` options for PostgreSQL to get detailed query execution plans. This requires the database adapter to support these options. The output includes the query plan and execution statistics.

```Ruby
Customer.where(id: 1).joins(:orders).explain(:analyze, :verbose)
```

```sql
EXPLAIN (ANALYZE, VERBOSE) SELECT "shop_accounts".* FROM "shop_accounts" INNER JOIN "customers" ON "customers"."id" = "shop_accounts"."customer_id" WHERE "shop_accounts"."id" = $1 [["id", 1]]
                                                                   QUERY PLAN
------------------------------------------------------------------------------------------------------------------------------------------------
 Nested Loop  (cost=0.30..16.37 rows=1 width=24) (actual time=0.003..0.004 rows=0 loops=1)
   Output: shop_accounts.id, shop_accounts.customer_id, shop_accounts.customer_carrier_id
   Inner Unique: true
   ->  Index Scan using shop_accounts_pkey on public.shop_accounts  (cost=0.15..8.17 rows=1 width=24) (actual time=0.003..0.003 rows=0 loops=1)
         Output: shop_accounts.id, shop_accounts.customer_id, shop_accounts.customer_carrier_id
         Index Cond: (shop_accounts.id = '1'::bigint)
   ->  Index Only Scan using customers_pkey on public.customers  (cost=0.15..8.17 rows=1 width=8) (never executed)
         Output: customers.id
         Index Cond: (customers.id = shop_accounts.customer_id)
         Heap Fetches: 0
 Planning Time: 0.063 ms
 Execution Time: 0.011 ms
(12 rows)
```