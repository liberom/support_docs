# Minitest

Minitest is a complete testing framework for Ruby that provides a rich suite of testing facilities supporting TDD (Test-Driven Development), BDD (Behavior-Driven Development), mocking, and benchmarking. It emphasizes simplicity and performance, offering a clean implementation that leverages standard Ruby features like classes, modules, and inheritance rather than reinventing them. The framework is designed to be small, fast, and easily understandable, making it ideal for both beginners and experienced developers.

The framework consists of several components: minitest/test provides a fast unit testing system with assertions, minitest/spec offers a spec-style DSL with expectations, minitest/benchmark enables performance testing with curve fitting, and minitest/mock provides simple mocking capabilities. Minitest is included in Ruby's standard library and serves as the testing foundation for major projects including Rails, Rake, and RDoc. Its plugin architecture allows for extensive customization through reporters and extensions.

## Unit Testing with Minitest::Test

Create test classes by subclassing Minitest::Test and defining methods starting with test_

```ruby
require "minitest/autorun"

class Meme
  def i_can_has_cheezburger?
    "OHAI!"
  end

  def will_it_blend?
    "YES!"
  end
end

class TestMeme < Minitest::Test
  def setup
    @meme = Meme.new
  end

  def test_that_kitty_can_eat
    assert_equal "OHAI!", @meme.i_can_has_cheezburger?
  end

  def test_that_it_will_not_blend
    refute_match /^no/i, @meme.will_it_blend?
  end

  def test_that_will_be_skipped
    skip "test this later"
  end

  def teardown
    # cleanup code here
  end
end
```

## Spec-Style Testing with Minitest::Spec

Use describe blocks and expectations for BDD-style testing

```ruby
require "minitest/autorun"

class Calculator
  def add(a, b)
    a + b
  end

  def divide(a, b)
    raise ArgumentError, "Cannot divide by zero" if b == 0
    a / b.to_f
  end
end

describe Calculator do
  before do
    @calc = Calculator.new
  end

  describe "when performing addition" do
    it "must add two numbers correctly" do
      _(@calc.add(2, 3)).must_equal 5
    end

    it "must handle negative numbers" do
      _(@calc.add(-5, 3)).must_equal -2
    end
  end

  describe "when performing division" do
    it "must divide two numbers correctly" do
      _(@calc.divide(10, 2)).must_equal 5.0
    end

    it "must raise error on division by zero" do
      _ { @calc.divide(10, 0) }.must_raise ArgumentError
    end
  end

  let(:default_calc) { Calculator.new }

  it "can use let for lazy evaluation" do
    _(default_calc).must_be_instance_of Calculator
  end
end
```

## Assert Equal with Diff Output

Compare expected and actual values with detailed diff output for failures

```ruby
require "minitest/autorun"

class TestStringComparison < Minitest::Test
  def test_long_string_comparison
    expected = "The quick brown fox jumps over the lazy dog"
    actual   = "The quick brown fox jumps over the lazy cat"

    assert_equal expected, actual
    # Failure shows diff:
    # --- expected
    # +++ actual
    # @@ -1 +1 @@
    # -"The quick brown fox jumps over the lazy dog"
    # +"The quick brown fox jumps over the lazy cat"
  end

  def test_array_comparison
    expected = [1, 2, 3, 4, 5]
    actual   = [1, 2, 3, 4, 6]

    assert_equal expected, actual
  end
end
```

## Float Comparisons with Delta and Epsilon

Handle floating-point comparisons with configurable precision

```ruby
require "minitest/autorun"

class TestFloatMath < Minitest::Test
  def test_pi_approximation
    # Assert values are within delta (absolute difference)
    assert_in_delta Math::PI, 22.0 / 7.0, 0.01
  end

  def test_large_float_comparison
    expected = 1_000_000.0
    actual   = 1_000_001.0

    # Assert relative error is less than epsilon
    assert_in_epsilon expected, actual, 0.00001
  end

  def test_refute_delta
    # Assert values are NOT within delta
    refute_in_delta 1.0, 2.0, 0.5
  end
end
```

## Exception Testing

Verify that code raises expected exceptions with proper messages

