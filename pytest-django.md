### Installing pytest-django with pip

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/tutorial.rst

Installs pytest-django and its dependencies using pip. This command automatically installs the latest version of pytest.

```bash
pip install pytest-django
```

--------------------------------

### Basic pyproject.toml for setuptools

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/managing_python_path.rst

A basic pyproject.toml file to get started with setuptools. This file is necessary for installing the project in editable mode using pip.

```python
# pyproject.toml
[build-system]
requires = [
    "setuptools>=61.0.0",
]
build-backend = "setuptools.build_meta"
```

--------------------------------

### Running tests with pytest

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/tutorial.rst

Executes the test suite using the pytest command. This replaces the standard manage.py test command.

```bash
pytest
```

--------------------------------

### Configuring Django settings in pyproject.toml

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/tutorial.rst

Specifies the Django settings module to be used for test runs when using pyproject.toml.

```toml
[tool.pytest.ini_options]
DJANGO_SETTINGS_MODULE = "yourproject.settings"
```

--------------------------------

### Using the client fixture

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This example demonstrates how to use the ``client`` fixture, which provides an instance of Django's ``Client``. The ``Client`` is used to simulate user interactions with the application, such as sending HTTP requests. The example shows a simple GET request.

```python
def test_with_client(client):
    response = client.get('/')
    assert response.content == 'Foobar'
```

--------------------------------

### Using the async_client fixture

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This example demonstrates how to use the ``async_client`` fixture, which provides an instance of Django's ``AsyncClient``. The ``AsyncClient`` is used to simulate user interactions with the application asynchronously. This example requires ``pytest-asyncio``.

```python
@pytest.mark.asyncio
async def test_with_async_client(async_client):
    response = await async_client.get('/')
    assert response.content == 'Foobar'
```

--------------------------------

### Installing pytest-django with pip

Source: https://github.com/pytest-dev/pytest-django/blob/main/README.rst

This command installs the pytest-django package using pip, the Python package installer. It allows you to use pytest for testing Django projects.

```bash
pip install pytest-django
```

--------------------------------

### Configuring Django settings in pytest.ini

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/tutorial.rst

Specifies the Django settings module to be used for test runs. This configuration is placed in the pytest.ini file in the project root directory.

```ini
[pytest]
DJANGO_SETTINGS_MODULE = yourproject.settings
```

--------------------------------

### Installing pytest-django with pip

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/index.rst

Installs the pytest-django plugin using pip. This command adds the necessary packages to your Python environment for using pytest with Django.

```bash
$ pip install pytest-django
```

--------------------------------

### Simple Doctest Example

Source: https://github.com/pytest-dev/pytest-django/blob/main/tests/test_doctest.txt

This doctest example demonstrates a simple print statement. It is intended to verify that pytest can execute basic doctests without errors.

```python
>>> print('works')
works
```

--------------------------------

### Configuring pytest to collect tests in Django's default app layouts

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/tutorial.rst

Instructs pytest to collect tests in Django's default app layouts by specifying the python_files option in the pytest.ini file.

```ini
python_files = tests.py test_*.py *_tests.py
```

--------------------------------

### Authenticating a client using force_login or login

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This example demonstrates how to authenticate a user using the ``client`` fixture's ``force_login()`` or ``login()`` methods. This allows you to test views that require authentication. It shows how to create a user and then log them in using the client.

```python
def test_with_authenticated_client(client, django_user_model):
    username = "user1"
    password = "bar"
    user = django_user_model.objects.create_user(username=username, password=password)
    # Use this:
    client.force_login(user)
    # Or this:
    client.login(username=username, password=password)
    response = client.get('/private')
    assert response.content == 'Protected Area'
```

--------------------------------

### Using the AsyncRequestFactory fixture

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This example demonstrates how to use the ``async_rf`` fixture, which provides an instance of Django's ``AsyncRequestFactory``. The ``AsyncRequestFactory`` is used to create mock asynchronous HTTP requests for testing async views. This example requires ``pytest-asyncio``.

```python
from myapp.views import my_view

@pytest.mark.asyncio
async def test_details(async_rf):
    request = await async_rf.get('/customer/details')
    response = my_view(request)
    assert response.status_code == 200
```

