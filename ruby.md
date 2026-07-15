### Making Basic GET Requests with Net::HTTP

Source: https://docs.ruby-lang.org/en/master/Net

This snippet shows how to perform simple GET requests using the Net::HTTP class. It includes examples of fetching content from a given URI and also from a hostname and path combination. It also illustrates how to start an HTTP session to make multiple requests.

```ruby
# Net::HTTP.get(uri)\n# Net::HTTP.get(hostname, '/index.html')\nNet::HTTP.start(hostname) do |http|\n  http.get('/todos/1')\n  http.get('/todos/2')\nend
```

--------------------------------

### Example: Installing to a directory - Ruby

Source: https://docs.ruby-lang.org/en/master/FileUtils

Shows how to install a file to a directory. The file is copied into the directory with its original name.

```Ruby
File.read('src2.txt')       # => "aaa\n"
File.read('dest2/src2.txt') # => "bbb\n"
FileUtils.install('src2.txt', 'dest2')
File.read('dest2/src2.txt') # => "aaa\n"
```

--------------------------------

### Execute RubyGems Setup

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

The main execution function for the setup command. It configures verbosity, extends FileUtils and MakeDirs, generates destination directories, installs libraries and executables, removes old files, and provides feedback on the installation process.

```ruby
def execute
  @verbose = Gem.configuration.really_verbose

  require "fileutils"
  if Gem.configuration.really_verbose
    extend FileUtils::Verbose
  else
    extend FileUtils
  end
  extend MakeDirs

  lib_dir, bin_dir = make_destination_dirs
  man_dir = generate_default_man_dir

  install_lib lib_dir

  install_executables bin_dir

  remove_old_bin_files bin_dir

  remove_old_lib_files lib_dir

  # Can be removed one we drop support for bundler 2.2.3 (the last version installing man files to man_dir)
  remove_old_man_files man_dir if man_dir && File.exist?(man_dir)

  install_default_bundler_gem bin_dir

  if mode = options[:dir_mode]
    @mkdirs.uniq!
    File.chmod(mode, @mkdirs)
  end

  say "RubyGems #{Gem::VERSION} installed"

  regenerate_binstubs(bin_dir) if options[:regenerate_binstubs]
  regenerate_plugins(bin_dir) if options[:regenerate_plugins]

  uninstall_old_gemcutter

  documentation_success = install_rdoc

  say
  if @verbose
    say "-" * 78
    say
  end

  if options[:previous_version].empty?
    options[:previous_version] = Gem::VERSION.sub(/[0-9]+$/, "0")
  end

  options[:previous_version] = Gem::Version.new(options[:previous_version])

  show_release_notes

  say
  say "-" * 78
  say

  say "RubyGems installed the following executables:"
  say bin_file_names.map {|name| "\t#{name}\n" }
  say

  unless bin_file_names.grep(/#{File::SEPARATOR}gem$/)
    say "If `gem` was installed by a previous RubyGems installation, you may need"
    say "to remove it by hand."
    say
  end

  if documentation_success
    if options[:document].include? "rdoc"
      say "Rdoc documentation was installed. You may now invoke:"
      say "  gem server"
      say "and then peruse beautifully formatted documentation for your gems"
      say "with your web browser. If you do not wish to install this documentation in the future, use the"
      say "--no-document flag, or set it as the default in your ~/.gemrc file. See"
      say "'gem help env' for details."
      say
    end

    if options[:document].include? "ri"
      say "Ruby Interactive (ri) documentation was installed. ri is kind of like man "
      say "pages for Ruby libraries. You may access it like this:"
      say "  ri Classname"
      say "  ri Classname.class_method"
      say "  ri Classname#instance_method"
      say "If you do not wish to install this documentation in the future, use the"
      say "--no-document flag, or set it as the default in your ~/.gemrc file. See"
      say "'gem help env' for details."
      say
    end
  end
end
```

--------------------------------

### Setup Coverage Measurement (Ruby)

Source: https://docs.ruby-lang.org/en/master/Coverage

Initializes coverage measurement. Does not start it; use Coverage.resume. Coverage.start can be used for both setup and start.

```ruby
coverages = rb_get_coverages();
if (!RTEST(coverages)) {
    coverages = rb_hash_new();
    rb_obj_hide(coverages);
    current_mode = mode;
    if (mode == 0) mode = COVERAGE_TARGET_LINES;
    rb_set_coverages(coverages, mode, me2counter);
    current_state = SUSPENDED;
}
else if (current_mode != mode) {
    rb_raise(rb_eRuntimeError, "cannot change the measuring target during coverage measurement");
}

return Qnil;
}
```

--------------------------------

### Example: Basic file installation - Ruby

Source: https://docs.ruby-lang.org/en/master/FileUtils

Demonstrates a basic file installation where a source file is copied to a destination file, overwriting if the destination exists.

```Ruby
File.read('src0.txt')    # => "aaa\n"
File.exist?('dest0.txt') # => false
FileUtils.install('src0.txt', 'dest0.txt')
File.read('dest0.txt')   # => "aaa\n"
```

--------------------------------

### Making GET Requests with Net::HTTP

Source: https://docs.ruby-lang.org/en/master/Net/HTTPResponse

Provides examples of making GET requests using Net::HTTP. It shows both direct requests using a URI and requests specifying the hostname and path. It also demonstrates starting an HTTP session and making multiple requests within it.

```ruby
Net::HTTP.get(uri)\nNet::HTTP.get(hostname, '/index.html')\nNet::HTTP.start(hostname) do |http|\n  http.get('/todos/1')\n  http.get('/todos/2')\nend
```

--------------------------------

### GET Request Examples

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Examples of making simple GET requests using Net::HTTP, including retrieving data as a string or as a response object.

```APIDOC
## GET Request Examples

### Description
Examples of making simple GET requests using Net::HTTP, including retrieving data as a string or as a response object.

### Method
GET

### Endpoint
Various (depends on URI provided)

### Parameters
#### Query Parameters
- **uri** (URI) - Required - The URI object for the request.
- **hostname** (String) - Required - The hostname for the request.
- **path** (String) - Required - The path for the request.

### Request Example
```ruby
require 'net/http'

# Example using URI object
hostname = 'jsonplaceholder.typicode.com'
path = '/todos/1'
uri = URI("https://#{hostname}#{path}")

# Get response as string
response_body = Net::HTTP.get(uri)
puts response_body

# Get response as Net::HTTPResponse object
response = Net::HTTP.get_response(uri)
puts response.body

# Get response using hostname and path
response_body_alt = Net::HTTP.get(hostname, path)
puts response_body_alt
```

### Response
#### Success Response (200)
- **body** (String) - The response body content.
- **code** (String) - The HTTP status code (e.g., "200").

#### Response Example
```json
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```
```

--------------------------------

### Build Ruby from Source Directory

Source: https://docs.ruby-lang.org/en/master/windows_md

This example demonstrates the standard process of building Ruby from its source directory on Windows. It outlines the necessary steps from configuring the build environment to installation.

```batch
C:
cd \ruby
win32\configure --prefix=/usr/local
nmake
nmake check
nmake install
```

--------------------------------

### Example: Installing multiple files to a directory - Ruby

Source: https://docs.ruby-lang.org/en/master/FileUtils

Illustrates installing multiple files from an array of paths to a specified directory. Each file is placed directly within the destination directory.

```Ruby
File.file?('src3.txt') # => true
File.file?('src3.dat') # => true
FileUtils.mkdir('dest3')
FileUtils.install(['src3.txt', 'src3.dat'], 'dest3')
File.file?('dest3/src3.txt') # => true
File.file?('dest3/src3.dat') # => true
```

--------------------------------

### Example usage of FileUtils.install with verbose and noop options

Source: https://docs.ruby-lang.org/en/master/FileUtils

Demonstrates how to use the `install` method with `noop: true` and `verbose: true` to see the commands that would be executed without actually performing the file operations.

```ruby
FileUtils.install('src0.txt', 'dest0.txt', noop: true, verbose: true)
FileUtils.install('src1.txt', 'dest1.txt', noop: true, verbose: true)
FileUtils.install('src2.txt', 'dest2', noop: true, verbose: true)
```

--------------------------------

### Execute Gem Installation

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/InstallCommand

Executes the gem installation process, handling gem dependencies, environment setup, version checks, and reporting installation results.

```ruby
# File lib/rubygems/commands/install_command.rb, line 148
def execute
  if options.include? :gemdeps
    install_from_gemdeps
    return # not reached
  end

  @installed_specs = []

  ENV.delete "GEM_PATH" if options[:install_dir].nil?

  check_version

  load_hooks

  exit_code = install_gems

  show_installed

  say update_suggestion if eligible_for_update?

  terminate_interaction exit_code
end
```

--------------------------------

### Configure Ruby Build with Visual C++

Source: https://docs.ruby-lang.org/en/master/windows_md

Example of running the configure script for Visual C++ builds, specifying the target platform and installation directory. It also shows how to use --program-prefix and --program-suffix.

```batch
win32\configure.bat --target=i686-mswin32
win32\configure.bat --prefix=<install_directory>
win32\configure.bat --program-suffix=-$(MAJOR)$(MINOR)
win32\configure.bat --install-name=$(RUBY_BASE_NAME)-$(MAJOR)$(MINOR)
```

--------------------------------

### Ruby Compilation and Installation Steps

Source: https://docs.ruby-lang.org/en/master/README_ja_md

This outlines the essential steps for compiling and installing Ruby from source. It includes running autogen.sh, configuring the build, editing configuration files, making, testing, and installing the compiled binaries.

```bash
./autogen.sh
configure
make
make check
make install
```

--------------------------------

### Example: Verbose output for symbolic link creation

Source: https://docs.ruby-lang.org/en/master/FileUtils

Illustrates how to get verbose output, showing the equivalent command-line operations for symbolic link creation.

```ruby
FileUtils.ln_s('src0.txt', 'dest0.txt', noop: true, verbose: true)
FileUtils.ln_s('src1.txt', 'destdir1', noop: true, verbose: true)
FileUtils.ln_s('src2.txt', 'dest2.txt', force: true, noop: true, verbose: true)
FileUtils.ln_s(['srcdir3/src0.txt', 'srcdir3/src1.txt'], 'destdir3', noop: true, verbose: true)
```

--------------------------------

### Basic OptionParser Setup in Ruby

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Demonstrates the basic setup for `OptionParser` in Ruby: requiring the library, creating a parser instance, defining simple options with descriptions and blocks, and parsing the command line using `parse!`.

```Ruby
# Require the OptionParser code.
require 'optparse
# Create an OptionParser object.
parser = OptionParser.new
# Define one or more options.
parser.on('-x', 'Whether to X') do |value|
  p ['x', value]
end
parser.on('-y', 'Whether to Y') do |value|
  p ['y', value]
end
parser.on('-z', 'Whether to Z') do |value|
  p ['z', value]
end
# Parse the command line and return pared-down ARGV.
p parser.parse!
```

--------------------------------

### Install File List (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Installs multiple files by iterating through a list and calling the 'install_file' function for each file. This is a utility function to simplify the installation of multiple files.

```Ruby
def install_file_list(files, dest_dir)
  files.each do |file|
    install_file file, dest_dir
  end
end
```

--------------------------------

### Initialize Gem::Commands::SetupCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Initializes the SetupCommand with various options for installing RubyGems. It configures options such as executable formatting, documentation types, installation directories, and binstub regeneration. Dependencies include the superclass `Gem::Command`.

```ruby
# File lib/rubygems/commands/setup_command.rb, line 15
def initialize
  super "setup", "Install RubyGems",
        format_executable: false, document: %w[ri],
        force: true,
        site_or_vendor: "sitelibdir",
        destdir: "", prefix: "", previous_version: "",
        regenerate_binstubs: true,
        regenerate_plugins: true

  add_option "--previous-version=VERSION",
             "Previous version of RubyGems",
             "Used for changelog processing" do |version, options|
    options[:previous_version] = version
  end

  add_option "--prefix=PREFIX",
             "Prefix path for installing RubyGems",
             "Will not affect gem repository location" do |prefix, options|
    options[:prefix] = File.expand_path prefix
  end

  add_option "--destdir=DESTDIR",
             "Root directory to install RubyGems into",
             "Mainly used for packaging RubyGems" do |destdir, options|
    options[:destdir] = File.expand_path destdir
  end

  add_option "--[no-]vendor",
             "Install into vendorlibdir not sitelibdir" do |vendor, options|
    options[:site_or_vendor] = vendor ? "vendorlibdir" : "sitelibdir"
  end

  add_option "--[no-]format-executable",
             "Makes `gem` match ruby",
             "If Ruby is ruby18, gem will be gem18" do |value, options|
    options[:format_executable] = value
  end

  add_option "--[no-]document [TYPES]", Array,
             "Generate documentation for RubyGems",
             "List the documentation types you wish to",
             "generate.  For example: rdoc,ri" do |value, options|
    options[:document] = case value
                         when nil   then %w[rdoc ri]
                         when false then []
                         else value
    end
  end

  add_option "--[no-]rdoc",
             "Generate RDoc documentation for RubyGems" do |value, options|
    if value
      options[:document] << "rdoc"
    else
      options[:document].delete "rdoc"
    end

    options[:document].uniq!
  end

  add_option "--[no-]ri",
             "Generate RI documentation for RubyGems" do |value, options|
    if value
      options[:document] << "ri"
    else
      options[:document].delete "ri"
    end

    options[:document].uniq!
  end

  add_option "--[no-]regenerate-binstubs",
             "Regenerate gem binstubs" do |value, options|
    options[:regenerate_binstubs] = value
  end

  add_option "--[no-]regenerate-plugins",
             "Regenerate gem plugins" do |value, options|
    options[:regenerate_plugins] = value
  end

  add_option "-f", "--[no-]force",
             "Forcefully overwrite binstubs" do |value, options|
    options[:force] = value
  end

  add_option("-E", "--[no-]env-shebang",
             "Rewrite executables with a shebang",
             "of /usr/bin/env") do |value, options|
    options[:env_shebang] = value
  end

  @verbose = nil
end
```

--------------------------------

### Install File (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Installs a single file to a specified destination directory. It ensures the destination directory exists by creating it if necessary, and then copies the file with appropriate permissions.

```Ruby
def install_file(file, dest_dir)
  dest_file = File.join dest_dir, file
  dest_dir = File.dirname dest_file
  unless File.directory? dest_dir
    mkdir_p dest_dir, mode: 0o755
  end

  install file, dest_file, mode: options[:data_mode] || 0o644
end
```

--------------------------------

### Generate HTML Documentation (Shell)

Source: https://docs.ruby-lang.org/en/master/contributing/documentation_guide_md

Command to generate HTML documentation from source files. Assumes a build directory exists; otherwise, follow the quick start guide.

```shell
make html
```

--------------------------------

### Install Default Bundler Gem (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Installs the default Bundler gem, handling existing installations by removing old specs and executables. It rebuilds and installs the Bundler gem, ensuring the latest version is set as default.

```Ruby
def install_default_bundler_gem(bin_dir)
  current_default_spec = Gem::Specification.default_stubs.find {|s| s.name == "bundler" }
  specs_dir = if current_default_spec && default_dir == Gem.default_dir
    all_specs_current_version = Gem::Specification.stubs.select {|s| s.full_name == current_default_spec.full_name }

    Gem::Specification.remove_spec current_default_spec
    loaded_from = current_default_spec.loaded_from
    File.delete(loaded_from)

    # Remove previous default gem executables if they were not shadowed by a regular gem
    FileUtils.rm_rf current_default_spec.full_gem_path if all_specs_current_version.size == 1

    File.dirname(loaded_from)
  else
    target_specs_dir = File.join(default_dir, "specifications", "default")
    mkdir_p target_specs_dir, mode: 0o755
    target_specs_dir
  end

  new_bundler_spec = Dir.chdir("bundler") { Gem::Specification.load("bundler.gemspec") }
  full_name = new_bundler_spec.full_name
  gemspec_path = "#{full_name}.gemspec"

  default_spec_path = File.join(specs_dir, gemspec_path)
  Gem.write_binary(default_spec_path, new_bundler_spec.to_ruby)

  bundler_spec = Gem::Specification.load(default_spec_path)

  # Remove gemspec that was same version of vendored bundler.
  normal_gemspec = File.join(default_dir, "specifications", gemspec_path)
  if File.file? normal_gemspec
    File.delete normal_gemspec
  end

  # Remove gem files that were same version of vendored bundler.
  if File.directory? bundler_spec.gems_dir
    Dir.entries(bundler_spec.gems_dir).
      select {|default_gem| File.basename(default_gem) == full_name }.
      each {|default_gem| rm_r File.join(bundler_spec.gems_dir, default_gem) }
  end

  require_relative "../installer"

  Dir.chdir("bundler") do
    built_gem = Gem::Package.build(new_bundler_spec)
    begin
      Gem::Installer.at(
        built_gem,
        env_shebang: options[:env_shebang],
        format_executable: options[:format_executable],
        force: options[:force],
        install_as_default: true,
        bin_dir: bin_dir,
        install_dir: default_dir,
        wrappers: true
      ).install
    ensure
      FileUtils.rm_f built_gem
    end
  end

  new_bundler_spec.executables.each {|executable| bin_file_names << target_bin_path(bin_dir, executable) }

  say "Bundler #{new_bundler_spec.version} installed"
end
```

--------------------------------

### CLI Execution Examples (Ruby)

Source: https://docs.ruby-lang.org/en/master/SyntaxSuggest/Cli

Demonstrates various ways to invoke the SyntaxSuggest CLI with different arguments, including help, file paths, and recording options.

```ruby
Cli.new(argv: ["--help"]).call
Cli.new(argv: ["<path/to/file>.rb"]).call
Cli.new(argv: ["<path/to/file>.rb", "--record=tmp"]).call
Cli.new(argv: ["<path/to/file>.rb", "--terminal"]).call
```

--------------------------------

### Install Library Files (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Installs library files for RubyGems and Bundler. It identifies library directories for each tool, retrieves a list of files within those directories, and then uses 'install_file_list' to copy them to the target library directory.

```Ruby
def install_lib(lib_dir)
  libs = { "RubyGems" => "lib" }
  libs["Bundler"] = "bundler/lib"
  libs.each do |tool, path|
    say "Installing #{tool}" if @verbose

    lib_files = files_in path

    Dir.chdir path do
      install_file_list(lib_files, lib_dir)
    end
  end
end
```

--------------------------------

### Get String Representation of Path (Ruby Example)

Source: https://docs.ruby-lang.org/en/master/File

Provides examples of using `File.path` to get the string representation of file paths, including special paths like `/dev/null` and `Pathname` objects.

```ruby
File.path(File::NULL)           #=> "/dev/null"
File.path(Pathname.new("/tmp")) #=> "/tmp"
```

--------------------------------

### OptionParser Execution Examples in Ruby

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Illustrates various execution scenarios for a Ruby script using `OptionParser`, showing how options are parsed, arguments are handled, and how the remaining arguments are returned after `parse!` is called. Includes examples with valid options, invalid options, and arguments mixed with options.

```Shell
$ ruby basic.rb -x -z
["x", true]
["z", true]
[]
$ ruby basic.rb -z -y -x
["z", true]
["y", true]
["x", true]
[]
$ ruby basic.rb -x input_file.txt output_file.txt
["x", true]
["input_file.txt", "output_file.txt"]
$ ruby basic.rb -a
basic.rb:16:in '<main>': invalid option: -a (OptionParser::InvalidOption)
```

--------------------------------

### Example: Get Block Size

Source: https://docs.ruby-lang.org/en/master/File/Stat

Illustrates how to get the block size of the file system for a given file.

```ruby
File.stat("testfile").blksize   #=> 4096
```

--------------------------------

### Get Gem Installation Directory (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem

Returns the primary path where gems are installed. This method delegates to `paths.home`.

```Ruby
def self.dir
  paths.home
end
```

--------------------------------

### Ruby Method Calling Sequence Examples (RDoc)

Source: https://docs.ruby-lang.org/en/master/contributing/documentation_guide_md

Demonstrates the RDoc syntax for documenting method calling sequences in Ruby. Covers singleton methods, instance methods, operator methods, optional arguments, and block handling.

```ruby
*  call-seq:
*    Hash.new(default_value = nil) -> new_hash
*    Hash.new {|hash, key| ... } -> new_hash
```

```ruby
*  call-seq:
*    count -> integer
*    count(obj) -> integer
*    count {|element| ... } -> integer
```

```ruby
*  call-seq:
*    <=> other -> -1, 0, 1, or nil
```

```ruby
*  call-seq:
*    self & other_array -> new_array
```

```ruby
*  call-seq:
*    respond_to?(symbol, include_all = false) -> true or false
```

```ruby
*  call-seq:
*    max    -> element
*    max(n) -> array
```

```ruby
*  call-seq:
*    array.select {|element| ... } -> new_array
*    array.select -> new_enumerator
```

--------------------------------

### Aligning IRB Output in Examples (Ruby)

Source: https://docs.ruby-lang.org/en/master/contributing/documentation_guide_md

Shows how to align the output (`# => ...`) from `irb` sessions in code examples for improved readability.

```ruby
a = [1, 2, 3] #=> [1, 2, 3]
a.shuffle!    #=> [2, 3, 1]
a             #=> [2, 3, 1]
```

--------------------------------

### Ruby Example: Getting Ancillary Data Type

Source: https://docs.ruby-lang.org/en/master/Socket/AncillaryData

This Ruby example shows how to get the type of socket ancillary data. It creates a new `AncillaryData` object with specific parameters and then retrieves its type, printing the resulting integer.

```ruby
p Socket::AncillaryData.new(:INET6, :IPV6, :PKTINFO, "").type
#=> 2
```

--------------------------------

### Install Executables (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Installs executables for RubyGems, specifically 'gem'. It handles both Unix-like systems and Windows by creating necessary executable files and batch files for Windows. Dependencies include Ruby's built-in modules like 'tmpdir'.

```Ruby
def install_executables(bin_dir)
  prog_mode = options[:prog_mode] || 0o755

  executables = { "gem" => "exe" }
  executables.each do |tool, path|
    say "Installing #{tool} executable" if @verbose

    Dir.chdir path do
      bin_file = "gem"

      require "tmpdir"

      dest_file = target_bin_path(bin_dir, bin_file)
      bin_tmp_file = File.join Dir.tmpdir, "#{bin_file}.$$"

      begin
        bin = File.readlines bin_file
        bin[0] = shebang

        File.open bin_tmp_file, "w" do |fp|
          fp.puts bin.join
        end

        install bin_tmp_file, dest_file, mode: prog_mode
        bin_file_names << dest_file
      ensure
        rm bin_tmp_file
      end

      next unless Gem.win_platform?

      begin
        bin_cmd_file = File.join Dir.tmpdir, "#{bin_file}.bat"

        File.open bin_cmd_file, "w" do |file|
          file.puts <<-TEXT
  @ECHO OFF
  @"%~dp0#{File.basename(Gem.ruby).chomp('"')}" "%~dpn0" %*
  TEXT
        end

        install bin_cmd_file, "#{dest_file}.bat", mode: prog_mode
      ensure
        rm bin_cmd_file
      end
    end
  end
end
```

--------------------------------

### Get Instruction Sequence Examples

Source: https://docs.ruby-lang.org/en/master/RubyVM/InstructionSequence

Illustrates how to use `RubyVM::InstructionSequence.of` to obtain the instruction sequence for both procs and methods, showing how to inspect them in IRB and after requiring a file.

```ruby
# a proc
> p = proc { num = 1 + 2 }
> RubyVM::InstructionSequence.of(p)
> #=> <RubyVM::InstructionSequence:block in irb_binding@(irb)>

# for a method
> def foo(bar); puts bar; end
> RubyVM::InstructionSequence.of(method(:foo))
> #=> <RubyVM::InstructionSequence:foo@(irb)>
```

```ruby
# /tmp/iseq_of.rb
def hello
  puts "hello, world"
end

$a_global_proc = proc { str = 'a' + 'b' }

# in irb
> require '/tmp/iseq_of.rb'

# first the method hello
> RubyVM::InstructionSequence.of(method(:hello))
> #=> #<RubyVM::InstructionSequence:0x007fb73d7cb1d0>

# then the global proc
> RubyVM::InstructionSequence.of($a_global_proc)
> #=> #<RubyVM::InstructionSequence:0x007fb73d7caf78>
```

--------------------------------

### Get Binary Installation Directory

Source: https://docs.ruby-lang.org/en/master/Gem

Determines the path where gem executables are installed. It defaults to the standard Gem directory's 'bin' subdirectory, unless a custom install directory is specified or it matches the default gem directory.

```ruby
def self.bindir(install_dir = Gem.dir)
  return File.join install_dir, "bin" unless
    install_dir.to_s == Gem.default_dir.to_s
  Gem.default_bindir
end
```

--------------------------------

### Setup Bundler Environment

Source: https://docs.ruby-lang.org/en/master/Bundler

This snippet demonstrates how to set up the Bundler environment in a Ruby project. It requires the 'bundler/setup' library to ensure that only the specified gems and their versions from the gemfile are used.

```ruby
require 'bundler/setup'
```

--------------------------------

### Install Git and Ruby with Scoop

Source: https://docs.ruby-lang.org/en/master/windows_md

Instructions for installing Git and Ruby using the Scoop package manager, a common method for managing development tools on Windows.

```shell
scoop install git ruby
```

--------------------------------

### Get Start Line (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Retrieves the line number where the location starts within the source.

```ruby
def start_line
  source.line(start_offset)
end
```

--------------------------------

### Get RubyGems Installation Prefix (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem

Determines the directory prefix where RubyGems was installed. Returns nil if RubyGems is in a standard location.

```ruby
def self.prefix
  prefix = File.dirname RUBYGEMS_DIR

  if prefix != File.expand_path(RbConfig::CONFIG["sitelibdir"]) &&
     prefix != File.expand_path(RbConfig::CONFIG["libdir"]) &&
     File.basename(RUBYGEMS_DIR) == "lib"
    prefix
  end
end
```

--------------------------------

### Get Cached Start Code Units Column

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Calculates the start column of the location in code units, using a provided cache. The column is measured from the start of the line.

```Ruby
def cached_start_code_units_column(cache)
  cache[start_offset] - cache[source.line_start(start_offset)]
end
```

--------------------------------

### Initialize Gem::Installer (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Initializes a Gem::Installer instance. It takes a package (either a path or Gem::Package object) and options. It sets up file modes and processes installation options.

```ruby
def initialize(package, options = {})
  require "fileutils"

  @options = options
  @package = package

  process_options

  @package.dir_mode = options[:dir_mode]
  @package.prog_mode = options[:prog_mode]
  @package.data_mode = options[:data_mode]
end
```

--------------------------------

### Minimal OptionParser Example

Source: https://docs.ruby-lang.org/en/master/OptionParser

A basic example demonstrating how to create and parse command-line options using OptionParser. It sets up a verbose flag and prints the parsed options and remaining arguments.

```ruby
require 'optparse'

options = {}
OptionParser.new do |parser|
  parser.banner = "Usage: example.rb [options]"

  parser.on("-v", "--[no-]verbose", "Run verbosely") do |v|
    options[:verbose] = v
  end
end.parse!

p options
p ARGV

```

--------------------------------

### Initialize Gem::DependencyInstaller

Source: https://docs.ruby-lang.org/en/master/Gem/DependencyInstaller

Creates a new installer instance with specified options. Options control aspects like the installation directory, build root, and whether to install dependencies, prerelease versions, or generate wrappers.

```ruby
def initialize(options = {})
  @only_install_dir = !options[:install_dir].nil?
  @install_dir = options[:install_dir] || Gem.dir
  @build_root = options[:build_root]

  options = DEFAULT_OPTIONS.merge options

  @bin_dir             = options[:bin_dir]
  @dev_shallow         = options[:dev_shallow]
  @development         = options[:development]
  @document            = options[:document]
  @domain              = options[:domain]
  @env_shebang         = options[:env_shebang]
  @force               = options[:force]
  @format_executable   = options[:format_executable]
  @ignore_dependencies = options[:ignore_dependencies]
  @prerelease          = options[:prerelease]
  @security_policy     = options[:security_policy]
  @user_install        = options[:user_install]
  @wrappers            = options[:wrappers]
  @build_args          = options[:build_args]
  @build_docs_in_background = options[:build_docs_in_background]
  @install_as_default = options[:install_as_default]
  @dir_mode = options[:dir_mode]
  @data_mode = options[:data_mode]
  @prog_mode = options[:prog_mode]

  # Indicates that we should not try to update any deps unless
  # we absolutely must.
  @minimal_deps = options[:minimal_deps]

  @available      = nil
  @installed_gems = []
  @toplevel_specs = nil

  @cache_dir = options[:cache_dir] || @install_dir

  @errors = []
end
```

--------------------------------

### Get Start Line Slice (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Extracts the portion of the starting line that appears before this location begins.

```ruby
def start_line_slice
  offset = source.line_start(start_offset)
  source.slice(offset, start_offset - offset)
end
```

--------------------------------

### Build and Install Ruby with Visual C++

Source: https://docs.ruby-lang.org/en/master/windows_md

Commands to compile, test, and install Ruby using Visual C++ after configuration. This includes commands like nmake and nmake install, with a step for copying vcpkg libraries.

```makefile
nmake up
nmake
nmake prepare-vcpkg
nmake check
nmake install
```

--------------------------------

### Get OpenSSL Digest Name Example (Ruby)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/Digest

Demonstrates how to get the name of a SHA512 digest using the OpenSSL library in Ruby.

```ruby
digest = OpenSSL::Digest.new('SHA512')
puts digest.name # => SHA512
```

--------------------------------

### Get Ruby Install Name (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Returns the installation name for the Ruby executable. This is derived from the Ruby configuration.

```Ruby
def ruby_install_name
  rb_config["ruby_install_name"]
end
```

--------------------------------

### Bundler Module Overview

Source: https://docs.ruby-lang.org/en/master/Bundler

Provides an overview of the Bundler module and its basic usage for setting up project environments.

```APIDOC
## Bundler Module Overview

`Bundler` provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed.
`Bundler` is a part of Ruby’s standard library.
`Bundler` is used by creating _gemfiles_ listing all the project dependencies and (optionally) their versions and then using:

```ruby
require 'bundler/setup'
```

or `Bundler.setup` to setup environment where only specified gems and their specified versions could be used.

See Bundler website for extensive documentation on gemfiles creation and `Bundler` usage.

As a standard library inside project, `Bundler` could be used for introspection of loaded and required modules.
```

--------------------------------

### Get Start Column (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Calculates the column number in bytes where the location starts, relative to the beginning of the line.

```ruby
def start_column
  source.column(start_offset)
end
```

--------------------------------

### Get Path Examples

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/UnpackCommand

Demonstrates the usage of the `get_path` method with different arguments, showing successful retrieval of gem paths and cases where `nil` is returned.

```ruby
get_path 'rake', '> 0.4' # "/usr/lib/ruby/gems/1.8/cache/rake-0.4.2.gem"
get_path 'rake', '< 0.1' # nil
get_path 'rak'           # nil (exact name required)
```

--------------------------------

### Get OpenSSL Digest Size Example (Ruby)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/Digest

Demonstrates how to get the digest length of a SHA1 digest using the OpenSSL library in Ruby.

```ruby
digest = OpenSSL::Digest.new('SHA1')
puts digest.digest_length # => 20
```

--------------------------------

### Install Git Gem using Gem::Installer

Source: https://docs.ruby-lang.org/en/master/Gem/Resolver/GitSpecification

Demonstrates the `install` method of `Gem::Resolver::GitSpecification`. This method utilizes `Gem::Installer` to handle the installation process, including building extensions and running hooks. It requires the `rubygems/installer` library.

```ruby
def install(options = {})
  require_relative "../installer"

  installer = Gem::Installer.for_spec spec, options

  yield installer if block_given?

  installer.run_pre_install_hooks
  installer.build_extensions
  installer.run_post_build_hooks
  installer.generate_bin
  installer.run_post_install_hooks
end
```

--------------------------------

### Get Installed Gem Specifications

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Retrieves an array of Gem::Specification objects for all gems installed in the `gem_home`. It does this by globbing for .gemspec files in the specifications directory and loading each one.

```ruby
def installed_specs
  @installed_specs ||= begin
    specs = []

    Gem::Util.glob_files_in_dir("*.gemspec", File.join(gem_home, "specifications")).each do |path|
      spec = Gem::Specification.load path
      specs << spec if spec
    end

    specs
  end
end
```

--------------------------------

### Get Start Column of Node (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Node

Returns the starting column of the node. This is a delegate method to the `start_column` of the associated location object.

```ruby
def start_column
  location.start_column
end
```

--------------------------------

### Get Gem Installation Directory

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/ContentsCommand

Retrieves and displays the installation directory for a specified gem. It finds the gem's specification and then prints the `gem_dir` attribute.

```ruby
def gem_install_dir(name)
  spec = spec_for name

  return false unless spec

  say spec.gem_dir

  true
end
```

--------------------------------

### Setup Gem Signing - Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Package

Prepares the gem for signing and checksum generation. It sets up a `Gem::Security::Signer` instance using the signing key, certificate chain, and passphrase from the environment. If no signing key is present, it defaults to setting up for checksum generation only.

```ruby
def setup_signer(signer_options: {})
  passphrase = ENV["GEM_PRIVATE_KEY_PASSPHRASE"]
  if @spec.signing_key
    @signer =
      Gem::Security::Signer.new(
        @spec.signing_key,
        @spec.cert_chain,
        passphrase,
        signer_options
      )

    @spec.signing_key = nil
    @spec.cert_chain = @signer.cert_chain.map(&:to_s)
  else
    @signer = Gem::Security::Signer.new nil, nil, passphrase
    @spec.cert_chain = @signer.cert_chain.map(&:to_pem) if
      @signer.cert_chain
  end
end
```

--------------------------------

### Initialize and Add to Gem::SourceList (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/SourceList

Shows the process of creating a new Gem::SourceList and adding sources to it one by one.

```Ruby
sources = Gem::SourceList.new
sources << 'https://rubygems.example'
```

--------------------------------

### Get Start Character Column (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Calculates the column number in characters where this location starts, relative to the beginning of the line.

```ruby
def start_character_column
  source.character_column(start_offset)
end
```

--------------------------------

### Get OpenSSL Digest Block Length Example (Ruby)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/Digest

Demonstrates how to get the block length of a SHA1 digest using the OpenSSL library in Ruby.

```ruby
digest = OpenSSL::Digest.new('SHA1')
puts digest.block_length # => 64
```

--------------------------------

### Example: Get File Timestamps

Source: https://docs.ruby-lang.org/en/master/File/Stat

Demonstrates retrieving birthtime, mtime, ctime, and atime for a file. The example includes writing to the file and sleeping to ensure distinct timestamps.

```ruby
File.write("testfile", "foo")
sleep 10
File.write("testfile", "bar")
sleep 10
File.chmod(0644, "testfile")
sleep 10
File.read("testfile")
File.stat("testfile").birthtime   #=> 2014-02-24 11:19:17 +0900
File.stat("testfile").mtime       #=> 2014-02-24 11:19:27 +0900
File.stat("testfile").ctime       #=> 2014-02-24 11:19:37 +0900
File.stat("testfile").atime       #=> 2014-02-24 11:19:47 +0900
```

--------------------------------

### Get the directory for installed gems

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Determines and returns the directory where gems are installed. It constructs this path by joining the base directory with 'gems'.

```ruby
def gems_dir
  @gems_dir ||= File.join(base_dir, "gems")
end
```

--------------------------------

### Compile Ruby Code Examples

Source: https://docs.ruby-lang.org/en/master/RubyVM/InstructionSequence

Provides examples of using `RubyVM::InstructionSequence.compile` to compile different forms of Ruby code, including simple strings and code read from files, demonstrating how to provide metadata like file paths.

```ruby
RubyVM::InstructionSequence.compile("a = 1 + 2")
#=> <RubyVM::InstructionSequence:<compiled>@<compiled>>

path = "test.rb"
RubyVM::InstructionSequence.compile(File.read(path), path, File.expand_path(path))
#=> <RubyVM::InstructionSequence:<compiled>@test.rb:1>

file = File.open("test.rb")
RubyVM::InstructionSequence.compile(file)
#=> <RubyVM::InstructionSequence:<compiled>@<compiled>:1>

path = File.expand_path("test.rb")
RubyVM::InstructionSequence.compile(File.read(path), path, path)
#=> <RubyVM::InstructionSequence:<compiled>@/absolute/path/to/test.rb:1>
```

--------------------------------

### Ruby: Managing HTTP Sessions

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Provides an example of managing HTTP sessions using `Net::HTTP.start`. This approach is more efficient for making multiple requests to the same host, as it reuses the connection.

```ruby
Net::HTTP.start(hostname) do |http|
  # Session started automatically before block execution.
  http.get(path)
  http.head(path)
  body = 'Some text'
  http.post(path, body)  # Can also have a block.
  http.put(path, body)
  http.delete(path)
  http.options(path)
  http.trace(path)
  http.patch(path, body) # Can also have a block.
  http.copy(path)
  http.lock(path, body)
  http.mkcol(path, body)
  http.move(path)
  http.propfind(path, body)
  http.proppatch(path, body)
  http.unlock(path, body)
  # Session finished automatically at block exit.
end
```

--------------------------------

### Get Start Line of Node (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Node

Returns the starting line number of the node. This method delegates to the `start_line` of the associated location object.

```ruby
def start_line
  location.start_line
end
```

--------------------------------

### Sample Ruby File

Source: https://docs.ruby-lang.org/en/master/RubyVM/InstructionSequence

A simple 'Hello, world!' Ruby program that can be compiled using `RubyVM::InstructionSequence.compile_file`.

```ruby
puts "Hello, world!"

```

--------------------------------

### Get Bundler Gems Install Path (Ruby)

Source: https://docs.ruby-lang.org/en/master/Bundler

Returns the path where gems are installed by Bundler, usually located within the Bundler home directory.

```ruby
def install_path
  home.join("gems")
end
```

--------------------------------

### Get Start Character Offset of Node (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Node

Returns the starting character offset of the node from the beginning of the source. This delegates to the associated location object.

```ruby
def start_character_offset
  location.start_character_offset
end
```

--------------------------------

### Install Gem with RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Installs a gem by performing pre-installation checks, running hooks, managing gem directories, extracting files, building extensions, and generating necessary files like specifications and cache entries. It returns a loaded Gem::Specification for the installed gem.

```ruby
def install
  pre_install_checks

  run_pre_install_hooks

  # Set loaded_from to ensure extension_dir is correct
  if @options[:install_as_default]
    spec.loaded_from = default_spec_file
  else
    spec.loaded_from = spec_file
  end

  # Completely remove any previous gem files
  FileUtils.rm_rf gem_dir
  FileUtils.rm_rf spec.extension_dir

  dir_mode = options[:dir_mode]
  FileUtils.mkdir_p gem_dir, mode: dir_mode && 0o755

  if @options[:install_as_default]
    extract_bin
    write_default_spec
  else
    extract_files

    build_extensions
    write_build_info_file
    run_post_build_hooks
  end

  generate_bin
  generate_plugins

  unless @options[:install_as_default]
    write_spec
    write_cache_file
  end

  File.chmod(dir_mode, gem_dir) if dir_mode

  say spec.post_install_message if options[:post_install_message] && !spec.post_install_message.nil?

  Gem::Specification.add_spec(spec) unless @install_dir

  load_plugin

  run_post_install_hooks

  spec
rescue Errno::EACCES => e
  # Permission denied - /path/to/foo
  raise Gem::FilePermissionError, e.message.split(" - ").last
end
```

--------------------------------

### Ruby MonitorMixin: Public Class Methods - initialize

Source: https://docs.ruby-lang.org/en/master/MonitorMixin

Illustrates the initialization of MonitorMixin. It's noted that 'extend MonitorMixin' or 'include MonitorMixin' should be used instead of directly calling this constructor. This method ensures the monitor is properly set up.

```ruby
# File ext/monitor/lib/monitor.rb, line 222
def initialize(...)
  super
  mon_initialize
end

```

--------------------------------

### Ruby Net::HTTP::Get GET Request Example

Source: https://docs.ruby-lang.org/en/master/Net/HTTP/Get

Demonstrates how to create and use the Net::HTTP::Get class to send a GET request to a specified URI. It requires the 'net/http' library and shows how to initiate the HTTP connection and send the request.

```ruby
require 'net/http'
uri = URI('http://example.com')
hostname = uri.hostname # => "example.com"
req = Net::HTTP::Get.new(uri) # => #<Net::HTTP::Get GET>
res = Net::HTTP.start(hostname) do |http|
  http.request(req)
end

```

--------------------------------

### WebauthnListener Example - RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem/GemcutterUtilities

Example usage of the WebauthnListener to retrieve an OTP. It starts a listener thread, joins it, and then accesses the OTP or error from the thread's data.

```Ruby
thread = Gem::WebauthnListener.listener_thread("https://rubygems.example", server)
thread.join
otp = thread[:otp]
error = thread[:error]
```

--------------------------------

### SyntaxSuggest::Cli Initialization (Ruby)

Source: https://docs.ruby-lang.org/en/master/SyntaxSuggest/Cli

Shows the constructor for SyntaxSuggest::Cli, highlighting dependency injection for testing and how environment variables or debug flags influence options like record directory and terminal highlighting.

```ruby
# File lib/syntax_suggest/cli.rb, line 20
def initialize(argv:, exit_obj: Kernel, io: $stdout, env: ENV)
  @options = {}
  @parser = nil
  options[:record_dir] = env["SYNTAX_SUGGEST_RECORD_DIR"]
  options[:record_dir] = "tmp" if env["DEBUG"]
  options[:terminal] = SyntaxSuggest::DEFAULT_VALUE

  @io = io
  @argv = argv
  @exit_obj = exit_obj
end
```

--------------------------------

### Display Release Notes in RubyGems Setup Command

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Displays the release notes by reading the 'CHANGELOG.md' file. It parses the file to extract version information and changes made since the previous version, formatting the output for the user. It handles cases where the changelog file might not exist.

```ruby
def show_release_notes
  release_notes = File.join Dir.pwd, "CHANGELOG.md"

  release_notes =
    if File.exist? release_notes
      history = File.read release_notes

      history.force_encoding Encoding::UTF_8

      text = history.split(HISTORY_HEADER)
      text.shift # correct an off-by-one generated by split
      version_lines = history.scan(HISTORY_HEADER)
      versions = history.scan(VERSION_MATCHER).flatten.map do |x|
        Gem::Version.new(x)
      end

      history_string = ""

      until versions.length == 0 ||
            versions.shift <= options[:previous_version] do
        history_string += version_lines.shift + text.shift
      end

      history_string
    else
      "Oh-no! Unable to find release notes!"
    end

  say release_notes
end
```

--------------------------------

### Get Start Character Column of Node (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Node

Returns the starting character column of the node within its line. This delegates to the associated location object.

```ruby
def start_character_column
  location.start_character_column
end
```

--------------------------------

### Get Specifications from Directory (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/RequestSet

Retrieves a list of installed gem specifications from a specified directory. This is often used to check for existing gems before attempting a new installation.

```ruby
def specs_in(dir)
  # Implementation not provided in the snippet
end
```

--------------------------------

### Ruby Array Slice! with Start and Length (Usage)

Source: https://docs.ruby-lang.org/en/master/Array

Demonstrates the usage of Array#slice! with start and length arguments. Shows how it removes multiple elements and returns them, including examples with positive/negative start indices and edge cases like exceeding array bounds.

```ruby
a = ['a', 'b', 'c', 'd']
a.slice!(1, 2)     # => ["b", "c"]
a                  # => ["a", "d"]
a.slice!(0.1, 1.1) # => ["a"]
a                  # => ["d"]
```

```ruby
a = ['a', 'b', 'c', 'd']
a.slice!(-2, 1) # => ["c"]
a               # => ["a", "b", "d"]
```

```ruby
a = ['a', 'b', 'c', 'd']
a.slice!(2, 50) # => ["c", "d"]
a               # => ["a", "b"]
```

```ruby
a = ['a', 'b', 'c', 'd']
a.slice!(4, 0) # => []
a               # => ["a", "b", "c", "d"]
```

--------------------------------

### Example Usage of Gem::UserInteraction

Source: https://docs.ruby-lang.org/en/master/Gem/UserInteraction

Demonstrates how to include the Gem::UserInteraction module in a class and use its methods, such as 'ask', to interact with the user. This example shows a simple way to get input from the user.

```Ruby
class X
  include Gem::UserInteraction

  def get_answer
    n = ask("What is the meaning of life?")
  end
end
```

--------------------------------

### Install RubyGems RDoc and ri Documentation

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Installs RDoc and ri documentation for RubyGems. It checks for write permissions on the documentation directory and removes old RDoc directories before generating new ones. It requires the 'rdoc' gem to be available.

```ruby
def install_rdoc
  gem_doc_dir = File.join Gem.dir, "doc"
  rubygems_name = "rubygems-#{Gem::VERSION}"
  rubygems_doc_dir = File.join gem_doc_dir, rubygems_name

  begin
    Gem.ensure_gem_subdirectories Gem.dir
  rescue SystemCallError
    # ignore
  end

  if File.writable?(gem_doc_dir) &&
     (!File.exist?(rubygems_doc_dir) ||
      File.writable?(rubygems_doc_dir))
    say "Removing old RubyGems RDoc and ri" if @verbose
    Dir[File.join(Gem.dir, "doc", "rubygems-[0-9]*")].each do |dir|
      rm_rf dir
    end

    require_relative "../rdoc"

    return false unless defined?(Gem::RDoc)

    fake_spec = Gem::Specification.new "rubygems", Gem::VERSION
    def fake_spec.full_gem_path
      File.expand_path "../../..", __dir__
    end

    generate_ri   = options[:document].include? "ri"
    generate_rdoc = options[:document].include? "rdoc"

    rdoc = Gem::RDoc.new fake_spec, generate_rdoc, generate_ri
    rdoc.generate

    return true
  elsif @verbose
    say "Skipping RDoc generation, #{gem_doc_dir} not writable"
    say "Set the GEM_HOME environment variable if you want RDoc generated"
  end

  false
end
```

--------------------------------

### Get Gem Installation Directory in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Returns the installation directory for the gem. This method provides the path where the gem's files are intended to be placed.

```ruby
def dir
  gem_dir.to_s
end
```

--------------------------------

### Complete Ruby OptParse Example

Source: https://docs.ruby-lang.org/en/master/OptionParser

This Ruby code demonstrates a full program using the optparse library to parse command-line arguments. It defines multiple options for various functionalities like in-place editing, specifying delays, execution times, record separators, lists, encoding, and verbose output. It also includes standard help and version flags.

```ruby
require 'optparse'
require 'optparse/time'
require 'ostruct'
require 'pp'

class OptparseExample
  Version = '1.0.0'

  CODES = %w[iso-2022-jp shift_jis euc-jp binary]
  CODE_ALIASES = { "jis" => "iso-2022-jp", "sjis" => "shift_jis" }

  class ScriptOptions
    attr_accessor :library, :inplace, :encoding, :transfer_type,
                  :verbose, :extension, :delay, :time, :record_separator,
                  :list

    def initialize
      self.library = []
      self.inplace = false
      self.encoding = "utf8"
      self.transfer_type = :auto
      self.verbose = false
    end

    def define_options(parser)
      parser.banner = "Usage: example.rb [options]"
      parser.separator ""
      parser.separator "Specific options:"

      # add additional options
      perform_inplace_option(parser)
      delay_execution_option(parser)
      execute_at_time_option(parser)
      specify_record_separator_option(parser)
      list_example_option(parser)
      specify_encoding_option(parser)
      optional_option_argument_with_keyword_completion_option(parser)
      boolean_verbose_option(parser)

      parser.separator ""
      parser.separator "Common options:"
      # No argument, shows at tail.  This will print an options summary.
      # Try it and see!
      parser.on_tail("-h", "--help", "Show this message") do
        puts parser
        exit
      end
      # Another typical switch to print the version.
      parser.on_tail("--version", "Show version") do
        puts Version
        exit
      end
    end

    def perform_inplace_option(parser)
      # Specifies an optional option argument
      parser.on("-i", "--inplace [EXTENSION]",
                "Edit ARGV files in place",
                "(make backup if EXTENSION supplied)") do |ext|
        self.inplace = true
        self.extension = ext || ''
        self.extension.sub!(/\A\.?(?=.)/, ".")  # Ensure extension begins with dot.
      end
    end

    def delay_execution_option(parser)
      # Cast 'delay' argument to a Float.
      parser.on("--delay N", Float, "Delay N seconds before executing") do |n|
        self.delay = n
      end
    end

    def execute_at_time_option(parser)
      # Cast 'time' argument to a Time object.
      parser.on("-t", "--time [TIME]", Time, "Begin execution at given time") do |time|
        self.time = time
      end
    end

    def specify_record_separator_option(parser)
      # Cast to octal integer.
      parser.on("-F", "--irs [OCTAL]", OptionParser::OctalInteger,
                "Specify record separator (default \0)") do |rs|
        self.record_separator = rs
      end
    end

    def list_example_option(parser)
      # List of arguments.
      parser.on("--list x,y,z", Array, "Example 'list' of arguments") do |list|
        self.list = list
      end
    end

    def specify_encoding_option(parser)
      # Keyword completion.  We are specifying a specific set of arguments (CODES
      # and CODE_ALIASES - notice the latter is a Hash), and the user may provide
      # the shortest unambiguous text.
      code_list = (CODE_ALIASES.keys + CODES).join(', ')
      parser.on("--code CODE", CODES, CODE_ALIASES, "Select encoding",
                "(#{code_list})") do |encoding|
        self.encoding = encoding
      end
    end

    def optional_option_argument_with_keyword_completion_option(parser)
      # Optional '--type' option argument with keyword completion.
      parser.on("--type [TYPE]", [:text, :binary, :auto],
                "Select transfer type (text, binary, auto)") do |t|
        self.transfer_type = t
      end
    end

    def boolean_verbose_option(parser)
      # Boolean switch.
      parser.on("-v", "--[no-]verbose", "Run verbosely") do |v|
        self.verbose = v
      end
    end
  end

  #
  # Return a structure describing the options.
  #
  def parse(args)
    # The options specified on the command line will be collected in
    # *options*.

    @options = ScriptOptions.new
    @args = OptionParser.new do |parser|
      @options.define_options(parser)
      parser.parse!(args)
    end
    @options
  end

  attr_reader :parser, :options
end  # class OptparseExample

example = OptparseExample.new
options = example.parse(ARGV)
pp options # example.options
pp ARGV

```

--------------------------------

### Get Line Start Offset in Ruby

Source: https://docs.ruby-lang.org/en/master/Prism/Source

Returns the byte offset of the start of a line given its byte offset. It uses the `find_line` method and the `offsets` array.

```ruby
# File lib/prism/parse_result.rb, line 87
def line_start(byte_offset)
  offsets[find_line(byte_offset)]
end
```

--------------------------------

### Set up SSL Server and Handle Connections (Ruby)

Source: https://docs.ruby-lang.org/en/master/OpenSSL

Establishes an SSL server using Ruby's OpenSSL library. It configures an SSL context with a certificate and private key, then binds to a TCP port. The server listens for incoming connections, accepts them, reads data, sends a response, and closes the connection.

```ruby
require 'socket'

context = OpenSSL::SSL::SSLContext.new
context.cert = cert
context.key = key

tcp_server = TCPServer.new 5000
ssl_server = OpenSSL::SSL::SSLServer.new tcp_server, context

loop do
  ssl_connection = ssl_server.accept

  data = ssl_connection.gets

  response = "I got #{data.dump}"
  puts response

  ssl_connection.puts "I got #{data.dump}"
  ssl_connection.close
end
```

--------------------------------

### Get Start Offset of Node (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Node

Calculates and returns the starting offset of the node in the source. It handles cases where the location might not be a standard Location object.

```ruby
def start_offset
  location = @location
  location.is_a?(Location) ? location.start_offset : location >> 32
end
```

--------------------------------

### Get Binstub Installation Path

Source: https://docs.ruby-lang.org/en/master/Bundler

Returns the absolute path where binstubs are installed. It defaults to a 'bin' directory within the project's root if not otherwise configured. Creates the directory if it doesn't exist.

```ruby
# File lib/bundler.rb, line 119
def bin_path
  @bin_path ||= begin
    path = Bundler.settings[:bin] || "bin"
    path = Pathname.new(path).expand_path(root).expand_path
    mkdir_p(path)
    path
  end
end
```

--------------------------------

### Initialize RubyGems ExecCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/ExecCommand

Initializes the RubyGems ExecCommand, setting up command-line options for specifying the gem, version, and installation behavior.

```ruby
# File lib/rubygems/commands/exec_command.rb, line 12
def initialize
  super "exec", "Run a command from a gem", {
    version: Gem::Requirement.default,
  }

  add_version_option
  add_prerelease_option "to be installed"

  add_option "-g", "--gem GEM", "run the executable from the given gem" do |value, options|
    options[:gem_name] = value
  end

  add_option( :"Install/Update", "--conservative",
    "Prefer the most recent installed version, ",
    "rather than the latest version overall") do |_value, options|
    options[:conservative] = true
  end
end
```

--------------------------------

### Create RubyGems Destination Directories

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Ensures that the necessary library and binary directories for RubyGems are created. If default directories are not found, it generates them. The directories are created with read, write, and execute permissions for the owner.

```ruby
def make_destination_dirs
  lib_dir, bin_dir = Gem.default_rubygems_dirs

  unless lib_dir
    lib_dir, bin_dir = generate_default_dirs
  end

  mkdir_p lib_dir, mode: 0o755
  mkdir_p bin_dir, mode: 0o755

  [lib_dir, bin_dir]
end
```

--------------------------------

### Get Start Code Units Offset (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Retrieves the offset from the start of the file in code units for the beginning of the location, supporting different encodings.

```ruby
def start_code_units_offset(encoding = Encoding::UTF_16LE)
  source.code_units_offset(start_offset, encoding)
end
```

--------------------------------

### Get Latest Installed Gem Specifications

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Retrieves a list of the latest installed gem specifications. An optional boolean parameter can be passed to include prerelease versions in the results.

```ruby
def self.latest_specs(prerelease = false)
  specification_record.latest_specs(prerelease)
end
```

--------------------------------

### Example Usage of Etc.uname (Ruby)

Source: https://docs.ruby-lang.org/en/master/Etc

Demonstrates how to use the `Etc.uname` method in Ruby to fetch and display system information. The output is a hash containing system details.

```ruby
require 'etc'
require 'pp'

pp Etc.uname()
#=> {:sysname=>"Linux",
#    :nodename=>"boron",
#    :release=>"2.6.18-6-xen-686",
#    :version=>"#1 SMP Thu Nov 5 19:54:42 UTC 2009",
#    :machine=>"i686"}

```

--------------------------------

### Get Primary Installed Gems (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/CleanupCommand

Identifies the primary (latest) version for each installed gem. It iterates through all specifications and stores the highest version found for each gem name.

```ruby
# File lib/rubygems/commands/cleanup_command.rb, line 140
def get_primary_gems
  @primary_gems = {}

  Gem::Specification.each do |spec|
    if @primary_gems[spec.name].nil? ||
       @primary_gems[spec.name].version < spec.version
      @primary_gems[spec.name] = spec
    end
  end
end
```

--------------------------------

### Generate Basic Help Text with OptionParser

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Demonstrates how to use OptionParser to define command-line options and generate basic help text. It includes defining short and long option names, dummy arguments, and descriptions.

```ruby
require 'optparse'
parser = OptionParser.new
parser.on(
  '-x', '--xxx',
  'Adipiscing elit. Aenean commodo ligula eget.',
  'Aenean massa. Cum sociis natoque penatibus',
  )
parser.on(
  '-y', '--yyy YYY',
  'Lorem ipsum dolor sit amet, consectetuer.'
)
parser.on(
  '-z', '--zzz [ZZZ]',
  'Et magnis dis parturient montes, nascetur',
  'ridiculus mus. Donec quam felis, ultricies',
  'nec, pellentesque eu, pretium quis, sem.',
  )
parser.parse!
```

--------------------------------

### Example of Receiving Data with UNIXSocket in Ruby

Source: https://docs.ruby-lang.org/en/master/UNIXSocket

This Ruby example demonstrates receiving data from a UNIX domain socket. It sets up two sockets, binds them to different addresses, and then uses `recvfrom` to get data sent from one socket to another.

```ruby
s1 = Socket.new(:UNIX, :DGRAM, 0)
s1_ai = Addrinfo.unix("/tmp/sock1")
s1.bind(s1_ai)

s2 = Socket.new(:UNIX, :DGRAM, 0)
s2_ai = Addrinfo.unix("/tmp/sock2")
s2.bind(s2_ai)
s3 = UNIXSocket.for_fd(s2.fileno)

s1.send "a", 0, s2_ai
p s3.recvfrom(10) #=> ["a", ["AF_UNIX", "/tmp/sock1"]]


```

--------------------------------

### Initialize OpenSSL::X509::Store with Default Paths (Ruby)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/X509/Store

Creates a new X509::Store and loads the system's default CA certificates. This is the simplest way to set up a trusted certificate store.

```ruby
cert_store = OpenSSL::X509::Store.new
cert_store.set_default_paths
```

--------------------------------

### Get Bundle Installation Path

Source: https://docs.ruby-lang.org/en/master/Bundler

Returns the absolute path on the filesystem where gems are installed. This path is determined by Bundler's settings and expanded relative to the project's root directory.

```ruby
# File lib/bundler.rb, line 101
def bundle_path
  @bundle_path ||= Pathname.new(configured_bundle_path.path).expand_path(root)
end
```

--------------------------------

### Example Usage of DateTime.now (Ruby)

Source: https://docs.ruby-lang.org/en/master/DateTime

Demonstrates how to call the DateTime.now method and shows an example of the output.

```Ruby
DateTime.now              #=> #<DateTime: 2011-06-11T21:20:44+09:00 ...>
```

--------------------------------

### Create a YAML Document Object Example

Source: https://docs.ruby-lang.org/en/master/Psych/Nodes/Document

This example demonstrates how to create a YAML document object representing a YAML 1.1 document with a specific tag directive and an implicit start.

```Ruby
Psych::Nodes::Document.new(
  [1,1],
  ["!", "tag:tenderlovemaking.com,2009:"]],
  true
)
```

--------------------------------

### Get Installed Gem Stubs (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/SpecificationRecord

Retrieves stub specifications that are currently installed based on a provided pattern. It uses `map_stubs` to process paths and generate `Gem::StubSpecification` objects.

```ruby
def installed_stubs(pattern)
  map_stubs(pattern) do |path, base_dir, gems_dir|
    Gem::StubSpecification.gemspec_stub(path, base_dir, gems_dir)
  end
end
```

--------------------------------

### Instantiate and Execute BeforeAfterKeywordEnds

Source: https://docs.ruby-lang.org/en/master/SyntaxSuggest/Capture/BeforeAfterKeywordEnds

Example of how to instantiate and call the BeforeAfterKeywordEnds class with provided code lines and a block. This demonstrates the typical usage pattern for analyzing code structure.

```ruby
lines = BeforeAfterKeywordEnds.new(
  block: block,
  code_lines: code_lines
).call()

```

--------------------------------

### Spawn Executable with Arguments in Ruby

Source: https://docs.ruby-lang.org/en/master/Process

Shows how to spawn an executable and pass arguments or options to it. Multiple arguments can be provided after the executable path.

```ruby
spawn('echo', 'C*')             # => 799392
Process.wait                    # => 799392
spawn('echo', 'hello', 'world') # => 799393
Process.wait                    # => 799393

```

--------------------------------

### Get Start Code Units Column (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Calculates the column number in code units of the specified encoding where this location starts, relative to the line's beginning.

```ruby
def start_code_units_column(encoding = Encoding::UTF_16LE)
  source.code_units_column(start_offset, encoding)
end
```

--------------------------------

### Gem Installation Hooks

Source: https://docs.ruby-lang.org/en/master/Gem

Allows users to register callback hooks that execute at various stages of the gem installation, uninstallation, and reset processes.

```APIDOC
## Gem.post_build (&hook)

### Description
Adds a post-build hook that will be passed an `Gem::Installer` instance when `Gem::Installer#install` is called. The hook is called after the gem has been extracted and extensions have been built but before the executables or gemspec has been written. If the hook returns `false`, the gem’s files will be removed and the install will be aborted.

### Method
POST

### Endpoint
`/gems/hooks/post_build`

### Parameters
#### Request Body
- **hook** (function) - The callback function to execute after a gem build.

### Request Example
```json
{
  "hook": "lambda { |installer| puts 'Gem build finished.' }"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

### Response Example
```json
{
  "message": "Post-build hook registered successfully."
}
```
```

```APIDOC
## Gem.post_install (&hook)

### Description
Adds a post-install hook that will be passed an `Gem::Installer` instance when `Gem::Installer#install` is called.

### Method
POST

### Endpoint
`/gems/hooks/post_install`

### Parameters
#### Request Body
- **hook** (function) - The callback function to execute after a gem is installed.

### Request Example
```json
{
  "hook": "lambda { |installer| puts 'Gem installed successfully.' }"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

### Response Example
```json
{
  "message": "Post-install hook registered successfully."
}
```
```

```APIDOC
## Gem.post_reset (&hook)

### Description
Adds a hook that will be run after `Gem::Specification.reset` is run.

### Method
POST

### Endpoint
`/gems/hooks/post_reset`

### Parameters
#### Request Body
- **hook** (function) - The callback function to execute after a specification reset.

### Request Example
```json
{
  "hook": "lambda { puts 'Specifications were reset.' }"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

### Response Example
```json
{
  "message": "Post-reset hook registered successfully."
}
```
```

```APIDOC
## Gem.post_uninstall (&hook)

### Description
Adds a post-uninstall hook that will be passed a `Gem::Uninstaller` instance and the spec that was uninstalled when `Gem::Uninstaller#uninstall` is called.

### Method
POST

### Endpoint
`/gems/hooks/post_uninstall`

### Parameters
#### Request Body
- **hook** (function) - The callback function to execute after a gem is uninstalled.

### Request Example
```json
{
  "hook": "lambda { |uninstaller, spec| puts "#{spec.name} uninstalled."} "
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

### Response Example
```json
{
  "message": "Post-uninstall hook registered successfully."
}
```
```

```APIDOC
## Gem.pre_install (&hook)

### Description
Adds a pre-install hook that will be passed an `Gem::Installer` instance when `Gem::Installer#install` is called.

### Method
POST

### Endpoint
`/gems/hooks/pre_install`

### Parameters
#### Request Body
- **hook** (function) - The callback function to execute before a gem is installed.

### Request Example
```json
{
  "hook": "lambda { |installer| puts 'About to install gem.' }"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

### Response Example
```json
{
  "message": "Pre-install hook registered successfully."
}
```
```

--------------------------------

### Get Latest Installed Gem Specification by Name

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Returns the most recently installed specification for a gem identified by its name. It queries the specification records to find the latest version.

```ruby
def self.latest_spec_for(name)
  specification_record.latest_spec_for(name)
end
```

--------------------------------

### Execute Newly Compiled Ruby Version

Source: https://docs.ruby-lang.org/en/master/contributing/building_ruby_md

This command demonstrates how to run a simple Ruby script ('puts 'Hello, World!'') using the newly installed Ruby executable, located at ~/.rubies/ruby-master/bin/ruby. This verifies that the installation was successful.

```shell
~/.rubies/ruby-master/bin/ruby -e "puts 'Hello, World!'"
```

--------------------------------

### Ruby: Install a locally installed gem specification

Source: https://docs.ruby-lang.org/en/master/Gem/Resolver/InstalledSpecification

The `install` method for `InstalledSpecification` performs a null install because the gem is already present. It accepts options but ignores them and yields nil.

```ruby
# File lib/rubygems/resolver/installed_specification.rb, line 18
def install(options = {})
  yield nil
end
```

--------------------------------

### Gem::DependencyInstaller - Initialization

Source: https://docs.ruby-lang.org/en/master/Gem/DependencyInstaller

Initializes a new Gem::DependencyInstaller instance with optional configuration settings.

```APIDOC
## POST /gems/install

### Description
Initializes a new Gem::DependencyInstaller instance. This installer is responsible for installing a gem and all of its dependencies from local and remote sources.

### Method
POST

### Endpoint
/gems/install

### Parameters
#### Request Body
- **options** (object) - Optional - Configuration options for the installer.
  - **cache_dir** (string) - Optional - Alternate repository path to store .gem files.
  - **domain** (string) - Optional - Specifies where to search for gems (:local, :remote, or :both).
  - **env_shebang** (boolean) - Optional - Whether to use environment shebangs.
  - **force** (boolean) - Optional - Forces installation even if the gem is already present.
  - **format_executable** (boolean) - Optional - Formats executables for the gem.
  - **ignore_dependencies** (boolean) - Optional - Skips installation of dependencies.
  - **install_dir** (string) - Optional - The directory where gems will be installed.
  - **prerelease** (boolean) - Optional - Allows installation of prerelease versions.
  - **security_policy** (string) - Optional - The security policy to apply during installation.
  - **user_install** (boolean) - Optional - Installs gems for the current user.
  - **wrappers** (boolean) - Optional - Creates wrapper executables.
  - **build_args** (string) - Optional - Arguments to pass during the build process.
  - **build_docs_in_background** (boolean) - Optional - Builds documentation in a background process.
  - **install_as_default** (boolean) - Optional - Installs the gem as the default version.
  - **dir_mode** (string) - Optional - Sets the directory permissions.
  - **data_mode** (string) - Optional - Sets the data file permissions.
  - **prog_mode** (string) - Optional - Sets the program file permissions.
  - **minimal_deps** (boolean) - Optional - Installs only the minimal required dependencies.

### Request Example
```json
{
  "options": {
    "install_dir": "/usr/local/lib/ruby/gems/3.0.0",
    "domain": "remote",
    "prerelease": true,
    "force": false
  }
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the installer was initialized.

#### Response Example
```json
{
  "message": "Gem::DependencyInstaller initialized successfully."
}
```
```

--------------------------------

### Initialize Gem Install Command

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/InstallCommand

Initializes the `Gem::Commands::InstallCommand` with default options and adds various command-line options for installation control.

```ruby
# File lib/rubygems/commands/install_command.rb, line 24
def initialize
  defaults = Gem::DependencyInstaller::DEFAULT_OPTIONS.merge({
    format_executable: false,
    lock: true,
    suggest_alternate: true,
    version: Gem::Requirement.default,
    without_groups: [],
  })

  defaults.merge!(install_update_options)

  super "install", "Install a gem into the local repository", defaults

  add_install_update_options
  add_local_remote_options
  add_platform_option
  add_version_option
  add_prerelease_option "to be installed. (Only for listed gems)"

  @installed_specs = []
end
```

--------------------------------

### Get Gem Specification File Path in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Returns the full path to the installed gem's specification file (.gemspec). This is used to locate the metadata associated with a particular gem installation.

```Ruby
def spec_file
  File.join gem_home, "specifications", "#{spec.full_name}.gemspec"
end
```

--------------------------------

### Initialize Gem::Commands::PristineCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/PristineCommand

Initializes the PristineCommand with a description and various options for restoring gems. It sets up options for restoring all gems, skipping specific gems, handling extensions, and specifying installation directories. This method calls the superclass method `Gem::Command::new`.

```ruby
# File lib/rubygems/commands/pristine_command.rb, line 11
def initialize
  super "pristine",
        "Restores installed gems to pristine condition from files located in the gem cache",
        version: Gem::Requirement.default,
        extensions: true,
        extensions_set: false,
        all: false

  add_option("--all",
             "Restore all installed gems to pristine",
             "condition") do |value, options|
    options[:all] = value
  end

  add_option("--skip=gem_name",
             "used on --all, skip if name == gem_name") do |value, options|
    options[:skip] ||=[]
    options[:skip] << value
  end

  add_option("--[no-]extensions",
             "Restore gems with extensions",
             "in addition to regular gems") do |value, options|
    options[:extensions_set] = true
    options[:extensions]     = value
  end

  add_option("--only-missing-extensions",
             "Only restore gems with missing extensions") do |value, options|
    options[:only_missing_extensions] = value
  end

  add_option("--only-executables",
             "Only restore executables") do |value, options|
    options[:only_executables] = value
  end

  add_option("--only-plugins",
             "Only restore plugins") do |value, options|
    options[:only_plugins] = value
  end

  add_option("-E", "--[no-]env-shebang",
             "Rewrite executables with a shebang",
             "of /usr/bin/env") do |value, options|
    options[:env_shebang] = value
  end

  add_option("-i", "--install-dir DIR",
             "Gem repository to get gems restored") do |value, options|
    options[:install_dir] = File.expand_path(value)
  end

  add_option("-n", "--bindir DIR",
             "Directory where executables are",
             "located") do |value, options|
    options[:bin_dir] = File.expand_path(value)
  end

  add_version_option("restore to", "pristine condition")
end

```

--------------------------------

### Coverage.start

Source: https://docs.ruby-lang.org/en/master/Coverage

Sets up the coverage measurement. This method does not start the measurement itself. Use `Coverage.resume` to start the measurement.

```APIDOC
## Coverage.start

### Description
Sets up the coverage measurement. This method does not start the measurement itself. Use `Coverage.resume` to start the measurement. You may want to use `Coverage.start` to setup and then start the measurement.

### Method
`start`

### Endpoint
N/A (This is a static method)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```ruby
Coverage.start
Coverage.start(:all)
Coverage.start(lines: true, branches: false, methods: true, eval: false)
Coverage.start(oneshot_lines: true)
```

### Response
#### Success Response (200)
- **nil**: Indicates the setup was successful.

#### Response Example
```json
null
```
```

--------------------------------

### Initialize RubyGems PushCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/PushCommand

Initializes the `PushCommand` with options for pushing gems to a server. It sets up proxy, key, and OTP options, and allows specifying a custom host or attaching signature attestations.

```ruby
# File lib/rubygems/commands/push_command.rb, line 32
def initialize
  super "push", "Push a gem up to the gem server", host: host, attestations: []

  @user_defined_host = false

  add_proxy_option
  add_key_option
  add_otp_option

  add_option("--host HOST",
             "Push to another gemcutter-compatible host",
             "  (e.g. https://rubygems.org)") do |value, options|
    options[:host] = value
    @user_defined_host = true
  end

  add_option("--attestation FILE",
              "Push with sigstore attestations") do |value, options|
    options[:attestations] << value
  end

  @host = nil
end
```

--------------------------------

### Construct Installer from Gem File Path (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Creates a new Gem::Installer instance for a gem file located at the specified path. It handles security policies and package creation.

```ruby
def self.at(path, options = {})
  security_policy = options[:security_policy]
  package = Gem::Package.new path, security_policy
  new package, options
end
```

--------------------------------

### Create Executable Script and Run (Ruby)

Source: https://docs.ruby-lang.org/en/master/Process

Demonstrates creating a simple executable file with `File.write` and then executing it using `system`. This showcases how to create and run a shell script from within Ruby.

```ruby
File.write('shell_command', 'echo $SHELL', perm: 0o755)
```

```ruby
system('./shell_command')
```

--------------------------------

### Example: parse! Method

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Demonstrates the usage of the `parse!` method with a Ruby script, including its behavior with `--help`, default arguments, termination by `--`, and `POSIXLY_CORRECT`.

```APIDOC
## Example: `parse!` Method

### Description
This section provides a practical example of using the `parse!` method to process command-line arguments in Ruby. It showcases different scenarios and their outcomes.

### Method
`OptionParser#parse!`

### Endpoint
N/A (Instance method of OptionParser)

### Request Example (Ruby Script)
```ruby
require 'optparse'

parser = OptionParser.new

parser.on('--xxx') do |value|
  p ['--xxx', value]
end

parser.on('--yyy YYY') do |value|
  p ['--yyy', value]
end

parser.on('--zzz [ZZZ]') do |value|
  p ['--zzz', value]
end

ret = parser.parse!
puts "Returned: #{ret} ( #{ret.class})"
```

### Response Examples

#### Help Output:
```text
$ ruby parse_bang.rb --help
Usage: parse_bang [options]
        --xxx
        --yyy YYY
        --zzz [ZZZ]
```

#### Default Behavior:
```text
$ ruby parse_bang.rb input_file.txt output_file.txt --xxx --yyy FOO --zzz BAR
["--xxx", true]
["--yyy", "FOO"]
["--zzz", "BAR"]
Returned: ["input_file.txt", "output_file.txt"] (Array)
```

#### Processing Ended by Terminator Argument (`--`):
```text
$ ruby parse_bang.rb input_file.txt output_file.txt --xxx --yyy FOO -- --zzz BAR
["--xxx", true]
["--yyy", "FOO"]
Returned: ["input_file.txt", "output_file.txt", "--zzz", "BAR"] (Array)
```

#### Processing Ended by Non-Option Argument (`POSIXLY_CORRECT`):
```text
$ POSIXLY_CORRECT=true ruby parse_bang.rb --xxx input_file.txt output_file.txt -yyy FOO
["--xxx", true]
Returned: ["input_file.txt", "output_file.txt", "-yyy", "FOO"] (Array)
```
```

--------------------------------

### OptionParser Execution Examples (Shell)

Source: https://docs.ruby-lang.org/en/master/optparse/option_params_rdoc

These examples demonstrate the execution of a Ruby script using OptionParser with handler methods. They show the output for a --help request and for options with and without arguments.

```shell
$ ruby method.rb --help
Usage: method [options]
        --xxx                        Option with no argument
        --yyy YYY                    Option with required argument
```

```shell
$ ruby method.rb --xxx
["Handler method for -xxx called with value:", true]
```

```shell
$ ruby method.rb --yyy FOO
["Handler method for -yyy called with value:", "FOO"]
```

--------------------------------

### Get Socket Option Family as Integer (Ruby)

Source: https://docs.ruby-lang.org/en/master/Socket/Option

Retrieves the network family (e.g., AF_INET, AF_INET6) of the socket option and returns it as an integer. The example shows how to get the family for an IPv6 option.

```Ruby
p Socket::Option.new(:INET6, :IPV6, :RECVPKTINFO, [1].pack("i!")).family
#=> 10
```

--------------------------------

### Get current file object for ARGF (Ruby Example)

Source: https://docs.ruby-lang.org/en/master/ARGF

This Ruby example demonstrates how to access the current file object being processed by ARGF. It shows how the `ARGF.file` attribute updates as different files are read, and how `ARGF.read` reads content from the current file.

```ruby
$ echo "foo" > foo
$ echo "bar" > bar

$ ruby argf.rb foo bar

ARGF.file      #=> #<File:foo>
ARGF.read(5)   #=> "foo\nb"
ARGF.file      #=> #<File:bar>
```

--------------------------------

### Send WebDAV PROPFIND Request with Net::HTTP::Propfind

Source: https://docs.ruby-lang.org/en/master/Net/HTTP/Propfind

Demonstrates how to use the Net::HTTP::Propfind class to send a PROPFIND request to a specified URI. It requires the 'net/http' library and shows the steps for creating a URI, extracting the hostname, initializing the Propfind request, and making the HTTP request.

```ruby
require 'net/http'
uri = URI('http://example.com')
hostname = uri.hostname # => "example.com"
req = Net::HTTP::Propfind.new(uri) # => #<Net::HTTP::Propfind PROPFIND>
res = Net::HTTP.start(hostname) do |http|
  http.request(req)
end

```

--------------------------------

### Basic File Compression Example (Ruby)

Source: https://docs.ruby-lang.org/en/master/Zlib/Deflate

A basic example demonstrating how to compress a file ('big.file') and write the compressed content to another file ('compressed.file') using Zlib::Deflate.

```ruby
open "compressed.file", "w+" do |io|
  io << Zlib::Deflate.new.deflate(File.read("big.file"))
end

```

--------------------------------

### Socket Creation Examples (Ruby)

Source: https://docs.ruby-lang.org/en/master/Socket

Demonstrates common ways to create different types of sockets using `Socket.new`.

```Ruby
Socket.new(:INET, :STREAM) # TCP socket
Socket.new(:INET, :DGRAM)  # UDP socket
Socket.new(:UNIX, :STREAM) # UNIX stream socket
Socket.new(:UNIX, :DGRAM)  # UNIX datagram socket
```

--------------------------------

### Get Files in Regular Gem

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/ContentsCommand

Retrieves files for a regular installed gem. It constructs a glob pattern based on the gem's installation path and require paths (optionally filtered by lib_only) to find all associated files.

```ruby
def files_in_gem(spec)
  gem_path  = spec.full_gem_path
  extra     = "/#{spec.require_paths.join(",")}" if options[:lib_only]
  glob      = "#{gem_path}#{extra}/**/*"
  prefix_re = %r{#{Regexp.escape(gem_path)}/}

  Dir[glob].map do |file|
    [gem_path, file.sub(prefix_re, "")]
  end
end
```

--------------------------------

### Install Libraries with vcpkg

Source: https://docs.ruby-lang.org/en/master/windows_md

Command to install required libraries using vcpkg, a C++ package manager, for building Ruby from source on Windows.

```shell
vcpkg --triplet x64-windows install
```

--------------------------------

### Determine Default Gem Installation Directory

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Calculates the default directory for installing gems. It considers the installation prefix if provided, otherwise uses the system's default gem directory. The `prepend_destdir_if_present` method is used to prepend the destination directory if it exists.

```ruby
# File lib/rubygems/commands/setup_command.rb, line 605
def default_dir
  prefix = options[:prefix]

  if prefix.empty?
    dir = Gem.default_dir
  else
    dir = prefix
  end

  prepend_destdir_if_present(dir)
end
```

--------------------------------

### Execute Error Message in GenerateIndexCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/GenerateIndexCommand/RubygemsTrampoline

This method is part of the Gem::Commands::GenerateIndexCommand and is designed to be called when the 'rubygems-generate_index' gem is not installed. It displays an error message guiding the user to install the necessary gem.

```ruby
def execute
  alert_error "Install the rubygems-generate_index gem for the generate_index command"
end
```

--------------------------------

### Initialize Gem::Source::Git

Source: https://docs.ruby-lang.org/en/master/Gem/Source/Git

Creates a new git gem source for gems from a specified repository and reference. It handles parsing the repository URI, setting attributes like name, reference, and submodule status, and defining the installation directory.

```ruby
def initialize(name, repository, reference, submodules = false)
  require_relative "../uri"
  @uri = Gem::Uri.parse(repository)
  @name            = name
  @repository      = repository
  @reference       = reference || "HEAD"
  @need_submodules = submodules

  @remote   = true
  @root_dir = Gem.dir
end
```

--------------------------------

### Initialize Gem::Security::Signer

Source: https://docs.ruby-lang.org/en/master/Gem/Security/Signer

Constructs a new Gem::Security::Signer instance. It accepts a private key, a chain of X509 certificates, an optional passphrase, and configuration options. It handles loading default keys and certificates if not provided and ensures the key and certificates are in the correct OpenSSL format.

```ruby
def initialize(key, cert_chain, passphrase = nil, options = {})
  @cert_chain = cert_chain
  @key        = key
  @passphrase = passphrase
  @options = DEFAULT_OPTIONS.merge(options)

  unless @key
    default_key = File.join Gem.default_key_path
    @key = default_key if File.exist? default_key
  end

  unless @cert_chain
    default_cert = File.join Gem.default_cert_path
    @cert_chain = [default_cert] if File.exist? default_cert
  end

  @digest_name      = Gem::Security::DIGEST_NAME
  @digest_algorithm = Gem::Security.create_digest(@digest_name)

  if @key && !@key.is_a?(OpenSSL::PKey::PKey)
    @key = OpenSSL::PKey.read(File.read(@key), @passphrase)
  end

  if @cert_chain
    @cert_chain = @cert_chain.compact.map do |cert|
      next cert if OpenSSL::X509::Certificate === cert

      cert = File.read cert if File.exist? cert

      OpenSSL::X509::Certificate.new cert
    end

    load_cert_chain
  end
end
```

--------------------------------

### Get Process Group ID using Process.getpgid

Source: https://docs.ruby-lang.org/en/master/Process

Retrieves the process group ID for a given process ID using `Process.getpgid`. The example shows getting the parent process's group ID.

```Ruby
Process.getpgid(Process.ppid) # => 25527
```

--------------------------------

### Retrieving Ruby Executable Path with RbConfig.ruby

Source: https://docs.ruby-lang.org/en/master/RbConfig

An example demonstrating how to use the RbConfig.ruby method to get the absolute path to the Ruby command.

```ruby
RbConfig.ruby -> path
```

--------------------------------

### ScanHistory#initialize Method (Ruby)

Source: https://docs.ruby-lang.org/en/master/SyntaxSuggest/ScanHistory

The constructor for ScanHistory. It takes code_lines and an initial block, setting up the history and refreshing the index. This method is fundamental for starting a scan history.

```ruby
# File lib/syntax_suggest/scan_history.rb, line 24
def initialize(code_lines:, block:)
  @code_lines = code_lines
  @history = [block]
  refresh_index
end

```

--------------------------------

### Get external encoding of ARGF (Ruby Example)

Source: https://docs.ruby-lang.org/en/master/ARGF

This Ruby example shows how to retrieve the external encoding of files being read by ARGF. The external encoding represents how the text is stored within the file itself, and this method returns it as an `Encoding` object.

```ruby
ARGF.external_encoding  #=>  #<Encoding:UTF-8>
```

--------------------------------

### Get Julian Start Date

Source: https://docs.ruby-lang.org/en/master/Date

Returns the Julian start date for calendar reform. The returned value is a float suitable for use with Date#jd, with special values for infinity in certain reform cases.

```Ruby
static VALUE
d_lite_start(VALUE self)
{
    get_d1(self);
    return DBL2NUM(m_sg(dat));
}
```

```Ruby
d = Date.new(2001, 2, 3, Date::ITALY)
s = d.start     # => 2299161.0
Date.jd(s).to_s # => "1582-10-15"

d = Date.new(2001, 2, 3, Date::ENGLAND)
s = d.start     # => 2361222.0
Date.jd(s).to_s # => "1752-09-14"

Date.new(2001, 2, 3, Date::GREGORIAN).start # => -Infinity
Date.new(2001, 2, 3, Date::JULIAN).start    # => Infinity

```

--------------------------------

### Ruby Interpreter Core Implementation (C and Ruby)

Source: https://docs.ruby-lang.org/en/master/extension_rdoc

Lists the core C source files for the Ruby interpreter's main implementation, including initialization and version management. It also mentions essential Ruby prelude files that are loaded at startup.

```C
dmyext.c
dmydln.c
dmyencoding.c
id.c
inits.c
main.c
ruby.c
version.c
```

```Ruby
gem_prelude.rb
prelude.rb
```

--------------------------------

### Ruby FileUtils ln: Example Usage (Multiple Links to Directory)

Source: https://docs.ruby-lang.org/en/master/FileUtils

Demonstrates creating hard links from multiple source files into a destination directory. Shows the state of the destination directory before and after the operation.

```Ruby
Dir.children('tmp4/')                               # => []
FileUtils.ln(['tmp0/t.txt', 'tmp2/t.dat'], 'tmp4/') # => ["tmp0/t.txt", "tmp2/t.dat"]
Dir.children('tmp4/')                               # => ["t.dat", "t.txt"]
```

--------------------------------

### Bundler.setup

Source: https://docs.ruby-lang.org/en/master/Bundler

Configures the Bundler environment, ensuring that gems specified in the Gemfile are available and properly versioned. It can be called with specific groups.

```APIDOC
## Bundler.setup

### Description
Configures the Bundler runtime. If the Bundler environment is not set up, it loads the definition from the `Gemfile.lock` and prepares the environment. Subsequent calls are no-ops. It can optionally load gems from specific groups.

### Method
`Bundler.setup(*groups)`

### Parameters
* **groups** - Optional. A list of gem groups to load. If empty, all default gems are loaded.

### Overview
After calling `Bundler.setup`, any `load` or `require` operations will be restricted to gems listed in the Gemfile or the Ruby standard library. Only versions matching the Gemfile specifications will be loaded.

### Example Usage
```ruby
# Setup and load all default gems
Bundler.setup

# Setup and load gems from the 'development' group
Bundler.setup(:development)
```

### Important Notes
* `Bundler.setup` is designed to be called only once. Subsequent calls have no effect.
* If `groups` are provided, only gems from those specified groups (and the implicit `:default` group) are loaded.
* For loading all gems from specified groups, `Bundler.require` is the preferred method after `Bundler.setup`.
```

--------------------------------

### Setup Signer API

Source: https://docs.ruby-lang.org/en/master/Gem/Package

Prepares the gem for signing and checksum generation.

```APIDOC
## POST /websites/ruby-lang_en_master/setup_signer

### Description
Sets up the gem for signing and checksum generation. If the gem specification includes signing credentials, a `Gem::Security::Signer` is initialized. Otherwise, it initializes a signer for checksum generation only. The signing key and certificate chain are updated if signing is performed.

### Method
POST

### Endpoint
/websites/ruby-lang_en_master/setup_signer

### Parameters
#### Request Body
- **signer_options** (object) - Optional - Additional options to pass to the `Gem::Security::Signer` initializer.

### Request Example
```json
{
  "signer_options": {
    "digest_algorithm": "SHA256"
  }
}
```

### Response
#### Success Response (200)
Indicates that the signer was set up successfully.

#### Response Example
```json
{
  "message": "Signer setup complete."
}
```
```

--------------------------------

### Get All Stubs (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Returns a `Gem::StubSpecification` for every installed gem by accessing the specification record's stubs.

```Ruby
def self.stubs
  specification_record.stubs
end
```

--------------------------------

### Get Default Install/Update Options for RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Returns a hash containing the default options for gem installation and update commands. The primary default is to generate RI documentation.

```ruby
# File lib/rubygems/install_update_options.rb, line 192
def install_update_options
  {
    document: %w[ri],
  }
end
```

--------------------------------

### Create Stub Makefile (Ruby)

Source: https://docs.ruby-lang.org/en/master/MakeMakefile

Generates a basic Makefile with predefined cleaning rules and targets like 'all', 'install', 'static', 'install-so', and 'install-rb'. This serves as a starting point for more complex build configurations.

```ruby
def dummy_makefile(srcdir)
  configuration(srcdir) << <<RULES << CLEANINGS
CLEANFILES = #{$cleanfiles.join(' ')}
DISTCLEANFILES = #{$distcleanfiles.join(' ')}

all install static install-so install-rb: Makefile
        @$(NULLCMD) 
.PHONY: all install static install-so install-rb
.PHONY: clean clean-so clean-static clean-rb

RULES
  end
```

--------------------------------

### Manage HTTP Session with Net::HTTP.start and Net::HTTP.finish

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

This snippet demonstrates manual session management using Net::HTTP.start and Net::HTTP.finish. It establishes a connection to a hostname, performs multiple requests (GET, DELETE), and then explicitly closes the session to free resources.

```ruby
http = Net::HTTP.new(hostname)
http.start
http.get('/todos/1')
http.get('/todos/2')
http.delete('/posts/1')
http.finish # Needed to free resources.

```

--------------------------------

### Resolv::DNS Public Class Methods

Source: https://docs.ruby-lang.org/en/master/Resolv/DNS

Documentation for public class methods of Resolv::DNS, including initialization and opening a resolver.

```APIDOC
## Public Class Methods

### new

#### Description
Creates a new `DNS` resolver.

#### Parameters

- **config_info** (nil, String, Hash) - Optional. Configuration information for the resolver.
  - `nil`: Uses `/etc/resolv.conf`.
  - `String`: Path to a file with `/etc/resolv.conf` format.
  - `Hash`: Must contain `:nameserver`, `:search`, and `:ndots` keys. `:nameserver_port` can specify the port. `:raise_timeout_errors` can be set to raise timeout errors.
    - `:nameserver` (String or Array<String>): Address(es) of the nameserver.
    - `:nameserver_port` (Array<Array>): Array of [nameserver address, port number] pairs.

#### Request Example
```ruby
Resolv::DNS.new(:nameserver => ['210.251.121.21'],
                :search => ['ruby-lang.org'],
                :ndots => 1)
```

### open

#### Description
Creates a new `DNS` resolver and optionally yields it to a block.
See `Resolv::DNS.new` for argument details.

#### Parameters

- **args** (*args): Arguments to pass to `Resolv::DNS.new`.

#### Yields

- **dns** (Resolv::DNS): The created `DNS` resolver instance.

#### Returns

- (Resolv::DNS): The created `DNS` resolver if no block is given.

```

--------------------------------

### Get lineno and path from a stack frame in Ruby

Source: https://docs.ruby-lang.org/en/master/Thread/Backtrace/Location

Demonstrates how to get the line number (`lineno`) and file path (`path`) from a `Thread::Backtrace::Location` object in Ruby. The example uses `caller_locations` to obtain the location and then accesses these properties.

```ruby
loc = c(0..1).first
loc.lineno #=> 2
```

```ruby
loc = c(0..1).first
loc.path #=> caller_locations.rb
```

--------------------------------

### Get RubyGems plugin directory path (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem

Constructs and returns the path where RubyGems plugins are installed. It defaults to `Gem.dir` and appends 'plugins'.

```Ruby
def self.plugindir(install_dir = Gem.dir)
  File.join install_dir, "plugins"
end
```

--------------------------------

### Make GET Request over HTTPS using URI

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

This example shows a convenient way to make a GET request over HTTPS. When a `URI` object with an 'https' scheme is provided to `Net::HTTP.get`, the library automatically enables TLS verification, simplifying secure connections.

```ruby
uri # => #<URI::HTTPS https://jsonplaceholder.typicode.com/>
Net::HTTP.get(uri)

```

--------------------------------

### Install Gem from Gist ID (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/RequestSet/GemDependencyAPI

Example of specifying a gem dependency using its Gist ID with the 'gist' option.

```ruby
gem 'bang', gist: '1232884'
```

--------------------------------

### Ruby Dir.glob '*' pattern examples

Source: https://docs.ruby-lang.org/en/master/Dir

Provides examples of the '*' pattern in Dir.glob, which matches any substring in an entry name. This includes matching all entries, entries starting with 'c', entries ending with 'c', and entries containing 'c'. It does not match hidden 'dot files' by default.

```Ruby
Dir.glob('*').take(3)  # => ["BSDL", "CONTRIBUTING.md", "COPYING"]
```

```Ruby
Dir.glob('c*').take(3) # => ["CONTRIBUTING.md", "COPYING", "COPYING.ja"]
```

```Ruby
Dir.glob('*c').take(3) # => ["addr2line.c", "array.c", "ast.c"]
```

```Ruby
Dir.glob('*c*').take(3) # => ["CONTRIBUTING.md", "COPYING", "COPYING.ja"]
```

--------------------------------

### Ruby OptionParser - Parsing Arguments

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Demonstrates how to define and parse command-line arguments using Ruby's OptionParser. It shows how to handle different types of options, including those with values, optional values, and positional arguments. The example highlights the output of parsed arguments and the return value of the parse method.

```ruby
require 'optparse'
parser = OptionParser.new
parser.on('--xxx') do |value|
  p ['--xxx', value]
end
parser.on('--yyy YYY') do |value|
  p ['--yyy', value]
end
parser.on('--zzz [ZZZ]') do |value|
  p ['--zzz', value]
end
ret = parser.parse(ARGV)
puts "Returned: #{ret} (#{ret.class})"

```

--------------------------------

### Tempfile.create Usage Examples

Source: https://docs.ruby-lang.org/en/master/Tempfile

Demonstrates the usage of `Tempfile.create`. The first example shows creating a file, its path, permissions, and manual unlinking. The second example illustrates creating a temporary file within a block, writing to it, and confirming it's automatically removed upon block exit. The third example shows creating an anonymous temporary file.

```ruby
f = Tempfile.create     # => #<File:/tmp/20220505-9795-17ky6f6>
f.class                 # => File
f.path                  # => "/tmp/20220505-9795-17ky6f6"
f.stat.mode.to_s(8)     # => "100600"
f.close
File.exist?(f.path)     # => true
File.unlink(f.path)
File.exist?(f.path)     # => false

Tempfile.create {|f|
  f.puts "foo"
  f.rewind
  f.read                # => "foo\n"
  f.path                # => "/tmp/20240524-380207-oma0ny"
  File.exist?(f.path)   # => true
}                       # The file is removed at block exit.

f = Tempfile.create(anonymous: true)
```

--------------------------------

### Example Usage of Tempfile.new

Source: https://docs.ruby-lang.org/en/master/Tempfile

Demonstrates creating a `Tempfile`, checking its class, path, permissions, and existence. It also shows how to manually unlink the file and verify its removal.

```ruby
f = Tempfile.new # => #<Tempfile:/tmp/20220505-17839-1s0kt30>
f.class               # => Tempfile
f.path                # => "/tmp/20220505-17839-1s0kt30"
f.stat.mode.to_s(8)   # => "100600"
File.exist?(f.path)   # => true
File.unlink(f.path)   #
File.exist?(f.path)   # => false
```

--------------------------------

### Initialize SSLSocket C Implementation

Source: https://docs.ruby-lang.org/en/master/OpenSSL/SSL/SSLSocket

C implementation for initializing an OpenSSL::SSL::SSLSocket. It handles context setup, IO binding, and SSL structure initialization.

```c
static VALUE
ossl_ssl_initialize(int argc, VALUE *argv, VALUE self)
{
    VALUE io, v_ctx;
    SSL *ssl;
    SSL_CTX *ctx;

    TypedData_Get_Struct(self, SSL, &ossl_ssl_type, ssl);
    if (ssl)
        ossl_raise(eSSLError, "SSL already initialized");

    if (rb_scan_args(argc, argv, "11", &io, &v_ctx) == 1)
        v_ctx = rb_funcall(cSSLContext, rb_intern("new"), 0);

    GetSSLCTX(v_ctx, ctx);
    rb_ivar_set(self, id_i_context, v_ctx);
    ossl_sslctx_setup(v_ctx);

    if (rb_respond_to(io, rb_intern("nonblock=")))
        rb_funcall(io, rb_intern("nonblock="), 1, Qtrue);
    Check_Type(io, T_FILE);
    rb_ivar_set(self, id_i_io, io);

    ssl = SSL_new(ctx);
    if (!ssl)
        ossl_raise(eSSLError, NULL);
    RTYPEDDATA_DATA(self) = ssl;

    SSL_set_ex_data(ssl, ossl_ssl_ex_ptr_idx, (void *)self);
    SSL_set_info_callback(ssl, ssl_info_cb);

    rb_call_super(0, NULL);

    return self;
}
```

--------------------------------

### Get Start Character Offset (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Retrieves the character offset from the beginning of the source where this location begins.

```ruby
def start_character_offset
  source.character_offset(start_offset)
end
```

--------------------------------

### Construct Target Binary Path in RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Constructs the full path for a binary file, including the specified directory. It formats the filename based on the `format_executable` option, applying the default executable format if needed.

```ruby
def target_bin_path(bin_dir, bin_file)
  bin_file_formatted = if options[:format_executable]
    Gem.default_exec_format % bin_file
  else
    bin_file
  end
  File.join bin_dir, bin_file_formatted
end
```

--------------------------------

### Get Gem Extension Directory

Source: https://docs.ruby-lang.org/en/master/Gem/BasicSpecification

Returns the full path to the directory where the gem's extensions are installed. It caches the result.

```ruby
def extension_dir
  @extension_dir ||= File.expand_path(File.join(extensions_dir, full_name))
end
```

--------------------------------

### Get stack frames using caller_locations

Source: https://docs.ruby-lang.org/en/master/Thread/Backtrace/Location

Demonstrates how to use Kernel#caller_locations to get an array of Thread::Backtrace::Location objects, representing the current stack frame and its callers. The example shows how to iterate through these locations and print their string representation.

```ruby
def a(skip)
  caller_locations(skip)
end
def b(skip)
  a(skip)
end
def c(skip)
  b(skip)
end

c(0..2).map do |call|
  puts call.to_s
end
```

--------------------------------

### SyntaxSuggest::ExplainSyntax Initialization

Source: https://docs.ruby-lang.org/en/master/SyntaxSuggest/ExplainSyntax

Shows the constructor for SyntaxSuggest::ExplainSyntax, highlighting the required 'code_lines' argument and internal initialization of lexer and missing element trackers.

```ruby
# File lib/syntax_suggest/explain_syntax.rb, line 54
def initialize(code_lines:)
  @code_lines = code_lines
  @left_right = LeftRightLexCount.new
  @missing = nil
end
```

--------------------------------

### Ruby Math Module: Interval Notation Examples

Source: https://docs.ruby-lang.org/en/master/Math

Provides examples of interval notation commonly used to describe domains and ranges of mathematical functions.

```Ruby
(-INFINITY, INFINITY)
[-1.0, 1.0]
[1.0, INFINITY)
```

--------------------------------

### Get End Column (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Calculates the column number in bytes where the location ends, relative to the start of the line.

```ruby
def end_column
  source.column(end_offset)
end
```

--------------------------------

### Get End Character Column

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Returns the column number in characters where this location ends, relative to the start of the line.

```Ruby
def end_character_column
  source.character_column(end_offset)
end
```

--------------------------------

### Ruby Socket sysaccept Example

Source: https://docs.ruby-lang.org/en/master/Socket

Example Ruby code demonstrating the use of `Socket#sysaccept`. This includes setting up a server socket to listen for connections, accepting a client connection using `sysaccept`, and then communicating with the client. It also shows the corresponding client-side code to connect and exchange messages.

```ruby
# In one script, start this first
require 'socket'
include Socket::Constants
socket = Socket.new( AF_INET, SOCK_STREAM, 0 )
sockaddr = Socket.pack_sockaddr_in( 2200, 'localhost' )
socket.bind( sockaddr )
socket.listen( 5 )
client_fd, client_addrinfo = socket.sysaccept
client_socket = Socket.for_fd( client_fd )
puts "The client said, '#{client_socket.readline.chomp}'"
client_socket.puts "Hello from script one!"
socket.close

# In another script, start this second
require 'socket'
include Socket::Constants
socket = Socket.new( AF_INET, SOCK_STREAM, 0 )
sockaddr = Socket.pack_sockaddr_in( 2200, 'localhost' )
socket.connect( sockaddr )
socket.puts "Hello from script 2."
puts "The server said, '#{socket.readline.chomp}'"
socket.close
```

--------------------------------

### Initialize Resolv::MDNS Resolver (Ruby)

Source: https://docs.ruby-lang.org/en/master/Resolv/MDNS

Creates a new one-shot Multicast DNS (mDNS) resolver. Accepts optional configuration information, merging it with default mDNS addresses if provided. Calls the superclass `Resolv::DNS#initialize`.

```ruby
# File lib/resolv.rb, line 3216
def initialize(config_info=nil)
  if config_info then
    super({ nameserver_port: Addresses }.merge(config_info))
  else
    super(nameserver_port: Addresses)
  end
end
```

--------------------------------

### Install Gem in RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/ExecCommand

Installs a gem and its dependencies, setting up necessary paths and wrappers, and handling potential installation or dependency errors.

```ruby
# File lib/rubygems/commands/exec_command.rb, line 148
def install
  set_gem_exec_install_paths

  gem_name = options[:gem_name]
  gem_version = options[:version]

  install_options = options.merge(
    minimal_deps: false,
    wrappers: true
  )

  suppress_always_install do
    dep_installer = Gem::DependencyInstaller.new install_options

    request_set = dep_installer.resolve_dependencies gem_name, gem_version

    verbose "Gems to install:"
    request_set.sorted_requests.each do |activation_request|
      verbose "\t#{activation_request.full_name}"
    end

    request_set.install install_options
  end

  Gem::Specification.reset
rescue Gem::InstallError => e
  alert_error "Error installing #{gem_name}:\n\t#{e.message}"
  terminate_interaction 1
rescue Gem::GemNotFoundException => e
  show_lookup_failure e.name, e.version, e.errors, false

  terminate_interaction 2
rescue Gem::UnsatisfiableDependencyError => e
  show_lookup_failure e.name, e.version, e.errors, false,
                      "'#{gem_name}' (#{gem_version})"

  terminate_interaction 2
end
```

--------------------------------

### Configure Bundler Settings

Source: https://docs.ruby-lang.org/en/master/Bundler

Initializes and returns the Bundler configuration, which includes setting up the gem home and path. This ensures that Bundler correctly identifies and manages gem installations.

```ruby
# File lib/bundler.rb, line 87
def configure
  @configure ||= configure_gem_home_and_path
end
```

--------------------------------

### Generate Default Directories

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Determines the default library and binary directories based on configuration. It considers the prefix option and uses RbConfig for default paths if no prefix is specified.

```ruby
def generate_default_dirs
  prefix = options[:prefix]
  site_or_vendor = options[:site_or_vendor]

  if prefix.empty?
    lib_dir = RbConfig::CONFIG[site_or_vendor]
    bin_dir = RbConfig::CONFIG["bindir"]
  else
    lib_dir = File.join prefix, "lib"
    bin_dir = File.join prefix, "bin"
  end

  [prepend_destdir_if_present(lib_dir), prepend_destdir_if_present(bin_dir)]
end
```

--------------------------------

### Traverse Files and Calculate Total Size (Ruby)

Source: https://docs.ruby-lang.org/en/master/Find

This example demonstrates how to use the `Find` module to traverse a directory structure, calculate the total size of all files, and ignore directories starting with a dot.

```Ruby
require 'find'

total_size = 0

Find.find(ENV["HOME"]) do |path|
  if FileTest.directory?(path)
    if File.basename(path).start_with?('.')
      Find.prune       
    else
      next
    end
  else
    total_size += FileTest.size(path)
  end
end

```

--------------------------------

### Get Full Gem Path

Source: https://docs.ruby-lang.org/en/master/Gem/BasicSpecification

Returns the complete path to the gem, combining the install path and the full gem name. The result is cached.

```ruby
def full_gem_path
  @full_gem_path ||= find_full_gem_path
end
```

--------------------------------

### Ruby FileUtils ln: Example Usage (Single Link)

Source: https://docs.ruby-lang.org/en/master/FileUtils

Demonstrates creating a hard link from 'tmp0/t.txt' to 'tmp1/t.lnk'. Shows the state of directories before and after the operation.

```Ruby
Dir.children('tmp0/')                    # => ["t.txt"]
Dir.children('tmp1/')                    # => []
FileUtils.ln('tmp0/t.txt', 'tmp1/t.lnk') # => 0
Dir.children('tmp1/')                    # => ["t.lnk"]
```

--------------------------------

### Add a pre-install hook for RubyGems (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem

Registers a hook that executes before a gem installation begins. The hook is passed the `Gem::Installer` instance that will perform the installation.

```Ruby
def self.pre_install(&hook)
  @pre_install_hooks << hook
end
```

--------------------------------

### Parse Requirement Examples

Source: https://docs.ruby-lang.org/en/master/Gem/Requirement

Demonstrates the output of the `parse` method with different string inputs and a Gem::Version object.

```ruby
parse("> 1.0")                 # => [">", Gem::Version.new("1.0")]
parse("1.0")                   # => ["=", Gem::Version.new("1.0")]
parse(Gem::Version.new("1.0")) # => ["=",  Gem::Version.new("1.0")]
```

--------------------------------

### Run specific Ruby spec/ test example

Source: https://docs.ruby-lang.org/en/master/contributing/testing_ruby_md

Executes a specific test example within a Ruby spec file by using the '--example' flag in SPECOPTS. This allows for highly granular testing.

```make
make test-spec SPECOPTS="../spec/ruby/core/string/to_s_spec.rb --example='returns self when self.class == String'"
```

--------------------------------

### Get File Extension - Ruby

Source: https://docs.ruby-lang.org/en/master/File

Returns the extension of a given file path. Handles cases with dotfiles, paths starting with a period, and paths ending with a period. Behavior on Windows differs for trailing periods. It does not include the leading dot in the extension if the file is a dotfile or starts with a period.

```Ruby
File.extname("test.rb")         #=> ".rb"
File.extname("a/b/d/test.rb")   #=> ".rb"
File.extname(".a/b/d/test.rb")  #=> ".rb"
File.extname("foo.")            #=> "" on Windows
File.extname("foo.")            #=> "." on non-Windows
File.extname("test")            #=> ""
File.extname(".profile")        #=> ""
File.extname(".profile.sh")     #=> ".sh"
```

--------------------------------

### OpenURI::OpenRead#open Progress Proc Example

Source: https://docs.ruby-lang.org/en/master/OpenURI/OpenRead

Provides an example of using `:progress_proc` and `:content_length_proc` together to implement a progress bar for file transfers, showing how to update the progress based on received data.

```ruby
pbar = nil
open("http://...",
  :content_length_proc => lambda {|t|
    if t && 0 < t
      pbar = ProgressBar.new("...", t)
      pbar.file_transfer_mode
    end
  },
  :progress_proc => lambda {|s|
    pbar.set s if pbar
  }) {|f| ... }
```

--------------------------------

### Initialize Gem::RequestSet::Lockfile

Source: https://docs.ruby-lang.org/en/master/Gem/RequestSet/Lockfile

Initializes a new Lockfile instance with the request set, gem dependencies file path, and dependencies. It also sets up platform information.

```ruby
def initialize(request_set, gem_deps_file, dependencies)
  @set           = request_set
  @dependencies  = dependencies
  @gem_deps_file = File.expand_path(gem_deps_file)
  @gem_deps_dir  = File.dirname(@gem_deps_file)
  @platforms = []
end
```

--------------------------------

### Get Extensions Directory (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Retrieves the path where the gem installs its extensions. It calls the superclass method if the path hasn't been set.

```ruby
def extensions_dir
  @extensions_dir ||= super
end
```

--------------------------------

### Get Default Specifications Directory (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem

Returns the path to the default specification files for gems. This is typically located within the default gem installation directory.

```Ruby
def self.default_specifications_dir
  @default_specifications_dir ||= File.join(Gem.default_dir, "specifications", "default")
end
```

--------------------------------

### Create DH Instance from Scratch (Deprecated)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/PKey/DH

Example of creating a `DH` instance from scratch and manually setting parameters using `set_pqg`. Note that this method is deprecated and may not work with OpenSSL 3.0 or later.

```ruby
# Creating an instance from scratch
# Note that this is deprecated and will not work on OpenSSL 3.0 or later.
dh = OpenSSL::PKey::DH.new
dh.set_pqg(bn_p, nil, bn_g)
```

--------------------------------

### Initialize Gem::Resolver::InstallerSet

Source: https://docs.ruby-lang.org/en/master/Gem/Resolver/InstallerSet

Constructs a new InstallerSet to locate gems within a specified domain. It initializes internal structures for fetching gems and managing local and remote gem sets. Dependencies include Gem::SpecFetcher and Gem::Resolver::BestSet.

```ruby
# File lib/rubygems/resolver/installer_set.rb, line 38
def initialize(domain)
  super()

  @domain = domain

  @f = Gem::SpecFetcher.fetcher

  @always_install      = []
  @ignore_dependencies = false
  @ignore_installed    = false
  @local               = {}
  @local_source        = Gem::Source::Local.new
  @remote_set          = Gem::Resolver::BestSet.new
  @force               = false
  @specs               = {}
end
```

--------------------------------

### Get Dependency Type

Source: https://docs.ruby-lang.org/en/master/Gem/Resolver/DependencyRequest

Retrieves the type of the dependency. This could be, for example, ':development'. The type is fetched from the wrapped Gem::Dependency object.

```ruby
# File lib/rubygems/resolver/dependency_request.rb, line 71
def type
  @dependency.type
end
```

--------------------------------

### Install Gems in RequestSet

Source: https://docs.ruby-lang.org/en/master/Gem/RequestSet

Installs the gems specified in the RequestSet. It handles downloading, installation, and potential errors, with options for installation directory and prerelease versions. It can also yield requests and installers to a block.

```Ruby
# File lib/rubygems/request_set.rb, line 146
def install(options, &block) # :yields: request, installer
  if dir = options[:install_dir]
    requests = install_into dir, false, options, &block
    return requests
  end

  @prerelease = options[:prerelease]

  requests = []
  download_queue = Thread::Queue.new

  # Create a thread-safe list of gems to download
  sorted_requests.each do |req|
    download_queue << req
  end

  # Create N threads in a pool, have them download all the gems
  threads = Array.new(Gem.configuration.concurrent_downloads) do
    # When a thread pops this item, it knows to stop running. The symbol
    # is queued here so that there will be one symbol per thread.
    download_queue << :stop

    Thread.new do
      # The pop method will block waiting for items, so the only way
      # to stop a thread from running is to provide a final item that
      # means the thread should stop.
      while req = download_queue.pop
        break if req == :stop
        req.spec.download options unless req.installed?
      end
    end
  end

  # Wait for all the downloads to finish before continuing
  threads.each(&:value)

  # Install requested gems after they have been downloaded
  sorted_requests.each do |req|
    if req.installed? && @always_install.none? {|spec| spec == req.spec.spec }
      req.spec.spec.build_extensions
      yield req, nil if block_given?
      next
    end

    spec =
      begin
        req.spec.install options do |installer|
          yield req, installer if block_given?
        end
      rescue Gem::RuntimeRequirementNotMetError => e
        suggestion = "There are no versions of #{req.request} compatible with your Ruby & RubyGems"
        suggestion += ". Maybe try installing an older version of the gem you're looking for?" unless @always_install.include?(req.spec.spec)
        e.suggestion = suggestion
        raise
      end

    requests << spec
  end

  return requests if options[:gemdeps]

  install_hooks requests, options

  requests
end
```

--------------------------------

### Zlib::GzipWriter Initialization (C Source)

Source: https://docs.ruby-lang.org/en/master/Zlib/GzipWriter

The C source code for the `Zlib::GzipWriter.new` method, illustrating how a new GzipWriter object is initialized. It handles arguments for IO, compression level, strategy, and options for encoding. Error handling for zlib compression initialization is included.

```c
static VALUE
rb_gzwriter_initialize(int argc, VALUE *argv, VALUE obj)
{
    struct gzfile *gz;
    VALUE io, level, strategy, opt = Qnil;
    int err;

    if (argc > 1) {
        opt = rb_check_convert_type(argv[argc-1], T_HASH, "Hash", "to_hash");
        if (!NIL_P(opt)) argc--;
    }

    rb_scan_args(argc, argv, "12", &io, &level, &strategy);
    TypedData_Get_Struct(obj, struct gzfile, &gzfile_data_type, gz);

    /* this is undocumented feature of zlib */
    gz->level = ARG_LEVEL(level);
    err = deflateInit2(&gz->z.stream, gz->level, Z_DEFLATED,
                       -MAX_WBITS, DEF_MEM_LEVEL, ARG_STRATEGY(strategy));
    if (err != Z_OK) {
        raise_zlib_error(err, gz->z.stream.msg);
    }
    gz->io = io;
    ZSTREAM_READY(&gz->z);
    rb_gzfile_ecopts(gz, opt);

    if (rb_respond_to(io, id_path)) {
        /* File#path may raise IOError in case when a path is unavailable */
        rb_rescue2(gzfile_initialize_path_partial, obj, NULL, Qnil, rb_eIOError, (VALUE)0);
    }

    return obj;
}
```

--------------------------------

### Ruby: Get the source of an installed gem specification

Source: https://docs.ruby-lang.org/en/master/Gem/Resolver/InstalledSpecification

The `source` method returns the source for the `InstalledSpecification`. If the source is not yet set, it initializes it to `Gem::Source::Installed.new`.

```ruby
# File lib/rubygems/resolver/installed_specification.rb, line 54
def source
  @source ||= Gem::Source::Installed.new
end
```

--------------------------------

### Ruby MonitorMixin: Private Instance Methods - mon_initialize

Source: https://docs.ruby-lang.org/en/master/MonitorMixin

Details the private 'mon_initialize' method, which sets up the monitor. It handles cases where the monitor might already be initialized or owned by the same object, preventing re-initialization errors.

```ruby
# File ext/monitor/lib/monitor.rb, line 229
def mon_initialize
  if defined?(@mon_data)
    if defined?(@mon_initialized_by_new_cond)
      return # already initialized.
    elsif @mon_data_owner_object_id == self.object_id
      raise ThreadError, "already initialized"
    end
  end
  @mon_data = ::Monitor.new
  @mon_data_owner_object_id = self.object_id
end

```

--------------------------------

### Get Begin Value of Arithmetic Sequence

Source: https://docs.ruby-lang.org/en/master/Enumerator/ArithmeticSequence

Retrieves the starting number of the arithmetic sequence. This method returns nil if the sequence is not properly initialized.

```Ruby
static inline VALUE
arith_seq_begin(VALUE self)
{
    struct arith_seq *ptr;
    TypedData_Get_Struct(self, struct arith_seq, &enumerator_data_type, ptr);
    return ptr->begin;
}
```

--------------------------------

### Example: Get Last Access Time

Source: https://docs.ruby-lang.org/en/master/File/Stat

Shows how to retrieve the last access time of a file using the `atime` method of File::Stat.

```ruby
File.stat("testfile").atime   #=> Wed Dec 31 18:00:00 CST 1969
```

--------------------------------

### Process Gem Installation Hooks (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/RequestSet

Executes custom hooks after gems have been installed. It prepares a list of installed specifications and then iterates through registered 'done_installing_hooks', passing the installer and specs to each hook.

```ruby
def install_hooks(requests, options)
  specs = requests.map do |request|
    case request
    when Gem::Resolver::ActivationRequest then
      request.spec.spec
    else
      request
    end
  end

  require_relative "dependency_installer"
  inst = Gem::DependencyInstaller.new options
  inst.installed_gems.replace specs

  Gem.done_installing_hooks.each do |hook|
    hook.call inst, specs
  end unless Gem.done_installing_hooks.empty?
end
```

--------------------------------

### Get Gem Path in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Returns the file path of the gem being installed. This provides access to the packaged gem file.

```ruby
def gem
  @package.gem.path
end
```

--------------------------------

### Install Compiled Ruby

Source: https://docs.ruby-lang.org/en/master/contributing/building_ruby_md

This command installs the compiled Ruby binaries, libraries, and header files into the directory specified by the --prefix option during the configure step. The SUDO=sudo argument can be used if installation requires superuser privileges, though it's generally recommended to install into user-writable directories.

```shell
make install
```

--------------------------------

### Running HTTP Server

Source: https://docs.ruby-lang.org/en/master/NEWS/NEWS-3_1_0_md

Shows the command-line usage for starting a simple HTTP server using Ruby's built-in capabilities, which also displays access URLs.

```shell
ruby -run -e httpd
```

--------------------------------

### SSLServer Initialization

Source: https://docs.ruby-lang.org/en/master/OpenSSL/SSL/SSLServer

Creates a new instance of `SSLServer`. Requires an instance of `TCPServer` and `OpenSSL::SSL::SSLContext`.

```APIDOC
## new

### Description
Creates a new instance of `SSLServer`.
* _svr_ is an instance of `TCPServer`.
* _ctx_ is an instance of `OpenSSL::SSL::SSLContext`.

### Method
**Class Method**

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```ruby
server = TCPServer.new('localhost', 443)
context = OpenSSL::SSL::SSLContext.new
ssl_server = OpenSSL::SSL::SSLServer.new(server, context)
```

### Response
#### Success Response (200)
Returns a new `SSLServer` object.

#### Response Example
```ruby
# <OpenSSL::SSL::SSLServer: @svr=#<TCPServer:fd...> @ctx=#<OpenSSL::SSL::SSLContext:0x...>>
```
```

--------------------------------

### Constant Path Node Examples

Source: https://docs.ruby-lang.org/en/master/Prism/ConstantPathNode

Illustrates different forms of constant path access, including root lookups, self-referential paths, and paths starting from an expression.

```ruby
Foo::Bar
^^^

self::Test
^^^^ 

a.b::C
^^^
```

--------------------------------

### Get latest specification for a gem

Source: https://docs.ruby-lang.org/en/master/Gem/SpecificationRecord

Returns the latest installed specification for a given gem name. It searches through the available specifications to find the most recent one.

```ruby
# File lib/rubygems/specification_record.rb, line 192
def latest_spec_for(name)
  latest_specs(true).find {|installed_spec| installed_spec.name == name }
end
```

--------------------------------

### C: Get Beginning of Ruby Range

Source: https://docs.ruby-lang.org/en/master/Range

A C function to retrieve the starting object of a Ruby Range. It accesses the internal representation of the range.

```c
static VALUE
range_begin(VALUE range)
{
    return RANGE_BEG(range);
}
```

--------------------------------

### Get Full Gem Name with Location

Source: https://docs.ruby-lang.org/en/master/Gem/BasicSpecification

Returns the full name of the gem, appending the installation location if it's not the default GEM_HOME.

```ruby
def full_name_with_location
  if base_dir != Gem.dir
    "#{full_name} in #{base_dir}"
  else
    full_name
  end
end
```

--------------------------------

### Get Specification Record in RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem/Uninstaller

Retrieves the specification record, either from an existing install directory or by creating a new one. This is used for managing gem specifications.

```Ruby
def specification_record
  @specification_record ||= @install_dir ? Gem::SpecificationRecord.from_path(@install_dir) : Gem::Specification.specification_record
end
```

--------------------------------

### Ruby: Get the currently executing Ractor

Source: https://docs.ruby-lang.org/en/master/Ractor

Returns the Ractor instance that is currently executing. The example shows the typical output format for the current Ractor.

```ruby
# File ractor.rb, line 246
def self.current
  __builtin_cexpr! %q{
    rb_ractor_self(rb_ec_ractor_ptr(ec));
  }
end

Ractor.current #=> #<Ractor:#1 running>
```

--------------------------------

### Install or Activate Gem if Needed

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/ExecCommand

Attempts to activate a gem; if it's not found locally, it installs the gem and then activates it.

```ruby
# File lib/rubygems/commands/exec_command.rb, line 132
def install_if_needed
  activate!
rescue Gem::MissingSpecError
  verbose "#{Gem::Dependency.new(options[:gem_name], options[:version])} not available locally, installing from remote"
  install
  activate!
end
```

--------------------------------

### POST Request Examples

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Examples of making POST requests using Net::HTTP, sending data as a string or form parameters.

```APIDOC
## POST Request Examples

### Description
Examples of making POST requests using Net::HTTP, sending data as a string or form parameters.

### Method
POST

### Endpoint
Various (depends on URI provided)

### Parameters
#### Query Parameters
- **uri** (URI) - Required - The URI object for the request.
- **data** (String) - Required - The request body as a string.
- **params** (Hash) - Required - A hash of parameters for form submission.

### Request Example
```ruby
require 'net/http'

uri = URI('https://jsonplaceholder.typicode.com/todos')

# POST with string data
data = '{"title": "foo", "body": "bar", "userId": 1}'
response_string = Net::HTTP.post(uri, data)
puts response_string.body

# POST with form parameters
params = {title: 'foo', body: 'bar', userId: 1}
response_form = Net::HTTP.post_form(uri, params)
puts response_form.body
```

### Response
#### Success Response (201)
- **body** (String) - The response body content, often including the created resource.
- **code** (String) - The HTTP status code (e.g., "201").

#### Response Example
```json
{
  "title": "foo",
  "body": "bar",
  "userId": 1,
  "id": 101
}
```
```

--------------------------------

### Ruby: Bundler.setup - Activate Bundler runtime

Source: https://docs.ruby-lang.org/en/master/Bundler

Activates the Bundler runtime, ensuring that only gems specified in the Gemfile or standard libraries can be required. It loads all groups by default or specific groups if provided.

```ruby
def setup(*groups)
  # Return if all groups are already loaded
  return @setup if defined?(@setup) && @setup

  definition.validate_runtime!

  SharedHelpers.print_major_deprecations!

  if groups.empty?
    # Load all groups, but only once
    @setup = load.setup
  else
    load.setup(*groups)
  end
end
```

--------------------------------

### Get Source Slice (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Extracts and returns the portion of the source code that this location represents, based on its start offset and length.

```ruby
def slice
  source.slice(start_offset, length)
end
```

--------------------------------

### Ruby frexp() Function Usage Examples

Source: https://docs.ruby-lang.org/en/master/Math

Provides examples of the frexp function, showing how it breaks down numbers like -2.0, -1.0, 0.0, 1.0, and 2.0 into a fraction and exponent pair. Includes handling of infinities.

```ruby
frexp(-INFINITY) # => [-Infinity, -1]
frexp(-2.0)      # => [-0.5, 2]
frexp(-1.0)      # => [-0.5, 1]
frexp(0.0)       # => [0.0, 0]
frexp(1.0)       # => [0.5, 1]
frexp(2.0)       # => [0.5, 2]
frexp(INFINITY)  # => [Infinity, -1]
```

--------------------------------

### Install Gem and Dependencies (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/DependencyInstaller

Installs a specified gem and its dependencies. It resolves dependencies, sets installation options, and handles post-installation hooks. Returns an array of installed gem specifications. Supports prerelease versions and custom installation directories.

```ruby
def install(dep_or_name, version = Gem::Requirement.default)
  request_set = resolve_dependencies dep_or_name, version

  @installed_gems = []

  options = {
    bin_dir: @bin_dir,
    build_args: @build_args,
    document: @document,
    env_shebang: @env_shebang,
    force: @force,
    format_executable: @format_executable,
    ignore_dependencies: @ignore_dependencies,
    prerelease: @prerelease,
    security_policy: @security_policy,
    user_install: @user_install,
    wrappers: @wrappers,
    build_root: @build_root,
    install_as_default: @install_as_default,
    dir_mode: @dir_mode,
    data_mode: @data_mode,
    prog_mode: @prog_mode,
  }
  options[:install_dir] = @install_dir if @only_install_dir

  request_set.install options do |_, installer|
    @installed_gems << installer.spec if installer
  end

  @installed_gems.sort!

  # Since this is currently only called for docs, we can be lazy and just say
  # it's documentation. Ideally the hook adder could decide whether to be in
  # the background or not, and what to call it.
  in_background "Installing documentation" do
    Gem.done_installing_hooks.each do |hook|
      hook.call self, @installed_gems
    end
  end unless Gem.done_installing_hooks.empty?

  @installed_gems
end
```

--------------------------------

### Ruby Process.clock_gettime Examples

Source: https://docs.ruby-lang.org/en/master/Process

Demonstrates the usage of `Process.clock_gettime` with different clock IDs and unit options to retrieve time measurements.

```Ruby
Process.clock_gettime(:CLOCK_PROCESS_CPUTIME_ID, :float_microsecond)
# => 203605054.825
Process.clock_gettime(:CLOCK_PROCESS_CPUTIME_ID, :float_millisecond)
# => 203643.696848
Process.clock_gettime(:CLOCK_PROCESS_CPUTIME_ID, :float_second)
# => 203.762181929
Process.clock_gettime(:CLOCK_PROCESS_CPUTIME_ID, :microsecond)
# => 204123212
Process.clock_gettime(:CLOCK_PROCESS_CPUTIME_ID, :millisecond)
# => 204298
Process.clock_gettime(:CLOCK_PROCESS_CPUTIME_ID, :nanosecond)
# => 204602286036
Process.clock_gettime(:CLOCK_PROCESS_CPUTIME_ID, :second)
```

--------------------------------

### Get Cache File Path (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Returns the full path to the cached gem file (.gem) for this specific gem installation.

```ruby
def cache_file
  @cache_file ||= File.join cache_dir, "#{full_name}.gem"
end
```

--------------------------------

### Get Gem Binary File Names

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Returns a list of binary file names associated with the gem. This method caches the list to avoid recomputation.

```ruby
# File lib/rubygems/commands/setup_command.rb, line 660
def bin_file_names
  @bin_file_names ||= []
end
```

--------------------------------

### Install Gems from Gemfile and Resolve Dependencies (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/RequestSet

Installs gems specified in a dependency file (like Gemfile) and resolves their versions. It supports options for installation directory, prerelease versions, and conservative installation. It also handles lockfile generation and can optionally explain the installation plan.

```ruby
def install_from_gemdeps(options, &block)
  gemdeps = options[:gemdeps]

  @install_dir = options[:install_dir] || Gem.dir
  @prerelease  = options[:prerelease]
  @remote      = options[:domain] != :local
  @conservative = true if options[:conservative]

  gem_deps_api = load_gemdeps gemdeps, options[:without_groups], true

  resolve

  if options[:explain]
    puts "Gems to install:"

    sorted_requests.each do |spec|
      puts "  #{spec.full_name}"
    end

    if Gem.configuration.really_verbose
      @resolver.stats.display
    end
  else
    installed = install options, &block

    if options.fetch :lock, true
      lockfile =
        Gem::RequestSet::Lockfile.build self, gemdeps, gem_deps_api.dependencies
      lockfile.write
    end

    installed
  end
end
```

--------------------------------

### Get latest specifications

Source: https://docs.ruby-lang.org/en/master/Gem/SpecificationRecord

Retrieves the latest installed specifications, optionally including prerelease versions based on the `prerelease` flag. It uses an internal helper method for efficiency.

```ruby
# File lib/rubygems/specification_record.rb, line 185
def latest_specs(prerelease)
  Gem::Specification._latest_specs stubs, prerelease
end
```

--------------------------------

### Open3.pipeline_start

Source: https://docs.ruby-lang.org/en/master/Open3

Starts a pipeline of commands without waiting for them to complete.

```APIDOC
## Open3.pipeline_start

### Description
Starts a pipeline of commands; does not wait for processes to complete.

### Method
GET

### Endpoint
N/A (This is a Ruby method, not an HTTP endpoint)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```ruby
threads = Open3.pipeline_start("cat - | sort")
# threads is an array of Thread objects for each command in the pipeline.
# You would then use stdin, stdout, etc. from these threads.
```

### Response
#### Success Response (200)
- **threads** (Array<Thread>) - An array of thread objects, one for each process in the pipeline.

#### Response Example
```json
[
  {
    "pid": 12345, "status": "running"
  },
  {
    "pid": 12346, "status": "running"
  }
]
```

### Additional Notes
- Allows for asynchronous execution of pipelines. Manual management of streams and process completion is required.
```

--------------------------------

### Example Usage of Process.clock_gettime in Ruby

Source: https://docs.ruby-lang.org/en/master/Process

This Ruby code snippet demonstrates how to use Process.clock_gettime to get the process CPU time. The result is a Float representing seconds.

```ruby
Process.clock_gettime(:CLOCK_PROCESS_CPUTIME_ID) # => 198.650379677
```

--------------------------------

### Initialize Gem::Commands::DependencyCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/DependencyCommand

Initializes the DependencyCommand for RubyGems. This method sets up the command's name, description, default version, and domain. It also adds various options to control the command's behavior, such as version, platform, prerelease status, reverse dependencies, and output format.

```ruby
def initialize
  super "dependency",
        "Show the dependencies of an installed gem",
        version: Gem::Requirement.default, domain: :local

  add_version_option
  add_platform_option
  add_prerelease_option

  add_option("-R", "--[no-]reverse-dependencies",
             "Include reverse dependencies in the output") do |value, options|
    options[:reverse_dependencies] = value
  end

  add_option("-p", "--pipe",
             "Pipe Format (name --version ver)") do |value, options|
    options[:pipe_format] = value
  end

  add_local_remote_options
end
```

--------------------------------

### Fiber Context Switching Example

Source: https://docs.ruby-lang.org/en/master/fiber_md

Demonstrates the basic usage of Fiber.yield and Fiber#resume for cooperative concurrency.

```APIDOC
## Fiber Context Switching Example

### Description
This example demonstrates how to create a Fiber, yield control using `Fiber.yield`, and resume execution using `Fiber#resume`.

### Method
N/A (Code Example)

### Endpoint
N/A (Code Example)

### Parameters
N/A

### Request Example
```ruby
puts "1: Start program."

f = Fiber.new do
  puts "3: Entered fiber."
  Fiber.yield
  puts "5: Resumed fiber."
end

puts "2: Resume fiber first time."
f.resume

puts "4: Resume fiber second time."
f.resume

puts "6: Finished."
```

### Response
```
1: Start program.
2: Resume fiber first time.
3: Entered fiber.
4: Resume fiber second time.
5: Resumed fiber.
6: Finished.
```
```

--------------------------------

### Set up VS Code debugging configuration

Source: https://docs.ruby-lang.org/en/master/contributing/building_ruby_md

Copy the VS Code configuration files to set up editor-based debugging for Ruby. This includes 'launch.json' with configurations for debugging Ruby itself using lldb.

```shell
cp -r misc/.vscode .vscode
```

--------------------------------

### Get Source Slice by Lines (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Extracts the source code from the beginning of the starting line to the end of the ending line that this location spans.

```ruby
def slice_lines
  line_start = source.line_start(start_offset)
  line_end = source.line_end(end_offset)
  source.slice(line_start, line_end - line_start)
end
```

--------------------------------

### Example: Fetching and Printing HTTP Response Body (Ruby)

Source: https://docs.ruby-lang.org/en/master/Net/HTTPResponse

Demonstrates how to initiate an HTTP connection, send a GET request for a specific path, and print the response body. It also shows how to make a HEAD request to the same path and observe that it returns no body.

```Ruby
path = '/todos/1'
Net::HTTP.start(hostname) do |http|
  res = http.get(path)
  p res.body
  p http.head(path).body # No body.
end
```

--------------------------------

### Get End Code Units Offset

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Returns the offset in code units from the start of the file where this location ends, using a specified encoding.

```Ruby
def end_code_units_offset(encoding = Encoding::UTF_16LE)
  # Code missing for this snippet.
end
```

--------------------------------

### Get Byte Offset of Match Beginning (Integer)

Source: https://docs.ruby-lang.org/en/master/MatchData

Returns the starting byte offset of the nth match. Handles both integer and named capture group arguments.

```Ruby
m = /(.)(.)(\d+)(\d)/.match("THX1138.")
m.bytebegin(0) # => 1
m[3]       # => "113"
m.bytebegin(3) # => 3

m = /(т)(е)(с)/.match('тест')
m.bytebegin(0) # => 0
m[3]       # => "с"
m.bytebegin(3) # => 4
```

--------------------------------

### Install Gem Specification

Source: https://docs.ruby-lang.org/en/master/Gem/Resolver/Specification

Installs the specification using Gem::Installer. It downloads the gem, creates a Gem::Installer instance, and optionally yields the installer to a block. Updates the @spec attribute after installation.

```ruby
# File lib/rubygems/resolver/specification.rb, line 96
def install(options = {})
  require_relative "../installer"

  gem = download options

  installer = Gem::Installer.at gem, options

  yield installer if block_given?

  @spec = installer.install
end
```

--------------------------------

### Net::HTTP Session Management (Ruby)

Source: https://docs.ruby-lang.org/en/master/Net

Shows how to manage HTTP sessions efficiently using Net::HTTP.start with a block, which automatically handles session setup and teardown. Includes various HTTP and WebDAV methods.

```Ruby
require 'net/http'
require 'uri'

hostname = 'example.com'
path = '/some/path'
body = 'Some text'

Net::HTTP.start(hostname) do |http|
  # Session started automatically before block execution.
  http.get(path)
  http.head(path)
  http.post(path, body)
  http.put(path, body)
  http.delete(path)
  http.options(path)
  http.trace(path)
  http.patch(path, body)
  http.copy(path)
  http.lock(path, body)
  http.mkcol(path, body)
  http.move(path)
  http.propfind(path, body)
  http.proppatch(path, body)
  http.unlock(path, body)
  # Session finished automatically at block exit.
end
```

--------------------------------

### Get Configured Bundle Path

Source: https://docs.ruby-lang.org/en/master/Bundler

Returns the bundle path as configured by Bundler settings. This path is validated to ensure it's a proper directory for gem installations.

```ruby
# File lib/bundler.rb, line 114
def configured_bundle_path
  @configured_bundle_path ||= Bundler.settings.path.tap(&:validate!)
end
```

--------------------------------

### Get Binary Directory Path (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Returns the full path to the installed gem's binary directory (e.g., 'bin'). This is distinct from 'bindir', which is just the directory name.

```ruby
def bin_dir
  @bin_dir ||= File.join gem_dir, bindir
end
```

--------------------------------

### Gem::DependencyInstaller - install

Source: https://docs.ruby-lang.org/en/master/Gem/DependencyInstaller

Installs a specified gem and its dependencies.

```APIDOC
## POST /gems/install/{dep_or_name}

### Description
Installs a gem specified by `dep_or_name` and optionally a `version`. It also installs all of its dependencies.

### Method
POST

### Endpoint
/gems/install/{dep_or_name}

### Parameters
#### Path Parameters
- **dep_or_name** (string) - Required - The name of the gem or a dependency object to install.

#### Query Parameters
- **version** (string) - Optional - The specific version requirement for the gem.

### Response
#### Success Response (200)
- **installed_gems** (array) - A list of gems that were successfully installed.
- **errors** (array) - A list of errors encountered during the installation process.

#### Response Example
```json
{
  "installed_gems": [
    "gem-name-1.0.0",
    "dependency-a-2.1.0"
  ],
  "errors": []
}
```
```

--------------------------------

### Create a Simple TCP Server in Ruby

Source: https://docs.ruby-lang.org/en/master/TCPServer

Demonstrates how to create a basic TCP server that binds to a specified port and handles incoming client connections sequentially. Each client is greeted and then disconnected.

```ruby
require 'socket'

server = TCPServer.new 2000 # Server bind to port 2000
loop do
  client = server.accept    # Wait for a client to connect
  client.puts "Hello !"
  client.puts "Time is #{Time.now}"
  client.close
end
```

--------------------------------

### Open3.capture2 Usage Example

Source: https://docs.ruby-lang.org/en/master/Open3

Demonstrates how to use the Open3.capture2 method to execute a command and retrieve its standard output as a string and its exit status.

```ruby
stdout_s, status = Open3.capture2('echo "Foo"')

```

--------------------------------

### C Implementation of OpenSSL::X509::Store Initialization

Source: https://docs.ruby-lang.org/en/master/OpenSSL/X509/Store

The C source code for initializing an X509::Store object in OpenSSL, including setting a default verification callback and initializing instance variables.

```c
static VALUE
ossl_x509store_initialize(int argc, VALUE *argv, VALUE self)
{
    X509_STORE *store;

    GetX509Store(self, store);
    if (argc != 0)
        rb_warn("OpenSSL::X509::Store.new does not take any arguments");
    X509_STORE_set_verify_cb(store, x509store_verify_cb);
    ossl_x509store_set_vfy_cb(self, Qnil);

    /* last verification status */
    rb_iv_set(self, "@error", Qnil);
    rb_iv_set(self, "@error_string", Qnil);
    rb_iv_set(self, "@chain", Qnil);

    return self;
}
```

--------------------------------

### Documenting a Ruby Module in C with RDoc (Ruby)

Source: https://docs.ruby-lang.org/en/master/contributing/documentation_guide_md

Example of documenting a C-defined module 'Bar' using an external RDoc file (`doc/bar.rdoc`). This method supports ASCII-incompatible characters in the documentation.

```ruby
# Documentation for module Bar goes here.
module Bar; end
```

--------------------------------

### Get Build Arguments (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Retrieves the build arguments used during the gem's installation by reading them from a '.info' file. Returns an empty array if the file doesn't exist or is empty.

```ruby
def build_args
  if File.exist? build_info_file
    build_info = File.readlines build_info_file
    build_info = build_info.map(&:strip)
    build_info.delete ""
    build_info
  else
    []
  end
end
```

--------------------------------

### Require Net::HTTP and Setup URIs for Requests

Source: https://docs.ruby-lang.org/en/master/Net

This snippet demonstrates how to include the Net::HTTP library and set up a URI object along with its associated variables (hostname, path, port) for making HTTP requests. It also freezes the URI to prevent accidental modification in examples.

```ruby
require 'net/http'\n\nuri = URI('https://jsonplaceholder.typicode.com/')\uri.freeze # Examples may not modify.\nhostname = uri.hostname # => "jsonplaceholder.typicode.com"\npath = uri.path         # => "/"\nport = uri.port         # => 443
```

--------------------------------

### Ruby: Get AST node type

Source: https://docs.ruby-lang.org/en/master/RubyVM/AbstractSyntaxTree/Node

Returns the type of the AST node as a symbol. Examples show retrieving the type for SCOPE, LASGN, and OPCALL nodes.

```ruby
# File ast.rb, line 132
def type
  Primitive.ast_node_type
end
```

```ruby
root = RubyVM::AbstractSyntaxTree.parse("x = 1 + 2")
root.type # => :SCOPE
lasgn = root.children[2]
lasgn.type # => :LASGN
call = lasgn.children[1]
call.type # => :OPCALL
```

--------------------------------

### URI Module Basic Example

Source: https://docs.ruby-lang.org/en/master/URI

Demonstrates the basic usage of the URI module, including parsing a URI string and accessing its components.

```APIDOC
## URI Module Basic Example

### Description
This example shows how to parse a URI string and access its various components like scheme, host, path, query, and fragment.

### Method
```ruby
require 'uri'

uri = URI("http://foo.com/posts?id=30&limit=5#time=1305298413")
puts uri.scheme
puts uri.host
puts uri.path
puts uri.query
puts uri.fragment
puts uri.to_s
```

### Response Example
```
http
foo.com
/posts
id=30&limit=5
time=1305298413
http://foo.com/posts?id=30&limit=5#time=1305298413
```
```

--------------------------------

### Get Default Gem Load Path (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem

Returns an array of default paths where RubyGems looks for gems. It includes user directories, default installation directories, and vendor directories if they exist.

```Ruby
def self.default_path
  path = []
  path << user_dir if user_home && File.exist?(user_home)
  path << default_dir
  path << vendor_dir if vendor_dir && File.directory?(vendor_dir)
  path
end
```

--------------------------------

### Enumerator::Product Instance Methods

Source: https://docs.ruby-lang.org/en/master/Enumerator/Product

Provides documentation for the instance methods of Enumerator::Product, including iteration, inspection, and rewinding.

```APIDOC
## Enumerator::Product Instance Methods

### each

#### Description
Iterates over the elements of the product enumerator. If no block is given, returns an enumerator.

#### Method
`public`

#### Endpoint
`each { |...| ... }` or `each`

#### Parameters
None

### inspect

#### Description
Returns a printable version of the product enumerator.

#### Method
`public`

#### Endpoint
`inspect`

#### Parameters
None

### rewind

#### Description
Rewinds the product enumerator by calling the `rewind` method on each enumerable in reverse order.

#### Method
`public`

#### Endpoint
`rewind`

#### Parameters
None

### size

#### Description
Returns the total size of the enumerator product.

#### Method
`public`

#### Endpoint
`size`

#### Parameters
None

#### Response
#### Success Response (200)
Returns an integer, Float::INFINITY, or nil representing the size.

#### Response Example
```ruby
# Example usage:
product_enumerator = Enumerator::Product.new(1..3, [4, 5])
product_enumerator.size #=> 6
```
```

--------------------------------

### Get End Code Units Offset (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Retrieves the offset from the start of the file in code units for the end of the location, supporting different encodings.

```ruby
def end_code_units_offset(encoding = Encoding::UTF_16LE)
  source.code_units_offset(end_offset, encoding)
end
```

--------------------------------

### Install Gem in RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem

Provides a top-level helper method for installing gems, optionally specifying a version requirement. It handles the installation process and returns the installed gems.

```Ruby
# File lib/rubygems.rb, line 585
def self.install(name, version = Gem::Requirement.default, *options)
  require_relative "rubygems/dependency_installer"
  inst = Gem::DependencyInstaller.new(*options)
  inst.install name, version
  inst.installed_gems
end
```

--------------------------------

### Get End Code Units Column

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Returns the column number in code units of a specified encoding where this location ends, relative to the start of the line.

```Ruby
def end_code_units_column(encoding = Encoding::UTF_16LE)
  source.code_units_column(end_offset, encoding)
end
```

--------------------------------

### Get Node Type (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/InstanceVariableOperatorWriteNode

Returns a symbol representing the node's type. This method is used to identify the specific kind of node, with an example returning `:instance_variable_operator_write_node`.

```Ruby
def type
  :instance_variable_operator_write_node
end
```

--------------------------------

### Ruby Dir.mkdir for Directory Creation

Source: https://docs.ruby-lang.org/en/master/Dir

Illustrates creating directories in the file system using `Dir.mkdir` in Ruby. It demonstrates how to specify directory paths and permissions, with a note that permissions are ignored on Windows.

```ruby
Dir.mkdir('foo')
File.stat(Dir.new('foo')).mode.to_s(8)[1..4] # => "0755"
Dir.mkdir('bar', 0644)
File.stat(Dir.new('bar')).mode.to_s(8)[1..4] # => "0644"

```

--------------------------------

### Example: Basic hard link creation - Ruby

Source: https://docs.ruby-lang.org/en/master/FileUtils

Shows the creation of a simple hard link from one file to another. The destination file does not exist initially.

```Ruby
FileUtils.touch('src0.txt')
File.exist?('dest0.txt') # => false
FileUtils.link_entry('src0.txt', 'dest0.txt')
File.file?('dest0.txt')  # => true
```

--------------------------------

### Get Gem Directory Path in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Provides a lazy-initialized accessor for the gem's specific installation directory. It constructs the path based on the gem home and its full name.

```ruby
def gem_dir
  @gem_dir ||= File.join(gem_home, "gems", spec.full_name)
end
```

--------------------------------

### URI and Hostname Setup for HTTP Requests

Source: https://docs.ruby-lang.org/en/master/Net/HTTPResponse

Demonstrates setting up a URI object and extracting hostname and path for use in HTTP requests. It also shows how to freeze the URI to prevent modifications.

```ruby
uri = URI('https://jsonplaceholder.typicode.com/')\uri.freeze # Examples may not modify.\nhostname = uri.hostname # => "jsonplaceholder.typicode.com"\npath = uri.path         # => "/"\nport = uri.port         # => 443
```

--------------------------------

### Get Candidate Gems for Cleanup (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/CleanupCommand

Retrieves candidate gems for cleanup. If arguments are provided, it finds specifications for those specific gems; otherwise, it retrieves all installed gem specifications.

```ruby
# File lib/rubygems/commands/cleanup_command.rb, line 112
def get_candidate_gems
  @candidate_gems = if options[:args].empty?
    Gem::Specification.to_a
  else
    options[:args].flat_map do |gem_name|
      Gem::Specification.find_all_by_name gem_name
    end
  end
end
```

--------------------------------

### Ruby: Basic GET Requests

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Demonstrates simple GET requests using Net::HTTP, fetching content from a given URI or hostname and path. It covers fetching the response body as a string.

```ruby
# Return string response body.
Net::HTTP.get(hostname, path)
Net::HTTP.get(uri)
```

--------------------------------

### Initializing Net::HTTPRequest in Ruby

Source: https://docs.ruby-lang.org/en/master/Net/HTTPRequest

Shows the constructor for Net::HTTPRequest, detailing how to create a request object for a given path and optional initialization headers. It highlights the automatic addition of Accept-Encoding for response body compression.

```ruby
# File lib/net/http/request.rb, line 82
def initialize(path, initheader = nil)
  super self.class::METHOD,
        self.class::REQUEST_HAS_BODY,
        self.class::RESPONSE_HAS_BODY,
        path, initheader
end
```

--------------------------------

### Documenting a Ruby Class in C with RDoc (Ruby)

Source: https://docs.ruby-lang.org/en/master/contributing/documentation_guide_md

Example of documenting a C-defined class 'Foo' using an external RDoc file (`doc/foo.rdoc`). This method allows for ASCII-incompatible characters in the documentation.

```ruby
# Documentation for class Foo goes here.
class Foo; end
```

--------------------------------

### Get Gem Specification in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Provides a lazy accessor for the installer's specification. This method returns the gem's specification object, which contains metadata about the gem.

```Ruby
def spec
  @package.spec
end
```

--------------------------------

### Build Ruby from Relative Directory

Source: https://docs.ruby-lang.org/en/master/windows_md

This snippet shows how to build Ruby when the build process is initiated from a subdirectory relative to the Ruby source directory. It includes creating the subdirectory and configuring the build from there.

```batch
C:
cd \ruby
mkdir mswin32
cd mswin32
..\win32\configure --prefix=/usr/local
nmake
nmake check
nmake install
```

--------------------------------

### Ruby: Get Fiber Backtrace Locations

Source: https://docs.ruby-lang.org/en/master/Fiber

Retrieves the execution stack as Thread::Backtrace::Location objects. Supports specifying a start index, a count, or a range for the backtrace.

```Ruby
f = Fiber.new { Fiber.yield }
f.resume
loc = f.backtrace_locations.first
loc.label  #=> "yield"
loc.path   #=> "test.rb"
loc.lineno #=> 1
```

--------------------------------

### Configure Ruby Build with Custom Opt-Dir (Mingw)

Source: https://docs.ruby-lang.org/en/master/windows_md

Example of configuring the Ruby build with a specific optimization directory, typically used when MSYS2 is installed via a package manager like scoop. It sets the MINGW_PACKAGE_PREFIX and uses the --with-opt-dir option.

```shell
sh ../../ruby/configure -C --disable-install-doc --with-opt-dir=C:\Users\username\scoop\apps\msys2\current\ucrt64
```

--------------------------------

### ScanHistory Initialization and Usage Example (Ruby)

Source: https://docs.ruby-lang.org/en/master/SyntaxSuggest/ScanHistory

Demonstrates how to initialize a ScanHistory object with code lines and a block, and then use its scan, changed?, and stash_changes methods. This is useful for iterating and managing code block changes.

```ruby
scanner = ScanHistory.new(code_lines: code_lines, block: block)
scanner.scan(
  up: ->(_, _, _) { true },
  down: ->(_, _, _) { true }
)
scanner.changed? # => true
expect(scanner.lines).to eq(code_lines)

scanner.stash_changes

expect(scanner.lines).to_not eq(code_lines)

```

--------------------------------

### Get Digest Length of SHA2 Hash in Ruby

Source: https://docs.ruby-lang.org/en/master/Digest/SHA2

Explains how to get the length of the hash value (digest) in bytes for SHA2 algorithms. The examples show that SHA256 produces 32-byte digests (256 bits), SHA384 produces 48-byte digests (384 bits), and SHA512 produces 64-byte digests (512 bits).

```ruby
# File ext/digest/sha2/lib/sha2.rb, line 130
def digest_length
  @sha2.digest_length
end

# Example usage:
Digest::SHA256.new.digest_length * 8
# => 256
Digest::SHA384.new.digest_length * 8
# => 384
Digest::SHA512.new.digest_length * 8
# => 512
```

--------------------------------

### UNIXServer Creation and Acceptance

Source: https://docs.ruby-lang.org/en/master/UNIXServer

Demonstrates how to create a UNIXServer, accept an incoming connection, and read data from it.

```APIDOC
## POST /websites/ruby-lang_en_master

### Description
Creates a new UNIX server socket bound to a specified path and accepts an incoming connection.

### Method
POST

### Endpoint
/websites/ruby-lang_en_master

### Parameters
#### Path Parameters
- **path** (string) - Required - The file path for the UNIX domain socket.

### Request Example
```json
{
  "path": "/tmp/sock"
}
```

### Response
#### Success Response (200)
- **socket_data** (string) - The data read from the accepted client connection.

#### Response Example
```json
{
  "socket_data": "Hello from client!"
}
```
```

--------------------------------

### Ruby ThreadGroup List Method

Source: https://docs.ruby-lang.org/en/master/ThreadGroup

Demonstrates the `list` method, which returns an array of all threads currently belonging to a ThreadGroup. The example shows how to get the list of threads in the default ThreadGroup.

```Ruby
ThreadGroup::Default.list   #=> [#<Thread:0x401bdf4c run>]
```

--------------------------------

### Ruby `sysaccept` usage example

Source: https://docs.ruby-lang.org/en/master/UNIXServer

This Ruby code demonstrates how to use the `sysaccept` method to accept a new connection. It creates a `UNIXServer`, then a `UNIXSocket` to connect to it. The `sysaccept` method is called to get the file descriptor for the new connection, which is then used to send and receive data.

```ruby
UNIXServer.open("/tmp/sock") {|serv|
  UNIXSocket.open("/tmp/sock") {|c|
    fd = serv.sysaccept
    s = IO.new(fd)
    s.puts "hi"
    s.close
    p c.read #=> "hi\n"
  }
}
```

--------------------------------

### Curry Proc Examples (Ruby)

Source: https://docs.ruby-lang.org/en/master/Proc

These Ruby code examples demonstrate the usage of the `Proc#curry` method. They show how a proc can be curried to accept arguments one by one or in groups, and how the optional arity argument controls the number of arguments needed before the proc is executed. The examples cover procs with fixed and variable arguments.

```ruby
b = proc {|x, y, z| (x||0) + (y||0) + (z||0) }
p b.curry[1][2][3]           #=> 6
p b.curry[1, 2][3, 4]        #=> 6
p b.curry(5)[1][2][3][4][5]  #=> 6
p b.curry(5)[1, 2][3, 4][5]  #=> 6
p b.curry(1)[1]              #=> 1

b = proc {|x, y, z, *w| (x||0) + (y||0) + (z||0) + w.inject(0, &:+) }
p b.curry[1][2][3]           #=> 6
p b.curry[1, 2][3, 4]        #=> 10
p b.curry(5)[1][2][3][4][5]  #=> 15
p b.curry(5)[1, 2][3, 4][5]  #=> 15
p b.curry(1)[1]              #=> 1
```

--------------------------------

### Ruby MatchData begin Method

Source: https://docs.ruby-lang.org/en/master/MatchData

Explains and demonstrates the `begin` method of Ruby's MatchData class, which returns the character offset of the start of a match or capture group. Includes examples using both numerical and named capture group arguments.

```ruby
m = /(.)(.)(\d+)(\d)/.match("THX1138.")
# => #<MatchData "HX1138" 1:"H" 2:"X" 3:"113" 4:"8">
m[0]       # => "HX1138"
m.begin(0) # => 1
m[3]       # => "113"
m.begin(3) # => 3

m = /(т)(е)(с)/.match('тест')
```

--------------------------------

### Ruby: Using Hostname for HTTP Session

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Shows how to initiate an HTTP session using just the hostname, which Net::HTTP then resolves to connect to the server.

```ruby
hostname = uri.hostname # => "jsonplaceholder.typicode.com"
Net::HTTP.start(hostname) do |http|
  # Some HTTP stuff.
end
```

--------------------------------

### Ruby: Get the count of running Ractors

Source: https://docs.ruby-lang.org/en/master/Ractor

Returns the number of Ractors that are currently running or blocked (waiting). The example demonstrates how the count changes as new Ractors are created and joined.

```ruby
# File ractor.rb, line 260
def self.count
  __builtin_cexpr! %q{
    ULONG2NUM(GET_VM()->ractor.cnt);
  }
end


Ractor.count                   #=> 1
r = Ractor.new(name: 'example') { Ractor.receive }
Ractor.count                   #=> 2 (main + example ractor)
r << 42                        # r's Ractor.receive will resume
r.join                         # wait for r's termination
Ractor.count                   #=> 1
```

--------------------------------

### Install Gem from Local Path (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/RequestSet/GemDependencyAPI

Demonstrates using the 'path' option to install a gem from a local directory, useful for development or custom builds.

```ruby
gem 'modified_gem', path: 'vendor/modified_gem'
```

--------------------------------

### Get Current Line Number

Source: https://docs.ruby-lang.org/en/master/Ripper/Filter

Returns the line number of the current token. Line numbering starts from 1. This method is valid only when called within event handlers.

```ruby
# File ext/ripper/lib/ripper/filter.rb, line 39
def lineno
  @__line
end
```

--------------------------------

### Initialize Gem::RemoteFetcher

Source: https://docs.ruby-lang.org/en/master/Gem/RemoteFetcher

Initializes a new Gem::RemoteFetcher instance with optional proxy and headers. It sets up network configurations, including reverse lookup disabling and loading necessary URI and Net::HTTP libraries. It also handles proxy settings based on environment variables or explicit `:no_proxy`.

```ruby
# File lib/rubygems/remote_fetcher.rb, line 75
def initialize(proxy = nil, dns = nil, headers = {})
  require_relative "core_ext/tcpsocket_init" if Gem.configuration.ipv4_fallback_enabled
  require_relative "vendored_net_http"
  require_relative "vendor/uri/lib/uri"

  Socket.do_not_reverse_lookup = true

  @proxy = proxy
  @pools = {}
  @pool_lock = Thread::Mutex.new
  @cert_files = Gem::Request.get_cert_files

  @headers = headers
end
```

--------------------------------

### OptionParser Generated Help Text

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Shows the automatically generated help text produced by an `OptionParser` instance based on the defined options. This includes usage information and descriptions for each option.

```Shell
$ ruby basic.rb --help
Usage: basic [options]
    -x                               Whether to X
    -y                               Whether to Y
    -z                               Whether to Z
```

--------------------------------

### Get Current Column Number

Source: https://docs.ruby-lang.org/en/master/Ripper/Filter

Returns the column number of the current token. The column numbering starts from 0. This method is intended for use only within event handlers.

```ruby
# File ext/ripper/lib/ripper/filter.rb, line 46
def column
  @__col
end
```

--------------------------------

### Get Build Info File Path (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Returns the full path to the file containing build information, typically generated during gem installation. The filename is based on the gem's full name.

```ruby
def build_info_file
  File.join build_info_dir, "#{full_name}.info"
end
```

--------------------------------

### Ruby FileUtils ln: Example Usage (Link to Directory)

Source: https://docs.ruby-lang.org/en/master/FileUtils

Demonstrates creating a hard link from a file within 'tmp2' to the 'tmp3' directory. Shows the state of directories before and after the operation.

```Ruby
Dir.children('tmp2')               # => ["t.dat"]
Dir.children('tmp3')               # => []
FileUtils.ln('tmp2/t.dat', 'tmp3') # => 0
Dir.children('tmp3')               # => ["t.dat"]
```

--------------------------------

### Get Byte Offset of Match Beginning (Named Capture)

Source: https://docs.ruby-lang.org/en/master/MatchData

Returns the starting byte offset for a named capture group. Accepts string or symbol arguments for the capture name.

```Ruby
m = /(?<foo>.)(.)(?<bar>.)/.match("hoge")
m[:foo]        # => "h"
m.bytebegin('foo') # => 0
m[:bar]        # => "g"
m.bytebegin(:bar)  # => 2
```

--------------------------------

### Get Default Bundle Directory

Source: https://docs.ruby-lang.org/en/master/Bundler

Returns the default directory where Bundler installs gems. This is typically determined by RubyGems' default behavior or Bundler's global configuration.

```ruby
# File lib/bundler.rb, line 451
def default_bundle_dir
  SharedHelpers.default_bundle_dir
end
```

--------------------------------

### Example of Key Generation (Ruby)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/PKey

Demonstrates the usage of `generate_parameters` and `generate_key` to create DSA key parameters and then generate a corresponding private key.

```Ruby
pkey_params = OpenSSL::PKey.generate_parameters("DSA", "dsa_paramgen_bits" => 2048)
pkey_params.priv_key #=> nil
pkey = OpenSSL::PKey.generate_key(pkey_params)
pkey.priv_key #=> #<OpenSSL::BN 6277...
```

--------------------------------

### Prepare Ruby Installation Directory

Source: https://docs.ruby-lang.org/en/master/contributing/building_ruby_md

This command creates the directory structure ~/.rubies/ruby-master, which will be used as the installation path for the newly compiled Ruby version. This ensures the compiled Ruby is installed in a user-specific location, avoiding conflicts with system-installed Ruby versions.

```shell
mkdir ~/.rubies
```

--------------------------------

### Get Stubs for a Specific Gem (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Returns `Gem::StubSpecification` objects only for installed gems matching the given name and the current platform. It retrieves stubs from the specification record.

```Ruby
def self.stubs_for(name)
  specification_record.stubs_for(name)
end
```

--------------------------------

### Initialize TCPServer in Ruby

Source: https://docs.ruby-lang.org/en/master/TCPServer

Shows the internal C implementation of initializing a TCPServer, which involves using `getaddrinfo()` to find addresses and then creating a server socket. It also provides a Ruby example of binding and accepting a connection.

```c
static VALUE
tcp_svr_init(int argc, VALUE *argv, VALUE sock)
{
    VALUE hostname, port;

    rb_scan_args(argc, argv, "011", &hostname, &port);
    return rsock_init_inetsock(sock, hostname, port, Qnil, Qnil, INET_SERVER, Qnil, Qnil, Qnil, Qfalse, Qnil);
}
```

```ruby
serv = TCPServer.new("127.0.0.1", 28561)
s = serv.accept
s.puts Time.now
s.close
```

--------------------------------

### Ruby New Constant RUBY_PATCHLEVEL

Source: https://docs.ruby-lang.org/en/master/NEWS/NEWS-1_8_7

Highlights the introduction of a new global constant, `RUBY_PATCHLEVEL`, starting from the 1.8.5-p1 release. This constant provides information about the specific patch level of the Ruby installation.

```ruby
# New constant since 1.8.5-p1.
#   RUBY_PATCHLEVEL
```

--------------------------------

### Initialize SSLServer

Source: https://docs.ruby-lang.org/en/master/OpenSSL/SSL/SSLServer

Creates a new instance of SSLServer. It requires a TCPServer instance and an OpenSSL::SSL::SSLContext. It sets up the session ID context if not already present.

```ruby
# File ext/openssl/lib/openssl/ssl.rb, line 515
def initialize(svr, ctx)
  @svr = svr
  @ctx = ctx
  unless ctx.session_id_context
    # see #6137 - session id may not exceed 32 bytes
    prng = ::Random.new($0.hash)
    session_id = prng.bytes(16).unpack1('H*')
    @ctx.session_id_context = session_id
  end
  @start_immediately = true
end
```

--------------------------------

### Open3.pipeline_start implementation (Ruby)

Source: https://docs.ruby-lang.org/en/master/Open3

This is the source code for the `pipeline_start` method in the Open3 module. It handles optional options and either calls `pipeline_run` for block execution or returns the wait threads directly.

```Ruby
def pipeline_start(*cmds, &block)
  if Hash === cmds.last
    opts = cmds.pop.dup
  else
    opts = {}
  end

  if block
    pipeline_run(cmds, opts, [], [], &block)
  else
    ts, = pipeline_run(cmds, opts, [], [])
    ts
  end
end
```

--------------------------------

### Example: Creating a symbolic link to a non-existent file

Source: https://docs.ruby-lang.org/en/master/FileUtils

Demonstrates creating a symbolic link where the destination file does not exist. It shows the state before and after the operation.

```ruby
FileUtils.touch('src0.txt')
File.exist?('dest0.txt')   # => false
FileUtils.ln_s('src0.txt', 'dest0.txt')
File.symlink?('dest0.txt') # => true
```

--------------------------------

### Makefile Generation for Ruby Installations

Source: https://docs.ruby-lang.org/en/master/MakeMakefile

This Ruby code snippet generates installation rules within a Makefile. It handles the installation of shared libraries and Ruby files, including dependency management and cleanup operations. It dynamically creates rules for different file types and installation targets.

```Ruby
s = s.gsub(/(\$\(\w+)(\))/) {$1+sep+$2}
        s.gsub(/(\$\{\w+)(\})/) {$1+sep+$2}
      }
      rsep = ":#{fsep}=/"
    else
      fseprepl = proc {|s| s}
      sep = ""
      rsep = ""
    end
    dirs = []
    mfile.print "install: install-so install-rb\n\n"
    dir = sodir.dup
    mfile.print("install-so: ")
    if target
      f = "$(DLLIB)"
      dest = "$(TARGET_SO)"
      stamp = '$(TARGET_SO_DIR_TIMESTAMP)'
      if $extout
        mfile.puts dest
        mfile.print "clean-so::\n"
        mfile.print "\t-$(Q)$(RM) #{fseprepl[dest]} #{fseprepl[stamp]}\n"
        mfile.print "\t-$(Q)$(RM_RF) #{fseprepl['$(CLEANLIBS)']}\n"
        mfile.print "\t-$(Q)$(RMDIRS) #{fseprepl[dir]}#{$ignore_error}\n"
      else
        mfile.print "#{f} #{stamp}\n"
        mfile.print "\t$(INSTALL_PROG) #{fseprepl[f]} #{dir}\n"
        if defined?($installed_list)
          mfile.print "\t@echo #{dir}/#{File.basename(f)}>>$(INSTALLED_LIST)\n"
        end
      end
      mfile.print "clean-static::\n"
      mfile.print "\t-$(Q)$(RM) $(STATIC_LIB)\n"
    else
      mfile.puts "Makefile"
    end
    mfile.print("install-rb: pre-install-rb do-install-rb install-rb-default\n")
    mfile.print("install-rb-default: pre-install-rb-default do-install-rb-default\n")
    mfile.print("pre-install-rb: Makefile\n")
    mfile.print("pre-install-rb-default: Makefile\n")
    mfile.print("do-install-rb:\n")
    mfile.print("do-install-rb-default:\n")
    for sfx, i in [["-default", [["lib/**/*.rb", "$(RUBYLIBDIR)", "lib"]]], ["", $INSTALLFILES]]
      files = install_files(mfile, i, nil, srcprefix) or next
      for dir, *files in files
        unless dirs.include?(dir)
          dirs << dir
          mfile.print "pre-install-rb#{sfx}: #{timestamp_file(dir, target_prefix)}\n"
        end
        for f in files
          dest = "#{dir}/#{File.basename(f)}"
          mfile.print("do-install-rb#{sfx}: #{dest}\n")
          mfile.print("#{dest}: #{f} #{timestamp_file(dir, target_prefix)}\n")
          mfile.print("\t$(Q) $(#{$extout ? 'COPY' : 'INSTALL_DATA'}) #{f} $@\n")
          if defined?($installed_list) and !$extout
            mfile.print("\t@echo #{dest}>>$(INSTALLED_LIST)\n")
          end
          if $extout
            mfile.print("clean-rb#{sfx}::\n")
            mfile.print("\t-$(Q)$(RM) #{fseprepl[dest]}\n")
          end
        end
      end
      mfile.print "pre-install-rb#{sfx}:\n"
      if files.empty?
        mfile.print("\t@$(NULLCMD)\n")
      else
        q = "$(MAKE) -q do-install-rb#{sfx}"
        if $nmake
          mfile.print "!if \"$(Q)\" == \"@\"\n\t@#{q} || \ \
!endif\n\t"
        else
          mfile.print "\t$(Q1:0=@#{q} || )"
        end
        mfile.print "$(ECHO1:0=echo) installing#{sfx.sub(/^-/, ' ')} #{target} libraries\n"
      end
      if $extout
        dirs.uniq!
        unless dirs.empty?
          mfile.print("clean-rb#{sfx}::\n")
          for dir in dirs.sort_by {|d| -d.count('/')}
            stamp = timestamp_file(dir, target_prefix)
            mfile.print("\t-$(Q)$(RM) #{fseprepl[stamp]}\n")
            mfile.print("\t-$(Q)$(RMDIRS) #{fseprepl[dir]}#{$ignore_error}\n")
          end
        end
      end
    end
    if target and !dirs.include?(sodir)
      mfile.print "$(TARGET_SO_DIR_TIMESTAMP):\n\t$(Q) $(MAKEDIRS) $(@D) #{sodir}\n\t$(Q) $(TOUCH) $@\n"
    end
    dirs.each do |d|
      t = timestamp_file(d, target_prefix)
      mfile.print "#{t}:\n\t$(Q) $(MAKEDIRS) $(@D) #{d}\n\t$(Q) $(TOUCH) $@\n"
    end

    mfile.print <<-SITEINSTALL

site-install: site-install-so site-install-rb
site-install-so: install-so
site-install-rb: install-rb

    SITEINSTALL

    return unless target

    mfile.print ".SUFFIXES: .#{(SRC_EXT + [$OBJEXT, $ASMEXT]).compact.join(' .')}\n"
    mfile.print "\n"

    compile_command = "\n\t$(ECHO) compiling $(<#{rsep})\n\t$(Q) %s\n\n"
    command = compile_command % COMPILE_CXX
    asm_command = compile_command.sub(/compiling/, 'translating') % ASSEMBLE_CXX
    CXX_EXT.each do |e|
      each_compile_rules do |rule|
        mfile.printf(rule, e, $OBJEXT)
        mfile.print(command)
        mfile.printf(rule, e, $ASMEXT)
        mfile.print(asm_command)
      end
    end
    command = compile_command % COMPILE_C
    asm_command = compile_command.sub(/compiling/, 'translating') % ASSEMBLE_C
    C_EXT.each do |e|
      each_compile_rules do |rule|
        mfile.printf(rule, e, $OBJEXT)
        mfile.print(command)
        mfile.printf(rule, e, $ASMEXT)
        mfile.print(asm_command)
      end
    end

    mfile.print "$(TARGET_SO): "
    mfile.print "$(DEFFILE) " if makedef
    mfile.print "$(OBJS) Makefile"
    mfile.print " $(TARGET_SO_DIR_TIMESTAMP)" if $extout
    mfile.print "\n"
    mfile.print "\t$(ECHO) linking shared-object #{target_prefix.sub(/\A\/(.*)/, '\1/')}$(DLLIB)\n"
    mfile.print "\t-$(Q)$(RM) $(@#{sep})\n"
    link_so = LINK_SO.gsub(/^/, "\t$(Q) ")
    if srcs.any?(&%r"\.(?:#{CXX_EXT.join('|')})\z".method(:===))

```

--------------------------------

### Ruby YAML: Parse and Emit Examples

Source: https://docs.ruby-lang.org/en/master/YAML

Demonstrates basic usage of the Ruby YAML module for parsing a YAML string into Ruby objects and emitting Ruby objects into YAML format. Requires the 'yaml' library.

```Ruby
require 'yaml'

# Parse a YAML string
puts YAML.load("---" +
     "foo") #=> "foo"

# Emit some YAML
puts YAML.dump("foo")     # => "--- foo\n...\n"
puts ({ :a => 'b'}.to_yaml)  # => "---\n:a: b\n"
```

--------------------------------

### ArrayPatternNode Initialization in Ruby

Source: https://docs.ruby-lang.org/en/master/Prism/ArrayPatternNode

Provides the source code for the `initialize` method of `ArrayPatternNode`, detailing its parameters for setting up the node.

```ruby
# File lib/prism/node.rb, line 1024
def initialize(source, node_id, location, flags, constant, requireds, rest, posts, opening_loc, closing_loc)
  @source = source
  @node_id = node_id
  @location = location
  @flags = flags
  @constant = constant
  @requireds = requireds
  @rest = rest
  @posts = posts
  @opening_loc = opening_loc
  @closing_loc = closing_loc
end
```

--------------------------------

### Determine Default Installation Directory in RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Determines the default installation directory based on the provided prefix option. If no prefix is given, it uses `Gem.default_dir`. The function then ensures the destination directory is correctly handled.

```ruby
def default_dir
  prefix = options[:prefix]

  if prefix.empty?
    dir = Gem.default_dir
  else
    dir = prefix
  end

  prepend_destdir_if_present(dir)
end
```

--------------------------------

### Open3.popen3 with Command Arguments

Source: https://docs.ruby-lang.org/en/master/Open3

Shows how to pass arguments and options to a command executed via Open3.popen3. This example demonstrates capturing the output of 'echo "Foo"'.

```ruby
Open3.popen3('echo "Foo"') { |i, o, e, t| o.gets }
# => "Foo\n"

```

--------------------------------

### Define Short Option Names in Ruby

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Demonstrates defining options with single short names and multiple short name aliases using Ruby's OptionParser. It shows how to parse arguments and handle options with or without values.

```Ruby
require 'optparse'
parser = OptionParser.new
parser.on('-x', 'Short name') do |value|
  p ['x', value]
end
parser.on('-1', '-%', 'Two short names') do |value|
  p ['-1 or -%', value]
end
parser.parse!
```

--------------------------------

### Get mkmf library path

Source: https://docs.ruby-lang.org/en/master/Gem/Ext/CargoBuilder

Retrieves the library path configuration from mkmf, formatted for use as a linker argument. This typically includes the library directory for the Ruby installation.

```ruby
def mkmf_libpath
  ["-L", "native=#{makefile_config("libdir")}"]
end
```

--------------------------------

### Hash Pattern Examples in Ruby

Source: https://docs.ruby-lang.org/en/master/Prism/HashPatternNode

Demonstrates various ways to represent hash patterns in Ruby code, including simple key-value pairs, rest parameters, and constant path references.

```Ruby
foo => { a: 1, b: 2 }
       ^^^^^^^^^^^^^^^

foo => { a: 1, b: 2, **c }
       ^^^^^^^^^^^^^^^^^^^

foo => Bar[a: 1, b: 2]
       ^^^^^^^^^^^^^^^

foo in { a: 1, b: 2 }
       ^^^^^^^^^^^^^^
```

--------------------------------

### Open3.popen3 Overview

Source: https://docs.ruby-lang.org/en/master/Open3

Demonstrates the basic usage of Open3.popen3 to execute a command and capture its output.

```APIDOC
## Open3.popen3

### Description
Executes a command, providing access to its standard input, standard output, and standard error streams.

### Method
`popen3`

### Parameters

#### `command_line` or `exe_path`
- `command_line` (String) - The command to execute, including arguments, to be run through a shell.
- `exe_path` (String or Array) - The path to an executable, optionally with an array specifying the executable path and the name to be used for the process.

#### `env` (Optional)
- `env` (Hash) - A hash of environment variables for the child process.

#### `options` (Optional)
- `options` (Hash) - Additional options for process execution.

### Usage

#### With a block:
```ruby
Open3.popen3(command_line_or_exe_path, *args, **options) do |stdin, stdout, stderr, wait_thr|
  # Interact with stdin, stdout, stderr
  # wait_thr provides access to the process status
end
```

#### Without a block:
```ruby
stdin, stdout, stderr, wait_thr = Open3.popen3(command_line_or_exe_path, *args, **options)
# Remember to close the streams: stdin.close, stdout.close, stderr.close
```

### Examples

#### Executing a simple command:
```ruby
Open3.popen3('echo "Hello World"') do |stdin, stdout, stderr, wait_thr|
  puts stdout.read
end
# => "Hello World\n"
```

#### Passing arguments:
```ruby
Open3.popen3('echo', 'Argument 1', 'Argument 2') do |stdin, stdout, stderr, wait_thr|
  puts stdout.read
end
# => "Argument 1 Argument 2\n"
```

#### Handling non-existent executable:
```ruby
begin
  Open3.popen3('non_existent_command')
rescue Errno::ENOENT => e
  puts e.message
end
# => "No such file or directory - nonexistent_command"
```

### Related Methods
- `Open3.popen2`: Executes a command with access to stdin and stdout.
- `Open3.popen2e`: Executes a command with access to stdin and combined stdout/stderr.
```

--------------------------------

### Making HTTP Requests Using Net::HTTP

Source: https://docs.ruby-lang.org/en/master/Net/HTTPHeader

This code illustrates different ways to make HTTP requests using the Net::HTTP library in Ruby. It shows how to perform a simple GET request directly with a URI, another with hostname and path, and a more advanced usage using Net::HTTP.start to manage a connection and make multiple requests.

```ruby
Net::HTTP.get(uri)\nNet::HTTP.get(hostname, '/index.html')\nNet::HTTP.start(hostname) do |http|\n  http.get('/todos/1')\n  http.get('/todos/2')\nend\n
```

--------------------------------

### Get Cached End Code Units Offset

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Retrieves the end offset of the location in code units from the start of the file, using a provided cache. This is a direct lookup from the cache.

```Ruby
def cached_start_code_units_offset(cache)
  cache[start_offset]
end
```

--------------------------------

### Open and Communicate with UNIXServer (Ruby)

Source: https://docs.ruby-lang.org/en/master/UNIXServer

Shows a more comprehensive example of using UNIXServer, including opening the server, accepting a connection, sending data, and reading it back using UNIXSocket. It uses a block form for resource management.

```Ruby
UNIXServer.open("/tmp/sock") {|serv|
  UNIXSocket.open("/tmp/sock") {|c|
    s = serv.accept
    s.puts "hi"
    s.close
    p c.read #=> "hi\n"
  }
}
```

--------------------------------

### Get base_label output in Ruby

Source: https://docs.ruby-lang.org/en/master/Thread/Backtrace/Location

Provides a Ruby example to demonstrate the output of the `base_label` method within nested method calls and blocks. It shows how the base label remains consistent.

```ruby
def foo
  puts caller_locations(0).first.base_label

  1.times do
    puts caller_locations(0).first.base_label

    1.times do
      puts caller_locations(0).first.base_label
    end
  end
end
```

--------------------------------

### IO.select Example

Source: https://docs.ruby-lang.org/en/master/IO

Demonstrates a practical example of using IO.select with pipes for inter-process communication, showing how to read and write messages between processes.

```APIDOC
## IO.select Example

### Description
Illustrates the usage of `IO.select` for monitoring read and write readiness on file descriptors, commonly used in scenarios like inter-process communication via pipes.

### Method
`IO.select(reads, writes, excepts, timeout)`

### Endpoint
N/A (Class Method)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```ruby
rp, wp = IO.pipe
mesg = "ping "
100.times {
  # IO.select follows IO#read. Not the best way to use IO.select.
  rs, ws, = IO.select([rp], [wp])
  if r = rs[0]
    ret = r.read(5)
    print ret
    case ret
    when /ping/
      mesg = "pong\n"
    when /pong/
      mesg = "ping "
    end
  end
  if w = ws[0]
    w.write(mesg)
  end
}
```

### Response
#### Success Response (200)
Outputs a sequence of 'ping' and 'pong' to standard output.

#### Response Example
```
ping pong
ping pong
ping pong
(snipped)
ping
```
```

--------------------------------

### Retrieve System Configuration Variable with confstr

Source: https://docs.ruby-lang.org/en/master/Etc

Shows how to use the `Etc.confstr` method to get system configuration variables, such as the system's PATH. The `name` argument should be a constant starting with `Etc::CS_`. Returns a string or nil.

```ruby
Etc.confstr(Etc::CS_PATH) #=> "/bin:/usr/bin"
```

--------------------------------

### Get Resolved Gem Specifications (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/RequestSet

Returns an array of `Gem::Specification` objects corresponding to the resolved gem requests. This is useful for inspecting the exact versions and details of the gems that will be installed or activated.

```ruby
def specs
  @specs ||= @requests.map(&:full_spec)
end
```

--------------------------------

### Initialize Gem::Installer::FakePackage

Source: https://docs.ruby-lang.org/en/master/Gem/Installer/FakePackage

Initializes a new Gem::Installer::FakePackage object with a given specification. This is a constructor method for the class.

```Ruby
# File lib/rubygems/installer.rb, line 101
def initialize(spec)
  @spec = spec
end
```

--------------------------------

### Construct Installer from Spec (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Constructs an installer object for an ephemeral gem, meaning a gem that only has a specification and no actual .gem file.

```ruby
def self.for_spec(spec, options = {})
  # FIXME: we should have a real Package class for this
  new FakePackage.new(spec), options
end
```

--------------------------------

### Get Exception Backtrace as Strings in Ruby

Source: https://docs.ruby-lang.org/en/master/Exception

Explains how to retrieve the exception's backtrace as an array of strings using the `backtrace` method. It includes an example of handling a division by zero error and inspecting the backtrace.

```ruby
static VALUE
exc_backtrace(VALUE exc)
{
    VALUE obj;

    obj = rb_attr_get(exc, id_bt);

    if (rb_backtrace_p(obj)) {
        obj = rb_backtrace_to_str_ary(obj);
        /* rb_ivar_set(exc, id_bt, obj); */
    }

    return obj;
}
```

```ruby
def division(numerator, denominator)
  numerator / denominator
end

begin
  division(1, 0)
rescue => ex
  p ex.backtrace
  # ["t.rb:2:in 'Integer#/'", "t.rb:2:in 'Object#division'", "t.rb:6:in '<main>'"].
  loc = ex.backtrace.first
  p loc.class
  # String
end
```

--------------------------------

### Simple TCP Server Example (Ruby)

Source: https://docs.ruby-lang.org/en/master/Socket

Provides a basic example of a TCP server using `TCPServer`. It binds to a port, accepts incoming client connections in a loop, sends a greeting and the current time, and then closes the client connection. Requires the `socket` library.

```Ruby
require 'socket'

server = TCPServer.new 2000 # Server bound to port 2000

loop do
  client = server.accept    # Wait for a client to connect
  client.puts "Hello !"
  client.puts "Time is #{Time.now}"
  client.close
end
```

--------------------------------

### Execute System Command with Environment Variable Expansion on Windows

Source: https://docs.ruby-lang.org/en/master/Process

Demonstrates executing a system command on Windows using Ruby's `system` method. It shows how environment variables like %COMSPEC% are expanded by the Windows command interpreter (cmd.exe) and includes globbing as an example.

```ruby
system("echo %COMSPEC%: C*\n") # => true
```

--------------------------------

### Build x64 Ruby Version

Source: https://docs.ruby-lang.org/en/master/windows_md

This example details the steps to build the 64-bit version of Ruby on Windows, requiring a native x64 C++ compiler. It includes the specific target flag for the x64 architecture during configuration.

```batch
C:
cd \ruby
win32\configure --prefix=/usr/local --target=x64-mswin64
nmake
nmake check
nmake install
```

--------------------------------

### Enable Option Name Abbreviations in Ruby

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Demonstrates how to allow abbreviated option names in Ruby's OptionParser. By default, abbreviations are allowed if unique. This snippet shows the basic setup and examples of valid and ambiguous abbreviations.

```ruby
require 'optparse'
parser = OptionParser.new
parser.on('-n', '--dry-run',) do |value|
  p ['--dry-run', value]
end
parser.on('-d', '--draft',) do |value|
  p ['--draft', value]
end
parser.parse!
```

--------------------------------

### Ruby Symbol Class Method: all_symbols

Source: https://docs.ruby-lang.org/en/master/Symbol

Retrieves all symbols currently present in Ruby's symbol table. The examples show how to get the size of the symbol table and inspect the first few symbols.

```ruby
Symbol.all_symbols.size    # => 9334
Symbol.all_symbols.take(3) # => [:!, :"\"", :"#"]
```

--------------------------------

### Ruby Socket recvfrom Example

Source: https://docs.ruby-lang.org/en/master/Socket

Demonstrates how to use the `recvfrom` method in Ruby to receive data from a socket. The example sets up a server to listen for connections and a client to send data.

```ruby
# In one file, start this first
require 'socket'
include Socket::Constants
socket = Socket.new( AF_INET, SOCK_STREAM, 0 )
sockaddr = Socket.pack_sockaddr_in( 2200, 'localhost' )
socket.bind( sockaddr )
socket.listen( 5 )
client, client_addrinfo = socket.accept
data = client.recvfrom( 20 )[0].chomp
puts "I only received 20 bytes '#{data}'"
sleep 1
socket.close

# In another file, start this second
require 'socket'
include Socket::Constants
socket = Socket.new( AF_INET, SOCK_STREAM, 0 )
sockaddr = Socket.pack_sockaddr_in( 2200, 'localhost' )
socket.connect( sockaddr )
socket.puts "Watch this get cut short!"
socket.close
```

--------------------------------

### Get Code Units Offset in Prism::ASCIISource

Source: https://docs.ruby-lang.org/en/master/Prism/ASCIISource

Returns the offset from the start of the file, counting in code units for a given encoding. This method is tested with UTF-8, UTF-16, and UTF-32, and simplifies for ASCII sources.

```ruby
# File lib/prism/parse_result.rb, line 271
def code_units_offset(byte_offset, encoding)
  byte_offset
end
```

--------------------------------

### Check Gem Installation Satisfies Dependency

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Determines if the currently installed gems satisfy a given dependency. It considers development dependencies and checks if any installed specification matches the dependency's requirements. If an install directory is specified, it verifies if the dependency's matching specs are non-empty.

```ruby
def installation_satisfies_dependency?(dependency)
  return true if @options[:development] && dependency.type == :development
  return true if installed_specs.detect {|s| dependency.matches_spec? s }
  return false if @only_install_dir
  !dependency.matching_specs.empty?
end
```

--------------------------------

### Resolv::DNS Public Instance Methods

Source: https://docs.ruby-lang.org/en/master/Resolv/DNS

Documentation for public instance methods of Resolv::DNS, including closing, iterating over addresses and names, and fetching resources.

```APIDOC
## Public Instance Methods

### close

#### Description
Closes the `DNS` resolver.

### each_address

#### Description
Iterates over all IP addresses for `name` retrieved from the `DNS` resolver.

#### Parameters

- **name** (Resolv::DNS::Name or String): The name to resolve.

#### Yields

- **address** (Resolv::IPv4 or Resolv::IPv6): The resolved IP address.

### each_name

#### Description
Iterates over all hostnames for `address` retrieved from the `DNS` resolver.

#### Parameters

- **address** (Resolv::IPv4, Resolv::IPv6, or String): The IP address to resolve.

#### Yields

- **name** (Resolv::DNS::Name): The resolved hostname.

#### Errors

- **ResolvError**: If the address cannot be interpreted.

### each_resource

#### Description
Iterates over all `typeclass` `DNS` resources for `name`.
See `getresource` for argument details.

#### Parameters

- **name** (Object): The name to query.
- **typeclass** (Object): The resource record type.
- **proc** (Proc): A block to yield resources to.

### fetch_resource

#### Description
Fetches `DNS` resources for a given name and typeclass.

#### Parameters

- **name** (Object): The name to query.
- **typeclass** (Object): The resource record type.

#### Yields

- **reply** (Object): The DNS reply.
- **reply_name** (Object): The name from the reply.

```

--------------------------------

### Example: Creating multiple symbolic links to a directory

Source: https://docs.ruby-lang.org/en/master/FileUtils

Shows how to create multiple symbolic links within a destination directory when the source is an array of paths.

```ruby
FileUtils.mkdir('srcdir3')
FileUtils.touch('srcdir3/src0.txt')
FileUtils.touch('srcdir3/src1.txt')
FileUtils.mkdir('destdir3')
FileUtils.ln_s(['srcdir3/src0.txt', 'srcdir3/src1.txt'], 'destdir3')
File.symlink?('destdir3/src0.txt') # => true
File.symlink?('destdir3/src1.txt') # => true
```

--------------------------------

### Get label output in Ruby

Source: https://docs.ruby-lang.org/en/master/Thread/Backtrace/Location

Provides a Ruby example to demonstrate the output of the `label` method within nested method calls and blocks. It highlights how the label changes to reflect the context, such as 'block in foo'.

```ruby
def foo
  puts caller_locations(0).first.label

  1.times do
    puts caller_locations(0).first.label

    1.times do
      puts caller_locations(0).first.label
    end
  end
end
```

--------------------------------

### Ruby IO Example Files

Source: https://docs.ruby-lang.org/en/master/IO

Demonstrates creating and writing to files with different types of content, including plain text, Russian text, and binary data, using Ruby's File and IO classes.

```ruby
# English text with newlines.
text = <<~EOT
  First line
  Second line

  Fourth line
  Fifth line
EOT

# Russian text.
russian = "\u{442 435 441 442}" # => "тест"

# Binary data.
data = "\u9990\u9991\u9992\u9993\u9994"

# Text file.
File.write('t.txt', text)

# File with Russian text.
File.write('t.rus', russian)

# File with binary data.
f = File.new('t.dat', 'wb:UTF-16')
f.write(data)
f.close
```

--------------------------------

### PUT Request Example

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Example of making a PUT request using Net::HTTP to update a resource.

```APIDOC
## PUT Request Example

### Description
Example of making a PUT request using Net::HTTP to update a resource.

### Method
PUT

### Endpoint
Various (depends on URI provided)

### Parameters
#### Query Parameters
- **uri** (URI) - Required - The URI object for the request.
- **data** (String) - Required - The request body as a string containing the updated resource data.

### Request Example
```ruby
require 'net/http'

uri = URI('https://jsonplaceholder.typicode.com/todos/1')
data = '{"title": "foo", "body": "bar", "userId": 1, "completed": true}'
response = Net::HTTP.put(uri, data)
puts response.body
```

### Response
#### Success Response (200)
- **body** (String) - The response body content, often including the updated resource.
- **code** (String) - The HTTP status code (e.g., "200").

#### Response Example
```json
{
  "userId": 1,
  "id": 1,
  "title": "foo",
  "body": "bar",
  "completed": true
}
```
```

--------------------------------

### Install LockSpecification (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Resolver/LockSpecification

Handles the installation of a locked specification. If the specification already exists in the installation directory, it yields nil and returns, otherwise it calls the superclass's install method.

```Ruby
# File lib/rubygems/resolver/lock_specification.rb, line 30
def install(options = {})
  destination = options[:install_dir] || Gem.dir

  if File.exist? File.join(destination, "specifications", spec.spec_name)
    yield nil
    return
  end

  super
end
```

--------------------------------

### Initialize Gem::Commands::FetchCommand in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/FetchCommand

Initializes the `FetchCommand` for RubyGems, setting default options and adding command-line arguments for fetching gems. It includes options for suggestions, proxy, sources, version, platform, and prerelease versions.

```ruby
# File lib/rubygems/commands/fetch_command.rb, line 11
def initialize
  defaults = {
    suggest_alternate: true,
    version: Gem::Requirement.default,
  }

  super "fetch", "Download a gem and place it in the current directory", defaults

  add_bulk_threshold_option
  add_proxy_option
  add_source_option
  add_clear_sources_option

  add_version_option
  add_platform_option
  add_prerelease_option

  add_option "--[no-]suggestions", "Suggest alternates when gems are not found" do |value, options|
    options[:suggest_alternate] = value
  end
end
```

--------------------------------

### Thread::Mutex Synchronization Example (Ruby)

Source: https://docs.ruby-lang.org/en/master/Thread/Mutex

Demonstrates how to use Thread::Mutex to synchronize access to a shared resource between two threads. It creates a new Mutex, then starts two threads that each acquire the lock using `synchronize` before accessing the resource.

```Ruby
semaphore = Thread::Mutex.new

a = Thread.new {
  semaphore.synchronize {
    # access shared resource
  }
}

b = Thread.new {
  semaphore.synchronize {
    # access shared resource
  }
}
```

--------------------------------

### Start HTTP Transport in Ruby

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Initiates the HTTP connection by calling the `connect` method and then sets the connection state to started. This is the primary method to begin an HTTP communication.

```Ruby
def do_start
  connect
  @started = true
end
```

--------------------------------

### Ruby PP Usage Examples

Source: https://docs.ruby-lang.org/en/master/PP

Shows various ways to call the `pp` method to pretty-print one or more Ruby objects. The `pp` method returns the object(s) it prints.

```Ruby
pp(obj)             #=> obj
pp obj              #=> obj
pp(obj1, obj2, ...) #=> [obj1, obj2, ...]
pp()                #=> nil
```

--------------------------------

### Get First Column of AST Location (Ruby)

Source: https://docs.ruby-lang.org/en/master/RubyVM/AbstractSyntaxTree/Location

Retrieves the starting column number of an AST node's text in the source code. This method relies on the Primitive.ast_location_first_column method.

```ruby
# File ast.rb, line 304
def first_column
  Primitive.ast_location_first_column
end
```

--------------------------------

### Get User Gem Directory Path

Source: https://docs.ruby-lang.org/en/master/Gem

Determines and returns the path for gems installed in the user's home directory. It constructs the path by joining the user's home directory, '.gem', the Ruby engine, and the Ruby version. It prioritizes `Gem.data_home` if `.gem` does not exist.

```ruby
def self.user_dir
  gem_dir = File.join(Gem.user_home, ".gem")
  gem_dir = File.join(Gem.data_home, "gem") unless File.exist?(gem_dir)
  parts = [gem_dir, ruby_engine]
  parts << RbConfig::CONFIG["ruby_version"] unless RbConfig::CONFIG["ruby_version"].empty?
  File.join parts
end
```

--------------------------------

### Get Cached End Code Units Column

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Calculates the end column of the location in code units, utilizing a provided cache for efficient lookups. The column is determined relative to the start of the line.

```Ruby
def cached_end_code_units_column(cache)
  cache[end_offset] - cache[source.line_start(end_offset)]
end
```

--------------------------------

### Get Gems in Dependency Order

Source: https://docs.ruby-lang.org/en/master/Gem/DependencyList

Returns a list of gem specifications sorted according to their dependencies. This order ensures that dependencies are resolved before the gems that rely on them, preventing installation or removal conflicts. Handles circular dependencies gracefully.

```Ruby
def dependency_order
  sorted = strongly_connected_components.flatten

  result = []
  seen = {}

  sorted.each do |spec|
    if index = seen[spec.name]
      if result[index].version < spec.version
        result[index] = spec
      end
    else
      seen[spec.name] = result.length
      result << spec
    end
  end

  result.reverse
end
```

--------------------------------

### Generating Makefile with extconf.rb

Source: https://docs.ruby-lang.org/en/master/extension_rdoc

After preparing the `extconf.rb` file, you generate the Makefile by running the `ruby extconf.rb` command. This process uses the checks performed in `extconf.rb` to create a platform-specific Makefile. The `--vendor` option can be used to install the library in the `vendor_ruby` directory.

```shell
ruby extconf.rb

```

```shell
ruby extconf.rb --vendor

```

--------------------------------

### Ruby Fiber.new, Fiber.yield, and Fiber.kill example

Source: https://docs.ruby-lang.org/en/master/NEWS/NEWS-3_3_0_md

Demonstrates the creation and usage of a Fiber, including yielding control and terminating the fiber using `Fiber#kill`. This showcases asynchronous execution patterns within Ruby.

```ruby
fiber = Fiber.new do
  while true
    puts "Yielding..."
    Fiber.yield
  end
ensure
  puts "Exiting..."
end

fiber.resume
# Yielding...
fiber.kill
# Exiting...
```

--------------------------------

### Ruby ObjectSpace count_objects Usage Example

Source: https://docs.ruby-lang.org/en/master/ObjectSpace

This Ruby code demonstrates how to use the ObjectSpace.count_objects method to get a hash of all objects currently in memory, grouped by their type. It shows how to initialize an empty hash and pass it to the method for population.

```ruby
h = {}
ObjectSpace.count_objects(h)
puts h
```

--------------------------------

### Get All Gem Names from Command Line in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Command

Retrieves all gem names provided as arguments from the command line. It raises an error if no gem names are specified and filters out any arguments starting with '-'.

```Ruby
def get_all_gem_names
  args = options[:args]

  if args.nil? || args.empty?
    raise Gem::CommandLineError,
          "Please specify at least one gem name (e.g. gem build GEMNAME)"
  end

  args.reject {|arg| arg.start_with?("-") }
end
```

--------------------------------

### Simple Class include Example

Source: https://docs.ruby-lang.org/en/master/MonitorMixin

Illustrates creating a thread-safe array by including MonitorMixin in a new class.

```APIDOC
## Example: Simple Class include

### Description
This example defines a `SynchronizedArray` class that inherits from `Array` and includes `MonitorMixin`. Key methods like `shift` and `unshift` are overridden to ensure thread-safe access.

### Code
```ruby
require 'monitor'

class SynchronizedArray < Array

  include MonitorMixin

  def initialize(*args)
    super(*args)
  end

  alias :old_shift :shift
  alias :old_unshift :unshift

  def shift(n=1)
    self.synchronize do
      self.old_shift(n)
    end
  end

  def unshift(item)
    self.synchronize do
      self.old_unshift(item)
    end
  end

  # other methods ...
end
```
```

--------------------------------

### Setup SSL Context in C (OpenSSL)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/SSL/SSLContext

The C function `ossl_sslctx_setup` handles the low-level initialization and configuration of an OpenSSL SSL_CTX object. It sets up DH parameters, post-handshake authentication, certificates, private keys, and CA locations based on Ruby's SSLContext attributes.

```c
static VALUE
ossl_sslctx_setup(VALUE self)
{
    SSL_CTX *ctx;
    X509 *cert = NULL, *client_ca = NULL;
    EVP_PKEY *key = NULL;
    char *ca_path = NULL, *ca_file = NULL;
    int verify_mode;
    long i;
    VALUE val;

    if(OBJ_FROZEN(self)) return Qnil;
    GetSSLCTX(self, ctx);

#if !defined(OPENSSL_NO_DH)
    SSL_CTX_set_tmp_dh_callback(ctx, ossl_tmp_dh_callback);
#endif

#if !defined(OPENSSL_IS_AWSLC) /* AWS-LC has no support for TLS 1.3 PHA. */
    SSL_CTX_set_post_handshake_auth(ctx, 1);
#endif

    val = rb_attr_get(self, id_i_cert_store);
    if (!NIL_P(val)) {
        X509_STORE *store = GetX509StorePtr(val); /* NO NEED TO DUP */
        SSL_CTX_set_cert_store(ctx, store);
        X509_STORE_up_ref(store);
    }

    val = rb_attr_get(self, id_i_extra_chain_cert);
    if(!NIL_P(val)){
        rb_block_call(val, rb_intern("each"), 0, 0, ossl_sslctx_add_extra_chain_cert_i, self);
    }

    /* private key may be bundled in certificate file. */
    val = rb_attr_get(self, id_i_cert);
    cert = NIL_P(val) ? NULL : GetX509CertPtr(val); /* NO DUP NEEDED */
    val = rb_attr_get(self, id_i_key);
    key = NIL_P(val) ? NULL : GetPrivPKeyPtr(val); /* NO DUP NEEDED */
    if (cert && key) {
        if (!SSL_CTX_use_certificate(ctx, cert)) {
            /* Adds a ref => Safe to FREE */
            ossl_raise(eSSLError, "SSL_CTX_use_certificate");
        }
        if (!SSL_CTX_use_PrivateKey(ctx, key)) {
            /* Adds a ref => Safe to FREE */
            ossl_raise(eSSLError, "SSL_CTX_use_PrivateKey");
        }
        if (!SSL_CTX_check_private_key(ctx)) {
            ossl_raise(eSSLError, "SSL_CTX_check_private_key");
        }
    }

    val = rb_attr_get(self, id_i_client_ca);
    if(!NIL_P(val)){
        if (RB_TYPE_P(val, T_ARRAY)) {
            for(i = 0; i < RARRAY_LEN(val); i++){
                client_ca = GetX509CertPtr(RARRAY_AREF(val, i));
                if (!SSL_CTX_add_client_CA(ctx, client_ca)){
                    /* Copies X509_NAME => FREE it. */
                    ossl_raise(eSSLError, "SSL_CTX_add_client_CA");
                }
            }
        }
        else{
            client_ca = GetX509CertPtr(val); /* NO DUP NEEDED. */
            if (!SSL_CTX_add_client_CA(ctx, client_ca)){
                /* Copies X509_NAME => FREE it. */
                ossl_raise(eSSLError, "SSL_CTX_add_client_CA");
            }
        }
    }

    val = rb_attr_get(self, id_i_ca_file);
    ca_file = NIL_P(val) ? NULL : StringValueCStr(val);
    val = rb_attr_get(self, id_i_ca_path);
    ca_path = NIL_P(val) ? NULL : StringValueCStr(val);
#ifdef HAVE_SSL_CTX_LOAD_VERIFY_FILE
    if (ca_file && !SSL_CTX_load_verify_file(ctx, ca_file))
        ossl_raise(eSSLError, "SSL_CTX_load_verify_file");
    if (ca_path && !SSL_CTX_load_verify_dir(ctx, ca_path))
        ossl_raise(eSSLError, "SSL_CTX_load_verify_dir");
#else
    if (ca_file || ca_path) {
        if (!SSL_CTX_load_verify_locations(ctx, ca_file, ca_path))
            ossl_raise(eSSLError, "SSL_CTX_load_verify_locations");
    }
#endif

    val = rb_attr_get(self, id_i_verify_mode);
    verify_mode = NIL_P(val) ? SSL_VERIFY_NONE : NUM2INT(val);
    SSL_CTX_set_verify(ctx, verify_mode, ossl_ssl_verify_callback);
    if (RTEST(rb_attr_get(self, id_i_client_cert_cb)))
        SSL_CTX_set_client_cert_cb(ctx, ossl_client_cert_cb);

    val = rb_attr_get(self, id_i_timeout);
    if(!NIL_P(val)) SSL_CTX_set_timeout(ctx, NUM2LONG(val));

    val = rb_attr_get(self, id_i_verify_depth);
    if(!NIL_P(val)) SSL_CTX_set_verify_depth(ctx, NUM2INT(val));

#ifdef OSSL_USE_NEXTPROTONEG
    val = rb_attr_get(self, id_i_npn_protocols);
    if (!NIL_P(val)) {
        VALUE encoded = ssl_encode_npn_protocols(val);
        rb_ivar_set(self, id_npn_protocols_encoded, encoded);
        SSL_CTX_set_next_protos_advertised_cb(ctx, ssl_npn_advertise_cb, (void *)self);
        OSSL_Debug("SSL NPN advertise callback added");
    }
    if (RTEST(rb_attr_get(self, id_i_npn_select_cb))) {
        SSL_CTX_set_next_proto_select_cb(ctx, ssl_npn_select_cb, (void *) self);
        OSSL_Debug("SSL NPN select callback added");

```

--------------------------------

### ScanHistory#before_lines Private Method (Ruby)

Source: https://docs.ruby-lang.org/en/master/SyntaxSuggest/ScanHistory

A private helper method that returns an array of all CodeLines existing before the currently scanned block. It handles the case where the block starts at the beginning of the code lines.

```ruby
# File lib/syntax_suggest/scan_history.rb, line 114
        def before_lines
  @code_lines[0...@before_index] || []
end

```

--------------------------------

### Add a post-install hook for RubyGems (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem

Registers a hook that runs after a gem has been successfully installed. The hook is passed the `Gem::Installer` instance responsible for the installation.

```Ruby
def self.post_install(&hook)
  @post_install_hooks << hook
end
```

--------------------------------

### Ruby: Bind and Listen on Socket

Source: https://docs.ruby-lang.org/en/master/Socket

Demonstrates binding a socket to a local address and port, then listening for incoming connections. This example showcases setting up a server socket.

```ruby
require 'socket'
include Socket::Constants
socket = Socket.new( AF_INET, SOCK_STREAM, 0 )
sockaddr = Socket.pack_sockaddr_in(2200, 'localhost')
socket.bind(sockaddr)
socket.listen(5)
```

--------------------------------

### Regexp.union Examples with Strings

Source: https://docs.ruby-lang.org/en/master/Regexp

Demonstrates creating a union `Regexp` from strings. Each string is treated as a literal pattern. The example shows matching against the combined pattern.

```ruby
r = Regexp.union(%w[cat dog])      # => /cat|dog/
r.match('cat')      # => #<MatchData "cat">
r.match('dog')      # => #<MatchData "dog">
r.match('cog')      # => nil
Regexp.union('penzance')             # => /penzance/
Regexp.union('a+b*c')                # => /a\+b\*c/
Regexp.union('skiing', 'sledding')   # => /skiing|sledding/
Regexp.union(['skiing', 'sledding']) # => /skiing|sledding/
```

--------------------------------

### Get First Line Number of AST Location (Ruby)

Source: https://docs.ruby-lang.org/en/master/RubyVM/AbstractSyntaxTree/Location

Retrieves the starting line number of an AST node's text in the source code. This method relies on the Primitive.ast_location_first_lineno method.

```ruby
# File ast.rb, line 296
def first_lineno
  Primitive.ast_location_first_lineno
end
```

--------------------------------

### Add Post-Install Hook (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem

Allows adding a hook that executes after gem installation is complete. The hook receives the Gem::DependencyInstaller and a list of installed specifications.

```Ruby
def self.done_installing(&hook)
  @done_installing_hooks << hook
end
```

--------------------------------

### Format Gem Installation Path in RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem/QueryUtils

Adds the installation path of a gem to the entry. Differentiates between single and multiple specifications for the same gem.

```ruby
def spec_loaded_from(entry, spec, specs)
  return unless spec.loaded_from

  if specs.length == 1
    default = spec.default_gem? ? " (default)" : nil
    entry << "\n" << "    Installed at#{default}: #{spec.base_dir}"
  else
    label = "Installed at"
    specs.each do |s|
      version = s.version.to_s
      default = s.default_gem? ? ", default" : ""
      entry << "\n" << "    #{label} (#{version}#{default}): #{s.base_dir}"
      label = " " * label.length
    end
  end
end
```

--------------------------------

### Class Creation

Source: https://docs.ruby-lang.org/en/master/Class

Demonstrates the basic syntax for creating a new class in Ruby.

```APIDOC
## Class Creation

### Description
This section shows the fundamental way to define a new class in Ruby.

### Method
N/A (Syntax Definition)

### Endpoint
N/A

### Parameters
N/A

### Request Example
```ruby
class Name
  # some code describing the class behavior
end
```

### Response
N/A
```

--------------------------------

### Get Node Type (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/GlobalVariableOperatorWriteNode

Returns a symbol representing the type of the node. This is used to identify the specific kind of node within the Prism library. It returns a symbol, for example, `:global_variable_operator_write_node`.

```ruby
def type
  :global_variable_operator_write_node
end
```

--------------------------------

### Handle Start of Document Event

Source: https://docs.ruby-lang.org/en/master/Psych/TreeBuilder

The `start_document` method handles the `start_document` event, creating a `Psych::Nodes::Document` node with version, tag directives, and implicit styling, then setting its start location and adding it to the stack.

```ruby
# File ext/psych/lib/psych/tree_builder.rb, line 65
def start_document version, tag_directives, implicit
  n = Nodes::Document.new version, tag_directives, implicit
  set_start_location(n)
  @last.children << n
  push n
end
```

--------------------------------

### Posts Attribute Example in Ruby

Source: https://docs.ruby-lang.org/en/master/Prism/ArrayPatternNode

Shows an example of the 'posts' attribute in an array pattern, highlighting the elements following a rest element.

```ruby
foo in *bar, baz
             ^^^
```

--------------------------------

### ASN1 Primitive Creation Examples

Source: https://docs.ruby-lang.org/en/master/OpenSSL/ASN1/Primitive

Provides examples of how to create instances of `OpenSSL::ASN1::EndOfContent` and other `Primitive` subclasses.

```APIDOC
## Examples

### Creating `EndOfContent`

```ruby
eoc = OpenSSL::ASN1::EndOfContent.new
```

### Creating any other `Primitive`

```ruby
prim = <class>.new(value) # <class> being one of the sub-classes except EndOfContent
prim_zero_tagged_implicit = <class>.new(value, 0, :IMPLICIT)
prim_zero_tagged_explicit = <class>.new(value, 0, :EXPLICIT)
```
```

--------------------------------

### Enable HTTPS Connection with Net::HTTP.start

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

This snippet illustrates how to establish a secure HTTPS connection using `Net::HTTP.start`. By passing `:use_ssl => true` as an option, the connection is secured with TLS. It then proceeds to make a request over the established HTTPS session.

```ruby
Net::HTTP.start(hostname, :use_ssl => true) do |http|
  req = Net::HTTP::Get.new(uri)
  res = http.request(req)
end

```

--------------------------------

### Get Operator Location from Prism Node

Source: https://docs.ruby-lang.org/en/master/Prism/CallAndWriteNode

The operator_loc method retrieves the location of the operator in the source code. If the location is not already a Location object, it constructs one from an encoded integer. The example highlights the operator location for '&&='.

```Ruby
def operator_loc
  location = @operator_loc
  return location if location.is_a?(Location)
  @operator_loc = Location.new(source, location >> 32, location & 0xFFFFFFFF)
end
```

--------------------------------

### TCPServer.new

Source: https://docs.ruby-lang.org/en/master/TCPServer

Details on creating a new `TCPServer` instance, with options for specifying a hostname and port.

```APIDOC
## TCPServer.new

### Description
Creates a new server socket bound to a specified port. An optional hostname can be provided to bind the socket to a specific network interface. The method handles multiple addresses by trying to create a socket for each and returning the first successful one.

### Method
`TCPServer.new([hostname,] port)`

### Parameters
- **hostname** (String) - Optional - The hostname or IP address to bind the server to.
- **port** (Integer) - Required - The port number to listen on.

### Request Example
```ruby
serv = TCPServer.new("127.0.0.1", 28561)
s = serv.accept
s.puts Time.now
s.close
```
```

--------------------------------

### IO#sync - Get and Set Sync Mode

Source: https://docs.ruby-lang.org/en/master/IO

Allows checking and setting the synchronization mode of an IO stream. When sync mode is true, output is immediately flushed to the OS. The example demonstrates setting sync to true and verifying the change.

```ruby
f = File.open('t.tmp', 'w')
f.sync # => false
f.sync = true
f.sync # => true
f.close
```

--------------------------------

### Gem::SourceList#initialize (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/SourceList

Provides the code for initializing an empty Gem::SourceList, setting up an internal array to hold sources.

```Ruby
# File lib/rubygems/source_list.rb, line 22
def initialize
  @sources = []
end
```

--------------------------------

### Determine User Install Directory (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Calculates the user-specific installation directory for gems. It avoids installation in `--build-root` mode and checks for user installation preferences.

```Ruby
def user_install_dir
  # never install to user home in --build-root mode
  return unless @build_root.nil?

  # Please note that @user_install might have three states:
  # * `true`: `--user-install`
  # * `false`: `--no-user-install` and
  # * `nil`: option was not specified
  if @user_install || (@user_install.nil? && Gem.default_user_install)
    Gem.user_dir
  end
end
```

--------------------------------

### Net::HTTP Start Default Address Parameter

Source: https://docs.ruby-lang.org/en/master/NEWS/NEWS-2_5_0

The `Net::HTTP#start` method now passes `:ENV` to `p_addr` by default. To prevent this, pass `nil` explicitly.

```ruby
Net::HTTP#start(:ENV)
```

--------------------------------

### Ruby Range overlap? Method Examples

Source: https://docs.ruby-lang.org/en/master/Range

Demonstrates the `overlap?` method for Ruby Ranges, showing when two ranges are considered to overlap. It returns false if the start of one range is greater than the end of the other, or if they only touch at an exclusive endpoint.

```ruby
(4..5).overlap?(2..3)      # => false
(4..5).overlap?(2...4)     # => false

(1..2).overlap?(3..4)      # => false
(1...3).overlap?(3..4)     # => false

(...-Float::INFINITY).overlap?(...-Float::INFINITY) # => true
(..."").overlap?(..."") # => true
(...[]).overlap?(...[]) # => true
```

--------------------------------

### Install Gem into Vendor Directory

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Installs a gem into the vendor directory, intended for gem repackagers. It checks for platform support and sets the installation directory accordingly.

```ruby
add_option(:'Install/Update', "--vendor",
             "Install gem into the vendor directory.",
             "Only for use by gem repackagers.") do |_value, options|
    unless Gem.vendor_dir
      raise Gem::OptionParser::InvalidOption.new "your platform is not supported"
    end

    options[:vendor] = true
    options[:install_dir] = Gem.vendor_dir
  end
```

--------------------------------

### Argument Handling: exe_path

Source: https://docs.ruby-lang.org/en/master/Open3

Explains how the `exe_path` argument is handled, including direct execution and passing arguments.

```APIDOC
## Argument Handling: `exe_path`

### Description
Details the usage of the `exe_path` argument for `Open3.popen2e`, covering direct execution of an executable path and passing additional arguments.

### Method
`Open3.popen2e(exe_path, *args)`

### Parameters
#### Path Parameters
* **exe_path** (String or Array) - Required - The path to the executable. If an array, the first element is the path and the second is the name of the executing process.
* **args** (String) - Optional - Additional arguments to pass to the executable.

#### Query Parameters
None

#### Request Body
None

### Request Example
```ruby
Open3.popen2e('/bin/echo', 'Hello') { |i, o_e, t| puts o_e.gets }
Open3.popen2e(['/bin/echo', 'echo_cmd'], 'World') { |i, o_e, t| puts o_e.gets }
```

### Response
#### Success Response (Output)
The standard output of the command.

#### Response Example
```
Hello

World

```
```

--------------------------------

### Example: Detaching a Child Process

Source: https://docs.ruby-lang.org/en/master/Process

This example demonstrates how to use `Process.detach` to manage a child process spawned by `Process.spawn`. It shows the process state before and after detaching to illustrate the prevention of zombie processes.

```ruby
pid = Process.spawn('ruby', '-e', 'exit 13') # => 312691
sleep(1)
# Find zombies.
system("ps -ho pid,state -p #{pid}")

pid = Process.spawn('ruby', '-e', 'exit 13') # => 313213
thread = Process.detach(pid)
sleep(1)

```

--------------------------------

### Get string representation of a stack frame

Source: https://docs.ruby-lang.org/en/master/Thread/Backtrace/Location

Demonstrates the `to_s` method of Thread::Backtrace::Location, which returns a string representation of the frame similar to the output of `Kernel#caller`. The example shows how this string is generated.

```c
static VALUE
location_to_str_m(VALUE self)
{
    return location_to_str(location_ptr(self));
}
```

--------------------------------

### Require net/http and Define URI and Hostname Variables

Source: https://docs.ruby-lang.org/en/master/Net/HTTPHeader

This snippet demonstrates how to include the 'net/http' library and set up essential variables like URI, hostname, and path for making HTTP requests. These variables are commonly used in examples for making requests to websites like jsonplaceholder.typicode.com or example.com.

```ruby
require 'net/http'\n\nuri = URI('https://jsonplaceholder.typicode.com/')\uri.freeze # Examples may not modify.\nhostname = uri.hostname # => "jsonplaceholder.typicode.com"\npath = uri.path         # => "/"\nport = uri.port         # => 443\n
```

--------------------------------

### Open3.pipeline_start with block for process synchronization

Source: https://docs.ruby-lang.org/en/master/Open3

Starts a pipeline of processes and executes a block of code with an array of Process::Waiter objects. The block synchronizes by calling 'join' on each waiter, ensuring all processes in the pipeline complete. Requires 'ls' and 'grep R' commands.

```ruby
Open3.pipeline_start('ls', 'grep R') do |wait_threads|
  wait_threads.each do |wait_thread|
    wait_thread.join
  end
end
```

--------------------------------

### Get pathname configuration variable using fpathconf() in Ruby

Source: https://docs.ruby-lang.org/en/master/IO

Retrieves a pathname configuration variable using fpathconf(). The _name_ parameter should be a constant from the Etc module starting with PC_. Returns an integer or nil for indefinite limits.

```Ruby
require 'etc'
IO.pipe do |r, w|
  p w.pathconf(Etc::PC_PIPE_BUF) #=> 4096
end
```

--------------------------------

### Basic HTTP Requests

Source: https://docs.ruby-lang.org/en/master/Net

Demonstrates basic GET and POST requests using Net::HTTP.

```APIDOC
## GET Request

### Description
Performs an HTTP GET request to a specified hostname and path.

### Method
GET

### Endpoint
`/<path>`

### Parameters
#### Path Parameters
- **hostname** (String) - Required - The hostname of the server.
- **path** (String) - Required - The path to the resource.

### Request Example
```ruby
require 'net/http'
require 'uri'

hostname = 'example.com'
path = '/resource'

response = Net::HTTP.get_response(hostname, path)
```

## POST Request

### Description
Performs an HTTP POST request with data to a specified URI.

### Method
POST

### Endpoint
`/<path>`

### Parameters
#### Path Parameters
- **uri** (URI) - Required - The URI to send the POST request to.
- **data** (String) - Required - The request body data.

### Request Example
```ruby
require 'net/http'
require 'uri'

uri = URI('http://example.com/resource')
data = '{"key": "value"}'

response = Net::HTTP.post(uri, data)
```

## POST Form Request

### Description
Performs an HTTP POST request with form-encoded parameters to a specified URI.

### Method
POST

### Endpoint
`/<path>`

### Parameters
#### Path Parameters
- **uri** (URI) - Required - The URI to send the POST request to.
- **params** (Hash) - Required - A hash of form parameters.

### Request Example
```ruby
require 'net/http'
require 'uri'

uri = URI('http://example.com/form')
params = {name: 'example', value: 'test'}

response = Net::HTTP.post_form(uri, params)
```

## PUT Request

### Description
Performs an HTTP PUT request with data to a specified URI.

### Method
PUT

### Endpoint
`/<path>`

### Parameters
#### Path Parameters
- **uri** (URI) - Required - The URI to send the PUT request to.
- **data** (String) - Required - The request body data.

### Request Example
```ruby
require 'net/http'
require 'uri'

uri = URI('http://example.com/resource')
data = '{"key": "updated_value"}'

response = Net::HTTP.put(uri, data)
```
```

--------------------------------

### IO.popen - Special Examples

Source: https://docs.ruby-lang.org/en/master/IO

Provides examples of advanced usage, including setting IO encoding and merging stderr with stdout.

```APIDOC
## IO.popen - Advanced Usage

### Description
Examples covering specific configurations like setting external encoding or merging standard error with standard output.

### Example 1: Setting IO Encoding
```ruby
IO.popen("nkf -e filename", :external_encoding=>"EUC-JP") {|nkf_io|
  euc_jp_string = nkf_io.read
}
```

### Example 2: Merging Standard Output and Standard Error
```ruby
IO.popen(["ls", "/", :err=>[:child, :out]]) do |io|
  ls_result_with_error = io.read
end
```
```

--------------------------------

### Initialize RubyGems OwnerCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/OwnerCommand

Initializes the OwnerCommand, setting up options for managing gem owners, including adding, removing, proxy, and host configurations.

```ruby
# File lib/rubygems/commands/owner_command.rb, line 37
def initialize
  super "owner", "Manage gem owners of a gem on the push server"
  add_proxy_option
  add_key_option
  add_otp_option
  defaults.merge! add: [], remove: []

  add_option "-a", "--add NEW_OWNER", "Add an owner by user identifier" do |value, options|
    options[:add] << value
  end

  add_option "-r", "--remove OLD_OWNER", "Remove an owner by user identifier" do |value, options|
    options[:remove] << value
  end

  add_option "-h", "--host HOST",
             "Use another gemcutter-compatible host",
             "  (e.g. https://rubygems.org)" do |value, options|
    options[:host] = value
  end
end
```

--------------------------------

### Net::HTTP#start

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Starts an HTTP session. It can be used with or without a block. When used with a block, the session is automatically finished upon block exit.

```APIDOC
## Net::HTTP#start

### Description
Starts an HTTP session. It can be used with or without a block. When used with a block, the session is automatically finished upon block exit.

### Method
`start` or `start { |http| ... }`

### Parameters
None

### Request Example

Without a block:
```ruby
http = Net::HTTP.new(hostname)
http.start
# => #<Net::HTTP jsonplaceholder.typicode.com:80 open=true>
http.started? # => true
http.finish
```

With a block:
```ruby
Net::HTTP.start(hostname) do |http|
  http.started?
end # => true
```

### Response
Returns `self` if no block is given, or the block's return value if a block is given. The session is active within the block.
```

--------------------------------

### Install Gems into a Specific Directory (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/RequestSet

Installs a set of gem requests into a specified directory. It manages the GEM_HOME environment variable and handles existing gems, allowing for overwrites if 'force' is true. It also triggers post-installation hooks.

```ruby
def install_into(dir, force = true, options = {})
  gem_home = ENV["GEM_HOME"]
  ENV["GEM_HOME"] = dir

  existing = force ? [] : specs_in(dir)
  existing.delete_if {|s| @always_install.include? s }

  dir = File.expand_path dir

  installed = []

  options[:development] = false
  options[:install_dir] = dir
  options[:only_install_dir] = true
  @prerelease = options[:prerelease]

  sorted_requests.each do |request|
    spec = request.spec

    if existing.find {|s| s.full_name == spec.full_name }
      yield request, nil if block_given?
      next
    end

    spec.install options do |installer|
      yield request, installer if block_given?
    end

    installed << request
  end

  install_hooks installed, options

  installed
ensure
  ENV["GEM_HOME"] = gem_home
end
```

--------------------------------

### Creating a New Range Instance in Ruby

Source: https://docs.ruby-lang.org/en/master/Range

This snippet shows the Ruby `Range.new` method, used to instantiate a new range object. It accepts start and end values, with an optional boolean to exclude the end value. Examples illustrate usage with integers and characters.

```ruby
Range.new(2, 5).to_a            # => [2, 3, 4, 5]
Range.new(2, 5, true).to_a      # => [2, 3, 4]
Range.new('a', 'd').to_a        # => ["a", "b", "c", "d"]
Range.new('a', 'd', true).to_a  # => ["a", "b", "c"]
```

--------------------------------

### Set up Visual C++ Build Environment

Source: https://docs.ruby-lang.org/en/master/windows_md

Commands to set up the necessary environment variables for building Ruby with the Visual C++ compiler on Windows. These commands prepare the native or cross-compilation environment.

```batch
cmd /k win32\vssetup.cmd
```

```batch
cmd /k win32\vssetup.cmd -arch=arm64
```

```batch
cmd /k win32\vssetup.cmd -arch=x64
```

--------------------------------

### Open3.popen3 Example with Block

Source: https://docs.ruby-lang.org/en/master/Open3

Demonstrates the basic usage of Open3.popen3 with a block, passing stdin, stdout, stderr, and a wait_thread to the block. It shows how to access process information like PID and exit status.

```ruby
# => [#<IO:fd 8>, #<IO:fd 10>, #<IO:fd 12>, #<Process::Waiter:0x00007f58d5428f58 run>]
stdin.close
stdout.close
stderr.close
wait_thread.pid   # => 2210481
wait_thread.value # => #<Process::Status: pid 2210481 exit 0>

Open3.popen3('echo') do |stdin, stdout, stderr, wait_thread|
  p stdin
  p stdout
  p stderr
  p wait_thread
  p wait_thread.pid
  p wait_thread.value
end

# Output:
# #<IO:fd 6>
# #<IO:fd 7>
# #<IO:fd 9>
# #<Process::Waiter:0x00007f58d53606e8 sleep>
# 2211047
# #<Process::Status: pid 2211047 exit 0>

```

--------------------------------

### Iterate Strongly Connected Components from Node (Ruby)

Source: https://docs.ruby-lang.org/en/master/TSort

Yields strongly connected components starting from a given node. Requires a node and a method to get its children. The graph representation can be dynamic. Avoids needing a full graph object.

```Ruby
def self.each_strongly_connected_component_from(node, each_child, id_map={}, stack=[]) # :yields: nodes
  return to_enum(__method__, node, each_child, id_map, stack) unless block_given?

  minimum_id = node_id = id_map[node] = id_map.size
  stack_length = stack.length
  stack << node

  each_child.call(node) {|child|
    if id_map.include? child
      child_id = id_map[child]
      minimum_id = child_id if child_id && child_id < minimum_id
    else
      sub_minimum_id =
        each_strongly_connected_component_from(child, each_child, id_map, stack) {|c|
          yield c
        }
      minimum_id = sub_minimum_id if sub_minimum_id < minimum_id
    end
  }

  if node_id == minimum_id
    component = stack.slice!(stack_length .. -1)
    component.each {|n| id_map[n] = nil}
    yield component
  end

  minimum_id
end
```

--------------------------------

### Prism LambdaNode Initialization

Source: https://docs.ruby-lang.org/en/master/Prism/LambdaNode

Details on how to initialize a new LambdaNode instance, including the parameters it accepts.

```APIDOC
## Public Class Methods

### new

Source:
```ruby
# File lib/prism/node.rb, line 11638
def initialize(source, node_id, location, flags, locals, operator_loc, opening_loc, closing_loc, parameters, body)
  @source = source
  @node_id = node_id
  @location = location
  @flags = flags
  @locals = locals
  @operator_loc = operator_loc
  @opening_loc = opening_loc
  @closing_loc = closing_loc
  @parameters = parameters
  @body = body
end
```

Initialize a new `LambdaNode` node.

### type

Source:
```ruby
# File lib/prism/node.rb, line 11761
def self.type
  :lambda_node
end
```

Return a symbol representation of this node type. See `Node::type`.
```

--------------------------------

### Get path of a stack frame

Source: https://docs.ruby-lang.org/en/master/Thread/Backtrace/Location

Illustrates the `path` method of Thread::Backtrace::Location, which returns the file name of the stack frame. This path may be relative if the frame is in the main script. The example shows how to retrieve it.

```c
static VALUE
location_path_m(VALUE self)
{
    const rb_iseq_t *iseq = location_iseq(location_ptr(self));
    return iseq ? rb_iseq_path(iseq) : Qnil;
}
```

--------------------------------

### Start YAML Stream

Source: https://docs.ruby-lang.org/en/master/Psych/Visitors/YAMLTree

Starts the YAML stream with a specified encoding and sets the visitor's state to started.

```ruby
def start encoding = Nodes::Stream::UTF8
  @emitter.start_stream(encoding).tap do
    @started = true
  end
end
```

--------------------------------

### Initialize Prism::Relocation::Repository

Source: https://docs.ruby-lang.org/en/master/Prism/Relocation/Repository

Initializes a new Prism::Relocation::Repository with a given source. It sets up internal data structures for fields and entries.

```ruby
def initialize(source)
  @source = source
  @fields = {}
  @entries = Hash.new { |hash, node_id| hash[node_id] = {} }
end
```

--------------------------------

### Get Socket Option Data as String (Ruby)

Source: https://docs.ruby-lang.org/en/master/Socket/Option

Returns the raw data associated with a socket option as a string. This method is also aliased as `to_s`. Example usage demonstrates creating an option and retrieving its packed integer data.

```Ruby
p Socket::Option.new(:INET6, :IPV6, :RECVPKTINFO, [1].pack("i!")).data
#=> "\x01\x00\x00\x00"
```

--------------------------------

### Ruby FileUtils ln: Verbose Output Examples

Source: https://docs.ruby-lang.org/en/master/FileUtils

Shows how to use the `verbose: true` option to print the equivalent shell command for creating hard links.

```Ruby
FileUtils.ln('tmp0/t.txt', 'tmp1/t.lnk', verbose: true)
FileUtils.ln('tmp2/t.dat', 'tmp3', verbose: true)
FileUtils.ln(['tmp0/t.txt', 'tmp2/t.dat'], 'tmp4/', verbose: true)
```

--------------------------------

### Get Proc Source Location

Source: https://docs.ruby-lang.org/en/master/Proc

This function retrieves the source location of a Ruby Proc object. It returns an array containing the filename, start line/column, and end line/column of the proc's definition. Returns nil for native procs.

```c
VALUE
rb_proc_location(VALUE self)
{
    return iseq_location(rb_proc_get_iseq(self, 0));
}
```

--------------------------------

### Initialize OpenSSL::Config from File

Source: https://docs.ruby-lang.org/en/master/OpenSSL/Config

Creates an OpenSSL::Config instance by loading configuration from a specified file. It handles file access and potential data validity errors.

```ruby
require 'openssl'

# Example usage:
config = OpenSSL::Config.new('/path/to/your/openssl.cnf')
```

```c
static VALUE
config_initialize(int argc, VALUE *argv, VALUE self)
{
    CONF *conf = GetConfig(self);
    VALUE filename;

    /* 0-arguments call has no use-case, but is kept for compatibility */
    rb_scan_args(argc, argv, "01", &filename);
    rb_check_frozen(self);
    if (!NIL_P(filename)) {
        BIO *bio = BIO_new_file(StringValueCStr(filename), "rb");
        if (!bio)
            ossl_raise(eConfigError, "BIO_new_file");
        config_load_bio(conf, bio); /* Consumes BIO */
    }
    rb_obj_freeze(self);
    return self;
}
```

--------------------------------

### Manage Ruby Dependencies with vcpkg

Source: https://docs.ruby-lang.org/en/master/windows_md

Demonstrates how to manage Ruby dependencies on the MSWin platform using vcpkg. It shows commands to update and install vcpkg packages within the build directory.

```makefile
nmake update-vcpkg # Update baseline version of vcpkg
nmake install-vcpkg # Install vcpkg from build directory
```

--------------------------------

### Example of PTY.open and spawning a process in Ruby

Source: https://docs.ruby-lang.org/en/master/PTY

Demonstrates how to use PTY.open to create a pseudo-terminal and spawn the 'factor' command, controlling its input and reading its output. It highlights the importance of proper pipe handling to avoid deadlocks.

```Ruby
# start by requiring the standard library PTY
require 'pty'

master, slave = PTY.open
read, write = IO.pipe
pid = spawn("factor", :in=>read, :out=>slave)
read.close     # we dont need the read
slave.close    # or the slave

# pipe "42" to the factor command
write.puts "42"
# output the response from factor
p master.gets #=> "42: 2 3 7\n"

# pipe "144" to factor and print out the response
write.puts "144"
p master.gets #=> "144: 2 2 2 2 3 3\n"
write.close # close the pipe

# The result of read operation when pty slave is closed is platform
# dependent.
ret = begin
        master.gets     # FreeBSD returns nil.
      rescue Errno::EIO # GNU/Linux raises EIO.
        nil
      end
p ret #=> nil

```

--------------------------------

### Constructing a SEQUENCE

Source: https://docs.ruby-lang.org/en/master/OpenSSL/ASN1/Constructive

Example demonstrating how to construct an ASN.1 SEQUENCE using OpenSSL::ASN1::Sequence.

```APIDOC
## Constructing a SEQUENCE

### Example
```ruby
int = OpenSSL::ASN1::Integer.new(1)
str = OpenSSL::ASN1::PrintableString.new('abc')
sequence = OpenSSL::ASN1::Sequence.new( [ int, str ] )
```
```

--------------------------------

### Set Algorithm for Request (Example)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/Timestamp/Request

An example snippet showing how to set the algorithm for a request, likely within a cryptographic context.

```Ruby
request.algorithm = "SHA1"
```

--------------------------------

### TCPServer Creation and Basic Usage

Source: https://docs.ruby-lang.org/en/master/TCPServer

Demonstrates how to create a basic TCP server that listens on a specified port and handles incoming client connections.

```APIDOC
## TCPServer Creation and Basic Usage

### Description
This section shows how to initialize a `TCPServer` to listen on a specific port and demonstrates a simple loop to accept and interact with clients.

### Example 1: Simple Server
```ruby
require 'socket'

server = TCPServer.new 2000 # Server bind to port 2000
loop do
  client = server.accept    # Wait for a client to connect
  client.puts "Hello !"
  client.puts "Time is #{Time.now}"
  client.close
end
```

### Example 2: Multi-client Server using Threads
```ruby
require 'socket'

server = TCPServer.new 2000
loop do
  Thread.start(server.accept) do |client|
    client.puts "Hello !"
    client.puts "Time is #{Time.now}"
    client.close
  end
end
```
```

--------------------------------

### Ruby Regex: Derived Core Unicode Properties

Source: https://docs.ruby-lang.org/en/master/regexp/unicode_properties_rdoc

Explains the usage of derived core properties in Ruby regular expressions, which are combinations or refinements of other Unicode properties. Examples include Alphabetic, Cased, Grapheme Base, and ID Start.

```ruby
\p{Alphabetic}
\p{Case_Ignorable}
\p{Cased}
\p{Changes_When_Casefolded}
\p{Changes_When_Casemapped}
\p{Changes_When_Lowercased}
\p{Changes_When_Titlecased}
\p{Changes_When_Uppercased}
\p{Default_Ignorable_Code_Point}
\p{Grapheme_Base}
\p{Grapheme_Extend}
\p{Grapheme_Link}
\p{ID_Continue}
\p{ID_Start}
\p{InCB_Consonant}
\p{InCB_Extend}
\p{InCB_Linker}
\p{Lowercase}
\p{Math}
\p{Uppercase}
\p{XID_Continue}
\p{XID_Start}
```

--------------------------------

### Get line number of a stack frame

Source: https://docs.ruby-lang.org/en/master/Thread/Backtrace/Location

Demonstrates the `lineno` method of Thread::Backtrace::Location, which returns the line number of the stack frame. The example shows how to access this information from a location object obtained via `caller_locations`.

```c
static VALUE
location_lineno_m(VALUE self)
{
    return INT2FIX(location_lineno(location_ptr(self)));
}
```

--------------------------------

### Ruby Resolv: Constructor - initialize

Source: https://docs.ruby-lang.org/en/master/Resolv

Initializes a new Resolv object, optionally configuring it with custom resolvers or enabling IPv6 support. It defaults to using Hosts and DNS resolvers.

```ruby
# File lib/resolv.rb, line 88
def initialize(resolvers=(arg_not_set = true; nil), use_ipv6: (keyword_not_set = true; nil))
  if !keyword_not_set && !arg_not_set
    warn "Support for separate use_ipv6 keyword is deprecated, as it is ignored if an argument is provided. Do not provide a positional argument if using the use_ipv6 keyword argument.", uplevel: 1
  end

  @resolvers = case resolvers
  when Hash, nil
    [Hosts.new, DNS.new(DNS::Config.default_config_hash.merge(resolvers || {}))]
  else
    resolvers
  end
end
```

--------------------------------

### Download installed gem (no-op)

Source: https://docs.ruby-lang.org/en/master/Gem/Source/Installed

Handles the download process for an installed gem. This method is a no-operation (returns nil) because installed gems do not require downloading.

```ruby
# File lib/rubygems/source/installed.rb, line 30
def download(spec, path)
  nil
end
```

--------------------------------

### Prism::BeginNode Initialization in Ruby

Source: https://docs.ruby-lang.org/en/master/Prism/BeginNode

This method shows the initialization process for a Prism::BeginNode object, detailing the parameters required to construct a new node.

```ruby
# File lib/prism/node.rb, line 1497
def initialize(source, node_id, location, flags, begin_keyword_loc, statements, rescue_clause, else_clause, ensure_clause, end_keyword_loc)
  @source = source
  @node_id = node_id
  @location = location
  @flags = flags
  @begin_keyword_loc = begin_keyword_loc
  @statements = statements
  @rescue_clause = rescue_clause
  @else_clause = else_clause
  @ensure_clause = ensure_clause
  @end_keyword_loc = end_keyword_loc
end
```

--------------------------------

### File::Stat - Get File Status Information

Source: https://docs.ruby-lang.org/en/master/IO

Retrieves status information for an IO object as a File::Stat object. This includes details like file mode, block size, and access time. The example shows how to access these attributes.

```ruby
f = File.new("testfile")
s = f.stat
"%o" % s.mode   #=> "100644"
s.blksize       #=> 4096
s.atime         #=> Wed Apr 09 08:53:54 CDT 2003
```

--------------------------------

### Ruby File Size Method

Source: https://docs.ruby-lang.org/en/master/File

Demonstrates how to retrieve the size of a file in bytes using `File#size` in Ruby. This method returns an integer representing the file's size. The example shows getting the size of a file named 'testfile'.

```Ruby
File.new("testfile").size   #=> 66
```

--------------------------------

### Ruby Array Shuffle! Example

Source: https://docs.ruby-lang.org/en/master/Array

Demonstrates the in-place shuffle! method with example arrays, including handling duplicate elements.

```ruby
a =             [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
a.shuffle! # => [5, 3, 8, 7, 6, 1, 9, 4, 2, 0]
a.shuffle! # => [9, 4, 0, 6, 2, 8, 1, 5, 3, 7]

a =             [0, 1, 0, 1, 0, 1, 0, 1, 0, 1]
a.shuffle! # => [1, 0, 0, 1, 1, 0, 1, 0, 0, 1]
a.shuffle! # => [0, 1, 0, 1, 1, 0, 1, 0, 1, 0]
```

--------------------------------

### Install Dependencies with Bundler

Source: https://docs.ruby-lang.org/en/master/contributing/making_changes_to_stdlibs_md

Installs all necessary dependencies for a Ruby project using the Bundler tool. This is a prerequisite for many development tasks.

```bash
bundle install

```

--------------------------------

### Get Socket Protocol of Addrinfo in Ruby

Source: https://docs.ruby-lang.org/en/master/Addrinfo

This Ruby method returns the socket protocol of an Addrinfo object as an integer. Common values include Socket::IPPROTO_TCP for TCP and Socket::IPPROTO_UDP for UDP. The example demonstrates checking if the protocol is TCP.

```ruby
static VALUE
addrinfo_protocol(VALUE self)
{
    rb_addrinfo_t *rai = get_addrinfo(self);
    return INT2NUM(rai->protocol);
}
```

```ruby
Addrinfo.tcp("localhost", 80).protocol == Socket::IPPROTO_TCP #=> true
```

--------------------------------

### List Extensions - Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Returns a list of paths to extension files (e.g., extconf.rb) that need to be compiled during gem installation.

```ruby
# File lib/rubygems/specification.rb, line 588
def extensions
  @extensions ||= []
end

```

```ruby
spec.extensions << 'ext/rmagic/extconf.rb'

```

--------------------------------

### Ruby OptionParser: parse! Method Example

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Illustrates the usage of the `parse!` method from Ruby's OptionParser. This method parses command-line arguments, modifying the argument list in place and returning the remaining arguments. It shows how parsing can be terminated by a '--' argument or by the POSIXLY_CORRECT environment variable.

```ruby
require 'optparse'

parser = OptionParser.new
parser.on('--xxx') do |value|
  p ['--xxx', value]
end
parser.on('--yyy YYY') do |value|
  p ['--yyy', value]
end
parser.on('--zzz [ZZZ]') do |value|
  p ['--zzz', value]
end

ret = parser.parse! # Parses ARGV in-place
puts "Returned: #{ret} (#{ret.class})"

```

--------------------------------

### Net::HTTP#started?

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Checks if the HTTP session has been started.

```APIDOC
## Net::HTTP#started?

### Description
Returns `true` if the HTTP session has been started, `false` otherwise.

### Method
`started?`

### Parameters
None

### Request Example
```ruby
http = Net::HTTP.new(hostname)
http.started? # => false
http.start
http.started? # => true
http.finish
http.started? # => false

Net::HTTP.start(hostname) do |http|
  http.started?
end # => true
```

### Response
Returns a boolean value (`true` or `false`).
```

--------------------------------

### Diffie-Hellman Key Exchange Example

Source: https://docs.ruby-lang.org/en/master/OpenSSL/PKey/DH

Demonstrates a full Diffie-Hellman key exchange process between two parties.

```APIDOC
## Example of a Key Exchange

### Description
This example illustrates a secure Diffie-Hellman key exchange between two parties.

### Code Example
```ruby
# Party 1: Generates parameters and public key
dh1 = OpenSSL::PKey::DH.new(2048)
der = dh1.to_der
pub1 = dh1.pub_key

# Party 2: Generates its key pair using parameters from Party 1
dhparams = OpenSSL::PKey::DH.new(der)
dh2 = OpenSSL::PKey.generate_key(dhparams)
pub2 = dh2.pub_key

# Both parties compute the shared secret
symm_key1 = dh1.compute_key(pub2)
symm_key2 = dh2.compute_key(pub1)

puts symm_key1 == symm_key2 # Output: true
```
```

--------------------------------

### Passing Arguments to Executable with Open3.popen3

Source: https://docs.ruby-lang.org/en/master/Open3

Shows how to pass arguments to an executable when using Open3.popen3. Multiple arguments can be provided after the command path, and the example demonstrates passing arguments to 'echo'.

```Ruby
Open3.popen3('echo', 'C #') { |i, o, e, t| o.gets }
Open3.popen3('echo', 'hello', 'world') { |i, o, e, t| o.gets }
```

--------------------------------

### Initialize Resolv::DNS::Resource::TXT in Ruby

Source: https://docs.ruby-lang.org/en/master/Resolv/DNS/Resource/TXT

Initializes a new TXT resource record with one or more strings. This constructor takes the first string and any subsequent strings as arguments.

```ruby
def initialize(first_string, *rest_strings)
  @strings = [first_string, *rest_strings]
end
```

--------------------------------

### Yield in Cooked Mode - Ruby IO

Source: https://docs.ruby-lang.org/en/master/IO

Yields the IO object within cooked mode. This enables echo and line editing for terminal input. Requires 'io/console'. Example usage: STDIN.cooked(&:gets) reads a line with standard terminal behavior.

```c
static VALUE
console_cooked(VALUE io)
{
    return ttymode(io, rb_yield, io, set_cookedmode, NULL);
}
```

--------------------------------

### Perform Pre-installation Checks for RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Executes essential checks before installing a gem. This includes verifying the gem home directory, ensuring the spec is loadable, checking Ruby and gem version requirements, and verifying that all dependencies are met (unless installation is forced or dependencies are ignored).

```ruby
def pre_install_checks
  verify_gem_home

  # The name and require_paths must be verified first, since it could contain
  # ruby code that would be eval'ed in #ensure_loadable_spec
  verify_spec

  ensure_loadable_spec

  if options[:install_as_default]
    Gem.ensure_default_gem_subdirectories gem_home
  else
    Gem.ensure_gem_subdirectories gem_home
  end

  return true if @force

  ensure_dependencies_met unless @ignore_dependencies

  true
end
```

--------------------------------

### TSort: each_strongly_connected_component Examples

Source: https://docs.ruby-lang.org/en/master/TSort

Provides examples of using the `TSort.each_strongly_connected_component` class method with different graph structures represented by lambda functions for node and child iteration. Demonstrates the output for various dependency scenarios.

```ruby
g = {1=>[2, 3], 2=>[4], 3=>[2, 4], 4=>[]}
each_node = lambda {|&b| g.each_key(&b) }
each_child = lambda {|n, &b| g[n].each(&b) }
TSort.each_strongly_connected_component(each_node, each_child) {|scc| p scc }
#=> [4]
#   [2]
#   [3]
#   [1]

g = {1=>[2], 2=>[3, 4], 3=>[2], 4=>[]}
each_node = lambda {|&b| g.each_key(&b) }
each_child = lambda {|n, &b| g[n].each(&b) }
TSort.each_strongly_connected_component(each_node, each_child) {|scc| p scc }
#=> [4]
#   [2, 3]
#   [1]


```

--------------------------------

### Create and Accept on UNIXServer (Ruby)

Source: https://docs.ruby-lang.org/en/master/UNIXServer

Demonstrates creating a UNIXServer socket bound to a specific path and accepting an incoming connection. This is useful for inter-process communication on Unix-like systems.

```Ruby
require 'socket'

serv = UNIXServer.new("/tmp/sock")
s = serv.accept
p s.read
```

--------------------------------

### Get Message Location from Prism Node

Source: https://docs.ruby-lang.org/en/master/Prism/CallAndWriteNode

The message_loc method returns the location of the message within the source code. It handles cases where the location is nil or an encoded integer, converting it to a Location object if necessary. The example shows how '&&=' extracts the message part.

```Ruby
def message_loc
  location = @message_loc
  case location
  when nil
    nil
  when Location
    location
  else
    @message_loc = Location.new(source, location >> 32, location & 0xFFFFFFFF)
  end
end
```

--------------------------------

### Install All Development Dependencies Recursively

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Installs development dependencies for all gems, including their own development dependencies. This ensures a complete development environment is set up.

```ruby
add_option(:'Install/Update', "--development-all",
              "Install development dependencies for all",
              "gems (including dev deps themselves)") do |_value, options|
    options[:development] = true
    options[:dev_shallow] = false
  end
```

--------------------------------

### Execute commands and pipe output using pipeline_w (Ruby)

Source: https://docs.ruby-lang.org/en/master/Open3

Demonstrates using `Open3.pipeline_w` to execute a sequence of commands. It pipes the standard output of the first command ('sort') to the standard input of the second ('cat -n'). The example includes writing to the stdin of the first process and joining wait threads.

```Ruby
Open3.pipeline_w('sort', 'cat -n') do |first_stdin, wait_threads|
  first_stdin.puts("foo\nbar\nbaz")
  first_stdin.close # Send EOF to sort.
  wait_threads.each do |wait_thread|
    wait_thread.join
  end
end
```

--------------------------------

### Open3.pipeline_start

Source: https://docs.ruby-lang.org/en/master/Open3

Starts multiple processes and pipes their output to the next process's input. It returns an array of Process::Waiter objects for each process. If a block is given, it's executed with the array of wait threads.

```APIDOC
## Open3.pipeline_start

### Description
Starts multiple processes and pipes their output to the next process's input. It returns an array of Process::Waiter objects for each process. If a block is given, it's executed with the array of wait threads.

### Method
`Open3.pipeline_start(*cmds)`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **cmds** (Array<String | Array<String>>) - An array of commands to execute in a pipeline. Each command can be a string or an array of strings (executable path and arguments).

### Request Example
```ruby
Open3.pipeline_start('ls', 'grep R') do |wait_threads|
  wait_threads.each do |wait_thread|
    wait_thread.join
  end
end
```

### Response
#### Success Response (200)
- **wait_threads** (Array<Process::Waiter>) - An array of Process::Waiter objects, one for each process started in the pipeline.

#### Response Example
```ruby
# => [#<Process::Waiter:0x000055e8de9d2bb0 run>, #<Process::Waiter:0x000055e8de9d2890 run>]
```

### Additional Notes
- Potential security vulnerabilities if called with untrusted input (see Command Injection).
- Environment variables (`env`) and options can be passed as the first or last hash argument, respectively.
```

--------------------------------

### Psych::Visitors::Emitter Instance Methods

Source: https://docs.ruby-lang.org/en/master/Psych/Visitors/Emitter

Documentation for the public instance methods of Psych::Visitors::Emitter.

```APIDOC
## Psych::Visitors::Emitter#visit_Psych_Nodes_Alias

### Description
Visits a Psych::Nodes::Alias node.

### Method
GET

### Endpoint
/websites/ruby-lang_en_master

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
None

#### Response Example
None
```

```APIDOC
## Psych::Visitors::Emitter#visit_Psych_Nodes_Document

### Description
Visits a Psych::Nodes::Document node.

### Method
GET

### Endpoint
/websites/ruby-lang_en_master

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
None

#### Response Example
None
```

```APIDOC
## Psych::Visitors::Emitter#visit_Psych_Nodes_Mapping

### Description
Visits a Psych::Nodes::Mapping node.

### Method
GET

### Endpoint
/websites/ruby-lang_en_master

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
None

#### Response Example
None
```

```APIDOC
## Psych::Visitors::Emitter#visit_Psych_Nodes_Scalar

### Description
Visits a Psych::Nodes::Scalar node.

### Method
GET

### Endpoint
/websites/ruby-lang_en_master

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
None

#### Response Example
None
```

```APIDOC
## Psych::Visitors::Emitter#visit_Psych_Nodes_Sequence

### Description
Visits a Psych::Nodes::Sequence node.

### Method
GET

### Endpoint
/websites/ruby-lang_en_master

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
None

#### Response Example
None
```

```APIDOC
## Psych::Visitors::Emitter#visit_Psych_Nodes_Stream

### Description
Visits a Psych::Nodes::Stream node.

### Method
GET

### Endpoint
/websites/ruby-lang_en_master

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
None

#### Response Example
None
```

--------------------------------

### OpenSSL X509Store#verify_callback=

Source: https://docs.ruby-lang.org/en/master/OpenSSL/X509/Store

General callback for `OpenSSL` verify.

```APIDOC
## OpenSSL X509Store#verify_callback=

### Description
Sets a general callback for `OpenSSL` verify operations.

### Method
PUT

### Endpoint
/x509store/:store_id/verify_callback

### Parameters
#### Path Parameters
- **store_id** (integer) - Required - The ID of the X509 store.

#### Request Body
- **cb** (object) - Required - The callback function or object.

### Request Example
```json
{
  "cb": "your_callback_function"
}
```

### Response
#### Success Response (200)
- **cb** (object) - The callback that was set.

#### Response Example
```json
{
  "cb": "your_callback_function"
}
```
```

--------------------------------

### Ruby File mtime Method

Source: https://docs.ruby-lang.org/en/master/File

Shows how to get the modification time of a file using `File#mtime` in Ruby. This method returns the time when the file's content was last modified. The example demonstrates retrieving the mtime for a file named 'testfile'.

```Ruby
File.new("testfile").mtime   #=> Wed Apr 09 08:53:14 CDT 2003
```

--------------------------------

### Get Block Length of SHA2 Digest in Ruby

Source: https://docs.ruby-lang.org/en/master/Digest/SHA2

Demonstrates how to retrieve the block length of a SHA2 digest object in bytes. Examples are provided for SHA256, SHA384, and SHA512, showing their respective block lengths in bits when multiplied by 8.

```ruby
# File ext/digest/sha2/lib/sha2.rb, line 112
def block_length
  @sha2.block_length
end

# Example usage:
Digest::SHA256.new.block_length * 8
# => 512
Digest::SHA384.new.block_length * 8
# => 1024
Digest::SHA512.new.block_length * 8
# => 1024
```

--------------------------------

### Prism::SourceFileNode Initialization

Source: https://docs.ruby-lang.org/en/master/Prism/SourceFileNode

Shows the constructor for the `SourceFileNode` class, detailing the parameters required for initializing a new node. These include source, node ID, location, flags, and the file path.

```Ruby
# File lib/prism/node.rb, line 16712
def initialize(source, node_id, location, flags, filepath)
  @source = source
  @node_id = node_id
  @location = location
  @flags = flags
  @filepath = filepath
end
```

--------------------------------

### Initialize Gem::Ext::CargoBuilder

Source: https://docs.ruby-lang.org/en/master/Gem/Ext/CargoBuilder

Initializes the CargoBuilder with default settings. Requires necessary helper modules and sets up the runner and profile.

```ruby
# File lib/rubygems/ext/cargo_builder.rb, line 9
def initialize
  require_relative "../command"
  require_relative "ext/cargo_builder/link_flag_converter"

  @runner = self.class.method(:run)
  @profile = :release
end
```

--------------------------------

### Ruby: Basic Case Statement Example

Source: https://docs.ruby-lang.org/en/master/Prism/CaseNode

Demonstrates the basic structure of a Ruby case statement as represented by the Prism::CaseNode.

```ruby
case true
when false
end
^^^^^^^^^^
```

--------------------------------

### Ruby expm1() Function Usage Examples

Source: https://docs.ruby-lang.org/en/master/Math

Shows examples of the expm1 function, calculating e^x - 1 for various inputs including infinities and negative values. Highlights results like 1.0/E - 1.

```ruby
expm1(-INFINITY) # => 0.0
expm1(-1.0)      # => -0.6321205588285577 # 1.0/E - 1
expm1(0.0)       # => 0.0
expm1(0.5)       # => 0.6487212707001282  # sqrt(E) - 1
expm1(1.0)       # => 1.718281828459045   # E - 1
expm1(2.0)       # => 6.38905609893065    # E**2 - 1
expm1(INFINITY)  # => Infinity
```

--------------------------------

### Option Definition Methods

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Explains methods for defining options, such as `define`, `define_head`, `define_tail`, `on`, `on_head`, and `on_tail`. These methods allow customization of how options are added to the parser.

```APIDOC
## Option Definition Methods

### Description
Methods for defining command-line options. These methods allow you to create an option and append or prepend it to lists, or append it to the base list.

### Methods Overview:

- **`OptionParser#define(arg, ...)`**: Appends the created option to the top list.
- **`OptionParser#define_head(arg, ...)`**: Prepends the created option to the top list.
- **`OptionParser#define_tail(arg, ...)`**: Appends the created option to the base list.
- **`OptionParser#on(arg, ...)`**: Identical to `define`, but returns the parser object (`self`).
- **`OptionParser#on_head(arg, ...)`**: Identical to `define_head`, but returns the parser object (`self`).
- **`OptionParser#on_tail(arg, ...)`**: Identical to `define_tail`, but returns the parser object (`self`).
- **`OptionParser#make_switch(parameters, block)`**: The core method for defining an option. Accepts an array of parameters and a block. Returns an array containing the option object, names, and other values.

### Parameters for New Options
Refer to the `Parameters for New Options` section for details on arguments accepted by these methods.
```

--------------------------------

### Configure Ruby Build with vcpkg Path (Visual C++)

Source: https://docs.ruby-lang.org/en/master/windows_md

Specifying the vcpkg installation directory using the --with-opt-dir option when configuring the Ruby build with Visual C++.

```batch
win32\configure.bat --with-opt-dir=C:/vcpkg_installed/x64-windows
```

--------------------------------

### Ruby Hash Data Syntax Examples

Source: https://docs.ruby-lang.org/en/master/Hash

Demonstrates various syntaxes for creating Ruby Hash objects, including the 'hash rocket' (`=>`), JSON-style syntax for symbols, string keys, mixed styles, and using context for values.

```Ruby
h = {:foo => 0, :bar => 1, :baz => 2}
h # => {foo: 0, bar: 1, baz: 2}
```

```Ruby
h = {foo: 0, bar: 1, baz: 2}
h # => {foo: 0, bar: 1, baz: 2}
```

```Ruby
h = {'foo': 0, 'bar': 1, 'baz': 2}
h # => {foo: 0, bar: 1, baz: 2}
```

```Ruby
h = {foo: 0, :bar => 1, 'baz': 2}
h # => {foo: 0, bar: 1, baz: 2}
```

```Ruby
# Raises SyntaxError (syntax error, unexpected ':', expecting =>):
h = {0: 'zero'}
```

```Ruby
x = 0
y = 100
h = {x:, y:}
h # => {x: 0, y: 100}
```

--------------------------------

### Get label of a stack frame

Source: https://docs.ruby-lang.org/en/master/Thread/Backtrace/Location

Shows the `label` method of Thread::Backtrace::Location, which returns the decorated label of the frame, including method, class, or module names. The example demonstrates its output in different contexts, including within blocks.

```c
static VALUE
location_label_m(VALUE self)
{
    return location_label(location_ptr(self));
}
```

--------------------------------

### Process.initgroups

Source: https://docs.ruby-lang.org/en/master/Process

Initializes the supplemental group access list for a user.

```APIDOC
## Process.initgroups

### Description
Sets the supplemental group access list. The new list includes the group IDs of groups to which the specified `username` belongs, and the `base_grp` ID.

### Method
POST

### Endpoint
`/process/initgroups`

### Parameters
#### Request Body
- **username** (String) - Required - The username for whom to initialize group memberships.
- **base_grp** (Integer) - Required - The base group ID to include.

### Request Example
```json
{
  "username": "me",
  "base_grp": 30
}
```

### Response
#### Success Response (200)
- **groups** (Array<Integer>) - The initialized array of supplemental group IDs.

### Response Example
```json
{
  "groups": [
    30,
    6,
    10,
    11
  ]
}
```

### Notes
- Not available on all platforms.
```

--------------------------------

### Get Code Unit Offsets Field Values

Source: https://docs.ruby-lang.org/en/master/Prism/Relocation/CodeUnitOffsetsField

Retrieves the start and end code unit offsets for a given value. It utilizes a cached value obtained from the repository and encoding to fetch these offsets. This method is essential for accessing the core data managed by the field.

```ruby
def fields(value)
  {
    start_code_units_offset: value.cached_start_code_units_offset(cache),
    end_code_units_offset: value.cached_end_code_units_offset(cache)
  }
end
```

--------------------------------

### Ruby Array Shuffle Example

Source: https://docs.ruby-lang.org/en/master/Array

Demonstrates the usage of the shuffle method with example arrays, including handling duplicate elements.

```ruby
a =            [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
a.shuffle # => [0, 8, 1, 9, 6, 3, 4, 7, 2, 5]
a.shuffle # => [8, 9, 0, 5, 1, 2, 6, 4, 7, 3]

a =            [0, 1, 0, 1, 0, 1, 0, 1, 0, 1]
a.shuffle # => [1, 0, 1, 1, 0, 0, 1, 0, 0, 1]
a.shuffle # => [1, 1, 0, 0, 0, 1, 1, 0, 0, 1]
```

--------------------------------

### Ruby Fiber Backtrace Retrieval

Source: https://docs.ruby-lang.org/en/master/Fiber

Retrieves the call stack (backtrace) of a Ruby Fiber. The `backtrace` method returns an array of strings, where each string represents a frame in the call stack. It can be called with no arguments to get the full backtrace, or with arguments to specify a range or starting point.

```ruby
f.backtrace
#=> []

f.resume

f.backtrace
#=> ["test.rb:2:in `yield'", "test.rb:2:in `level3'", "test.rb:6:in `level2'", "test.rb:10:in `level1'", "test.rb:13:in `block in <main>'"]
p f.backtrace(1) # start from the item 1
#=> ["test.rb:2:in `level3'", "test.rb:6:in `level2'", "test.rb:10:in `level1'", "test.rb:13:in `block in <main>'"]
p f.backtrace(2, 2) # start from item 2, take 2
#=> ["test.rb:6:in `level2'", "test.rb:10:in `level1'"]
p f.backtrace(1..3) # take items from 1 to 3
#=> ["test.rb:2:in `level3'", "test.rb:6:in `level2'", "test.rb:10:in `level1'"]

f.resume
```

--------------------------------

### Initialize RubyGems ServerCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/ServerCommand

Initializes the ServerCommand, setting its name and description. It attempts to activate the 'rubygems-server' gem, handling potential load errors gracefully.

```ruby
def initialize
  super("server", "Starts up a web server that hosts the RDoc (requires rubygems-server)")
  begin
    Gem::Specification.find_by_name("rubygems-server").activate
  rescue Gem::LoadError
    # no-op
  end
end
```

--------------------------------

### Check if Installed Gem Option is Set

Source: https://docs.ruby-lang.org/en/master/Gem/QueryUtils

Determines if the '--installed' or '--no-installed' option has been used in the query. This flag influences whether the gem installation status is checked.

```Ruby
def check_installed_gems?
  !options[:installed].nil?
end
```

--------------------------------

### Get Socket Type of Addrinfo in Ruby

Source: https://docs.ruby-lang.org/en/master/Addrinfo

This Ruby method returns the socket type of an Addrinfo object as an integer. Typical values include Socket::SOCK_STREAM for TCP sockets and Socket::SOCK_DGRAM for UDP sockets. The example verifies if the socket type is SOCK_STREAM.

```ruby
static VALUE
addrinfo_socktype(VALUE self)
{
    rb_addrinfo_t *rai = get_addrinfo(self);
    return INT2NUM(rai->socktype);
}
```

```ruby
Addrinfo.tcp("localhost", 80).socktype == Socket::SOCK_STREAM #=> true
```

--------------------------------

### Initialize Gem::Platform (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Platform

Constructs a new Gem::Platform object from various input formats, including arrays, strings, or another Gem::Platform object. It parses the architecture string to set CPU, OS, and version.

```ruby
# File lib/rubygems/platform.rb, line 86
def initialize(arch)
  case arch
  when Array then
    @cpu, @os, @version = arch
  when String then
    cpu, os = arch.sub(/-+$/, "").split("-", 2)

    @cpu = if cpu&.match?(/i\d86/)
      "x86"
    else
      cpu
    end

    if os.nil?
      @cpu = nil
      os = cpu
    end # legacy jruby

    @os, @version = case os
                    when /aix-?(\d+)?/ then                ["aix",     $1]
                    when /cygwin/ then                     ["cygwin",  nil]
                    when /darwin-?(\d+)?/ then             ["darwin",  $1]
                    when "macruby" then                    ["macruby", nil]
                    when /^macruby-?(\d+(?:\.\d+)*)?/ then ["macruby", $1]
                    when /freebsd-?(\d+)?/ then            ["freebsd", $1]
                    when "java", "jruby" then              ["java",    nil]
                    when /^java-?(\d+(?:\.\d+)*)?/ then    ["java",    $1]
                    when /^dalvik-?(\d+)?$/ then           ["dalvik",  $1]
                    when /^dotnet$/ then                   ["dotnet",  nil]
                    when /^dotnet-?(\d+(?:\.\d+)*)?/ then  ["dotnet",  $1]
                    when /linux-?(\w+)?/ then              ["linux",   $1]
                    when /mingw32/ then                    ["mingw32", nil]
                    when /mingw-?(\w+)?/ then              ["mingw",   $1]
                    when /(mswin\d+)(?:[_-](\d+))?/ then
                      os = $1
                      version = $2
                      @cpu = "x86" if @cpu.nil? && os.end_with?("32")
                      [os, version]
                    when /netbsdelf/ then                  ["netbsdelf", nil]
                    when /openbsd-?(\d+\.\d+)?/ then       ["openbsd",   $1]
                    when /solaris-?(\d+\.\d+)?/ then       ["solaris",   $1]
                    when /wasi/ then                       ["wasi",      nil]
                    # test
                    when /^(\w+_platform)-?(\d+)?/ then    [$1,          $2]
                    else ["unknown", nil]
    end
  when Gem::Platform then
    @cpu = arch.cpu
    @os = arch.os
    @version = arch.version
  else
    raise ArgumentError, "invalid argument #{arch.inspect}"
  end
end
```

--------------------------------

### Get Protocol Family of Addrinfo in Ruby

Source: https://docs.ruby-lang.org/en/master/Addrinfo

This Ruby method retrieves the protocol family of an Addrinfo object as an integer. It's used to determine if an address is for IPv4 (PF_INET) or IPv6 (PF_INET6), among others. The example shows comparing the result with Socket::PF_INET.

```ruby
static VALUE
addrinfo_pfamily(VALUE self)
{
    rb_addrinfo_t *rai = get_addrinfo(self);
    return INT2NUM(rai->pfamily);
}
```

```ruby
Addrinfo.tcp("localhost", 80).pfamily == Socket::PF_INET #=> true
```

--------------------------------

### Ruby Time Comparison (Examples)

Source: https://docs.ruby-lang.org/en/master/Time

Examples demonstrating Ruby's Time#<=> method for comparing Time objects. It shows comparisons based on time differences and nanosecond precision.

```ruby
t = Time.now     # => 2007-11-19 08:12:12 -0600
t2 = t + 2592000 # => 2007-12-19 08:12:12 -0600
t <=> t2         # => -1
t2 <=> t         # => 1

t = Time.now     # => 2007-11-19 08:13:38 -0600
t2 = t + 0.1     # => 2007-11-19 08:13:38 -0600
t.nsec           # => 98222999
t2.nsec          # => 198222999
t <=> t2         # => -1
t2 <=> t         # => 1
t <=> t          # => 0
```

--------------------------------

### Get base label of a stack frame

Source: https://docs.ruby-lang.org/en/master/Thread/Backtrace/Location

Illustrates the `base_label` method of Thread::Backtrace::Location. This method returns the base label of the frame, typically the method or function name without any decorations. The example shows its output within nested blocks.

```c
static VALUE
location_base_label_m(VALUE self)
{
    return location_base_label(location_ptr(self));
}
```

--------------------------------

### OpenSSL::X509::Extension Instance Methods

Source: https://docs.ruby-lang.org/en/master/OpenSSL/X509/Extension

Provides documentation for instance methods of the OpenSSL::X509::Extension class, including equality checks, critical flag management, OID and value retrieval/setting, and conversion to different formats.

```APIDOC
## OpenSSL::X509::Extension Instance Methods

### Description
Details on how to compare extensions, manage their critical status, access their OID and value, and convert them to arrays, DER, or hash formats.

### Methods

#### `== (other)`

Compares this extension with another object for equality. Returns `true` if the other object is an `Extension` and has the same DER encoding.

#### `critical= (flag)`

Sets the critical flag of the extension. `flag` should be a boolean value.

#### `critical? ()`

Returns `true` if the extension is marked as critical, `false` otherwise.

#### `oid ()`

Returns the OID of the extension as a string. If a standard name exists for the OID, it is returned; otherwise, the OID string itself is returned.

#### `oid= (oid_string)`

Sets the OID of the extension using the provided string. The string can be an OID or a recognized extension name.

#### `to_a ()`

Returns an array representation of the extension: `[oid, value, critical?]`.

#### `to_der ()`

Returns the DER-encoded string representation of the extension.

#### `to_h ()`

Returns a hash representation of the extension with keys `"oid"`, `"value"`, and `"critical"`.
```

--------------------------------

### Net::HTTP#get

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Sends a GET request to the server.

```APIDOC
## Net::HTTP#get

### Description
Sends a `GET` request to the server for a given path. It returns an instance of a subclass of `Net::HTTPResponse`. An optional block can be provided to process the response.

### Method

`get(path, initheader = nil) {|res| ... }`

### Parameters
#### Path Parameters
* **path** (String) - The path to the resource to retrieve.
* **initheader** (Hash, optional) - A hash of initial headers to send with the request.

### Request Example
```ruby
http = Net::HTTP.new(hostname)
response = http.get('/todos/1')
puts response.body
```

### Response
#### Success Response (200)
An instance of a subclass of `Net::HTTPResponse`.

#### Response Example
```json
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```
```

--------------------------------

### Open3.pipeline_start: Start a pipeline without waiting (Ruby)

Source: https://docs.ruby-lang.org/en/master/Open3

Starts a pipeline of commands, creating child processes via Process.spawn but not waiting for them to exit. It returns an array of wait threads. This is useful for background process management.

```Ruby
wait_threads = Open3.pipeline_start('ls', 'grep R')
```

--------------------------------

### Ruby UDPSocket Send and Receive Example

Source: https://docs.ruby-lang.org/en/master/UDPSocket

Demonstrates sending and receiving data using Ruby's `UDPSocket`. It shows how to bind a socket, send a message to a specific address and port, and receive messages. The example highlights the typical workflow for basic UDP communication.

```ruby
u1 = UDPSocket.new
u1.bind("127.0.0.1", 4913)

u2 = UDPSocket.new
u2.send "hi", 0, "127.0.0.1", 4913

mesg, addr = u1.recvfrom(10)
u1.send mesg, 0, addr[3], addr[1]

p u2.recv(100) #=> "hi"
```

--------------------------------

### Auto Install Missing Gems

Source: https://docs.ruby-lang.org/en/master/Bundler

Automatically installs missing gems if the 'auto_install' setting is enabled. This method resets the global Definition object before and after installation to ensure it picks up the latest dependencies.

```ruby
# File lib/bundler.rb, line 181
def auto_install
  return unless Bundler.settings[:auto_install]

  begin
    definition.specs
  rescue GemNotFound, GitError
    ui.info "Automatically installing missing gems."
    reset!
    CLI::Install.new({}).run
    reset!
  end
end
```

--------------------------------

### Install Development Dependencies

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Installs additional development dependencies required for a gem. This option also sets 'dev_shallow' to true, indicating a shallow development dependency installation.

```ruby
add_option(:'Install/Update', "--development",
              "Install additional development",
              "dependencies") do |_value, options|
    options[:development] = true
    options[:dev_shallow] = true
  end
```

--------------------------------

### Ruby String Slicing with Start and Length

Source: https://docs.ruby-lang.org/en/master/String

Illustrates extracting a substring from a Ruby string using a starting index and a length. Handles positive, negative start indices, zero length, and out-of-bounds conditions.

```ruby
'foo'[0, 2]      # => "fo"
'тест'[1, 2]     # => "ес"
'こんにちは'[2, 2] # => "にち"
# Zero length.
'foo'[2, 0]      # => ""
# Length not entirely available.
'foo'[1, 200]    # => "oo"
# Start out of range.
'foo'[4, 2]      # => nil

# Special case: start equals length.
'foo'[3, 2]    # => ""
'foo'[3, 200]  # => ""

# Negative start index.
'foo'[-2, 2]     # => "oo"
'foo'[-2, 200]   # => "oo"
# Start out of range.
'foo'[-4, 2]     # => nil

# Negative length.
'foo'[1, -1]   # => nil
'foo'[-2, -1]  # => nil

```

--------------------------------

### Constructing a SET

Source: https://docs.ruby-lang.org/en/master/OpenSSL/ASN1/Constructive

Example demonstrating how to construct an ASN.1 SET using OpenSSL::ASN1::Set.

```APIDOC
## Constructing a SET

### Example
```ruby
int = OpenSSL::ASN1::Integer.new(1)
str = OpenSSL::ASN1::PrintableString.new('abc')
set = OpenSSL::ASN1::Set.new( [ int, str ] )
```
```

--------------------------------

### Start HTTP Session with Net::HTTP

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Initiates an HTTP session with a specified host. Supports optional port, proxy configuration, and SSL settings. Can be used with or without a block for managing the session lifecycle.

```ruby
def HTTP.start(address, *arg, &block)
  arg.pop if opt = Hash.try_convert(arg[-1])
  port, p_addr, p_port, p_user, p_pass = *arg
  p_addr = :ENV if arg.size < 2
  port = https_default_port if !port && opt && opt[:use_ssl]
  http = new(address, port, p_addr, p_port, p_user, p_pass)
  http.ipaddr = opt[:ipaddr] if opt && opt[:ipaddr]

  if opt
    if opt[:use_ssl]
      opt = {verify_mode: OpenSSL::SSL::VERIFY_PEER}.update(opt)
    end
    http.methods.grep(/\A(\w+)=\z/) do |meth|
      key = $1.to_sym
      opt.key?(key) or next
      http.__send__(meth, opt[key])
    end
  end

  http.start(&block)
end
```

```ruby
hostname = 'jsonplaceholder.typicode.com'
Net::HTTP.start(hostname) do |http|
  puts http.get('/todos/1').body
  puts http.get('/todos/2').body
end
```

```ruby
http = Net::HTTP.start(hostname)
http.started? # => true
http.finish
http.started? # => false
```

--------------------------------

### Get UNIX Domain Socket Path in Ruby

Source: https://docs.ruby-lang.org/en/master/Addrinfo

This Ruby method extracts and returns the filesystem path of a UNIX domain socket from an Addrinfo object. It raises an error if the Addrinfo is not a UNIX domain socket or if the path is malformed. The example shows retrieving the path for a given UNIX domain socket.

```ruby
static VALUE
addrinfo_unix_path(VALUE self)
{
    rb_addrinfo_t *rai = get_addrinfo(self);
    int family = ai_get_afamily(rai);
    struct sockaddr_un *addr;
    long n;

    if (family != AF_UNIX)
        rb_raise(rb_eSocket, "need AF_UNIX address");

    addr = &rai->addr.un;

    n = rai_unixsocket_len(rai);
    if (n < 0)
        rb_raise(rb_eSocket, "too short AF_UNIX address: %"PRIuSIZE" bytes given for minimum %"PRIuSIZE" bytes.", (size_t)rai->sockaddr_len, offsetof(struct sockaddr_un, sun_path));
    if ((long)sizeof(addr->sun_path) < n)
        rb_raise(rb_eSocket,
            "too long AF_UNIX path ( %"PRIuSIZE" bytes given but %"PRIuSIZE" bytes max)",
            (size_t)n, sizeof(addr->sun_path));
    return rb_str_new(addr->sun_path, n);
}
```

```ruby
Addrinfo.unix("/tmp/sock").unix_path       #=> "/tmp/sock"
```

--------------------------------

### Initialize Zlib::Deflate Stream (Ruby)

Source: https://docs.ruby-lang.org/en/master/Zlib/Deflate

Creates a new deflate stream for compression with customizable parameters. Supports setting compression level, window bits, memory level, and strategy.

```ruby
static VALUE
rb_deflate_initialize(int argc, VALUE *argv, VALUE obj)
{
    struct zstream *z;
    VALUE level, wbits, memlevel, strategy;
    int err;

    rb_scan_args(argc, argv, "04", &level, &wbits, &memlevel, &strategy);
    TypedData_Get_Struct(obj, struct zstream, &zstream_data_type, z);

    err = deflateInit2(&z->stream, ARG_LEVEL(level), Z_DEFLATED,
                       ARG_WBITS(wbits), ARG_MEMLEVEL(memlevel),
                       ARG_STRATEGY(strategy));
    if (err != Z_OK) {
        raise_zlib_error(err, z->stream.msg);
    }
    ZSTREAM_READY(z);

    return obj;
}
```

--------------------------------

### Example Usage of Git Block (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/RequestSet/GemDependencyAPI

An example showing how to use the 'git' block to specify multiple gem dependencies from a single Git repository.

```ruby
git 'https://github.com/rails/rails.git' do
  gem 'activesupport'
  gem 'activerecord'
end
```

--------------------------------

### Gem Plugin Directory

Source: https://docs.ruby-lang.org/en/master/Gem

Retrieves the standard installation directory for RubyGems plugins.

```APIDOC
## Gem.plugindir (install_dir = Gem.dir)

### Description
Returns the path where RubyGems plugins are to be installed.

### Method
GET

### Endpoint
`/gems/plugindir`

### Parameters
#### Query Parameters
- **install_dir** (string, optional) - The base installation directory. Defaults to `Gem.dir`.

### Response
#### Success Response (200)
- **plugindir** (string) - The path to the plugin directory.

### Response Example
```json
{
  "plugindir": "/usr/local/lib/ruby/gems/3.0.0/plugins"
}
```
```

--------------------------------

### Get Keyword String

Source: https://docs.ruby-lang.org/en/master/Prism/PreExecutionNode

Retrieves the string representation of the 'BEGIN' keyword associated with this pre-execution node.

```ruby
# File lib/prism/node.rb, line 15006
def keyword
  keyword_loc.slice
end
```

--------------------------------

### Check if Gem is Installable (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Platform

Determines if a given gem specification is installable. It checks if the specification responds to `installable_platform?` and calls it, otherwise it falls back to using `match_spec?`.

```ruby
# File lib/rubygems/platform.rb, line 67
def self.installable?(spec)
  if spec.respond_to? :installable_platform?
    spec.installable_platform?
  else
    match_spec? spec
  end
end
```

--------------------------------

### Capture3 with Stdin Data and Options

Source: https://docs.ruby-lang.org/en/master/Open3

Demonstrates using Open3.capture3 with the `stdin_data` option to provide input to the command's standard input and the `binmode` option to set streams to binary mode.

```ruby
Open3.capture3('tee', stdin_data: 'Foo')
# => ["Foo", "", #<Process::Status: pid 2319575 exit 0>]

```

--------------------------------

### Copy File (cp_r) - Example

Source: https://docs.ruby-lang.org/en/master/FileUtils

Shows a basic example of using `FileUtils.cp_r` to copy a single file to another file. It includes checks for the existence of the destination file before and after the operation.

```ruby
FileUtils.touch('src0.txt')
File.exist?('dest0.txt') # => false
FileUtils.cp_r('src0.txt', 'dest0.txt')
File.file?('dest0.txt')  # => true
```

--------------------------------

### Configure Ruby Build with Installation Prefix

Source: https://docs.ruby-lang.org/en/master/contributing/building_ruby_md

This command runs the configure script, which generates the Makefile. The --prefix option specifies the target directory for installing the compiled Ruby, in this case, ~/.rubies/ruby-master. The -C flag enables configuration caching for faster subsequent runs.

```shell
../configure --prefix="${HOME}/.rubies/ruby-master"
```

--------------------------------

### Initialize Win32::Registry::PredefinedKey

Source: https://docs.ruby-lang.org/en/master/Win32/Registry/PredefinedKey

Constructor for the Win32::Registry::PredefinedKey class. It takes a handle to a registry key (hkey) and the key name as arguments. Initializes instance variables for the registry key handle, parent key, key name, and disposition.

```Ruby
def initialize(hkey, keyname)
  @hkey = Fiddle::Pointer.new(hkey)
  @parent = nil
  @keyname = keyname
  @disposition = REG_OPENED_EXISTING_KEY
end
```

--------------------------------

### Fill Array with Block and Negative Start Index (Ruby)

Source: https://docs.ruby-lang.org/en/master/Array

Demonstrates filling an array using a block with negative start indices, counting backwards from the end. Includes cases where the array is extended and when the start index is out of range.

```ruby
['a', 'b', 'c', 'd'].fill(-4, 3) {|e| e.to_s }
# => ["0", "1", "2", "d"]
['a', 'b', 'c', 'd'].fill(-3, 3) {|e| e.to_s }
# => ["a", "1", "2", "3"]
['a', 'b', 'c', 'd'].fill(-2, 3) {|e| e.to_s }
# => ["a", "b", "2", "3", "4"]
['a', 'b', 'c', 'd'].fill(-1, 3) {|e| e.to_s }
# => ["a", "b", "c", "3", "4", "5"]
['a', 'b', 'c', 'd'].fill(-5, 2) {|e| e.to_s }
# => ["0", "1", "c", "d"]
['a', 'b', 'c', 'd'].fill(-6, 2) {|e| e.to_s }
# => ["0", "1", "c", "d"]
```

--------------------------------

### Handle Start of Stream Event

Source: https://docs.ruby-lang.org/en/master/Psych/TreeBuilder

The `start_stream` method initializes the root `Psych::Nodes::Stream` node with the specified encoding, sets its start location, and pushes it onto the stack.

```ruby
# File ext/psych/lib/psych/tree_builder.rb, line 84
def start_stream encoding
  @root = Nodes::Stream.new(encoding)
  set_start_location(@root)
  push @root
end
```

--------------------------------

### Bundler.require

Source: https://docs.ruby-lang.org/en/master/Bundler

Sets up the Bundler environment and loads specified gem groups. It can be called multiple times with different groups.

```APIDOC
## Bundler.require

### Description
Sets up the Bundler environment if not already set, and loads all gems from the specified groups. This method can be invoked multiple times with different groups.

### Method
`Bundler.require(*groups)`

### Parameters
* **groups** - A list of gem groups to load. If empty, all groups are loaded.

### Request Example
```ruby
# Load default group gems
Bundler.require(:default)

# Load test group gems
Bundler.require(:test)
```

### Response
This method does not return a value; it performs setup and loads gems.

### Example Usage
```ruby
# Assuming Gemfile:
# gem 'first_gem', '= 1.0'
# group :test do
#   gem 'second_gem', '= 1.0'
# end

Bundler.setup # Sets up all groups
Bundler.require(:default) # Requires first_gem
Bundler.require(:test)   # Requires second_gem
```
```

--------------------------------

### Example Usage of PriorityQueue

Source: https://docs.ruby-lang.org/en/master/SyntaxSuggest/PriorityQueue

Demonstrates how to create a PriorityQueue, add elements to it, and retrieve the highest priority element using the peek method. Shows the basic functionality of the class.

```ruby
queue = PriorityQueue.new
queue << 33
queue << 44
queue << 1

puts queue.peek # => 44
```

--------------------------------

### Open3.popen3 implementation details

Source: https://docs.ruby-lang.org/en/master/Open3

Internal implementation of Open3.popen3, showing how pipes and process spawning are managed.

```ruby
def popen3(*cmd, &block)
  if Hash === cmd.last
    opts = cmd.pop.dup
  else
    opts = {}
  end

  in_r, in_w = IO.pipe
  opts[:in] = in_r
  in_w.sync = true

  out_r, out_w = IO.pipe
  opts[:out] = out_w

  err_r, err_w = IO.pipe
  opts[:err] = err_w

  popen_run(cmd, opts, [in_r, out_w, err_w], [in_w, out_r, err_r], &block)
end
```

--------------------------------

### Write Gem Build Information File in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Writes a file containing the arguments used for building a gem's extensions. This information is stored in a 'build_info' subdirectory within the gem's home directory.

```Ruby
def write_build_info_file
  return if build_args.empty?

  build_info_dir = File.join gem_home, "build_info"

  dir_mode = options[:dir_mode]
  FileUtils.mkdir_p build_info_dir, mode: dir_mode && 0o755

  build_info_file = File.join build_info_dir, "#{spec.full_name}.info"

  File.open build_info_file, "w" do |io|
    build_args.each do |arg|
      io.puts arg
    end
  end

  File.chmod(dir_mode, build_info_dir) if dir_mode
end
```

--------------------------------

### Ruby Array Slice - Start and Length

Source: https://docs.ruby-lang.org/en/master/Array

Returns a new array containing elements starting from `start` for a given `length`. Handles cases where `start + length` exceeds array bounds.

```ruby
slice(start, length) -> object or nil

a = [:foo, 'bar', 2]
a[0, 2] # => [:foo, "bar"]
a[1, 2] # => ["bar", 2]
a[0, 4] # => [:foo, "bar", 2]
a[1, 3] # => ["bar", 2]
```

--------------------------------

### Open3.pipeline_start: Start a pipeline of processes

Source: https://docs.ruby-lang.org/en/master/Open3

Starts a pipeline of processes without waiting for them to exit. It spawns child processes for each command in the sequence. If a block is provided, it's called with an array of wait threads. Without a block, it returns the array of wait threads.

```ruby
# File lib/open3.rb, line 1272
def pipeline_start(*cmds, &block)
  if Hash === cmds.last
    opts = cmds.pop.dup
  else
    opts = {}
  end

  if block
    pipeline_run(cmds, opts, [], [], &block)
  else
    ts, = pipeline_run(cmds, opts, [], [])
    ts
  end
end

```

```ruby
wait_threads = Open3.pipeline_start('ls', 'grep R')
# => [#<Process::Waiter:0x000055e8de9d2bb0 run>, #<Process::Waiter:0x000055e8de9d2890 run>]
wait_threads.each do |wait_thread|
  wait_thread.join
end

```

```ruby
Open3.pipeline_start('ls', 'grep R') do |wait_threads|
  wait_threads.each do |wait_thread|
    wait_thread.join
  end
end

```

--------------------------------

### Initialize Gem::Commands::UninstallCommand with Options

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/UninstallCommand

Initializes the UninstallCommand with various command-line options. These options control aspects like uninstalling all versions, ignoring dependencies, checking development dependencies, managing executables, specifying installation directories, and forcing uninstallation.

```ruby
# File lib/rubygems/commands/uninstall_command.rb, line 16
def initialize
  super "uninstall", "Uninstall gems from the local repository",
        version: Gem::Requirement.default, user_install: true,
        check_dev: false, vendor: false

  add_option("-a", "--[no-]all",
    "Uninstall all matching versions") do |value, options|
    options[:all] = value
  end

  add_option("-I", "--[no-]ignore-dependencies",
             "Ignore dependency requirements while",
             "uninstalling") do |value, options|
    options[:ignore] = value
  end

  add_option("-D", "--[no-]check-development",
             "Check development dependencies while uninstalling",
             "(default: false)") do |value, options|
    options[:check_dev] = value
  end

  add_option("-x", "--[no-]executables",
               "Uninstall applicable executables without",
               "confirmation") do |value, options|
    options[:executables] = value
  end

  add_option("-i", "--install-dir DIR",
             "Directory to uninstall gem from") do |value, options|
    options[:install_dir] = File.expand_path(value)
  end

  add_option("-n", "--bindir DIR",
             "Directory to remove executables from") do |value, options|
    options[:bin_dir] = File.expand_path(value)
  end

  add_option("--[no-]user-install",
             "Uninstall from user's home directory",
             "in addition to GEM_HOME.") do |value, options|
    options[:user_install] = value
  end

  add_option("--[no-]format-executable",
             "Assume executable names match Ruby's prefix and suffix.") do |value, options|
    options[:format_executable] = value
  end

  add_option("--[no-]force",
             "Uninstall all versions of the named gems",
             "ignoring dependencies") do |value, options|
    options[:force] = value
  end

  add_option("--[no-]abort-on-dependent",
             "Prevent uninstalling gems that are",
             "depended on by other gems.") do |value, options|
    options[:abort_on_dependent] = value
  end

  add_version_option
  add_platform_option

  add_option("--vendor",
             "Uninstall gem from the vendor directory.",
             "Only for use by gem repackagers.") do |_value, options|
    unless Gem.vendor_dir
      raise Gem::OptionParser::InvalidOption.new "your platform is not supported"
    end

    alert_warning "Use your OS package manager to uninstall vendor gems"
    options[:vendor] = true
    options[:install_dir] = Gem.vendor_dir
  end
end
```

--------------------------------

### Ruby Socket getaddrinfo Usage Examples

Source: https://docs.ruby-lang.org/en/master/Socket

Examples demonstrating the usage of Socket.getaddrinfo to resolve network addresses. It shows how to specify hostnames, service names, address families, and socket types to obtain corresponding network information.

```Ruby
# Socket.getaddrinfo("www.ruby-lang.org", "http", nil, :STREAM)
#=> [["AF_INET", 80, "carbon.ruby-lang.org", "221.186.184.68", 2, 1, 6]] # PF_INET/SOCK_STREAM/IPPROTO_TCP

# Socket.getaddrinfo("localhost", nil)
#=> [["AF_INET", 0, "localhost", "127.0.0.1", 2, 1, 6],  # PF_INET/SOCK_STREAM/IPPROTO_TCP
#    ["AF_INET", 0, "localhost", "127.0.0.1", 2, 2, 17] # PF_INET/SOCK_DGRAM/IPPROTO_UDP
#]
```

--------------------------------

### Fill Array with Negative Start Index (Ruby)

Source: https://docs.ruby-lang.org/en/master/Array

Explains how to use negative start indices to count backwards from the end of the array for filling. Shows array extension and handling out-of-range negative start indices.

```ruby
['a', 'b', 'c', 'd'].fill('-', -4, 3) # => ["-", "-", "-", "d"]
['a', 'b', 'c', 'd'].fill('-', -3, 3) # => ["a", "-", "-", "-"]
['a', 'b', 'c', 'd'].fill('-', -2, 3) # => ["a", "b", "-", "-", "-"]
['a', 'b', 'c', 'd'].fill('-', -1, 3) # => ["a", "b", "c", "-", "-", "-"]
['a', 'b', 'c', 'd'].fill('-', -5, 2) # => ["-", "-", "c", "d"]
['a', 'b', 'c', 'd'].fill('-', -6, 2) # => ["-", "-", "c", "d"]
```

--------------------------------

### Ruby Time Addition (Examples)

Source: https://docs.ruby-lang.org/en/master/Time

Examples demonstrating the usage of Ruby's Time#+ method to add seconds or fractional seconds to a Time object, resulting in a new Time object.

```ruby
t = Time.new(2000) # => 2000-01-01 00:00:00 -0600
t + (60 * 60 * 24) # => 2000-01-02 00:00:00 -0600
t + 0.5            # => 2000-01-01 00:00:00.5 -0600
```

--------------------------------

### Check if Specification is Installable

Source: https://docs.ruby-lang.org/en/master/Gem/Resolver/Specification

Determines if the current gem specification is installable on the current platform by matching the specification's platform with the system's platform.

```ruby
# File lib/rubygems/resolver/specification.rb, line 119
def installable_platform?
  Gem::Platform.match_spec? spec
end
```

--------------------------------

### Ruby PP Class Overview

Source: https://docs.ruby-lang.org/en/master/PP

Demonstrates the difference between standard 'p' output and pretty-printed output using the PP class. The pretty-printed output is more structured and readable for complex objects.

```Ruby
#<PP:0x81fedf0 @genspace=#<Proc:0x81feda0>, @group_queue=#<PrettyPrint::GroupQueue:0x81fed3c @queue=[[#<PrettyPrint::Group:0x81fed78 @breakables=[], @depth=0, @break=false>], []]>, @buffer=[], @newline="\n", @group_stack=[#<PrettyPrint::Group:0x81fed78 @breakables=[], @depth=0, @break=false>], @buffer_width=0, @indent=0, @maxwidth=79, @output_width=2, @output=#<IO:0x8114ee4>>
```

```Ruby
#<PP:0x81fedf0
 @buffer=[],
 @buffer_width=0,
 @genspace=#<Proc:0x81feda0>,
 @group_queue=
  #<PrettyPrint::GroupQueue:0x81fed3c
   @queue=
    [[#<PrettyPrint::Group:0x81fed78 @break=false, @breakables=[], @depth=0>],
     []]>,
 @group_stack=
  [#<PrettyPrint::Group:0x81fed78 @break=false, @breakables=[], @depth=0>],
 @indent=0,
 @maxwidth=79,
 @newline="\n",
 @output=#<IO:0x8114ee4>,
 @output_width=2>
```

--------------------------------

### Example of Missing Character Detection

Source: https://docs.ruby-lang.org/en/master/SyntaxSuggest/ExplainSyntax

Provides an example of how the 'missing' method can be used to detect a missing closing brace '}' in the source code.

```ruby
ExplainSyntax.new(code_lines: lines).missing
# => ["}"]
```

--------------------------------

### Ruby Array Slicing with Start and Length

Source: https://docs.ruby-lang.org/en/master/Array

Returns a new array containing a specified number of elements starting from a given offset. If start + length exceeds array bounds, it returns elements from start to the end. Negative length returns nil.

```ruby
a = [:foo, 'bar', 2]
a[0, 2] # => [:foo, "bar"]
a[1, 2] # => ["bar", 2]
a[0, 4] # => [:foo, "bar", 2]
a[1, 3] # => ["bar", 2]
a[2, 2] # => [2]
a[0, -1] # => nil
```

--------------------------------

### SyntaxSuggest::Cli Parser Configuration (Ruby)

Source: https://docs.ruby-lang.org/en/master/SyntaxSuggest/Cli

Defines the command-line options for the SyntaxSuggest tool using OptionParser, including help, record directory, and terminal highlighting.

```ruby
# File lib/syntax_suggest/cli.rb, line 81
    def parser
      @parser ||= OptionParser.new do |opts|
        opts.banner = <<~EOM
          Usage: syntax_suggest <file> [options]

          Parses a ruby source file and searches for syntax error(s) such as
          unexpected `end', expecting end-of-input.

          Example:

            $ syntax_suggest dog.rb

            # ...

              > 10  defdog
              > 15  end

          ENV options:

            SYNTAX_SUGGEST_RECORD_DIR=<dir>

            Records the steps used to search for a syntax error
            to the given directory

          Options:
        EOM

        opts.version = SyntaxSuggest::VERSION

        opts.on("--help", "Help - displays this message") do |v|
          @io.puts opts
          options[:exit] = true
          @exit_obj.exit
        end

        opts.on("--record <dir>", "Records the steps used to search for a syntax error to the given directory") do |v|
          options[:record_dir] = v
        end

        opts.on("--terminal", "Enable terminal highlighting") do |v|
          options[:terminal] = true
        end

        opts.on("--no-terminal", "Disable terminal highlighting") do |v|
          options[:terminal] = false
        end
      end
    end
```

--------------------------------

### Fetch Start Offset

Source: https://docs.ruby-lang.org/en/master/Prism/Relocation/Entry

Retrieves the start byte offset of a value from the Prism::Relocation::Entry. This method relies on the fetch_value private method.

```ruby
# File lib/prism/relocation.rb, line 46
def start_offset
  fetch_value(:start_offset)
end
```

--------------------------------

### Clone and Prepare Ruby Git Repository for Building

Source: https://docs.ruby-lang.org/en/master/contributing/building_ruby_md

This sequence of commands shows how to clone the CRuby source code repository from GitHub using git, navigate into the cloned directory, and then run the autogen.sh script to generate the configure script necessary for the build process.

```shell
git clone https://github.com/ruby/ruby.git
cd ruby
./autogen.sh
```

--------------------------------

### Initialize Resolv::DNS

Source: https://docs.ruby-lang.org/en/master/Resolv/DNS

Creates a new DNS resolver instance. It can be configured with a file path or a hash containing nameserver details and search domains. The resolver manages thread safety with a mutex.

```ruby
# File lib/resolv.rb, line 339
def initialize(config_info=nil)
  @mutex = Thread::Mutex.new
  @config = Config.new(config_info)
  @initialized = nil
end
```

--------------------------------

### Interpreter Initialization and Execution

Source: https://docs.ruby-lang.org/en/master/extension_rdoc

Functions for initializing the Ruby interpreter, processing command-line arguments, and running compiled Ruby code.

```APIDOC
## void ruby_init()

### Description
Initializes the interpreter.

### Method
void

### Endpoint
N/A (C function)

### Parameters
None

### Request Example
None

### Response
None
```

```APIDOC
## void *ruby_options(int argc, char **argv)

### Description
Process command line arguments for the interpreter. And compiles the Ruby source to execute. It returns an opaque pointer to the compiled source or an internal special value.

### Method
void *

### Endpoint
N/A (C function)

### Parameters
- **argc** (int) - The number of command line arguments.
- **argv** (char **) - An array of command line argument strings.

### Request Example
None

### Response
- **Return Value** (void *) - An opaque pointer to the compiled source or an internal special value.
```

```APIDOC
## int ruby_run_node(void *n)

### Description
Runs the given compiled source and exits this process. It returns EXIT_SUCCESS if successfully runs the source. Otherwise, it returns other value.

### Method
int

### Endpoint
N/A (C function)

### Parameters
- **n** (void *) - An opaque pointer to the compiled source.

### Request Example
None

### Response
- **Return Value** (int) - EXIT_SUCCESS on success, other value on failure.
```

```APIDOC
## void ruby_script(char *name)

### Description
Specifies the name of the script ($0).

### Method
void

### Endpoint
N/A (C function)

### Parameters
- **name** (char *) - The name of the script.

### Request Example
None

### Response
None
```

--------------------------------

### Check if Gem is Installed

Source: https://docs.ruby-lang.org/en/master/Gem/QueryUtils

Checks if a gem with the given name and requirement is installed. It iterates through all installed specifications and returns true if a matching gem is found, false otherwise.

```Ruby
def installed?(name, req = Gem::Requirement.default)
  Gem::Specification.any? {|s| s.name =~ name && req =~ s.version }
end
```

--------------------------------

### Fetch Start Column

Source: https://docs.ruby-lang.org/en/master/Prism/Relocation/Entry

Retrieves the start byte column of a value from the Prism::Relocation::Entry. This method relies on the fetch_value private method.

```ruby
# File lib/prism/relocation.rb, line 78
def start_column
  fetch_value(:start_column)
end
```

--------------------------------

### OpenStruct JSON Example (Ruby)

Source: https://docs.ruby-lang.org/en/master/OpenStruct

This example demonstrates the usage of `as_json` to serialize an OpenStruct object into a JSON hash and `json_create` to deserialize it back. It requires the 'json/add/ostruct' library to be loaded.

```Ruby
require 'json/add/ostruct'
x = OpenStruct.new('name' => 'Rowdy', :age => nil).as_json
# => {"json_class"=>"OpenStruct", "t"=>{:name=>'Rowdy', :age=>nil}}

OpenStruct.json_create(x)
# => #<OpenStruct name='Rowdy', age=nil>
```

--------------------------------

### Ruby Time Instance Methods

Source: https://docs.ruby-lang.org/en/master/Time

Examples and descriptions of common instance methods available for Ruby Time objects.

```APIDOC
## Working with an Instance of `Time`

Once you have an instance of `Time`, there are many operations you can perform. The following examples demonstrate some of these operations.

### Initialization Example
```ruby
t = Time.new(1993, 2, 24, 12, 0, 0, "+09:00")
```

### Querying Day of Week
```ruby
t.monday? #=> false
```

### Fetching Year
```ruby
t.year #=> 1993
```

### Checking Daylight Saving Time
```ruby
t.dst? #=> false
```

### Time Arithmetic (Adding Days)
```ruby
# Add 365 days to the current time
t + (60 * 60 * 24 * 365) #=> 1994-02-24 12:00:00 +0900
```

### Converting to Unix Timestamp
```ruby
t.to_i #=> 730522800
```

### Comparing Time Objects
```ruby
t1 = Time.new(2010)
t2 = Time.new(2011)

t1 == t2 #=> false
t1 == t1 #=> true
t1 < t2 #=> true
t1 > t2 #=> false

Time.new(2010, 10, 31).between?(t1, t2) #=> true
```

### Time Class Overview

**Inheritance:**
*   Inherits from class `Object`.
*   Includes module `Comparable`.

**Key Functionalities:**
*   Creating Time objects.
*   Fetching Time values.
*   Querying a Time object's properties.
*   Comparing Time objects.
*   Converting Time objects.
*   Rounding Time values.

```

--------------------------------

### Open3.popen2e - Basic Usage

Source: https://docs.ruby-lang.org/en/master/Open3

Demonstrates the basic usage of Open3.popen2e to execute a command and capture its output.

```APIDOC
## Open3.popen2e - Basic Usage

### Description
Executes a command with its standard output and standard error merged, providing access to stdin, stdout_and_stderr, and a wait_thread.

### Method
`Open3.popen2e`

### Parameters

#### Command Line/Executable Path
- `command_line` (String) - A command string to be passed to a shell. Must begin with a shell reserved word, a special built-in, or contain meta characters.
- `exe_path` (String or Array) - The path to an executable or a 2-element array with the path and the process name.

#### Optional Arguments
- `env` (Hash) - Environment variables for the child process.
- `options` (Hash) - Execution options for `Process.spawn`.

### Request Example

**Using command line:**
```ruby
Open3.popen2e('echo "Foo"') { |stdin, stdout_and_stderr, wait_thread| stdout_and_stderr.gets }
# => "Foo\n"
```

**Using executable path:**
```ruby
Open3.popen2e('/usr/bin/date') { |stdin, stdout_and_stderr, wait_thread| stdout_and_stderr.gets }
# => "Thu Sep 28 09:41:06 AM CDT 2023\n"
```

**With arguments:**
```ruby
Open3.popen2e('echo', 'hello', 'world') { |stdin, stdout_and_stderr, wait_thread| stdout_and_stderr.gets }
# => "hello world\n"
```

### Response

#### Success Response
- `stdin` (IO) - The standard input stream of the child process.
- `stdout_and_stderr` (IO) - The merged standard output and standard error stream of the child process.
- `wait_thread` (Process::Waiter) - A thread that waits for the child process to exit.

#### Response Example (with block)
```ruby
Open3.popen2e('echo') do |stdin, stdout_and_stderr, wait_thread|
  p stdin
  p stdout_and_stderr
  p wait_thread
  p wait_thread.pid
  p wait_thread.value
end

# Output:
#<IO:fd 6>
#<IO:fd 7>
#<Process::Waiter:0x00007f75777578c8 sleep>
2274763
#<Process::Status: pid 2274763 exit 0>
```

#### Response Example (without block)
```ruby
stdin, stdout_and_stderr, wait_thread = Open3.popen2e('echo')
# => [#<IO:fd 6>, #<IO:fd 7>, #<Process::Waiter:0x00007f7577da4398 run>]
stdin.close
stdout_and_stderr.close
wait_thread.pid   # => 2274600
wait_thread.value # => #<Process::Status: pid 2274600 exit 0>
```

### Error Handling
- `Errno::ENOENT` - Raised if the executable path does not exist.

### Security Considerations
- Potential security vulnerabilities if called with untrusted input (Command Injection). Ensure input is sanitized.
```

--------------------------------

### Array Pattern Examples in Ruby

Source: https://docs.ruby-lang.org/en/master/Prism/ArrayPatternNode

Demonstrates various syntaxes for array patterns used in Ruby's pattern matching, showcasing different ways to destructure arrays.

```ruby
foo in 1, 2
^^^^^^^^^^^
```

```ruby
foo in [1, 2]
^^^^^^^^^^^^^
```

```ruby
foo in *bar
^^^^^^^^^^^
```

```ruby
foo in Bar[]
^^^^^^^^^^^^
```

```ruby
foo in Bar[1, 2, 3]
^^^^^^^^^^^^^^^^^^^
```

--------------------------------

### Ruby Array Slicing - Negative Range Start Behaviour

Source: https://docs.ruby-lang.org/en/master/Array

When the start of a range is negative, it is interpreted as an offset from the end of the array to determine the actual start index for slicing.

```ruby
a = [:foo, 'bar', 2]
a[-1..2] # => [2]
a[-2..2] # => ["bar", 2]
a[-3..2] # => [:foo, "bar", 2]
```

--------------------------------

### Initialize Gem::Commands::InfoCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/InfoCommand

Initializes the `InfoCommand` for RubyGems, setting up options for querying gem information. It calls the superclass constructor and configures default behaviors.

```ruby
# File lib/rubygems/commands/info_command.rb, line 9
def initialize
  super "info", "Show information for the given gem",
       name: //, domain: :local, details: false, versions: true,
       installed: nil, version: Gem::Requirement.default

  add_query_options

  remove_option("-d")

  defaults[:details] = true
  defaults[:exact] = true
end
```

--------------------------------

### Documenting a Ruby Method with File Inclusion (RDoc)

Source: https://docs.ruby-lang.org/en/master/contributing/documentation_guide_md

Demonstrates documenting a method using RDoc's file inclusion (`:include:`). This preserves the 'click to toggle source' feature and is recommended for methods defined in C.

```rdoc
/*
 *  call-seq:
 *    each_byte {|byte| ... } -> self
 *    each_byte               -> enumerator
 *
 *  :include: doc/string/each_byte.rdoc
 *
 */
```

--------------------------------

### Configure and Build Ruby with YJIT (Debug Mode)

Source: https://docs.ruby-lang.org/en/master/yjit/yjit_md

Steps to configure and build Ruby with YJIT enabled for development/debugging. It specifies a custom installation prefix and includes essential libraries like OpenSSL, Readline, and LibYAML. It also covers making and installing the built Ruby.

```shell
./autogen.sh
./configure --enable-yjit=dev --prefix=$HOME/.rubies/ruby-yjit --disable-install-doc --with-opt-dir="$(brew --prefix openssl):$(brew --prefix readline):$(brew --prefix libyaml)"
make -j && make install
```

--------------------------------

### Build Extensions in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Builds gem extensions using an external builder. It takes the specification, build arguments, and Ruby's configuration as input.

```ruby
def build_extensions
  builder = Gem::Ext::Builder.new spec, build_args, Gem.target_rbconfig

  builder.build_extensions
end
```

--------------------------------

### Ruby Marshal: Symbol Link Example

Source: https://docs.ruby-lang.org/en/master/marshal_rdoc

Illustrates the Marshal format for symbol linking, where a symbol is referenced by its index. This example shows how repeated symbols are efficiently stored.

```ruby
"\x04\b[\a:\nhello;\x00"
```

--------------------------------

### Fiber Context Switching Example in Ruby

Source: https://docs.ruby-lang.org/en/master/fiber_md

Demonstrates the cooperative concurrency model of Fibers. It shows how to create a Fiber, yield control using `Fiber.yield`, and resume execution using `f.resume` to switch between the main program flow and the Fiber.

```Ruby
#!/usr/bin/env ruby

puts "1: Start program."

f = Fiber.new do
  puts "3: Entered fiber."
  Fiber.yield
  puts "5: Resumed fiber."
end

puts "2: Resume fiber first time."
f.resume

puts "4: Resume fiber second time."
f.resume

puts "6: Finished."


```

--------------------------------

### Configure Build Root for Temporary Installations

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Sets a temporary root directory for installations, primarily useful for building packages. This option should not be used when installing remote gems.

```ruby
add_option(:'Install/Update', "--build-root DIR",
             "Temporary installation root. Useful for building",
             "packages. Do not use this when installing remote gems.") do |value, options|
    options[:build_root] = File.expand_path(value)
  end
```

--------------------------------

### Initialize Gem HelpCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/HelpCommand

Initializes the HelpCommand for the Ruby Gem system. It sets the command name to 'help' and provides a description for its functionality. It also retrieves an instance of the Gem::CommandManager.

```ruby
def initialize
  super "help", "Provide help on the 'gem' command"

  @command_manager = Gem::CommandManager.instance
end
```

--------------------------------

### Ruby: Sample Program

Source: https://docs.ruby-lang.org/en/master/ruby/option_dump_md

A simple Ruby program that prints 'Foo' to standard output. Used in examples for demonstrating the --dump option.

```shell
$ cat t.rb
```

```ruby
puts 'Foo'
```

--------------------------------

### Ruby Resolv: Basic DNS Lookups

Source: https://docs.ruby-lang.org/en/master/Resolv

Demonstrates basic DNS lookups using Resolv.getaddress and Resolv.getname to resolve hostnames to IP addresses and vice versa.

```ruby
p Resolv.getaddress "www.ruby-lang.org"
p Resolv.getname "210.251.121.214"
```

--------------------------------

### Check if Gem is Installed with Gem::Resolver::ActivationRequest

Source: https://docs.ruby-lang.org/en/master/Gem/Resolver/ActivationRequest

Checks if the gem associated with this activation request is already installed. It handles vendor specifications and compares against existing installed specifications.

```ruby
def installed?
  case @spec
  when Gem::Resolver::VendorSpecification then
    true
  else
    this_spec = full_spec

    Gem::Specification.any? do |s|
      s == this_spec && s.base_dir == this_spec.base_dir
    end
  end
end
```

--------------------------------

### Ruby Proc Lambda Behavior Examples

Source: https://docs.ruby-lang.org/en/master/Proc

Illustrates the differences in argument handling between `proc` and `lambda`.

```ruby
proc {|a,b| [a,b] }.call(1,2,3)    #=> [1,2]
proc {|a,b| [a,b] }.call(1)        #=> [1,nil]
proc {|a,b| [a,b] }.call([1,2])    #=> [1,2]

lambda {|a,b| [a,b] }.call(1,2,3)  #=> ArgumentError
lambda {|a,b| [a,b] }.call(1)      #=> ArgumentError
lambda {|a,b| [a,b] }.call([1,2])  #=> ArgumentError
```

--------------------------------

### Ring example in Actor-model using Ractors

Source: https://docs.ruby-lang.org/en/master/ractor_md

Implements a traditional ring example in the Actor-model using Ruby's Ractors, demonstrating inter-Ractor communication.

```ruby
RN = 1_000
CR = Ractor.current

r = Ractor.new do
  p Ractor.receive
  CR << :fin
end

RN.times{
  r = Ractor.new r do |next_r|
    next_r << Ractor.receive
  end
}

p :setup_ok
r << 1
p Ractor.receive

```

--------------------------------

### Ruby Pattern Matching Examples

Source: https://docs.ruby-lang.org/en/master/NEWS/NEWS-2_7_0

Demonstrates the experimental pattern matching feature in Ruby 2.7.0 using case statements with arrays, hashes, and JSON parsing. Includes examples of successful matches, mismatches, and error handling.

```Ruby
case [0, [1, 2, 3]]
in [a, [b, *c]]
  p a #=> 0
  p b #=> 1
  p c #=> [2, 3]
end

case {a: 0, b: 1}
in {a: 0, x: 1}
  :unreachable
in {a: 0, b: var}
  p var #=> 1
end

case -1
in 0 then :unreachable
in 1 then :unreachable
end #=> NoMatchingPatternError

json = <<END
{
  "name": "Alice",
  "age": 30,
  "children": [{ "name": "Bob", "age": 2 }]
}
END

JSON.parse(json, symbolize_names: true) in {name: "Alice", children: [{name: name, age: age}]}

p name #=> "Bob"
p age  #=> 2

JSON.parse(json, symbolize_names: true) in {name: "Alice", children: [{name: "Charlie", age: age}]}
#=> NoMatchingPatternError
```

--------------------------------

### Ruby: Execute pristine command logic

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/PristineCommand

The `execute` method in `pristine_command.rb` handles the core logic for restoring gems. It selects gems based on options like `--all`, `--extensions`, or `--only-missing-extensions`, filters them by platform, and then iterates through the selected gems. For each gem, it checks for cached files, fetches them if necessary, and installs them using `Gem::Installer` with appropriate options (like `wrappers`, `force`, `install_dir`, `env_shebang`, `build_args`, `bin_dir`). It also handles skipping gems specified in options or those requiring extension compilation.

```ruby
def execute
  install_dir = options[:install_dir]

  specification_record = install_dir ? Gem::SpecificationRecord.from_path(install_dir) : Gem::Specification.specification_record

  specs = if options[:all]
    specification_record.map

  # `--extensions` must be explicitly given to pristine only gems
  # with extensions.
  elsif options[:extensions_set] &&
        options[:extensions] && options[:args].empty?
    specification_record.select do |spec|
      spec.extensions && !spec.extensions.empty?
    end
  elsif options[:only_missing_extensions]
    specification_record.select(&:missing_extensions?)
  else
    get_all_gem_names.sort.flat_map do |gem_name|
      specification_record.find_all_by_name(gem_name, options[:version]).reverse
    end
  end

  specs = specs.select {|spec| spec.platform == RUBY_ENGINE || Gem::Platform.local === spec.platform || spec.platform == Gem::Platform::RUBY }

  if specs.to_a.empty?
    raise Gem::Exception,
          "Failed to find gems #{options[:args]} #{options[:version]}"
  end

  say "Restoring gems to pristine condition..."

  specs.group_by(&:full_name_with_location).values.each do |grouped_specs|
    spec = grouped_specs.find {|s| !s.default_gem? } || grouped_specs.first

    only_executables = options[:only_executables]
    only_plugins = options[:only_plugins]

    unless only_executables || only_plugins
      # Default gemspecs include changes provided by ruby-core installer that
      # can't currently be pristined (inclusion of compiled extension targets in
      # the file list). So stick to resetting executables if it's a default gem.
      only_executables = true if spec.default_gem?
    end

    if options.key? :skip
      if options[:skip].include? spec.name
        say "Skipped #{spec.full_name}, it was given through options"
        next
      end
    end

    unless spec.extensions.empty? || options[:extensions] || only_executables || only_plugins
      say "Skipped #{spec.full_name_with_location}, it needs to compile an extension"
      next
    end

    gem = spec.cache_file

    unless File.exist?(gem) || only_executables || only_plugins
      require_relative "../remote_fetcher"

      say "Cached gem for #{spec.full_name_with_location} not found, attempting to fetch..."

      dep = Gem::Dependency.new spec.name, spec.version
      found, _ = Gem::SpecFetcher.fetcher.spec_for_dependency dep

      if found.empty?
        say "Skipped #{spec.full_name}, it was not found from cache and remote sources"
        next
      end

      spec_candidate, source = found.first
      Gem::RemoteFetcher.fetcher.download spec_candidate, source.uri.to_s, spec.base_dir
    end

    env_shebang =
      if options.include? :env_shebang
        options[:env_shebang]
      else
        install_defaults = Gem::ConfigFile::PLATFORM_DEFAULTS["install"]
        install_defaults.to_s["--env-shebang"]
      end

    bin_dir = options[:bin_dir] if options[:bin_dir]

    installer_options = {
      wrappers: true,
      force: true,
      install_dir: install_dir || spec.base_dir,
      env_shebang: env_shebang,
      build_args: spec.build_args,
      bin_dir: bin_dir,
    }

    if only_executables
      installer = Gem::Installer.for_spec(spec, installer_options)
      installer.generate_bin
    elsif only_plugins
      installer = Gem::Installer.for_spec(spec, installer_options)
      installer.generate_plugins
    else
      installer = Gem::Installer.at(gem, installer_options)
      installer.install
    end

    say "Restored #{spec.full_name_with_location}"
  end
end
```

--------------------------------

### Generate Default Man Directory

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Generates the default man directory path. It checks the prefix option and uses RbConfig for the default 'mandir' if no prefix is set. Returns nil if the man directory cannot be determined.

```ruby
def generate_default_man_dir
  prefix = options[:prefix]

  if prefix.empty?
    man_dir = RbConfig::CONFIG["mandir"]
    return unless man_dir
  else
    man_dir = File.join prefix, "man"
  end

  prepend_destdir_if_present(man_dir)
end
```

--------------------------------

### FileUtils.install

Source: https://docs.ruby-lang.org/en/master/FileUtils

Copies files from a source to a destination, with options for permissions, ownership, and verbosity. Supports single or multiple sources and can handle directory destinations.

```APIDOC
## POST /fileutils/install

### Description
Copies a file entry. See install(1). Arguments `src` (a single path or an array of paths) and `dest` (a single path) should be interpretable as paths.

### Method
POST

### Endpoint
/fileutils/install

### Parameters
#### Path Parameters
- None

#### Query Parameters
- None

#### Request Body
- **src** (string | array) - Required - The source file path or an array of source file paths.
- **dest** (string) - Required - The destination path.
- **mode** (string) - Optional - Changes the permissions using `File.chmod`.
- **owner** (string) - Optional - Changes the owner using `File.chown`.
- **group** (string) - Optional - Changes the group using `File.chown`.
- **preserve** (boolean) - Optional - Preserves timestamps using `File.utime`.
- **noop** (boolean) - Optional - If true, does not copy entries and returns `nil`.
- **verbose** (boolean) - Optional - If true, prints the equivalent command.

### Request Example
```json
{
  "src": "src0.txt",
  "dest": "dest0.txt",
  "verbose": true
}
```

### Response
#### Success Response (200)
- **message** (string) - A message indicating the success of the operation or the command executed if verbose is true.

#### Response Example
```json
{
  "message": "install -c src0.txt dest0.txt"
}
```

#### Error Response (400)
- **error** (string) - Description of the error.

#### Response Example
```json
{
  "error": "Invalid source or destination path."
}
```
```

--------------------------------

### Instance Variable Assignment Example

Source: https://docs.ruby-lang.org/en/master/Prism/InstanceVariableTargetNode

Demonstrates the syntax for assigning values to multiple instance variables simultaneously.

```ruby
@foo, @bar = baz
```

--------------------------------

### Get Binary File Names in RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Returns an array of binary file names. It uses memoization to ensure the list is generated only once during the command's execution.

```ruby
def bin_file_names
  @bin_file_names ||= []
end
```

--------------------------------

### Generating Help with OptionParser

Source: https://docs.ruby-lang.org/en/master/OptionParser

Illustrates how OptionParser can automatically generate help messages for command-line scripts. This example defines options for a name and a help flag, and the help output is displayed when --help is invoked.

```ruby
require 'optparse'

Options = Struct.new(:name)

class Parser
  def self.parse(options)
    args = Options.new("world")

    opt_parser = OptionParser.new do |parser|
      parser.banner = "Usage: example.rb [options]"

      parser.on("-nNAME", "--name=NAME", "Name to say hello to") do |n|
        args.name = n
      end

      parser.on("-h", "--help", "Prints this help") do
        puts parser
        exit
      end
    end

    opt_parser.parse!(options)
    return args
  end
end
options = Parser.parse %w[--help]

#=>
   # Usage: example.rb [options]
   #     -n, --name=NAME                  Name to say hello to
   #     -h, --help                       Prints this help

```

--------------------------------

### Fetch Start Line

Source: https://docs.ruby-lang.org/en/master/Prism/Relocation/Entry

Retrieves the start line number of a value from the Prism::Relocation::Entry. This method relies on the fetch_value private method.

```ruby
# File lib/prism/relocation.rb, line 36
def start_line
  fetch_value(:start_line)
end
```

--------------------------------

### Initialize Emitter in Ruby

Source: https://docs.ruby-lang.org/en/master/Psych/Visitors/Emitter

Initializes a new Psych::Emitter. Accepts an IO object and optional parameters for indentation, canonical output, and line width. Creates a Psych::Emitter instance with or without dumper options based on the provided options.

```ruby
def initialize io, options = {}
  opts = [:indentation, :canonical, :line_width].find_all { |opt|
    options.key?(opt)
  }

  if opts.empty?
    @handler = Psych::Emitter.new io
  else
    du = Handler::DumperOptions.new
    opts.each { |option| du.send :"#{option} Mac", options[option] }
    @handler = Psych::Emitter.new io, du
  end
end
```

--------------------------------

### Ruby ARGV: Initial State Display

Source: https://docs.ruby-lang.org/en/master/ARGF

A simple Ruby script to display the initial contents of the ARGV array, showing command-line arguments and options passed to the program.

```ruby
# Print arguments (and options, if any) found on command line.
p ['ARGV', ARGV]
```

--------------------------------

### Writing to IO Buffer in Ruby (Usage Example)

Source: https://docs.ruby-lang.org/en/master/IO/Buffer

This Ruby code demonstrates how to write a specified number of bytes from an IO::Buffer to a file. It uses `File.open` to create an output file and `IO::Buffer.for` to create the buffer.

```ruby
out = File.open('output.txt', 'wb')
IO::Buffer.for('1234567').write(out, 3)
```

--------------------------------

### Set Post-Installation Message - Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Specification

Sets a message that will be displayed to the user after the gem is successfully installed.

```ruby
spec.post_install_message = "Thanks for installing!"

```

--------------------------------

### Initialize GzipReader with IO object and options

Source: https://docs.ruby-lang.org/en/master/Zlib/GzipReader

Shows the C implementation for initializing a Zlib::GzipReader. It takes an IO object and an optional options hash. The method handles stream initialization, reading the gzip header, and setting up options like encoding. It also includes error handling for invalid gzip headers.

```c
static VALUE
rb_gzreader_initialize(int argc, VALUE *argv, VALUE obj)
{
    VALUE io, opt = Qnil;
    struct gzfile *gz;
    int err;

    TypedData_Get_Struct(obj, struct gzfile, &gzfile_data_type, gz);
    rb_scan_args(argc, argv, "1:", &io, &opt);

    /* this is undocumented feature of zlib */
    err = inflateInit2(&gz->z.stream, -MAX_WBITS);
    if (err != Z_OK) {
        raise_zlib_error(err, gz->z.stream.msg);
    }
    gz->io = io;
    ZSTREAM_READY(&gz->z);
    gzfile_read_header(gz, Qnil);
    rb_gzfile_ecopts(gz, opt);

    if (rb_respond_to(io, id_path)) {
        /* File#path may raise IOError in case when a path is unavailable */
        rb_rescue2(gzfile_initialize_path_partial, obj, NULL, Qnil, rb_eIOError, (VALUE)0);
    }

    return obj;
}
```

--------------------------------

### Regenerate RubyGems Binstubs

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Regenerates the executable "binstubs" for all installed gems. It uses the PristineCommand to ensure executables are up-to-date and correctly linked. This function can optionally include a specific bindir and manage environment shebangs.

```ruby
def regenerate_binstubs(bindir)
  require_relative "pristine_command"
  say "Regenerating binstubs"

  args = %w[--all --only-executables --silent]
  args << "--bindir=#{bindir}"
  args << "--install-dir=#{default_dir}"

  if options[:env_shebang]
    args << "--env-shebang"
  end

  command = Gem::Commands::PristineCommand.new
  command.invoke(*args)
end
```

--------------------------------

### Configure Gem Installation Directory

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Sets the directory where gems will be installed. Uses File.expand_path to resolve the absolute path. This option is part of the install/update functionality.

```ruby
add_option(:'Install/Update', "-i", "--install-dir DIR",
             "Gem repository directory to get installed",
             "gems") do |value, options|
    options[:install_dir] = File.expand_path(value)
  end
```

--------------------------------

### Example Usage of Tempfile.open with a block

Source: https://docs.ruby-lang.org/en/master/Tempfile

Shows how to use `Tempfile.open` with a block to perform operations on a temporary file and how it's equivalent to manually opening, yielding, and ensuring closure.

```ruby
Tempfile.open('foo', '/home/temp') do |f|
   # ... do something with f ...
end

# Equivalent:
f = Tempfile.open('foo', '/home/temp')
begin
   # ... do something with f ...
ensure
   f.close
end
```

--------------------------------

### Initialize Net::WriteAdapter (Ruby)

Source: https://docs.ruby-lang.org/en/master/Net/WriteAdapter

Initializes a new instance of Net::WriteAdapter with a given writer object. The writer is expected to be a callable object (like a Proc or lambda) that handles the actual writing.

```ruby
# File lib/net/protocol.rb, line 487
def initialize(writer)
  @writer = writer
end
```

--------------------------------

### GET Request

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Sends a GET request to the specified path with optional headers. Returns the response object or yields it to a block.

```APIDOC
## GET /todos

### Description
Retrieves a list of resources or a specific resource if an ID is provided.

### Method
GET

### Endpoint
/todos

#### Query Parameters
- **id** (integer) - Optional - The ID of the specific resource to retrieve.

### Response
#### Success Response (200)
- **response** (Net::HTTPResponse) - The response from the server.

### Response Example
```
#<Net::HTTPOK 200 OK readbody=true>
```
```

--------------------------------

### Create and Run a Simple Ractor in Ruby

Source: https://docs.ruby-lang.org/en/master/Ractor

Demonstrates the creation of a basic Ractor using Ractor.new and how to wait for its completion using join. The Ractor executes a simple puts statement.

```ruby
r = Ractor.new {puts "I am in Ractor!"}
r.join # wait for it to finish
# Here, "I am in Ractor!" is printed
```

--------------------------------

### RubyVM::InstructionSequence.new

Source: https://docs.ruby-lang.org/en/master/RubyVM/InstructionSequence

Creates a new instruction sequence from Ruby source code, similar to `compile`.

```APIDOC
## RubyVM::InstructionSequence.new

### Description
Creates a new instruction sequence from Ruby source code. This method is similar to `::compile` and accepts the same parameters for source code, metadata, and compiler options.

### Method
`RubyVM::InstructionSequence.new(source[, file[, path[, line[, options]]]])`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **source** (String or File) - The Ruby source code to compile.
- **file** (String, optional) - Metadata for the filename.
- **path** (String, optional) - Metadata for the real path (used for `require_relative`).
- **line** (Integer, optional) - Metadata for the starting line number.
- **options** (Boolean or Hash, optional) - Compiler options.

### Request Example
```json
{
  "source": "def greet; puts 'hello'; end",
  "file": "greet.rb"
}
```

### Response
#### Success Response (200)
- **iseq** (RubyVM::InstructionSequence) - The newly created instruction sequence object.

#### Response Example
```json
{
  "iseq": "<RubyVM::InstructionSequence:greet.rb>"
}
```
```

--------------------------------

### Ruby Array Assignment with Start and Length

Source: https://docs.ruby-lang.org/en/master/Array

Assigns an object to a slice of the array defined by a start index and length. The specified elements are replaced. If start + length exceeds bounds, assignment occurs up to the end or the specified length.

```ruby
a = [:foo, 'bar', 2]
a[0, 2] = 'foo'
# a is now ["foo", 2]
a[6, 50] = 'foo'
# a is now [:foo, "bar", 2, nil, nil, nil, "foo"]
```

--------------------------------

### Gem Install Failure due to Untrusted Certificate

Source: https://docs.ruby-lang.org/en/master/Gem/Security

Demonstrates the error encountered when installing a gem with a 'HighSecurity' policy where the signing certificate is not trusted.

```shell
$ gem install -P HighSecurity your-gem-1.0.gem
ERROR:  While executing gem ... (Gem::Security::Exception) 
    root cert /CN=you/DC=example is not trusted
```

--------------------------------

### Setup Coverage Measurement

Source: https://docs.ruby-lang.org/en/master/Coverage

Configures the coverage measurement. Can be called with no arguments for default mode, with 'all' to enable all types of coverage, or with a hash to specify lines, branches, methods, eval, or oneshot_lines. Raises an error if setup is already done or if lines and oneshot_lines are enabled simultaneously.

```C
static VALUE
rb_coverage_setup(int argc, VALUE *argv, VALUE klass)
{
    VALUE coverages, opt;
    int mode;

    if (current_state != IDLE) {
        rb_raise(rb_eRuntimeError, "coverage measurement is already setup");
    }

    rb_scan_args(argc, argv, "01", &opt);

    if (argc == 0) {
        mode = 0; /* compatible mode */
    }
    else if (opt == ID2SYM(rb_intern("all"))) {
        mode = COVERAGE_TARGET_LINES | COVERAGE_TARGET_BRANCHES | COVERAGE_TARGET_METHODS | COVERAGE_TARGET_EVAL;
    }
    else {
        mode = 0;
        opt = rb_convert_type(opt, T_HASH, "Hash", "to_hash");

        if (RTEST(rb_hash_lookup(opt, ID2SYM(rb_intern("lines")))))
            mode |= COVERAGE_TARGET_LINES;
        if (RTEST(rb_hash_lookup(opt, ID2SYM(rb_intern("branches")))))
            mode |= COVERAGE_TARGET_BRANCHES;
        if (RTEST(rb_hash_lookup(opt, ID2SYM(rb_intern("methods")))))
            mode |= COVERAGE_TARGET_METHODS;
        if (RTEST(rb_hash_lookup(opt, ID2SYM(rb_intern("oneshot_lines"))))) {
            if (mode & COVERAGE_TARGET_LINES)
                rb_raise(rb_eRuntimeError, "cannot enable lines and oneshot_lines simultaneously");
            mode |= COVERAGE_TARGET_LINES;
            mode |= COVERAGE_TARGET_ONESHOT_LINES;
        }
        if (RTEST(rb_hash_lookup(opt, ID2SYM(rb_intern("eval")))))
            mode |= COVERAGE_TARGET_EVAL;
    }

    if (mode & COVERAGE_TARGET_METHODS) {
        me2counter = rb_ident_hash_new();
    }
    else {
        me2counter = Qnil;
    }

```

--------------------------------

### Define Long Option Names in Ruby

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Illustrates defining command-line options with single long names and multiple long name aliases using Ruby's OptionParser. The examples cover parsing options and handling different long name formats.

```Ruby
require 'optparse'
parser = OptionParser.new
parser.on('--xxx', 'Long name') do |value|
  p ['-xxx', value]
end
parser.on('--y1%', '--z2#', "Two long names") do |value|
  p ['--y1% or --z2#', value]
end
parser.parse!
```

--------------------------------

### Install macOS Dependencies

Source: https://docs.ruby-lang.org/en/master/yjit/yjit_md

This command installs necessary libraries (openssl and libyaml) on macOS using Homebrew, which might be required for building Ruby with YJIT.

```bash
# Install dependencies
brew install openssl libyaml
```

--------------------------------

### Initialize Prism::PostExecutionNode

Source: https://docs.ruby-lang.org/en/master/Prism/PostExecutionNode

Initializes a new PostExecutionNode instance. It takes source, node_id, location, flags, statements, and location details for keyword, opening, and closing delimiters.

```ruby
# File lib/prism/node.rb, line 14782
def initialize(source, node_id, location, flags, statements, keyword_loc, opening_loc, closing_loc)
  @source = source
  @node_id = node_id
  @location = location
  @flags = flags
  @statements = statements
  @keyword_loc = keyword_loc
  @opening_loc = opening_loc
  @closing_loc = closing_loc
end
```

--------------------------------

### Fetch Start Character Offset

Source: https://docs.ruby-lang.org/en/master/Prism/Relocation/Entry

Retrieves the start character offset of a value from the Prism::Relocation::Entry. This method relies on the fetch_value private method.

```ruby
# File lib/prism/relocation.rb, line 56
def start_character_offset
  fetch_value(:start_character_offset)
end
```

--------------------------------

### GET /fetch_https

Source: https://docs.ruby-lang.org/en/master/Gem/RemoteFetcher

Alias for `fetch_http`. Performs an HTTPS GET or HEAD request to a given URI.

```APIDOC
## GET /fetch_https

### Description
Alias for `fetch_http`. Performs an HTTPS GET or HEAD request to a given URI.

### Method
GET

### Endpoint
/fetch_https

### Parameters
#### Path Parameters
- **uri** (URI) - Required - The URI to fetch.
- **last_modified** (Time) - Optional - The If-Modified-Since header value.
- **head** (Boolean) - Optional - If true, performs a HEAD request. Defaults to false.
- **depth** (Integer) - Optional - Internal use for tracking redirect depth.

### Request Example
```json
{
  "uri": "https://example.com/secure_resource",
  "last_modified": "2023-01-01T10:00:00Z",
  "head": false
}
```

### Response
#### Success Response (200)
- **response** (Object) - The HTTPS response object. If `head` is true, returns the response headers; otherwise, returns the response body.

#### Response Example
```json
{
  "response": "HTTP/1.1 200 OK\nContent-Type: text/plain\n\nResponse body content"
}
```
```

--------------------------------

### Send GET Request

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Sends an HTTP GET request to the specified path. Can optionally take initialization headers and a block to process the response.

```ruby
def get(path, initheader = nil) {|res| ... }
```

--------------------------------

### Installing Rosetta on Apple Silicon

Source: https://docs.ruby-lang.org/en/master/yjit/yjit_md

Demonstrates the command to install Rosetta on Apple Silicon Macs, enabling the execution of x86 binaries. This is a prerequisite for running x86 YJIT on M1 machines.

```shell
$ softwareupdate --install-rosetta

```

--------------------------------

### Ruby IO#gets - Special Separator Values

Source: https://docs.ruby-lang.org/en/master/IO

Shows the usage of special values `nil` and `''` for the separator argument. `gets(nil)` reads the entire stream, while `gets('')` reads up to two consecutive line separators (paragraphs).

```ruby
f = File.new('t.txt')
# Get all.
f.gets(nil) # => "First line\nSecond line\n\nFourth line\nFifth line\n"
f.rewind
# Get paragraph (up to two line separators).
f.gets('')  # => "First line\nSecond line\n\n"
f.close
```

--------------------------------

### Get Ruby Configuration (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Retrieves the Ruby configuration settings for the target platform. This method uses `Gem.target_rbconfig` to access these settings.

```Ruby
def rb_config
  Gem.target_rbconfig
end
```

--------------------------------

### Basic Net::HTTP Requests (Ruby)

Source: https://docs.ruby-lang.org/en/master/Net

Demonstrates making basic HTTP requests using Net::HTTP in Ruby. Includes GET, POST, and PUT requests to a specified URI with optional data.

```Ruby
require 'net/http'
require 'uri'

uri = URI('http://example.com/path')

# GET request
response_get = Net::HTTP.get_response(uri)

# POST request with data
data_post = '{"title": "foo", "body": "bar", "userId": 1}'
response_post = Net::HTTP.post(uri, data_post)

# POST request with form parameters
params_post_form = {title: 'foo', body: 'bar', userId: 1}
response_post_form = Net::HTTP.post_form(uri, params_post_form)

# PUT request with data
data_put = '{"title": "foo", "body": "bar", "userId": 1}'
response_put = Net::HTTP.put(uri, data_put)
```

--------------------------------

### Ruby: Prism::FindPatternNode Examples

Source: https://docs.ruby-lang.org/en/master/Prism/FindPatternNode

Illustrates various ways a find pattern can be represented in Ruby's pattern matching.

```ruby
foo in *bar, baz, *qux
       ^^^^^^^^^^^^^^^^

foo in [*bar, baz, *qux]
       ^^^^^^^^^^^^^^^^^^^

foo in Foo(*bar, baz, *qux)
       ^^^^^^^^^^^^^^^^^^^^^^^

foo => *bar, baz, *qux
       ^^^^^^^^^^^^^^^^

```

--------------------------------

### Open3.popen3 with Environment and Options

Source: https://docs.ruby-lang.org/en/master/Open3

Allows specifying environment variables and process options, similar to `Process.spawn`. The first hash argument sets the environment, and the last hash argument sets options for `Process.spawn`.

```APIDOC
## Open3.popen3 with Environment and Options

### Description
Allows specifying environment variables and process options, similar to `Process.spawn`. The first hash argument sets the environment (`env`), and the last hash argument sets options for `Process.spawn` (`options`). The method yields three streams (stdin, stdout, stderr) and a wait_thread to a block.

### Method
`Open3.popen3`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **command_line** or **exe_path** (String or Array) - Required - The command or executable to run.
- **env** (Hash) - Optional - A hash of environment variables for the child process.
- **[args]** (String) - Optional - Arguments to be passed to the executable.
- **options** (Hash) - Optional - A hash of options for `Process.spawn`.
- **[block]** (Proc) - The block to be executed with the child process's streams and wait thread.

### Request Example
```ruby
env_vars = { "MY_VAR" => "my_value" }
Open3.popen3('puts ENV["MY_VAR"]', :env => env_vars) do |stdin, stdout, stderr, wait_thread|
  puts stdout.read
end
```

### Response
#### Success Response (Block Return Value)
- The return value of the provided block.

#### Response Example
```
my_value
```

### Error Handling
- **Errno::ENOENT**: Raised if the executable specified does not exist.
- **Deadlock**: Potential deadlock if stdout or stderr are not read simultaneously, leading to buffer fills.
```

--------------------------------

### YAML::Store Initialize Method in Ruby

Source: https://docs.ruby-lang.org/en/master/YAML/Store

Shows the implementation of the `initialize` method for the YAML::Store class, detailing how it handles file names, optional hash arguments, and superclass calls.

```ruby
# File lib/yaml/store.rb, line 57
def initialize( *o )
  @opt = {}
  if o.last.is_a? Hash
    @opt.update(o.pop)
  end
  super(*o)
end
```

--------------------------------

### Process.waitall usage example (Ruby)

Source: https://docs.ruby-lang.org/en/master/Process

Illustrates waiting for all spawned child processes to complete using Process.waitall. It returns an array of [pid, status] pairs for each finished child process.

```ruby
pid0 = Process.spawn('ruby', '-e', 'exit 13') # => 325470
pid1 = Process.spawn('ruby', '-e', 'exit 14') # => 325495
Process.waitall
```

--------------------------------

### Force Gem Installation

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Forces the installation of a gem, bypassing dependency checks. This can be useful when dealing with specific version requirements or resolving conflicts, but should be used with caution.

```ruby
add_option(:'Install/Update', "-f", "--[no-]force",
             "Force gem to install, bypassing dependency",
             "checks") do |value, options|
    options[:force] = value
  end
```

--------------------------------

### Initialize Gem::StreamUI::ThreadedDownloadReporter

Source: https://docs.ruby-lang.org/en/master/Gem/StreamUI/ThreadedDownloadReporter

Creates a new threaded download reporter. It initializes the reporter to display progress on a given output stream. Other arguments are ignored.

```ruby
def initialize(out_stream, *args)
  @file_name = nil
  @out = out_stream
end
```

--------------------------------

### Fetch Start Character Column

Source: https://docs.ruby-lang.org/en/master/Prism/Relocation/Entry

Retrieves the start character column of a value from the Prism::Relocation::Entry. This method relies on the fetch_value private method.

```ruby
# File lib/prism/relocation.rb, line 88
def start_character_column
  fetch_value(:start_character_column)
end
```

--------------------------------

### Ruby Range.end Method Examples

Source: https://docs.ruby-lang.org/en/master/Range

Provides examples of using the `end` method on different types of Ruby Ranges, including inclusive, exclusive, and infinite ranges.

```ruby
(1..4).end  # => 4
(1...4).end # => 4
(1..).end   # => nil
```

--------------------------------

### Ruby: GET Request with Output to STDOUT

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Shows how to perform a GET request and print the response body directly to standard output using Net::HTTP. This is useful for quick checks or simple data retrieval.

```ruby
# Write string response body to $stdout.
Net::HTTP.get_print(hostname, path)
Net::HTTP.get_print(uri)
```

--------------------------------

### Ruby OptionParser: Define Options

Source: https://docs.ruby-lang.org/en/master/optparse/tutorial_rdoc

Demonstrates defining options using 'define', 'define_head', and 'define_tail' methods in Ruby's OptionParser. These methods allow appending or prepending options to lists and return the created option object.

```ruby
require 'optparse'

parser = OptionParser.new do |opts|
  opts.on('-a', '--all', 'Include all data') do
    # Process --all option
  end

  opts.on_head('-v', '--verbose', 'Enable verbose output') do
    # Process --verbose option
  end

  opts.define_tail('--config FILE', 'Specify configuration file') do |file|
    # Process --config option
  end
end

# Example usage: The 'opts' object itself is returned by 'on' and 'on_head'
# 'define_tail' returns the created option object
```

--------------------------------

### Ruby Proc Closure Example

Source: https://docs.ruby-lang.org/en/master/Proc

Illustrates the closure behavior of Procs, where they remember the context (variables) in which they were created. This example shows a Proc remembering a 'factor' variable.

```ruby
def gen_times(factor)
  Proc.new {|n| n*factor } # remembers the value of factor at the moment of creation
end

times3 = gen_times(3)
times5 = gen_times(5)

times3.call(12)               #=> 36
times5.call(5)                #=> 25
times3.call(times5.call(4))   #=> 60
```

--------------------------------

### Prepend Destination Directory to Path

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Prepends the destination directory (specified in options[:destdir]) to a given path. This is useful for staging installations where a different root directory is used. It handles Windows drive letters by removing them before joining.

```ruby
def prepend_destdir_if_present(path)
  destdir = options[:destdir]
  return path if destdir.empty?

  File.join(options[:destdir], path.gsub(/^[a-zA-Z]:/, ""))
end
```

--------------------------------

### Psych::Handler#start_document - Handle Start of Document

Source: https://docs.ruby-lang.org/en/master/Psych/Handler

Called at the beginning of a YAML document. It receives the `version` information, `tag_directives` (prefix/suffix mappings), and an `implicit` flag indicating if the document start was implicit.

```ruby
# File ext/psych/lib/psych/handler.rb, line 72
def start_document version, tag_directives, implicit
end
```

--------------------------------

### Build Ruby with Mingw (cmd)

Source: https://docs.ruby-lang.org/en/master/windows_md

Steps to build Ruby using the Mingw compiler with UCRT in a Windows command prompt. This involves installing the RIDK, enabling the UCRT64 environment, and using pacman for dependencies.

```shell
ridk install
ridk enable ucrt64

pacman -S --needed %MINGW_PACKAGE_PREFIX%-openssl %MINGW_PACKAGE_PREFIX%-libyaml %MINGW_PACKAGE_PREFIX%-libffi

mkdir c:\work\ruby
cd /d c:\work\ruby

git clone https://github.com/ruby/ruby src

sh ./src/autogen.sh

mkdir build
cd build
sh ../src/configure -C --disable-install-doc
make
```

--------------------------------

### Net::HTTP.start

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Starts an HTTP session. It can be used with or without a block. When used with a block, it automatically manages the session lifecycle.

```APIDOC
## Net::HTTP.start

### Description
Starts an HTTP session, establishing a connection to the specified host and port. This method can optionally take an options hash for configuring the connection, such as SSL settings.

### Method

`HTTP.start(address, *arg, &block)`

### Parameters

#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```ruby
hostname = 'jsonplaceholder.typicode.com'
Net::HTTP.start(hostname) do |http|
  puts http.get('/todos/1').body
end
```

### Response
#### Success Response (200)
Returns the result of the block if a block is given, otherwise returns the `Net::HTTP` object itself.

#### Response Example
```json
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```

**Note**: The `opts` hash can include keys like `ca_file`, `cert`, `ipaddr`, `read_timeout`, `use_ssl`, etc.
```

--------------------------------

### Thread::Queue Initialization Source Code

Source: https://docs.ruby-lang.org/en/master/Thread/Queue

Provides the C source code for the `Thread::Queue.initialize` method, detailing how new queue instances are created and optionally populated.

```c
static VALUE
rb_queue_initialize(int argc, VALUE *argv, VALUE self)
{
    VALUE initial;
    struct rb_queue *q = queue_ptr(self);
    if ((argc = rb_scan_args(argc, argv, "01", &initial)) == 1) {
        initial = rb_to_array(initial);
    }
    RB_OBJ_WRITE(self, queue_list(q), ary_buf_new());
    ccan_list_head_init(queue_waitq(q));
    if (argc == 1) {
        rb_ary_concat(q->que, initial);
    }
    return self;
}
```

--------------------------------

### Set File Creation umask for New Process (Ruby)

Source: https://docs.ruby-lang.org/en/master/Process

Demonstrates using the `:umask` execution option with `Process.spawn` to control the file mode creation mask for the new process. The example executes Ruby code to print its umask.

```Ruby
command = 'ruby -e "puts sprintf(\"0%o\", File.umask)"'
options = {:umask => 0644}
Process.spawn(command, options)
```

--------------------------------

### Build Ruby on Different Drive

Source: https://docs.ruby-lang.org/en/master/windows_md

Illustrates building Ruby when the source and build directories are located on different drives. This involves changing drives and specifying the correct paths for the configure script and installation.

```batch
D:
cd D:\build\ruby
C:\src\ruby\win32\configure --prefix=/usr/local
nmake
nmake check
nmake install DESTDIR=C:
```

--------------------------------

### Build Gem Package with Specification

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/BuildCommand

Loads the specified gemspec and uses `Gem::Package.build` to create the gem. It passes options for force, strictness, and output file. Includes error handling for loading the gemspec.

```ruby
def build_package(gemspec)
  spec = Gem::Specification.load(gemspec)
  if spec
    Gem::Package.build(
      spec,
      options[:force],
      options[:strict],
      options[:output]
    )
  else
    alert_error "Error loading gemspec. Aborting."
    terminate_interaction 1
  end
end
```

--------------------------------

### Ruby MonitorMixin: Simple object.extend Example

Source: https://docs.ruby-lang.org/en/master/MonitorMixin

Demonstrates using MonitorMixin to synchronize threads accessing a shared buffer. The consumer thread waits for data, and the producer thread adds data and signals the consumer. This showcases basic thread communication and synchronization.

```ruby
require 'monitor.rb'

buf = []
buf.extend(MonitorMixin)
empty_cond = buf.new_cond

# consumer
Thread.start do
  loop do
    buf.synchronize do
      empty_cond.wait_while { buf.empty? }
      print buf.shift
    end
  end
end

# producer
while line = ARGF.gets
  buf.synchronize do
    buf.push(line)
    empty_cond.signal
  end
end

```

--------------------------------

### OpenSSL::Config Constructor

Source: https://docs.ruby-lang.org/en/master/OpenSSL/Config

Creates a new OpenSSL::Config object from a file. Supports loading configuration from a specified file path.

```APIDOC
## new /websites/ruby-lang_en_master

### Description
Creates an instance of `OpenSSL::Config` from the content of the file specified by _filename_.
This can be used in contexts like `OpenSSL::X509::ExtensionFactory.config=`
This can raise `IO` exceptions based on the access, or availability of the file. A `ConfigError` exception may be raised depending on the validity of the data being configured.

### Method
**NEW**

### Endpoint
**/websites/ruby-lang_en_master**

### Parameters
#### Path Parameters
- **filename** (String) - Required - The path to the configuration file.

### Request Example
```json
{
  "filename": "/etc/ssl/openssl.cnf"
}
```

### Response
#### Success Response (200)
- **OpenSSL::Config** (Object) - An instance of the OpenSSL::Config class.

#### Response Example
```json
{
  "config_object": "<OpenSSL::Config>"
}
```
```

--------------------------------

### Example: Signing data with RSA PSS padding in Ruby

Source: https://docs.ruby-lang.org/en/master/OpenSSL/PKey/PKey

This example demonstrates signing a string using RSA with PSS padding. It first generates an RSA key, then calls the `sign` method with the digest algorithm, the data to be signed, and a hash specifying the padding mode.

```ruby
data = "Sign me!"
pkey = OpenSSL::PKey.generate_key("RSA", rsa_keygen_bits: 2048)
signopts = { rsa_padding_mode: "pss" }
signature = pkey.sign("SHA256", data, signopts)
```

--------------------------------

### Execute Command via Shell in Ruby

Source: https://docs.ruby-lang.org/en/master/Process

This Ruby code example shows how to execute a command line string through the system's shell. It demonstrates using shell reserved words, built-ins, and meta-characters, and includes examples of handling command output and errors. Potential security risks like command injection are highlighted.

```ruby
spawn('if true; then echo "Foo"; fi') # => 798847 # Shell reserved word.
Process.wait                          # => 798847
spawn('exit')                         # => 798848 # Built-in.
Process.wait                          # => 798848
spawn('date > /tmp/date.tmp')         # => 798879 # Contains meta character.
Process.wait                          # => 798849
spawn('date > /nop/date.tmp')         # => 798882 # Issues error message.
Process.wait                          # => 798882
```

```ruby
spawn('echo "Foo"') # => 799031
Process.wait        # => 799031
```

--------------------------------

### Example: Creating a symbolic link when the destination is a directory

Source: https://docs.ruby-lang.org/en/master/FileUtils

Demonstrates creating a symbolic link within a destination directory, where the link name is derived from the source path.

```ruby
FileUtils.touch('src2.txt')
FileUtils.mkdir('destdir2')
FileUtils.ln_s('src2.txt', 'destdir2')
File.symlink?('destdir2/src2.txt') # => true
```

--------------------------------

### Object singleton_method example in Ruby

Source: https://docs.ruby-lang.org/en/master/NEWS/NEWS-3_4_0_md

Demonstrates the usage of Object#singleton_method, which now includes methods from modules prepended or included in the receiver's singleton class. This example shows how to extend an object with a module and then call a singleton method defined within that module.

```ruby
o = Object.new
o.extend(Module.new{def a = 1})
o.singleton_method(:a).call #=> 1
```

--------------------------------

### Ruby String Conversion Example

Source: https://docs.ruby-lang.org/en/master/implicit_conversion_rdoc

Presents a String-convertible object in Ruby using the `to_str` method. The example shows `String.new` successfully converting this object into a String.

```Ruby
class StringConvertible
  def to_str
    'foo'
  end
end
String.new(StringConvertible.new) # => "foo"

```

--------------------------------

### Set Start Location for Node

Source: https://docs.ruby-lang.org/en/master/Psych/TreeBuilder

The private `set_start_location` method assigns the stored start line and column numbers to the provided node.

```ruby
# File ext/psych/lib/psych/tree_builder.rb, line 127
def set_start_location(node)
  node.start_line   = @start_line
  node.start_column = @start_column
end
```

--------------------------------

### Initialize Gem::Commands::CheckCommand in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/CheckCommand

Initializes the CheckCommand for RubyGems, setting up options for checking gem repositories and installed gems. This includes options for reporting unmanaged files, cleaning up uninstalled gems, performing dry runs, and checking installed gems.

```ruby
# File lib/rubygems/commands/check_command.rb, line 11
def initialize
  super "check", "Check a gem repository for added or missing files",
        alien: true, doctor: false, dry_run: false, gems: true

  add_option("-a", "--[no-]alien",
             'Report "unmanaged" or rogue files in the',
             "gem repository") do |value, options|
    options[:alien] = value
  end

  add_option("--[no-]doctor",
             "Clean up uninstalled gems and broken",
             "specifications") do |value, options|
    options[:doctor] = value
  end

  add_option("--[no-]dry-run",
             "Do not remove files, only report what",
             "would be removed") do |value, options|
    options[:dry_run] = value
  end

  add_option("--[no-]gems",
             "Check installed gems for problems") do |value, options|
    options[:gems] = value
  end

  add_version_option "check"
end
```

--------------------------------

### Inspect Location (Ruby)

Source: https://docs.ruby-lang.org/en/master/Prism/Location

Provides a string representation of the Location object, including its start offset, length, and start line.

```ruby
def inspect
  "#<Prism::Location @start_offset=#{@start_offset} @length=#{@length} start_line=#{start_line}>"
end
```

--------------------------------

### Initialize Configuration Copy (Ruby)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/Config

Initializes a new configuration object by copying the contents of another configuration object. It converts the source object to a string, loads it into a BIO, and then populates the new configuration. The new object is frozen after copying.

```Ruby
static VALUE
config_initialize_copy(VALUE self, VALUE other)
{
    CONF *conf = GetConfig(self);
    VALUE str;
    BIO *bio;

    str = rb_funcall(other, rb_intern("to_s"), 0);
    rb_check_frozen(self);
    bio = ossl_obj2bio(&str);
    config_load_bio(conf, bio); /* Consumes BIO */
    rb_obj_freeze(self);
    return self;
}
```

--------------------------------

### Default Executable Format (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Retrieves the default format for executables, which is typically based on Ruby's program prefix and suffix.

```ruby
def exec_format
  @exec_format ||= Gem.default_exec_format
end
```

--------------------------------

### Initialize OpenSSL::X509::StoreContext in C

Source: https://docs.ruby-lang.org/en/master/OpenSSL/X509/StoreContext

Initializes a new StoreContext for validating an X.509 certificate. It takes a store, an optional certificate, and an optional chain of certificates. The context is initialized using X509_STORE_CTX_init. Dependencies include the OpenSSL library.

```c
static VALUE
ossl_x509stctx_initialize(int argc, VALUE *argv, VALUE self)
{
    VALUE store, cert, chain;
    X509_STORE_CTX *ctx;
    X509_STORE *x509st;
    X509 *x509 = NULL;
    STACK_OF(X509) *x509s = NULL;
    int state;

    rb_scan_args(argc, argv, "12", &store, &cert, &chain);
    GetX509StCtx(self, ctx);
    GetX509Store(store, x509st);
    if (!NIL_P(cert))
        x509 = DupX509CertPtr(cert); /* NEED TO DUP */
    if (!NIL_P(chain)) {
        x509s = ossl_protect_x509_ary2sk(chain, &state);
        if (state) {
            X509_free(x509);
            rb_jump_tag(state);
        }
    }
    if (X509_STORE_CTX_init(ctx, x509st, x509, x509s) != 1){
        X509_free(x509);
        sk_X509_pop_free(x509s, X509_free);
        ossl_raise(eX509StoreError, "X509_STORE_CTX_init");
    }
    rb_iv_set(self, "@verify_callback", rb_iv_get(store, "@verify_callback"));
    rb_iv_set(self, "@cert", cert);

    return self;
}
```

--------------------------------

### Ruby: String Translation Examples

Source: https://docs.ruby-lang.org/en/master/String

Provides examples of the `tr` method's behavior, including simple character replacement, padding with the last replacement character, and using character selectors like negation and ranges.

```Ruby
'hello'.tr('el', 'ip') #=> "hippo"
'hello'.tr('aeiou', '-')   # => "h-ll-"
'hello'.tr('aeiou', 'AA-') # => "hAll-"

# Negation.
'hello'.tr('^aeiou', '-') # => "-e--o"
# Ranges.
'ibm'.tr('b-z', 'a-z') # => "hal"
```

--------------------------------

### Get Gem Contents

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/ContentsCommand

Fetches and displays the contents of a specified gem. It first finds the gem's specification and then uses `files_in` to get the list of files, subsequently displaying them.

```ruby
def gem_contents(name)
  spec = spec_for name

  return false unless spec

  files = files_in spec

  show_files files

  true
end
```

--------------------------------

### Ruby: Constant Assignment Example

Source: https://docs.ruby-lang.org/en/master/Prism/ConstantWriteNode

Demonstrates the basic syntax for assigning a value to a constant in Ruby.

```ruby
Foo = 1
^^^^^^^
```

--------------------------------

### Initialize OpenSSL::X509::Store from a PEM File (Ruby)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/X509/Store

Creates a new X509::Store and adds certificates from a specified PEM file. This is useful when system defaults are unavailable or a custom set of CAs is required.

```ruby
cert_store = OpenSSL::X509::Store.new
cert_store.add_file 'cacert.pem'
```

--------------------------------

### Spawn Process with Environment Variables (Ruby)

Source: https://docs.ruby-lang.org/en/master/Process

Demonstrates spawning a new process with specific environment variables set. The `spawn` method executes a command and returns the new process ID without waiting for completion. This example shows how to pass an environment hash to `spawn`.

```ruby
Process.spawn({'Foo' => '0'}, 'ruby -e "p ENV[\"Foo\"]"')
```

--------------------------------

### Execute RubyGems ServerCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/ServerCommand

Executes the server command, which currently provides an error message instructing the user to install the 'rubygems-server' gem.

```ruby
def execute
  alert_error "Install the rubygems-server gem for the server command"
end
```

--------------------------------

### Execute a pipeline of commands using Open3.pipeline in Ruby

Source: https://docs.ruby-lang.org/en/master/Open3

Creates a pipeline of child processes by calling Process.spawn for each command. The standard output of each process is piped to the standard input of the next, and the method returns an array of Process::Status objects, one for each child process. Accepts an options hash as the last argument.

```ruby
def pipeline(*cmds)
  if Hash === cmds.last
    opts = cmds.pop.dup
  else
    opts = {}
  end

  pipeline_run(cmds, opts, [], []) {|ts|
    ts.map(&:value)
  }
end
```

```ruby
wait_threads = Open3.pipeline('ls', 'grep R')
```

--------------------------------

### Install Gem with High Security Policy

Source: https://docs.ruby-lang.org/en/master/Gem/Security

Installs a gem while enforcing a 'HighSecurity' policy, which requires trusted signatures and disallows unsigned gems.

```shell
# install the gem with using the security policy "HighSecurity"
$ sudo gem install your.gem -P HighSecurity
```

--------------------------------

### Initialize BlockParameterNode

Source: https://docs.ruby-lang.org/en/master/Prism/BlockParameterNode

Shows the constructor for the `BlockParameterNode` class, detailing the parameters required for initialization.

```ruby
# File lib/prism/node.rb, line 1990
def initialize(source, node_id, location, flags, name, name_loc, operator_loc)
  @source = source
  @node_id = node_id
  @location = location
  @flags = flags
  @name = name
  @name_loc = name_loc
  @operator_loc = operator_loc
end
```

--------------------------------

### Execute Make Commands - Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Ext/Builder

Executes 'make' commands to build and install gem native extensions. It handles Makefile existence checks, determines the appropriate make program, sets environment variables like DESTDIR and sitedir, and iterates through specified targets.

```Ruby
# File lib/rubygems/ext/builder.rb, line 24
def self.make(dest_path, results, make_dir = Dir.pwd, sitedir = nil, targets = ["clean", "", "install"],
  target_rbconfig: Gem.target_rbconfig)
  unless File.exist? File.join(make_dir, "Makefile")
    # No makefile exists, nothing to do.
    raise NoMakefileError, "No Makefile found in #{make_dir}"
  end

  # try to find make program from Ruby configure arguments first
  target_rbconfig["configure_args"] =~ /with-make-prog\=(\w+)/
  make_program_name = ENV["MAKE"] || ENV["make"] || $1
  make_program_name ||= RUBY_PLATFORM.include?("mswin") ? "nmake" : "make"
  make_program = shellsplit(make_program_name)

  # The installation of the bundled gems is failed when DESTDIR is empty in mswin platform.
  destdir = /\bnmake/i !~ make_program_name || ENV["DESTDIR"] && ENV["DESTDIR"] != "" ? format("DESTDIR=%s", ENV["DESTDIR"]) : ""

  env = [destdir]

  if sitedir
    env << format("sitearchdir=%s", sitedir)
    env << format("sitelibdir=%s", sitedir)
  end

  targets.each do |target|
    # Pass DESTDIR via command line to override what's in MAKEFLAGS
    cmd = [
      *make_program,
      *env,
      target,
    ].reject(&:empty?)
    begin
      run(cmd, results, "make #{target}".rstrip, make_dir)
    rescue Gem::InstallError
      raise unless target == "clean" # ignore clean failure
    end
  end
end
```

--------------------------------

### Build YJIT in Release Mode (Max Performance)

Source: https://docs.ruby-lang.org/en/master/yjit/yjit_md

This script configures, builds, and installs the YJIT-enabled Ruby binary in release mode for optimal performance. It uses GCC and disables documentation installation.

```bash
# Configure in release mode for maximum performance, build and install
./autogen.sh
./configure --enable-yjit --prefix=$HOME/.rubies/ruby-yjit --disable-install-doc
make -j && make install
```

--------------------------------

### Ignore Gem Dependencies

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Prevents the installation of any required dependent gems. This is useful for installing a gem in isolation or when managing dependencies manually.

```ruby
add_option(:'Install/Update', "--ignore-dependencies",
             "Do not install any required dependent gems") do |value, options|
    options[:ignore_dependencies] = value
  end
```

--------------------------------

### Start and Manage Net::HTTP Sessions in Ruby

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Initiates an HTTP session. Can be used with or without a block. When used with a block, it yields the current HTTP object, ensuring the session is automatically finished upon block completion. Without a block, it returns the HTTP object after starting the session.

```Ruby
def start  # :yield: http
  raise IOError, 'HTTP session already opened' if @started
  if block_given?
    begin
      do_start
      return yield(self)
    ensure
      do_finish
    end
  end
  do_start
  self
end
```

```Ruby
http = Net::HTTP.new(hostname)
# => #<Net::HTTP jsonplaceholder.typicode.com:80 open=false>
http.start
# => #<Net::HTTP jsonplaceholder.typicode.com:80 open=true>
http.started? # => true
http.finish
```

```Ruby
http.start do |http|
  http
end
# => #<Net::HTTP jsonplaceholder.typicode.com:80 open=false>
http.started? # => false
```

--------------------------------

### Ruby MatchData Usage Examples

Source: https://docs.ruby-lang.org/en/master/MatchData

Demonstrates how to use MatchData objects in Ruby to extract information from string matches, including accessing the full match, captures, and named captures. Shows examples with URL matching and capturing groups.

```ruby
url = 'https://docs.ruby-lang.org/en/2.5.0/MatchData.html'
m = url.match(/(\d\.?)+/)   # => #<MatchData "2.5.0" 1:"0">
m.string                    # => "https://docs.ruby-lang.org/en/2.5.0/MatchData.html"
m.regexp                    # => /(\d\.?)+/
# entire matched substring:
m[0]                        # => "2.5.0"

# Working with unnamed captures
m = url.match(%r{([^/]+)/([^/]+)\.html$})
m.captures                  # => ["2.5.0", "MatchData"]
m[1]                        # => "2.5.0"
m.values_at(1, 2)           # => ["2.5.0", "MatchData"]

# Working with named captures
m = url.match(%r{(?<version>[^/]+)/(?<module>[^/]+)\.html$})
m.captures                  # => ["2.5.0", "MatchData"]
m.named_captures            # => {"version"=>"2.5.0", "module"=>"MatchData"}
m[:version]                 # => "2.5.0"
m.values_at(:version, :module)
                            # => ["2.5.0", "MatchData"]
# Numerical indexes are working, too
m[1]                        # => "2.5.0"
m.values_at(1, 2)           # => ["2.5.0", "MatchData"]
```

--------------------------------

### Remove Installed Gems

Source: https://docs.ruby-lang.org/en/master/Gem/AvailableSet

Removes gem specifications from the set if they are already installed locally and satisfy the given dependency. The set is marked as unsorted.

```ruby
def remove_installed!(dep)
  @set.reject! do |_t|
    # already locally installed
    Gem::Specification.any? do |installed_spec|
      dep.name == installed_spec.name &&
        dep.requirement.satisfied_by?(installed_spec.version)
    end
  end

  @sorted = nil
  self
end
```

--------------------------------

### Format Program Filename in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Prefixes and suffixes a given filename according to Ruby's executable format conventions. This ensures consistency in executable naming.

```ruby
def formatted_program_filename(filename)
  if @format_executable
    self.class.exec_format % File.basename(filename)
  else
    filename
  end
end
```

--------------------------------

### Fetch Start Code Units Column

Source: https://docs.ruby-lang.org/en/master/Prism/Relocation/Entry

Retrieves the start code units column of a value, considering the repository's configured encoding. This method relies on the fetch_value private method.

```ruby
# File lib/prism/relocation.rb, line 99
def start_code_units_column
  fetch_value(:start_code_units_column)
end
```

--------------------------------

### Initialize Gem::Security::Policy

Source: https://docs.ruby-lang.org/en/master/Gem/Security/Policy

Creates a new Gem::Security::Policy object with the given name, policy settings, and options. It initializes security attributes and applies provided policy configurations.

```ruby
# File lib/rubygems/security/policy.rb, line 27
def initialize(name, policy = {}, opt = {})
  @name = name

  @opt = opt

  # Default to security
  @only_signed   = true
  @only_trusted  = true
  @verify_chain  = true
  @verify_data   = true
  @verify_root   = true
  @verify_signer = true

  policy.each_pair do |key, val|
    case key
    when :verify_data   then @verify_data   = val
    when :verify_signer then @verify_signer = val
    when :verify_chain  then @verify_chain  = val
    when :verify_root   then @verify_root   = val
    when :only_trusted  then @only_trusted  = val
    when :only_signed   then @only_signed   = val
    end
  end
end
```

--------------------------------

### Strip Comments from YAML Value | Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/YAMLSerializer

Removes YAML comments (starting with '#') from a string value, unless the string itself starts with '#'. Ensures clean data parsing.

```ruby
def strip_comment(val)
  if val.include?("#") && !val.start_with?("#")
    val.split("#", 2).first.strip
  else
    val
  end
end
```

--------------------------------

### Example: Compare File Modification Times

Source: https://docs.ruby-lang.org/en/master/File/Stat

Demonstrates comparing the modification times of two files using File::Stat#<=>. The example creates two files with a one-second delay to ensure different modification times.

```ruby
f1 = File.new("f1", "w")
sleep 1
f2 = File.new("f2", "w")
f1.stat <=> f2.stat   #=> -1
```

--------------------------------

### Fetch Start Code Units Offset

Source: https://docs.ruby-lang.org/en/master/Prism/Relocation/Entry

Retrieves the start code units offset of a value, considering the repository's configured encoding. This method relies on the fetch_value private method.

```ruby
# File lib/prism/relocation.rb, line 67
def start_code_units_offset
  fetch_value(:start_code_units_offset)
end
```

--------------------------------

### Ruby Time Class: Sunday Check Example

Source: https://docs.ruby-lang.org/en/master/Time

Provides an example of using the `sunday?` method to check if a given time falls on a Sunday.

```Ruby
t = Time.utc(2000, 1, 2) # => 2000-01-02 00:00:00 UTC
t.sunday?                # => true
```

--------------------------------

### C: Start tracing object allocations

Source: https://docs.ruby-lang.org/en/master/ObjectSpace

This C function, `trace_object_allocations`, starts tracing object allocations by calling `trace_object_allocations_start`. It then uses `rb_ensure` to execute a block (`rb_yield`) and ensures that `trace_object_allocations_stop` is called afterward, returning the result of the block.

```c
static VALUE
trace_object_allocations(VALUE self)
{
    trace_object_allocations_start(self);
    return rb_ensure(rb_yield, Qnil, trace_object_allocations_stop, self);
}
```

--------------------------------

### Ruby: Get Encoding names and aliases

Source: https://docs.ruby-lang.org/en/master/encodings_rdoc

Demonstrates how to get all names associated with an Encoding object, including its primary name and any aliases, using the `#names` method.

```ruby
Encoding::ASCII_8BIT.names
# => ["ASCII-8BIT", "BINARY"]
Encoding::WINDOWS_31J.names
#=> ["Windows-31J", "CP932", "csWindows31J", "SJIS", "PCK"]
```

--------------------------------

### Display help for test/ suite options

Source: https://docs.ruby-lang.org/en/master/contributing/testing_ruby_md

Shows the available help information for the TESTS variable, which controls the execution of the 'test/' suite. This is useful for understanding the options available.

```make
make test-all TESTS=--help
```

--------------------------------

### Execute 'echo' with arguments using Open3.popen2e

Source: https://docs.ruby-lang.org/en/master/Open3

Demonstrates passing arguments to an executable via `Open3.popen2e`. This example shows how to pass multiple arguments to the 'echo' command.

```ruby
Open3.popen2e('echo', 'C #') { |i, o, t| o.gets }
```

```ruby
Open3.popen2e('echo', 'hello', 'world') { |i, o, t| o.gets }
```

--------------------------------

### Create RubyGems Package with Gem::PackageTask

Source: https://docs.ruby-lang.org/en/master/Gem/PackageTask

Demonstrates how to create a RubyGems package using Gem::PackageTask. It requires the 'rubygems' and 'rubygems/package_task' libraries. The example defines a Gem::Specification and then uses Gem::PackageTask to configure packaging options like including zip and tar formats.

```ruby
require 'rubygems'
require 'rubygems/package_task'

spec = Gem::Specification.new do |s|
  s.summary = "Ruby based make-like utility."
  s.name = 'rake'
  s.version = PKG_VERSION
  s.requirements << 'none'
  s.files = PKG_FILES
  s.description = <<-EOF
Rake is a Make-like program implemented in Ruby. Tasks
and dependencies are specified in standard Ruby syntax.
  EOF
end

Gem::PackageTask.new(spec) do |pkg|
  pkg.need_zip = true
  pkg.need_tar = true
end
```

--------------------------------

### Execute Shell Command with Arguments (Ruby)

Source: https://docs.ruby-lang.org/en/master/Process

Demonstrates executing a shell command with arguments and redirection using `system`. This is a basic way to run external commands and capture their success status.

```Ruby
system('echo', '<', 'C*', '|', '$SHELL', '>')   # => true
```

--------------------------------

### Ruby: Check if a gem specification is installable on the current platform

Source: https://docs.ruby-lang.org/en/master/Gem/Resolver/InstalledSpecification

The `installable_platform?` method checks if the gem represented by `InstalledSpecification` can be installed on the current system. It includes backward compatibility logic for specific file sources.

```ruby
# File lib/rubygems/resolver/installed_specification.rb, line 25
def installable_platform?
  # BACKCOMPAT If the file is coming out of a specified file, then we
  # ignore the platform. This code can be removed in RG 3.0.
  return true if @source.is_a? Gem::Source::SpecificFile

  super
end
```

--------------------------------

### OpenStruct to JSON String Example (Ruby)

Source: https://docs.ruby-lang.org/en/master/OpenStruct

This example shows how to use the `to_json` method to directly obtain a JSON string from an OpenStruct object. It requires the 'json/add/ostruct' library to be included.

```Ruby
require 'json/add/ostruct'
puts OpenStruct.new('name' => 'Rowdy', :age => nil).to_json

# Output:
# {"json_class":"OpenStruct","t":{'name':'Rowdy',"age":null}}
```

--------------------------------

### Generate Bash Prolog Script (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Generates a bash script prologue for executable gems. It includes logic to locate the correct Ruby interpreter based on the script's location.

```Ruby
def bash_prolog_script
  if load_relative_enabled?
    <<~EOS
      #!/bin/sh
      # -*- ruby -*- 
      _=_\
      =begin
      bindir="${0%/*}"
      ruby="$bindir/#{ruby_install_name}"
      if [ ! -f "$ruby" ]; then
        ruby="#{ruby_install_name}"
      fi
      exec "$ruby" "-x" "$0" "$@"
      =end
    EOS
  else
    ""
  end
end
```

--------------------------------

### Set Net::HTTP Proxy with Hostname and Port

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Demonstrates how to initialize a Net::HTTP object with explicit proxy host, port, username, and password.

```ruby
http = Net::HTTP.new(hostname, nil, 'proxy.example', 8000, 'pname', 'ppass')
```

--------------------------------

### Ruby Integer Conversion Example

Source: https://docs.ruby-lang.org/en/master/implicit_conversion_rdoc

Shows a user-defined class that is Integer-convertible via its `to_int` method. The example demonstrates `Array.new` successfully using this method to determine the array size.

```Ruby
class IntegerConvertible
  def to_int
    3
  end
end
a = Array.new(IntegerConvertible.new).size
a # => 3

```

--------------------------------

### Ruby String delete_prefix Method Examples

Source: https://docs.ruby-lang.org/en/master/String

Illustrates how to remove a specified prefix from a Ruby string, returning a new string without the prefix. Includes examples with different languages.

```ruby
'oof'.delete_prefix('o')
'oof'.delete_prefix('oo')
'oof'.delete_prefix('oof')
'oof'.delete_prefix('x')
'тест'.delete_prefix('те')
'こんにちは'.delete_prefix('こん')
```

--------------------------------

### ObjectSpace::WeakKeyMap Usage Example

Source: https://docs.ruby-lang.org/en/master/ObjectSpace/WeakKeyMap

Demonstrates the creation and behavior of ObjectSpace::WeakKeyMap, showing how keys and values are handled during garbage collection. Keys are compared by value.

```ruby
map = ObjectSpace::WeakKeyMap.new
val = Time.new(2023, 12, 7)
key = "name"
map[key] = val

# Value is fetched by equality: the instance of string "name" is
# different here, but it is equal to the key
map["name"] #=> 2023-12-07 00:00:00 +0200

val = nil
GC.start
# There are no more references to `val`, yet the pair isn't
# garbage-collected.
map["name"] #=> 2023-12-07 00:00:00 +0200

key = nil
GC.start
# There are no more references to `key`, key and value are
# garbage-collected.
map["name"] #=> nil
```

--------------------------------

### Get Scheduling Priority with Process.getpriority

Source: https://docs.ruby-lang.org/en/master/Process

Shows how to get the scheduling priority of a process, process group, or user using `Process.getpriority`. The `kind` argument specifies the target type, and `id` specifies the identifier.

```Ruby
Process.getpriority(Process::PRIO_USER, 0)    # => 19
Process.getpriority(Process::PRIO_PROCESS, 0) # => 19
```

--------------------------------

### Ruby: Start tracing object allocations with ObjectSpace

Source: https://docs.ruby-lang.org/en/master/ObjectSpace

This method starts tracing object allocations from the `ObjectSpace` extension module. It uses `rb_ensure` to yield a block and then stops tracing. This feature can significantly impact performance and memory usage.

```ruby
require 'objspace'

class C
  include ObjectSpace

  def foo
    trace_object_allocations do
      obj = Object.new
      p "#{allocation_sourcefile(obj)}:#{allocation_sourceline(obj)}"
    end
  end
end

C.new.foo #=> "objtrace.rb:8"
```

--------------------------------

### Create and Use UNIX Sockets for Communication in Ruby

Source: https://docs.ruby-lang.org/en/master/UNIXSocket

This example demonstrates creating a UNIX server and client to communicate using `UNIXSocket`. It shows how to send and receive standard output between the client and server.

```ruby
UNIXServer.open("/tmp/sock") {|serv|
  UNIXSocket.open("/tmp/sock") {|c|
    s = serv.accept

    c.send_io STDOUT
    stdout = s.recv_io

    p STDOUT.fileno #=> 1
    p stdout.fileno #=> 7

    stdout.puts "hello" # outputs "hello\n" to standard output.
  }
}

```

--------------------------------

### Ruby IO#gets - With Separator and Limit

Source: https://docs.ruby-lang.org/en/master/IO

Explains that `gets` can be used with both a separator and a limit argument, combining the functionalities of custom separators and byte limits.

```ruby
f = File.open('t.txt')
```

--------------------------------

### Get Session Callback (Ruby)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/SSL/SSLSocket

Retrieves the session get callback from the SSL context. This Ruby method is used for managing SSL session retrieval.

```ruby
# File ext/openssl/lib/openssl/ssl.rb, line 468
def session_get_cb
  @context.session_get_cb
end
```

--------------------------------

### Ruby Method Entry Probe Example

Source: https://docs.ruby-lang.org/en/master/dtrace_probes_rdoc

An example of a DTrace probe definition for Ruby, specifically for tracking method entry events. It shows the provider name, blank module and function, the probe name 'method-entry', and its expected arguments.

```dtrace
ruby:::method-entry(class name, method name, file name, line number)
```

--------------------------------

### Run Program in gets Loop (-n)

Source: https://docs.ruby-lang.org/en/master/ruby/options_md

The -n option executes the provided Ruby code within a `Kernel#gets` loop, processing the input line by line. Each line read is assigned to the global variable `$_`.

```ruby
while gets
  # Your Ruby code.
end

```

```shell
$ ruby -n -e 'puts $_' desiderata.txt
Go placidly amid the noise and the haste,
and remember what peace there may be in silence.
As far as possible, without surrender,
be on good terms with all persons.

```

--------------------------------

### Remove Old RubyGems Library Files

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SetupCommand

Removes outdated library files and directories for RubyGems and Bundler. It compares existing files with expected files and removes any that are no longer necessary. It specifically handles the 'gauntlet_rubygems.rb' file and excludes files starting with 'defaults'.

```ruby
def remove_old_lib_files(lib_dir)
  lib_dirs = { File.join(lib_dir, "rubygems") => "lib/rubygems" }
  lib_dirs[File.join(lib_dir, "bundler")] = "bundler/lib/bundler"
  lib_dirs.each do |old_lib_dir, new_lib_dir|
    lib_files = files_in(new_lib_dir)

    old_lib_files = files_in(old_lib_dir)

    to_remove = old_lib_files - lib_files

    gauntlet_rubygems = File.join(lib_dir, "gauntlet_rubygems.rb")
    to_remove << gauntlet_rubygems if File.exist? gauntlet_rubygems

    to_remove.delete_if do |file|
      file.start_with? "defaults"
    end

    remove_file_list(to_remove, old_lib_dir)
  end
end
```

--------------------------------

### Type Coercion with OptionParser (Time Example)

Source: https://docs.ruby-lang.org/en/master/OptionParser

Shows how OptionParser can automatically coerce command-line arguments into specific data types, using `Time` as an example. It requires the `optparse/time` library and demonstrates successful parsing and invalid argument handling.

```ruby
require 'optparse'
require 'optparse/time'
OptionParser.new do |parser|
  parser.on("-t", "--time [TIME]", Time, "Begin execution at given time") do |time|
    p time
  end
end.parse!


```

--------------------------------

### begin_addr

Source: https://docs.ruby-lang.org/en/master/IPAddr

Calculates the starting IP address of the network.

```APIDOC
## begin_addr

### Description
Calculates the starting IP address of the network.

### Method
GET

### Endpoint
`/websites/ruby-lang_en_master/lib/ipaddr.rb#L547`

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **start_ip_address** (String) - The starting IP address of the network.

#### Response Example
```json
{
  "start_ip_address": "192.168.1.0"
}
```
```

--------------------------------

### Instance Method: Get Default UI (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/DefaultUserInteraction

An instance method that calls the class method `Gem::DefaultUserInteraction.ui` to get the default user interface.

```ruby
def ui
  Gem::DefaultUserInteraction.ui
end
```

--------------------------------

### Initialize RubyGems SourcesCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SourcesCommand

Initializes the SourcesCommand with options for managing gem sources. It requires the 'fileutils' library and sets up command-line arguments for adding, prepending, appending, listing, removing, clearing sources, and updating the cache.

```ruby
def initialize
  require "fileutils"

  super "sources",
        "Manage the sources and cache file RubyGems uses to search for gems"

  add_option "-a", "--add SOURCE_URI", "Add source" do |value, options|
    options[:add] = value
  end

  add_option "--append SOURCE_URI", "Append source (can be used multiple times)" do |value, options|
    options[:append] = value
  end

  add_option "-p", "--prepend SOURCE_URI", "Prepend source (can be used multiple times)" do |value, options|
    options[:prepend] = value
  end

  add_option "-l", "--list", "List sources" do |value, options|
    options[:list] = value
  end

  add_option "-r", "--remove SOURCE_URI", "Remove source" do |value, options|
    options[:remove] = value
  end

  add_option "-c", "--clear-all", "Remove all sources (clear the cache)" do |value, options|
    options[:clear_all] = value
  end

  add_option "-u", "--update", "Update source cache" do |value, options|
    options[:update] = value
  end

  add_option "-f", "--[no-]force", "Do not show any confirmation prompts and behave as if 'yes' was always answered" do |value, options|
    options[:force] = value
  end

  add_proxy_option
end
```

--------------------------------

### TSort Example: Make-like Build Tool

Source: https://docs.ruby-lang.org/en/master/TSort

Implements a simple 'make' like tool using TSort for dependency management. It defines rules for file dependencies and a `build` method that utilizes `each_strongly_connected_component_from` to execute commands based on file modification times and dependencies.

```ruby
require 'tsort'

class Make
  def initialize
    @dep = {}
    @dep.default = []
  end

  def rule(outputs, inputs=[], &block)
    triple = [outputs, inputs, block]
    outputs.each {|f| @dep[f] = [triple]}
    @dep[triple] = inputs
  end

  def build(target)
    each_strongly_connected_component_from(target) {|ns|
      if ns.length != 1
        fs = ns.delete_if {|n| Array === n}
        raise TSort::Cyclic.new("cyclic dependencies: #{fs.join ', '}")
      end
      n = ns.first
      if Array === n
        outputs, inputs, block = n
        inputs_time = inputs.map {|f| File.mtime f}.max
        begin
          outputs_time = outputs.map {|f| File.mtime f}.min
        rescue Errno::ENOENT
          outputs_time = nil
        end
        if outputs_time == nil ||
           inputs_time != nil && outputs_time <= inputs_time
          sleep 1 if inputs_time != nil && inputs_time.to_i == Time.now.to_i
          block.call
        end
      end
    }
  end

  def tsort_each_child(node, &block)
    @dep[node].each(&block)
  end
  include TSort
end

def command(arg)
  print arg, "\n"
  system arg
end

m = Make.new
m.rule(%w[t1]) { command 'date > t1' }
m.rule(%w[t2]) { command 'date > t2' }
m.rule(%w[t3]) { command 'date > t3' }
m.rule(%w[t4], %w[t1 t3]) { command 'cat t1 t3 > t4' }
m.rule(%w[t5], %w[t4 t2]) { command 'cat t4 t2 > t5' }
m.build('t5')


```

--------------------------------

### Initialize RDocCommand in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/RdocCommand

Initializes the RDocCommand with various options for generating RDoc and RI documentation for installed gems. It allows specifying whether to include RDoc, RI, overwrite existing files, or process all installed gems.

```ruby
def initialize
  super "rdoc", "Generates RDoc for pre-installed gems",
        version: Gem::Requirement.default, include_rdoc: false, include_ri: true, overwrite: false

  add_option("--all",
             "Generate RDoc/RI documentation for all",
             "installed gems") do |value, options|
    options[:all] = value
  end

  add_option("--[no-]rdoc",
             "Generate RDoc HTML") do |value, options|
    options[:include_rdoc] = value
  end

  add_option("--[no-]ri",
             "Generate RI data") do |value, options|
    options[:include_ri] = value
  end

  add_option("--[no-]overwrite",
             "Overwrite installed documents") do |value, options|
    options[:overwrite] = value
  end

  add_version_option
end
```

--------------------------------

### Set Install/Update Default Documentation to RI

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Returns a string representing the default option for generating RI documentation during gem installation or updates. This is a simple string return function.

```ruby
# File lib/rubygems/install_update_options.rb, line 201
def install_update_defaults_str
  "--document=ri"
end
```

--------------------------------

### Creating HTTP Request Objects in Ruby

Source: https://docs.ruby-lang.org/en/master/Net/HTTPRequest

Demonstrates how to create instances of Net::HTTP request objects using a URI or hostname. It shows the creation of GET requests and mentions other common HTTP methods like HEAD, POST, and PUT.

```ruby
require 'net/http'
uri = URI('https://jsonplaceholder.typicode.com/')
req = Net::HTTP::Get.new(uri)          # => #<Net::HTTP::Get GET>
req = Net::HTTP::Get.new(uri.hostname) # => #<Net::HTTP::Get GET>

req = Net::HTTP::Head.new(uri) # => #<Net::HTTP::Head HEAD>
req = Net::HTTP::Post.new(uri) # => #<Net::HTTP::Post POST>
req = Net::HTTP::Put.new(uri)  # => #<Net::HTTP::Put PUT>
```

--------------------------------

### Ruby IO#gets - Default Behavior

Source: https://docs.ruby-lang.org/en/master/IO

Demonstrates the default behavior of `gets` when no arguments are provided. It reads the next line based on the default line separator ($/) and assigns it to the global variable $_.

```ruby
f = File.open('t.txt')
f.gets # => "First line\n"
$_     # => "First line\n"
f.gets # => "\n"
f.gets # => "Fourth line\n"
f.gets # => "Fifth line\n"
f.gets # => nil
f.close
```

--------------------------------

### Range#begin

Source: https://docs.ruby-lang.org/en/master/Range

Retrieves the starting element of a Range.

```APIDOC
## Range#begin

### Description
Returns the object that defines the beginning of the Range.

### Method
`Range#begin`

### Endpoint
N/A (Instance Method)

### Parameters
None

### Request Example
```ruby
(1..4).begin # => 1
(..2).begin  # => nil
```

### Response Example
```ruby
# Returns the starting element of the range
1
```

### Related
`Range#first`, `Range#end`
```

--------------------------------

### Spawn Process with Path Containing Spaces (Ruby)

Source: https://docs.ruby-lang.org/en/master/Process

Illustrates how to use `spawn` with a path that includes spaces. It shows the correct way to pass such paths as a 2-element array to `spawn` to avoid errors.

```Ruby
path = '/Applications/Google Chrome.app/Contents/MacOS/Google Chrome'
spawn(path) # Raises Errno::ENOENT; No such file or directory - /Applications/Google
spawn([path] * 2)
```

--------------------------------

### Ruby Array Slicing - Negative Range Start and End

Source: https://docs.ruby-lang.org/en/master/Array

Demonstrates how negative values in a range are interpreted to calculate start and end indices from the end of the array.

```ruby
a = [:foo, 'bar', 2]
a[0..-1] # => [:foo, "bar", 2]
a[0..-2] # => [:foo, "bar"]
a[0..-3] # => [:foo]
a[-1..2] # => [2]
a[-2..2] # => ["bar", 2]
a[-3..2] # => [:foo, "bar", 2]
```

--------------------------------

### Ruby: GET Request Returning Response Object

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Illustrates how to obtain the full Net::HTTPResponse object for a GET request. This allows access to status codes, headers, and the response body.

```ruby
# Return response as Net::HTTPResponse object.
Net::HTTP.get_response(hostname, path)
Net::HTTP.get_response(uri)
```

--------------------------------

### Gem::Package#build instance method

Source: https://docs.ruby-lang.org/en/master/Gem/Package

Builds the gem package based on the currently set `Gem::Specification`. It handles validation, signing, and writing the final .gem file.

```ruby
# File lib/rubygems/package.rb, line 293
  def build(skip_validation = false, strict_validation = false)
    raise ArgumentError, "skip_validation = true and strict_validation = true are incompatible" if skip_validation && strict_validation

    Gem.load_yaml

    @spec.validate true, strict_validation unless skip_validation

    setup_signer(
      signer_options: {
        expiration_length_days: Gem.configuration.cert_expiration_length_days,
      }
    )

    @gem.with_write_io do |gem_io|
      Gem::Package::TarWriter.new gem_io do |gem|
        add_metadata gem
        add_contents gem
        add_checksums gem
      end
    end

    say <<-EOM
  Successfully built RubyGem
  Name: #{@spec.name}
  Version: #{@spec.version}
  File: #{File.basename @gem.path}
EOM
  ensure
    @signer = nil
  end

```

--------------------------------

### Ruby Example: Handling Unix Domain Socket Rights

Source: https://docs.ruby-lang.org/en/master/Socket/AncillaryData

This Ruby example demonstrates sending and receiving UNIX domain socket rights using `recvmsg` with the `:scm_rights=>true` option. It shows how to create a pair of UNIX sockets, send file descriptors (like STDIN) along with a message, and then extract these file descriptors from the received ancillary data.

```ruby
# recvmsg needs :scm_rights=>true for unix_rights
s1, s2 = UNIXSocket.pair
p s1                                         #=> #<UNIXSocket:fd 3>
s1.sendmsg "stdin and a socket", 0, nil, Socket::AncillaryData.unix_rights(STDIN, s1)
_, _, _, ctl = s2.recvmsg(:scm_rights=>true)
p ctl                                        #=> #<Socket::AncillaryData: UNIX SOCKET RIGHTS 6 7>
p ctl.unix_rights                            #=> [#<IO:fd 6>, #<Socket:fd 7>]
p File.identical?(STDIN, ctl.unix_rights[0]) #=> true
p File.identical?(s1, ctl.unix_rights[1])    #=> true

# If :scm_rights=>true is not given, unix_rights returns nil
s1, s2 = UNIXSocket.pair
s1.sendmsg "stdin and a socket", 0, nil, Socket::AncillaryData.unix_rights(STDIN, s1)
_, _, _, ctl = s2.recvmsg
p ctl #=> #<Socket::AncillaryData: UNIX SOCKET RIGHTS 6 7>
p ctl.unix_rights #=> nil
```

--------------------------------

### Constant Reference Example

Source: https://docs.ruby-lang.org/en/master/Prism/ConstantReadNode

Illustrates a basic constant reference in Ruby.

```ruby
Foo
^^^
```

--------------------------------

### Ruby Hash Common Uses Examples

Source: https://docs.ruby-lang.org/en/master/Hash

Illustrates common applications of Ruby Hashes, such as naming objects, providing named arguments to methods, and initializing objects.

```Ruby
person = {name: 'Matz', language: 'Ruby'}
person # => {name: "Matz", language: "Ruby"}
```

```Ruby
def some_method(hash)
  p hash
end
some_method({foo: 0, bar: 1, baz: 2}) # => {foo: 0, bar: 1, baz: 2}
```

```Ruby
def some_method(hash)
  p hash
end
some_method(foo: 0, bar: 1, baz: 2) # => {foo: 0, bar: 1, baz: 2}
```

```Ruby
class Dev
  attr_accessor :name, :language
  def initialize(hash)
    self.name = hash[:name]
    self.language = hash[:language]
  end
end
matz = Dev.new(name: 'Matz', language: 'Ruby')
matz # => #<Dev: @name="Matz", @language="Ruby">
```

--------------------------------

### Socket Options LINGER

Source: https://docs.ruby-lang.org/en/master/BasicSocket

Demonstrates how to get and set socket linger options.

```APIDOC
## Socket Options LINGER

### Description
Retrieves and sets the linger options for a socket.

### Method
GET/SET (Implicit)

### Endpoint
N/A (Internal method)

### Parameters
None

### Request Example
```ruby
optval =  sock.getsockopt(Socket::SOL_SOCKET, Socket::SO_LINGER)
onoff, linger = optval.unpack "ii"
onoff = onoff == 0 ? false : true
```

### Response
#### Success Response (200)
- **onoff** (Boolean) - Indicates if linger is on.
- **linger** (Integer) - The linger time in seconds.

#### Response Example
```ruby
# Example output structure after unpack
# onoff: true, linger: 60
```
```

--------------------------------

### WebauthnPoller Example - RubyGems

Source: https://docs.ruby-lang.org/en/master/Gem/GemcutterUtilities

Example usage of the WebauthnPoller to poll for an OTP. It initiates a polling thread with provided options, host, and verification URL, then joins the thread to retrieve the OTP or error.

```Ruby
thread = Gem::WebauthnPoller.poll_thread(
  {},
  "RubyGems.org",
  "https://rubygems.org/api/v1/webauthn_verification/odow34b93t6aPCdY",
  { email: "email@example.com", password: "password" }
)
thread.join
otp = thread[:otp]
error = thread[:error]
```

--------------------------------

### Ruby: Get a list of all encoding names and aliases

Source: https://docs.ruby-lang.org/en/master/encodings_rdoc

Shows how to get a flat array of all encoding names and their aliases using `Encoding.name_list`. This is useful for seeing all possible identifiers for encodings.

```ruby
Encoding.name_list.size # => 175
Encoding.name_list.take(3)
# => ["ASCII-8BIT", "UTF-8", "US-ASCII"]
```

--------------------------------

### Generate Binary Script for Gem Executables in Ruby

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Creates executable scripts for gem applications, handling existing files and setting appropriate permissions. It also generates Windows-specific scripts.

```ruby
def generate_bin_script(filename, bindir)
  bin_script_path = File.join bindir, formatted_program_filename(filename)

  Gem.open_file_with_lock(bin_script_path) do
    require "fileutils"
    FileUtils.rm_f bin_script_path # prior install may have been --no-wrappers

    File.open(bin_script_path, "wb", 0o755) do |file|
      file.write app_script_text(filename)
      file.chmod(options[:prog_mode] || 0o755)
    end
  end

  verbose bin_script_path

  generate_windows_script filename, bindir
end
```

--------------------------------

### Initialize CodeLine Instance

Source: https://docs.ruby-lang.org/en/master/SyntaxSuggest/CodeLine

The initialize method sets up a CodeLine object with its line content, index, and lexical data. It calculates indentation and determines if the line is empty. The original line content is preserved even if the line is marked as invisible, which is useful for debugging and displaying context.

```ruby
# File lib/syntax_suggest/code_line.rb, line 42
def initialize(line:, index:, lex:)
  @lex = lex
  @line = line
  @index = index
  @original = line
  @line_number = @index + 1
  strip_line = line.dup
  strip_line.lstrip!

  @indent = if (@empty = strip_line.empty?)
    line.length - 1 # Newline removed from strip_line is not "whitespace"
  else
    line.length - strip_line.length
  end

  set_kw_end
end
```

--------------------------------

### Get Process ID (Ruby)

Source: https://docs.ruby-lang.org/en/master/Process

Returns the process ID (PID) of the current process. This is the standard Ruby method to get the current process's identifier.

```ruby
Process.pid # => 15668
```

--------------------------------

### Ruby: Get Do Keyword Location

Source: https://docs.ruby-lang.org/en/master/Prism/ForNode

The `do_keyword` method returns the string slice of the `do` keyword's location. It relies on `do_keyword_loc` to get the actual location object.

```ruby
def do_keyword
  do_keyword_loc&.slice
end
```

--------------------------------

### Create Directories with FileUtils.mkdir

Source: https://docs.ruby-lang.org/en/master/FileUtils

Creates a single directory. Handles options like `mode`, `noop`, and `verbose`.

```ruby
def mkdir (list, mode: nil, noop: nil, verbose: nil)
  # Implementation details omitted for brevity, but would mirror mkdir_p logic for single dirs
end
```

--------------------------------

### Ruby: Get Array of Products from Enumerator::Product

Source: https://docs.ruby-lang.org/en/master/Enumerator/Product

Demonstrates how to use Enumerator::Product to generate a Cartesian product and then convert it into an array using `to_a`. It also shows how to get the size of the product.

```ruby
e = Enumerator::Product.new(1..3, [4, 5])
e.to_a #=> [[1, 4], [1, 5], [2, 4], [2, 5], [3, 4], [3, 5]]
e.size #=> 6

```

--------------------------------

### Ruby Net::HTTP GET Request

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Sends a GET request to the server, returning an instance of Net::HTTPResponse. Can optionally take a block to process the response body.

```ruby
def get(path, initheader = nil, dest = nil, &block)
  res = nil

  request(Get.new(path, initheader)) {
    |r|
    r.read_body dest, &block
    res = r
  }
  res
end
```

```ruby
http = Net::HTTP.new(hostname)
http.get('/todos/1') do |res|
  p res
end
```

```ruby
http.get('/')
```

--------------------------------

### Start Document Emission (C)

Source: https://docs.ruby-lang.org/en/master/Psych/Emitter

Initiates a YAML document emission process. It takes version, tags, and an implicit flag as arguments. This function is crucial for starting a new YAML document within a stream.

```c
static VALUE start_document(VALUE self, VALUE version, VALUE tags, VALUE imp) {
    struct start_document_data data = {
        .self = self,
        .version = version,
        .tags = tags,
        .imp = imp,

        .head = NULL,
    };

    return rb_ensure(start_document_try, (VALUE)&data, start_document_ensure, (VALUE)&data);
}
```

--------------------------------

### Execute 'echo "Foo"' using Open3.popen2e

Source: https://docs.ruby-lang.org/en/master/Open3

Demonstrates executing a simple command 'echo "Foo"' using `Open3.popen2e` and capturing its output. It shows how to get the output from the child process.

```ruby
Open3.popen2e('echo "Foo"') { |i, o, t| o.gets }
```

--------------------------------

### Build Ruby with Mingw (bash)

Source: https://docs.ruby-lang.org/en/master/windows_md

Instructions for building Ruby using Mingw with UCRT within an MSYS2 bash shell. It includes installing RIDK, enabling UCRT64, and using pacman for package management.

```shell
ridk install
ridk enable ucrt64
bash

pacman -S --needed $MINGW_PACKAGE_PREFIX-openssl $MINGW_PACKAGE_PREFIX-libyaml $MINGW_PACKAGE_PREFIX-libffi

mkdir /c/work/ruby
cd /c/work/ruby

git clone https://github.com/ruby/ruby src

./src/autogen.sh
cd build
../src/configure -C --disable-install-doc
make
```

--------------------------------

### Ruby gets function implementation

Source: https://docs.ruby-lang.org/en/master/Kernel

C implementation of the Ruby `gets` function, responsible for reading input lines. It handles argument parsing and delegates to internal functions based on the context.

```c
static VALUE
rb_f_gets(int argc, VALUE *argv, VALUE recv)
{
    if (recv == argf) {
        return argf_gets(argc, argv, argf);
    }
    return forward(argf, idGets, argc, argv);
}
```

--------------------------------

### GET Request with Response Body

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Sends a GET request and returns the HTTP response body as a string. Can be used with host/path or URI objects.

```APIDOC
## GET / HTTP/1.1

### Description
Sends a GET request and returns the HTTP response body as a string.

### Method
GET

### Endpoint
/

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```ruby
hostname = 'jsonplaceholder.typicode.com'
path = '/todos/1'
puts Net::HTTP.get(hostname, path)
```

```ruby
uri = URI('https://jsonplaceholder.typicode.com/todos/1')
headers = {'Content-type' => 'application/json; charset=UTF-8'}
Net::HTTP.get(uri, headers)
```

### Response
#### Success Response (200)
- **body** (String) - The response body content.

#### Response Example
```json
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```
```

--------------------------------

### Install Signed Gem with High Security Policy

Source: https://docs.ruby-lang.org/en/master/Gem/Security

Installs a RubyGems package using the 'HighSecurity' policy, which enforces trust verification. This command will succeed if the package's signing certificate is trusted.

```shell
$ gem install -P HighSecurity your-gem-1.0.gem
```

--------------------------------

### Initialize data class instances with keyword arguments

Source: https://docs.ruby-lang.org/en/master/Data

Shows the creation of data class instances using keyword arguments, which is the primary and safest initialization method.

```ruby
Measure = Data.define(:amount, :unit)
Measure.new(amount: 1, unit: 'km')
#=> #<data Measure amount=1, unit="km">
```

--------------------------------

### Get X509 Request Attributes (C)

Source: https://docs.ruby-lang.org/en/master/OpenSSL/X509/Request

Retrieves all attributes from an X509::Request object. It gets the attribute count, iterates through them, and converts each attribute to a Ruby object.

```c
static VALUE
ossl_x509req_get_attributes(VALUE self)
{
    X509_REQ *req;
    int count, i;
    X509_ATTRIBUTE *attr;
    VALUE ary;

    GetX509Req(self, req);

    count = X509_REQ_get_attr_count(req);
    if (count < 0) {
        OSSL_Debug("count < 0???");
        return rb_ary_new();
    }
    ary = rb_ary_new2(count);
    for (i=0; i<count; i++) {
        attr = X509_REQ_get_attr(req, i);
        rb_ary_push(ary, ossl_x509attr_new(attr));
    }

    return ary;
}
```

--------------------------------

### Start Coverage Measurement (Ruby)

Source: https://docs.ruby-lang.org/en/master/Coverage

Enables coverage measurement, equivalent to calling Coverage.setup and Coverage.resume. Supports various modes including lines, branches, methods, and eval.

```ruby
static VALUE
rb_coverage_start(int argc, VALUE *argv, VALUE klass)
{
    rb_coverage_setup(argc, argv, klass);
    rb_coverage_resume(klass);
    return Qnil;
}
```

--------------------------------

### Install Gems in User's Home Directory

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Installs gems into the user's home directory instead of the default GEM_HOME. This is useful for managing gems without requiring administrator privileges.

```ruby
add_option(:'Install/Update', "--[no-]user-install",
             "Install in user's home directory instead",
             "of GEM_HOME.") do |value, options|
    options[:user_install] = value
  end
```

--------------------------------

### Determine Gems to Cleanup (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/CleanupCommand

Partitions candidate gems into default gems and those to be cleaned up. It selects gems whose versions differ from the primary installed version and are located in the target installation directory.

```ruby
# File lib/rubygems/commands/cleanup_command.rb, line 122
def get_gems_to_cleanup
  gems_to_cleanup = @candidate_gems.select do |spec|
    @primary_gems[spec.name].version != spec.version
  end

  default_gems, gems_to_cleanup = gems_to_cleanup.partition(&:default_gem?)

  uninstall_from = options[:user_install] ? Gem.user_dir : Gem.dir

  gems_to_cleanup = gems_to_cleanup.select do |spec|
    spec.base_dir == uninstall_from
  end

  @default_gems += default_gems
  @default_gems.uniq!
  @gems_to_cleanup = gems_to_cleanup.uniq
end
```

--------------------------------

### Omit Gem Groups During Installation

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Specifies groups of gems to omit when installing from a gem dependencies file. The groups are provided as a comma-separated array and converted to symbols.

```ruby
add_option(:'Install/Update', "--without GROUPS", Array,
             "Omit the named groups (comma separated)",
             "when installing from a gem dependencies",
             "file") do |v,_o|
    options[:without_groups].concat v.map(&:intern)
  end
```

--------------------------------

### Demonstrate Ruby IO#seek with :SET

Source: https://docs.ruby-lang.org/en/master/IO

This Ruby snippet demonstrates using `IO#seek` with the `:SET` (set) `whence` option. It opens a file, checks its position, seeks to position 20, checks the new position, seeks to position 40, and checks the final position. This illustrates absolute seeking to a specific position from the beginning of the file.

```ruby
f = File.open('t.txt')
f.tell            # => 0
f.seek(20, :SET) # => 0
f.tell           # => 20
f.seek(40, :SET) # => 0
f.tell           # => 40
f.close
```

--------------------------------

### Argument Handling: command_line

Source: https://docs.ruby-lang.org/en/master/Open3

Explains how the `command_line` argument is handled, including conditions for shell execution and meta-character usage.

```APIDOC
## Argument Handling: `command_line`

### Description
Details the usage of the `command_line` argument for `Open3.popen2e`, specifying when it's passed to a shell and when it should include shell reserved words or meta-characters.

### Method
`Open3.popen2e(command_line)`

### Parameters
#### Path Parameters
* **command_line** (String) - Required - The command line string to be executed. If it begins with a shell reserved word, a special built-in, or contains meta-characters, it will be passed to the shell.

#### Query Parameters
None

#### Request Body
None

### Request Example
```ruby
Open3.popen2e('echo "Hello"') { |i, o_e, t| puts o_e.gets }
Open3.popen2e('if true; then echo "Bar"; fi') { |i, o_e, t| puts o_e.gets }
```

### Response
#### Success Response (Output)
The standard output of the command.

#### Response Example
```
Hello

Bar

```
```

--------------------------------

### Conservative Gem Installation

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Installs gems conservatively, meaning it avoids upgrading gems that already meet the version requirement. It also sets 'minimal_deps' to true.

```ruby
add_option(:'Install/Update', "--conservative",
              "Don't attempt to upgrade gems already",
              "meeting version requirement") do |_value, options|
    options[:conservative] = true
    options[:minimal_deps] = true
  end
```

--------------------------------

### Example of Sending File Descriptor with UNIXSocket in Ruby

Source: https://docs.ruby-lang.org/en/master/UNIXSocket

This Ruby example demonstrates sending a file descriptor (specifically standard output) from one UNIX socket to another using `send_io` and `recv_io`. It verifies the transfer by printing the file descriptor numbers and writing to the received IO object.

```ruby
s1, s2 = UNIXSocket.pair

s1.send_io STDOUT
stdout = s2.recv_io

p STDOUT.fileno #=> 1
p stdout.fileno #=> 6

stdout.puts "hello" # outputs "hello\n" to standard output.


```

--------------------------------

### Open3.popen3 with Multiple Arguments

Source: https://docs.ruby-lang.org/en/master/Open3

Shows how to pass multiple arguments to an executable using Open3.popen3. The examples demonstrate passing arguments to 'echo'.

```ruby
Open3.popen3('echo', 'C #') { |i, o, e, t| o.gets }
# => "C #\n"
Open3.popen3('echo', 'hello', 'world') { |i, o, e, t| o.gets }
# => "hello world\n"

```

--------------------------------

### Initialize RubyGems SigninCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/SigninCommand

Initializes the SigninCommand for RubyGems, setting default options and allowing for custom host specification. It also adds an option for One-Time Password (OTP).

```ruby
def initialize
  super "signin", "Sign in to any gemcutter-compatible host. " \
        "It defaults to https://rubygems.org"

  add_option("--host HOST", "Push to another gemcutter-compatible host") do |value, options|
    options[:host] = value
  end

  add_otp_option
end
```

--------------------------------

### Format Executable Names Based on Ruby Version

Source: https://docs.ruby-lang.org/en/master/Gem/InstallUpdateOptions

Determines whether installed executable names should match the Ruby version (e.g., appending '18' for ruby18). This helps differentiate executables from different Ruby installations.

```ruby
add_option(:'Install/Update', "--[no-]format-executable",
             "Make installed executable names match Ruby.",
             "If Ruby is ruby18, foo_exec will be",
             "foo_exec18") do |value, options|
    options[:format_executable] = value
  end
```

--------------------------------

### Ruby Enumerator peek() Example

Source: https://docs.ruby-lang.org/en/master/Enumerator

Demonstrates the `peek` method, which returns the next element without advancing the enumerator's position. The example shows how multiple calls to `peek` return the same element until `next` is called.

```ruby
a = [1,2,3]
e = a.to_enum
p e.next   #=> 1
p e.peek   #=> 2
p e.peek   #=> 2
p e.peek   #=> 2
p e.next   #=> 2
p e.next   #=> 3
p e.peek   #raises StopIteration
```

--------------------------------

### Finish HTTP Session

Source: https://docs.ruby-lang.org/en/master/Net/HTTP

Closes the active HTTP session and the underlying TCP connection. This method must be called after starting a session if it was not started with a block.

```ruby
def finish
  raise IOError, 'HTTP session not yet started' unless started?
  do_finish
end
```

```ruby
http = Net::HTTP.new(hostname)
http.start
http.started? # => true
http.finish   # => nil
http.started? # => false
```

--------------------------------

### Create and Manipulate Empty IO::Buffer

Source: https://docs.ruby-lang.org/en/master/IO/Buffer

Demonstrates creating an empty IO::Buffer, setting string data at a specific offset, and retrieving the buffer's content as a string. This is useful for building buffers from scratch.

```ruby
buffer = IO::Buffer.new(8) # create empty 8-byte buffer
# =>
# #<IO::Buffer 0x0000555f5d1a5c50+8 INTERNAL>
# ...
buffer
# =>
# <IO::Buffer 0x0000555f5d156ab0+8 INTERNAL>
# 0x00000000  00 00 00 00 00 00 00 00
buffer.set_string('test', 2) # put there bytes of the "test" string, starting from offset 2
# => 4
buffer.get_string  # get the result
# => "\x00\x00test\x00\x00"
```

--------------------------------

### Ruby Array Slicing - Range Start Exceeding Array Size

Source: https://docs.ruby-lang.org/en/master/Array

When the start of a range for slicing is greater than the array size, the result is nil, regardless of the end index.

```ruby
a = [:foo, 'bar', 2]
a[4..1] # => nil
a[4..0] # => nil
a[4..-1] # => nil
```

--------------------------------

### Initialize RubyGems YankCommand

Source: https://docs.ruby-lang.org/en/master/Gem/Commands/YankCommand

Initializes the YankCommand, setting up options for removing a gem version and platform, and configuring the host to interact with.

```ruby
# File lib/rubygems/commands/yank_command.rb, line 31
def initialize
  super "yank", "Remove a pushed gem from the index"

  add_version_option("remove")
  add_platform_option("remove")
  add_otp_option

  add_option("--host HOST",
             "Yank from another gemcutter-compatible host",
             "  (e.g. https://rubygems.org)") do |value, options|
    options[:host] = value
  end

  add_key_option
  @host = nil
end
```

--------------------------------

### Initialize Gem::Resolver::SourceSet

Source: https://docs.ruby-lang.org/en/master/Gem/Resolver/SourceSet

Initializes a new Gem::Resolver::SourceSet instance. It sets up internal data structures to manage gem sources and their links. This is a fundamental step for using the SourceSet to resolve gem dependencies.

```ruby
# File lib/rubygems/resolver/source_set.rb, line 13
def initialize
  super()

  @links = {}
  @sets  = {}
end
```

--------------------------------

### Compile Ruby file using Prism backend

Source: https://docs.ruby-lang.org/en/master/RubyVM/InstructionSequence

Compiles a Ruby file into an instruction sequence using the Prism parser backend. It takes the file path as input and returns an InstructionSequence object.

```Ruby
RubyVM::InstructionSequence.compile_file_prism("/tmp/hello.rb")
#=> <RubyVM::InstructionSequence:<main>@/tmp/hello.rb>
```

--------------------------------

### UnlessNode: Ruby 'unless' predicate examples

Source: https://docs.ruby-lang.org/en/master/Prism/UnlessNode

Illustrates the 'predicate' attribute of the 'unless' statement, which is the condition being evaluated. Examples show the predicate in both modifier and block forms of the 'unless' keyword.

```ruby
unless cond then bar end
       ^^^^ 

bar unless cond
           ^^^^
```

--------------------------------

### Initialize Resolv::DNS::SvcParams

Source: https://docs.ruby-lang.org/en/master/Resolv/DNS/SvcParams

Creates a new SvcParams object, optionally initializing it with a list of SvcParam objects. Duplicate keys in the initial list will result in the last occurrence taking precedence.

```ruby
def initialize(params = [])
  @params = {}

  params.each do |param|
    add param
  end
end
```

--------------------------------

### Write Default Gem Specification (Ruby)

Source: https://docs.ruby-lang.org/en/master/Gem/Installer

Writes the full .gemspec specification to the gem home's specifications/default directory. This preserves file lists, enabling commands like `gem contents`.

```Ruby
def write_default_spec
  Gem.write_binary(default_spec_file, spec.to_ruby)
end
```

--------------------------------

### Ruby IO#gets - With Integer Limit

Source: https://docs.ruby-lang.org/en/master/IO

Demonstrates limiting the number of bytes read by `gets` using an integer argument `limit`. The method will return at most `limit` bytes.

```ruby
# No more than one line.
File.open('t.txt') {|f| f.gets(10) } # => "First line"
File.open('t.txt') {|f| f.gets(11) } # => "First line\n"
File.open('t.txt') {|f| f.gets(12) } # => "First line\n"
```

--------------------------------

### Ruby Time as_json Serialization (Example)

Source: https://docs.ruby-lang.org/en/master/Time

Example of using Ruby's Time#as_json method to serialize a Time object into a JSON-compatible hash, and then using JSON.create to deserialize it back into a Time object.

```ruby
require 'json/add/time'
x = Time.now.as_json
# => {"json_class"=>"Time", "s"=>1700931656, "n"=>472846644}

Time.json_create(x)
```

--------------------------------

### Getting End Offset of nth Match in Ruby

Source: https://docs.ruby-lang.org/en/master/MatchData

Demonstrates how to get the character offset of the end of the nth captured substring using the `end(n)` method on a MatchData object.

```ruby
m = /(.)(.)(\d+)(\d)/.match("THX1138.")
# => #<MatchData "HX1138" 1:"H" 2:"X" 3:"113" 4:"8">
m[0]     # => "HX1138"
m.end(0) # => 7
m[3]     # => "113"
m.end(3) # => 6
```

```ruby
m = /(т)(е)(с)/.match('тест')
# => #<MatchData "тес" 1:"т" 2:"е" 3:"с">
m[0]     # => "тес"
m.end(0) # => 3
m[3]     # => "с"
m.end(3) # => 3
```

--------------------------------

### Initialize HashPatternNode in Ruby

Source: https://docs.ruby-lang.org/en/master/Prism/HashPatternNode

Shows the constructor for the HashPatternNode class, detailing the parameters required for its initialization.

```Ruby
# File lib/prism/node.rb, line 8373
def initialize(source, node_id, location, flags, constant, elements, rest, opening_loc, closing_loc)
  @source = source
  @node_id = node_id
  @location = location
  @flags = flags
  @constant = constant
  @elements = elements
  @rest = rest
  @opening_loc = opening_loc
  @closing_loc = closing_loc
end
```

--------------------------------

### SSLServer Instance Methods

Source: https://docs.ruby-lang.org/en/master/OpenSSL/SSL/SSLServer

Provides methods for accepting connections, closing the server, listening for connections, and shutting down the socket.

```APIDOC
## accept

### Description
Works similar to `TCPServer#accept`. It accepts an incoming connection and returns an `SSLSocket`.

### Method
**Instance Method**

### Endpoint
N/A (Instance Method)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```ruby
client_socket = ssl_server.accept
```

### Response
#### Success Response (200)
Returns an `OpenSSL::SSL::SSLSocket` object representing the client connection.

#### Response Example
```ruby
# <OpenSSL::SSL::SSLSocket:...
```
```

```APIDOC
## close

### Description
Closes the underlying `TCPServer` socket. See `IO#close` for details.

### Method
**Instance Method**

### Endpoint
N/A (Instance Method)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```ruby
ssl_server.close
```

### Response
#### Success Response (200)
Closes the socket. No return value specified.

#### Response Example
```ruby
# No output
```
```

```APIDOC
## listen

### Description
Binds the server to a port and listens for incoming connections. See `TCPServer#listen` for details.

### Method
**Instance Method**

### Endpoint
N/A (Instance Method)

### Parameters
#### Path Parameters
None

#### Query Parameters
- **backlog** (Integer) - Optional - The maximum number of pending connections. Defaults to `Socket::SOMAXCONN`.

#### Request Body
None

### Request Example
```ruby
ssl_server.listen(10)
```

### Response
#### Success Response (200)
Starts listening for connections. No return value specified.

#### Response Example
```ruby
# No output
```
```

```APIDOC
## shutdown

### Description
Shuts down the underlying `TCPServer` socket. See `BasicSocket#shutdown` for details.

### Method
**Instance Method**

### Endpoint
N/A (Instance Method)

### Parameters
#### Path Parameters
None

#### Query Parameters
- **how** (Integer) - Optional - Specifies how to shut down the connection (e.g., `Socket::SHUT_RDWR`). Defaults to `Socket::SHUT_RDWR`.

#### Request Body
None

### Request Example
```ruby
ssl_server.shutdown
```

### Response
#### Success Response (200)
Shuts down the socket. No return value specified.

#### Response Example
```ruby
# No output
```
```

```APIDOC
## to_io

### Description
Returns the `TCPServer` instance that was passed to the `SSLServer` upon initialization.

### Method
**Instance Method**

### Endpoint
N/A (Instance Method)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```ruby
underlying_server = ssl_server.to_io
```

### Response
#### Success Response (200)
Returns the `TCPServer` object.

#### Response Example
```ruby
# <TCPServer:fd...>
```
```

--------------------------------

### Ruby Array#one? - Examples

Source: https://docs.ruby-lang.org/en/master/Array

Illustrates the use of Ruby's Array#one? method. Examples cover checking for a single truthy element without arguments, using a block to define a condition for exactly one element, and comparing elements against a specific object.

```ruby
[nil, 0].one? # => true
[0, 0].one? # => false
[nil, nil].one? # => false
[].one? # => false

[0, 1, 2].one? {|element| element > 0 } # => false
[0, 1, 2].one? {|element| element > 1 } # => true
[0, 1, 2].one? {|element| element > 2 } # => false

[0, 1, 2].one?(0) # => true
[0, 0, 1].one?(0) # => false
[1, 1, 2].one?(0) # => false
['food', 'drink'].one?(/bar/) # => false
['food', 'drink'].one?(/foo/) # => true
[].one?(/foo/) # => false
```

--------------------------------

### Open3.pipeline_rw implementation (Ruby)

Source: https://docs.ruby-lang.org/en/master/Open3

This is the source code for the `pipeline_rw` method in the Open3 module. It sets up pipes for input and output and calls `pipeline_run` to execute the command pipeline.

```Ruby
def pipeline_rw(*cmds, &block)
  if Hash === cmds.last
    opts = cmds.pop.dup
  else
    opts = {}
  end

  in_r, in_w = IO.pipe
  opts[:in] = in_r
  in_w.sync = true

  out_r, out_w = IO.pipe
  opts[:out] = out_w

  pipeline_run(cmds, opts, [in_r, out_w], [in_w, out_r], &block)
end
```

--------------------------------

### Listen with UNIXServer (Ruby)

Source: https://docs.ruby-lang.org/en/master/UNIXServer

Demonstrates setting the backlog for a UNIXServer socket, which determines the maximum length of the queue for pending connections. This example shows how to configure the server to handle multiple incoming requests.

```Ruby
require 'socket'
include Socket::Constants
socket = Socket.new( AF_INET, SOCK_STREAM, 0 )
sockaddr = Socket.pack_sockaddr_in( 2200, 'localhost' )
socket.bind( sockaddr )
socket.listen( 5 )
```

--------------------------------

### Extract and Navigate Ruby Source Tarball

Source: https://docs.ruby-lang.org/en/master/contributing/building_ruby_md

These commands demonstrate how to download a Ruby source code tarball (e.g., for Ruby 3.0.2), extract its contents using tar, and then change the directory into the extracted source folder to prepare for building.

```shell
tar -xzf ruby-3.0.2.tar.gz
cd ruby-3.0.2
```

--------------------------------

### Resolv::DNS Class Overview

Source: https://docs.ruby-lang.org/en/master/Resolv/DNS

Overview of the Resolv::DNS class, its purpose as a DNS stub resolver, and its information sources.

```APIDOC
## Class Resolv::DNS

### Description
`Resolv::DNS` is a `DNS` stub resolver. It provides methods for querying DNS records.
Information is taken from sources like STD0013, RFC 1035, and IANA assignments.

### Constants

- **Port** (Integer): Default DNS UDP port.
- **UDPSize** (Integer): Default DNS UDP packet size.

```

--------------------------------

### Initialize Prism::Relocation::Entry

Source: https://docs.ruby-lang.org/en/master/Prism/Relocation/Entry

Initializes a new Prism::Relocation::Entry with a given repository. It stores the repository and initializes values to nil, to be reified upon first access.

```ruby
# File lib/prism/relocation.rb, line 25
def initialize(repository)
  @repository = repository
  @values = nil
end
```

--------------------------------

### Spawn Process with Custom Process Name (Ruby)

Source: https://docs.ruby-lang.org/en/master/Process

Illustrates using `spawn` with a 2-element array argument to specify both the executable path and the string used as the process name. This allows for more control over how the process appears in system process listings.

```ruby
pid = spawn(['sleep', 'Hello!'], '1')
```

```ruby
p `ps -p #{pid} -o command=`
```

--------------------------------

### YAML Deserialization Example

Source: https://docs.ruby-lang.org/en/master/security_rdoc

Demonstrates how YAML can deserialize arbitrary Ruby objects, posing a security risk. This example shows deserializing data that creates an ERB object, which can execute arbitrary code.

```yaml
!ruby/object:ERB
src: puts `uname`
```