### Install Gems and Initialize Cucumber with Bundler

Source: https://cucumber.io/docs/installation/ruby

Installs all dependencies listed in the Gemfile using Bundler and initializes a 'features/' directory for Cucumber. This sets up the basic structure for writing Cucumber features.

```bash
bundle
cucumber --init
```

--------------------------------

### Verify Cucumber Installation with Maven

Source: https://cucumber.io/docs/guides/10-minute-tutorial

Runs the default Maven test goal to verify the Cucumber installation and project setup. This command executes any tests found in the project, confirming that Cucumber is integrated correctly.

```bash
mvn test
```

--------------------------------

### Cucumber Feature File Examples

Source: https://cucumber.io/docs/guides/parallel-execution

Example feature files demonstrating scenarios and scenario outlines for Cucumber testing.

```gherkin
Feature: Scenarios feature file  
  
  Scenario: Scenario Number One  
    Given Step from 'Scenario 1' in 'scenarios' feature file  
  
  Scenario: Scenario Number Two  
    Given Step from 'Scenario 2' in 'scenarios' feature file  

```

```gherkin
Feature: Scenario Outlines feature file  
  
  Scenario Outline: <scen_out_row_num>  
    Given Step from '<scen_out_row_num>' in 'scenario-outlines' feature file  
  
    Examples:   
      | scen_out_row_num       |  
      | Scenario Outline Row 1 |  
      | Scenario Outline Row 2 |  

```

--------------------------------

### Install Gems and Generate Cucumber Rails Configuration

Source: https://cucumber.io/docs/installation/ruby

Installs gems using Bundler and then runs the Cucumber Rails generator to set up the necessary configuration files for Cucumber within a Rails application.

```bash
bundle
rails generate cucumber:install
```

--------------------------------

### Install Cucumber Gem using Rubygems

Source: https://cucumber.io/docs/installation/ruby

Installs the Cucumber gem directly from Rubygems using the command line. This is a straightforward method for global or project-specific installations.

```bash
gem install cucumber
```

--------------------------------

### Install Cucumber-R from CRAN

Source: https://cucumber.io/docs/installation/r

Installs the 'cucumber' package using the standard R package installation command from CRAN. This is the recommended method for most users.

```r
install.packages("cucumber")
```

--------------------------------

### InstallPlugin Hook Example (Ruby)

Source: https://cucumber.io/docs/cucumber/api

A Ruby-specific hook that runs once after Cucumber is configured but before any features are loaded. It receives the configuration and a registry, allowing for Cucumber extension.

```ruby
InstallPlugin do |config, registry|
  puts "Features dwell in #{config.feature_dirs}"
end

```

--------------------------------

### Example Scenario for Adding Description (Gherkin)

Source: https://cucumber.io/docs/guides/anti-patterns

A Gherkin scenario demonstrating how to add a description to a CV. This scenario is used as an example for step definition implementations in various languages.

```gherkin
Scenario: add description  
  Given I have a CV and I'm on the edit description page  
  And I fill in "Description" with "Cucumber BDD tool"  
  When I press "Save"  
  Then I should see "Cucumber BDD tool" under "Descriptions"  
```

--------------------------------

### Gherkin Scenario Example

Source: https://cucumber.io/docs/index

An example of a scenario written in Gherkin, demonstrating the Given-When-Then structure for defining executable specifications. Gherkin is a plain-text language used by Cucumber.

```gherkin
Scenario: Breaker guesses a word  
  Given the Maker has chosen a word  
  When the Breaker makes a guess  
  Then the Maker is asked to score  

```

--------------------------------

### Cucumber Scenario Outline Example

Source: https://cucumber.io/docs/gherkin/reference

Demonstrates how to use Scenario Outline to run a scenario with multiple sets of data. It uses `<parameter>` placeholders in the scenario steps and provides data in an Examples table. This reduces repetition by defining a template scenario.

```gherkin
Scenario Outline: eating
  Given there are <start> cucumbers
  When I eat <eat> cucumbers
  Then I should have <left> cucumbers

  Examples:
    | start | eat | left |
    |    12 |   5 |    7 |
    |    20 |   5 |   15 |
```

--------------------------------

### Cucumber Feature File with Scenario Outline and Examples

Source: https://cucumber.io/docs/guides/10-minute-tutorial

This feature file defines a scenario outline for checking if it's Friday, using examples to test different days and expected outcomes. It replaces static scenarios with a dynamic approach.

```gherkin
Feature: Is it Friday yet?  
  Everybody wants to know when it's Friday  
  
  Scenario Outline: Today is or is not Friday  
    Given today is "<day>"  
    When I ask whether it's Friday yet  
    Then I should be told "<answer>"  
  
  Examples:  
    | day            | answer |  
    | Friday         | TGIF   |  
    | Sunday         | Nope   |  
    | anything else! | Nope   |  

```

--------------------------------

### BeforeAll Hook Examples

Source: https://cucumber.io/docs/cucumber/api

Defines actions to be performed once before any scenario is run. Supports annotated methods and lambda styles in Java, Kotlin, Scala, JavaScript, and Ruby.

```java
@BeforeAll
public static void beforeAll() {
    // Runs before all scenarios
}

```

```kotlin
BeforeAll {
    // doSomething
}

```

```scala
BeforeAll {
    // doSomething
}

```

```javascript
const { BeforeAll } = require('@cucumber/cucumber');

BeforeAll(async function () {
  // perform some shared setup
});

```

```ruby
BeforeAll do
  # Do something before any scenario is executed
end

```

--------------------------------

### Install Cucumber-R from GitHub

Source: https://cucumber.io/docs/installation/r

Installs the 'cucumber' package directly from its GitHub repository using the 'remotes' package. This method is useful for installing development versions or specific branches.

```r
remotes::install_github("jakubsob/cucumber")
```

--------------------------------

### Gherkin Feature File Example

Source: https://cucumber.io/docs/gherkin/reference

An example of a Gherkin feature file demonstrating the structure with Feature, Scenario, and Step keywords. It includes comments and indentation.

```gherkin
Feature: Guess the word  
  
  # The first example has two steps  
  Scenario: Maker starts a game  
    When the Maker starts a game  
    Then the Maker waits for a Breaker to join  
  
  # The second example has three steps  
  Scenario: Breaker joins a game  
    Given the Maker has started a game with the word "silky"  
    When the Breaker joins the Maker's game  
    Then the Breaker must guess a word with 5 characters  

```

--------------------------------

### Gherkin Feature File Example

Source: https://cucumber.io/docs/bdd/who-does-what

An example of a Gherkin feature file demonstrating the structure for defining a feature, its purpose, the user role, and a specific scenario with Given, When, and Then steps. This format helps in clearly outlining testable requirements.

```gherkin
Feature: Explaining Cucumber  
  In order to gain an understanding of the Cucumber testing system  
  As a non-programmer  
  I want to have an overview of Cucumber that is understandable by non-geeks  
  
  Scenario: A worker seeks an overview of Cucumber  
    Given I have a coworker who knows a lot about Cucumber  
    When I ask my coworker to give an overview of how Cucumber works  
    And I listen to their explanation  
    Then I should have a basic understanding of Cucumber  

```

--------------------------------

### JavaScript Step Definition Example for Cucumber

Source: https://cucumber.io/docs/index

An example of a step definition written in JavaScript for Cucumber. Step definitions connect Gherkin steps to the actual programming code that performs the described actions.

```javascript
When('{maker} starts a game', maker => {  
  maker.startGameWithWord({ word: 'whale' })
})

```

--------------------------------

### Cucumber Step Definition with Guice Injection (Java)

Source: https://cucumber.io/docs/cucumber/state

Example of a Cucumber step definition class using Google Guice for dependency injection. It injects an 'AppService' and defines steps to start and check the status of application services.

```java
package com.example.app;  
  
import static org.junit.Assert.assertTrue;  
  
import io.cucumber.java.en.When;  
import io.cucumber.java.en.Then;  
import io.cucumber.guice.ScenarioScoped;  
import com.example.app.service.AppService;  
import java.util.Objects;  
import javax.inject.Inject;  
  
@ScenarioScoped  
public final class StepDefinition {  
  
    private final AppService appService;  
  
    @Inject  
    public StepDefinition( AppService appService ) {  
        this.appService = Objects.requireNonNull( appService, "appService must not be null" );  
    }  
  
    @When("the application services are started")  
    public void startServices() {  
        this.appService.startServices();  
    }  
  
    @Then("all application services should be running")  
    public void checkThatApplicationServicesAreRunning() {  
        assertTrue( this.appService.servicesAreRunning() );  
    }  
}

```

--------------------------------

### Splitting Conjunction Steps Example (Gherkin)

Source: https://cucumber.io/docs/guides/anti-patterns

Demonstrates how to split a Gherkin step that combines multiple conditions into separate, more atomic steps using 'And'. This improves readability and reusability.

```gherkin
Given I have shades  
And I have a brand new Mustang  
```

--------------------------------

### Conditional Hooks Examples

Source: https://cucumber.io/docs/cucumber/api

Allows hooks to be conditionally executed based on scenario tags. Examples show how to apply hooks to specific scenarios using tag expressions in Java, Kotlin, Scala, JavaScript, and Ruby.

```java
@After("@browser and not @headless")
public void doSomethingAfter(Scenario scenario){
}

```

```kotlin
After("@browser and not @headless", (Scenario scenario) -> {
});

```

```scala
After (arrayOf("@browser and not @headless")) { scenario: Scenario ->
    driver.quit()
}

```

```javascript
Before({tags: '@browser and not @headless'}, async function () {
})

```

```ruby
Before('@browser and not @headless') do
end

```

--------------------------------

### Cucumber-JVM Step Definition Examples: Regex vs. Cucumber Expressions

Source: https://cucumber.io/docs/faq

Demonstrates the syntax for defining step definitions using both regular expressions (regex) and Cucumber expressions in Cucumber-JVM. Regex steps typically start with '^' and end with '$', while Cucumber expressions do not have these anchors. Note that a step definition cannot mix regex and Cucumber expressions.

```java
@Given("^today is ([0-9]{4}-[0-9]{2}-[0-9]{2})$")  
    public void today_is(Date date) {  
        calculator = new DateCalculator(date);  
    }
```

```java
@When("I add {int} and {int}")  
    public void adding(int arg1, int arg2) {  
        calc.push(arg1);  
        calc.push(arg2);  
        calc.push("+");  
    }
```

--------------------------------

### Create Cucumber Project with Maven Archetype

Source: https://cucumber.io/docs/guides/10-minute-tutorial

Generates a new Cucumber project using the `cucumber-archetype` Maven plugin. This command initializes a project structure with necessary dependencies for Cucumber. It requires Maven to be installed and configured.

```bash
mvn archetype:generate \
"-DarchetypeGroupId=io.cucumber" \
"-DarchetypeArtifactId=cucumber-archetype" \
"-DarchetypeVersion=7.33.0" \
"-DgroupId=hellocucumber" \
"-DartifactId=hellocucumber" \
"-Dpackage=hellocucumber" \
"-Dversion=1.0.0-SNAPSHOT" \
"-DinteractiveMode=false"
```

--------------------------------

### Feature-Coupled Step Definitions Example Structure (Java, Kotlin, JavaScript, Ruby)

Source: https://cucumber.io/docs/guides/anti-patterns

Illustrates the directory structure for feature files and corresponding step definition files in Java, Kotlin, JavaScript, and Ruby. This structure can lead to code duplication and high maintenance costs if not managed properly.

```text
features/  
+--edit_work_experience.feature  
+--edit_languages.feature  
+--edit_education.feature  
+--steps/  
   +--edit_work_experience_steps.java  
   +--edit_languages_steps.java  
   +--edit_education_steps.java  
```

```text
features/  
+--edit_work_experience.feature  
+--edit_languages.feature  
+--edit_education.feature  
+--steps/  
   +--edit_work_experience_steps.kt  
   +--edit_languages_steps.kt  
   +--edit_education_steps.kt  
```

```text
features/  
+--edit_work_experience.feature  
+--edit_languages.feature  
+--edit_education.feature  
+--steps/  
   +--edit_work_experience_steps.js  
   +--edit_languages_steps.js  
   +--edit_education_steps.js  
```

```text
features/  
+--edit_work_experience.feature  
+--edit_languages.feature  
+--edit_education.feature  
+--steps/  
   +--edit_work_experience_steps.rb  
   +--edit_languages_steps.rb  
   +--edit_education_steps.rb  
```

--------------------------------

### Cucumber Options - Plugins Configuration

Source: https://cucumber.io/docs/cucumber/api

Example of configuring Cucumber plugins using the `@CucumberOptions` annotation. This example specifies 'pretty' for detailed output and 'html' to generate an HTML report.

```java
@CucumberOptions(plugin = {"pretty", "html:target/cucumber.html"})
```

--------------------------------

### Abstracting Steps with Helper Methods

Source: https://cucumber.io/docs/gherkin/step-organization

Reduce code duplication by abstracting common step behaviors into helper methods. This example demonstrates how to generalize a step that opens a web page, making it more reusable across different pages.

```Java
@Given("I go to the {string} page")
public void i_want_to_open_page(String webpage) {
    webpageFactory.openPage(webpage);
}
```

```Kotlin
@Given("I go to the {string} page")
fun `I want to open page`(webpage: String) {
    webpageFactory.openPage(webpage)
}
```

```JavaScript
Given("I go to the {string} page", function (webpage) {
    webpageFactory.openPage(webpage)
})
```

```Ruby
Given 'I go to the {string} page' do |page|
    open_web_page page
end
```

```Go
s.Step(`^I go to the \"([^\"]*)\" page$`, goToPage)

func goToPage(webpage string) error {
    return webpageFactory.Open(webpage)
}
```

--------------------------------

### Run Cucumber Tests with Specific Browser in Java

Source: https://cucumber.io/docs/guides/browser-automation

Command-line examples for running Cucumber tests with a specified browser. The first command uses Maven to set the 'browser' system property for Java tests. The second command shows how to use the 'driver' system property if Serenity is integrated, requiring no extra coding.

```shell
mvn test -Dbrowser=chrome
```

```shell
mvn test -Ddriver=chrome
```

--------------------------------

### Grouping Step Definitions by Domain Concept

Source: https://cucumber.io/docs/gherkin/step-organization

Organize step definitions into separate files based on domain concepts for better project maintainability. This example shows common file naming conventions for Java, Kotlin, Ruby, JavaScript, and Go.

```Java
EmployeeStepDefinitions.java
EducationStepDefinitions.java
ExperienceStepDefinitions.java
AuthenticationStepDefinitions.java
```

```Kotlin
EmployeeStepDefinitions.kt
EducationStepDefinitions.kt
ExperienceStepDefinitions.kt
AuthenticationStepDefinitions.kt
```

```Ruby
employee_steps.rb
education_steps.rb
experience_steps.rb
authentication_steps.rb
```

```JavaScript
employee_steps.js
education_steps.js
experience_steps.js
authentication_steps.js
```

```Go
employee_steps.go
education_steps.go
experience_steps.go
authentication_steps.go
```

--------------------------------

### Add Cucumber-Rails to Gemfile for Rails Projects

Source: https://cucumber.io/docs/installation/ruby

Adds the 'cucumber-rails' and optionally 'database_cleaner' gems to the test group in a Rails project's Gemfile. This prepares the project to use Cucumber for testing.

```ruby
group :test do
  gem 'cucumber-rails', require: false
  # database_cleaner is not mandatory, but highly recommended
  gem 'database_cleaner'