--------------------------------

### Using the admin_client fixture

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This example demonstrates how to use the ``admin_client`` fixture, which provides an instance of Django's ``Client`` logged in as an admin user. This fixture simplifies testing admin views.

```python
def test_an_admin_view(admin_client):
    response = admin_client.get('/admin/')
    assert response.status_code == 200
```

--------------------------------

### Creating a virtual environment with make testenv

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/contributing.rst

This command creates a virtual environment using the Makefile. It installs pytest and the latest stable version of Django, providing an isolated environment for testing.

```bash
$ make testenv
```

--------------------------------

### Creating a new user with django_user_model

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This example demonstrates how to use the `django_user_model` fixture to create a new user in the Django database. The fixture provides access to the User model configured for the current Django project, allowing for pluggable apps to be tested regardless of the User model configuration.

```python
def test_new_user(django_user_model):
    django_user_model.objects.create_user(username="someone", password="something")
```

--------------------------------

### Add editable install to requirements.txt

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/managing_python_path.rst

This shows how to add an editable install to your project's requirements.txt file. This ensures that the project is installed in editable mode along with its dependencies.

```python
# requirements.txt
-e .
django
pytest-django
```

--------------------------------

### Using the RequestFactory fixture

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This example demonstrates how to use the ``rf`` fixture, which provides an instance of Django's ``RequestFactory``. The ``RequestFactory`` is used to create mock HTTP requests for testing views. The example also shows how to set the ``request.user`` attribute when using ``RequestFactory``.

```python
from myapp.views import my_view

def test_details(rf, admin_user):
    request = rf.get('/customer/details')
    # Remember that when using RequestFactory, the request does not pass
    # through middleware. If your view expects fields such as request.user
    # to be set, you need to set them explicitly.
    # The following line sets request.user to an admin user.
    request.user = admin_user
    response = my_view(request)
    assert response.status_code == 200
```

--------------------------------

### Installing pytest-xdist

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/usage.rst

Installs the pytest-xdist plugin using pip. This plugin is required for running tests in parallel.

```python
pip install pytest-xdist
```

--------------------------------

### Install project in editable mode using pip

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/managing_python_path.rst

This command installs the project in editable mode using pip. This makes the project code available on the Python path.

```bash
pip install --editable .
```

--------------------------------

### Modify App Before Django Setup

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/configuring_django.rst

This snippet shows how to modify an app before Django is set up using the pytest_load_initial_conftests hook. This allows for early modifications to the application's behavior before Django's setup process.

```python
@pytest.hookimpl(tryfirst=True)
def pytest_load_initial_conftests(early_config, parser, args):
    import project.app.signals

    def noop(*args, **kwargs):
        pass

    project.app.signals.something = noop
```

--------------------------------

### Combining coverage files

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/contributing.rst

These commands combine the individual coverage files generated during parallel testing and generate an HTML coverage report. It requires the coverage tool to be installed.

```Shell
$ coverage combine
```

```Shell
$ coverage html
```

--------------------------------

### Using the Same Database for All xdist Processes

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This code snippet overrides the `django_db_modify_db_settings` fixture to prevent each xdist process from getting its own database. By providing an empty fixture, all tests will use the same database, which is useful when transactional tests are not required.

```python
import pytest


@pytest.fixture(scope='session')
def django_db_modify_db_settings():
    pass
```

--------------------------------

### Randomizing Database Sequences in PostgreSQL

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This code snippet extends the `django_db_setup` fixture to randomize the starting value of a PostgreSQL sequence. This helps detect and prevent hard-coded primary key IDs in tests by altering the sequence before tests are run.

```python
import random
import pytest
from django.db import connection


@pytest.fixture(scope='session')
def django_db_setup(django_db_setup, django_db_blocker):
    with django_db_blocker.unblock():
        cur = connection.cursor()
        cur.execute('ALTER SEQUENCE app_model_id_seq RESTART WITH %s;',
                    [random.randint(10000, 20000)])
```

--------------------------------