```ruby
require "minitest/autorun"

class BankAccount
  def initialize(balance)
    @balance = balance
  end

  def withdraw(amount)
    raise ArgumentError, "Amount must be positive" if amount <= 0
    raise RuntimeError, "Insufficient funds" if amount > @balance
    @balance -= amount
  end
end

class TestBankAccount < Minitest::Test
  def test_raises_on_negative_withdrawal
    account = BankAccount.new(100)

    error = assert_raises(ArgumentError) do
      account.withdraw(-50)
    end

    assert_equal "Amount must be positive", error.message
  end

  def test_raises_on_insufficient_funds
    account = BankAccount.new(50)

    assert_raises(RuntimeError) { account.withdraw(100) }
  end

  def test_accepts_multiple_exception_types
    account = BankAccount.new(50)

    # Will pass if any of these exceptions are raised
    assert_raises(ArgumentError, RuntimeError) do
      account.withdraw(100)
    end
  end
end
```

## Output Capture and Verification

Test stdout and stderr output from your code

```ruby
require "minitest/autorun"

class Logger
  def log_info(message)
    puts "INFO: #{message}"
  end

  def log_error(message)
    warn "ERROR: #{message}"
  end

  def log_both(info, error)
    puts "INFO: #{info}"
    warn "ERROR: #{error}"
  end
end

class TestLogger < Minitest::Test
  def test_info_output
    logger = Logger.new

    assert_output("INFO: Starting process\n") do
      logger.log_info("Starting process")
    end
  end

  def test_error_output
    logger = Logger.new

    assert_output(nil, "ERROR: Failed to start\n") do
      logger.log_error("Failed to start")
    end
  end

  def test_both_outputs
    logger = Logger.new

    assert_output("INFO: Done\n", "ERROR: Warning\n") do
      logger.log_both("Done", "Warning")
    end
  end

  def test_regex_matching
    logger = Logger.new

    assert_output(/INFO:.*process/) do
      logger.log_info("Starting the process")
    end
  end

  def test_silent_execution
    assert_silent do
      result = 1 + 1  # Silent operation
    end
  end
end
```

## Collection and Object Assertions

Test collection membership, object types, and predicates

```ruby
require "minitest/autorun"

class TestCollections < Minitest::Test
  def test_array_inclusion
    fruits = ["apple", "banana", "orange"]

    assert_includes fruits, "banana"
    refute_includes fruits, "grape"
  end

  def test_empty_collections
    assert_empty []
    refute_empty [1, 2, 3]
  end

  def test_instance_and_kind
    assert_instance_of String, "hello"
    assert_kind_of Numeric, 42
    assert_kind_of Numeric, 3.14  # Integer and Float are both Numeric
  end

  def test_nil_checks
    value = nil
    assert_nil value

    value = "something"
    refute_nil value
  end

  def test_object_identity
    a = "hello"
    b = a
    c = "hello"

    assert_same a, b      # Same object
    refute_same a, c      # Different objects, same value
  end

  def test_predicates
    str = ""
    assert_predicate str, :empty?

    arr = [1, 2, 3]
    refute_predicate arr, :empty?
  end

  def test_respond_to
    obj = "string"
    assert_respond_to obj, :upcase
    refute_respond_to obj, :nonexistent_method
  end
end
```

## Pattern Matching (Ruby 3.0+)

Test pattern matching expressions and their matches

```ruby
require "minitest/autorun"

class TestPatternMatching < Minitest::Test
  def test_array_pattern_match
    assert_pattern do
      [1, 2, 3] => [Integer, Integer, Integer]
    end
  end

  def test_hash_pattern_match
    assert_pattern do
      {name: "Alice", age: 30} => {name: String, age: Integer}
    end
  end

  def test_pattern_mismatch
    refute_pattern do
      [1, 2, 3] => [String, String, String]
    end
  end

  def test_complex_pattern
    data = {user: {name: "Bob", age: 25}, status: "active"}

    assert_pattern do
      data => {user: {name: String, age: Integer}, status: String}
    end
  end
end
```

## Parallel Test Execution

Run tests in parallel across multiple cores for faster test suites

```ruby
require "minitest/autorun"

class TestParallel < Minitest::Test
  # Enable parallel execution for this test class
  parallelize_me!

  def test_example_1
    sleep 0.1
    assert_equal 2, 1 + 1
  end

  def test_example_2
    sleep 0.1
    assert_equal 4, 2 + 2
  end

  def test_example_3
    sleep 0.1
    assert_equal 6, 3 + 3
  end

  # All these tests run concurrently across available CPU cores
  # Set MT_CPU environment variable to control thread count:
  # MT_CPU=4 ruby test.rb
end
```