end
```

--------------------------------

### Step Definition for 'edit_work_experience.feature' (Kotlin)

Source: https://cucumber.io/docs/guides/anti-patterns

Kotlin implementation of a step definition for the 'edit_work_experience.feature' scenario. This example demonstrates creating an Employee object and initializing a CV using Kotlin syntax.

```kotlin
@Given("I have a CV and I'm on the edit description page")  
fun I_have_a_CV_and_Im_on_the_edit_description_page() {  
    val employee = Employee("Sally")  
    employee.createCV()  
}  
```

--------------------------------

### Step Definition for 'edit_work_experience.feature' (Ruby)

Source: https://cucumber.io/docs/guides/anti-patterns

Ruby implementation of a step definition for the 'edit_work_experience.feature' scenario. This example uses Ruby syntax to create an Employee, their CV, and navigate to the descriptions page.

```ruby
Given /I have a CV and I'm on the edit description page/ do  
  @employee = Employee.create!(name: 'Sally')  
  @employee.create_cv  
  visits("/employees/#{@employee.id}/descriptions/new")  
end  
```

--------------------------------

### Cucumber Step Definition Example

Source: https://cucumber.io/docs/cucumber/api

Illustrates a basic Cucumber step definition corresponding to a Gherkin step. This example shows how a numerical value from the Gherkin step is passed as an argument to the step definition method.

```gherkin
Given I have 93 cucumbers in my belly
```

--------------------------------

### Combine Cucumber Profiles and Arguments

Source: https://cucumber.io/docs/cucumber/configuration

This command-line example shows how to execute Cucumber using a specific profile while also applying additional command-line arguments. This allows for flexible test execution by combining predefined profiles with ad-hoc filtering or options.

```bash
[user@system project] cucumber --profile html_report --tags ~@wip  
```

--------------------------------

### Step Definition for 'edit_work_experience.feature' (Java)

Source: https://cucumber.io/docs/guides/anti-patterns

Java implementation of a step definition for the 'edit_work_experience.feature' scenario. This example shows how to create an Employee object and initialize a CV.

```java
@Given("I have a CV and I'm on the edit description page")  
    public void I_have_a_CV_and_Im_on_the_edit_description_page() {  
        Employee employee = new Employee("Sally");  
        employee.createCV();  
    }  
```

--------------------------------

### User Story Format Example

Source: https://cucumber.io/docs/terms/user-story

Illustrates the standard format for writing a user story, including the actor, feature, and benefit. This format helps in clearly defining the 'who', 'what', and 'why' of a piece of functionality.

```gherkin
As an <actor>  
I want a <feature>  
So that <benefit>  


```

```gherkin
As an mobile bank customer  
I want to see balance on my accounts  
So that I can make better informed decisions about my spending  


```

--------------------------------

### AfterStep Hook Examples

Source: https://cucumber.io/docs/cucumber/api

Defines actions to be performed after each step. Supports annotated methods and lambda styles in Java, Kotlin, Scala, JavaScript, and Ruby.

```java
@AfterStep
public void doSomethingAfterStep(Scenario scenario){
}

```

```kotlin
AfterStep((Scenario scenario) -> {
});

```

```scala
AfterStep { scenario: Scenario ->
    // doSomething
}

```

```javascript
AfterStep(async function({pickle, pickleStep, gherkinDocument, result, testCaseStartedId, testStepId}) {
    // doSomething
})

```

```ruby
AfterStep do |scenario|
end

```

--------------------------------

### Add Cucumber to Gemfile for Bundler (without Rails)

Source: https://cucumber.io/docs/installation/ruby

Adds the 'cucumber' gem to your project's Gemfile when using Bundler for dependency management. This ensures Cucumber is available for your project.

```ruby
gem 'cucumber'
```

--------------------------------

### AfterAll Hook Examples

Source: https://cucumber.io/docs/cucumber/api

Defines actions to be performed once after all scenarios have been executed. Supports annotated methods and lambda styles in Java, Kotlin, Scala, JavaScript, and Ruby.

```java
@AfterAll
public static void afterAll() {
    // Runs after all scenarios
}

```

```kotlin
AfterAll {
    // doSomething
}

```

```scala
AfterAll {
    // doSomething
}

```

```javascript
const { AfterAll } = require('@cucumber/cucumber');

AfterAll(async function () {
  // perform some shared setup
});

```

```ruby
AfterAll do
  # Do something after all scenarios have been executed
end

```

--------------------------------

### Install Cucumber-JS with npm

Source: https://cucumber.io/docs/installation/javascript

Installs the Cucumber-JS package as a development dependency in a Node.js project using npm. This command adds `@cucumber/cucumber` to your project's `devDependencies` in `package.json`.

```bash
npm install --save-dev @cucumber/cucumber
```

--------------------------------

### Run All Cucumber Features

Source: https://cucumber.io/docs/cucumber/api

Command to execute all Cucumber features in the project. This command assumes Cucumber is installed and configured in the project's environment.

```bash
cucumber
```

--------------------------------

### Install Cucumber-JS with Yarn

Source: https://cucumber.io/docs/installation/javascript

Installs the Cucumber-JS package as a development dependency in a Node.js project using Yarn. This command adds `@cucumber/cucumber` to your project's `devDependencies` in `package.json`.

```bash
yarn add --dev @cucumber/cucumber
```

--------------------------------

### Declarative Cucumber Feature File Example

Source: https://cucumber.io/docs/bdd/better-gherkin

An example of a Cucumber feature file written in a declarative style. This style focuses on the behavior and intent, making scenarios more resilient to implementation changes.

```gherkin
Feature: Subscribers see different articles based on their subscription level  
   
Scenario: Free subscribers see only the free articles  
  Given Free Frieda has a free subscription  
  When Free Frieda logs in with her valid credentials  
  Then she sees a Free article  
  
Scenario: Subscriber with a paid subscription can access both free and paid articles  
  Given Paid Patty has a basic-level paid subscription  
  When Paid Patty logs in with her valid credentials  
  Then she sees a Free article and a Paid article  

```

--------------------------------

### Cucumber Step Example: Splitting Compound Steps

Source: https://cucumber.io/docs/bdd/who-does-what

Demonstrates how to split a single step containing multiple actions into separate, more readable steps using Cucumber's 'And' keyword. This improves clarity and maintainability of feature files.

```gherkin
When I fill in the "Name" field and the "Address" field
```

```gherkin
When I fill in the "Name" field
And I fill in the "Address" field
```

--------------------------------

### Execute Multiple Cucumber Profiles

Source: https://cucumber.io/docs/cucumber/configuration

This command-line example demonstrates executing Cucumber with multiple profiles simultaneously. By specifying multiple `-p` flags, Cucumber will combine the options from all listed profiles for a comprehensive test run.

```bash
[user@system project] cucumber -p html_report -p bvt  
```

--------------------------------

### Gherkin: Feature-Level Background Setup

Source: https://cucumber.io/docs/gherkin/reference

Illustrates the use of the Background keyword in Gherkin to define common Given steps that are executed before each scenario within a Feature. This reduces repetition for incidental details.

```gherkin
Feature: Multiple site support  
  Only blog owners can post to a blog, except administrators,  
  who can post to all blogs.  
  
  Background:  
    Given a global administrator named "Greg"  
    And a blog named "Greg's anti-tax rants"  
    And a customer named "Dr. Bill"  
    And a blog named "Expensive Therapy" owned by "Dr. Bill"  
  
  Scenario: Dr. Bill posts to his own blog  
    Given I am logged in as Dr. Bill  
    When I try to post to "Expensive Therapy"  
    Then I should see "Your article was published."  
  
  Scenario: Dr. Bill tries to post to somebody else's blog, and fails  
    Given I am logged in as Dr. Bill  
    When I try to post to "Greg's anti-tax rants"  
    Then I should see "Hey! That's not your blog!"  
  
  Scenario: Greg posts to a client's blog  
    Given I am logged in as Greg  
    When I try to post to "Expensive Therapy"  
    Then I should see "Your article was published."  
```

--------------------------------

### Gherkin: Rule-Level Background Setup

Source: https://cucumber.io/docs/gherkin/reference

Shows how the Background keyword can be applied at the Rule level in Gherkin to set up common preconditions for scenarios within that specific Rule, providing more granular context management.

```gherkin
Feature: Overdue tasks  
  Let users know when tasks are overdue, even when using other  
  features of the app  
  
  Rule: Users are notified about overdue tasks on first use of the day  
    Background:  
      Given I have overdue tasks  
  
    Example: First use of the day  
      Given I last used the app yesterday  
      When I use the app  
      Then I am notified about overdue tasks  
  
    Example: Already used today  
      Given I last used the app earlier today  
      When I use the app  
      Then I am not notified about overdue tasks  
  ...  
```

--------------------------------

### BeforeStep Hook Examples

Source: https://cucumber.io/docs/cucumber/api

Defines actions to be performed before each step. Supports annotated methods and lambda styles in Java, Kotlin, Scala, and JavaScript. Cucumber-Ruby does not support BeforeStep hooks.

```java
@BeforeStep
public void doSomethingBeforeStep(Scenario scenario){
}

```

```kotlin
BeforeStep { scenario: Scenario ->
  // doSomething
}

```

```scala
BeforeStep { scenario: Scenario =>
  // doSomething
}

```

```javascript
BeforeStep(async function({pickle, pickleStep, gherkinDocument, testCaseStartedId, testStepId}) {
    // doSomething
})

BeforeStep({tags: "@foo"}, async function() {
    // apply this hook to only specific scenarios
})

```

--------------------------------

### Cucumber Step Example: Ensuring Step Consistency

Source: https://cucumber.io/docs/bdd/who-does-what

Illustrates the importance of using consistent phrasing for identical step definitions in Cucumber feature files. This avoids ambiguity and ensures that the same action is always represented in the same way.

```gherkin
Given I am logged in
```

```gherkin
Given I have logged in to the site
```

--------------------------------

### Cucumber UI Test with Selenium WebDriver (Kotlin)

Source: https://cucumber.io/docs/guides/browser-automation

Kotlin implementation of Cucumber step definitions for UI testing using Selenium WebDriver. It mirrors the Java example, providing steps for Google search and title verification. Requires Selenium WebDriver and Cucumber Kotlin dependencies.

```kotlin
package com.example
  
import io.cucumber.java8.Scenario
import io.cucumber.java8.En
import org.openqa.selenium.By
import org.openqa.selenium.WebDriver
import org.openqa.selenium.WebElement
import org.openqa.selenium.support.ui.WebDriverWait
  
class ExampleSteps: En {
  
    lateinit var driver: WebDriver
  
    init {
        Given("I am on the Google search page") {
            driver.get("https:\www.google.com")
        }
  
        When("I search for {string}") { query: String ->
            val element: WebElement = driver.findElement(By.name("q"))
            // Enter something to search for
            element.sendKeys(query)
            // Now submit the form. WebDriver will find the form for us from the element
            element.submit()
        }
  
        Then("the page title should start with {string}") { titleStartsWith: String ->
            // Google's search is rendered dynamically with JavaScript
            // Wait for the page to load timeout after ten seconds
            WebDriverWait(driver, 10L).until { d ->
                d.title.toLowerCase().startsWith(titleStartsWith)
            }
        }
  
        After { scenario: Scenario ->
            driver.quit()
        }
    }
}
```

--------------------------------

### Imperative Cucumber Feature File Example

Source: https://cucumber.io/docs/bdd/better-gherkin

An example of a Cucumber feature file written in an imperative style. This style details specific user actions and expected outcomes, making it brittle to UI changes.

```gherkin
Feature: Subscribers see different articles based on their subscription level   
  
Scenario: Free subscribers see only the free articles  
  Given users with a free subscription can access "FreeArticle1" but not "PaidArticle1"   
  When I type "freeFrieda@example.com" in the email field  
  And I type "validPassword123" in the password field  
  And I press the "Submit" button  
  Then I see "FreeArticle1" on the home page  
  And I do not see "PaidArticle1" on the home page  
  
Scenario: Subscriber with a paid subscription can access "FreeArticle1" and "PaidArticle1"  
  Given I am on the login page  
  When I type "paidPattya@example.com" in the email field  
  And I type "validPassword123" in the password field  
  And I press the "Submit" button  
  Then I see "FreeArticle1" and "PaidArticle1" on the home page    

```

--------------------------------

### Gherkin Rule Keyword Example

Source: https://cucumber.io/docs/gherkin/reference

Illustrates the use of the 'Rule' keyword in Gherkin to represent a business rule and group related scenarios. This example shows two rules with associated scenarios.

```gherkin
# -- FILE: features/gherkin.rule_example.feature  
Feature: Highlander  
  
  Rule: There can be only One  
  
    Example: Only One -- More than one alive  
      Given there are 3 ninjas  
      And there are more than one ninja alive  
      When 2 ninjas meet, they will fight  
      Then one ninja dies (but not me)  
      And there is one ninja less alive  
  
    Example: Only One -- One alive  
      Given there is only 1 ninja alive  
      Then they will live forever ;-)  
  
  Rule: There can be Two (in some cases)  
  
    Example: Two -- Dead and Reborn as Phoenix  
      ...  

```

--------------------------------

### Configure Cucumber Java Run Configuration in IntelliJ IDEA

Source: https://cucumber.io/docs/faq

This guide explains how to set up a Cucumber Java run configuration in IntelliJ IDEA when step definitions are not automatically recognized. It involves creating a new run configuration and optionally specifying the glue package.

```text
1. Click **Run** > **Edit Configurations** from the menu in IntelliJ IDEA.
2. Click the **+** icon on the top-left and type in _cucumber_. Select **Cucumber Java**.
3. Create the configuration according to the Run/Debug Configuration Cucumber Java instructions from JetBrains.

If IntelliJ IDEA doesn't recognize the package with step definitions, you can specify it manually by entering the package name in the Glue field, for example _stepdefs_.
```

--------------------------------

### Execute Cucumber Profile using CLI

Source: https://cucumber.io/docs/cucumber/configuration

These command-line examples demonstrate how to execute Cucumber with a defined profile. The `--profile` flag (or its shorthand `-p`) is used to specify which profile from `cucumber.yml` should be applied.

```bash
[user@system project] cucumber --profile html_report  
```

```bash
[user@system project] cucumber -p bvt  
```

--------------------------------

### Norwegian Gherkin Scenario Example

Source: https://cucumber.io/docs/gherkin/reference

Provides an example of a Gherkin scenario written in Norwegian, demonstrating Cucumber's support for over 70 languages. This allows teams to write specifications in their natural language.

```gherkin
# This is a placeholder for a Norwegian Gherkin scenario.
# Example:
# Scenario: Enkel kalkulasjon
#   Gitt at jeg har 5 epler
#   Når jeg legger til 3 epler
#   Så skal jeg ha 8 epler
```

--------------------------------

### Execute Default Cucumber Profile

Source: https://cucumber.io/docs/cucumber/configuration

This command-line example shows how to execute Cucumber when a `default` profile is configured in `cucumber.yml`. Simply running the `cucumber` command without any profile flags will invoke the default settings.

```bash
[user@system project] cucumber  
```

--------------------------------

### Step Definition for 'edit_work_experience.feature' (JavaScript)

Source: https://cucumber.io/docs/guides/anti-patterns

JavaScript implementation of a step definition for the 'edit_work_experience.feature' scenario. This example uses the 'cucumber' library to define a step that creates an Employee and their CV.

```javascript
var { Given } = require('cucumber');  
  
Given(/^I have a CV and I'm on the edit description page$/, function () {  
  this.employee = new Employee('Sally');  
  this.employee.createCV();  
});  
```

--------------------------------

### JavaScript Node.js Assert Module Example

Source: https://cucumber.io/docs/cucumber/checking-assertions

An example of a Cucumber 'Then' step definition in JavaScript using Node.js' built-in 'assert' module. It asserts that the actual result (stored in 'this.actual') is equal to the expected value provided as an argument.

```javascript
const assert = require('assert')

Then('the result should be {word}', function (expected) {
  // this.actual is typically set in a previous step
  assert.equal(this.actual, expected)
})
```

--------------------------------

### Run Cucumber Tests with Specific Browser in Ruby

Source: https://cucumber.io/docs/guides/browser-automation

Command-line example for running Cucumber tests with a specified browser in Ruby. This command sets the 'browser' environment variable to 'chrome' before executing Cucumber.

```shell
browser=chrome cucumber
```

--------------------------------

### Ruby RSpec Assertion Example

Source: https://cucumber.io/docs/cucumber/checking-assertions

An example of a Cucumber step definition in Ruby using RSpec's 'expect' syntax. It asserts that a 'bike' object 'be_shiny'. This assumes 'bike' is defined in the step's context.

```ruby
Given /^a nice new bike$/ do
  expect(bike).to be_shiny