### Overriding URL configuration using pytest.mark.urls

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This example demonstrates how to override the default URL configuration for a test using the ``@pytest.mark.urls`` marker. It specifies a different URLconf module (``myapp.test_urls``) to be used for the test, allowing testing of specific URL mappings.

```python
@pytest.mark.urls('myapp.test_urls')
def test_something(client):
    assert b'Success!' in client.get('/some_url_defined_in_test_urls/').content
```

--------------------------------

### Modifying Django settings using the settings fixture

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This example shows how to use the `settings` fixture to temporarily modify Django settings within a test function. The fixture automatically reverts any changes made to the settings after the test completes, ensuring isolation between tests.

```python
def test_with_specific_settings(settings):
    settings.USE_TZ = True
    assert settings.USE_TZ
```

--------------------------------

### Ignoring template errors using pytest.mark.ignore_template_errors

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This example shows how to use the ``@pytest.mark.ignore_template_errors`` marker to prevent tests from failing when templates contain invalid variables. This is useful when you want to temporarily disable template error checking during development.

```python
@pytest.mark.ignore_template_errors
def test_something(client):
    client('some-url-with-invalid-template-vars')
```

--------------------------------

### Running tests with manage.py

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/faq.rst

This code snippet shows how to run tests using the manage.py command after configuring the test runner. It demonstrates how to pass Django arguments and pytest arguments to the test runner.

```Bash
./manage.py test <django args> -- <pytest args>
```

--------------------------------

### Running tests with make test

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/contributing.rst

This command uses the Makefile to set up a virtual environment and run the pytest test suite. It simplifies the process of executing tests within a consistent environment.

```bash
$ make test
```

--------------------------------

### Running tests with tox

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/contributing.rst

This command uses tox to run the test suite under different configurations defined in `tox.ini`. Tox automates the process of testing against multiple Python and Django versions.

```bash
$ tox
```

--------------------------------

### Using Template Database for Tests - Python

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This conftest.py snippet sets up a test database by copying a pre-existing PostgreSQL database. It defines a session-scoped fixture django_db_setup that creates a new database (the_copied_db) as a template of an existing database (the_source_db). It also takes care of cleaning up the copied database after the test session.

```python
import pytest
from django.db import connections

import psycopg


def run_sql(sql):
    with psycopg.connect(database='postgres') as conn:
        conn.execute(sql)


@pytest.fixture(scope='session')
def django_db_setup():
    from django.conf import settings

    settings.DATABASES['default']['NAME'] = 'the_copied_db'

    run_sql('DROP DATABASE IF EXISTS the_copied_db')
    run_sql('CREATE DATABASE the_copied_db TEMPLATE the_source_db')

    yield

    for connection in connections.all():
        connection.close()

    run_sql('DROP DATABASE the_copied_db')
```

--------------------------------

### Creating Test Database from Custom SQL Script (SQLite)

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This code snippet replaces the `django_db_setup` fixture to create the test database from a custom SQL script using SQLite's `executescript` method. It drops an existing table, creates a new one, and inserts data, demonstrating how to fully customize database creation.

```python
import pytest
from django.db import connection


@pytest.fixture(scope='session')
def django_db_setup(django_db_blocker):
    with django_db_blocker.unblock():
        with connection.cursor() as c:
            c.executescript('''
            DROP TABLE IF EXISTS theapp_item;
            CREATE TABLE theapp_item (id, name);
            INSERT INTO theapp_item (name) VALUES ('created from a sql script');
            ''')
```

--------------------------------

### Activating the virtual environment

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/contributing.rst

This command activates the virtual environment created by `make testenv`. Activating the virtual environment ensures that the correct versions of pytest and Django are used for testing.

```bash
$ source bin/activate
```

--------------------------------

### Running pytest with Django settings

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/contributing.rst

This command invokes pytest to run the test suite, specifying the Django settings file to use. The `--ds` option points to the settings file for the test environment.

```bash
$ pytest --ds=pytest_django_test.settings_sqlite
```

--------------------------------

### Running tests with tox for specific environments

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/contributing.rst

This command uses tox to run the test suite for specific environments defined in `tox.ini`. The `-e` flag allows specifying a comma-separated list of environments to test against.

```bash
$ tox -e py38-dj32-postgres,py310-dj41-mysql
```