## Benchmark Testing

Verify algorithm performance characteristics with curve fitting

```ruby
require "minitest/autorun"
require "minitest/benchmark"

class TestSortPerformance < Minitest::Benchmark
  def setup
    @random_data = Array.new(10_000) { rand(1_000_000) }
  end

  # Override default benchmark range [1, 10, 100, 1_000, 10_000]
  def self.bench_range
    bench_exp(10, 10_000, 10)
  end

  def bench_linear_search
    assert_performance_linear 0.9999 do |n|
      data = @random_data.first(n)
      data.include?(data.last)
    end
  end

  def bench_binary_search
    assert_performance_logarithmic 0.9999 do |n|
      data = @random_data.first(n).sort
      data.bsearch { |x| x >= data.last }
    end
  end

  def bench_constant_time_operation
    assert_performance_constant 0.99 do |n|
      {}.class
    end
  end

  # Output format (tab-delimited, paste into spreadsheet):
  # bench_linear_search    0.000123    0.001234    0.012345
  # bench_binary_search    0.000100    0.000200    0.000300
end
```

## Spec-Style Benchmarks

Write benchmarks using describe/it syntax

```ruby
require "minitest/autorun"
require "minitest/benchmark"

describe "Array Performance Benchmark" do
  bench_range do
    bench_exp(100, 10_000, 10)
  end

  bench_performance_linear "array append", 0.9999 do |n|
    arr = []
    n.times { arr << 1 }
  end

  bench_performance_constant "array access", 0.99 do |n|
    arr = Array.new(n, 0)
    arr[n/2]
  end

  bench_performance_logarithmic "binary search", 0.9999 do |n|
    arr = (1..n).to_a
    arr.bsearch { |x| x >= n/2 }
  end
end
```

## Custom Reporters

Create custom output formats by implementing reporters

```ruby
require "minitest"

class JSONReporter < Minitest::StatisticsReporter
  def start
    super
    puts "{"
    puts '  "results": ['
  end

  def record(result)
    super
    puts "    {"
    puts "      \"name\": \"#{result.name}\","
    puts "      \"class\": \"#{result.class_name}\","
    puts "      \"time\": #{result.time},"
    puts "      \"passed\": #{result.passed?}"
    puts "    },"
  end

  def report
    super
    puts "  ],"
    puts "  \"summary\": {"
    puts "    \"total\": #{count},"
    puts "    \"failures\": #{failures},"
    puts "    \"errors\": #{errors},"
    puts "    \"skips\": #{skips}"
    puts "  }"
    puts "}"
  end
end

# Register the custom reporter
def Minitest.plugin_json_init(options)
  self.reporter << JSONReporter.new(options[:io], options)
end
```

## Minitest Rake Task

Configure test execution via Rake with full control over options

```ruby
# Rakefile
require "minitest/test_task"

# Simple configuration
Minitest::TestTask.create

# Advanced configuration
Minitest::TestTask.create(:test) do |t|
  t.libs << "test"
  t.libs << "lib"
  t.warning = false
  t.test_globs = ["test/**/*_test.rb"]
  t.verbose = true
end

task :default => :test

# Generates these rake tasks:
# rake test          - Run the test suite
# rake test:cmd      - Print the test command
# rake test:isolated - Show which tests fail when run separately
# rake test:slow     - Show 25 slowest tests

# Run with variables:
# rake test N=/pattern/          # Run tests matching pattern
# rake test X=/pattern/          # Exclude tests matching pattern
# rake test SEED=12345           # Use specific random seed
# rake test MT_CPU=4             # Use 4 parallel threads
```

## Lifecycle Hooks for Extensions

Create reusable test extensions with before/after hooks

```ruby
require "minitest/autorun"

module DatabaseCleaner
  def before_setup
    super
    puts "Connecting to test database..."
    @db_connection = "DB_CONNECTION"
  end

  def after_setup
    puts "Database ready"
    super
  end

  def before_teardown
    super
    puts "Rolling back transaction..."
  end

  def after_teardown
    puts "Closing database connection..."
    @db_connection = nil
    super
  end
end

class TestWithDatabase < Minitest::Test
  include DatabaseCleaner

  def setup
    puts "Test-specific setup"
  end

  def test_database_operations
    assert_equal "DB_CONNECTION", @db_connection
    puts "Running test"
  end

  def teardown
    puts "Test-specific teardown"
  end
end

# Execution order:
# before_setup -> setup -> after_setup
# [test runs]
# before_teardown -> teardown -> after_teardown
```