end
```

--------------------------------

### Web Browser Automation with Watir (Ruby)

Source: https://cucumber.io/docs/guides/browser-automation

Demonstrates web browser automation using the Watir library in Ruby. It sets up a Firefox browser, navigates to Google, performs a search, and asserts the resulting page title. Requires the 'watir' and 'rspec' gems.

```ruby
require "rubygems"  
require "rspec"  
require "watir"  
  
describe "google.com" do  
  let(:browser) { @browser ||= Watir::Browser.new :firefox }  
  before { browser.goto "http://google.com" }  
  browser.text_field(name: "q").set "watir"  
  browser.button.click  
  browser.div(id: "resultStats").wait_until  
  browser.title.should == "watir - Google Search"  
  after { browser.close }  
end  
```

--------------------------------

### Java JUnit 4 Assertion Example

Source: https://cucumber.io/docs/cucumber/checking-assertions

An example of a Cucumber 'Then' step definition in Java using JUnit 4's 'assertEquals' method. This step compares an expected integer value with an actual result, which is assumed to be available in a variable named 'result'.

```java
import static org.junit.Assert.*;

public class Example {

    @Then("the result should be {int}")
    public void the_result_should_be(int expectedResult) {
        assertEquals(expectedResult, result);
    }
```

--------------------------------

### Cucumber Command Line Tag Filtering

Source: https://cucumber.io/docs/cucumber/api

Provides examples of using command-line options to filter Cucumber scenarios based on tags. It demonstrates tag negation and the combination logic for tag options.

```bash
cucumber --tags=@authentication  
Using the default profile...  
  
0 scenarios  
0 steps  
0m0.000s  

```

```bash
cucumber --tags=@wip:3 features/log\*  

```

--------------------------------

### Gherkin: Avoid Implementation Details (How)

Source: https://cucumber.io/docs/bdd/better-gherkin

This Gherkin snippet illustrates an example of procedural Gherkin that describes implementation details. It details the exact steps and UI interactions, making it brittle and prone to breaking with minor code changes. It's recommended to avoid this style for better maintainability.

```gherkin
Given I visit "/login"
When I enter "Bob" in the "user name" field
  And I enter "tester" in the "password" field
  And I press the "login" button
Then I should see the "welcome" page
```

--------------------------------

### Run Cucumber.js from Node Modules

Source: https://cucumber.io/docs/cucumber/api

Executes Cucumber.js tests using the executable file located in the project's `node_modules` directory. This is the standard way to run JavaScript Cucumber tests after installation.

```bash
./node_modules/.bin/cucumber.js  
```

--------------------------------

### Cucumber Configuration File for JavaScript

Source: https://cucumber.io/docs/cucumber/configuration

This example shows the file path for a Cucumber configuration file used in JavaScript projects. The `cucumber.yml` or `cucumber.yaml` file should reside in a `.config` directory or a `config` subdirectory.

```yaml
config/cucumber.yml
```

--------------------------------

### Ruby RSpec Configuration Example

Source: https://cucumber.io/docs/cucumber/checking-assertions

This Ruby code snippet shows how to configure RSpec syntax within your Cucumber project's environment file (features/support/env.rb). It explicitly sets the expectation syntax to ':expect'.

```ruby
RSpec.configure do |config|
  config.expect_with :rspec do |c|
    c.syntax = :expect
  end
end
```

--------------------------------

### Passing Environment Variables via Command Line

Source: https://cucumber.io/docs/cucumber/configuration

This example demonstrates how to pass environment variables directly on the command line when running Cucumber. The `FOO=BAR` part sets the environment variable `FOO` to the value `BAR` for the duration of the Cucumber execution.

```bash
cucumber FOO=BAR --format progress features
```

--------------------------------

### Configure Glue Path for Cucumber-JVM Step Definitions

Source: https://cucumber.io/docs/faq

Specifies how to configure the glue path in Cucumber-JVM to ensure step definitions are found. This is crucial when Cucumber reports steps as undefined despite implementation. It allows explicit definition of packages to search for step definitions.

```java
@CucumberOptions(glue = {"<package>", "<package>", "<etc>"})  
public class RunCucumberTest{}
```

```kotlin
@CucumberOptions(glue = ["<package>", "<package>", "<etc>"])  
class RunCucumberTest
```

--------------------------------

### Cucumber Options - Custom Object Factory

Source: https://cucumber.io/docs/cucumber/api

Example of specifying a custom object factory for Cucumber using the `objectFactory` option in `@CucumberOptions`. This is useful when integrating Cucumber with Dependency Injection frameworks.

```java
@CucumberOptions(objectFactory = FooFactory.class)
```

--------------------------------

### Cucumber Doc String Example with Content Type Annotation

Source: https://cucumber.io/docs/gherkin/reference

Demonstrates annotating a Doc String with its content type (e.g., 'markdown') immediately after the opening delimiter. This helps tools and step definitions understand the nature of the enclosed text, although tool support may vary.

```gherkin
Given a blog post named "Random" with Markdown body
  """markdown
  Some Title, Eh?
  ===============
  Here is the first paragraph of my blog post. Lorem ipsum dolor sit amet,
  consectetur adipiscing elit.
  """
```

--------------------------------

### Cucumber Options - Snippets and Summary Plugin

Source: https://cucumber.io/docs/cucumber/api

Example of configuring Cucumber to use the 'summary' plugin and generate code snippets in CAMELCASE format. The 'summary' plugin provides a summary of test execution, and CAMELCASE affects the naming convention of generated step definition snippets.

```java
@CucumberOptions(plugin = {"pretty", "summary"}, snippets = SnippetType.CAMELCASE)
```

--------------------------------

### Advanced Tag Expressions

Source: https://cucumber.io/docs/cucumber/api

Provides examples of complex tag expressions using boolean operators like AND, OR, and NOT, along with parentheses for controlling precedence. These expressions allow for sophisticated scenario filtering.

```gherkin
(@smoke or @ui) and (not @slow)  

```

--------------------------------

### Cucumber Doc String Example with Triple Double Quotes

Source: https://cucumber.io/docs/gherkin/reference

Shows how to pass a large block of text to a step definition using a Doc String. The text is enclosed in triple double quotes (`"""`). Indentation of the opening quotes is flexible, but indentation within the quotes is significant and preserved.

```gherkin
Given a blog post named "Random" with Markdown body
  """
  Some Title, Eh?
  ===============
  Here is the first paragraph of my blog post. Lorem ipsum dolor sit amet,
  consectetur adipiscing elit.
  """
```

--------------------------------

### Cucumber Doc String Example with Triple Backticks

Source: https://cucumber.io/docs/gherkin/reference

Illustrates using triple backticks (```) as an alternative delimiter for Doc Strings. This syntax is similar to Markdown and can be useful for embedding code or formatted text within scenarios.

```gherkin
Given a blog post named "Random" with Markdown body
  ```
  Some Title, Eh?
  ===============
  Here is the first paragraph of my blog post. Lorem ipsum dolor sit amet,
  consectetur adipiscing elit.
  ```
```

--------------------------------

### Cucumber Options - Monochrome Output

Source: https://cucumber.io/docs/cucumber/api

Example of configuring Cucumber to use monochrome output with `monochrome=true` in `@CucumberOptions`. This setting disables colorized output in the console, making it more readable in certain environments.

```java
@CucumberOptions(monochrome=true)
```

--------------------------------

### Compile Step Definitions using CLI

Source: https://cucumber.io/docs/guides/parallel-execution

This command compiles the Java step definition file using the javac compiler. It includes the necessary Cucumber JARs in the classpath using the -cp option, preparing the code for execution via the CLI.

```bash
javac -cp .;<path to cucumber jar folder>/* ./parallel/StepDefs.java
```

--------------------------------

### JavaScript Chai Assertion Example

Source: https://cucumber.io/docs/cucumber/checking-assertions

This JavaScript code snippet demonstrates a Cucumber 'Then' step using the Chai assertion library. It uses the 'expect' interface to assert that the actual result is deeply equal to the expected value.

```javascript
const { expect } = require('chai')

Then('the result should be {word}', function (expected) {
  expect(this.actual).to.eql(expected)
})
```

--------------------------------

### Cucumber Options - Tag Selection

Source: https://cucumber.io/docs/cucumber/api

Example of configuring Cucumber to run specific scenarios using tags. The `tags` option in `@CucumberOptions` allows filtering scenarios based on specified tag expressions, such as running scenarios tagged with '@foo' but not '@bar'.

```java
@CucumberOptions(tags = "@foo and not @bar")
```

--------------------------------

### Accessing Environment Variables in Ruby

Source: https://cucumber.io/docs/cucumber/configuration

This snippet shows how to access environment variables within Ruby code, such as in `env.rb` or step definitions. The example uses `ENV['FOO']` to retrieve the value of the `FOO` environment variable, which was set previously.

```ruby
# In env.rb or a Step Definition
foo_value = ENV['FOO']
puts "The value of FOO is: #{foo_value}"
```

--------------------------------

### Navigate to Project Directory

Source: https://cucumber.io/docs/guides/10-minute-tutorial

Changes the current directory to the newly created Cucumber project. This command is essential for running subsequent build and test commands within the project's context.

```bash
cd hellocucumber
```

--------------------------------

### Configuring Cucumber Profiles with Environment Variables (YAML)

Source: https://cucumber.io/docs/cucumber/configuration

This snippet shows how to define profiles in a `cucumber.yml` file that set environment variables. These variables can then be used by step definitions. For example, the 'ie' profile sets the BROWSER environment variable to 'IE'.

```yaml
default: --profile html_report --profile bvt
html_report: --format progress --format html --out=features_report.html
bvt: --tags @bvt
ie: BROWSER=IE
```

--------------------------------

### Cucumber Data Table Example

Source: https://cucumber.io/docs/gherkin/reference

Presents a Data Table used to pass structured data to a step definition. The table is defined using pipe symbols (`|`) to separate cells. It's passed as the last argument to the corresponding step.

```gherkin
Given the following users exist:
  | name   | email              | twitter         |
  | Aslak  | aslak@cucumber.io  | @aslak_hellesoy |
  | Julien | julien@cucumber.io | @jbpros         |
  | Matt   | matt@cucumber.io   | @mattwynne      |
```

--------------------------------

### Cucumber Options - Dry Run Configuration

Source: https://cucumber.io/docs/cucumber/api

Example of configuring Cucumber to perform a dry run using the `dryRun=true` option within `@CucumberOptions`. A dry run checks if all feature file steps have corresponding step definitions without actually executing the steps.

```java
@CucumberOptions(dryRun=true)
```

--------------------------------

### Guard Cucumber Rake Task

Source: https://cucumber.io/docs/tools/ruby

This Ruby code provides a robust Rake task definition for Cucumber that includes error handling. It attempts to load the Cucumber Rake task and defines a fallback task that informs the user if Cucumber is not installed.

```ruby
require 'rubygems'  

begin  
  require 'cucumber'  
  require 'cucumber/rake/task'  

  Cucumber::Rake::Task.new(:features) do |t|  
    t.cucumber_opts = "--format pretty"  
  end  

  task features: 'db:test:prepare'  
rescue LoadError  
  desc 'Cucumber rake task not available'  
  task :features do  
    abort 'Cucumber rake task is not available. Be sure to install cucumber as a gem or plugin'  
  end  
end  

```

--------------------------------

### Cucumber Data Table to List<String> in Scala

Source: https://cucumber.io/docs/cucumber/api

Provides an example of using a Gherkin data table as a list of strings in a Scala step definition. Note that Cucumber Scala currently does not support Scala collection types directly for data tables.

```gherkin
Given the following animals:
| cow |
| horse |
| sheep |
```

```scala
Given("the following animals:") { animals: java.util.List[String] =>
}
```

--------------------------------

### Write a Gherkin Feature File for Cucumber

Source: https://cucumber.io/docs/guides/10-minute-tutorial

Defines a feature and a scenario using Gherkin syntax for Cucumber. This `.feature` file acts as an executable specification, outlining the desired behavior of the software. It includes `Feature`, `Scenario`, `Given`, `When`, and `Then` keywords.

```gherkin
Feature: Is it Friday yet? 
  Everybody wants to know when it's Friday  

  Scenario: Sunday isn't Friday  
    Given today is Sunday  
    When I ask whether it's Friday yet  
    Then I should be told "Nope"
```

--------------------------------

### Define Cucumber Rake Task

Source: https://cucumber.io/docs/tools/ruby

This Ruby code defines a Rake task for running Cucumber tests. It requires the cucumber gem and sets up a 'features' task that can accept command-line options via `cucumber_opts`. This is a common setup for automating Cucumber execution in Ruby projects.

```ruby
require 'rubygems'  
require 'cucumber'  
require 'cucumber/rake/task'  

Cucumber::Rake::Task.new(:features) do |t|  
  t.cucumber_opts = "--format pretty" # Any valid command line option can go here.  
end  

```

--------------------------------

### Maven Surefire/Failsafe Plugin - Parallel Options

Source: https://cucumber.io/docs/guides/parallel-execution

Configuration to set different parallelization strategies for Maven Surefire or Failsafe plugins, such as 'classesAndMethods' or 'classes'.

```xml
<configuration>  
	<parallel>classesAndMethods</parallel>  
	useUnlimitedThreads>true</useUnlimitedThreads>  
</configuration>  

```

--------------------------------

### Running Scenarios with Tags using Maven

Source: https://cucumber.io/docs/cucumber/api

Shows how to execute specific scenarios using Maven by filtering tags via a JVM system property. This allows for targeted test runs based on tag expressions.

```bash
mvn test -Dcucumber.filter.tags="@smoke and @fast"  

```

--------------------------------

### Kotlin Package Level Functions for Hooks

Source: https://cucumber.io/docs/cucumber/api

Demonstrates using package-level functions in Kotlin for BeforeAll and AfterAll hooks to avoid issues with companion objects.

```Kotlin
package io.cucumber.example

import io.cucumber.java.AfterAll
import io.cucumber.java.BeforeAll

@BeforeAll
fun beforeAll() {
   println("before all")
}

@AfterAll
fun afterAll() {
   println("after all")
}

```

--------------------------------

### Configure WebDriver for Multiple Browsers in Java

Source: https://cucumber.io/docs/guides/browser-automation

This Java code snippet demonstrates a factory class to create WebDriver instances based on a runtime 'browser' system property. It supports 'firefox' and 'chrome', throwing an exception for unsupported browsers. Dependencies include Selenium WebDriver.

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class WebDriverFactory {
    public static WebDriver createWebDriver() {
        String webdriver = System.getProperty("browser", "firefox");
        switch(webdriver) {
            case "firefox":
                return new FirefoxDriver();
            case "chrome":
                return new ChromeDriver();
            default:
                throw new RuntimeException("Unsupported webdriver: " + webdriver);
        }
    }
}
```

--------------------------------

### Acceptance Criteria using Gherkin Syntax

Source: https://cucumber.io/docs/terms/user-story

Demonstrates the structure of acceptance criteria written in Gherkin, a business-readable domain-specific language. It shows how to define features and scenarios with Given, When, Then steps.

```gherkin
Feature: Some important feature  
  
  Scenario: Get something  
    Given I have something  
    When I do something  
    Then I get something else  
  
  Scenario: Get something different  
    Given I have something  
    And I have also some other thing  
    When I do something different  
    Then I get something different  


```

```gherkin
Feature: Some important feature  
  
  Scenario: Do not show balance if not logged in  
    Given I am not logged on to the mobile banking app  
    When I open the mobile banking app  
    Then I can see a login page  
    And I do not see account balance  
  
  Scenario: Show balance on the accounts page after logging in  
    Given I have just logged on to the mobile banking app  
    When I load the accounts page  
    Then I can see account balance for each of my accounts  


```

--------------------------------

### Generate Timeline Report via Cucumber CLI

Source: https://cucumber.io/docs/guides/parallel-execution

This command demonstrates how to generate the timeline report using the Cucumber command-line interface. It specifies the timeline plugin, the report folder, the number of threads, the steps package, and the path to feature files. Ensure to replace placeholders like '<classpath>', '<report folder>', '<thread count>', '<steps package>', and '<path to feature files>' with actual values.

```bash
java -cp <classpath> io.cucumber.core.cli.Main -p timeline:<report folder> --threads <thread count> -g <steps package> <path to feature files>

```

--------------------------------

### Maven Surefire/Failsafe Plugin - Thread Count Across All Cores

Source: https://cucumber.io/docs/guides/parallel-execution

Configuration to set a specific thread count that applies across all CPU cores, rather than per core. 'perCoreThreadCount' is set to 'false'.

```xml
<configuration>  
	<parallel>methods</parallel>  
	<threadCount>4</threadCount>  
	<perCoreThreadCount>false</perCoreThreadCount>  
</configuration>  

```

--------------------------------

### Run Cucumber with Rake

Source: https://cucumber.io/docs/tools/ruby

This command demonstrates the simplest way to execute Cucumber tests using Rake. Assuming a Rakefile is configured with a 'features' task, this command initiates the test run.

```shell
rake features  

```

--------------------------------

### Implement Undefined Cucumber Steps (Java)

Source: https://cucumber.io/docs/guides/10-minute-tutorial

This snippet shows how to implement undefined steps in Cucumber using Java. It includes the necessary annotations (@Given, @When, @Then) and a placeholder for the step logic. These snippets are generated by Cucumber when steps are not yet defined.

```java
@Given("today is Sunday")
public void today_is_sunday() {
    // Write code here that turns the phrase above into concrete actions
    throw new io.cucumber.java.PendingException();
}
@When("I ask whether it's Friday yet")
public void i_ask_whether_it_s_friday_yet() {
    // Write code here that turns the phrase above into concrete actions
    throw new io.cucumber.java.PendingException();
}
@Then("I should be told {string}")
public void i_should_be_told(String string) {
    // Write code here that turns the phrase above into concrete actions
    throw new io.cucumber.java.PendingException();
}
```

--------------------------------

### Cucumber Test Execution Output

Source: https://cucumber.io/docs/guides/10-minute-tutorial

This output shows the results of running the Cucumber tests after updating the feature file and step definitions. It confirms that all scenarios, including those using the scenario outline, have passed successfully.

```text
-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running hellocucumber.RunCucumberTest
Feature: Is it Friday yet?
  Everybody wants to know when it's Friday

  Scenario Outline: Today is or is not Friday # hellocucumber/is_it_friday_yet.feature:4
    Given today is "<day>"
    When I ask whether it's Friday yet
    Then I should be told "<answer>"

    Examples:

  Scenario Outline: Today is or is not Friday # hellocucumber/is_it_friday_yet.feature:11
    Given today is "Friday"                   # StepDefinitions.today_is(String)
    When I ask whether it's Friday yet        # StepDefinitions.i_ask_whether_it_s_Friday_yet()
    Then I should be told "TGIF"              # StepDefinitions.i_should_be_told(String)

  Scenario Outline: Today is or is not Friday # hellocucumber/is_it_friday_yet.feature:12
    Given today is "Sunday"                   # StepDefinitions.today_is(String)
    When I ask whether it's Friday yet        # StepDefinitions.i_ask_whether_it_s_Friday_yet()
    Then I should be told "Nope"              # StepDefinitions.i_should_be_told(String)

  Scenario Outline: Today is or is not Friday # hellocucumber/is_it_friday_yet.feature:13
    Given today is "anything else!"           # StepDefinitions.today_is(String)
    When I ask whether it's Friday yet        # StepDefinitions.i_ask_whether_it_s_Friday_yet()
    Then I should be told "Nope"              # StepDefinitions.i_should_be_told(String)

3 Scenarios (3 passed)
9 Steps (9 passed)
0m0.255s

```

--------------------------------

### Kotlin Step Definition for Gherkin

Source: https://cucumber.io/docs/cucumber/step-definitions

Provides Kotlin implementations for Cucumber step definitions. It demonstrates how to link Gherkin steps to Kotlin functions using both a standard approach and the Java 8 lambda style syntax.

```Kotlin
package com.example
import io.cucumber.java8.En

class StepDefinitions : En {

    init {
        Given("I have {int} cukes in my belly") { cukes: Int ->
                println("Cukes: $cukes")
        }
    }

}
```

```Kotlin
package com.example
import io.cucumber.scala.{ScalaDsl, EN}

class StepDefinitions extends ScalaDsl with EN {

    Given("I have {int} cukes in my belly") { cukes: Int =>
        println(s"Cukes: $cukes")
    }

}
```

--------------------------------

### Java Cucumber Step Definitions for 'Is it Friday?'

Source: https://cucumber.io/docs/guides/10-minute-tutorial

This Java code defines the step definitions for a Cucumber scenario. It uses the io.cucumber.java.en annotations to link Gherkin steps to Java methods. The code includes a helper class 'IsItFriday' and the main 'StepDefinitions' class with assertions using AssertJ.

```java
package hellocucumber;  
  
import io.cucumber.java.en.Given;  
import io.cucumber.java.en.When;  
import io.cucumber.java.en.Then;  
import static org.assertj.core.api.Assertions.assertThat;  
  
class IsItFriday {  
    static String isItFriday(String today) {  
        return null;  
    }  
}  
  
public class StepDefinitions {  
    private String today;  
    private String actualAnswer;  
  
    @Given("today is Sunday")  
    public void today_is_Sunday() {  
        today = "Sunday";  
    }
    @When("I ask whether it's Friday yet")  
    public void i_ask_whether_it_s_Friday_yet() {  
        actualAnswer = IsItFriday.isItFriday(today);  
    }  
  
    @Then("I should be told {string}")  
    public void i_should_be_told(String expectedAnswer) {  
        assertThat(actualAnswer).isEqualTo(expectedAnswer);  
    }  
}  

```

--------------------------------

### Cucumber Step Definitions in Java

Source: https://cucumber.io/docs/guides/parallel-execution

Java class containing step definitions for Cucumber scenarios. It uses the @Given annotation to map Gherkin steps to Java methods and prints the current thread ID.

```java
package parallel;  
  
import io.cucumber.java.BeforeStep;  
import io.cucumber.java.en.Given;  
  
public class StepDefinitions {  
  
	@Given("Step from {string} in {string} feature file")  
	public void step(String scenario, String file) {  
		System.out.format("Thread ID - %2d - %s from %s feature file.\n",  
		Thread.currentThread().getId(), scenario,file);  
	}
}

```

--------------------------------

### Before Hook: Lambda Style (Kotlin)

Source: https://cucumber.io/docs/cucumber/api

Executes code before the first step of each scenario using a lambda expression in Kotlin. Supports specifying an execution order.

```Kotlin
Before { scenario: Scenario ->
    // doSomething
}

Before(10) { scenario: Scenario ->
    // Do something before each scenario
}

```

--------------------------------

### Ruby Step Definition for Gherkin

Source: https://cucumber.io/docs/cucumber/step-definitions

Shows how to define a step definition in Ruby for Cucumber. It uses a block syntax to associate the Gherkin step text with the corresponding Ruby code to be executed.

```Ruby
Given('I have {int} cukes in my belly') do |cukes|
  puts "Cukes: #{cukes}"
end
```

--------------------------------

### Kotlin Step Definition with Regular Expressions

Source: https://cucumber.io/docs/cucumber/step-definitions

Shows a Kotlin step definition using a regular expression. Capture groups from the regex are passed as arguments to the Kotlin function.

```Kotlin
Given("I have {int} cukes in my belly") { cukes: Int ->
        println("Cukes: $cukes")
}
```

```Kotlin
Given("I have {int} cukes in my belly") { cukes: Int =>
    println(s"Cukes: $cukes")
}
```

--------------------------------

### Running Cucumber with Ruby

Source: https://cucumber.io/docs/cucumber/api

Describes the execution method for Cucumber when used with Ruby projects. It is launched using the `cucumber` command from the command line or via build scripts.

```bash
cucumber  

```

--------------------------------

### Gherkin: Using Asterisk (*) for List Steps

Source: https://cucumber.io/docs/gherkin/reference

Demonstrates how to use the asterisk (*) as a wildcard in Gherkin steps to represent lists, improving readability by allowing a more bullet-point-like structure.

```gherkin
Scenario: All done  
  Given I am out shopping  
  * I have eggs  
  * I have milk  
  * I have butter  
  When I check my list  
  Then I don't need anything  
```

--------------------------------

### Configure TestNG Runner for Parallel Execution

Source: https://cucumber.io/docs/guides/parallel-execution

This Java code extends AbstractTestNGCucumberTests and overrides the scenarios method to enable parallel execution. The DataProvider annotation with parallel=true is crucial for this functionality. It requires TestNG and Cucumber TestNG dependencies.

```java
package parallel;
  
import org.testng.annotations.DataProvider;
import io.cucumber.testng.AbstractTestNGCucumberTests;
  
public class RunCucumberTest extends AbstractTestNGCucumberTests{
  
	@Override
	@DataProvider(parallel = true)
	public Object[][] scenarios() {
		return super.scenarios();
	}
}
```

--------------------------------

### Gherkin: Describe Behavior (What)

Source: https://cucumber.io/docs/bdd/better-gherkin

This Gherkin snippet demonstrates how to describe the intended behavior of a system. It focuses on the 'what' the system should do, making scenarios more abstract and resilient to implementation changes. This approach leads to shorter, more understandable tests.

```gherkin
When "Bob" logs in
```

--------------------------------

### Google Search Automation with Selenium WebDriver (Ruby)

Source: https://cucumber.io/docs/guides/browser-automation

Automates Google searches using Selenium WebDriver with Ruby. It navigates to Google, searches for a term, and verifies the page title. Requires the Selenium WebDriver gem.

```ruby
Given(/^I am on the Google search page$/) do  
  driver = Selenium::WebDriver.for :firefox  
  driver.get "http://google.com"  
end  
  
When(/^I search for "([^"]*)"$/) do  
  element = driver.find_element(name: "q")  
  element.send_keys "Cheese!"  
  element.submit  
end  
  
Then(/^the page title should start with "([^"]*)"$/) do  
  wait = Selenium::WebDriver::Wait.new(timeout: 10)  
  wait.until { driver.title.downcase.start_with? "cheese!" }  
  puts "Page title is #{driver.title}"  
    browser.close  
end  
```

--------------------------------

### Run WIP Scenarios with Rake

Source: https://cucumber.io/docs/tools/ruby

This Rake command executes only those Cucumber scenarios tagged with '@wip'. This is useful for focusing on work-in-progress features during development.

```shell
rake cucumber:wip

```

--------------------------------

### Maven Failsafe Plugin Configuration for Parallel Execution

Source: https://cucumber.io/docs/guides/parallel-execution

Maven Failsafe plugin configuration in the POM file for parallel integration test execution. It includes goals for integration-test and verify, and enables parallel execution with unlimited threads.

```xml
<plugin>  
	<groupId>org.apache.maven.plugins</groupId>  
	<artifactId>maven-failsafe-plugin</artifactId>  
	<version>2.22.0</version>  
	<executions>  
		<execution>  
			<goals>  
				<goal>integration-test</goal>  
				<goal>verify</goal>  
			</goals>  
			<configuration>  
				<parallel>methods</parallel>  
				<useUnlimitedThreads>true</useUnlimitedThreads>  
			</configuration>  
		</execution>  
	</executions>  
</plugin>  

```

--------------------------------

### Configure Maven Surefire Plugin for Parallel Execution

Source: https://cucumber.io/docs/guides/parallel-execution

This XML snippet configures the Maven Surefire plugin in the POM.xml file. It specifies the plugin version and is essential for enabling parallel test execution when using TestNG as the test runner.

```xml
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-surefire-plugin</artifactId>
	<version>2.22.0</version>
</plugin>
```

--------------------------------

### Cucumber Feature File: Is it Friday yet?

Source: https://cucumber.io/docs/guides/10-minute-tutorial

Defines the 'Is it Friday yet?' feature with two scenarios: one for Sunday and one for Friday. This file serves as the specification for the test automation.

```gherkin
Feature: Is it Friday yet?  
  Everybody wants to know when it's Friday  
  
  Scenario: Sunday isn't Friday  
    Given today is Sunday  
    When I ask whether it's Friday yet  
    Then I should be told "Nope"  
  
  Scenario: Friday is Friday  
    Given today is Friday  
    When I ask whether it's Friday yet  
    Then I should be told "TGIF"  


```

--------------------------------

### Running Scenarios with Tags using Cucumber CLI

Source: https://cucumber.io/docs/cucumber/api

Shows how to execute scenarios with specific tags using the main Cucumber command-line interface. The `--tags` option is used to specify the desired tag expression.

```bash
cucumber --tags "@smoke and @fast"  

```

--------------------------------

### Cucumber UI Test with Selenium WebDriver (JavaScript)

Source: https://cucumber.io/docs/guides/browser-automation

JavaScript implementation of Cucumber step definitions for UI testing using Selenium WebDriver. It utilizes async/await for asynchronous operations and Chai for assertions. Requires Cucumber.js, Selenium WebDriver, and ChromeDriver.

```javascript
const { Given, When, Then, AfterAll } = require('cucumber');
const { Builder, By, Capabilities, Key } = require('selenium-webdriver');
const { expect } = require('chai');
  
require("chromedriver");
  
// driver setup
const capabilities = Capabilities.chrome();
capabilities.set('chromeOptions', { "w3c": false });
const driver = new Builder().withCapabilities(capabilities).build();
  
Given('I am on the Google search page', async function () {
    await driver.get('http://www.google.com');
});
  
When('I search for {string}', async function (searchTerm) {
    const element = await driver.findElement(By.name('q'));
    element.sendKeys(searchTerm, Key.RETURN);
    element.submit();
});
  
Then('the page title should start with {string}', {timeout: 60 * 1000}, async function (searchTerm) {
    const title = await driver.getTitle();
    const isTitleStartWithCheese = title.toLowerCase().lastIndexOf(`${searchTerm}`, 0) === 0;
    expect(isTitleStartWithCheese).to.equal(true);
});
  
AfterAll(async function(){
    await driver.quit();
});

```

--------------------------------

### Cucumber UI Test with Selenium WebDriver (Ruby)

Source: https://cucumber.io/docs/guides/browser-automation

Ruby implementation for setting up Selenium WebDriver. This snippet shows the require statements needed to use Selenium WebDriver in a Ruby project, typically for use with Cucumber.

```ruby
require 'rubygems'
require 'selenium-webdriver'

```

--------------------------------

### Java Step Definitions for Cucumber 'Is it Friday Yet?' Feature

Source: https://cucumber.io/docs/guides/10-minute-tutorial

These Java step definitions implement the logic for the 'Is it Friday Yet?' feature. They use Cucumber annotations to map Gherkin steps to Java methods and include assertions for validation. The `isItFriday` method is included within the test class for demonstration.

```java
package hellocucumber;  
  
import io.cucumber.java.en.Given;  
import io.cucumber.java.en.When;  
import io.cucumber.java.en.Then;  
import static org.assertj.core.api.Assertions.assertThat;  
  
class IsItFriday {  
    static String isItFriday(String today) {  
        return "Friday".equals(today) ? "TGIF" : "Nope";  
    }  
}

public class Stepdefs {  
    private String today;  
    private String actualAnswer;  
  
    @Given("today is {string}")  
    public void today_is(String today) {  
        this.today = today;  
    }

    @When("I ask whether it's Friday yet")  
    public void i_ask_whether_it_s_Friday_yet() {  
        actualAnswer = IsItFriday.isItFriday(today);  
    }

    @Then("I should be told {string}")  
    public void i_should_be_told(String expectedAnswer) {  
        assertThat(actualAnswer).isEqualTo(expectedAnswer);  
    }
}

```

--------------------------------

### Maven Surefire Plugin Configuration for Parallel Execution

Source: https://cucumber.io/docs/guides/parallel-execution

Maven Surefire plugin configuration in the POM file to enable parallel test execution. It sets parallel execution to 'methods' and uses unlimited threads.

```xml
<plugin>  
	<groupId>org.apache.maven.plugins</groupId>  
	<artifactId>maven-surefire-plugin</artifactId>  
	<version>2.22.0</version>  
	<configuration>  
		<parallel>methods</parallel>  
		<useUnlimitedThreads>true</useUnlimitedThreads>  
	</configuration>  
</plugin>  

```

--------------------------------

### Running Scenarios with Tags using Cucumber.js CLI

Source: https://cucumber.io/docs/cucumber/api

Explains how to use the Cucumber.js command-line interface to run scenarios filtered by tags. The `--tags` option accepts tag expressions.

```bash
./node_modules/.bin/cucumber.js --tags "@smoke and @fast"  

```

--------------------------------

### Running Cucumber with Custom Object Factory (CLI)

Source: https://cucumber.io/docs/cucumber/state

Command-line instruction to run Cucumber tests using a specified custom object factory. This overrides the default object factory and enables the use of custom injectors and configurations.

```bash
java io.cucumber.core.cli.Main --object-factory com.example.app.CustomObjectFactory  

```

--------------------------------

### Configure Timeline Report with CucumberOptions Annotation

Source: https://cucumber.io/docs/guides/parallel-execution

This snippet shows how to enable the timeline report by adding the 'timeline:<report folder>' plugin to the CucumberOptions annotation in a JUnit or TestNG runner class. Replace '<report folder>' with the desired directory for the report.

```java
@CucumberOptions(plugin= {"timeline:<report folder>"})

```

--------------------------------

### JavaScript Step Definition with Regular Expressions

Source: https://cucumber.io/docs/cucumber/step-definitions

Illustrates a JavaScript step definition using a regular expression. Capture groups from the regex are passed as arguments to the JavaScript function.

```JavaScript
Given(/I have {int} cukes in my belly/, function (cukes) {
});

```

--------------------------------

### Cucumber UI Test with Selenium WebDriver (Java)

Source: https://cucumber.io/docs/guides/browser-automation

Java implementation of Cucumber step definitions for UI testing using Selenium WebDriver. It includes steps for navigating to Google, searching for a term, and verifying the page title. Requires Selenium WebDriver and Cucumber Java dependencies.

```java
package com.example;
  
import io.cucumber.java.After;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.ExpectedCondition;
import org.openqa.selenium.support.ui.WebDriverWait;
import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;
  
public class ExampleSteps {
  
    private final WebDriver driver = new FirefoxDriver();
  
    @Given("I am on the Google search page")
    public void I_visit_google() {
        driver.get("https://www.google.com");
    }
  
    @When("I search for {string}")
    public void search_for(String query) {
        WebElement element = driver.findElement(By.name("q"));
        // Enter something to search for
        element.sendKeys(query);
        // Now submit the form. WebDriver will find the form for us from the element
        element.submit();
   }
  
   @Then("the page title should start with {string}")
   public void checkTitle(String titleStartsWith) {
       // Google's search is rendered dynamically with JavaScript
       // Wait for the page to load timeout after ten seconds
       new WebDriverWait(driver,10L).until(new ExpectedCondition<Boolean>() {
           public Boolean apply(WebDriver d) {
               return d.getTitle().toLowerCase().startsWith(titleStartsWith);
           }
       });
   }
  
   @After()
   public void closeBrowser() {
       driver.quit();
   }
}
```

--------------------------------

### Screenshot on Failure with Capybara (Ruby)

Source: https://cucumber.io/docs/guides/browser-automation

Takes a screenshot on test failure when using Capybara in Ruby. It checks the scenario's failure status, saves the screenshot to a file, and attaches it to the report. Requires Capybara and a testing framework.

```ruby
# Available scenario methods: #failed?, #passed?, and #exception  
if scenario.failed?  
  path = "html-report/#{scenario.__id__}.html"  
  page.driver.browser.save_screenshot(path)  
  attach(path, "image/png")  
end  
```

--------------------------------

### Configure Parallel Execution with Multiple Runners

Source: https://cucumber.io/docs/guides/parallel-execution

This XML configuration snippet is used within the Maven Surefire or Failsafe plugin configuration. It sets the 'parallel' option to 'classes' and specifies the 'threadCount', which is beneficial when you have multiple Cucumber runners to optimize execution time.

```xml
<configuration>
	<parallel>classes</parallel>
	<threadCount>4</threadCount>
</configuration>
```

--------------------------------

### Before Hook: Ruby

Source: https://cucumber.io/docs/cucumber/api

Executes code before the first step of each scenario in Ruby. Uses a block for defining the hook's logic.

```Ruby
Before do
  # Do something before each scenario
end

```

--------------------------------

### Guice Module for Service Binding (Java)

Source: https://cucumber.io/docs/cucumber/state

A Google Guice module that configures bindings for application services. It specifies that the 'AppService' interface should be implemented by 'AppServiceImpl'.

```java
package com.example.app.service.impl;  
  
import com.example.app.service.AppService;  
import com.google.inject.AbstractModule;  
  
public final class ServiceModule extends AbstractModule {  
    @Override  
    protected void configure() {  
        bind( AppService.class ).to( AppServiceImpl.class );  
        // ... (further bindings)  
    }  
}

```

--------------------------------

### Maven Surefire/Failsafe Plugin - Specific Thread Count

Source: https://cucumber.io/docs/guides/parallel-execution

Configuration to set a specific number of threads for parallel execution in Maven Surefire or Failsafe plugins. 'threadCount' specifies the number of threads.

```xml
<configuration>  
	<parallel>methods</parallel>  
	<threadCount>4</threadCount>  
</configuration>  

```

--------------------------------

### Java Step Definition with Regular Expressions

Source: https://cucumber.io/docs/cucumber/step-definitions

Demonstrates using a regular expression to define a Java step definition in Cucumber. Capture groups within the regex are passed as arguments to the method.

```Java
@Given("I have {int} cukes in my belly")
public void i_have_n_cukes_in_my_belly(int cukes) {
}
```

--------------------------------

### Before Hook: Lambda Style (Java)

Source: https://cucumber.io/docs/cucumber/api

Executes code before the first step of each scenario using a lambda expression in Java. Supports specifying an execution order.

```Java
Before(() -> {
});

Before(10, () -> {
    // Do something before each scenario
});

```

--------------------------------

### Screenshot on Failure with WebDriver (Kotlin)

Source: https://cucumber.io/docs/guides/browser-automation

Captures a screenshot on test failure using Selenium WebDriver in Kotlin. Similar to the Java version, it attaches the screenshot to the scenario. Requires Selenium WebDriver and a compatible testing framework.

```kotlin
if (scenario.isFailed()) {  
    val screenshot = ((TakesScreenshot) webDriver).getScreenshotAs(OutputType.BYTES)  
    scenario.attach(screenshot, "image/png", "name")  
}  
```

--------------------------------

### Before Hook: Annotated Method Style (Java)

Source: https://cucumber.io/docs/cucumber/api

Executes code before the first step of each scenario using an annotated method in Java. Allows specifying an order for execution.

```Java
@Before
public void doSomethingBefore() {
}

@Before(order = 10)
public void doSomething(){
    // Do something before each scenario
}

```

--------------------------------

### Cucumber Step Argument Conversion to Integer

Source: https://cucumber.io/docs/cucumber/api

Demonstrates how Cucumber extracts a value from a step, converts it to an integer, and passes it as an argument to a method. The number of parameters must match the capture groups in the expression to avoid errors.

```gherkin
Given I have 48 cucumbers in my belly
```

--------------------------------

### Execute Cucumber Tests in Parallel via CLI

Source: https://cucumber.io/docs/guides/parallel-execution

This command executes Cucumber feature files directly from the command line using the Main class. The --threads option is set to 4 to enable parallel execution, running scenarios and scenario outline rows in multiple threads. It specifies the classpath and the package containing the step definitions.

```bash
java -cp .;<path to cucumber jar folder>/* io.cucumber.core.cli.Main --threads 4 -g parallel parallel
```

--------------------------------

### After Hook: Lambda Style (Kotlin)

Source: https://cucumber.io/docs/cucumber/api

Executes code after the last step of each scenario using a lambda expression in Kotlin. The 'scenario' parameter is optional.

```Kotlin
After { scenario: Scenario ->
    // doSomething
}

```

--------------------------------

### Run Cucumber with Ruby

Source: https://cucumber.io/docs/cucumber/api

Executes Cucumber tests written in Ruby. This command requires specifying the feature directory and optionally a specific feature file. The `--require` option is used to include step definition files.

```bash
cucumber --require features features/authentication/authenticate_user.feature  
```

--------------------------------

### Fixing Failing Cucumber Scenario

Source: https://cucumber.io/docs/guides/10-minute-tutorial

This code snippet demonstrates the minimal change required to make a failing Cucumber scenario pass. By modifying the 'isItFriday' method to return 'Nope', the assertion in the 'Then' step will succeed.

```java
static String isItFriday(String today) {  
    return "Nope";  
}  

```

--------------------------------

### Take Screenshots After Intermittent Steps (Ruby)

Source: https://cucumber.io/docs/cucumber/debugging

This Ruby code snippet defines an `AfterStep` hook that takes a full-page screenshot after steps tagged with '@intermittent' if the `STEP` environment variable is set. It saves the screenshot to the 'tmp/capybara/' directory with a sequential naming convention.

```ruby
AfterStep do |scenario|
  CucumberCounters.step_counter += 1
  step = CucumberCounters.step_counter
  file_name = format('tmp/capybara/step_%03d.png', step)
  Rails.logger.info("[Cucumber] after step: #{@scenario_name}, step: #{step}")
  next unless scenario.source_tag_names.include?('@intermittent')
  begin
    Capybara.page.save_screenshot(file_name, full: true)
    Rails.logger.info("[Cucumber] Screenshot #{step} saved")
  rescue
    Rails.logger.info("[Cucumber] Can not make screenshot of #{step}")
  end
end
```

--------------------------------

### Screenshot on Failure with WebDriver (JavaScript)

Source: https://cucumber.io/docs/guides/browser-automation

Implements taking a screenshot on test failure in JavaScript using WebDriver. It checks the scenario status and attaches the screenshot if the scenario failed. Requires WebDriver and a testing framework like Cucumber.js.

```javascript
After(async function (scenario) {  
    if (scenario.result.status === Status.FAILED) {  
        return webDriver.takeScreenshot().then((screenShot, error) => {  
            if (!error) {  
                this.attach(screenShot, "image/png");  
            }  
        });  
    }  
});  
```

--------------------------------

### Run Non-WIP Scenarios with Rake

Source: https://cucumber.io/docs/tools/ruby

This Rake command executes Cucumber scenarios that are not tagged with '@wip'. It effectively runs all scenarios except those marked as work-in-progress.

```shell
rake cucumber:ok

```

--------------------------------

### Screenshot on Failure with WebDriver (Java)

Source: https://cucumber.io/docs/guides/browser-automation

Captures a screenshot when a test scenario fails using Selenium WebDriver in Java. The screenshot is attached to the scenario report. Requires Selenium WebDriver and a testing framework that provides scenario context.

```java
if (scenario.isFailed()) {  
    byte[] screenshot = ((TakesScreenshot) webDriver).getScreenshotAs(OutputType.BYTES);  
    scenario.attach(screenshot, "image/png", "name");  
}  
```

--------------------------------

### Running Scenarios with Tags using Environment Variable (Maven)

Source: https://cucumber.io/docs/cucumber/api

Demonstrates running scenarios with specific tags by setting the `CUCUMBER_FILTER_TAGS` environment variable before executing Maven tests. This is an alternative to using JVM system properties.

```bash
# Linux / OS X:
CUCUMBER_FILTER_TAGS="@smoke and @fast" mvn test  

# Windows:
set CUCUMBER_FILTER_TAGS="@smoke and @fast"  
mvn test  

```

--------------------------------

### Before Hook: Lambda Style (Scala)

Source: https://cucumber.io/docs/cucumber/api

Executes code before the first step of each scenario using a lambda expression in Scala. Supports specifying an execution order.

```Scala
Before { scenario: Scenario =>
    // doSomething
}

Before(10) { scenario: Scenario =>
    // Do something before each scenario
}

```

--------------------------------

### Running Cucumber with JavaScript

Source: https://cucumber.io/docs/cucumber/api

Explains how to execute Cucumber tests when using the JavaScript implementation. It is typically run via the `cucumber-js` command in the terminal or through build scripts.

```bash
cucumber-js  

```

--------------------------------

### Ruby World Customization for Step State

Source: https://cucumber.io/docs/cucumber/state

Demonstrates how to customize the Ruby Cucumber World to share state and helper methods between steps within a single scenario. It shows how to define custom modules and include them in the World, ensuring state isolation between scenarios.

```ruby
module CustomWorld  
  def a_helper  
    ...
  end  
end  

World(CustomWorld)
```

```ruby
module MyHelper  
  def some_other_helper  
    ...
  end  
end  

module CustomWorld  
  include MyHelper  
  
  def a_helper  
    ...
  end  
end  

World(CustomWorld)
```

```ruby
module MyHelper  
  def some_other_helper  
    ...
  end  
end  

module MyOtherHelpers  
  def helper_b  
    ...
  end  
end  

World(MyHelper, MyOtherHelpers)
```

--------------------------------

### Configure Maven Profiles for Cucumber Environments

Source: https://cucumber.io/docs/cucumber/configuration

This snippet demonstrates how to configure Maven profiles to set different Cucumber tag filters for various environments like 'dev' and 'qa'. It utilizes the `maven-surefire-plugin` to pass these configurations as system properties.

```xml
<profiles>
    <profile>
      <id>dev</id>
        <properties>
            <cucumber.filter.tags>@dev and not @ignore</cucumber.filter.tags>
        </properties>
    </profile>
    <profile>
      <id>qa</id>
        <properties>
            <cucumber.filter.tags>@qa</cucumber.filter.tags>
        </properties>
    </profile>
</profiles>

<build>
    <plugins>
        ...
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0-M4</version>
            <configuration>
                <systemPropertyVariables>
                   <cucumber.filter.tags>${cucumber.filter.tags}</cucumber.filter.tags>
                </systemPropertyVariables>
            </configuration>
        </plugin>
    </plugins>
</build>
```

--------------------------------

### Run Cucumber CLI with Java

Source: https://cucumber.io/docs/cucumber/api

Executes the Cucumber CLI runner directly using Java. Requires adding `cucumber-core` jar and its dependencies to the classpath, along with compiled .class files. Step definitions are specified using the `--glue` option and feature file paths.

```bash
java io.cucumber.core.cli.Main  
```

```bash
java -cp "path/to/each/jar:path/to/compiled/.class/files" io.cucumber.core.cli.Main /path/to/your/feature/files --glue hellocucumber --glue anotherpackage  
```

--------------------------------

### Cucumber Feature with Watir Integration (Ruby)

Source: https://cucumber.io/docs/guides/browser-automation

Integrates Cucumber with Watir for UI testing. This defines Gherkin steps for entering search terms, clicking buttons, and verifying results, using Watir to interact with the browser. Requires 'watir' and 'rspec/expectations' gems.

```ruby
require "watir"  
require "rspec/expectations"  
  
Given(/^I have entered "([^"]*)" into the query$/) do |term|  
  @browser ||= Watir::Browser.new :firefox  
  @browser.goto "google.com"  
  @browser.text_field(name: "q").set term  
end  
  
When(/^I click "([^"]*)"$/) do  
 @browser.button.click  
end  
  
Then(/^I should see some results$/) do  
  @browser.div(id: "resultStats").wait_until_present  
  @browser.close  
end  
```

--------------------------------

### Before Hook: JavaScript

Source: https://cucumber.io/docs/cucumber/api

Executes code before the first step of each scenario in JavaScript. Avoids arrow functions to prevent 'this' binding issues.

```JavaScript
// Import the Before function
const { Before } = require('@cucumber/cucumber')

Before(async function () {
})

```

--------------------------------

### Configure Cucumber Object Factory with properties file

Source: https://cucumber.io/docs/cucumber/state

Specify a custom object factory for Cucumber by adding an entry to the `cucumber.properties` file. This allows for custom object instantiation during Cucumber's execution.

```properties
cucumber.object-factory=com.example.app.CustomObjectFactory
```

--------------------------------

### Configure Default Transformers using Lambdas in Java 8

Source: https://cucumber.io/docs/cucumber/configuration

Sets up default parameter, data table cell, and data table entry transformers using lambda expressions in Java 8. This approach leverages Jackson's ObjectMapper for flexible type conversions.

```java
import com.fasterxml.jackson.databind.ObjectMapper
  
import io.cucumber.java8.En
import java.lang.reflect.Type
  
class LambdaStepDefinitions : En {
    init {
        val objectMapper = ObjectMapper()

        DefaultParameterTransformer { fromValue: String, toValueType: Type ->
            objectMapper.convertValue(fromValue, objectMapper.constructType(toValueType))
        }

        DefaultDataTableCellTransformer { fromValue, toValueType ->
            objectMapper.convertValue(fromValue, objectMapper.constructType(toValueType))
        }

        DefaultDataTableEntryTransformer { fromValue, toValueType ->

```

--------------------------------

### Running Cucumber with JUnit Formatter in Jenkins

Source: https://cucumber.io/docs/guides/continuous-integration

This command executes Cucumber tests and generates JUnit XML reports, which can be parsed by CI servers like Jenkins for test result reporting. The `-f junit` flag specifies the JUnit formatter, and `--out WORKSPACE` directs the output to the WORKSPACE directory. Jenkins can then be configured to publish these XML reports.

```bash
cucumber -f junit --out WORKSPACE
```

--------------------------------

### Helper Functions for Web Interaction (Ruby)

Source: https://cucumber.io/docs/cucumber/debugging

This Ruby code provides two helper functions: `dismiss_nav_warning` and `wait_until_jquery_inactive`. `dismiss_nav_warning` unbinds the 'beforeunload' event, and `wait_until_jquery_inactive` waits for all jQuery AJAX requests to complete.

```ruby
def dismiss_nav_warning
  execute_script "$(window).unbind('beforeunload')"
  wait_until_jquery_inactive
end

def wait_until_jquery_inactive
  Capybara.using_wait_time(Capybara.default_max_wait_time) do
    page.evaluate_script('jQuery.active').zero?
  end
end
```

--------------------------------

### After Hook: Lambda Style (Java)

Source: https://cucumber.io/docs/cucumber/api

Executes code after the last step of each scenario using a lambda expression in Java. The 'scenario' parameter is optional.

```Java
After((Scenario scenario) -> {
});

```

--------------------------------

### Run Cucumber CLI with Maven Exec Plugin

Source: https://cucumber.io/docs/cucumber/api

Executes the Cucumber CLI runner using the Maven Exec plugin for projects managed with Maven. This command specifies the main class and arguments, including feature file paths and glue packages, leveraging the test classpath.

```bash
mvn exec:java                                  \
    -Dexec.classpathScope=test                 \
    -Dexec.mainClass=io.cucumber.core.cli.Main \
    -Dexec.args="/path/to/your/feature/files --glue hellocucumber --glue anotherpackage"  
```

--------------------------------

### Gherkin Feature and Scenario Tagging

Source: https://cucumber.io/docs/cucumber/api

Demonstrates how to apply tags to Gherkin features and scenarios for organization and filtering. Tags are placed above the Gherkin element they apply to.

```gherkin
@billing  
Feature: Verify billing  
  
  @important  
  Scenario: Missing product description  
    Given hello  
  
  Scenario: Several products  
    Given hello  

```

```gherkin
@billing @bicker @annoy  
Feature: Verify billing  

```

```gherkin
Scenario Outline: Steps will run conditionally if tagged  
  Given user is logged in  
  When user clicks <link>  
  Then user will be logged out  
  
  @mobile  
  Examples:  
    | link                  |  
    | logout link on mobile |  
  
  @desktop  
  Examples:  
    | link                   |  
    | logout link on desktop |  

```

--------------------------------

### Cucumber Rails Configuration for @wip Tag

Source: https://cucumber.io/docs/cucumber/api

Illustrates how the `@wip` tag is handled in the `config/cucumber.yml` file for Cucumber-Rails. It shows the use of negation (`~@wip`) to exclude scenarios marked as work-in-progress from the default run.

```ruby
<%  
.  .  .  
std_opts = "--format #{ENV['CUCUMBER_FORMAT'] || 'progress'} --strict --tags ~@wip"  
%>  
default: <%= std_opts %> features  
.  .  .  

```

--------------------------------

### JavaScript Step Definition for Gherkin

Source: https://cucumber.io/docs/cucumber/step-definitions

Illustrates defining a Cucumber step definition using JavaScript. It imports the 'Given' function and associates it with a Gherkin step, providing a callback function to execute.

```JavaScript
const { Given } = require('cucumber')

Given('I have {int} cukes in my belly', function (cukes) {
  console.log(`Cukes: ${cukes}`)
});

```

--------------------------------

### Running Scenarios with Tags using JUnit Runner Annotation

Source: https://cucumber.io/docs/cucumber/api

Illustrates how to filter scenarios by tags directly within a JUnit 4/TestNG runner class using the `@CucumberOptions` annotation. This provides an in-code configuration for tag filtering.

```java
@CucumberOptions(tags = "@smoke and @fast")  

```

--------------------------------

### Gherkin Feature Keyword Usage

Source: https://cucumber.io/docs/gherkin/reference

Demonstrates the usage of the 'Feature' keyword in Gherkin, including its name, colon, and optional free-form description. The description text is ignored by Cucumber at runtime but available for reporting.

```gherkin
Feature: Guess the word  
  
  The word guess game is a turn-based game for two players.  
  The Maker makes a word for the Breaker to guess. The game  
  is over when the Breaker guesses the Maker's word.  
  
  Example: Maker starts a game  

```

--------------------------------

### Set DataProvider Thread Count in Surefire/Failsafe Plugin

Source: https://cucumber.io/docs/guides/parallel-execution

This XML configuration snippet is added to the Maven Surefire or Failsafe plugin's configuration in the POM.xml. It allows you to set the 'dataproviderthreadcount' property, controlling the number of threads used for parallel execution of DataProviders.

```xml
<configuration>
	<properties>
    	<property>
        	<name>dataproviderthreadcount</name>
        	<value>20</value>
    	</property>
	</properties>
</configuration>
```

--------------------------------

### After Hook: JavaScript

Source: https://cucumber.io/docs/cucumber/api

Executes code after the last step of each scenario in JavaScript. The 'scenario' parameter is optional.

```JavaScript
After(async function (scenario) {
})

```

--------------------------------

### After Hook: Ruby

Source: https://cucumber.io/docs/cucumber/api

Executes code after the last step of each scenario in Ruby. The 'scenario' parameter is optional and can be used to inspect scenario status.

```Ruby
After do |scenario|
end

After do |s|
  # Tell Cucumber to quit after this scenario is done - if it failed.
  Cucumber.wants_to_quit = true if s.failed?
end

```

--------------------------------

### Unbind Beforeunload Event (Ruby)

Source: https://cucumber.io/docs/cucumber/debugging

This Ruby code snippet defines an `AfterStep` hook that unbinds the 'beforeunload' event from the window. This is useful for preventing unexpected confirmation dialogs during automated testing. It includes error handling for robustness.

```ruby
AfterStep do
  begin
    execute_script "$(window).unbind('beforeunload')"
  rescue => e
    Rails.logger.error("An error was encountered and rescued")
    Rails.logger.error(e.backtrace)
  end
end
```

--------------------------------

### After Hook: Lambda Style (Scala)

Source: https://cucumber.io/docs/cucumber/api

Executes code after the last step of each scenario using a lambda expression in Scala. The 'scenario' parameter is optional.

```Scala
After { scenario: Scenario =>
    // doSomething
}

```

--------------------------------

### Configure Default Transformers with Jackson in Java

Source: https://cucumber.io/docs/cucumber/configuration

Configures default transformers using Jackson's ObjectMapper to handle conversions for parameters, data table entries, and cells. This simplifies type conversions by centralizing object mapping logic.

```java
package com.example
  
import com.fasterxml.jackson.databind.ObjectMapper
import io.cucumber.java.DefaultDataTableCellTransformer
import io.cucumber.java.DefaultDataTableEntryTransformer
import io.cucumber.java.DefaultParameterTransformer
  
import java.lang.reflect.Type
  
class StepDefinitions {
  
    private val objectMapper = ObjectMapper()

    @DefaultParameterTransformer
    @DefaultDataTableEntryTransformer
    @DefaultDataTableCellTransformer
    fun transformer(fromValue: Any, toValueType: Type): Any {
        return objectMapper.convertValue(fromValue, objectMapper.constructType(toValueType))
    }
}
```

--------------------------------

### Ruby Step Definition with Regular Expressions

Source: https://cucumber.io/docs/cucumber/step-definitions

Defines a Ruby step definition using a regular expression. The capture groups from the regex are passed as arguments to the Ruby block.

```Ruby
Given(/I have {int} cukes in my belly/) do |cukes|
end
```

--------------------------------

### Debugging Ruby Cucumber Steps

Source: https://cucumber.io/docs/cucumber/debugging

This Ruby code snippet provides helper classes and hooks for debugging Cucumber scenarios. It includes functionality to save screenshots on failure, stop execution on the first failure, and drop into a debugger on failure. It also logs scenario names and attempts to capture screenshots of errors. This code is intended for use within a Ruby on Rails project, but can be adapted for other Ruby environments.

```ruby
# rubocop:disable Lint/Debugger
class CucumberCounters
  @error_counter = 0
  @step_counter = 0
  @screenshot_counter = 0
  class << self
    attr_accessor :error_counter, :step_counter, :screenshot_counter
  end
end

# `LAUNCHY=1 cucumber` to open save screenshot after every step
After do |scenario|
  next unless (ENV['LAUNCHY'] || ENV['CI']) && scenario.failed?
  puts "Opening snapshot for #{scenario.name}"
  begin
    save_and_open_screenshot
  rescue StandardError
    puts "Can't save screenshot"
  end
  begin
    save_and_open_page
  rescue StandardError
    puts "Can't save page"
  end
end

# `FAST=1 cucumber` to stop on first failure
After do |scenario|
  Cucumber.wants_to_quit = ENV['FAST'] && scenario.failed?
end

# `DEBUG=1 cucumber` to drop into debugger on failure
Cucumber::Core::Test::Action.class_eval do
  ## first make sure we don't lose original accept method
  unless instance_methods.include?(:orig_failed)
    alias_method :orig_failed, :failed
  end

  ## wrap original accept method to catch errors in executed step
  def failed(*args)
    begin
      CucumberCounters.error_counter += 1
      file_name = format('tmp/capybara/error_%03d.png',
                         CucumberCounters.error_counter)
      Capybara.page.save_screenshot(file_name, full: true)
    rescue
      Rails.logger.info('[Cucumber] Can not make screenshot of failure')
    end
    binding.pry if ENV['DEBUG']
    orig_failed(*args)
  end
end

# Store the current scenario name as an instance variable, to make it
# available to the other hooks.
Before do |scenario|
  case scenario
  when Cucumber::Ast::Scenario
    @scenario_name = scenario.name
  when Cucumber::Ast::OutlineTable::ExampleRow
    @scenario_name = scenario.scenario_outline.name
  end
  Rails.logger.info("[Cucumber] starting the #{@scenario_name}")
end

```

--------------------------------

### Configure Selenium Driver for Multiple Browsers in Ruby

Source: https://cucumber.io/docs/guides/browser-automation

This Ruby code snippet registers a Capybara Selenium driver that selects the browser based on the 'browser' environment variable, defaulting to 'firefox'. It allows dynamic browser selection for Capybara-driven tests.

```ruby
Capybara.register_driver :selenium do |app|
  browser = (ENV['browser'] || 'firefox').to_sym
  Capybara::Selenium::Driver.new(app, browser: browser)
end
```

--------------------------------

### Define Custom Types using Lambdas in Java 8

Source: https://cucumber.io/docs/cucumber/configuration

Demonstrates defining custom parameter, data table, and doc string types using lambda expressions in Java 8. This provides a concise way to register custom converters.

```java
package com.example
  
import com.fasterxml.jackson.databind.JsonNode
import com.fasterxml.jackson.databind.ObjectMapper
  
import io.cucumber.java8.En
  
class LambdaStepDefinitions : En {
  
    init {
        val objectMapper = ObjectMapper()

        ParameterType("book", ".*") { s : String ->
            Book(s)
        }

        DataTableType { entry: Map<String, String> ->
            Author(entry["firstName"], entry["lastName"], entry["famousBook"])
        }

        DocStringType("json") { docString: String ->
	        objectMapper.readValue(docString, JsonNode::class)
	    }
    }
}
```

--------------------------------

### After Hook: Annotated Method Style (Java)

Source: https://cucumber.io/docs/cucumber/api

Executes code after the last step of each scenario using an annotated method in Java. The 'scenario' parameter can be used to inspect the scenario's status.

```Java
@After
public void doSomethingAfter(Scenario scenario){
    // Do something after after scenario
}

```

--------------------------------

### Custom Cucumber Object Factory with Guice (Java)

Source: https://cucumber.io/docs/cucumber/state

Implementation of a custom Cucumber ObjectFactory that integrates with Google Guice. This factory creates a Guice injector with specific modules and manages the lifecycle of scenario-scoped objects.

```java
package com.example.app;  
  
import io.cucumber.core.backend.ObjectFactory;  
import io.cucumber.guice.CucumberModules;  
import io.cucumber.guice.ScenarioScope;  
import com.example.app.service.impl.ServiceModule;  
import com.google.inject.Guice;  
import com.google.inject.Injector;  
import com.google.inject.Stage;  
  
public final class CustomObjectFactory implements ObjectFactory {  
  
    private Injector injector;  
  
    public CustomObjectFactory() {  
        // Create an injector with our service module  
        this.injector =  
          Guice.createInjector( Stage.PRODUCTION, CucumberModules.createScenarioModule(), new ServiceModule());  
    }  
  
    @Override  
    public boolean addClass( Class< ? > clazz ) {  
        return true;  
    }  
  
    @Override  
    public void start() {  
        this.injector.getInstance( ScenarioScope.class ).enterScope();  
    }  
  
    @Override  
    public void stop() {  
        this.injector.getInstance( ScenarioScope.class ).exitScope();  
    }  
  
    @Override  
    public < T > T getInstance( Class< T > clazz ) {  
        return this.injector.getInstance( clazz );  
    }  
}

```

--------------------------------

### Define Cucumber YAML Profiles

Source: https://cucumber.io/docs/cucumber/configuration

This YAML snippet defines named profiles for Cucumber execution. Each profile is associated with specific command-line options. The `html_report` profile configures output formats, while the `bvt` profile filters scenarios by tags.

```yaml
## ##YAML Template  
html_report: --format progress --format html --out=features_report.html  
bvt: --tags @bvt  
```

--------------------------------

### Cucumber Feature Tag for Development Readiness

Source: https://cucumber.io/docs/cucumber/api

Shows a simple tag used to indicate that a feature is ready for a specific stage in the development process, such as quality assurance.

```gherkin
@qa_ready  
Feature: Index projects  

```

--------------------------------

### Add Guice Dependency for Cucumber JVM

Source: https://cucumber.io/docs/cucumber/state

This snippet provides the Maven and Gradle dependencies required to integrate Guice with Cucumber JVM. Guice is a popular DI framework for Java applications.

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-guice</artifactId>
    <version>7.33.0</version>
    <scope>test</scope>
</dependency>
```

```gradle
testImplementation("io.cucumber:cucumber-guice:7.33.0")
```

--------------------------------

### Add OpenEJB Dependency for Cucumber JVM

Source: https://cucumber.io/docs/cucumber/state

This snippet shows the Maven and Gradle configurations for adding the OpenEJB dependency to a Cucumber JVM project, enabling integration with OpenEJB for dependency injection.

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-openejb</artifactId>
    <version>7.33.0</version>
    <scope>test</scope>
</dependency>
```

```gradle
testImplementation("io.cucumber:cucumber-openejb:7.33.0")
```

--------------------------------

### ServiceLoader Configuration for Custom Object Factory

Source: https://cucumber.io/docs/cucumber/state

Configuration file for Java's ServiceLoader mechanism. This file, located at META-INF/services/io.cucumber.core.backend.ObjectFactory, tells Cucumber to use the custom 'CustomObjectFactory' implementation.

```properties
com.example.app.CustomObjectFactory  
#  
# ... additional custom object factories could be added here  
#  

```

--------------------------------

### Setting Environment Variables in cucumber.yml Profile

Source: https://cucumber.io/docs/cucumber/configuration

This YAML configuration for `cucumber.yml` defines a profile named 'baz'. This profile not only specifies tags to run (`@mytag`) but also sets an environment variable `FOO` to `BAR`.

```yaml
baz: --tags @mytag FOO=BAR
```

--------------------------------

### Ignoring Scenarios with Tags using Cucumber.js CLI

Source: https://cucumber.io/docs/cucumber/api

Explains how to use the Cucumber.js command-line interface to ignore scenarios matching a specific tag. The `--tags` option with the `not` operator is used for this purpose.

```bash
./node_modules/.bin/cucumber.js --tags "not @smoke"  

```

--------------------------------

### Ignoring Scenarios with Tags using Cucumber CLI

Source: https://cucumber.io/docs/cucumber/api

Shows how to exclude scenarios with specific tags using the main Cucumber command-line interface. The `--tags` option combined with the `not` operator allows for ignoring scenarios.

```bash
cucumber --tags "not @smoke"  

```

--------------------------------

### Troubleshoot Cucumber Dependency Conflicts with Maven

Source: https://cucumber.io/docs/faq

This section addresses errors like `Failed to instantiate public cucumber.runtime.java.JavaBackend` or `NoSuchMethodException` by ensuring consistent Cucumber dependency versions. It recommends using `mvn dependency:tree` to inspect dependencies and excluding conflicting transitive dependencies in the `pom.xml`.

```bash
mvn dependency:tree
```

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-java</artifactId>
    <version>X.Y.Z</version>
</dependency>

<!-- Example of excluding a transitive dependency -->
<dependency>
    <groupId>some.other.library</groupId>
    <artifactId>library-with-cucumber-transitive</artifactId>
    <version>1.0.0</version>
    <exclusions>
        <exclusion>
            <groupId>io.cucumber</groupId>
            <artifactId>cucumber-core</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

--------------------------------

### Java Step Definition for Gherkin

Source: https://cucumber.io/docs/cucumber/step-definitions

Defines a Java method that matches a Gherkin step 'I have {int} cukes in my belly'. It uses the @Given annotation and expects an integer argument. This is a standard approach for integrating Gherkin with Java.

```Java
package com.example;
import io.cucumber.java.en.Given;

public class StepDefinitions {
    @Given("I have {int} cukes in my belly")
    public void i_have_n_cukes_in_my_belly(int cukes) {
        System.out.format("Cukes: %n\n", cukes);
    }
}
```

```Java
package com.example;
import io.cucumber.java8.En;

public class StepDefinitions implements En {
    public StepDefinitions() {
        Given("I have {int} cukes in my belly", (Integer cukes) -> {
            System.out.format("Cukes: %n\n", cukes);
        });
    }
}
```

--------------------------------

### Configure Jackson Object Mapper for Transformers in Scala

Source: https://cucumber.io/docs/cucumber/configuration

Configures default transformers using Jackson's ObjectMapper for parameter, data table cell, and data table entry conversions. This simplifies type conversions by leveraging Jackson's capabilities.

```scala
package com.example
  
import com.fasterxml.jackson.databind.ObjectMapper
import io.cucumber.scala.ScalaDsl

import java.lang.reflect.Type

class StepDefinitions extends ScalaDsl {
  
    private val objectMapper = ObjectMapper()
  
    DefaultParameterTransformer { (fromValue: String, toValueType: Type) =>
        objectMapper.convertValue(fromValue, objectMapper.constructType(toValueType))
    }
  
    DefaultDataTableCellTransformer { (fromValue: String, toValueType: Type) =>
        objectMapper.convertValue(fromValue, objectMapper.constructType(toValueType))
    }
  
    DefaultDataTableEntryTransformer { (fromValue: Map[String, String], toValueType: Type) =>
        objectMapper.convertValue(fromValue, objectMapper.constructType(toValueType))
    }
}
```

--------------------------------

### Java Function to Determine Friday

Source: https://cucumber.io/docs/guides/10-minute-tutorial

Provides the core logic for the 'Is it Friday yet?' feature. This Java function checks if the input 'today' string is equal to 'Friday' and returns the appropriate response.

```java
static String isItFriday(String today) {  
    return "Friday".equals(today) ? "TGIF" : "Nope";  
}  


```

--------------------------------

### Cucumber Feature with External System Tags

Source: https://cucumber.io/docs/cucumber/api

Demonstrates how to use tags in Cucumber features to reference external systems like requirement management or issue trackers. These tags can be processed by custom reporting plugins to create links.

```gherkin
@BJ-x98.77 @BJ-z12.33  
Feature: Convert transaction  

```

--------------------------------

### Pause Cucumber Execution After Each Step (Ruby)

Source: https://cucumber.io/docs/cucumber/debugging

This Ruby code snippet defines an `AfterStep` hook that pauses the Cucumber execution after each step if the `STEP` environment variable is set. It displays the current step number and name, waiting for user input to continue.

```ruby
AfterStep do |scenario|
  next unless ENV['STEP']
  unless defined?(@counter)
    puts "Stepping through #{@scenario_name}"
    @counter = 0
  end
  @counter += 1
  print "After step ##{@counter}/#{scenario.send(:steps).try(:count)}: " \
        "#{scenario.send(:steps).to_a[@counter].try(:name) ||
        '[RETURN to continue]'}"...
  STDIN.getc
end
```

--------------------------------

### Add PicoContainer Dependency for Cucumber JVM

Source: https://cucumber.io/docs/cucumber/state

This snippet shows how to add the PicoContainer dependency for Cucumber JVM projects using Maven or Gradle. PicoContainer is recommended if your application doesn't use another DI module.

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-picocontainer</artifactId>
    <version>7.33.0</version>
    <scope>test</scope>
</dependency>
```

```gradle
testImplementation("io.cucumber:cucumber-picocontainer:7.33.0")
```

--------------------------------

### Add Spring Dependency for Cucumber JVM

Source: https://cucumber.io/docs/cucumber/state

This snippet demonstrates how to include the Spring dependency for Cucumber JVM projects via Maven or Gradle. This allows for integration with Spring's dependency injection capabilities.

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-spring</artifactId>
    <version>7.33.0</version>
    <scope>test</scope>
</dependency>
```

```gradle
testImplementation("io.cucumber:cucumber-spring:7.33.0")
```

--------------------------------

### Cucumber JUnit Runner Class

Source: https://cucumber.io/docs/guides/parallel-execution

A Java class that serves as the entry point for running Cucumber tests with JUnit. It uses the @RunWith annotation to specify Cucumber as the runner.

```java
package parallel;  
  
import io.cucumber.junit.Cucumber;  
import org.junit.runner.RunWith;  
  
@RunWith(Cucumber.class)  
public class RunCucumberTest {  
}

```

--------------------------------

### Cucumber Data Table to List<String> in Java

Source: https://cucumber.io/docs/cucumber/api

Shows how to pass a simple list of strings from a Gherkin data table to a Java step definition. Cucumber automatically flattens the DataTable to a List<String> when no capture groups are defined in the step expression.

```gherkin
Given the following animals:
| cow |
| horse |
| sheep |
```

```java
@Given("the following animals:")
public void the_following_animals(List<String> animals) {
}
```

--------------------------------

### Add Cucumber-Java and Cucumber-JUnit Gradle Dependencies (5.0+)

Source: https://cucumber.io/docs/installation/java

This snippet shows the dependencies for Gradle versions 5.0 and newer, using testImplementation for cucumber-java and cucumber-junit. It also includes the mavenCentral() repository.

```gradle
dependencies {
    testImplementation("io.cucumber:cucumber-java:7.33.0")
    testImplementation("io.cucumber:cucumber-junit:7.33.0")
}

repositories {
    mavenCentral()
}
```

--------------------------------

### Java TestNG Maven Dependencies for Assertions

Source: https://cucumber.io/docs/cucumber/checking-assertions

These Maven dependencies are needed to use TestNG assertions with Cucumber. It includes the TestNG library and the 'cucumber-testng' integration. Ensure the versions are compatible with your project.

```xml
<dependency>
    <groupId>org.testng</groupId>
    <artifactId>testng</artifactId>
    <version>7.11.0</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-testng</artifactId>
    <version>7.33.0</version>
    <scope>test</scope>
</dependency>
```

--------------------------------

### Cucumber Data Table to List<String> in Kotlin

Source: https://cucumber.io/docs/cucumber/api

Demonstrates passing a list of strings from a Gherkin data table to a Kotlin step definition. Cucumber automatically converts the DataTable to a List<String> if the step expression has no capture groups.

```gherkin
Given the following animals:
| cow |
| horse |
| sheep |
```

```kotlin
@Given("the following animals:")
fun the_following_animals(animals: List<String>) {
}
```

--------------------------------

### Ignoring Scenarios with Tags using JUnit Runner Annotation

Source: https://cucumber.io/docs/cucumber/api

Demonstrates how to exclude scenarios with specific tags by using the `not` operator within the `tags` attribute of the `@CucumberOptions` annotation in JUnit 4/TestNG runner classes.

```java
@CucumberOptions(tags = "not @smoke")  

```

--------------------------------

### Add Needle Dependency for Cucumber JVM

Source: https://cucumber.io/docs/cucumber/state

This snippet provides the Maven and Gradle dependencies for incorporating the Needle DI framework into Cucumber JVM projects.

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-needle</artifactId>
    <version>7.33.0</version>
    <scope>test</scope>
</dependency>
```

```gradle
testImplementation("io.cucumber:cucumber-needle:7.33.0")
```

--------------------------------

### Ruby Test::Unit World Augmentation

Source: https://cucumber.io/docs/cucumber/checking-assertions

This Ruby code demonstrates how to include Test::Unit's assertion methods into your Cucumber 'World'. This allows you to use Test::Unit's 'assert' methods directly within your step definitions.

```ruby
require 'test/unit/assertions'

World(Test::Unit::Assertions)
```

--------------------------------

### Ruby RSpec Gemfile Configuration

Source: https://cucumber.io/docs/cucumber/checking-assertions

This shows how to add the 'rspec-expectations' gem to your Gemfile for using RSpec assertions in Cucumber. Cucumber automatically loads RSpec's matchers and expectation methods.

```ruby
# Add to your Gemfile:
gem 'rspec-expectations'
```

--------------------------------

### Add cucumber-junit Dependency for Maven

Source: https://cucumber.io/docs/cucumber/api

Maven dependency configuration to include the `cucumber-junit` artifact. This allows Cucumber scenarios to be executed using JUnit 4.

```xml
<dependencies>
  [...]
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-junit</artifactId>
        <version>${cucumber.version}</version>
        <scope>test</scope>
    </dependency>
  [...]
</dependencies>
```

--------------------------------

### Add Weld Dependency for Cucumber JVM

Source: https://cucumber.io/docs/cucumber/state

This snippet includes the Maven and Gradle dependencies for integrating Weld, a CDI implementation, with Cucumber JVM projects.

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-weld</artifactId>
    <version>7.33.0</version>
    <scope>test</scope>
</dependency>
```

```gradle
testImplementation("io.cucumber:cucumber-weld:7.33.0")
```

--------------------------------

### Dynamic Cucumber YAML with ERB

Source: https://cucumber.io/docs/cucumber/configuration

This YAML snippet demonstrates using ERB (Embedded RuBy) within `cucumber.yml` to dynamically generate configuration values. It defines a common set of options in a Ruby variable and then interpolates it into different profiles, reducing repetition.

```yaml
1. config/cucumber.yml  
   ## ##YAML Template  
   <% common = "--tags ~@wip --strict" %>  
   default: <%= common %> features  
   html_report: <%= common %> --format html --out=features_report.html features  
```

--------------------------------

### Around Hook: Ruby

Source: https://cucumber.io/docs/cucumber/api

Executes code 'around' a scenario in Ruby, wrapping its execution. Receives a Scenario object and a block to call for scenario execution. Useful for timeouts.

```Ruby
Around('@fast') do |scenario, block|
  Timeout.timeout(0.5) do
    block.call
  end
end

```

--------------------------------

### Java Step Definition for Friday

Source: https://cucumber.io/docs/guides/10-minute-tutorial

Implements the 'Given today is Friday' step for the Cucumber test. This Java method sets a variable to indicate that the current day is Friday, enabling the test to proceed.

```java
@Given("today is Friday")  
public void today_is_Friday() {  
    today = "Friday";  
}  


```

--------------------------------

### Stubbing External API Calls in Ruby with RSpec

Source: https://cucumber.io/docs/cucumber/mocking-and-stubbing-with-cucumber

This snippet demonstrates how to stub an external API call using RSpec's mocking framework within a Cucumber step definition. It requires the 'cucumber/rspec/doubles' library and uses `RSpec::Mocks.with_temporary_scope` to isolate the stubbing. The stubbed response is a hash representing city and state information.

```ruby
require 'cucumber/rspec/doubles'  
  
RSpec::Mocks.with_temporary_scope do  
stub_resp = {"city"=>"San Francisco", "state_abbreviation"=>"CA", "state"=>"California", "mailable_city"=>true}
SmartyStreets.stub(:get_city_state).with("94109").and_return(stub_resp)  

click_button "check zip"  
end  

```

--------------------------------

### Cucumber Data Table Collections

Source: https://cucumber.io/docs/cucumber/api

Illustrates the various collection types that can be used to access Gherkin data tables as the last parameter in a step definition. Cucumber automatically performs the conversion to these types.

```java
List<List<String>> table
List<Map<String, String>> table
Map<String, String> table
Map<String, List<String>> table
Map<String, Map<String, String>> table
```

--------------------------------

### Add Cucumber-Java and Cucumber-JUnit Gradle Dependencies (4.10.3 or older)

Source: https://cucumber.io/docs/installation/java

This snippet provides the dependencies for Gradle versions 4.10.3 and older, including cucumber-java and cucumber-junit. It also specifies the mavenCentral() repository.

```gradle
dependencies {
    testCompile 'io.cucumber:cucumber-java:7.33.0'
    testCompile 'io.cucumber:cucumber-junit:7.33.0'
}

repositories {
    mavenCentral()
}
```

--------------------------------

### Lambda-Defined Default Transformers in Java

Source: https://cucumber.io/docs/cucumber/configuration

This Java code snippet shows lambda-defined default transformers for parameters, data table cells, and data table entries using the io.cucumber.java8.En interface. It utilizes Jackson's ObjectMapper for conversion, offering a concise alternative to annotation-based transformers.

```java
package com.example;
  
import io.cucumber.java8.En;
  
import com.fasterxml.jackson.databind.ObjectMapper;
  
import java.lang.reflect.Type;
  
public class LambdaStepDefinitions implements En {
  
    public LambdaStepDefinitions() {
        ObjectMapper objectMapper = new ObjectMapper();
  
        DefaultParameterTransformer((String fromValue, Type toValueType) ->
            objectMapper.convertValue(fromValue, objectMapper.constructType(toValueType)));
  
        DefaultDataTableCellTransformer((fromValue, toValueType) ->

```

--------------------------------

### Define Custom Book Parameter Type in Java

Source: https://cucumber.io/docs/cucumber/configuration

This Java code snippet shows how to define a custom 'Book' parameter type using the @ParameterType annotation. It converts a string matched by a regular expression into a Book object. This allows for more expressive step definitions.

```java
package com.example;
  
import io.cucumber.java.ParameterType;
import io.cucumber.java.en.Given;
  
public class StepDefinitions {
  
    @ParameterType(".*")
    public Book book(String bookName) {
    	return new Book(bookName);
    }
  
    @Given("{book} is my favorite book")
    public void this_is_my_favorite_book(Book book) {
        // step implementation
    }
}
```

--------------------------------

### Use Custom Person Parameter Type in Ruby Step Definition

Source: https://cucumber.io/docs/cucumber/configuration

Demonstrates how to use the custom 'person' parameter type within a Ruby step definition. The 'person' argument is automatically converted to a Person object before being passed to the step.

```ruby
Then('a user {person} should have {int} followers') do |person, count|
  puts person.is_a?(Person)
end
```

--------------------------------

### Define Custom UUID Generator in Java

Source: https://cucumber.io/docs/cucumber/state

Implement a custom UUID generator by creating a Java class that implements the `UuidGenerator` interface. This allows for custom logic in generating unique identifiers for events.

```java
package mypackage.mysubpackage;
import io.cucumber.core.eventbus.UuidGenerator;
public class MyUuidGenerator implements UuidGenerator {
  @Override
  public UUID generateId() {
      return ...
  }
}
```

--------------------------------

### Set Default Cucumber Profile

Source: https://cucumber.io/docs/cucumber/configuration

This YAML snippet configures a `default` profile in `cucumber.yml`. When Cucumber is run without explicitly specifying a profile, it will use the command-line options defined in the `default` profile.

```yaml
## ##YAML Template  
default: --profile html_report --profile bvt  
html_report: --format progress --format html --out=features_report.html  
bvt: --tags @bvt  
```

--------------------------------

### Cucumber JUnit Runner Class - Kotlin

Source: https://cucumber.io/docs/cucumber/api

An empty Kotlin class annotated to run Cucumber tests using JUnit. It specifies `io.cucumber.junit.Cucumber` as the runner and uses `@CucumberOptions` for configuration.

```kotlin
package com.example

import io.cucumber.junit.Cucumber
import io.cucumber.junit.CucumberOptions
import org.junit.runner.RunWith

@RunWith(Cucumber::class)
@CucumberOptions()
class RunCucumberTest
```

--------------------------------

### Register Custom UUID Generator with SPI

Source: https://cucumber.io/docs/cucumber/state

Register a custom UUID generator using the Service Provider Interface (SPI) mechanism. Create a file named `io.cucumber.code.eventbus.UuidGenerator` in the `META-INF/services` directory on the classpath, containing the fully qualified name of your custom generator class.

```text
mypackage.mysubpackage.MyUuidGenerator
```

--------------------------------

### Add Quarkus Dependency for Cucumber JVM

Source: https://cucumber.io/docs/cucumber/state

This snippet shows how to add the Quarkus-Cucumber dependency for JVM projects using Maven or Gradle. This integrates Cucumber with the Quarkus framework.

```xml
<dependency>
    <groupId>io.quarkiverse.cucumber</groupId>
    <artifactId>quarkus-cucumber</artifactId>
    <version>{quarkus-cucumber.version}</version>
    <scope>test</scope>
</dependency>
```

```gradle
testImplementation("io.quarkiverse.cucumber:quarkus-cucumber:{quarkus-cucumber.version}")
```

--------------------------------

### Define Profiled Rake Tasks for Cucumber

Source: https://cucumber.io/docs/tools/ruby

This Ruby code defines Rake tasks that utilize Cucumber profiles for complex test runs. It sets up 'non_js' and 'selenium' tasks, each associated with a specific profile defined in Cucumber's configuration.

```ruby
require 'rubygems'  
require 'cucumber'  
require 'cucumber/rake/task'  

namespace :features do  
  Cucumber::Rake::Task.new(:non_js) do |t|  
    t.profile = "webrat"  
  end  
  
  Cucumber::Rake::Task.new(:selenium) do |t|  
    t.profile = "selenium"  
  end  
end  

```

--------------------------------

### Default Parameter Transformer in Java

Source: https://cucumber.io/docs/cucumber/configuration

This Java code snippet demonstrates using @DefaultParameterTransformer, @DefaultDataTableEntryTransformer, and @DefaultDataTableCellTransformer annotations to plug in an object mapper (Jackson) for automatic type conversion. This simplifies handling various parameter and data table types.

```java
package com.example;
  
import com.fasterxml.jackson.databind.ObjectMapper;
import io.cucumber.java.DefaultDataTableCellTransformer;
import io.cucumber.java.DefaultDataTableEntryTransformer;
import io.cucumber.java.DefaultParameterTransformer;
  
import java.lang.reflect.Type;
  
public class StepDefinitions {
  
    private final ObjectMapper objectMapper = new ObjectMapper();
  
    @DefaultParameterTransformer
    @DefaultDataTableEntryTransformer
    @DefaultDataTableCellTransformer
    public Object transformer(Object fromValue, Type toValueType) {
        return objectMapper.convertValue(fromValue, objectMapper.constructType(toValueType));
    }
}
```

--------------------------------

### Lambda-Defined Parameter Types in Java

Source: https://cucumber.io/docs/cucumber/configuration

This Java code snippet shows how to define custom parameter, data table, and doc string types using lambda expressions with the io.cucumber.java8.En interface. This provides a more concise way to register types compared to annotations.

```java
package com.example;
  
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
  
import io.cucumber.java8.En;
  
import java.util.Map;
  
public class LambdaStepDefinitions implements En {
  
    private static ObjectMapper objectMapper = new ObjectMapper();
  
    public LambdaStepDefinitions() {
  
        DataTableType((Map<String, String> entry) -> new Author(
            entry.get("firstName"),
            entry.get("lastName"),
            entry.get("famousBook")
        ));
  
        ParameterType("book", ".*", (String bookName) -> new Book(bookName));
  
        DocStringType("json", (String docString) ->
            objectMapper.readValue(docString, JsonNode.class));
    }
}
```

--------------------------------

### Define Custom Author Data Table Type in Java

Source: https://cucumber.io/docs/cucumber/configuration

This Java code snippet demonstrates how to define a custom 'Author' data table type using the @DataTableType annotation. It converts a Map<String, String> entry into an Author object. This is useful for transforming data table rows into domain objects.

```java
package com.example;
  
import io.cucumber.java.DataTableType;
import io.cucumber.java.en.Given;
  
import java.util.List;
import java.util.Map;
  
public class StepDefinitions {
  
    @DataTableType
    public Author authorEntry(Map<String, String> entry) {
        return new Author(
            entry.get("firstName"),
            entry.get("lastName"),
            entry.get("famousBook"));
    }
  
    @Given("These are my favorite authors")
    public void these_are_my_favourite_authors(List<Author> authors) {
        // step implementation
    }
}
```

--------------------------------

### Add Cucumber-Scala Sbt Dependency

Source: https://cucumber.io/docs/installation/scala

This snippet demonstrates how to add the Cucumber-Scala dependency to your Sbt project. It's crucial to use the same version as other Cucumber dependencies. The dependency is marked for the 'Test' configuration.

```scala
libraryDependencies += "io.cucumber" %% "cucumber-scala" % "6.10.4" % Test
```

--------------------------------

### Java JUnit 4 Maven Dependencies for Assertions

Source: https://cucumber.io/docs/cucumber/checking-assertions

These are the Maven dependencies required to use JUnit 4 assertions with Cucumber. Ensure the versions of 'junit' and 'cucumber-junit' are compatible with your project. The 'cucumber-junit' version should match your 'cucumber-java' or 'cucumber-java8' version.

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>6.0.2</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-junit</artifactId>
    <version>7.33.0</version>
    <scope>test</scope>
</dependency>
```

--------------------------------

### Add Cucumber-Java Maven Dependency

Source: https://cucumber.io/docs/installation/java

This snippet shows how to add the cucumber-java dependency to your Maven project's pom.xml file. Ensure the version matches other Cucumber dependencies.

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-java</artifactId>
    <version>7.33.0</version>
    <scope>test</scope>
</dependency>
```

--------------------------------

### Cucumber JUnit Runner Class - Java

Source: https://cucumber.io/docs/cucumber/api

An empty Java class annotated to run Cucumber tests using JUnit. It specifies `io.cucumber.junit.Cucumber` as the runner and uses `@CucumberOptions` for configuration.

```java
package com.example;

import io.cucumber.junit.Cucumber;
import io.cucumber.junit.CucumberOptions;
import org.junit.runner.RunWith;

@RunWith(Cucumber.class)
@CucumberOptions()
public class RunCucumberTest {
}
```

--------------------------------

### Define Custom Book Parameter Type in Java

Source: https://cucumber.io/docs/cucumber/configuration

Registers a custom 'Book' parameter type using a regular expression to capture book names. This enables Cucumber to convert string parameters in step definitions into Book objects.

```java
package com.example
  
import io.cucumber.java.ParameterType
import io.cucumber.java.en.Given
  
class StepDefinitions {
  
    @ParameterType(".*")
    fun book(bookName: String): Book {
        return Book(bookName)
    }
  
    @Given("{book} is my favorite book")
    fun this_is_my_favorite_book(book: Book) {
        // step implementation
    }
}
```

--------------------------------

### Define Custom Book Parameter Type in Scala

Source: https://cucumber.io/docs/cucumber/configuration

Registers a custom 'book' parameter type. It takes a string (bookName) and transforms it into a Book object. This allows for more expressive step definitions by directly using custom types.

```scala
package com.example
  
import io.cucumber.scala.{ScalaDsl, EN}
  
class StepDefinitions extends ScalaDsl with EN {
  
    ParameterType("book", ".*") { bookName: String =>
        Book(bookName)
    }
  
    Given("{book} is my favorite book") { book: Book =>
        // step implementation
    }
}
```

--------------------------------

### Define Custom Author Data Table Type in Java

Source: https://cucumber.io/docs/cucumber/configuration

Registers a custom 'Author' data table type by mapping map entries to Author object properties. This allows Cucumber to automatically convert data table rows into Author objects for step definitions.

```java
package com.example
  
import io.cucumber.java.DataTableType
import io.cucumber.java.en.Given
import kotlin.streams.toList
  
class StepDefinitions {
  
    @DataTableType
    fun authorEntry(entry: Map<String, String>): Author {
        return Author(
                entry["firstName"],
                entry["lastName"],
                entry["famousBook"])
    }
  
    @Given("There are my favorite authors")
    fun these_are_my_favourite_authors(authors: List<Author>) {
        // step implementation
    }
}
```

--------------------------------

### Define Custom JSON Doc String Type in Java

Source: https://cucumber.io/docs/cucumber/configuration

Registers a custom type for doc strings, converting a string into a Jackson JsonNode. This is useful for handling JSON payloads within step definitions.

```java
package com.example
  
import com.fasterxml.jackson.core.JsonProcessingException
import com.fasterxml.jackson.databind.JsonNode
import com.fasterxml.jackson.databind.ObjectMapper
import io.cucumber.java.DocStringType
import io.cucumber.java.en.Given
  
class StepsDefinitions {
  
    companion object {
        private val objectMapper = ObjectMapper()
    }
  
    @DocStringType
    @Throws(JsonProcessingException::class)
    fun json(docString: String): JsonNode {
        return objectMapper.readValue(docString, JsonNode::class)
    }
  
    @Given("Books are defined by json")
    fun books_are_defined_by_json(books: JsonNode) {
        // step implementation
    }
}
```

--------------------------------

### Cucumber JUnit Runner Class - Scala

Source: https://cucumber.io/docs/cucumber/api

An empty Scala class annotated to run Cucumber tests using JUnit. It specifies `classOf[Cucumber]` as the runner and uses `@CucumberOptions` for configuration.

```scala
package com.example

import io.cucumber.junit.Cucumber
import io.cucumber.junit.CucumberOptions
import org.junit.runner.RunWith

@RunWith(classOf[Cucumber])
@CucumberOptions()
class RunCucumberTest
```

--------------------------------

### Define Custom JSON Doc String Type in Java

Source: https://cucumber.io/docs/cucumber/configuration

This Java code snippet illustrates defining a custom doc string type for JSON using the @DocStringType annotation. It parses a string into a Jackson JsonNode object. This is useful for handling structured data passed as doc strings.

```java
package com.example;
  
import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
import io.cucumber.java.DocStringType;
import io.cucumber.java.en.Given;
  
public class StepsDefinitions {
  
    private static ObjectMapper objectMapper = new ObjectMapper();
  
    @DocStringType
    public JsonNode json(String docString) throws JsonProcessingException {
        return objectMapper.readValue(docString, JsonNode.class);
    }
  
    @Given("Books are defined by json")
    public void books_are_defined_by_json(JsonNode books) {
        // step implementation
    }
}
```

--------------------------------

### Define Custom JSON Doc String Type in Scala

Source: https://cucumber.io/docs/cucumber/configuration

Registers a custom 'json' doc string type. It takes a string (docString) and parses it into a Jackson JsonNode object. This is useful for handling JSON payloads within doc strings in feature files.

```scala
package com.example
  
import com.fasterxml.jackson.core.JsonProcessingException
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper
import io.cucumber.scala.{ScalaDsl, EN}
  
object StepsDefinitions {
    private val objectMapper = ObjectMapper()
}
  
class StepsDefinitions extends ScalaDsl with EN {
  
    DocStringType("json") { docString: String =>
        objectMapper.readValue(docString, classOf[JsonNode])
    }
  
    Given("Books are defined by json") { books: JsonNode =>
        // step implementation
    }
}
```

--------------------------------

### Cucumber Data Table Cell Escaping

Source: https://cucumber.io/docs/gherkin/reference

Explains how to escape special characters within Data Table cells. Newlines are escaped with `\n`, pipe symbols with `\|`, and backslashes with `\\`. This allows for more complex data representation within tables.

```gherkin
# Example of escaping:
# | cell with \n newline | cell with \| pipe | cell with \\ backslash |
# This is a conceptual example, actual Gherkin syntax for escaping is within the table definition itself.
```

--------------------------------

### Define Custom Author Data Table Type in Scala

Source: https://cucumber.io/docs/cucumber/configuration

Registers a custom 'Author' data table type. It takes a map of strings and returns an Author object. This is useful for converting structured data from tables in feature files into objects for step definitions.

```scala
package com.example
  
import io.cucumber.scala.{ScalaDsl, EN}
  
class StepDefinitions extends ScalaDsl with EN {
  
    DataTableType { entry: Map[String, String] =>
        Author(
            entry("firstName"),
            entry("lastName"),
            entry("famousBook"))
    }
  
    Given("There are my favorite authors") { authors: List[Author] =>
        // step implementation
    }
}
```

--------------------------------

### Add Cucumber-Scala Maven Dependency

Source: https://cucumber.io/docs/installation/scala

This snippet shows how to add the Cucumber-Scala dependency to your Maven project. Ensure the version matches other Cucumber dependencies. The scope is set to 'test'.

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-scala_2.13</artifactId>
    <version>6.10.4</version>
    <scope>test</scope>
</dependency>
```

--------------------------------

### Define Custom Person Parameter Type in Ruby

Source: https://cucumber.io/docs/cucumber/configuration

Defines a custom 'person' parameter type in Ruby. It uses a regular expression to match names and transforms them into Person objects. This enhances step definition readability.

```ruby
ParameterType(
  name: 'person',
  regexp: /[A-Z][a-z]+/, 
  transformer: -> (name) { Person.new(name) }
)
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.