--------------------------------

### Running tests with pytest

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/index.rst

Executes the pytest test runner. This command discovers and runs all tests in your project, providing feedback on test results.

```bash
$ pytest
```

--------------------------------

### Running pytest with xdist

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/usage.rst

Runs pytest with the xdist plugin to execute tests in parallel using a specified number of processes. Replace <number of processes> with the desired number of processes.

```python
pytest -n <number of processes>
```

--------------------------------

### Running tests with coverage

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/contributing.rst

This command runs pytest with coverage measurement enabled, specifying the configuration file and coverage file location. It requires the pytest-cov plugin and a properly configured coverage environment.

```Shell
$ COVERAGE_PROCESS_START=`pwd`/pyproject.toml COVERAGE_FILE=`pwd`/.coverage pytest --ds=pytest_django_test.settings_postgres
```

--------------------------------

### Populating Test Database (Non-Transactional) - Python

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This conftest.py snippet populates the test database with initial data using Django's loaddata command. It defines a session-scoped fixture django_db_setup that unblocks database access, loads a Django fixture (my_fixture.json), and makes the data available to tests marked with @pytest.mark.django_db or using the db fixture.

```python
import pytest

from django.core.management import call_command

@pytest.fixture(scope='session')
def django_db_setup(django_db_setup, django_db_blocker):
    with django_db_blocker.unblock():
        call_command('loaddata', 'my_fixture.json')
```

--------------------------------

### Type Annotations for django_assert_num_queries Fixture

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This code shows how to use type annotations with the django_assert_num_queries fixture for better code clarity and static analysis.

```python
from pytest_django import DjangoAssertNumQueries

def test_num_queries(
    django_assert_num_queries: DjangoAssertNumQueries,
):
    ...
```

--------------------------------

### Configuring Django settings in pyproject.toml

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/index.rst

Configures the Django settings module in a pyproject.toml file. This allows pytest to locate and use your Django project's settings during testing. It also includes an optional setting for specifying Python test files.

```toml
[tool.pytest.ini_options]
DJANGO_SETTINGS_MODULE = "test.settings"
# -- recommended but optional:
python_files = ["test_*.py", "*_test.py", "testing/python/*.py"]
```

--------------------------------

### Enabling Database Access for All Tests

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/faq.rst

This code snippet demonstrates how to create an autouse fixture that enables database access for all tests without using the django_db marker. By placing this fixture in conftest.py, all tests will automatically have database access. This is useful when most or all of your tests require database access.

```Python
@pytest.fixture(autouse=True)
def enable_db_access_for_all_tests(db):
    pass
```

--------------------------------

### Loading fixture data in tests

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/changelog.rst

Shows how to load fixture data using Django's management command call_command. This replaces the undocumented pytest.load_fixture function.

```python
django.management.call_command('loaddata', 'foo.json')
```

--------------------------------

### Using a Read-Only Database

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This code snippet replaces the `django_db_setup` fixture to avoid database creation and migrations, allowing the use of a read-only database. It also defines a `db_access_without_rollback_and_truncate` fixture that unblocks the database and restores it after use, ensuring no changes are made during the test.

```python
import pytest


@pytest.fixture(scope='session')
def django_db_setup():
    """Avoid creating/setting up the test database"""
    pass


@pytest.fixture
def db_access_without_rollback_and_truncate(request, django_db_setup, django_db_blocker):
    django_db_blocker.unblock()
    yield
    django_db_blocker.restore()
```

--------------------------------

### Running pytest

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/usage.rst

Invokes the pytest command to run tests in the current directory. This command executes all tests found in the current directory and its subdirectories.

```python
pytest
```

--------------------------------

### Capturing on-commit Callbacks with django_capture_on_commit_callbacks

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This code demonstrates how to use the django_capture_on_commit_callbacks fixture to capture transaction.on_commit callbacks and optionally execute them, emulating a commit.