## Expectations DSL

Use RSpec-style expectations with must/wont syntax

```ruby
require "minitest/autorun"

describe "User" do
  before do
    @user = Struct.new(:name, :age).new("Alice", 30)
  end

  it "uses must_equal for equality" do
    _(@user.name).must_equal "Alice"
    _(@user.age).must_equal 30
  end

  it "uses wont_equal for inequality" do
    _(@user.name).wont_equal "Bob"
  end

  it "uses must_be for operators" do
    _(@user.age).must_be :>, 18
    _(@user.age).must_be :<=, 100
  end

  it "uses must_include for collections" do
    names = ["Alice", "Bob", "Charlie"]
    _(names).must_include @user.name
  end

  it "uses must_match for patterns" do
    _(@user.name).must_match /^A/
    _(@user.name).wont_match /^Z/
  end

  it "uses must_raise for exceptions" do
    _ { raise ArgumentError }.must_raise ArgumentError
  end

  it "uses must_be_instance_of for type checking" do
    _(@user).must_be_instance_of Struct
  end

  it "uses must_respond_to for duck typing" do
    _(@user).must_respond_to :name
    _(@user).must_respond_to :age
  end
end
```

## Skip and Conditional Tests

Skip tests conditionally or until a specific date

```ruby
require "minitest/autorun"

class TestConditional < Minitest::Test
  def test_unconditional_skip
    skip "Not implemented yet"
    # Test code never runs
  end

  def test_skip_on_windows
    skip "Windows not supported" if windows?
    # Test continues on non-Windows systems
  end

  def test_skip_until_date
    skip_until 2025, 12, 31, "Fix this after release"
    # After the date, this warning appears:
    # Stale skip_until "Fix this after release" at test/example.rb:10
  end

  def test_fail_after_date
    fail_after 2025, 6, 30, "Remove deprecated feature by June 2025"
    # Test passes before date, fails after
  end

  def test_platform_specific
    skip "JRuby only" unless jruby?
    skip "MRI only" unless mri?
    skip "macOS only" unless osx?
  end
end
```

## Running Tests from Command Line

Execute tests with various runtime options and filters

```bash
# Run all tests in a file
ruby -Ilib:test test/my_test.rb

# Run with specific seed for reproducibility
ruby test/my_test.rb --seed 12345

# Run only tests matching pattern
ruby test/my_test.rb --name /calculation/
ruby test/my_test.rb -n /addition/

# Exclude tests matching pattern
ruby test/my_test.rb --exclude /slow/
ruby test/my_test.rb -e /benchmark/

# Verbose output (show each test name)
ruby test/my_test.rb --verbose

# Show help and available options
ruby test/my_test.rb --help

# Enable pride output (colorful dots)
ruby test/my_test.rb --pride

# Skip reporting certain result types (E=errors, F=failures, S=skips)
ruby test/my_test.rb --skip E

# Show skipped tests at end
ruby test/my_test.rb --show-skips

# Turn Ruby warnings into errors
ruby test/my_test.rb -Werror
```

Minitest serves as a comprehensive testing solution suitable for projects of any size, from small scripts to large applications like Ruby on Rails. Its main use cases include unit testing with assertions for granular test control, BDD-style testing with specs for readable test documentation, performance verification through benchmarking to prevent algorithm regressions, and custom reporter development for CI/CD integration. The framework's minimalist design means developers only need to understand Ruby itself, with no DSL magic to learn.

Integration with existing Ruby projects is straightforward through require statements, Rake tasks, or test runners. The plugin architecture enables seamless extension through custom reporters, assertions, and hooks without modifying core code. Minitest's parallel execution capabilities scale test suites across multiple CPU cores, while its comprehensive assertion library covers common testing needs including equality checks, exception handling, output verification, and pattern matching. Whether building test-first applications, maintaining legacy code, or establishing CI/CD pipelines, Minitest provides the essential testing infrastructure with minimal overhead.