```python
def test_on_commit(client, mailoutbox, django_capture_on_commit_callbacks):
    with django_capture_on_commit_callbacks(execute=True) as callbacks:
        response = client.post(
            '/contact/',
            {'message': 'I like your site'},
        )

    assert response.status_code == 200
    assert len(callbacks) == 1
    assert len(mailoutbox) == 1
    assert mailoutbox[0].subject == 'Contact Form'
    assert mailoutbox[0].body == 'I like your site'
```

--------------------------------

### Running specific pytest tests

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/usage.rst

Runs pytest on specific test files or directories.  This allows you to target specific tests for execution, rather than running the entire test suite.

```python
pytest test_something.py a_directory
```

--------------------------------

### Type Annotations for django_assert_max_num_queries Fixture

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This code shows how to use type annotations with the django_assert_max_num_queries fixture for better code clarity and static analysis.

```python
from pytest_django import DjangoAssertNumQueries

def test_max_num_queries(
    django_assert_max_num_queries: DjangoAssertNumQueries,
):
    ...
```

--------------------------------

### Type Annotations for django_capture_on_commit_callbacks Fixture

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This code shows how to use type annotations with the django_capture_on_commit_callbacks fixture for better code clarity and static analysis.

```python
from pytest_django import DjangoCaptureOnCommitCallbacks

def test_on_commit(
    django_capture_on_commit_callbacks: DjangoCaptureOnCommitCallbacks,
):
    ...
```

--------------------------------

### Accessing the Email Outbox with mailoutbox

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This code demonstrates how to use the mailoutbox fixture to access and assert on emails sent during a test.

```python
from django.core import mail

def test_mail(mailoutbox):
    mail.send_mail('subject', 'body', 'from@example.com', ['to@example.com'])
    assert len(mailoutbox) == 1
    m = mailoutbox[0]
    assert m.subject == 'subject'
    assert m.body == 'body'
    assert m.from_email == 'from@example.com'
    assert list(m.to) == ['to@example.com']
```

--------------------------------

### Configure Django Settings in conftest.py

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/configuring_django.rst

This snippet demonstrates how to configure Django settings programmatically within the conftest.py file using django.conf.settings.configure(). This approach is useful when a DJANGO_SETTINGS_MODULE is not defined.

```python
from django.conf import settings

def pytest_configure():
    settings.configure(DATABASES=...)
```

--------------------------------

### pytest.ini Configuration for Database Reuse

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This code snippet demonstrates how to configure pytest to reuse the database between test runs by adding the `--reuse-db` option to the `addopts` setting in the `pytest.ini` file.

```ini
[pytest]
addopts = --reuse-db
```

--------------------------------

### Configuring Test File Discovery

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/faq.rst

This code snippet shows how to configure pytest to discover test files with specific naming patterns. By adding a python_files line to the pytest.ini file, you can specify which files pytest should consider as test files. This is useful when tests are located in files named differently from the default test_*.py and *_test.py.

```INI
[pytest]
python_files = tests.py test_*.py *_tests.py
```

--------------------------------

### Django Configuration in pyproject.toml

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/configuring_django.rst

This snippet shows how to specify the Django configuration class in the pyproject.toml file. This is used when using django-configurations to configure Django settings.

```toml
[tool.pytest.ini_options]
DJANGO_CONFIGURATION = "MySettings"
```

--------------------------------

### Using Existing External Database - Python

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This conftest.py snippet configures Django to use an existing external database for testing. It defines a session-scoped fixture django_db_setup that overrides the default database settings to point to a MySQL database on a specified host. This disables the creation of a test database and uses the existing one directly.

```python
import pytest


@pytest.fixture(scope='session')
def django_db_setup():
    from django.conf import settings

    settings.DATABASES['default'] = {
        'ENGINE': 'django.db.backends.mysql',
        'HOST': 'db.example.com',
        'NAME': 'external_db',
    }
```

--------------------------------

### Setting Default Language for Tests

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/faq.rst

This code snippet demonstrates how to create a pytest fixture that automatically activates a specific language (in this case, English) before each test case. This ensures that all tests run with the desired locale. It should be placed in the project's conftest.py file.

```Python
from django.utils.translation import activate

@pytest.fixture(autouse=True)
def set_default_language():
    activate('en')
```

--------------------------------

### Asserting Number of Queries with django_assert_num_queries

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This code demonstrates how to use the django_assert_num_queries fixture to assert the exact number of database queries executed within a block of code. It captures the queries and allows inspection of the SQL.

```python
def test_queries(django_assert_num_queries):
    with django_assert_num_queries(3) as captured:
        Item.objects.create('foo')
        Item.objects.create('bar')
        Item.objects.create('baz')

    assert 'foo' in captured.captured_queries[0]['sql']
```

--------------------------------

### Asserting Maximum Number of Queries with django_assert_max_num_queries

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This code demonstrates how to use the django_assert_max_num_queries fixture to assert the maximum number of database queries executed within a block of code.

```python
def test_max_queries(django_assert_max_num_queries):
    with django_assert_max_num_queries(2):
        Item.objects.create('foo')
        Item.objects.create('bar')
```

--------------------------------

### Integrating pytest-django with manage.py test

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/faq.rst

This code snippet demonstrates how to integrate pytest-django with Django's manage.py test command. By setting the TEST_RUNNER in Django settings, you can use manage.py test to run tests with pytest-django. Note that pytest-django command line options --ds and --dc are not compatible with this approach.

```Python
TEST_RUNNER = 'pytest_django.runner.TestRunner'
```

--------------------------------

### Configuring Django settings in pytest.ini

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/index.rst

Configures the Django settings module in a pytest.ini file. This allows pytest to locate and use your Django project's settings during testing. It also includes an optional setting for specifying Python test files.

```ini
[pytest]
DJANGO_SETTINGS_MODULE = test.settings
# -- recommended but optional:
python_files = tests.py test_*.py *_tests.py
```

--------------------------------

### Using Django Assertions in pytest-django

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/helpers.rst

This code snippet demonstrates how to import and use Django's assertions, such as assertTemplateUsed, within pytest-django tests. It shows the basic import statement required to access these assertions.

```python
from pytest_django.asserts import assertTemplateUsed
```

--------------------------------

### Configure pythonpath and Django settings in pytest.ini

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/managing_python_path.rst

This configuration shows how to specify the Django settings module and add paths to the Python search path using pytest's pythonpath option. This is useful for projects with a src layout.

```ini
[pytest]
DJANGO_SETTINGS_MODULE = tests.settings
pythonpath = . src
```

--------------------------------

### Enable Database Access with Context Manager - Python

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This fixture demonstrates how to temporarily enable database access within a specific code block using the django_db_blocker as a context manager. The unblock() method allows database operations within the 'with' statement, ensuring that database access is properly managed and restricted when not needed.

```python
@pytest.fixture
def myfixture(django_db_blocker):
    with django_db_blocker.unblock():
        ...  # modify something in the database
```

--------------------------------

### Django Settings in pyproject.toml

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/configuring_django.rst

This snippet demonstrates how to configure the Django settings module within the pyproject.toml file for pytest. This configuration enables pytest to discover and utilize the specified Django settings during test execution.

```toml
[tool.pytest.ini_options]
DJANGO_SETTINGS_MODULE = "test.settings"
```

--------------------------------

### Enabling Database Access with django_db Mark

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This code snippet demonstrates how to use the `django_db` mark to enable database access for a specific test function in pytest-django. The test function `test_my_user` retrieves a user from the database and asserts that the user is a superuser. Requires pytest and Django User model.

```python
import pytest

@pytest.mark.django_db
def test_my_user():
    me = User.objects.get(username='me')
    assert me.is_superuser
```

--------------------------------

### Django Settings in pytest.ini

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/configuring_django.rst

This snippet shows how to specify the Django settings module in the pytest.ini configuration file. This allows pytest to locate and load the Django settings for running tests.

```ini
[pytest]
DJANGO_SETTINGS_MODULE = test.settings
```

--------------------------------

### Accessing Multiple Databases with django_db Mark

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This code snippet shows how to access multiple databases using the `django_db` mark with the `databases` argument. It specifies the databases to be used by the test. Requires pytest and Django model.

```python
@pytest.mark.django_db(databases=['default', 'other'])
def test_spam():
    assert MyModel.objects.using('other').count() == 0
```

--------------------------------

### Marking a Class with django_db for Database Access

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This code snippet shows how to mark an entire test class with the `django_db` mark, enabling database access for all test methods within the class. It also demonstrates how to mark the module itself. Requires pytest and Django User model.

```python
import pytest

pytestmark = pytest.mark.django_db

@pytest.mark.django_db
class TestUsers:
    pytestmark = pytest.mark.django_db
    def test_my_user(self):
        me = User.objects.get(username='me')
        assert me.is_superuser
```

--------------------------------

### Testing Transactions with django_db Mark

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This code snippet demonstrates how to test transactions using the `django_db` mark with the `transaction=True` argument. This ensures that the database is flushed between tests to isolate them. Requires pytest.

```python
@pytest.mark.django_db(transaction=True)
def test_spam():
    pass  # test relying on transactions
```

--------------------------------

### Enabling fail-on-template-vars in pytest.ini

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/usage.rst

Enables the fail-on-template-vars option in the pytest.ini file. This setting causes tests to fail if they render templates with invalid template variables.

```ini
[pytest]
FAIL_INVALID_TEMPLATE_VARS = True
```

--------------------------------

### Marking tests for Django database access

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/changelog.rst

Demonstrates how to mark tests that require database access using the pytest.mark.django_db marker. This is necessary for tests that interact with the Django database.

```python
pytestmark = pytest.mark.django_db
```

```python
@pytest.mark.django_db
```

--------------------------------

### Django Configuration in pytest.ini

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/configuring_django.rst

This snippet shows how to specify the Django configuration class in the pytest.ini file. This is used when using django-configurations to configure Django settings.

```ini
[pytest]
DJANGO_CONFIGURATION=MySettings
```

--------------------------------

### Disable automatic Django project finder in pytest

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/managing_python_path.rst

This configuration disables the automatic Django project finder in pytest-django. It should be added to pytest.ini, setup.cfg, or tox.ini.

```ini
[pytest]
django_find_project = false
```

--------------------------------

### Setting django_debug_mode in pytest.ini

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/usage.rst

Sets the django_debug_mode option in the pytest.ini file to true. This configures tests to run with the Django DEBUG setting set to True.

```ini
[pytest]
django_debug_mode = true
```

--------------------------------

### Override Django Settings with Fixture

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/configuring_django.rst

This snippet demonstrates how to override Django settings using a pytest fixture. The fixture is automatically applied to all tests and modifies the CACHES setting.

```python
@pytest.fixture(autouse=True)
def use_dummy_cache_backend(settings):
    settings.CACHES = {
        "default": {
            "BACKEND": "django.core.cache.backends.dummy.DummyCache",
        }
    }
```

--------------------------------

### Accessing Django Models in Fixtures (Function Scope)

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/database.rst

This code snippet demonstrates how to access and interact with Django models within a pytest fixture. It creates a `Widget` object using the Django ORM within the fixture's scope, ensuring the object is available for tests that use the fixture.

```python
from myapp.models import Widget

@pytest.fixture(scope='function')
def django_db_setup(django_db_setup, django_db_blocker):
    with django_db_blocker.unblock():
        Widget.objects.create(...)
```

--------------------------------

### Clearing Django mail outbox in conftest.py

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/changelog.rst

This code snippet demonstrates how to clear the Django mail outbox in your project's conftest.py file. This is a workaround for older versions of pytest-django where the internal `_django_clear_outbox` fixture was removed. It ensures that the mail.outbox is empty before each test.

```python
@pytest.fixture(autouse=True)
def clear_outbox():
    from django.core import mail
    mail.outbox = []
```

--------------------------------

### Keeping existing DEBUG setting in pytest.ini

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/usage.rst

Sets the django_debug_mode option in the pytest.ini file to keep. This disables the overriding of the DEBUG setting and uses whatever is already set in the Django settings.

```ini
[pytest]
django_debug_mode = keep
```

--------------------------------

### Disable Django project discovery in pytest

Source: https://github.com/pytest-dev/pytest-django/blob/main/docs/changelog.rst

This configuration snippet disables the automatic discovery of Django projects. This can be useful to restore the old behavior if the automatic discovery causes issues.

```ini
[pytest]
django_find_project = false
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.