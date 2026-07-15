### Implement pytest_runtest_setup hook in conftest.py

Source: https://docs.pytest.org/en/stable/how-to/writing_plugins

This snippet demonstrates how to implement the `pytest_runtest_setup` hook within a `conftest.py` file to execute specific setup actions for tests within a particular directory. It shows the hook implementation and example test files.

```python
a/conftest.py:
    def pytest_runtest_setup(item):
        # called for running each test in 'a' directory
        print("setting up", item)

a/test_sub.py:
    def test_sub():
        pass

test_flat.py:
    def test_flat():
        pass

```

--------------------------------

### Pytest Test Module Example

Source: https://docs.pytest.org/en/stable/how-to/capture-stdout-stderr

A simple pytest module demonstrating test functions and setup. It shows how pytest executes tests and reports failures, including captured output during setup.

```python
def setup_function(function):
    print("setting up", function)

def test_func1():
    assert True

def test_func2():
    assert False
```

--------------------------------

### Get help and version information with pytest

Source: https://docs.pytest.org/en/stable/how-to/usage

These commands provide essential help and information about pytest. `--version` shows the installation path, `--fixtures` lists available fixtures, and `-h` or `--help` displays command-line and configuration options.

```bash
pytest --version
```

```bash
pytest --fixtures
```

```bash
pytest -h
```

```bash
pytest --help
```

--------------------------------

### Define pytest plugin entry point in pyproject.toml

Source: https://docs.pytest.org/en/stable/how-to/writing_plugins

This example shows how to define a pytest plugin's entry point in a `pyproject.toml` file, making the plugin discoverable by pytest when installed. It specifies the build system, project metadata, and the `pytest11` entry point configuration.

```toml
# sample ./pyproject.toml file
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "myproject"
classifiers = [
    "Framework :: Pytest",
]

[project.entry-points.pytest11]
myproject = "myproject.pluginmodule"

```

--------------------------------

### Setup, Teardown, and Parent Iteration

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

Documents the placeholder `setup` and `teardown` methods, and the `iter_parents` method for traversing the collection tree upwards.

```APIDOC
## setup, teardown, and iter_parents

### Description
Includes placeholder `setup` and `teardown` methods that can be overridden by subclasses for node-specific setup and cleanup. The `iter_parents` method iterates over all parent collectors, starting from the node itself up to the root of the collection tree.

### Method
`setup`, `teardown`, `iter_parents`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```python
node.setup() # Typically called internally by pytest
node.teardown() # Typically called internally by pytest

for parent_node in node.iter_parents():
    print(parent_node.name)
```

### Response
#### Success Response (200)
- **setup** (None) - Placeholder method.
- **teardown** (None) - Placeholder method.
- **iter_parents** (Iterator[Node]) - An iterator yielding parent nodes.

#### Response Example
```json
{
  "setup": null,
  "teardown": null,
  "iter_parents": "<generator object Node.iter_parents at 0x...>"
}
```
```

--------------------------------

### Nose Setup/Teardown vs. Pytest Methods (Python)

Source: https://docs.pytest.org/en/stable/deprecations

Compares the deprecated `setup` and `teardown` methods from Nose support with the native Pytest `setup_method` and `teardown_method`. The example shows how to migrate from the Nose-style to the Pytest-native approach.

```Python
class Test:
    def setup(self):
        self.resource = make_resource()

    def teardown(self):
        self.resource.close()

    def test_foo(self): ...

    def test_bar(self): ...

```

```Python
class Test:
    def setup_method(self):
        self.resource = make_resource()

    def teardown_method(self):
        self.resource.close()

    def test_foo(self): ...

    def test_bar(self): ...

```

--------------------------------

### Copying Example Files with Pytester

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Copies example files or directories to the test's temporary path. It resolves example paths based on configuration and markers, handling both file and directory sources. Raises LookupError if the example is not found.

```python
def copy_example(self, name: str | None = None) -> Path:
    """Copy example file or directory to the test path.

    :rtype: pathlib.Path
    """
    example_dir_ = self._request.config.getini("pytester_example_dir")
    if example_dir_ is None:
        raise ValueError("pytester_example_dir is unset, can't copy examples")
    example_dir: Path = self._request.config.rootpath / example_dir_

    for extra_element in self._request.node.iter_markers("pytester_example_path"):
        assert extra_element.args
        example_dir = example_dir.joinpath(*extra_element.args)

    if name is None:
        func_name = self._name
        maybe_dir = example_dir / func_name
        maybe_file = example_dir / (func_name + ".py")

        if maybe_dir.is_dir():
            example_path = maybe_dir
        elif maybe_file.is_file():
            example_path = maybe_file
        else:
            raise LookupError(
                f"{func_name} can't be found as module or package in {example_dir}"
            )
    else:
        example_path = example_dir.joinpath(name)

    if example_path.is_dir() and not example_path.joinpath("__init__.py").is_file():
        shutil.copytree(example_path, self.path, symlinks=True, dirs_exist_ok=True)
        return self.path
    elif example_path.is_file():
        result = self.path.joinpath(example_path.name)
        shutil.copy(example_path, result)
        return result
    else:
        raise LookupError(
            f'example "{example_path}" is not found as a file or directory'
        )

```

--------------------------------

### Install and Uninstall pytest Plugins

Source: https://docs.pytest.org/en/stable/how-to/plugins

Demonstrates the basic pip commands for installing and uninstalling third-party pytest plugins. Ensure you replace 'pytest-NAME' with the actual plugin name.

```bash
pip install pytest-NAME
pip uninstall pytest-NAME
```

--------------------------------

### Install Tox for Testing (Python/Bash)

Source: https://docs.pytest.org/en/stable/contributing

This snippet demonstrates how to install tox, a tool used for automating testing in different virtual environments, using pip.

```bash
$ pip install tox
```

--------------------------------

### Copy Example Files with pytester.copy_example

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `copy_example` method copies a file from the project's example directory into the test directory managed by pytester. It takes the filename as an argument and returns the path to the copied file.

```python
def copy_example(self, name: str | None = None) -> Path:
    """Copy file from project's directory into the testdir.

    :param name:
        The name of the file to copy.
    :return:
        Path to the copied directory (inside ``self.path``).
    """
    # Implementation details omitted for brevity
```

--------------------------------

### Install and Install Pre-commit Hooks (Python/Bash)

Source: https://docs.pytest.org/en/stable/contributing

This snippet covers installing the pre-commit tool using pip and then installing its hooks into the pytest repository to automate code style checks before commits.

```bash
$ pip install --user pre-commit
$ pre-commit install
```

--------------------------------

### Configure Pytester Example Directory

Source: https://docs.pytest.org/en/stable/how-to/writing_plugins

Configures pytest to look for example files in the current directory for use with 'pytester.copy_example'. This is specified in the pytest.toml configuration file.

```toml
# content of pytest.toml
[pytest]
pytester_example_dir = "."
```

--------------------------------

### Editable Install and Run Pytest Directly (Python/Bash)

Source: https://docs.pytest.org/en/stable/contributing

This snippet details how to set up a virtual environment, activate it, install pytest in editable mode with the 'dev' extra, and then run pytest tests directly.

```bash
$ python3 -m venv .venv
$ source .venv/bin/activate  # Linux
$ .venv/Scripts/activate.bat  # Windows
$ pip install -e ".[dev]"
$ pytest testing/test_config.py
```

--------------------------------

### Copy example file with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Copies an example file from the pytest test suite into the test directory. If no name is specified, it attempts to copy a default example. The path to the copied file is returned as a legacy_path object.

```python
def copy_example(self, name=None) -> LEGACY_PATH:
    """See :meth:`Pytester.copy_example`."""
    return legacy_path(self._pytester.copy_example(name))
```

--------------------------------

### Install and Verify Pytest

Source: https://docs.pytest.org/en/stable/getting-started

Instructions to install the pytest package using pip and verify the installation by checking the pytest version.

```bash
pip install -U pytest
pytest --version
```

--------------------------------

### Display Pytest Help and Configuration Options

Source: https://docs.pytest.org/en/stable/reference/customize

This command displays all available command-line options and configuration file settings registered by installed plugins. It's a useful starting point for understanding pytest's capabilities.

```bash
pytest -h   # prints options _and_ config file settings
```

--------------------------------

### pytest_runtest_setup

Source: https://docs.pytest.org/en/stable/reference/reference

Called to perform the setup phase for a test item. The default implementation runs `setup()` on the item and its parents.

```APIDOC
## pytest_runtest_setup

### Description
Called to perform the setup phase for a test item. The default implementation runs `setup()` on `item` and all of its parents (which haven’t been setup yet). This includes obtaining the values of fixtures required by the item (which haven’t been obtained yet).

### Method
HOOK

### Endpoint
N/A (Hook)

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

### Parameters
* **item** (_Item_) – The item.
```

--------------------------------

### Copy and Run Example Test with Pytester

Source: https://docs.pytest.org/en/stable/how-to/writing_plugins

Demonstrates using 'pytester.copy_example' to copy a test file into the isolated test environment and then running pytest on it. This is useful for testing more complex plugin interactions.

```python
# content of test_example.py


def test_plugin(pytester):
    pytester.copy_example("test_example.py")
    pytester.runpytest("-k", "test_example")


def test_example():
    pass
```

--------------------------------

### Pytest Fixture Not Found Error Example

Source: https://docs.pytest.org/en/stable/example/simple

Demonstrates a common Pytest error where a test function requests a fixture ('db') that is not available in its scope. This results in an 'ERROR at setup' message, listing available fixtures.

```python
def test_root(db):  # no db here, will error out
    pass
```

--------------------------------

### Install or Upgrade pytest using pip or easy_install

Source: https://docs.pytest.org/en/stable/announce/release-2.1.3

This snippet shows how to install or upgrade the pytest package using either pip or easy_install. It's a common task for users to ensure they have the latest version or to install pytest for the first time.

```shell
pip install -U pytest # or
easy_install -U pytest

```

--------------------------------

### Pytest with Failing Fixtures and Tests

Source: https://docs.pytest.org/en/stable/example/simple

This Python code defines a test module with a failing fixture and several tests that depend on it or have their own failures. It showcases how pytest reports errors during fixture setup and test execution, including scenarios where setup fails, call fails, or simple assertions fail.

```python
import pytest


@pytest.fixture
def other():
    assert 0


def test_setup_fails(something, other):
    pass


def test_call_fails(something):
    assert 0


def test_fail2():
    assert 0

```

--------------------------------

### Get Pytest Session Start Directory with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

The `Session_startdir` function returns the path from which pytest was invoked during a session. It returns a legacy `py.path.local` object, but `startpath` (a `pathlib.Path`) is preferred.

```python
def Session_startdir(self: Session) -> LEGACY_PATH:
    """The path from which pytest was invoked.

    Prefer to use ``startpath`` which is a :class:`pathlib.Path`.

    :type: LEGACY_PATH
    """
    return legacy_path(self.startpath)
```

--------------------------------

### Implementing xunit-style setup/teardown with pytest

Source: https://docs.pytest.org/en/stable/contents

Explains how to implement xunit-style setup and teardown methods at various levels (module, class, method/function) using pytest. This is useful for managing resources and ensuring proper cleanup during test execution.

```python
# Module level setup/teardown
def setup_module(module):
    print("\nSetting up module")

def teardown_module(module):
    print("\nTearing down module")

# Class level setup/teardown
class TestMyClass:
    def setup_class(cls):
        print("\nSetting up class")

    def teardown_class(cls):
        print("\nTearing down class")

    # Method and function level setup/teardown
    def setup_method(self, method):
        print("\nSetting up method")

    def teardown_method(self, method):
        print("\nTearing down method")

    def test_example(self):
        assert True

```

--------------------------------

### Manage Test Setup Phase with pytest_runtest_setup

Source: https://docs.pytest.org/en/stable/_modules/_pytest/runner

Implements the pytest_runtest_setup hook to handle the setup phase of a test. It updates the current test variable and calls the session's setup state manager to perform the necessary setup actions for the test item.

```python
import pytest
from _pytest.main import Item

def _update_current_test_var(item: Item, stage: str) -> None:
    # This is a placeholder for the actual implementation
    pass

def pytest_runtest_setup(item: Item) -> None:
    _update_current_test_var(item, "setup")
    item.session._setupstate.setup(item)
```

--------------------------------

### Manage Test Session Setup and Teardown with pytest Hooks

Source: https://docs.pytest.org/en/stable/_modules/_pytest/runner

Implements pytest hooks for managing the test session's setup and teardown phases. pytest_sessionstart initializes a SetupState object, and pytest_sessionfinish ensures that all teardown processes are completed, which is crucial for correctly reporting fixture teardown errors.

```python
import pytest
from _pytest.main import Session
from _pytest.runner import SetupState

def pytest_sessionstart(session: Session) -> None:
    session._setupstate = SetupState()

def pytest_sessionfinish(session: Session) -> None:
    session._setupstate.teardown_exact(None)
```

--------------------------------

### Pytest Fixture Setup and Execution

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

Handles the execution of fixture setup, including argument resolution, calling the fixture function, and managing results and potential exceptions. Issues warnings for deprecated async fixture usage.

```python
def pytest_fixture_setup(
    fixturedef: FixtureDef[FixtureValue], request: SubRequest
) -> FixtureValue:
    """Execution of fixture setup."""
    kwargs = {}
    for argname in fixturedef.argnames:
        kwargs[argname] = request.getfixturevalue(argname)

    fixturefunc = resolve_fixture_function(fixturedef, request)
    my_cache_key = fixturedef.cache_key(request)

    if inspect.isasyncgenfunction(fixturefunc) or inspect.iscoroutinefunction(
        fixturefunc
    ):
        auto_str = " with autouse=True" if fixturedef._autouse else ""

        warnings.warn(
            PytestRemovedIn9Warning(
                f"{request.node.name!r} requested an async fixture "
                f"{request.fixturename!r}{auto_str}, with no plugin or hook that "
                "handled it. This is usually an error, as pytest does not natively "
                "support it. "
                "This will turn into an error in pytest 9.\n"
                "See: https://docs.pytest.org/en/stable/deprecations.html#sync-test-depending-on-async-fixture"
            ),
            # no stacklevel will point at users code, so we just point here
            stacklevel=1,
        )

    try:
        result = call_fixture_func(fixturefunc, request, kwargs)
    except TEST_OUTCOME as e:
        if isinstance(e, skip.Exception):
            # The test requested a fixture which caused a skip.
            # Don't show the fixture as the skip location, as then the user
            # wouldn't know which test skipped.
            e._use_item_location = True
        fixturedef.cached_result = (None, my_cache_key, (e, e.__traceback__))
        raise
    fixturedef.cached_result = (result, my_cache_key, None)
    return result
```

--------------------------------

### Handle Test Collection Start

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

Initiates the test collection process. It writes a 'collecting ...' message to the terminal if the output is a TTY or if verbose mode is enabled.

```python
def pytest_collection(self) -> None:
        if self.isatty():
            if self.config.option.verbose >= 0:
                self.write("collecting ... ", flush=True, bold=True)
        elif self.config.option.verbose >= 1:
            self.write("collecting ... ", flush=True, bold=True)
```

--------------------------------

### Pytest Run Test Setup Hook (pytest_runtest_setup)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

The `pytest_runtest_setup` hook is responsible for executing the setup phase of a test item. The default implementation handles setting up the item and its parent fixtures. This hook allows customization of test setup procedures, ensuring all necessary prerequisites are met before the test call phase.

```python
from _pytest.nodes import Item

def pytest_runtest_setup(item: Item) -> None:
    """Called to perform the setup phase for a test item."""
    pass
```

--------------------------------

### CaptureFixture: Starting and Closing Capture

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Methods to start and close the capture mechanism within the CaptureFixture. `_start` initializes the MultiCapture object and begins capturing, while `close` stops capturing, flushes any remaining output, and resets the capture object.

```python
    def _start(self) -> None:
        if self._capture is None:
            self._capture = MultiCapture(
                in_=None,
                out=self.captureclass(1, **self._config),
                err=self.captureclass(2, **self._config),
            )
            self._capture.start_capturing()
```

```python
    def close(self) -> None:
        if self._capture is not None:
            out, err = self._capture.pop_outerr_to_orig()
            self._captured_out += out
            self._captured_err += err
            self._capture.stop_capturing()
            self._capture = None
```

--------------------------------

### Extract Plugin Names and Versions

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

Processes plugin information to extract and format names and versions of installed plugins. It shortens names starting with 'pytest-' and ensures uniqueness in the returned list.

```python
def _plugin_nameversions(plugininfo) -> list[str]:
    values: list[str] = []
    for plugin, dist in plugininfo:
        # Gets us name and version!
        name = f"{dist.project_name}-{dist.version}"
        # Questionable convenience, but it keeps things short.
        if name.startswith("pytest-"):
            name = name[7:]
        # We decided to print python package names they can have more than one plugin.
        if name not in values:
            values.append(name)
    return values
```

--------------------------------

### Pytest: Indirect Parametrization Example

Source: https://docs.pytest.org/en/stable/example/parametrize

This example illustrates indirect parametrization in pytest, where a fixture receives values before passing them to the test function. The `indirect=True` parameter allows for more expensive setup in the fixture at test run time, rather than collection time.

```python
import pytest


@pytest.fixture
def fixt(request):
    return request.param * 3


@pytest.mark.parametrize("fixt", ["a", "b"], indirect=True)
def test_indirect(fixt):
    assert len(fixt) == 3

```

--------------------------------

### Handle Session Start

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

The entry point for pytest session startup. It initializes session-related attributes and writes a header to the terminal if configured to do so, including platform and Python version information.

```python
@hookimpl(trylast=True)
    def pytest_sessionstart(self, session: Session) -> None:
        self._session = session
        self._session_start = timing.Instant()
        if not self.showheader:
            return
        self.write_sep("=", "test session starts", bold=True)
        verinfo = platform.python_version()
        if not self.no_header:
            msg = f"platform {sys.platform} -- Python {verinfo}"
            pypy_version_info = getattr(sys, "pypy_version_info", None)
            if pypy_version_info:

```

--------------------------------

### Install or Upgrade pytest using pip or easy_install

Source: https://docs.pytest.org/en/stable/announce/release-2.0.1

Instructions for installing or upgrading pytest using either pip or easy_install. This is a standard Python package management task.

```shell
pip install -U pytest
```

```shell
easy_install -U pytest
```

--------------------------------

### Conditionally Skip Doctests with pytest.skip()

Source: https://docs.pytest.org/en/stable/how-to/doctest

Shows how to use `pytest.skip()` within a doctest to conditionally skip a test based on external factors, such as the operating system. This requires Pytest to be installed. The example checks if the platform is Windows and skips the test if it is.

```python
import sys, pytest


>>> if sys.platform.startswith('win'):
...     pytest.skip('this doctest does not work on Windows')
...

>>> import fcntl
>>> ...

```

--------------------------------

### Display Active Plugins with pytest --trace-config

Source: https://docs.pytest.org/en/stable/how-to/plugins

Illustrates the command-line option to display a detailed test header, including all activated plugins and their names, as well as local conftest.py files when they are loaded.

```bash
pytest --trace-config
```

--------------------------------

### Run Pytest with Failing Fixtures and Capture Output

Source: https://docs.pytest.org/en/stable/example/simple

This snippet demonstrates running pytest with the `-s` flag to show print statements, when the test module includes failing fixtures and tests. The output clearly indicates errors during fixture setup and failures during test execution, providing detailed information for debugging.

```bash
$ pytest -s test_module.py
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y
rootdir: /home/sweet/project
collected 3 items

test_module.py Esetting up a test failed test_module.py::test_setup_fails
Fexecuting test failed or skipped test_module.py::test_call_fails
F

================================== ERRORS ==================================
____________________ ERROR at setup of test_setup_fails ____________________

    @pytest.fixture
    def other():
>       assert 0
E       assert 0

test_module.py:7: AssertionError
================================= FAILURES =================================
_____________________________ test_call_fails ______________________________

something = None

    def test_call_fails(something):
>       assert 0
E       assert 0

test_module.py:15: AssertionError
________________________________ test_fail2 ________________________________

    def test_fail2():
>       assert 0
E       assert 0

test_module.py:19: AssertionError
========================= short test summary info ==========================
FAILED test_module.py::test_call_fails - assert 0
FAILED test_module.py::test_fail2 - assert 0
ERROR test_module.py::test_setup_fails - assert 0
======================== 2 failed, 1 error in 0.12s ========================

```

--------------------------------

### Install or Upgrade pytest using pip or easy_install

Source: https://docs.pytest.org/en/stable/announce/release-2.0.3

Instructions for installing or upgrading the pytest package using either pip or easy_install. These commands ensure you have the latest version or a specific version of pytest available in your Python environment.

```bash
pip install -U pytest # or
easy_install -U pytest
```

--------------------------------

### FDCaptureBase Initialization and State Management (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Demonstrates the initialization logic for FDCaptureBase, including setting up file descriptors, temporary files, and capture mechanisms. It also shows the assertion method for state management.

```python
class FDCaptureBase[T]:
    def __init__(self, targetfd: int, patchsysdict: dict[int, object]) -> None:
        self._state = "initialized"
        self.targetfd_invalid: int | None = os.open(os.devnull, os.O_RDWR)
        os.dup2(self.targetfd_invalid, targetfd)
        else:
            self.targetfd_invalid = None
        self.targetfd_save = os.dup(targetfd)

        if targetfd == 0:
            self.tmpfile = open(os.devnull, encoding="utf-8")
            self.syscapture: CaptureBase[str] = SysCapture(targetfd)
        else:
            self.tmpfile = EncodedFile(
                TemporaryFile(buffering=0),
                encoding="utf-8",
                errors="replace",
                newline="",
                write_through=True,
            )
            if targetfd in patchsysdict:
                self.syscapture = SysCapture(targetfd, self.tmpfile)
            else:
                self.syscapture = NoCapture(targetfd)

        self._state = "initialized"

    def __repr__(self) -> str:
        return (
            f"<{self.__class__.__name__} {self.targetfd} oldfd={self.targetfd_save} "
            f"_state={self._state!r} tmpfile={self.tmpfile!r}>"
        )

    def _assert_state(self, op: str, states: tuple[str, ...]) -> None:
        assert self._state in states, (
            "cannot {} in state {!r}: expected one of {}".format(
                op, self._state, ", ".join(states)
            )
        )
```

--------------------------------

### pytest_fixture_setup

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

Hook for performing fixture setup execution. It stops at the first non-None result.

```APIDOC
## pytest_fixture_setup

### Description
Perform fixture setup execution. Stops at first non-None result.

### Method
HOOK

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "fixturedef": "FixtureDef object",
  "request": "SubRequest object"
}
```

### Response
#### Success Response (200)
- **object | None**: The return value of the call to the fixture function.

#### Response Example
```json
{
  "returnValue": "object or null"
}
```

### Notes
If the fixture function returns None, other implementations of this hook function will continue to be called, according to the behavior of the :ref:`firstresult` option.

Use in conftest plugins
=======================

Any conftest file can implement this hook. For a given fixture, only conftest files in the fixture scope's directory and its parent directories are consulted.
```

--------------------------------

### Perform Pytest Fixture Setup

Source: https://docs.pytest.org/en/stable/reference/reference

The `pytest_fixture_setup` hook is executed during the setup phase of a fixture. It allows plugins to hook into the fixture setup process, receiving the fixture definition and request objects. The return value can influence the fixture's result.

```python
def pytest_fixture_setup(fixturedef, request):
    """Perform fixture setup execution."""
    # Custom fixture setup logic
    return None  # Or the result of the fixture function
```

--------------------------------

### Pytest Function Setup Procedure

Source: https://docs.pytest.org/en/stable/_modules/_pytest/python

Performs the setup steps required before executing a test function. This primarily involves filling in the necessary fixtures for the request object.

```python
def setup(self) -> None:
    self._request._fillxtures()
```

--------------------------------

### Pytest Cleanup Command Examples

Source: https://docs.pytest.org/en/stable/changelog

Provides examples of using the `py.cleanup` command for removing temporary files and directories. It shows options for specifying file extensions to remove, cleaning build/dist directories, removing empty directories, and performing a dry run.

```bash
py.cleanup     # remove "*.pyc" and "*$py.class" (jython) files
py.cleanup -e .swp -e .cache # also remove files with these extensions
py.cleanup -s  # remove "build" and "dist" directory next to setup.py files
py.cleanup -d  # also remove empty directories
py.cleanup -a  # synonym for "-s -d -e 'pip-log.txt'"
py.cleanup -n  # dry run, only show what would be removed
```

--------------------------------

### Correct Pytest Approx Usage Example

Source: https://docs.pytest.org/en/stable/changelog

Demonstrates the correct way to use pytest.approx() for assertions. Incorrect usage, like asserting pytest.approx(actual, expected), will now raise an error, guiding users to the proper syntax: assert actual == pytest.approx(expected).

```python
assert actual == pytest.approx(expected)
```

--------------------------------

### Pytest Docstring Example (Sphinx Format)

Source: https://docs.pytest.org/en/stable/contributing

An example of a Python function docstring formatted according to the Sphinx style, commonly used by Pytest. It demonstrates how to include parameter descriptions, return values, raised exceptions, and version information.

```python
def my_function(arg: ArgType) -> Foo:
    """Do important stuff.

    More detailed info here, in separate paragraphs from the subject line.
    Use proper sentences -- start sentences with capital letters and end
    with periods.

    Can include annotated documentation:

    :param short_arg: An argument which determines stuff.
    :param long_arg:
        A long explanation which spans multiple lines, overflows
        like this.
    :returns: The result.
    :raises ValueError:
        Detailed information when this can happen.

    .. versionadded:: 6.0

    Including types into the annotations above is not necessary when
    type-hinting is being used (as in this example).
    """


```

--------------------------------

### Disable Plugin Autoloading (Environment Variable)

Source: https://docs.pytest.org/en/stable/how-to/plugins

Disables plugin autoloading by setting the PYTEST_DISABLE_PLUGIN_AUTOLOAD environment variable to 1. This is useful for CI environments or specific setups where automatic plugin loading is not desired.

```bash
export PYTEST_DISABLE_PLUGIN_AUTOLOAD=1
export PYTEST_PLUGINS=NAME,NAME2
pytest
```

--------------------------------

### Run Pytest and Capture Failures

Source: https://docs.pytest.org/en/stable/example/simple

This snippet shows how to run pytest tests and capture the output, including identifying failing tests. It demonstrates a basic test file with failing assertions and the command to execute pytest. The output highlights the failures and provides a summary.

```bash
$ pytest test_module.py
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y
rootdir: /home/sweet/project
collected 2 items

test_module.py FF                                                    [100%]

================================= FAILURES =================================
________________________________ test_fail1 ________________________________

tmp_path = PosixPath('PYTEST_TMPDIR/test_fail10')

    def test_fail1(tmp_path):
>       assert 0
E       assert 0

test_module.py:2: AssertionError
________________________________ test_fail2 ________________________________

    def test_fail2():
>       assert 0
E       assert 0

test_module.py:6: AssertionError
========================= short test summary info ==========================
FAILED test_module.py::test_fail1 - assert 0
FAILED test_module.py::test_fail2 - assert 0
============================ 2 failed in 0.12s =============================

```

```bash
$ cat failures
test_module.py::test_fail1 (PYTEST_TMPDIR/test_fail10)
test_module.py::test_fail2

```

--------------------------------

### Create Generic Files with pytester.makefile

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `makefile` method creates files with specified extensions and content. Arguments are treated as strings and joined by newlines for the file content. Keyword arguments define filenames and their content. It returns the first created file.

```python
pytester.makefile(".txt", "line1", "line2")
pytester.makefile(".ini", pytest="[pytest]\naddopts=-rs\n")
```

--------------------------------

### Install pytest using pip

Source: https://docs.pytest.org/en/stable/announce/release-2.4.1

This command installs or upgrades the pytest package to the latest version using pip, the Python package installer. It ensures you have the most recent features and bug fixes.

```bash
pip install -U pytest

```

--------------------------------

### Pytest Test Execution Summary Example

Source: https://docs.pytest.org/en/stable/example/simple

Shows a typical Pytest test session output, including the platform, Pytest version, collected test items, and the status of each test file (F for failed, E for error, . for passed, x for xfailed). It highlights the summary of errors and failures.

```bash
$ pytest
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y
rootdir: /home/sweet/project
collected 7 items

a/test_db.py F                                                       [ 14%]
a/test_db2.py F                                                      [ 28%]
b/test_error.py E                                                    [ 42%]
test_step.py .Fx.                                                    [100%]

================================== ERRORS ==================================
_______________________ ERROR at setup of test_root ________________________
file /home/sweet/project/b/test_error.py, line 1
  def test_root(db):  # no db here, will error out
E       fixture 'db' not found
>       available fixtures: cache, capfd, capfdbinary, caplog, capsys, capsysbinary, capteesys, doctest_namespace, monkeypatch, pytestconfig, record_property, record_testsuite_property, record_xml_attribute, recwarn, subtests, tmp_path, tmp_path_factory, tmpdir, tmpdir_factory
>       use 'pytest --fixtures [testpath]' for help on them.

/home/sweet/project/b/test_error.py:1
================================= FAILURES =================================
_________________________________ test_a1 __________________________________

db = <conftest.DB object at 0xdeadbeef0002>

    def test_a1(db):
>       assert 0, db  # to show value
        ^^^^^^^^^^^^
E       AssertionError: <conftest.DB object at 0xdeadbeef0002>
E       assert 0

a/test_db.py:2: AssertionError
_________________________________ test_a2 __________________________________

db = <conftest.DB object at 0xdeadbeef0002>

    def test_a2(db):
>       assert 0, db  # to show value
        ^^^^^^^^^^^^
E       AssertionError: <conftest.DB object at 0xdeadbeef0002>
E       assert 0

a/test_db2.py:2: AssertionError
____________________ TestUserHandling.test_modification ____________________

self = <test_step.TestUserHandling object at 0xdeadbeef0003>

    def test_modification(self):
>       assert 0
E       assert 0

test_step.py:11: AssertionError
========================= short test summary info ==========================
FAILED a/test_db.py::test_a1 - AssertionError: <conftest.DB object at 0x7...
FAILED a/test_db2.py::test_a2 - AssertionError: <conftest.DB object at 0x...
FAILED test_step.py::TestUserHandling::test_modification - assert 0
ERROR b/test_error.py::test_root
============= 3 failed, 2 passed, 1 xfailed, 1 error in 0.12s ==============

```

--------------------------------

### Update Test Case Duration

Source: https://docs.pytest.org/en/stable/_modules/_pytest/junitxml

Updates the total duration for a test case based on the report's 'when' attribute (setup, call, or teardown). It uses the node_reporter to get the reporter object and accumulates the duration.

```python
def update_testcase_duration(self, report: TestReport) -> None:
        """Accumulate total duration for nodeid from given report and update
        the Junit.testcase with the new total if already created."""
        if self.report_duration in {"total", report.when}:
            reporter = self.node_reporter(report)
```

--------------------------------

### Pytest: Deferring Resource Setup with Indirect Parametrization

Source: https://docs.pytest.org/en/stable/example/parametrize

This snippet demonstrates how to defer the setup of database resources in pytest. It uses `pytest_generate_tests` to parametrize a test function and an indirect fixture to create database objects only when the test runs. This is useful for expensive resource initialization.

```python
# content of test_backends.py

import pytest


def test_db_initialized(db):
    # a dummy test
    if db.__class__.__name__ == "DB2":
        pytest.fail("deliberately failing for demo purposes")

```

```python
# content of conftest.py
import pytest


def pytest_generate_tests(metafunc):
    if "db" in metafunc.fixturenames:
        metafunc.parametrize("db", ["d1", "d2"], indirect=True)


class DB1:
    "one database object"


class DB2:
    "alternative database object"


@pytest.fixture
def db(request):
    if request.param == "d1":
        return DB1()
    elif request.param == "d2":
        return DB2()
    else:
        raise ValueError("invalid internal test config")

```

--------------------------------

### Pytest Fixture Discovery with Third-Party Plugins

Source: https://docs.pytest.org/en/stable/reference/fixtures

Illustrates how pytest finds fixtures provided by installed third-party plugins. Pytest searches for fixtures in local scopes first, then in plugins as a last resort. This example shows a test file requesting fixtures ('a_fix', 'b_fix') that are assumed to be provided by external plugins.

```python
tests/conftest.py
import pytest

@pytest.fixture
def order():
    return []

tests/subpackage/conftest.py
import pytest

@pytest.fixture(autouse=True)
def mid(order, b_fix):
    order.append("mid subpackage")

tests/subpackage/test_subpackage.py
import pytest

@pytest.fixture
def inner(order, mid, a_fix):
    order.append("inner subpackage")

def test_order(order, inner):
    assert order == ["b_fix", "mid subpackage", "a_fix", "inner subpackage"]
```

--------------------------------

### Create Artificial Slow Tests for Profiling

Source: https://docs.pytest.org/en/stable/example/simple

This Python code defines a simple test file with three test functions that simulate different execution times using `time.sleep`. This setup is used to demonstrate pytest's `--durations` option for profiling.

```python
# content of test_some_are_slow.py
import time


def test_funcfast():
    time.sleep(0.1)


def test_funcslow1():
    time.sleep(0.2)


def test_funcslow2():
    time.sleep(0.3)
```

--------------------------------

### FDCaptureBase Start, Done, Suspend, Resume Methods (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Details the core lifecycle methods of FDCaptureBase: start capturing, stop capturing and restore streams, suspend capture, and resume capture. These methods manage the state transitions and file descriptor manipulations.

```python
    def start(self) -> None:
        """Start capturing on targetfd using memorized tmpfile."""
        self._assert_state("start", ("initialized",))
        os.dup2(self.tmpfile.fileno(), self.targetfd)
        self.syscapture.start()
        self._state = "started"

    def done(self) -> None:
        """Stop capturing, restore streams, return original capture file,
        seeked to position zero."""
        self._assert_state("done", ("initialized", "started", "suspended", "done"))
        if self._state == "done":
            return
        os.dup2(self.targetfd_save, self.targetfd)
        os.close(self.targetfd_save)
        if self.targetfd_invalid is not None:
            if self.targetfd_invalid != self.targetfd:
                os.close(self.targetfd)
            os.close(self.targetfd_invalid)
        self.syscapture.done()
        self.tmpfile.close()
        self._state = "done"

    def suspend(self) -> None:
        self._assert_state("suspend", ("started", "suspended"))
        if self._state == "suspended":
            return
        self.syscapture.suspend()
        os.dup2(self.targetfd_save, self.targetfd)
        self._state = "suspended"

    def resume(self) -> None:
        self._assert_state("resume", ("started", "suspended"))
        if self._state == "started":
            return
        self.syscapture.resume()
        os.dup2(self.tmpfile.fileno(), self.targetfd)
        self._state = "started"
```

--------------------------------

### Control Test Execution Protocol with pytest_runtest_protocol

Source: https://docs.pytest.org/en/stable/_modules/_pytest/runner

Implements the pytest_runtest_protocol hook to manage the execution flow of individual tests. It logs the start and end of test execution and calls the core runtestprotocol function to handle setup, call, and teardown phases for a test item.

```python
import pytest
from _pytest.main import Item, call_and_report, runtestprotocol

def pytest_runtest_protocol(item: Item, nextitem: Item | None) -> bool:
    ihook = item.ihook
    ihook.pytest_runtest_logstart(nodeid=item.nodeid, location=item.location)
    runtestprotocol(item, nextitem=nextitem)
    ihook.pytest_runtest_logfinish(nodeid=item.nodeid, location=item.location)
    return True
```

--------------------------------

### SetupState for Test Item Lifecycle Management

Source: https://docs.pytest.org/en/stable/_modules/_pytest/runner

The SetupState class manages the setup and teardown phases for test items and collectors within a pytest session. It uses a stack to track the current hierarchy of collectors and ensures that setup and teardown operations are performed in the correct order.

```python
class SetupState:
    """Shared state for setting up/tearing down test items or collectors
    in a session.

    Suppose we have a collection tree as follows:

    <Session session>
        <Module mod1>
            <Function item1>
        <Module mod2>
            <Function item2>

    The SetupState maintains a stack. The stack starts out empty:

        []

    During the setup phase of item1, setup(item1) is called. What it does
    is:

        push session to stack, run session.setup()
        push mod1 to stack, run mod1.setup()
        push item1 to stack, run item1.setup()

    The stack is:

        [session, mod1, item1]

    While the stack is in this shape, it is allowed to add finalizers to
    each of session, mod1, item1 using addfinalizer().

    During the teardown phase of item1, teardown_exact(item2) is called,
    where item2 is the next item to item1. What it does is:

        pop item1 from stack, run its teardowns
        pop mod1 from stack, run its teardowns

    mod1 was popped because it ended its purpose with item1. The stack is:

        [session]

    During the setup phase of item2, setup(item2) is called. What it does
    is:

        push mod2 to stack, run mod2.setup()
        push item2 to stack, run item2.setup()

    Stack:

        [session, mod2, item2]

    During the teardown phase of item2, teardown_exact(None) is called,
    because item2 is the last item. What it does is:

        pop item2 from stack, run its teardowns
        pop mod2 from stack, run its teardowns
        pop session from stack, run its teardowns

    Stack:

        []

    The end!
    """

    def __init__(self) -> None:
        # The stack is in the dict insertion order.
        self.stack: dict[
            Node,
            tuple[
                # Node's finalizers.
                list[Callable[[], object]],
                # Node's exception and original traceback, if its setup raised.
                tuple[OutcomeException | Exception, types.TracebackType | None] | None,
            ],
        ] = {}

    def setup(self, item: Item) -> None:
        """Setup objects along the collector chain to the item."""
        needed_collectors = item.listchain()

        # If a collector fails its setup, fail its entire subtree of items.
        # The setup is not retried for each item - the same exception is used.
        for col, (finalizers, exc) in self.stack.items():
            assert col in needed_collectors, "previous item was not torn down properly"
            if exc:
                raise exc[0].with_traceback(exc[1])

        for col in needed_collectors[len(self.stack) :]:
            assert col not in self.stack

```

--------------------------------

### Define Hello Fixture and Option for Plugin Testing

Source: https://docs.pytest.org/en/stable/how-to/writing_plugins

Defines a custom pytest fixture 'hello' and adds a command-line option '--name' to configure its behavior. This setup is used for testing plugin functionality with 'pytester'.

```python
import pytest


def pytest_addoption(parser):
    group = parser.getgroup("helloworld")
    group.addoption(
        "--name",
        action="store",
        dest="name",
        default="World",
        help='Default "name" for hello().'
    )


@pytest.fixture
def hello(request):
    name = request.config.getoption("name")

    def _hello(name=None):
        if not name:
            name = request.config.getoption("name")
        return f"Hello {name}!"

    return _hello
```

--------------------------------

### Pytest Package Collector Setup with Xunit Methods

Source: https://docs.pytest.org/en/stable/_modules/_pytest/python

Handles the setup for a Python package collector, specifically invoking `setUpModule` or `setup_module` and registering `tearDownModule` or `teardown_module` as a finalizer. This method is used because autouse fixtures from packages are not automatically called.

```python
init_mod = importtestmodule(self.path / "__init__.py", self.config)

# Not using fixtures to call setup_module here because autouse fixtures
# from packages are not called automatically (#4085).
setup_module = _get_first_non_fixture_func(
    init_mod, ("setUpModule", "setup_module")
)
if setup_module is not None:
    _call_with_optional_argument(setup_module, init_mod)

teardown_module = _get_first_non_fixture_func(
    init_mod, ("tearDownModule", "teardown_module")
)
if teardown_module is not None:
    func = partial(_call_with_optional_argument, teardown_module, init_mod)
    self.addfinalizer(func)
```

--------------------------------

### Pytest Class Method Setup/Teardown

Source: https://docs.pytest.org/en/stable/how-to/xunit_setup

These methods are invoked around each test method invocation within a class. `setup_method` prepares state, and `teardown_method` cleans it up. The `method` parameter is optional since Pytest 3.0.

```python
def setup_method(self, method):
    """setup any state tied to the execution of the given method in a
    class.  setup_method is invoked for every test method of a class.
    """


def teardown_method(self, method):
    """teardown any state that was previously setup with a setup_method
    call.
    """

```

--------------------------------

### Pytest Fixture: Basic Setup and Test

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Demonstrates a simple pytest fixture 'order' that depends on 'first_entry' and a test function 'test_string' that modifies and asserts the fixture's state. This illustrates basic fixture definition and usage.

```python
# contents of test_append.py
import pytest


# Arrange
@pytest.fixture
def first_entry():
    return "a"


# Arrange
@pytest.fixture
def order(first_entry):
    return [first_entry]


def test_string(order):
    # Act
    order.append("b")

    # Assert
    assert order == ["a", "b"]

```

--------------------------------

### Create conftest.py with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Creates a conftest.py file with the provided source code in the test directory. The path to the created file is returned as a legacy_path object.

```python
def makeconftest(self, source) -> LEGACY_PATH:
    """See :meth:`Pytester.makeconftest`."""
    return legacy_path(self._pytester.makeconftest(source))
```

--------------------------------

### Pytest Documentation Example for Abstract Test Classes

Source: https://docs.pytest.org/en/stable/changelog

Provides an example demonstrating how to handle abstract test classes in Pytest documentation using a mixin class. This approach ensures that subclasses of abstract test classes are automatically collected by Pytest without manual intervention.

```python
# Example demonstrating handling of abstract test classes using a mixin
# (Specific code for the mixin and abstract class not provided in the source text,
# but the concept is described.)

# Assume an abstract base class and a mixin are defined elsewhere.
# Subclasses inheriting from the abstract class (potentially via the mixin)
# will be automatically discovered by pytest.

```

--------------------------------

### Get Fixture Value (Pytest)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

Retrieves the cached value of a fixture by its argument name. This method is called by Pytest during item and fixture setup to evaluate statically requested fixtures. It asserts that the fixture value is available and returns it. It raises an error if the fixture has already been torn down.

```python
def getfixturevalue(self, argname: str) -> object:
        """Return the value of the fixture named argname."""
        # getfixturevalue() is also called by pytest itself during item and fixture
        # setup to evaluate the fixtures that are requested statically
        # (using function parameters, autouse, etc).

        fixturedef = self._get_active_fixturedef(argname)
        assert fixturedef.cached_result is not None, (
            f'The fixture value for "{argname}" is not available.  '
            "This can happen when the fixture has already been torn down."
        )
        return fixturedef.cached_result[0]
```

--------------------------------

### Pytest Configuration in setup.cfg

Source: https://docs.pytest.org/en/stable/reference/customize

Example of configuring pytest within a setup.cfg file using the [tool:pytest] section. This allows specifying minimum version, additional options, and test paths. Usage is not recommended for complex cases.

```ini
# setup.cfg
[tool:pytest]
minversion = 6.0
addopts = -ra -q
testpaths =
    tests
    integration
```

--------------------------------

### Run Pytest as Subprocess

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Launches pytest as a subprocess with specified arguments. It handles plugin loading and temporary directory setup. Accepts arguments and an optional timeout, returning a RunResult.

```python
def runpytest_subprocess(
    self, *args: str | os.PathLike[str], timeout: float | None = None
) -> RunResult:
    """Run pytest as a subprocess with given arguments.

    Any plugins added to the :py:attr:`plugins` list will be added using the
    ``-p`` command line option.  Additionally ``--basetemp`` is used to put
    any temporary files and directories in a numbered directory prefixed
    with "runpytest-" to not conflict with the normal numbered pytest
    location for temporary files and directories.

    :param args:
        The sequence of arguments to pass to the pytest subprocess.
    :param timeout:
        The period in seconds after which to timeout and raise
        :py:class:`Pytester.TimeoutExpired`.
    :returns:
        The result.
    """
    __tracebackhide__ = True
    p = make_numbered_dir(root=self.path, prefix="runpytest-", mode=0o700)
    args = (f"--basetemp={p}", *args)
    for plugin in self.plugins:
        if not isinstance(plugin, str):
            raise ValueError(
                f"Specifying plugins as objects is not supported in pytester subprocess mode; "
                f"specify by name instead: {plugin}"
            )
        args = ("-p", plugin, *args)
    args = self._getpytestargs() + args
    return self.run(*args, timeout=timeout)
```

--------------------------------

### Pytest Hooks for Fixture Lifecycle Management

Source: https://docs.pytest.org/en/stable/changelog

These hooks provide extension points for managing the setup and teardown of fixtures. `pytest_fixture_setup` is called during fixture setup, while `pytest_fixture_post_finalizer` is called after a fixture's finalizer has run, providing access to the fixture's result cache.

```python
def pytest_fixture_setup(fixturedef, request):
    # ... implementation ...
    pass

def pytest_fixture_post_finalizer(fixturedef):
    # ... implementation ...
    pass
```

--------------------------------

### Install LegacyTmpdirPlugin if tmpdir Plugin Exists (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

This hook implementation installs the LegacyTmpdirPlugin when the 'tmpdir' plugin is already present. It ensures that plugins relying on the older tmpdir handler can still function by attaching a TempdirFactory instance to the config object.

```python
@hookimpl
def pytest_configure(config: Config) -> None:
    """Installs the LegacyTmpdirPlugin if the ``tmpdir`` plugin is also installed."""
    if config.pluginmanager.has_plugin("tmpdir"):
        mp = MonkeyPatch()
        config.add_cleanup(mp.undo)
        try:
            tmp_path_factory = config._tmp_path_factory  # type: ignore[attr-defined]
        except AttributeError:
            pass
        else:
            _tmpdirhandler = TempdirFactory(tmp_path_factory, _ispytest=True)
            mp.setattr(config, "_tmpdirhandler", _tmpdirhandler, raising=False)

        config.pluginmanager.register(LegacyTmpdirPlugin, "legacypath-tmpdir")
```

--------------------------------

### Pytest Fixture Setup Hook

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

The `pytest_fixture_setup` hook is called during fixture setup execution. It allows plugins to intercept and potentially modify the fixture's setup process. The hook stops at the first non-None result, as per the 'firstresult' behavior. If a fixture function returns None, other implementations of this hook will continue to be called.

```python
from typing import Any

from _pytest.fixtures import FixtureDef, SubRequest


@hookspec(firstresult=True)
def pytest_fixture_setup(
    fixturedef: FixtureDef[Any], request: SubRequest
) -> object | None:
    """Perform fixture setup execution.

    :param fixturedef:
        The fixture definition object.
    :param request:
        The fixture request object.
    :returns:
        The return value of the call to the fixture function.

    Stops at first non-None result, see :ref:`firstresult`.

    .. note::
        If the fixture function returns None, other implementations of
        this hook function will continue to be called, according to the
        behavior of the :ref:`firstresult` option.

    Use in conftest plugins
    =======================

    Any conftest file can implement this hook. For a given fixture, only
    conftest files in the fixture scope's directory and its parent directories
    are consulted.
    """
    pass
```

--------------------------------

### Listing Setuptools-Registered Plugins and Distribution Info in PytestPluginManager

Source: https://docs.pytest.org/en/stable/reference/reference

Returns a list of tuples, pairing setuptools-registered plugins with their distribution information (distinfo). This helps in identifying plugins installed via setuptools.

```python
def list_plugin_distinfo(self):
    """Return a list of (plugin, distinfo) pairs for all setuptools-registered plugins."""
    # Implementation details...
```

--------------------------------

### Pytest Fixture for Test Result Reporting

Source: https://docs.pytest.org/en/stable/example/simple

This Python code demonstrates a pytest plugin that makes test result information available within fixture finalizers. It uses `pytest_runtest_makereport` to store report data in the item's stash and a fixture to access this data, allowing for custom reporting logic based on test phase outcomes (setup, call, teardown).

```python
from typing import Dict
import pytest
from pytest import StashKey, CollectReport

phase_report_key = StashKey[Dict[str, CollectReport]]()


@pytest.hookimpl(wrapper=True, tryfirst=True)
def pytest_runtest_makereport(item, call):
    # execute all other hooks to obtain the report object
    rep = yield

    # store test results for each phase of a call, which can
    # be "setup", "call", "teardown"
    item.stash.setdefault(phase_report_key, {})[rep.when] = rep

    return rep


@pytest.fixture
def something(request):
    yield
    # request.node is an "item" because we use the default
    # "function" scope
    report = request.node.stash[phase_report_key]
    if report["setup"].failed:
        print("setting up a test failed", request.node.nodeid)
    elif report["setup"].skipped:
        print("setting up a test skipped", request.node.nodeid)
    elif ("call" not in report) or report["call"].failed:
        print("executing test failed or skipped", request.node.nodeid)

```

--------------------------------

### Initialize Session Start Time

Source: https://docs.pytest.org/en/stable/_modules/_pytest/junitxml

Records the start time of the Pytest test session. This is used later to calculate the total duration of the test run.

```python
def pytest_sessionstart(self) -> None:
    self.suite_start = timing.Instant()
```

--------------------------------

### Skip Doctests if All Examples are Skipped

Source: https://docs.pytest.org/en/stable/_modules/_pytest/doctest

This utility function checks if all examples within a `doctest.DocTest` object have the `SKIP` option set. If all examples are marked to be skipped, it raises a `pytest.skip()` exception, effectively skipping the entire doctest.

```python
def _check_all_skipped(test: doctest.DocTest) -> None:
    """Raise pytest.skip() if all examples in the given DocTest have the SKIP
    option set."""
    import doctest

    all_skipped = all(x.options.get(doctest.SKIP, False) for x in test.examples)
    if all_skipped:
        skip("all tests skipped by +SKIP option")
```

--------------------------------

### Early load plugins with pytest

Source: https://docs.pytest.org/en/stable/how-to/usage

This command demonstrates how to explicitly load plugins, both internal and external, using the '-p' option. It shows examples for loading a custom plugin module and a registered entry-point plugin like pytest-cov.

```bash
pytest -p mypluginmodule
```

```bash
pytest -p pytest_cov
```

--------------------------------

### Pytest Session Start and Collection Hooks

Source: https://docs.pytest.org/en/stable/_modules/_pytest/logging

Implements pytest hooks for session start and collection phases. It configures and wraps logging handlers to capture logs during these phases, yielding control back to Pytest.

```python
    @hookimpl(wrapper=True, tryfirst=True)
    def pytest_sessionstart(self) -> Generator[None]:
        self.log_cli_handler.set_when("sessionstart")

        with catching_logs(self.log_cli_handler, level=self.log_cli_level):
            with catching_logs(self.log_file_handler, level=self.log_file_level):
                return (yield)

    @hookimpl(wrapper=True, tryfirst=True)
    def pytest_collection(self) -> Generator[None]:
        self.log_cli_handler.set_when("collection")

        with catching_logs(self.log_cli_handler, level=self.log_cli_level):
            with catching_logs(self.log_file_handler, level=self.log_file_level):
                return (yield)
```

--------------------------------

### Pytest Command-Line Options for Test Execution (Shell)

Source: https://docs.pytest.org/en/stable/how-to/cache

These shell commands demonstrate how to run pytest with different options to control test execution based on previous failures. The examples show running all tests, running only the last failed tests (--lf), running failed tests first (--ff), and running new tests first (--nf). They illustrate how pytest reports failures and manages test runs.

```shell
$ pytest -q

```

```shell
$ pytest --lf

```

```shell
$ pytest --ff

```

--------------------------------

### Create Binary Files Directly

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

For binary files, `makefile` is not used. Instead, use `pathlib.Path.write_bytes` directly on a path object obtained from `pytester.path`.

```python
filename = pytester.path.joinpath("foo.bin")
filename.write_bytes(b"...")
```

--------------------------------

### Node Constructor and Initialization

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

Details the initialization process for a Pytest Node, including its name, parent, configuration, session, file path, and node ID.

```APIDOC
## __init__ Node Constructor

### Description
Initializes a Pytest Node object with essential attributes like name, parent, configuration, session, file path, and node ID. It enforces type checking for required parameters and sets up internal structures like keywords and stash.

### Method
`__init__`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **name** (str) - Required - A unique name within the scope of the parent node.
- **parent** (Node | None) - Optional - The parent collector node.
- **config** (Config | None) - Optional - The pytest config object.
- **session** (Session | None) - Optional - The pytest session this node is part of.
- **fspath** (LEGACY_PATH | None) - Optional - Filesystem path (legacy).
- **path** (Path | None) - Optional - Filesystem path.
- **nodeid** (str | None) - Optional - A unique identifier for the node.

### Request Example
```json
{
  "name": "test_example",
  "parent": null, 
  "config": {},
  "session": {},
  "fspath": null,
  "path": null,
  "nodeid": "test_example"
}
```

### Response
#### Success Response (200)
None (This is a constructor, it does not return a value directly but initializes the object.)

#### Response Example
None
```

--------------------------------

### Nose @with_setup to Pytest Fixture (Python)

Source: https://docs.pytest.org/en/stable/deprecations

Demonstrates migrating from the deprecated `@with_setup` decorator (from `nose.tools`) to a Pytest fixture. This involves defining setup and teardown functions and using `yield` within the fixture to manage resources.

```Python
from nose.tools import with_setup

def setup_some_resource(): ...

def teardown_some_resource(): ...

@with_setup(setup_some_resource, teardown_some_resource)
def test_foo(): ...

```

```Python
import pytest

def setup_some_resource(): ...

def teardown_some_resource(): ...

@pytest.fixture
def some_resource():
    setup_some_resource()
    yield
    teardown_some_resource()

def test_foo(some_resource): ...

```

--------------------------------

### Install Project in Development Mode with pip

Source: https://docs.pytest.org/en/stable/how-to/existingtestsuite

This command installs the current project in development mode using pip. This creates a symlink to your code in site-packages, allowing you to edit your code and have tests run against it without reinstallation. It's a common practice for contributing to existing repositories.

```bash
cd <repository>
pip install -e .  # Environment dependent alternatives include
                  # 'python setup.py develop' and 'conda develop'
```

--------------------------------

### Pytest Class Instance Isolation for Tests

Source: https://docs.pytest.org/en/stable/getting-started

Illustrates a potential pitfall when grouping tests in classes: each test gets a unique instance of the class. This example shows a class 'TestClassDemoInstance' where 'test_one' modifies a class attribute 'value', but 'test_two' fails because it receives a fresh instance where 'value' is still at its initial state, not the modified state from 'test_one'. This highlights the importance of test isolation.

```python
class TestClassDemoInstance:
    value = 0

    def test_one(self):
        self.value = 1
        assert self.value == 1

    def test_two(self):
        assert self.value == 1
```

--------------------------------

### Pytest Features and Usage

Source: https://docs.pytest.org/en/stable/contents

This section covers core pytest features such as integrating with unittest.TestCase, using fixtures, and implementing xUnit-style setup and teardown methods.

```APIDOC
## Pytest Features and Usage

### Description
This section details how to leverage pytest's features within standard Python testing structures, including mixing pytest fixtures into `unittest.TestCase` subclasses and implementing various levels of setup and teardown.

### Key Topics

*   **`unittest.TestCase` Integration**: Learn how to use pytest features like fixtures within `unittest.TestCase` subclasses, including the use of marks for mixing fixtures.
*   **Fixtures**: Understand how to use autouse fixtures and access other fixtures effectively.
*   **xUnit-style Setup/Teardown**: Implement module, class, and method/function level setup and teardown procedures.
*   **Bash Completion**: Instructions on setting up bash completion for pytest.
```

--------------------------------

### Initialize Pytester with Temporary Directory and Monkeypatch

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Initializes the Pytester instance, setting up a temporary directory for tests and configuring environment variables using monkeypatch. It ensures isolation by managing sys.path and sys.modules snapshots.

```python
def __init__(
        self,
        request: FixtureRequest,
        tmp_path_factory: TempPathFactory,
        monkeypatch: MonkeyPatch,
        *,
        _ispytest: bool = False,
    ) -> None:
        check_ispytest(_ispytest)
        self._request = request
        self._mod_collections: WeakKeyDictionary[Collector, list[Item | Collector]] = (
            WeakKeyDictionary()
        )
        if request.function:
            name: str = request.function.__name__
        else:
            name = request.node.name
        self._name = name
        self._path: Path = tmp_path_factory.mktemp(name, numbered=True)
        #: A list of plugins to use with :py:meth:`parseconfig` and
        #: :py:meth:`runpytest`. Initially this is an empty list but plugins can
        #: be added to the list.
        #: 
        #: When running in subprocess mode, specify plugins by name (str) - adding
        #: plugin objects directly is not supported.
        self.plugins: list[str | _PluggyPlugin] = []
        self._sys_path_snapshot = SysPathsSnapshot()
        self._sys_modules_snapshot = self.__take_sys_modules_snapshot()
        self._request.addfinalizer(self._finalize)
        self._method = self._request.config.getoption("--runpytest")
        self._test_tmproot = tmp_path_factory.mktemp(f"tmp-{name}", numbered=True)

        self._monkeypatch = mp = monkeypatch
        self.chdir()
        mp.setenv("PYTEST_DEBUG_TEMPROOT", str(self._test_tmproot))
        # Ensure no unexpected caching via tox.
        mp.delenv("TOX_ENV_DIR", raising=False)
        # Discard outer pytest options.
        mp.delenv("PYTEST_ADDOPTS", raising=False)
        # Ensure no user config is used.
        tmphome = str(self.path)
        mp.setenv("HOME", tmphome)
        mp.setenv("USERPROFILE", tmphome)
        # Do not use colors for inner runs by default.
        mp.setenv("PY_COLORS", "0")
```

--------------------------------

### Install Assertion Rewriting Hook in Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Installs the PEP 302 import hook for assertion rewriting if the '--assert=rewrite' option is enabled. It determines the assertion mode from command-line arguments or environment variables and attempts to install the hook. If successful, it marks relevant plugins for rewriting; otherwise, it falls back to plain assertion mode.

```python
def _consider_importhook(self) -> None:
    """Install the PEP 302 import hook if using assertion rewriting.

    Needs to parse the --assert=<mode> option from the commandline
    and find all the installed plugins to mark them for rewriting
    by the importhook.
    """
    mode = getattr(self.known_args_namespace, "assertmode", "plain")

    disable_autoload = getattr(
        self.known_args_namespace, "disable_plugin_autoload", False
    ) or bool(os.environ.get("PYTEST_DISABLE_PLUGIN_AUTOLOAD"))
    if mode == "rewrite":
        import _pytest.assertion

        try:
            hook = _pytest.assertion.install_importhook(self)
        except SystemError:
            mode = "plain"
        else:
            self._mark_plugins_for_rewrite(hook, disable_autoload)
    self._warn_about_missing_assertion(mode)
```

--------------------------------

### Create pyproject.toml with pytester.makepyprojecttoml

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `makepyprojecttoml` method creates a `pyproject.toml` file. It takes the file content as a string and returns the `Path` object for the created file.

```python
def makepyprojecttoml(self, source: str) -> Path:
    """Write a pyproject.toml file.

    :param source: The contents.
    :returns: The pyproject.ini file.

    .. versionadded:: 6.0
    """
    return self.makefile(".toml", pyproject=source)
```

--------------------------------

### Pytest Fixture Modularity with Fixture Dependencies

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Illustrates how fixture functions can depend on other fixtures, promoting modularity and reusability. This example shows an `app` fixture that utilizes an `smtp_connection` fixture to instantiate an `App` object.

```python
import pytest


class App:
    def __init__(self, smtp_connection):
        self.smtp_connection = smtp_connection


@pytest.fixture(scope="module")
def app(smtp_connection):
    return App(smtp_connection)

def test_smtp_connection_exists(app):
    assert app.smtp_connection
```

--------------------------------

### Create a Basic Pytest Test File

Source: https://docs.pytest.org/en/stable/getting-started

A simple Python file demonstrating a function and a test case using the assert statement. This example shows how pytest discovers and runs tests, and reports failures.

```python
# content of test_sample.py
def func(x):
    return x + 1

def test_answer():
    assert func(3) == 5
```

--------------------------------

### Configure pytest command-line options with PYTEST_ADDOPTS environment variable

Source: https://docs.pytest.org/en/stable/example/simple

This snippet shows how to set default command-line options for pytest using the `PYTEST_ADDOPTS` environment variable. This method is useful for temporary configuration changes within a specific environment. The example sets the verbose flag (`-v`).

```bash
export PYTEST_ADDOPTS="-v"

```

--------------------------------

### Pytest Module Function Setup/Teardown

Source: https://docs.pytest.org/en/stable/how-to/xunit_setup

These functions are used at the module level to implement fixtures for test functions. `setup_function` sets up state for a test function, and `teardown_function` cleans it up. The `function` parameter is optional since Pytest 3.0.

```python
def setup_function(function):
    """setup any state tied to the execution of the given function.
    Invoked for every test function in the module.
    """


def teardown_function(function):
    """teardown any state that was previously setup with a setup_function
    call.
    """

```

--------------------------------

### Start PDB at Test Beginning in Pytest

Source: https://docs.pytest.org/en/stable/how-to/failures

Initiate the Python Debugger (pdb) at the very start of each test execution using the `--trace` command-line option. This is helpful for understanding the initial state of a test or for debugging issues that occur early in the test's lifecycle.

```bash
pytest --trace
```

--------------------------------

### Pytest Fixture Usage with @pytest.mark.usefixtures

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Demonstrates how to use the `cleandir` fixture for test methods using the `@pytest.mark.usefixtures` decorator. This ensures the fixture is activated for each test, and shows an example of specifying multiple fixtures.

```python
import os

import pytest


@pytest.mark.usefixtures("cleandir")
class TestDirectoryInit:
    def test_cwd_starts_empty(self):
        assert os.listdir(os.getcwd()) == []
        with open("myfile", "w", encoding="utf-8") as f:
            f.write("hello")

    def test_cwd_again_starts_empty(self):
        assert os.listdir(os.getcwd()) == []


@pytest.mark.usefixtures("cleandir", "anotherfixture")
def test():
    pass
```

--------------------------------

### Spawn Pytest with Pexpect

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Runs pytest using the pexpect library for interactive control. It sets up temporary directories and constructs the command line. Returns a pexpect.spawn object for further interaction.

```python
def spawn_pytest(self, string: str, expect_timeout: float = 10.0) -> pexpect.spawn:
    """Run pytest using pexpect.

    This makes sure to use the right pytest and sets up the temporary
    directory locations.

    The pexpect child is returned.
    """
    basetemp = self.path / "temp-pexpect"
    basetemp.mkdir(mode=0o700)
    invoke = " ".join(map(str, self._getpytestargs()))
    cmd = f"{invoke} --basetemp={basetemp} {string}"
    return self.spawn(cmd, expect_timeout=expect_timeout)
```

--------------------------------

### Module-level setup/teardown in pytest

Source: https://docs.pytest.org/en/stable/how-to/xunit_setup

Implement these methods to set up and tear down state once for all functions within a module. The `module` parameter is optional since pytest 3.0.

```python
def setup_module(module):
    """setup any state specific to the execution of the given module."""


def teardown_module(module):
    """teardown any state that was previously setup with a setup_module
    method.
    """

```

--------------------------------

### Doctest Using Injected Namespace Item

Source: https://docs.pytest.org/en/stable/how-to/doctest

This doctest example assumes that the `numpy` library has been injected into the doctest namespace as `np` (as shown in the previous `conftest.py` example). It then uses `np.arange` within the doctest.

```python
# content of numpy.py
def arange():
    """
    >>> a = np.arange(10)
    >>> len(a)
    10
    """

```

--------------------------------

### Running Pytest with Quiet Mode

Source: https://docs.pytest.org/en/stable/getting-started

Example of executing pytest with the `-q` or `--quiet` flag to produce brief output, showing a successful test run.

```bash
$ pytest -q test_sysexit.py
.                                                                    [100%]
1 passed in 0.12s
```

--------------------------------

### pytest_collectstart

Source: https://docs.pytest.org/en/stable/reference/reference

Collector starts collecting. This hook is called when a collector begins its collection process.

```APIDOC
## pytest_collectstart

### Description
Collector starts collecting.

### Method
HOOK

### Endpoint
N/A (Hook)

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

### Parameters
* **collector** (_Collector_) – The collector.
```

--------------------------------

### Validate Required Plugins

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Ensures that all plugins specified in the `required_plugins` configuration are installed and meet version requirements. It lazily imports `packaging.requirements` and `packaging.version`.

```python
def _validate_plugins(self) -> None:
    required_plugins = sorted(self.getini("required_plugins"))
    if not required_plugins:
        return

    # Imported lazily to improve start-up time.
    from packaging.requirements import InvalidRequirement
    from packaging.requirements import Requirement
    from packaging.version import Version

    plugin_info = self.pluginmanager.list_plugin_distinfo()
    plugin_dist_info = {dist.project_name: dist.version for _, dist in plugin_info}

    missing_plugins = []
    for required_plugin in required_plugins:
        try:
            req = Requirement(required_plugin)
        except InvalidRequirement:
            missing_plugins.append(required_plugin)
            continue

        if req.name not in plugin_dist_info:
            missing_plugins.append(required_plugin)
        elif not req.specifier.contains(
            Version(plugin_dist_info[req.name]), prereleases=True
        ):
            missing_plugins.append(required_plugin)

    if missing_plugins:
        raise UsageError(
            "Missing required plugins: {}".format(", ".join(missing_plugins)),
        )
```

--------------------------------

### Pytest Fixture: Fixture Dependency Example in Python

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Shows how fixtures can depend on other fixtures. The 'first_entry' fixture provides a simple string value, demonstrating how a test or another fixture can request and utilize it.

```python
# contents of test_append.py
import pytest


# Arrange
@pytest.fixture
def first_entry():
    return "a"

```

--------------------------------

### Create text file with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Creates a text file with the specified name and content in the test directory. The path to the created file is returned as a legacy_path object.

```python
def maketxtfile(self, *args, **kwargs) -> LEGACY_PATH:
    """See :meth:`Pytester.maketxtfile`."""
    return legacy_path(self._pytester.maketxtfile(*args, **kwargs))
```

--------------------------------

### Start Interactive Debugger with Pytest

Source: https://docs.pytest.org/en/stable/reference/reference

Starts the interactive Python debugger when errors or KeyboardInterrupt occur. This is useful for inspecting the state of your tests at the point of failure. It leverages the built-in `pdb` module.

```bash
pytest --pdb
```

--------------------------------

### Pytest: Applying marks to parametrize parameters

Source: https://docs.pytest.org/en/stable/historical-notes

This code illustrates how to apply marks, such as `pytest.mark.xfail`, directly to parameters within a `@pytest.mark.parametrize` decorator. The older syntax, shown in the first example, was prone to errors and limitations. The second example demonstrates the correct and recommended way to achieve this, ensuring proper handling of marks and their parameters.

```python
import pytest


@pytest.mark.parametrize(
    "test_input,expected", [("3+5", 8), ("2+4", 6), pytest.mark.xfail(("6*9", 42))]
)
def test_eval(test_input, expected):
    assert eval(test_input) == expected
```

--------------------------------

### Pytest Output Capture Example

Source: https://docs.pytest.org/en/stable/how-to/capture-stdout-stderr

Demonstrates using the 'capsys' fixture in pytest to capture standard output and standard error streams during test execution. It shows how to assert the captured output.

```python
import sys

def test_myoutput(capsys):
    print("hello")
    sys.stderr.write("world\n")
    captured = capsys.readouterr()
    assert captured.out == "hello\n"
    assert captured.err == "world\n"
    print("next")
    captured = capsys.readouterr()
    assert captured.out == "next\n"
```

--------------------------------

### Get Configuration File Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Retrieves the absolute path to the Pytest configuration file (e.g., pytest.ini, setup.cfg). Returns None if no configuration file is found.

```python
@property
def inipath(self) -> pathlib.Path | None:
    """The path to the :ref:`configfile <configfiles>`. 

    .. versionadded:: 6.1
    """
    return self._inipath
```

--------------------------------

### Create pyproject.toml with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Creates a pyproject.toml file with the specified source content in the test directory. The path to the created file is returned as a legacy_path object.

```python
def makepyprojecttoml(self, source) -> LEGACY_PATH:
    """See :meth:`Pytester.makepyprojecttoml`."""
    return legacy_path(self._pytester.makepyprojecttoml(source))
```

--------------------------------

### Pytest Capture Manager Initialization and Cleanup

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

This snippet shows the initialization of Pytest's capture manager, including necessary workarounds for Windows console I/O and readline, registering the capture manager with the plugin manager, and setting up cleanup routines to stop global capturing at the end of the test session. It also demonstrates starting global capturing before yielding control to the tests and handling exceptions by capturing and writing any output before re-raising.

```python
ns = early_config.known_args_namespace
if ns.capture == "fd":
    _windowsconsoleio_workaround(sys.stdout)
_colorama_workaround()
_readline_workaround()
pluginmanager = early_config.pluginmanager
capman = CaptureManager(ns.capture)
pluginmanager.register(capman, "capturemanager")

# Make sure that capturemanager is properly reset at final shutdown.
early_config.add_cleanup(capman.stop_global_capturing)

# Finally trigger conftest loading but while capturing (issue #93).
capman.start_global_capturing()
try:
    try:
        yield
    finally:
        capman.suspend_global_capture()
except BaseException:
    out, err = capman.read_global_capture()
    sys.stdout.write(out)
    sys.stderr.write(err)
    raise
```

--------------------------------

### Build Pytest Documentation Locally

Source: https://docs.pytest.org/en/stable/contributing

Command to build the documentation locally using tox. This command executes the documentation build process within a tox environment, making the built documentation accessible in the specified directory.

```bash
$ tox -e docs
```

--------------------------------

### Install Package in Editable Mode (Shell)

Source: https://docs.pytest.org/en/stable/explanation/goodpractices

This command installs the current Python package in editable mode using pip. This allows changes in the source code to be immediately reflected without reinstallation, which is ideal for development and testing cycles.

```shell
pip install -e .

```

--------------------------------

### Get Marks Directly Applied to Class in Python

Source: https://docs.pytest.org/en/stable/_modules/_pytest/mark/structures

Demonstrates how to get only the marks directly applied to a Python class, ignoring marks from its superclasses, using the `consider_mro=False` option in `get_unpacked_marks`.

```python
import pytest

class BaseClass:
    @pytest.mark.BASE_MARK
    pass

class DerivedClass(BaseClass):
    @pytest.mark.DERIVED_MARK
    pass

# Get only marks directly on DerivedClass
# This will exclude BASE_MARK
derived_marks = pytest.get_unpacked_marks(DerivedClass, consider_mro=False)

print(f"Derived class marks (direct): {derived_marks}")

```

--------------------------------

### Python System Path and Directory Reset

Source: https://docs.pytest.org/en/stable/_modules/_pytest/monkeypatch

Illustrates how to restore the system path and current working directory to their original states after potential modifications. It checks if saved paths and directories exist before applying the reset.

```python
self._setitem[:] = []
        if self._savesyspath is not None:
            sys.path[:] = self._savesyspath
            self._savesyspath = None

        if self._cwd is not None:
            os.chdir(self._cwd)
            self._cwd = None
```

--------------------------------

### Add Command-Line Option with Choices in Pytest conftest.py

Source: https://docs.pytest.org/en/stable/example/simple

This example extends the previous one by adding a 'choices' parameter to the '--cmdopt' command-line option. This restricts the allowed values for the option to 'type1' or 'type2', providing built-in validation and user feedback for invalid choices.

```python
import pytest


def pytest_addoption(parser):
    parser.addoption(
        "--cmdopt",
        action="store",
        default="type1",
        help="my option: type1 or type2",
        choices=("type1", "type2"),
    )
```

--------------------------------

### pytest_collectstart

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

This hook is called when a Collector starts its collection process. It provides the collector object that is about to begin collecting items.

```APIDOC
## POST /pytest_collectstart

### Description
Called when a Collector starts collecting. This hook allows for actions to be taken just before a collector begins its work.

### Method
POST

### Endpoint
/pytest_collectstart

### Parameters
#### Query Parameters
- **collector** (Collector) - Required - The collector that is starting its collection.

### Request Example
```json
{
  "collector": { /* Collector object */ }
}
```

### Response
#### Success Response (200)
- **None** - This hook does not return a value.

#### Response Example
```json
{
  "message": "Collector started successfully."
}
```
```

--------------------------------

### Add Finalizer Callback (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

Registers a callable function to be executed without arguments when the node is finalized. This method must be called when the node is active in a setup chain, such as during `self.setup()`.

```python
def addfinalizer(self, fin: Callable[[], object]) -> None:
    """Register a function to be called without arguments when this node is
    finalized.

    This method can only be called when this node is active
    in a setup chain, for example during self.setup().
    """
    self.session._setupstate.addfinalizer(fin, self)
```

--------------------------------

### Install Pytest Assertion Rewriting Import Hook

Source: https://docs.pytest.org/en/stable/_modules/_pytest/assertion

This function installs pytest's assertion rewriting import hook into sys.meta_path. It stores the hook and associated state in the pytest configuration's stash and ensures the hook is removed upon cleanup.

```python
def install_importhook(config: Config) -> rewrite.AssertionRewritingHook:
    """Try to install the rewrite hook, raise SystemError if it fails."""
    config.stash[assertstate_key] = AssertionState(config, "rewrite")
    config.stash[assertstate_key].hook = hook = rewrite.AssertionRewritingHook(config)
    sys.meta_path.insert(0, hook)
    config.stash[assertstate_key].trace("installed rewrite import hook")

    def undo() -> None:
        hook = config.stash[assertstate_key].hook
        if hook is not None and hook in sys.meta_path:
            sys.meta_path.remove(hook)

    config.add_cleanup(undo)
    return hook
```

--------------------------------

### Get Configuration Value (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Retrieves a configuration value by name. If the value is not found in the configuration file, it returns the registered default value. Raises ValueError if the name has not been registered.

```python
def getini(self, name: str) -> Any:
    """Return configuration value the an :ref:`configuration file <configfiles>`. 

    If a configuration value is not defined in a
    :ref:`configuration file <configfiles>`, then the ``default`` value
    provided while registering the configuration through
    :func:`parser.addini <pytest.Parser.addini>` will be returned. 
    Please note that you can even provide ``None`` as a valid
    default value.

    If ``default`` is not provided while registering using
    :func:`parser.addini <pytest.Parser.addini>`, then a default value
    based on the ``type`` parameter passed to
    :func:`parser.addini <pytest.Parser.addini>` will be returned.
    The default values based on ``type`` are:
    ``paths``, ``pathlist``, ``args`` and ``linelist`` : empty list ``[]``
    ``bool`` : ``False``
    ``string`` : empty string ``""``
    ``int`` : ``0``
    ``float`` : ``0.0``

    If neither the ``default`` nor the ``type`` parameter is passed
    while registering the configuration through
    :func:`parser.addini <pytest.Parser.addini>`, then the configuration
    is treated as a string and a default empty string '' is returned.

    If the specified name hasn't been registered through a prior
    :func:`parser.addini <pytest.Parser.addini>` call (usually from a
    plugin), a ValueError is raised.
    """
    canonical_name = self._parser._ini_aliases.get(name, name)
    try:
        return self._inicache[canonical_name]
    except KeyError:
        pass
    self._inicache[canonical_name] = val = self._getini(canonical_name)
    return val
```

--------------------------------

### Pytest Incremental Test Class Example

Source: https://docs.pytest.org/en/stable/example/simple

This Python code demonstrates a pytest test class using the 'incremental' marker. If any test within this class fails, subsequent tests in the same class will be automatically skipped and marked as expected failures.

```python
# content of test_step.py

import pytest


@pytest.mark.incremental
class TestUserHandling:
    def test_login(self):
        pass

    def test_modification(self):
        assert 0

    def test_deletion(self):
        pass


def test_normal():
    pass
```

--------------------------------

### Pytest Command Line Main Entry Point

Source: https://docs.pytest.org/en/stable/_modules/_pytest/main

The primary function for initiating a pytest command-line session. It wraps the core session logic, ensuring proper setup and execution.

```python
def pytest_cmdline_main(config: Config) -> int | ExitCode:
    return wrap_session(config, _main)
```

--------------------------------

### Loading Setuptools Entry Points in PytestPluginManager

Source: https://docs.pytest.org/en/stable/reference/reference

Loads plugins by querying a specified setuptools entry point group. Optionally, it can filter by a specific plugin name within that group. Returns the count of loaded plugins.

```python
def load_setuptools_entrypoints(self, _group_, _name=None):
    """Load modules from querying the specified setuptools `group`."""
    # Implementation details...
```

--------------------------------

### Copy Files from Project with pytester.copy_example

Source: https://docs.pytest.org/en/stable/reference/reference

The `copy_example` method copies a file from the project's directory into the test directory. An optional name can be provided for the copied file.

```python
pytester.copy_example("my_test_file.py")

```

--------------------------------

### Getting Canonical Plugin Name in PytestPluginManager

Source: https://docs.pytest.org/en/stable/reference/reference

Returns a canonical name for a plugin object. Note that a plugin might be registered under a different name. Use get_name(plugin) to get the actual registered name.

```python
def get_canonical_name(self, _plugin_):
    """Return a canonical name for a plugin object."""
    # Implementation details...
```

--------------------------------

### Pytest Assertion Helper with Traceback Hiding

Source: https://docs.pytest.org/en/stable/example/simple

This example illustrates how to create a helper function 'checkconfig' that can be used in pytest tests. By setting '__tracebackhide__ = True', the internal calls to this helper function are hidden in the traceback when a test fails, making the failure report cleaner and focusing on the test itself. It uses 'pytest.fail' to report an error with a specific message.

```python
# content of test_checkconfig.py
import pytest


def checkconfig(x):
    __tracebackhide__ = True
    if not hasattr(x, "config"):
        pytest.fail(f"not configured: {x}")


def test_something():
    checkconfig(42)
```

--------------------------------

### Get Crash Line in Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

The `_getcrashline` method extracts a concise crash message from a test report. It attempts to get the crash message from `longrepr.reprcrash` or falls back to a truncated string representation of `longrepr`.

```python
    def _getcrashline(self, rep):
        try:
            return str(rep.longrepr.reprcrash)
        except AttributeError:
            try:
                return str(rep.longrepr)[:50]
            except AttributeError:
                return ""
```

--------------------------------

### Create Python file with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Creates a Python file (e.g., test_*.py) with the provided source code or arguments. The path to the created file is returned as a legacy_path object.

```python
def makepyfile(self, *args, **kwargs) -> LEGACY_PATH:
    """See :meth:`Pytester.makepyfile`."""
    return legacy_path(self._pytester.makepyfile(*args, **kwargs))
```

--------------------------------

### TempdirFactory.mktemp

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Creates a temporary directory with a given basename, returning it as a legacy path object.

```APIDOC
## POST /tmppath_factory/mktemp

### Description
Creates a temporary directory with the given basename. If `numbered` is True, a unique number will be appended to the basename. Returns the created directory as a ``py.path.local`` object.

### Method
POST

### Endpoint
/tmppath_factory/mktemp

### Parameters
#### Query Parameters
- **basename** (str) - Required - The base name for the temporary directory.
- **numbered** (bool) - Optional - If True, a unique number will be appended to the basename. Defaults to True.

### Request Example
```json
{
  "basename": "test_dir",
  "numbered": true
}
```

### Response
#### Success Response (200)
- **mktemp** (LEGACY_PATH) - A legacy path object representing the created temporary directory.

#### Response Example
```json
{
  "mktemp": "/path/to/temporary/directory/test_dir0"
}
```
```

--------------------------------

### Advanced Pytest Topics and Customization

Source: https://docs.pytest.org/en/stable/contents

Covers advanced techniques for customizing pytest, including examples, parametrization, working with custom markers, and managing non-Python tests.

```APIDOC
## Advanced Pytest Topics and Customization

### Description
This section explores advanced usage patterns and customization options within pytest, providing practical examples and techniques for tailoring pytest to specific project needs.

### Advanced Topics

*   **Examples and Customization Tricks**: Demonstrations of Python failure reports, basic patterns, parametrizing tests, working with custom markers, creating session-scoped fixtures, modifying test discovery, handling non-Python tests, and using custom directory collectors.
*   **Backwards Compatibility Policy**: Information on pytest's commitment to backwards compatibility.
*   **History**: Overview of significant changes and milestones in pytest's development.
*   **Python Version Support**: Details on supported Python versions.
*   **Deprecations and Removals**: Information on deprecated features and breaking changes in recent versions.
*   **Contributing**: Guidelines for contributing to pytest, including feature requests, bug reporting, bug fixing, implementation, documentation writing, plugin submission, pull request preparation, joining the development team, merge/squash guidelines, backporting fixes, handling stale issues, and closing issues.
*   **Development Guide**: A guide for developers working on pytest itself.
*   **Sponsor**: Information on how to sponsor pytest development.
*   **Pytest for Enterprise**: Information relevant to enterprise usage.
*   **License**: The license under which pytest is distributed.
*   **Contact Channels**: Ways to get in touch with the pytest community (web, chat, microblogging, mail, etc.).
*   **Historical Notes**: Specific historical details about major changes and features (e.g., marker revamp, cache plugin integration, funcargs, `@pytest.yield_fixture`, etc.).
*   **Talks and Tutorials**: Links to books, talks, and blog postings related to pytest.
```

--------------------------------

### Dynamically Modify Pytest Command-Line Arguments

Source: https://docs.pytest.org/en/stable/example/simple

This example shows how to dynamically modify pytest's command-line arguments before they are processed, using the pytest_load_initial_conftests hook. It checks for the presence of the 'xdist' plugin and, if found, modifies the arguments to include '-n' with a number of subprocesses based on CPU count.

```python
import sys


def pytest_load_initial_conftests(args):
    if "xdist" in sys.modules:  # pytest-xdist plugin
        import multiprocessing

        num = max(multiprocessing.cpu_count() / 2, 1)
        args[:] = ["-n", str(num)] + args
```

--------------------------------

### Configuration Options

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Methods for retrieving command-line option values and handling their absence.

```APIDOC
## GET /config/options

### Description
Retrieves command-line option values. Supports fallback defaults and skipping if options are undeclared or have null values.

### Method
GET

### Endpoint
/config/options

### Parameters
#### Query Parameters
- **name** (string) - Required - The name of the option to retrieve. Can be the option's 'dest' name or the literal '--OPT' name.
- **default** (any) - Optional - A fallback value to return if the option is not declared. Ignored if the option is declared, even if its value is None.
- **skip** (boolean) - Optional - If True, raises `pytest.skip` if the option is undeclared or has a None value. If a default is provided, it will be returned instead of skipping.

### Response
#### Success Response (200)
- **value** (any) - The value of the requested option.

#### Response Example
```json
{
  "value": "some_option_value"
}
```

## GET /config/value

### Description
Deprecated method for retrieving command-line option values. Use `getoption()` instead.

### Method
GET

### Endpoint
/config/value

### Parameters
#### Query Parameters
- **name** (string) - Required - The name of the option.
- **path** (string) - Optional - Path parameter (unused in this deprecated method).

### Response
#### Success Response (200)
- **value** (any) - The value of the requested option.

#### Response Example
```json
{
  "value": "some_option_value"
}
```

## GET /config/valueorskip

### Description
Deprecated method for retrieving command-line option values with skipping behavior. Use `getoption(skip=True)` instead.

### Method
GET

### Endpoint
/config/valueorskip

### Parameters
#### Query Parameters
- **name** (string) - Required - The name of the option.
- **path** (string) - Optional - Path parameter (unused in this deprecated method).

### Response
#### Success Response (200)
- **value** (any) - The value of the requested option.

#### Response Example
```json
{
  "value": "some_option_value"
}
```
```

--------------------------------

### Configure Pytest Plugin for FD Leak Checking

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Configures pytest upon startup, specifically registering an `LsofFdLeakChecker` if the '--lsof' option is enabled and the platform supports 'lsof'. It also adds a custom marker for example paths.

```python
def pytest_configure(config: Config) -> None:
    if config.getvalue("lsof"):
        checker = LsofFdLeakChecker()
        if checker.matching_platform():
            config.pluginmanager.register(checker)

    config.addinivalue_line(
        "markers",
        "pytester_example_path(*path_segments): join the given path "
        "segments to `pytester_example_dir` for this test.",
    )
```

--------------------------------

### Get Configuration Option

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Retrieves the value of a specified configuration option. If the option is not found, it returns a default value or raises a ValueError if the option was never registered.

```APIDOC
## GET /config/ini/{name}

### Description
Retrieves the value of a configuration option by its name. It handles aliases and provides default values based on registration type or explicit defaults. Raises ValueError if the option is unknown.

### Method
GET

### Endpoint
/config/ini/{name}

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the configuration option to retrieve.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **value** (any) - The value of the configuration option. The type depends on how the option was registered (e.g., string, list, boolean, int, float).

#### Response Example
```json
{
  "value": "some_config_value"
}
```

#### Error Response (400)
- **error** (string) - Description of the error, e.g., "unknown configuration value: 'non_existent_option'"

#### Error Response Example
```json
{
  "error": "unknown configuration value: 'non_existent_option'"
}
```
```

--------------------------------

### Imperatively Xfail a Test (pytest.xfail)

Source: https://docs.pytest.org/en/stable/reference/reference

Imperatively marks the current test or setup function as xfailed with a given reason. This function should only be called during test execution (setup, call, or teardown) as it raises an exception internally. It is generally recommended to use the `pytest.mark.xfail` marker for declaring xfailed tests under specific conditions.

```python
import pytest

pytest.xfail("This feature is not yet implemented.")

```

--------------------------------

### Check for Setup.py in Pytest Doctest Collection

Source: https://docs.pytest.org/en/stable/_modules/_pytest/doctest

Helper function to determine if a given path points to a 'setup.py' file. This is used to prevent running doctests within setup files, which is generally not intended.

```python
def _is_setup_py(path: Path) -> bool:
    if path.name != "setup.py":
        return False
    contents = path.read_bytes()
    return b"setuptools" in contents or b"distutils" in contents
```

--------------------------------

### Pytest Fixtures: Manual Execution for Multiple Tests

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Presents the manual execution flow for multiple tests that utilize the same fixtures. This example clarifies how each test receives its own set of fixture results, reinforcing the concept of fixture isolation.

```python
def first_entry():
    return "a"


def order(first_entry):
    return [first_entry]


def test_string(order):
    # Act
    order.append("b")

    # Assert
    assert order == ["a", "b"]


def test_int(order):
    # Act
    order.append(2)

    # Assert
    assert order == ["a", 2]


entry = first_entry()
the_list = order(first_entry=entry)
test_string(order=the_list)

entry = first_entry()
the_list = order(first_entry=entry)
test_int(order=the_list)

```

--------------------------------

### Pytest Collection Hook

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

The pytest_collection hook is the entry point for the collection phase. It performs the collection of tests starting from a given session. This hook can be implemented to perform actions before collection begins, such as starting a collection counter in the terminal plugin. It stops at the first non-None result.

```python
@hookspec(firstresult=True)
def pytest_collection(session: Session) -> object | None:
    """Perform the collection phase for the given session.

    Stops at first non-None result, see :ref:`firstresult`.
    The return value is not used, but only stops further processing.

    The default collection phase is this (see individual hooks for full details):

    1. Starting from ``session`` as the initial collector:

      1. ``pytest_collectstart(collector)``
      2. ``report = pytest_make_collect_report(collector)``
      3. ``pytest_exception_interact(collector, call, report)`` if an interactive exception occurred
      4. For each collected node:

        1. If an item, ``pytest_itemcollected(item)``
        2. If a collector, recurse into it.

      5. ``pytest_collectreport(report)``

    2. ``pytest_collection_modifyitems(session, config, items)``

      1. ``pytest_deselected(items)`` for any deselected items (may be called multiple times)

    3. ``pytest_collection_finish(session)``
    4. Set ``session.items`` to the list of collected items
    5. Set ``session.testscollected`` to the number of collected items

    You can implement this hook to only perform some action before collection, 
    for example the terminal plugin uses it to start displaying the collection
    counter (and returns `None`).

    :param session: The pytest session object.

    Use in conftest plugins
    =======================

    This hook is only called for :ref:`initial conftests <pluginorder>`.
    """
    pass
```

--------------------------------

### Stash Data Storage Example (Python)

Source: https://docs.pytest.org/en/stable/reference/reference

Illustrates the usage of Pytest's Stash for type-safe, heterogeneous data storage. It shows how to create StashKeys and store/retrieve data associated with them.

```python
# At the top-level of the module
some_str_key = StashKey[str]()
some_bool_key = StashKey[bool]()

# To store information:
stash: Stash = some_object.stash
stash[some_str_key] = "some value"
stash[some_bool_key] = True

# To retrieve information:
retrieved_str = stash[some_str_key]
retrieved_bool = stash[some_bool_key]
```

--------------------------------

### Create .toml Files with pytester.maketoml

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `maketoml` method creates a `.toml` file, commonly used for configuration like `pytest.toml`. It accepts the file content as a string and returns the `Path` object.

```python
def maketoml(self, source: str) -> Path:
    """Write a pytest.toml file.

    :param source: The contents.
    :returns: The pytest.toml file.

    .. versionadded:: 9.0
    """
    return self.makefile(".toml", pytest=source)
```

--------------------------------

### Select Pytest Tests with '-m interface' Option

Source: https://docs.pytest.org/en/stable/example/markers

This example shows the command-line usage of pytest to run only tests marked with the 'interface' marker. The output illustrates a test session where tests are collected, filtered, and failures are reported, demonstrating the effect of the '-m interface' option.

```bash
$ pytest -m interface --tb=short
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y
rootdir: /home/sweet/project
collected 4 items / 2 deselected / 2 selected

test_module.py FF                                                    [100%]

================================= FAILURES =================================
__________________________ test_interface_simple ___________________________
test_module.py:4: in test_interface_simple
    assert 0
E   assert 0
__________________________ test_interface_complex __________________________
test_module.py:8: in test_interface_complex
    assert 0
E   assert 0
========================= short test summary info ==========================
FAILED test_module.py::test_interface_simple - assert 0
FAILED test_module.py::test_interface_complex - assert 0
===================== 2 failed, 2 deselected in 0.12s ======================
```

--------------------------------

### Run unittest-based tests with pytest

Source: https://docs.pytest.org/en/stable/announce/release-2.0.0

Illustrates how pytest can discover and run tests written using Python's built-in `unittest` module. This includes running tests from installed packages.

```bash
py.test --pyargs unittest

```

--------------------------------

### Pytest Run Test Log Start Hook (pytest_runtest_logstart)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

The `pytest_runtest_logstart` hook is called at the beginning of the runtest protocol for an individual test item. It receives the item's node ID and location information (filename, line number, test name). This hook can be implemented in conftest plugins to perform actions before a test starts executing.

```python
def pytest_runtest_logstart(nodeid: str, location: tuple[str, int | None, str]) -> None:
    """Called at the start of running the runtest protocol for a single item."""
    pass
```

--------------------------------

### Session.startdir

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Returns the path from which pytest was invoked, as a legacy path object.

```APIDOC
## GET /session/startdir

### Description
Returns the path from which pytest was invoked. It is recommended to use ``startpath`` which provides a ``pathlib.Path`` object instead.

### Method
GET

### Endpoint
/session/startdir

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **startdir** (LEGACY_PATH) - The legacy path object of the invocation directory.

#### Response Example
```json
{
  "startdir": "/path/where/pytest/was/invoked"
}
```
```

--------------------------------

### Pytest Xfail Mechanism Examples

Source: https://docs.pytest.org/en/stable/changelog

Demonstrates the usage of the `@py.test.mark.xfail` decorator for marking tests as expected to fail. It shows how to prevent a decorated test from running (`run=False`) and how to provide a reason for the failure.

```python
@py.test.mark.xfail(run=False)
def test_this_should_not_run():
    assert False

@py.test.mark.xfail(reason="This test is expected to fail due to a known issue")
def test_known_failure():
    assert 1 == 2
```

--------------------------------

### Pytest Session Start Hook (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

Implements the pytest_sessionstart hook for the TerminalProgressPlugin. This method is called when the pytest session begins and initializes the progress display by emitting an 'indeterminate' state. It stores the session object for later use.

```python
@hookimpl
def pytest_sessionstart(self, session: Session) -> None:
    self._session = session
    # Show indeterminate progress during collection.
    self._emit_progress("indeterminate")
```

--------------------------------

### Get Base Temporary Directory with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

The `getbasetemp` method retrieves the base temporary directory. Similar to `TempPathFactory.getbasetemp`, it returns a `py.path.local` object.

```python
def getbasetemp(self) -> LEGACY_PATH:
    """Same as :meth:`TempPathFactory.getbasetemp`, but returns a ``py.path.local`` object."""
    return legacy_path(self._tmppath_factory.getbasetemp().resolve())
```

--------------------------------

### pytest.xfail

Source: https://docs.pytest.org/en/stable/reference/reference

Imperatively xfails an executing test or setup function with a given reason.

```APIDOC
## POST /pytest.xfail

### Description
Imperatively xfails an executing test or setup function with the given reason. This function should be called only during testing.

### Method
POST

### Endpoint
/pytest.xfail

### Parameters
#### Query Parameters
- **reason** (str) - Required - The message to show the user as reason for the xfail.

### Request Example
{
  "reason": "Known bug in feature X"
}

### Response
#### Success Response (200)
- **status** (str) - Indicates that the test has been xfailed.

#### Response Example
{
  "status": "XFAIL"
}
```

--------------------------------

### Create Text Files with pytester.maketxtfile

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `maketxtfile` method is a shortcut for `makefile` with a `.txt` extension. It defaults to creating a file named after the test function, overwriting existing files. It can create multiple files using keyword arguments.

```python
def maketxtfile(self, *args, **kwargs) -> Path:
    r"""Shortcut for .makefile() with a .txt extension.

    Defaults to the test name with a '.txt' extension, e.g test_foobar.txt, overwriting
    existing files.

    Examples:

    .. code-block:: python

        def test_something(pytester):
            # Initial file is created test_something.txt.
            pytester.maketxtfile("foobar")
            # To create multiple files, pass kwargs accordingly.
            pytester.maketxtfile(custom="foobar")
            # At this point, both 'test_something.txt' & 'custom.txt' exist in the test directory.

    """
    return self._makefile(".txt", args, kwargs)
```

--------------------------------

### Create Text Files in Test Directory

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Public method to create new text file(s) in the test directory with a specified file extension. It accepts file names and content as arguments.

```python
def makefile(self, ext: str, *args: str, **kwargs: str) -> Path:
    r"""Create new text file(s) in the test directory.

    :param ext:
        The extension the file(s) should use, including the dot, e.g. `.py`.
    """
```

--------------------------------

### Pytest --lfnf Option Behavior (Shell)

Source: https://docs.pytest.org/en/stable/how-to/cache

This example shows the usage of the --last-failed-no-failures (or --lfnf) option in pytest. It demonstrates how to configure pytest's behavior when no tests failed in the previous run. The 'all' option runs the full suite, while 'none' exits without running tests.

```shell
pytest --last-failed --last-failed-no-failures all

```

```shell
pytest --last-failed --last-failed-no-failures none

```

--------------------------------

### Require Plugins in Test Modules or conftest.py

Source: https://docs.pytest.org/en/stable/how-to/plugins

Shows how to specify plugins to be loaded automatically when a test module or conftest.py file is processed. Note that using `pytest_plugins` in non-root conftest.py files is deprecated.

```python
pytest_plugins = ("myapp.testsupport.myplugin",)
```

--------------------------------

### Cache.makedir

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Creates a subdirectory within the cache, returning it as a legacy path object.

```APIDOC
## POST /cache/makedir

### Description
Creates a directory with the given name within the cache. Returns the created directory path as a legacy ``py.path.local`` instance.

### Method
POST

### Endpoint
/cache/makedir

### Parameters
#### Query Parameters
- **name** (str) - Required - The name of the directory to create.

### Request Example
```json
{
  "name": "my_cache_dir"
}
```

### Response
#### Success Response (200)
- **makedir** (LEGACY_PATH) - A legacy path object representing the created cache directory.

#### Response Example
```json
{
  "makedir": "/path/to/cache/my_cache_dir"
}
```
```

--------------------------------

### pytest_runtest_logstart

Source: https://docs.pytest.org/en/stable/reference/reference

Called at the start of running the runtest protocol for a single test item. This hook is part of the test execution logging process.

```APIDOC
## pytest_runtest_logstart

### Description
Called at the start of running the runtest protocol for a single item. See `pytest_runtest_protocol` for a description of the runtest protocol.

### Method
HOOK

### Endpoint
N/A (Hook)

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

### Parameters
* **nodeid** (_str_) – Full node ID of the item.
* **location** (_tuple_ _[__str_ _,__int_ _|__None_ _,__str_ _]_) – A tuple of `(filename, lineno, testname)` where `filename` is a file path relative to `config.rootpath` and `lineno` is 0-based.
```

--------------------------------

### Pytest Autouse Fixture Execution Order Example

Source: https://docs.pytest.org/en/stable/reference/fixtures

Demonstrates the execution order of fixtures, including autouse fixtures and fixtures that depend on them. The 'order' fixture records the sequence of fixture execution.

```python
from __future__ import annotations

import pytest


@pytest.fixture
def order():
    return []


@pytest.fixture
def a(order):
    order.append("a")


@pytest.fixture
def b(a, order):
    order.append("b")


@pytest.fixture(autouse=True)
def c(b, order):
    order.append("c")


@pytest.fixture
def d(b, order):
    order.append("d")


@pytest.fixture
def e(d, order):
    order.append("e")


@pytest.fixture
def f(e, order):
    order.append("f")


@pytest.fixture
def g(f, c, order):
    order.append("g")


def test_order_and_g(g, order):
    assert order == ["a", "b", "c", "d", "e", "f", "g"]

```

--------------------------------

### Pytest Explanation and Best Practices

Source: https://docs.pytest.org/en/stable/contents

Explains fundamental concepts of pytest, such as the anatomy of a test, the purpose and benefits of fixtures, and best practices for integration and handling flaky tests.

```APIDOC
## Pytest Explanation and Best Practices

### Description
This section provides in-depth explanations of core pytest concepts and offers guidance on best practices for integrating pytest into your projects and managing common testing challenges.

### Core Concepts

*   **Anatomy of a Test**: Understanding the structure of a pytest test.
*   **Fixtures**: Detailed explanation of what fixtures are, their advantages over xUnit-style setup/teardown, handling fixture errors, sharing test data, and cleanup procedures.
*   **Good Integration Practices**: Guidelines for installing packages with pip, Python test discovery conventions, choosing test layouts, using `tox`, avoiding running tests via `setuptools`, checking code with `flake8-pytest-style`, and using pytest's strict mode.
*   **Flaky Tests**: Discussion on the problem of flaky tests, their potential root causes, related pytest features, general strategies for mitigation, and relevant research and resources.
*   **Import Mechanisms**: How pytest handles imports and interacts with `sys.path` and `PYTHONPATH`, including different import modes and scenarios.
```

--------------------------------

### Get Unknown INI Keys

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Retrieves a set of configuration keys that are present in the current configuration but not recognized by pytest's parser or its aliases.

```python
def _get_unknown_ini_keys(self) -> set[str]:
    known_keys = self._parser._inidict.keys() | self._parser._ini_aliases.keys()
    return self._inicfg.keys() - known_keys
```

--------------------------------

### Use Fixtures in Doctests with getfixture

Source: https://docs.pytest.org/en/stable/how-to/doctest

This example demonstrates how to use pytest fixtures within doctests by employing the `getfixture` helper function. The fixture must be accessible to pytest, typically defined in a `conftest.py` file or a plugin.

```python
# content of example.rst
>>> tmp = getfixture('tmp_path')
>>> ...
>>>

```

--------------------------------

### Get Module Collection

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Performs collection on a module represented by source code, with optional configuration arguments and initialization flag. It returns the module collector. This is useful for testing module-level collection behavior.

```python
def getmodulecol(self, source, configargs=(), withinit=False):
    """See :meth:`Pytester.getmodulecol`."""
    return self._pytester.getmodulecol(
        source, configargs=configargs, withinit=withinit
    )
```

--------------------------------

### Pytest Fixture: Manual Execution Equivalent

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Shows the manual equivalent of executing pytest fixtures and tests. This helps understand the underlying process when fixtures are requested by tests, illustrating how dependencies are resolved and executed.

```python
def first_entry():
    return "a"


def order(first_entry):
    return [first_entry]


def test_string(order):
    # Act
    order.append("b")

    # Assert
    assert order == ["a", "b"]


entry = first_entry()
the_list = order(first_entry=entry)
test_string(order=the_list)
```

--------------------------------

### Configure pytest using ini-files

Source: https://docs.pytest.org/en/stable/announce/release-2.0.0

Shows how to customize pytest's behavior by using configuration options in ini-files like `setup.cfg` or `tox.ini`. This allows for default command-line options and directory exclusion rules.

```ini
[pytest]
norecursedirs = .hg data*  # don't ever recurse in such dirs
addopts = -x --pyargs      # add these command line options by default

```

--------------------------------

### Get Current Line Width

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

A property that returns the width of the current line in the terminal. This is useful for calculating spacing and positioning of output.

```python
@property
    def _width_of_current_line(self) -> int:
        """Return the width of the current line."""
        return self._tw.width_of_current_line
```

--------------------------------

### pytest_runtest_makereport

Source: https://docs.pytest.org/en/stable/reference/reference

Called to create a `TestReport` for each of the setup, call, and teardown runtest phases of a test item.

```APIDOC
## pytest_runtest_makereport

### Description
Called to create a `TestReport` for each of the setup, call and teardown runtest phases of a test item. See `pytest_runtest_protocol` for a description of the runtest protocol.

### Method
HOOK

### Endpoint
N/A (Hook)

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

### Parameters
* **item** (_Item_) – The item.
* **call** (_CallInfo_ _[__None_ _]_) – The `CallInfo` for the phase.

Stops at first non-None result, see firstresult: stop at first non-None result.
```

--------------------------------

### Get Items by Source

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Collects and returns all test items found within the provided source code. It returns a list of Item objects. This method is helpful for analyzing test structures within a given script.

```python
def getitems(self, source):
    """See :meth:`Pytester.getitems`."""
    return self._pytester.getitems(source)
```

--------------------------------

### Create conftest.py with pytester.makeconftest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `makeconftest` method is a convenience function to create a `conftest.py` file. It takes the file's source content as a string and returns the created `Path` object.

```python
def makeconftest(self, source: str) -> Path:
    """Write a conftest.py file.

    :param source: The contents.
    :returns: The conftest.py file.
    """
    return self.makepyfile(conftest=source)
```

--------------------------------

### Write and Run a Basic Pytest Test

Source: https://docs.pytest.org/en/stable/index

This snippet demonstrates how to write a simple test function using pytest and how to execute it. It includes a function `inc` and a test function `test_answer` that asserts the output of `inc`. The example also shows the expected output when the test fails.

```python
# content of test_sample.py
def inc(x):
    return x + 1

def test_answer():
    assert inc(3) == 5

```

```bash
$ pytest
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y
rootdir: /home/sweet/project
collected 1 item

test_sample.py F                                                     [100%]

================================= FAILURES =================================
_______________________________ test_answer ________________________________

    def test_answer():
>       assert inc(3) == 5
E       assert 4 == 5
E        +  where 4 = inc(3)

test_sample.py:6: AssertionError
========================= short test summary info ==========================
FAILED test_sample.py::test_answer - assert 4 == 5
============================ 1 failed in 0.12s =============================

```

--------------------------------

### Configure Doctest Options in Pytest (INI)

Source: https://docs.pytest.org/en/stable/how-to/doctest

This snippet demonstrates configuring pytest's doctest options using an INI file. It achieves the same result as the TOML example by specifying 'NORMALIZE_WHITESPACE' and 'IGNORE_EXCEPTION_DETAIL' flags.

```ini
[pytest]
doctest_optionflags = NORMALIZE_WHITESPACE IGNORE_EXCEPTION_DETAIL

```

--------------------------------

### Spawn Generic Command with Pexpect

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Executes a generic command using the pexpect library. It's a flexible way to run external commands and capture their output. Returns a pexpect.spawn object.

```python
def spawn(self, cmd: str, expect_timeout: float = 10.0) -> pexpect.spawn:
    """Run a command using pexpect.

    The pexpect child is returned.
    """
    pexpect = importorskip("pexpect", "3.0")
    if hasattr(sys, "pypy_version_info") and "64" in platform.machine():
        skip("pypy-64 bit not supported")
    if not hasattr(pexpect, "spawn"):
        skip("pexpect.spawn not available")
    logfile = self.path.joinpath("spawn.out").open("wb")

    child = pexpect.spawn(cmd, logfile=logfile, timeout=expect_timeout)
    self._request.addfinalizer(logfile.close)
    return child
```

--------------------------------

### Select Pytest Tests with '-m "interface or event"' Option

Source: https://docs.pytest.org/en/stable/example/markers

This example demonstrates how to use the pytest command line to execute tests marked with either 'interface' or 'event'. The output shows a test session where tests matching either marker are run, and the summary reflects the combined results of both sets of tests.

```bash
$ pytest -m "interface or event" --tb=short
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y
rootdir: /home/sweet/project
collected 4 items / 1 deselected / 3 selected

test_module.py FFF                                                   [100%]

================================= FAILURES =================================
__________________________ test_interface_simple ___________________________
test_module.py:4: in test_interface_simple
    assert 0
E   assert 0
__________________________ test_interface_complex __________________________
test_module.py:8: in test_interface_complex
    assert 0
E   assert 0
____________________________ test_event_simple _____________________________
test_module.py:12: in test_event_simple
    assert 0
E   assert 0
========================= short test summary info ==========================
FAILED test_module.py::test_interface_simple - assert 0
FAILED test_module.py::test_interface_complex - assert 0
FAILED test_module.py::test_event_simple - assert 0
===================== 3 failed, 1 deselected in 0.12s ======================
```

--------------------------------

### Pytest XFAIL Marker Examples

Source: https://docs.pytest.org/en/stable/how-to/skipping

Demonstrates various ways to use the `pytest.mark.xfail` marker, including basic xfail, conditional xfail based on a string expression, xfail with a reason, and xfail based on a specific exception.

```python
from __future__ import annotations

import pytest


xfail = pytest.mark.xfail


@xfail
def test_hello():
    assert 0


@xfail(run=False)
def test_hello2():
    assert 0


@xfail("hasattr(os, 'sep')")
def test_hello3():
    assert 0


@xfail(reason="bug 110")
def test_hello4():
    assert 0


@xfail('pytest.__version__[0] != "17"')
def test_hello5():
    assert 0


def test_hello6():
    pytest.xfail("reason")


@xfail(raises=IndexError)
def test_hello7():
    x = []
    x[1] = 1

```

--------------------------------

### Listing Pytest Builtin Fixtures

Source: https://docs.pytest.org/en/stable/getting-started

Provides the command-line instruction to list all available builtin and custom fixtures in a Pytest project. Running `pytest --fixtures` will display these fixtures, aiding in understanding the testing environment and available resources. Note that fixtures starting with an underscore `_` are omitted unless the `-v` option is used.

```bash
pytest --fixtures
```

--------------------------------

### Get Pytest Invocation Directory with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

The `TerminalReporter_startdir` function returns the directory from which pytest was invoked. It returns a legacy `py.path.local` object, but `startpath` (a `pathlib.Path`) is preferred.

```python
def TerminalReporter_startdir(self: TerminalReporter) -> LEGACY_PATH:
    """The directory from which pytest was invoked.

    Prefer to use ``startpath`` which is a :class:`pathlib.Path`.

    :type: LEGACY_PATH
    """
    return legacy_path(self.startpath)
```

--------------------------------

### Pytest Autouse Fixture Example

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Demonstrates the use of an 'autouse' fixture in pytest. By setting `autouse=True` in the decorator, the fixture is automatically requested by all tests in the scope, eliminating the need for explicit requests.

```python
# contents of test_append.py
import pytest


# Arrange
@pytest.fixture(autouse=True)
def my_autouse_fixture():
    # This fixture will be executed for every test
    print("Executing autouse fixture")

def test_example_one():
    assert True

def test_example_two():
    assert True

```

--------------------------------

### Create directory with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Creates a directory with the given name within the test directory. The path to the created directory is returned as a legacy_path object.

```python
def mkdir(self, name) -> LEGACY_PATH:
    """See :meth:`Pytester.mkdir`."""
    return legacy_path(self._pytester.mkdir(name))
```

--------------------------------

### Getting All Registered Plugins in PytestPluginManager

Source: https://docs.pytest.org/en/stable/reference/reference

Returns a set containing all plugin objects that are currently registered with this plugin manager.

```python
def get_plugins(self):
    """Return a set of all registered plugin objects."""
    # Implementation details...
```

--------------------------------

### Pytest Mark Decorator Factory Initialization

Source: https://docs.pytest.org/en/stable/_modules/_pytest/mark/structures

Initializes the MarkGenerator, which acts as a factory for MarkDecorator objects. It includes internal checks and setup for marker configuration.

```python
class MarkGenerator:
    """Factory for :class:`MarkDecorator` objects - exposed as
    a ``pytest.mark`` singleton instance.

    Example::

         import pytest


         @pytest.mark.slowtest
         def test_function():
             pass

    applies a 'slowtest' :class:`Mark` on ``test_function``.
    """

    # See TYPE_CHECKING above.
    if TYPE_CHECKING:
        skip: _SkipMarkDecorator
        skipif: _SkipifMarkDecorator
        xfail: _XfailMarkDecorator
        parametrize: _ParametrizeMarkDecorator
        usefixtures: _UsefixturesMarkDecorator
        filterwarnings: _FilterwarningsMarkDecorator

    def __init__(self, *, _ispytest: bool = False) -> None:
        check_ispytest(_ispytest)
        self._config: Config | None = None
        self._markers: set[str] = set()

```

--------------------------------

### Initialize Testdir with Pytester Instance

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Initializes the Testdir class, which acts as a wrapper around Pytester to support legacy path objects. It requires an instance of Pytester and optionally a flag to ensure it's used within pytest.

```python
def __init__(self, pytester: Pytester, *, _ispytest: bool = False) -> None:
    check_ispytest(_ispytest)
    self._pytester = pytester
```

--------------------------------

### Get Terminal Writer

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Retrieves the TerminalWriter instance from the plugin manager, which is used for writing output to the console. Asserts that the 'terminalreporter' plugin is available.

```python
def get_terminal_writer(self) -> TerminalWriter:
    terminalreporter: TerminalReporter | None = self.pluginmanager.get_plugin(
        "terminalreporter"
    )
    assert terminalreporter is not None
    return terminalreporter._tw
```

--------------------------------

### Create Files with Legacy Path Conversion

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Creates files with a specified extension and content within the test directory. It handles potential issues with file extensions by prepending a dot if missing, ensuring compatibility with both pathlib and legacy path behaviors, and returns the created file path as a legacy_path object.

```python
def makefile(self, ext, *args, **kwargs) -> LEGACY_PATH:
    """See :meth:`Pytester.makefile`."""
    if ext and not ext.startswith("."):
        # pytester.makefile is going to throw a ValueError in a way that
        # testdir.makefile did not, because
        # pathlib.Path is stricter suffixes than py.path
        # This ext arguments is likely user error, but since testdir has
        # allowed this, we will prepend "" as a workaround to avoid breaking
        # testdir usage that worked before
        ext = "." + ext
    return legacy_path(self._pytester.makefile(ext, *args, **kwargs))
```

--------------------------------

### Pytest Configuration File (TOML)

Source: https://docs.pytest.org/en/stable/changelog

Example of a pytest configuration file using the TOML format. This file specifies minimum version, additional command-line options, and test directory paths.

```toml
[pytest]
minversion = "9.0"
addopts = ["-ra", "-q"]
testpaths = [
    "tests",
    "integration",
]

```

--------------------------------

### Implement a Type-Safe Heterogeneous Stash

Source: https://docs.pytest.org/en/stable/_modules/_pytest/stash

The Stash class provides a type-safe, heterogeneous mutable mapping. It allows storing and retrieving values associated with StashKey objects. This is useful for plugins or modules to store data without conflicts. It supports standard dictionary operations like setting, getting, deleting items, checking for containment, and getting the size.

```python
from typing import Any
from typing import cast
from typing import Generic
from typing import TypeVar

T = TypeVar("T")
D = TypeVar("D")



class StashKey(Generic[T]):
    """``StashKey`` is an object used as a key to a :class:`Stash`.

    A ``StashKey`` is associated with the type ``T`` of the value of the key.

    A ``StashKey`` is unique and cannot conflict with another key.

    .. versionadded:: 7.0
    """

    __slots__ = ()





class Stash:
    ""``Stash`` is a type-safe heterogeneous mutable mapping that
    allows keys and value types to be defined separately from
    where it (the ``Stash``) is created.

    Usually you will be given an object which has a ``Stash``, for example
    :class:`~pytest.Config` or a :class:`~_pytest.nodes.Node`:

    .. code-block:: python

        stash: Stash = some_object.stash

    If a module or plugin wants to store data in this ``Stash``, it creates
    :class:`StashKey`\s for its keys (at the module level):

    .. code-block:: python

        # At the top-level of the module
        some_str_key = StashKey[str]()
        some_bool_key = StashKey[bool]()

    To store information:

    .. code-block:: python

        # Value type must match the key.
        stash[some_str_key] = "value"
        stash[some_bool_key] = True

    To retrieve the information:

    .. code-block:: python

        # The static type of some_str is str.
        some_str = stash[some_str_key]
        # The static type of some_bool is bool.
        some_bool = stash[some_bool_key]

    .. versionadded:: 7.0
    """

    __slots__ = ("_storage",)

    def __init__(self) -> None:
        self._storage: dict[StashKey[Any], object] = {}



    def __setitem__(self, key: StashKey[T], value: T) -> None:
        """Set a value for key."""
        self._storage[key] = value





    def __getitem__(self, key: StashKey[T]) -> T:
        """Get the value for key.

        Raises ``KeyError`` if the key wasn't set before.
        """
        return cast(T, self._storage[key])





    def get(self, key: StashKey[T], default: D) -> T | D:
        """Get the value for key, or return default if the key wasn't set
        before."""
        try:
            return self[key]
        except KeyError:
            return default





    def setdefault(self, key: StashKey[T], default: T) -> T:
        """Return the value of key if already set, otherwise set the value
        of key to default and return default."""
        try:
            return self[key]
        except KeyError:
            self[key] = default
            return default





    def __delitem__(self, key: StashKey[T]) -> None:
        """Delete the value for key.

        Raises ``KeyError`` if the key wasn't set before.
        """
        del self._storage[key]





    def __contains__(self, key: StashKey[T]) -> bool:
        """Return whether key was set."""
        return key in self._storage





    def __len__(self) -> int:
        """Return how many items exist in the stash."""
        return len(self._storage)

```

--------------------------------

### Get Temporary Directory Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Provides access to the temporary directory path managed by Pytester. This path is used for creating files and running tests within an isolated environment.

```python
@property
def path(self) -> Path:
    """Temporary directory path used to create files/run tests from, etc."""
    return self._path
```

--------------------------------

### Create .ini Files with pytester.makeini

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `makeini` method creates a `.ini` file, typically used for configuration like `tox.ini`. It takes the file content as a string and returns the `Path` object for the created file.

```python
def makeini(self, source: str) -> Path:
    """Write a tox.ini file.

    :param source: The contents.
    :returns: The tox.ini file.
    """
    return self.makefile(".ini", tox=source)
```

--------------------------------

### Get Node File System Path with Legacy Path (Deprecated)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

The `Node_fspath` function returns a legacy `py.path.local` copy of the node's path. This attribute is deprecated.

```python
def Node_fspath(self: Node) -> LEGACY_PATH:
    """(deprecated) returns a legacy_path copy of self.path"""
    return legacy_path(self.path)
```

--------------------------------

### pytest_collection_finish

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

Called after collection has been performed and modified. This hook is typically used for final setup or reporting after all tests have been collected.

```APIDOC
## pytest_collection_finish

### Description
Called after collection has been performed and modified.

### Method
`hookspec`

### Endpoint
N/A (Hook)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```python
# Example usage in conftest.py
def pytest_collection_finish(session):
    print(f"Finished collecting {session.testscollected} items.")
```

### Response
#### Success Response (200)
None

#### Response Example
None
```

--------------------------------

### List Node Collection Chain (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

Returns a list of all parent collectors starting from the root of the collection tree down to and including the current node. This is useful for traversing the hierarchy.

```python
def listchain(self) -> list[Node]:
    """Return a list of all parent collectors starting from the root of the
    collection tree down to and including self."""
    chain = []
    item: Node | None = self
    while item is not None:
        chain.append(item)
        item = item.parent
    chain.reverse()
    return chain
```

--------------------------------

### Create Files with Specified Extension and Content

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

A private helper method to create files with a given extension and content within the Pytester's temporary directory. It handles encoding and ensures parent directories exist.

```python
def _makefile(
        self,
        ext: str,
        lines: Sequence[Any | bytes],
        files: dict[str, str],
        encoding: str = "utf-8",
    ) -> Path:
        items = list(files.items())

        if ext is None:
            raise TypeError("ext must not be None")

        if ext and not ext.startswith("."):
            raise ValueError(
                f"pytester.makefile expects a file extension, try .{ext} instead of {ext}"
            )

        def to_text(s: Any | bytes) -> str:
            return s.decode(encoding) if isinstance(s, bytes) else str(s)

        if lines:
            source = "\n".join(to_text(x) for x in lines)
            basename = self._name
            items.insert(0, (basename, source))

        ret = None
        for basename, value in items:
            p = self.path.joinpath(basename).with_suffix(ext)
            p.parent.mkdir(parents=True, exist_ok=True)
            source_ = Source(value)
            source = "\n".join(to_text(line) for line in source_.lines)
            p.write_text(source.strip(), encoding=encoding)
            if ret is None:
                ret = p
        assert ret is not None
        return ret
```

--------------------------------

### Pytest: Group Tests by Fixture Instances (Python)

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Demonstrates how pytest automatically groups tests based on fixture instances to minimize active resources. It shows the setup and teardown flow for module-scoped and function-scoped parametrized fixtures, illustrating efficient resource management.

```python
# content of test_module.py
import pytest


@pytest.fixture(scope="module", params=["mod1", "mod2"])
def modarg(request):
    param = request.param
    print("  SETUP modarg", param)
    yield param
    print("  TEARDOWN modarg", param)


@pytest.fixture(scope="function", params=[1, 2])
def otherarg(request):
    param = request.param
    print("  SETUP otherarg", param)
    yield param
    print("  TEARDOWN otherarg", param)


def test_0(otherarg):
    print("  RUN test0 with otherarg", otherarg)


def test_1(modarg):
    print("  RUN test1 with modarg", modarg)


def test_2(otherarg, modarg):
    print(f"  RUN test2 with otherarg {otherarg} and modarg {modarg}")

```

--------------------------------

### Create Python directory with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Creates a Python package directory (a directory containing an __init__.py file) with the specified name. The path to the created directory is returned as a legacy_path object.

```python
def mkpydir(self, name) -> LEGACY_PATH:
    """See :meth:`Pytester.mkpydir`."""
    return legacy_path(self._pytester.mkpydir(name))
```

--------------------------------

### addfinalizer Execution Order in Python

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Demonstrates the execution order of finalizers added using request.addfinalizer. This example shows that finalizers are executed in the reverse order they were added, adhering to a LIFO principle, similar to yield fixture teardowns.

```python
from functools import partial
import pytest


@pytest.fixture
def fix_w_finalizers(request):
    request.addfinalizer(partial(print, "finalizer_2"))
    request.addfinalizer(partial(print, "finalizer_1"))


def test_bar(fix_w_finalizers):
    print("test_bar")

```

--------------------------------

### pytest_runtest_protocol

Source: https://docs.pytest.org/en/stable/reference/reference

Perform the runtest protocol for a single test item. This hook orchestrates the setup, call, and teardown phases of test execution.

```APIDOC
## pytest_runtest_protocol

### Description
Perform the runtest protocol for a single test item. The default runtest protocol involves setup, call, and teardown phases, each invoking specific sub-hooks.

### Method
All runtest related hooks receive a `pytest.Item` object.

### Endpoint
N/A (Hook)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
N/A

### Response
#### Success Response (200)
- **item** (_Item_) – Test item for which the runtest protocol is performed.
- **nextitem** (_Item_ | _None_) – The scheduled-to-be-next test item (or None if this is the end).

#### Response Example
N/A
```

--------------------------------

### pytest_deselected

Source: https://docs.pytest.org/en/stable/reference/reference

This hook is called for test items that have been deselected, for example, due to keyword filtering.

```APIDOC
## POST /pytest_deselected

### Description
Called for deselected test items, such as those filtered out by keywords. This hook can be implemented to be notified of deselected items and must be called from `pytest_collection_modifyitems` when items are deselected.

### Method
POST

### Endpoint
/pytest_deselected

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **items** (_Sequence_[_Item_]) - Required - A sequence of deselected test items.

### Request Example
```json
{
  "items": [
    "<Item Object 1>",
    "<Item Object 2>"
  ]
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation that deselected items were processed.

#### Response Example
```json
{
  "message": "Deselected items processed."
}
```
```

--------------------------------

### Disable plugins with pytest

Source: https://docs.pytest.org/en/stable/how-to/usage

This command shows how to disable specific plugins during pytest invocation by using the '-p' option with the 'no:' prefix. The example disables the 'doctest' plugin.

```bash
pytest -p no:doctest
```

--------------------------------

### Clear Pytest Cache

Source: https://docs.pytest.org/en/stable/how-to/cache

Demonstrates how to clear all pytest cache files and values using the `--cache-clear` command-line option. This is recommended for CI environments to ensure test isolation and correctness by starting with a clean cache.

```bash
pytest --cache-clear

```

--------------------------------

### Get Item by Source

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Retrieves a specific test item from source code, optionally specifying the function name. It returns the Item. This is useful for directly obtaining a test item for further processing.

```python
def getitem(self, source, funcname="test_func"):
    """See :meth:`Pytester.getitem`."""
    return self._pytester.getitem(source, funcname)
```

--------------------------------

### Pytest Fixture: Requesting and Using Fixtures in Python

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Demonstrates how a test function requests a fixture by declaring it as an argument. Pytest finds the fixture, executes it, and passes its return value to the test function. This example uses a 'fruit_bowl' fixture to provide data for a 'test_fruit_salad' function.

```python
import pytest


class Fruit:
    def __init__(self, name):
        self.name = name
        self.cubed = False

    def cube(self):
        self.cubed = True


class FruitSalad:
    def __init__(self, *fruit_bowl):
        self.fruit = fruit_bowl
        self._cube_fruit()

    def _cube_fruit(self):
        for fruit in self.fruit:
            fruit.cube()


# Arrange
@pytest.fixture
def fruit_bowl():
    return [Fruit("apple"), Fruit("banana")]


def test_fruit_salad(fruit_bowl):
    # Act
    fruit_salad = FruitSalad(*fruit_bowl)

    # Assert
    assert all(fruit.cubed for fruit in fruit_salad.fruit)

```

--------------------------------

### Get Pytest Version String

Source: https://docs.pytest.org/en/stable/reference/reference

Retrieves the current pytest version as a string. This is useful for checking compatibility or displaying version information.

```python
import pytest
print(pytest.__version__)
```

--------------------------------

### Getting Registered Plugin Name in PytestPluginManager

Source: https://docs.pytest.org/en/stable/reference/reference

Returns the name under which a plugin is currently registered. If the plugin is not registered, it returns None.

```python
def get_name(self, _plugin_):
    """Return the name the plugin is registered under, or None if is isn’t."""
    # Implementation details...
```

--------------------------------

### Configure pytest command-line options with pytest.toml

Source: https://docs.pytest.org/en/stable/example/simple

This snippet demonstrates how to set default command-line options for pytest by creating a `pytest.toml` configuration file. It specifies options to show detailed information on skipped and xfailed tests (`-ra`) and use terse progress output (`-q`).

```toml
# content of pytest.toml
[pytest]
addopts = ["-ra", "-q"]

```

--------------------------------

### pytest.raises as Context Manager Returning ExceptionInfo

Source: https://docs.pytest.org/en/stable/_modules/_pytest/raises

This example demonstrates capturing the raised exception's details using pytest.raises as a context manager. The `as exc_info` clause assigns an `ExceptionInfo` object to the `exc_info` variable, allowing inspection of the exception type, value, and traceback.

```python
>>> with pytest.raises(ValueError) as exc_info:
...     raise ValueError("value must be 42")
>>> assert exc_info.type is ValueError
>>> assert exc_info.value.args[0] == "value must be 42"
```

--------------------------------

### Parametrizing Fixtures for Multiple Runs (pytest)

Source: https://docs.pytest.org/en/stable/how-to/fixtures

This example illustrates how to parametrize a fixture, causing dependent tests to run multiple times with different fixture configurations. The fixture function gains access to the parameter via the 'request' object, enabling dynamic test execution.

```python
import pytest


@pytest.fixture(params=[0, 1, 2])
def smtp_connection(request):
    # Fixture logic here, using request.param
    server = getattr(request.module, "smtpserver", "smtp.gmail.com")
    smtp_connection = smtplib.SMTP(server, 587, timeout=5)
    yield smtp_connection
    print(f"finalizing {smtp_connection} ({server})")
    smtp_connection.close()
```

--------------------------------

### Pytest Test Execution and Failure Report

Source: https://docs.pytest.org/en/stable/getting-started

Example output of running pytest on a test file that contains a failing assertion. It illustrates pytest's failure reporting, including assertion introspection.

```bash
$ pytest
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y
rootdir: /home/sweet/project
collected 1 item

test_sample.py F                                                     [100%]

================================= FAILURES =================================
_______________________________ test_answer ________________________________

    def test_answer():
>       assert func(3) == 5
E       assert 4 == 5
E        +  where 4 = func(3)

test_sample.py:6: AssertionError
========================= short test summary info ==========================
FAILED test_sample.py::test_answer - assert 4 == 5
============================ 1 failed in 0.12s =============================

```

--------------------------------

### Parse Hook Implementation Options (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Parses options for a hook implementation, ensuring the hook name starts with 'pytest_' and is not 'pytest_plugins'. It checks for legacy hook marks like 'tryfirst', 'trylast', 'optionalhook', and 'hookwrapper'.

```python
def parse_hookimpl_opts(
        self, plugin: _PluggyPlugin, name: str
    ) -> HookimplOpts | None:
        """:meta private:"""
        # pytest hooks are always prefixed with "pytest_",
        # so we avoid accessing possibly non-readable attributes
        # (see issue #1073).
        if not name.startswith("pytest_"):
            return None
        # Ignore names which cannot be hooks.
        if name == "pytest_plugins":
            return None

        opts = super().parse_hookimpl_opts(plugin, name)
        if opts is not None:
            return opts

        method = getattr(plugin, name)
        # Consider only actual functions for hooks (#3775).
        if not inspect.isroutine(method):
            return None
        # Collect unmarked hooks as long as they have the `pytest_' prefix.
        legacy = _get_legacy_hook_marks(
            method, "impl", ("tryfirst", "trylast", "optionalhook", "hookwrapper")
        )
        return cast(HookimplOpts, legacy)
```

--------------------------------

### Create Temporary Directory with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

The `mktemp` method creates a temporary directory. It mirrors the functionality of `TempPathFactory.mktemp` but returns a `py.path.local` object instead of a `pathlib.Path` object.

```python
def mktemp(self, basename: str, numbered: bool = True) -> LEGACY_PATH:
    """Same as :meth:`TempPathFactory.mktemp`, but returns a ``py.path.local`` object."""
    return legacy_path(self._tmppath_factory.mktemp(basename, numbered).resolve())
```

--------------------------------

### Perform Configuration

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Marks the configuration as complete and triggers the `pytest_configure` hook. This method should only be called once.

```python
def _do_configure(self) -> None:
    assert not self._configured
    self._configured = True
    self.hook.pytest_configure.call_historic(kwargs=dict(config=self))
```

--------------------------------

### Get Root Directory Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Retrieves the absolute path to the root directory of the Pytest project. This is typically the directory where pytest is invoked or where the configuration file is located.

```python
@property
def rootpath(self) -> pathlib.Path:
    """The path to the :ref:`rootdir <rootdir>`. 

    .. versionadded:: 6.1
    """
    return self._rootpath
```

--------------------------------

### Get Pytest Config File Path with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

The `Config_inifile` function returns the path to the pytest configuration file. It returns a legacy `py.path.local` object, but `inipath` (a `pathlib.Path`) is preferred.

```python
def Config_inifile(self: Config) -> LEGACY_PATH | None:
    """The path to the :ref:`configfile <configfiles>`.

    Prefer to use :attr:`inipath`, which is a :class:`pathlib.Path`.

    :type: Optional[LEGACY_PATH]
    """
    return legacy_path(str(self.inipath)) if self.inipath else None
```

--------------------------------

### Pytest Autouse Fixture Example

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Demonstrates an autouse fixture in pytest that automatically affects tests. The `append_first` fixture modifies the `order` list before each test runs, showcasing automatic fixture application.

```python
import pytest


@pytest.fixture
def first_entry():
    return "a"


@pytest.fixture
def order():
    return []


@pytest.fixture(autouse=True)
def append_first(order, first_entry):
    return order.append(first_entry)


def test_string_only(order, first_entry):
    assert order == [first_entry]


def test_string_and_int(order, first_entry):
    order.append(2)
    assert order == [first_entry, 2]
```

--------------------------------

### RaisesGroup Usage Examples

Source: https://docs.pytest.org/en/stable/reference/reference

Demonstrates various ways to use RaisesGroup as a context manager to assert expected exceptions, including matching specific exception types, message content, and handling nested exception groups.

```APIDOC
## RaisesGroup Context Manager Examples

### Description
Provides examples of using `RaisesGroup` to assert that specific exceptions are raised within a block of code. It covers basic exception matching, matching with specific message content, handling nested exception groups, and controlling subgroup flattening.

### Method
Context Manager (`with` statement)

### Endpoint
N/A (This is a Python construct, not a network endpoint)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```python
# Example 1: Basic ValueError and TypeError matching
with pytest.raises(ValueError, match="^my group$"):
    raise ExceptionGroup(
        "my group",
        [
            ValueError(),
            TypeError("expected int"),
            ValueError(),
        ],
    )

# Example 2: Matching with specific exception type and message content
with RaisesGroup(
    ValueError,
    ValueError,
    RaisesExc(TypeError, match="^expected int$"),
    match="^my group$",
):
    raise ExceptionGroup(
        "my group",
        [
            ValueError(),
            TypeError("expected int"),
            ValueError(),
        ],
    )

# Example 3: Handling nested exception groups
with RaisesGroup(RaisesGroup(ValueError)):
    raise ExceptionGroup("", (ExceptionGroup("", (ValueError(),)),))

# Example 4: Flattening subgroups
with RaisesGroup(ValueError, flatten_subgroups=True):
    raise ExceptionGroup("", (ExceptionGroup("", (ValueError(),)),))

# Example 5: Allowing unwrapped exceptions
with RaisesGroup(ValueError, allow_unwrapped=True):
    raise ValueError
```

### Response
#### Success Response (200)
N/A (This is a testing construct, not an API response)

#### Response Example
N/A
```

--------------------------------

### Get Closest Parent by Class (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

Finds and returns the closest ancestor node (including self) that is an instance of the specified class. Returns `None` if no such parent is found.

```python
def getparent(self, cls: type[_NodeType]) -> _NodeType | None:
    """Get the closest parent node (including self) which is an instance of
    the given class.

    :param cls: The node class to search for.
    :returns: The node, if found.
    """
    for node in self.iter_parents():
        if isinstance(node, cls):
            return node
    return None
```

--------------------------------

### Spawn Process

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Spawns a general process using pexpect and returns the spawn object. It takes a command string and an optional timeout. This is useful for interacting with any command-line process.

```python
def spawn(self, cmd: str, expect_timeout: float = 10.0) -> pexpect.spawn:
    """See :meth:`Pytester.spawn`."""
    return self._pytester.spawn(cmd, expect_timeout=expect_timeout)
```

--------------------------------

### Get Pytest Plugin by Name (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Retrieves a registered plugin by its name. This method supports deprecated plugin naming conventions to maintain backward compatibility with older plugins.

```python
def getplugin(self, name: str):
        # Support deprecated naming because plugins (xdist e.g.) use it.
        plugin: _PluggyPlugin | None = self.get_plugin(name)
        return plugin
```

--------------------------------

### Handle Strict Parametrization IDs Example (Python)

Source: https://docs.pytest.org/en/stable/reference/reference

Demonstrates how strict_parametrization_ids causes an error with duplicate IDs and how to fix it by explicitly assigning unique IDs using the 'ids' argument in pytest.mark.parametrize.

```python
import pytest


@pytest.mark.parametrize("letter", ["a", "a"])
def test_letter_is_ascii(letter):
    assert letter.isascii()

@pytest.mark.parametrize("letter", ["a", "a"], ids=["a0", "a1"])
def test_letter_is_ascii_fixed(letter):
    assert letter.isascii()

```

--------------------------------

### Commit and Push Changes (Git)

Source: https://docs.pytest.org/en/stable/contributing

This snippet shows the standard Git commands for committing your changes with a message and then pushing them to the remote repository.

```bash
$ git commit -a -m "<commit message>"
$ git push -u
```

--------------------------------

### Filter Public Names from Iterable

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

A utility function to filter out names that start with an underscore from an iterable of strings. It returns a new list containing only the public names.

```python
from typing import Iterable

def get_public_names(values: Iterable[str]) -> list[str]:
    """Only return names from iterator values without a leading underscore."""
    return [x for x in values if x[0] != "_"]
```

--------------------------------

### Email Sending and Receiving Fixture (Python)

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Sets up an email sending and receiving scenario using emaillib. It creates users, sends an email, and yields the receiving user and email for testing. Includes teardown to clear the mailbox and delete users.

```python
from emaillib import Email, MailAdminClient

import pytest


@pytest.fixture
def setup():
    mail_admin = MailAdminClient()
    sending_user = mail_admin.create_user()
    receiving_user = mail_admin.create_user()
    email = Email(subject="Hey!", body="How's it going?")
    sending_user.send_email(email, receiving_user)
    yield receiving_user, email
    receiving_user.clear_mailbox()
    mail_admin.delete_user(sending_user)
    mail_admin.delete_user(receiving_user)


def test_email_received(setup):
    receiving_user, email = setup
    assert email in receiving_user.inbox
```

--------------------------------

### Pytest Set Comparison Failure Example

Source: https://docs.pytest.org/en/stable/how-to/assert

Demonstrates a failed set comparison in a pytest test. The output shows the specific elements that differ between the two sets, highlighting pytest's detailed failure reporting for collections.

```python
def test_set_comparison():
    set1 = set("1308")
    set2 = set("8035")
    assert set1 == set2
```

--------------------------------

### Get Pytest Invocation Directory (Config) with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

The `Config_invocation_dir` function returns the directory from which pytest was invoked. It returns a legacy `py.path.local` object, but `invocation_params.dir` (a `pathlib.Path`) is preferred.

```python
def Config_invocation_dir(self: Config) -> LEGACY_PATH:
    """The directory from which pytest was invoked.

    Prefer to use :attr:`invocation_params.dir <InvocationParams.dir>`,
    which is a :class:`pathlib.Path`.

    :type: LEGACY_PATH
    """
    return legacy_path(str(self.invocation_params.dir))
```

--------------------------------

### Get the number of recorded warnings

Source: https://docs.pytest.org/en/stable/reference/reference

Returns the total count of warnings that have been recorded. This provides a quick way to check how many warnings were captured.

```python
__len__()
```

--------------------------------

### Get Node by Config and Argument

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Fetches a pytest node (item or collector) using configuration and an argument. It returns the node or None. This method is helpful for programmatically accessing collected test items.

```python
def getnode(self, config: Config, arg) -> Item | Collector | None:
    """See :meth:`Pytester.getnode`."""
    return self._pytester.getnode(config, arg)
```

--------------------------------

### Config.inifile

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Returns the path to the pytest configuration file, as a legacy path object.

```APIDOC
## GET /config/inifile

### Description
Returns the path to the pytest :ref:`configfile <configfiles>`. It is recommended to use :attr:`inipath`, which provides a ``pathlib.Path`` object instead. Returns None if no configuration file is found.

### Method
GET

### Endpoint
/config/inifile

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **inifile** (Optional[LEGACY_PATH]) - The legacy path object of the configuration file, or None.

#### Response Example
```json
{
  "inifile": "/path/to/pytest.ini"
}
```
```

--------------------------------

### TestReport Class Initialization and Attributes (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/reports

This snippet details the initialization of the TestReport class in Python, outlining its various attributes such as nodeid, location, keywords, outcome, longrepr, when, sections, duration, start, and stop. It also includes user properties and extra attributes.

```python
def __init__(self,
        nodeid: str,
        location: tuple[str, int | None, str],
        keywords: Mapping[str, Any],
        outcome: Literal["passed", "failed", "skipped"],
        longrepr: (None | ExceptionInfo[BaseException] | tuple[str, int, str] | str | TerminalRepr),
        when: Literal["setup", "call", "teardown"],
        sections: Iterable[tuple[str, str]] = (),
        duration: float = 0,
        start: float = 0,
        stop: float = 0,
        user_properties: Iterable[tuple[str, object]] | None = None,
        **extra,
    ) -> None:
        #: Normalized collection nodeid.
        self.nodeid = nodeid

        #: A (filesystempath, lineno, domaininfo) tuple indicating the
        #: actual location of a test item - it might be different from the
        #: collected one e.g. if a method is inherited from a different module.
        #: The filesystempath may be relative to ``config.rootdir``.
        #: The line number is 0-based.
        self.location: tuple[str, int | None, str] = location

        #: A name -> value dictionary containing all keywords and
        #: markers associated with a test invocation.
        self.keywords: Mapping[str, Any] = keywords

        #: Test outcome, always one of "passed", "failed", "skipped".
        self.outcome = outcome

        #: None or a failure representation.
        self.longrepr = longrepr

        #: One of 'setup', 'call', 'teardown' to indicate runtest phase.
        self.when: Literal["setup", "call", "teardown"] = when

        #: User properties is a list of tuples (name, value) that holds user
        #: defined properties of the test.
        self.user_properties = list(user_properties or [])

        #: Tuples of str ``(heading, content)`` with extra information
        #: for the test report. Used by pytest to add text captured
        #: from ``stdout``, ``stderr``, and intercepted logging events. May
        #: be used by other plugins to add arbitrary information to reports.
        self.sections = list(sections)

        #: Time it took to run just the test.
        self.duration: float = duration

        #: The system time when the call started, in seconds since the epoch.
        self.start: float = start
        #: The system time when the call ended, in seconds since the epoch.
        self.stop: float = stop

        self.__dict__.update(extra)

    def __repr__(self) -> str:
        return f"<{self.__class__.__name__} {self.nodeid!r} when={self.when!r} outcome={self.outcome!r}>"
```

--------------------------------

### Get Pytest Root Directory with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

The `Config_rootdir` function returns the path to the pytest root directory. It returns a legacy `py.path.local` object, but `rootpath` (a `pathlib.Path`) is preferred.

```python
def Config_rootdir(self: Config) -> LEGACY_PATH:
    """The path to the :ref:`rootdir <rootdir>`.

    Prefer to use :attr:`rootpath`, which is a :class:`pathlib.Path`.

    :type: LEGACY_PATH
    """
    return legacy_path(str(self.rootpath))
```

--------------------------------

### Pytest Header Reporting Hook

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

Implements the `pytest_report_header` hook to provide information about the test session, including the root directory, configuration file path, test paths, and installed plugins.

```python
def pytest_report_header(self, config: Config) -> list[str]:
    result = [f"rootdir: {config.rootpath}"]

    if config.inipath:
        warning = ""
        if config._ignored_config_files:
            warning = f" (WARNING: ignoring pytest config in {', '.join(config._ignored_config_files)}!)"
        result.append(
            "configfile: " + bestrelpath(config.rootpath, config.inipath) + warning
        )

    if config.args_source == Config.ArgsSource.TESTPATHS:
        testpaths: list[str] = config.getini("testpaths")
        result.append("testpaths: {}".format(", ".join(testpaths)))

    plugininfo = config.pluginmanager.list_plugin_distinfo()
    if plugininfo:
        result.append(
            "plugins: {}".format(", ".join(_plugin_nameversions(plugininfo)))
        )
    return result
```

--------------------------------

### Node Factory Method

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

Provides a class method `from_parent` for creating Node instances, abstracting away complex initialization logic.

```APIDOC
## from_parent Node Factory

### Description
A public constructor for Nodes that allows creation of Node instances using a parent node, abstracting away the fragile logic from the direct constructors. Subclasses can use `super().from_parent(...)`.

### Method
`from_parent` (classmethod)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **parent** (Node) - Required - The parent node of this Node.
- ****kw** - Additional keyword arguments to pass to the Node constructor.

### Request Example
```json
{
  "parent": { ... Node object ... },
  "name": "child_node"
}
```

### Response
#### Success Response (200)
- **Node** (Node) - A newly created Node instance.

#### Response Example
```json
{
  "__class__": "Node",
  "name": "child_node",
  "nodeid": "parent_node_id::child_node"
}
```
```

--------------------------------

### Get Pytest Version Tuple

Source: https://docs.pytest.org/en/stable/reference/reference

Retrieves the current pytest version as a tuple of integers and strings. This allows for programmatic comparison of version numbers.

```python
import pytest
print(pytest.version_tuple)
```

--------------------------------

### Using pytest.yield_fixture for Context Managers

Source: https://docs.pytest.org/en/stable/announce/release-2.4.0

Introduces the experimental `pytest.yield_fixture` decorator, which allows fixtures to use `yield` for setup and teardown, enabling direct integration with 'with-style' context managers. This is an alternative to `pytest.fixture` when generator-like behavior is needed.

```python
import pytest

@pytest.yield_fixture
def my_fixture():
    # Setup code
    resource = setup_resource()
    yield resource
    # Teardown code
    teardown_resource(resource)
```

--------------------------------

### Generate JUnit XML Reports (Command Line)

Source: https://docs.pytest.org/en/stable/how-to/output

Generate JUnit XML format files for compatibility with CI/CD servers like Jenkins. This is achieved using the --junit-xml command-line option, specifying the output path.

```bash
pytest --junit-xml=path

```

--------------------------------

### Jenkins XML Schema for Testcase

Source: https://docs.pytest.org/en/stable/how-to/output

An example XML schema definition (XSD) used by Jenkins to validate incoming JUnit XML reports. It defines the structure and allowed attributes for the 'testcase' element.

```xml
<xs:element name="testcase">
    <xs:complexType>
        <xs:sequence>
            <xs:element ref="skipped" minOccurs="0" maxOccurs="1"/>
            <xs:element ref="error" minOccurs="0" maxOccurs="unbounded"/>
            <xs:element ref="failure" minOccurs="0" maxOccurs="unbounded"/>
            <xs:element ref="system-out" minOccurs="0" maxOccurs="unbounded"/>
            <xs:element ref="system-err" minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="name" type="xs:string" use="required"/>
        <xs:attribute name="assertions" type="xs:string" use="optional"/>
        <xs:attribute name="time" type="xs:string" use="optional"/>
        <xs:attribute name="classname" type="xs:string" use="optional"/>
        <xs:attribute name="status" type="xs:string" use="optional"/>
    </xs:complexType>
</xs:element>
```

--------------------------------

### Test Plugin Fixture with Pytester

Source: https://docs.pytest.org/en/stable/how-to/writing_plugins

Tests a custom pytest fixture 'hello' using the 'pytester' fixture. It creates temporary conftest.py and test files, runs pytest, and asserts the test outcomes.

```python
def test_hello(pytester):
    """Make sure that our plugin works."""

    # create a temporary conftest.py file
    pytester.makeconftest(
        """
        import pytest

        @pytest.fixture(params=[
            "Brianna",
            "Andreas",
            "Floris",
        ])
        def name(request):
            return request.param
    """
    )

    # create a temporary pytest test file
    pytester.makepyfile(
        """
        def test_hello_default(hello):
            assert hello() == "Hello World!"

        def test_hello_name(hello, name):
            assert hello(name) == "Hello {0}!".format(name)
    """
    )

    # run all tests with pytest
    result = pytester.runpytest()

    # check that all 4 tests passed
    result.assert_outcomes(passed=4)
```

--------------------------------

### Getting a Registered Plugin by Name in PytestPluginManager

Source: https://docs.pytest.org/en/stable/reference/reference

Retrieves a plugin object registered under a specific name. Returns the plugin if found, otherwise returns None.

```python
def get_plugin(self, _name_):
    """Return the plugin registered under the given name, if any."""
    # Implementation details...
```

--------------------------------

### Get Lines Following a Specific Line

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Retrieves all lines that appear in the output after a specified line. The specified line can include glob wildcards for flexible matching. Raises ValueError if the specified line is not found.

```python
def get_lines_after(self, fnline: str) -> Sequence[str]:
    """Return all lines following the given line in the text.

    The given line can contain glob wildcards.
    """
    for i, line in enumerate(self.lines):
        if fnline == line or fnmatch(line, fnline):
            return self.lines[i + 1 :]
    raise ValueError(f"line {fnline!r} not found in output")
```

--------------------------------

### Considering Pre-parse Arguments in Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

This method processes command-line arguments during the pre-parsing phase to identify and consider plugins. It specifically looks for the '-p' option and arguments starting with '-p' to determine which plugins to load or exclude.

```python
def consider_preparse(
        self, args: Sequence[str], *, exclude_only: bool = False
    ) -> None:
        """:meta private:"""
        i = 0
        n = len(args)
        while i < n:
            opt = args[i]
            i += 1
            if isinstance(opt, str):
                if opt == "-p":
                    try:
                        parg = args[i]
                    except IndexError:
                        return
                    i += 1
                elif opt.startswith("-p"):
                    parg = opt[2:]
                else:
                    continue
                parg = parg.strip()
                if exclude_only and not parg.startswith("no:"):
                    continue
                self.consider_pluginarg(parg)
```

--------------------------------

### Pytest: Asserting Dictionary Equality with Verbosity

Source: https://docs.pytest.org/en/stable/how-to/output

This example shows a failing assertion between two dictionaries in pytest. Verbose output includes common items, items unique to each dictionary, and a text-based diff highlighting the differences.

```python
def test_numbers_fail():
    number_to_text1 = {str(x): x for x in range(5)}
    number_to_text2 = {str(x * 10): x * 10 for x in range(5)}
    assert number_to_text1 == number_to_text2
```

--------------------------------

### Pytest Session Start Hook

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

The `pytest_sessionstart` hook is executed after the `Session` object has been initialized and before the test collection process begins. It's called only for initial conftest files and is suitable for setting up global configurations or state for the entire test session.

```python
from _pytest.main import Session


def pytest_sessionstart(session: Session) -> None:
    """Called after the ``Session`` object has been created and before performing collection
    and entering the run test loop.

    :param session: The pytest session object.

    Use in conftest plugins
    =======================

    This hook is only called for :ref:`initial conftests <pluginorder>`.
    """
    pass
```

--------------------------------

### Pytest Fixture Finalization with Parametrized Arguments

Source: https://docs.pytest.org/en/stable/announce/release-2.5.0

This change simplifies and fixes the implementation for calling finalizers when parametrized fixtures or function arguments are involved. Finalization is now lazy and occurs at setup time.

```python
import pytest

@pytest.fixture(params=[1, 2, 3])
def my_fixture(request):
    return request.param

def test_with_fixture(my_fixture):
    assert my_fixture is not None
```

--------------------------------

### Pytest Configuration in pytest.toml

Source: https://docs.pytest.org/en/stable/reference/customize

Example of configuring pytest using a pytest.toml file. This format takes precedence and allows specifying minimum version, additional options, and test paths. Supports native TOML types.

```toml
# pytest.toml or .pytest.toml
[pytest]
minversion = "9.0"
addopts = ["-ra", "-q"]
testpaths = [
    "tests",
    "integration",
]
```

--------------------------------

### TerminalReporter.startdir

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Returns the directory from which pytest was invoked, as a legacy path object.

```APIDOC
## GET /terminal_reporter/startdir

### Description
Returns the directory from which pytest was invoked. It is recommended to use ``startpath`` which provides a ``pathlib.Path`` object instead.

### Method
GET

### Endpoint
/terminal_reporter/startdir

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **startdir** (LEGACY_PATH) - The legacy path object of the invocation directory.

#### Response Example
```json
{
  "startdir": "/path/where/pytest/was/invoked"
}
```
```

--------------------------------

### Apply Pytest Marker to Individual Test Instance with Parametrize

Source: https://docs.pytest.org/en/stable/example/markers

Illustrates how to apply markers to specific instances of a parameterized test using `pytest.param`. This allows for fine-grained control over which parameterized test runs receive certain marks, such as 'bar' in this example.

```python
import pytest

@pytest.mark.foo
@pytest.mark.parametrize(
    ("n", "expected"), [(1, 2), pytest.param(1, 3, marks=pytest.mark.bar), (2, 3)]
)
def test_increment(n, expected):
    assert n + 1 == expected
```

--------------------------------

### Calculate Fixture Closure and Mapping

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

Collects the closure of all fixtures starting from initial names, ignoring specified arguments. It also returns a mapping of argument names to their corresponding FixtureDefs.

```python
def getfixtureclosure(
    self,
    parentnode: nodes.Node,
    initialnames: tuple[str, ...],
    ignore_args: AbstractSet[str],
) -> tuple[list[str], dict[str, Sequence[FixtureDef[Any]]]]:
    # Collect the closure of all fixtures, starting with the given
    # fixturenames as the initial set.  As we have to visit all
    # factory definitions anyway, we also return an arg2fixturedefs
    # mapping so that the caller can reuse it and does not have
    # to re-discover fixturedefs again for each fixturename
    # (discovering matching fixtures for a given name/node is expensive).

    fixturenames_closure = list(initialnames)

    arg2fixturedefs: dict[str, Sequence[FixtureDef[Any]]] = {}

    # Track the index for each fixture name in the simulated stack.
    # Needed for handling override chains correctly, similar to _get_active_fixturedef.
```

--------------------------------

### Create Directories with pytester.mkdir

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `mkdir` method creates a new directory (or subdirectory) relative to the pytester's root path. It returns the `Path` object of the created directory.

```python
def mkdir(self, name: str | os.PathLike[str]) -> Path:
    """Create a new (sub)directory.

    :param name:
        The name of the directory, relative to the pytester path.
    :returns:
        The created directory.
    :rtype: pathlib.Path
    """
    p = self.path / name
    p.mkdir()
    return p
```

--------------------------------

### Pytest Fixture Instantiation Order by Scope

Source: https://docs.pytest.org/en/stable/reference/fixtures

Demonstrates how pytest executes fixtures based on their scope, with higher-scoped fixtures running before lower-scoped ones. This example defines fixtures with different scopes (session, package, module, class, function) and asserts the correct execution order within a test.

```python
from __future__ import annotations

import pytest


@pytest.fixture(scope="session")
def order():
    return []


@pytest.fixture
def func(order):
    order.append("function")


@pytest.fixture(scope="class")
def cls(order):
    order.append("class")


@pytest.fixture(scope="module")
def mod(order):
    order.append("module")


@pytest.fixture(scope="package")
def pack(order):
    order.append("package")


@pytest.fixture(scope="session")
def sess(order):
    order.append("session")


class TestClass:
    def test_order(self, func, cls, mod, pack, sess, order):
        assert order == ["session", "package", "module", "class", "function"]
```

--------------------------------

### Selecting Tests by Marker in pytest Command Line

Source: https://docs.pytest.org/en/stable/example/markers

Illustrates how to use the `pytest -m` command-line option to select tests based on custom markers. Examples show running only tests marked with 'webtest', running all tests except 'webtest', and running tests matching specific marker arguments like `device(serial='123')`.

```bash
$ pytest -v -m webtest
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y -- $PYTHON_PREFIX/bin/python
cachedir: .pytest_cache
rootdir: /home/sweet/project
collecting ... collected 4 items / 3 deselected / 1 selected

test_server.py::test_send_http PASSED                                [100%]

===================== 1 passed, 3 deselected in 0.12s ======================

```

```bash
$ pytest -v -m "not webtest"
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y -- $PYTHON_PREFIX/bin/python
cachedir: .pytest_cache
rootdir: /home/sweet/project
collecting ... collected 4 items / 1 deselected / 3 selected

test_server.py::test_something_quick PASSED                          [ 33%]
test_server.py::test_another PASSED                                  [ 66%]
test_server.py::TestClass::test_method PASSED                        [100%]

===================== 3 passed, 1 deselected in 0.12s ======================

```

```bash
$ pytest -v -m "device(serial='123')"
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y -- $PYTHON_PREFIX/bin/python
cachedir: .pytest_cache
rootdir: /home/sweet/project
collecting ... collected 4 items / 3 deselected / 1 selected

test_server.py::test_something_quick PASSED                          [100%]

===================== 1 passed, 3 deselected in 0.12s ======================

```

--------------------------------

### Run All Tests and Linting with Tox (Bash)

Source: https://docs.pytest.org/en/stable/contributing

This snippet shows how to execute all tests and linting checks using tox against your default Python version. It also covers running tests on a specific Python version (e.g., 3.13) and passing arguments to pytest.

```bash
$ tox -e linting,py
$ tox -e py313 -- --pdb
$ tox -e py312 -- testing/test_config.py
```

--------------------------------

### Upgrade pytest using pip

Source: https://docs.pytest.org/en/stable/announce/release-3.2.4

This command upgrades the pytest package to the latest version using pip, the Python package installer. It's a straightforward command-line operation.

```bash
pip install --upgrade pytest

```

--------------------------------

### Pytest Node Parent Iteration

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

Iterates over all parent collectors starting from and including the current node up to the root of the collection tree. This method was added in version 8.1.

```python
def iter_parents(self) -> Iterator[Node]:
    """Iterate over all parent collectors starting from and including self
    up to the root of the collection tree.

    .. versionadded:: 8.1
    """
    parent: Node | None = self
    while parent is not None:

```

--------------------------------

### Create ini file with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Creates an ini configuration file (e.g., pytest.ini) with the given source content. The path to the created file is returned as a legacy_path object.

```python
def makeini(self, source) -> LEGACY_PATH:
    """See :meth:`Pytester.makeini`."""
    return legacy_path(self._pytester.makeini(source))
```

--------------------------------

### TeeCaptureIO Class for Tying Output

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

TeeCaptureIO inherits from CaptureIO and adds the functionality to write captured output to another specified text stream (other) in addition to capturing it internally. This allows for both capturing and displaying output simultaneously.

```python
class TeeCaptureIO(CaptureIO):
    def __init__(self, other: TextIO) -> None:
        self._other = other
        super().__init__()

    def write(self, s: str) -> int:
        super().write(s)
        return self._other.write(s)
```

--------------------------------

### Getting Collection Node with Configured Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Obtains the collection node for a file path by first configuring Pytest using `parseconfigure`. This method is similar to `getnode` but ensures the Pytest configuration is applied before collection.

```python
def getpathnode(self, path: str | os.PathLike[str]) -> Collector | Item:
    """Return the collection node of a file.

    This is like :py:meth:`getnode` but uses :py:meth:`parseconfigure` to
    create the (configured) pytest Config instance.

    :param path:
        Path to the file.
    :returns:
        The node.
    """
    path = Path(path)
    config = self.parseconfigure(path)
    session = Session.from_config(config)
    x = bestrelpath(session.path, path)
    config.hook.pytest_sessionstart(session=session)
    res = session.perform_collect([x], genitems=False)[0]
    config.hook.pytest_sessionfinish(session=session, exitstatus=ExitCode.OK)
    return res

```

--------------------------------

### Handle Test Collection Start with pytest_collectstart Hook (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/main

Implements the `pytest_collectstart` hook to handle the beginning of the collection process. It checks the `shouldfail` and `shouldstop` properties and raises appropriate exceptions (`self.Failed` or `self.Interrupted`) if they are set.

```python
    @hookimpl(tryfirst=True)
    def pytest_collectstart(self) -> None:
        if self.shouldfail:
            raise self.Failed(self.shouldfail)
        if self.shouldstop:
            raise self.Interrupted(self.shouldstop)
```

--------------------------------

### Get Failure Headline in Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

The `_getfailureheadline` method retrieves the headline for a test failure report. It prioritizes the `head_line` attribute of the report, falling back to 'test session' if unavailable.

```python
    def _getfailureheadline(self, rep):
        head_line = rep.head_line
        if head_line:
            return head_line
        return "test session"  # XXX?
```

--------------------------------

### Running Pytest with Session Fixture and Output (Shell)

Source: https://docs.pytest.org/en/stable/example/special

This command demonstrates how to run pytest with specific options: `-q` for quiet output and `-s` to disable output capturing, allowing print statements to be displayed. It targets a specific test file, `test_module.py`, and shows the expected output when the session fixture and test classes with `callme` methods are used.

```shell
$ pytest -q -s test_module.py
callattr_ahead_of_alltests called
callme called!
callme other called
SomeTest callme called
test_method1 called
.test_method2 called
.test other
.test_unit1 method called
.
4 passed in 0.12s

```

--------------------------------

### Demonstrate Pytest Fixture Error Handling

Source: https://docs.pytest.org/en/stable/explanation/fixtures

This example illustrates how pytest stops executing fixtures for a test if an earlier fixture raises an exception. It shows the order of fixture execution and how errors in one fixture prevent subsequent fixtures and the test itself from running.

```python
import pytest


@pytest.fixture
def order():
    return []


@pytest.fixture
def append_first(order):
    order.append(1)


@pytest.fixture
def append_second(order, append_first):
    order.extend([2])


@pytest.fixture(autouse=True)
def append_third(order, append_second):
    order += [3]


def test_order(order):
    assert order == [1, 2, 3]

```

--------------------------------

### Pytest Configuration Initialization

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Function to create and initialize a Pytest configuration object. It sets up the plugin manager, processes command-line arguments, and loads default plugins.

```python
def get_config(
    args: Iterable[str] | None = None,
    plugins: Sequence[str | _PluggyPlugin] | None = None,
) -> Config:
    # Subsequent calls to main will create a fresh instance.
    pluginmanager = PytestPluginManager()
    invocation_params = Config.InvocationParams(
        args=args or (),
        plugins=plugins,
        dir=pathlib.Path.cwd(),
    )
    config = Config(pluginmanager, invocation_params=invocation_params)

    if invocation_params.args:
        # Handle any "-p no:plugin" args.
        pluginmanager.consider_preparse(invocation_params.args, exclude_only=True)

    for spec in default_plugins:
        pluginmanager.import_plugin(spec)

    return config
```

--------------------------------

### Get lines following a specific line

Source: https://docs.pytest.org/en/stable/reference/reference

Retrieves all lines that appear after a given line in the text. The specified line can include glob wildcards for flexible matching.

```python
get_lines_after(_fnline_)
```

--------------------------------

### Pytest Fixture Parametrization with Marks

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Shows how to use `pytest.param()` within a parametrized fixture to apply marks, such as `pytest.mark.skip`, to specific parameter values. This allows selective skipping or marking of test runs based on fixture parameters.

```python
import pytest


@pytest.fixture(params=[0, 1, pytest.param(2, marks=pytest.mark.skip)])
def data_set(request):
    return request.param


def test_data(data_set):
    pass
```

--------------------------------

### Factory Function for MultiCapture Initialization

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Provides a factory function `_get_multicapture` to create `MultiCapture` instances based on a specified capture method ('fd', 'sys', 'no', 'tee-sys'). This simplifies the instantiation process for different capture configurations.

```python
def _get_multicapture(method: _CaptureMethod) -> MultiCapture[str]:
    if method == "fd":
        return MultiCapture(in_=FDCapture(0), out=FDCapture(1), err=FDCapture(2))
    elif method == "sys":
        return MultiCapture(in_=SysCapture(0), out=SysCapture(1), err=SysCapture(2))
    elif method == "no":
        return MultiCapture(in_=None, out=None, err=None)
    elif method == "tee-sys":
        return MultiCapture(
            in_=None, out=SysCapture(1, tee=True), err=SysCapture(2, tee=True)
        )
    raise ValueError(f"unknown capturing method: {method!r}")

```

--------------------------------

### Get a recorded warning by index

Source: https://docs.pytest.org/en/stable/reference/reference

Retrieves a specific recorded warning from the list using its index. This allows direct access to individual warnings based on their position.

```python
__getitem__(_i_)
```

--------------------------------

### Pytest Item Initialization and Inheritance Check

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

Demonstrates the initialization of a Pytest Item, including setting its name, parent, configuration, session, and node ID. It also includes a check for diamond inheritance issues between Item and Collector subclasses, emitting a warning if detected.

```python
class Item(Node, abc.ABC):
    """Base class of all test invocation items.

    Note that for a single function there might be multiple test invocation items.
    """

    nextitem = None

    def __init__(
        self,
        name,
        parent=None,
        config: Config | None = None,
        session: Session | None = None,
        nodeid: str | None = None,
        **kw,
    ) -> None:
        # The first two arguments are intentionally passed positionally,
        # to keep plugins who define a node type which inherits from
        # (pytest.Item, pytest.File) working (see issue #8435).
        # They can be made kwargs when the deprecation above is done.
        super().__init__(
            name,
            parent,
            config=config,
            session=session,
            nodeid=nodeid,
            **kw,
        )
        self._report_sections: list[tuple[str, str, str]] = []

        #: A list of tuples (name, value) that holds user defined properties
        #: for this test.
        self.user_properties: list[tuple[str, object]] = []

        self._check_item_and_collector_diamond_inheritance()

    def _check_item_and_collector_diamond_inheritance(self) -> None:
        """
        Check if the current type inherits from both File and Collector
        at the same time, emitting a warning accordingly (#8447).
        """
        cls = type(self)

        # We inject an attribute in the type to avoid issuing this warning
        # for the same class more than once, which is not helpful.
        # It is a hack, but was deemed acceptable in order to avoid
        # flooding the user in the common case.
        attr_name = "_pytest_diamond_inheritance_warning_shown"
        if getattr(cls, attr_name, False):
            return
        setattr(cls, attr_name, True)

        problems = ", ".join(
            base.__name__ for base in cls.__bases__ if issubclass(base, Collector)
        )
        if problems:
            warnings.warn(
                f"{cls.__name__} is an Item subclass and should not be a collector, "
                f"however its bases {problems} are collectors.\n"
                "Please split the Collectors and the Item into separate node types.\n"
                "Pytest Doc example: https://docs.pytest.org/en/latest/example/nonpython.html\n"
                "example pull request on a plugin: https://github.com/asmeurer/pytest-flakes/pull/40/",
                PytestWarning,
            )

```

--------------------------------

### Pytest Configuration in tox.ini

Source: https://docs.pytest.org/en/stable/reference/customize

Example of configuring pytest within a tox.ini file. Pytest configuration can be included in a [pytest] section, allowing specification of minimum version, additional options, and test paths.

```ini
# tox.ini
[pytest]
minversion = 6.0
addopts = -ra -q
testpaths =
    tests
    integration
```

--------------------------------

### CaptureManager: Global Capturing Control (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Manages global output capturing. Includes methods to start, stop, resume, suspend, and read captured output. It ensures that global capture is handled correctly during test collection and execution phases.

```python
class CaptureManager:
    # ... (init and other methods)

    def is_globally_capturing(self) -> bool:
        return self._method != "no"

    def start_global_capturing(self) -> None:
        assert self._global_capturing is None
        self._global_capturing = _get_multicapture(self._method)
        self._global_capturing.start_capturing()

    def stop_global_capturing(self) -> None:
        if self._global_capturing is not None:
            self._global_capturing.pop_outerr_to_orig()
            self._global_capturing.stop_capturing()
            self._global_capturing = None

    def resume_global_capture(self) -> None:
        if self._global_capturing is not None:
            self._global_capturing.resume_capturing()

    def suspend_global_capture(self, in_: bool = False) -> None:
        if self._global_capturing is not None:
            self._global_capturing.suspend_capturing(in_=in_)

    def read_global_capture(self) -> CaptureResult[str]:
        assert self._global_capturing is not None
        return self._global_capturing.readouterr()
```

--------------------------------

### Get Test Module File Path with Legacy Path (Deprecated)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

The `FixtureRequest_fspath` function returns the file system path of the test module that collected the test. This is a deprecated attribute and returns a legacy `py.path.local` object.

```python
def FixtureRequest_fspath(self: FixtureRequest) -> LEGACY_PATH:
    """(deprecated) The file system path of the test module which collected this test."""
    return legacy_path(self.path)
```

--------------------------------

### Pytest Subtests Example

Source: https://docs.pytest.org/en/stable/changelog

Demonstrates how to use pytest's subtests feature for testing individual files. It iterates through Python files and asserts the presence of a docstring for each, reporting failures individually. This feature is experimental and may evolve.

```python
from pathlib import Path
import pytest

def contains_docstring(p: Path) -> bool:
    """Return True if the given Python file contains a top-level docstring."""
    # Implementation details omitted for brevity
    pass

def test_py_files_contain_docstring(subtests: pytest.Subtests) -> None:
    for path in Path.cwd().glob("*.py"):
        with subtests.test(path=str(path)):
            assert contains_docstring(path)
```

--------------------------------

### Pytest Fixture: Manual Execution Simulation in Python

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Illustrates the manual process of executing a fixture and passing its result to a test function, mimicking pytest's internal behavior. This helps understand the flow of data from fixture to test.

```python
def fruit_bowl():
    return [Fruit("apple"), Fruit("banana")]


def test_fruit_salad(fruit_bowl):
    # Act
    fruit_salad = FruitSalad(*fruit_bowl)

    # Assert
    assert all(fruit.cubed for fruit in fruit_salad.fruit)


# Arrange
bowl = fruit_bowl()
test_fruit_salad(fruit_bowl=bowl)

```

--------------------------------

### Pytest Collection Output Example

Source: https://docs.pytest.org/en/stable/example/pythoncollection

This output demonstrates the result of using the '--collect-only' flag with pytest, showing the collected test items. It includes the test session information, root directory, configuration file, and the hierarchical structure of collected modules, classes, and functions.

```text
$ pytest --collect-only
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y
rootdir: /home/sweet/project
configfile: pytest.toml
collected 2 items

<Dir pythoncollection.rst-213>
  <Module check_myapp.py>
    <Class CheckMyApp>
      <Function simple_check>
      <Function complex_check>

======================== 2 tests collected in 0.12s ========================

```

```text
. $ pytest --collect-only pythoncollection.py
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y
rootdir: /home/sweet/project
configfile: pytest.toml
collected 3 items

<Dir pythoncollection.rst-213>
  <Dir CWD>
    <Module pythoncollection.py>
      <Function test_function>
      <Class TestClass>
        <Function test_method>
        <Function test_anothermethod>

======================== 3 tests collected in 0.12s ========================

```

--------------------------------

### Configure Addopts in Pytest TOML

Source: https://docs.pytest.org/en/stable/reference/reference

Shows how to use the `addopts` configuration option in a `pytest.toml` file to specify default command-line arguments. These options are appended to the user-provided arguments, effectively modifying how pytest runs. For example, `--maxfail` and `-rf` can be set here.

```toml
[pytest]
addopts = ["--maxfail=2", "-rf"]  # exit after 2 failures, report fail info
```

--------------------------------

### Get Direct Parametrize Arguments

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

Retrieves direct parametrization argument names from a node's markers. This helps distinguish parametrization arguments from fixtures, preventing potential conflicts.

```python
def _get_direct_parametrize_args(node: nodes.Node) -> set[str]:
    """Return all direct parametrization arguments of a node, so we don't
    mistake them for fixtures.

    Check https://github.com/pytest-dev/pytest/issues/5036.

    These things are done later as well when dealing with parametrization
    so this could be improved.
    """
    parametrize_argnames: set[str] = set()
    for marker in node.iter_markers(name="parametrize"):
        if not marker.kwargs.get("indirect", False):
            p_argnames, _ = ParameterSet._parse_parametrize_args(
                *marker.args, **marker.kwargs
            )
            parametrize_argnames.update(p_argnames)
    return parametrize_argnames
```

--------------------------------

### Pytest Initial Conftest Loading Logic

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Illustrates the internal pytest function for loading initial conftest.py files based on parsed arguments. It handles path normalization, checks for file existence, and manages the import mode for plugins.

```python
    def _set_initial_conftests(
        self,
        args: Sequence[str | pathlib.Path],
        pyargs: bool,
        noconftest: bool,
        rootpath: pathlib.Path,
        confcutdir: pathlib.Path | None,
        invocation_dir: pathlib.Path,
        importmode: ImportMode | str,
        *, 
        consider_namespace_packages: bool,
    ) -> None:
        """Load initial conftest files given a preparsed "namespace".

        As conftest files may add their own command line options which have
        arguments ('--my-opt somepath') we might get some false positives. 
        All builtin and 3rd party plugins will have been loaded, however, so 
        common options will not confuse our logic here.
        """
        self._confcutdir = (
            absolutepath(invocation_dir / confcutdir) if confcutdir else None
        )
        self._noconftest = noconftest
        self._using_pyargs = pyargs
        foundanchor = False
        for initial_path in args:
            path = str(initial_path)
            # remove node-id syntax
            i = path.find("::")
            if i != -1:
                path = path[:i]
            anchor = absolutepath(invocation_dir / path)

            # Ensure we do not break if what appears to be an anchor
            # is in fact a very long option (#10169, #11394).
            if safe_exists(anchor):
                self._try_load_conftest(
                    anchor,
                    importmode,
                    rootpath,
                    consider_namespace_packages=consider_namespace_packages,
                )
                foundanchor = True
        if not foundanchor:
            self._try_load_conftest(
                invocation_dir,
                importmode,
                rootpath,
                consider_namespace_packages=consider_namespace_packages,
            )
```

--------------------------------

### Parse Hook Specification Options (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Parses options for a hook specification, checking for legacy marks like 'firstresult' and 'historic' if the name starts with 'pytest_'. It extends the functionality of the parent class's method.

```python
def parse_hookspec_opts(self, module_or_class, name: str) -> HookspecOpts | None:
        """:meta private:"""
        opts = super().parse_hookspec_opts(module_or_class, name)
        if opts is None:
            method = getattr(module_or_class, name)
            if name.startswith("pytest_"):
                legacy = _get_legacy_hook_marks(
                    method, "spec", ("firstresult", "historic")
                )
                opts = cast(HookspecOpts, legacy)
        return opts
```

--------------------------------

### Store Data in Pytest Item Stash

Source: https://docs.pytest.org/en/stable/how-to/writing_hook_functions

This example demonstrates how to store data in an item's stash during the `pytest_runtest_setup` hook. It uses predefined stash keys to assign values to the item.

```python
import pytest

# Assuming been_there_key and done_that_key are defined elsewhere

def pytest_runtest_setup(item: pytest.Item) -> None:
    item.stash[been_there_key] = True
    item.stash[done_that_key] = "no"
```

--------------------------------

### Run Pytest In-Process with HookRecorder

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Runs pytest.main() in-process and returns a HookRecorder instance for detailed results. This method allows passing command-line arguments and extra plugins to the pytest run. It also handles system module and path snapshots to ensure isolation between test runs.

```python
from _pytest.unraisableexception import gc_collect_iterations_key
import importlib

importlib.invalidate_caches()

plugins = list(plugins)
finalizers = []
try:
    finalizers.append(self.__take_sys_modules_snapshot().restore)
    finalizers.append(SysPathsSnapshot().restore)

    rec = []

    class PytesterHelperPlugin:
        @staticmethod
        def pytest_configure(config: Config) -> None:
            rec.append(self.make_hook_recorder(config.pluginmanager))
            config.stash[gc_collect_iterations_key] = 0

    plugins.append(PytesterHelperHelperPlugin())
    ret = main([str(x) for x in args], plugins=plugins)
    if len(rec) == 1:
        reprec = rec.pop()
    else:
        class reprec:  # type: ignore
            pass

    reprec.ret = ret

    if ret == ExitCode.INTERRUPTED and not no_reraise_ctrlc:
        calls = reprec.getcalls("pytest_keyboard_interrupt")
        if calls and calls[-1].excinfo.type == KeyboardInterrupt:
            raise KeyboardInterrupt()
    return reprec
finally:
    for finalizer in finalizers:
        finalizer()
```

--------------------------------

### Getting Hook Callers for a Plugin in PytestPluginManager

Source: https://docs.pytest.org/en/stable/reference/reference

Retrieves all hook callers associated with a specific plugin. Returns a list of HookCaller instances or None if the plugin is not registered.

```python
def get_hookcallers(self, _plugin_):
    """Get all hook callers for the specified plugin."""
    # Implementation details...
```

--------------------------------

### Get Node by Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Retrieves a node (item or collector) from the pytest collection tree based on a given path. It returns the node or None if not found. This is useful for inspecting the collection process.

```python
def getpathnode(self, path):
    """See :meth:`Pytester.getpathnode`."""
    return self._pytester.getpathnode(path)
```

--------------------------------

### Get Callable Representation

Source: https://docs.pytest.org/en/stable/_modules/_pytest/raises

Returns the string representation of a callable function. This utility is designed to be monkeypatchable, allowing for custom representations, for instance, by testing frameworks like Hypothesis.

```python
from typing import Callable
def repr_callable(fun: Callable[[BaseExcT_1], bool]) -> str:
    """Get the repr of a ``check`` parameter.

    Split out so it can be monkeypatched (e.g. by hypothesis)
    """
    return repr(fun)
```

--------------------------------

### Get Module Collection Node

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `getmodulecol` method retrieves the module collection node for a given source code. It writes the source to a file (optionally creating an `__init__.py` for packages) and then runs pytest's collection on it.

```python
def getmodulecol(
        self,
        source: str | os.PathLike[str],
        configargs=(),
        *,
        withinit: bool = False,
    ):
    """Return the module collection node for ``source``.

    Writes ``source`` to a file using :py:meth:`makepyfile` and then
    runs the pytest collection on it, returning the collection node for the
    test module.

    :param source:
        The source code of the module to collect.

    :param configargs:
        Any extra arguments to pass to :py:meth:`parseconfigure`.

    :param withinit:
        Whether to also write an ``__init__.py`` file to the same
        directory to ensure it is a package.
    """
    if isinstance(source, os.PathLike):
        path = self.path.joinpath(source)
        assert not withinit, "not supported for paths"
    else:
        kw = {self._name: str(source)}
        path = self.makepyfile(**kw)
    if withinit:
        self.makepyfile(__init__="#")
    self.config = config = self.parseconfigure(path, *configargs)
    return self.getnode(config, path)
```

--------------------------------

### Pytest Fixture Dependency Order Example

Source: https://docs.pytest.org/en/stable/reference/fixtures

Demonstrates how fixtures with interdependencies are executed in a specific order by pytest. The 'order' fixture tracks the execution sequence, and the test verifies this sequence against the expected order based on fixture requests.

```python
from __future__ import annotations

import pytest


@pytest.fixture
def order():
    return []


@pytest.fixture
def a(order):
    order.append("a")


@pytest.fixture
def b(a, order):
    order.append("b")


@pytest.fixture
def c(b, order):
    order.append("c")


@pytest.fixture
def d(c, b, order):
    order.append("d")


@pytest.fixture
def e(d, b, order):
    order.append("e")


@pytest.fixture
def f(e, order):
    order.append("f")


@pytest.fixture
def g(f, c, order):
    order.append("g")


def test_order(g, order):
    assert order == ["a", "b", "c", "d", "e", "f", "g"]

```

--------------------------------

### Pytest Configuration Initialization

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Initializes pytest configuration by parsing arguments, loading ini options, and setting up the plugin manager. It handles extra command-line options, minimum version checks, and python path configurations. Dependencies include the 'copy' module for namespace copying and 'os' for environment variable checks.

```python
self.known_args_namespace = self._parser.parse_known_args(
            args, namespace=copy.copy(self.option)
        )
        self._checkversion()
        self._consider_importhook()
        self._configure_python_path()
        self.pluginmanager.consider_preparse(args, exclude_only=False)
        if (
            not os.environ.get("PYTEST_DISABLE_PLUGIN_AUTOLOAD")
            and not self.known_args_namespace.disable_plugin_autoload
        ):
            # Autoloading from distribution package entry point has
            # not been disabled.
            self.pluginmanager.load_setuptools_entrypoints("pytest11")
        # Otherwise only plugins explicitly specified in PYTEST_PLUGINS
        # are going to be loaded.
        self.pluginmanager.consider_env()

        self._parser.parse_known_args(args, namespace=self.known_args_namespace)

        self._validate_plugins()
        self._warn_about_skipped_plugins()

        if self.known_args_namespace.confcutdir is None:
            if self.inipath is not None:
                confcutdir = str(self.inipath.parent)
            else:
                confcutdir = str(self.rootpath)
            self.known_args_namespace.confcutdir = confcutdir
        try:
            self.hook.pytest_load_initial_conftests(
                early_config=self, args=args, parser=self._parser
            )
        except ConftestImportFailure as e:
            if self.known_args_namespace.help or self.known_args_namespace.version:
                # we don't want to prevent --help/--version to work
                # so just let it pass and print a warning at the end
                self.issue_config_time_warning(
                    PytestConfigWarning(f"could not load initial conftests: {e.path}"),
                    stacklevel=2,
                )
            else:
                raise

        try:
            self._parser.parse(args, namespace=self.option)
        except PrintHelp:
            return

        self.args, self.args_source = self._decide_args(
            args=getattr(self.option, FILE_OR_DIR),
            pyargs=self.option.pyargs,
            testpaths=self.getini("testpaths"),
            invocation_dir=self.invocation_params.dir,
            rootpath=self.rootpath,
            warn=True,
        )
```

--------------------------------

### Pytest Foo Class Comparison Example

Source: https://docs.pytest.org/en/stable/how-to/assert

A simple Python class `Foo` with an equality method, used in conjunction with a pytest test to demonstrate the custom assertion explanation hook. The test intentionally fails to show the custom output.

```python
class Foo:
    def __init__(self, val):
        self.val = val

    def __eq__(self, other):
        return self.val == other.val

def test_compare():
    f1 = Foo(1)
    f2 = Foo(2)
    assert f1 == f2
```

--------------------------------

### pytest.raises with Exception Type and Match Pattern

Source: https://docs.pytest.org/en/stable/_modules/_pytest/raises

This example shows how to use pytest.raises with both an expected exception type and a regular expression pattern to match against the exception's string representation. This allows for more specific assertion of the exception's message content. The `match` argument supports string literals and regex objects.

```python
>>> with pytest.raises(ValueError, match='must be 0 or None'):
...     raise ValueError("value must be 0 or None")

>>> with pytest.raises(ValueError, match=r'must be \d+$'):
...     raise ValueError("value must be 42")
```

--------------------------------

### Pytest Autouse Fixture Scope Limitation Example

Source: https://docs.pytest.org/en/stable/reference/fixtures

Shows that a fixture made effectively autouse by an autouse fixture only becomes autouse within the scope of the original autouse fixture, not globally.

```python
from __future__ import annotations

import pytest


@pytest.fixture
def order():
    return []


@pytest.fixture
def c1(order):
    order.append("c1")


@pytest.fixture
def c2(order):
    order.append("c2")


class TestClassWithAutouse:
    @pytest.fixture(autouse=True)
    def c3(self, order, c2):
        order.append("c3")

    def test_req(self, order, c1):
        assert order == ["c2", "c3", "c1"]

    def test_no_req(self, order):
        assert order == ["c2", "c3"]


class TestClassWithoutAutouse:
    def test_req(self, order, c1):
        assert order == ["c1"]

    def test_no_req(self, order):
        assert order == []

```

--------------------------------

### Using pytest.set_trace() for Debugging

Source: https://docs.pytest.org/en/stable/historical-notes

An example of how pytest.set_trace() was used prior to version 2.4 to invoke the PDB debugger within a test function. This functionality is now superseded by the native pdb.set_trace().

```python
import pytest


def test_function():
    ...
    pytest.set_trace()  # invoke PDB debugger and tracing

```

--------------------------------

### Get Fixture Information for an Item

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

Calculates the FuncFixtureInfo for a given test item (node), considering function arguments, autouse fixtures, and usefixtures markers. It handles cases where the function is not examined.

```python
def getfixtureinfo(
    self,
    node: nodes.Item,
    func: Callable[..., object] | None,
    cls: type | None,
) -> FuncFixtureInfo:
    """Calculate the :class:`FuncFixtureInfo` for an item.

    If ``func`` is None, or if the item sets an attribute
    ``nofuncargs = True``, then ``func`` is not examined at all.

    :param node:
        The item requesting the fixtures.
    :param func:
        The item's function.
    :param cls:
        If the function is a method, the method's class.
    """
    if func is not None and not getattr(node, "nofuncargs", False):
        argnames = getfuncargnames(func, name=node.name, cls=cls)
    else:
        argnames = ()
    usefixturesnames = self._getusefixturesnames(node)
    autousenames = self._getautousenames(node)
    initialnames = deduplicate_names(autousenames, usefixturesnames, argnames)

    direct_parametrize_args = _get_direct_parametrize_args(node)

    names_closure, arg2fixturedefs = self.getfixtureclosure(
        parentnode=node,
        initialnames=initialnames,
        ignore_args=direct_parametrize_args,
    )

    return FuncFixtureInfo(argnames, initialnames, names_closure, arg2fixturedefs)
```

--------------------------------

### Advanced Warning Assertion with pytest.warns() and match argument

Source: https://docs.pytest.org/en/stable/how-to/capture-warnings

Provides examples of using the `match` keyword argument in pytest.warns() to assert that a warning message conforms to a specific text or regular expression pattern. It also shows how to escape special characters for literal string matching.

```python
import warnings
import pytest
import re

with pytest.warns(UserWarning, match="must be 0 or None"):
    warnings.warn("value must be 0 or None", UserWarning)

with pytest.warns(UserWarning, match=r"must be \d+$"):
    warnings.warn("value must be 42", UserWarning)

# Example of a failing test (commented out)
# with pytest.warns(UserWarning, match=r"must be \d+$"):
#     warnings.warn("this is not here", UserWarning)

with pytest.warns(UserWarning, match=re.escape("issue with foo() func")):
    warnings.warn("issue with foo() func")
```

--------------------------------

### Get All Test Items from Source Code

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `getitems` method collects all test items from a given source code. It writes the source to a file and then runs pytest's collection process on the resulting module to gather all test items.

```python
def getitems(self, source: str | os.PathLike[str]) -> list[Item]:
    """Return all test items collected from the module.

    Writes the source to a Python file and runs pytest's collection on
    the resulting module, returning all test items contained within.
    """
    modcol = self.getmodulecol(source)
    return self.genitems([modcol])
```

--------------------------------

### CaptureFixture: Reading Captured Output

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Provides the `readouterr` method to retrieve captured stdout and stderr. This method returns the accumulated output since the last call to `readouterr` or since the capture started, and then resets the internal buffers.

```python
    def readouterr(self) -> CaptureResult[AnyStr]:
        """Read and return the captured output so far, resetting the internal
        buffer.

        :returns:
            The captured content as a namedtuple with ``out`` and ``err``
            string attributes.
        """
        captured_out, captured_err = self._captured_out, self._captured_err
        if self._capture is not None:
            out, err = self._capture.readouterr()
            captured_out += out
            captured_err += err
        self._captured_out = self.captureclass.EMPTY_BUFFER
        self._captured_err = self.captureclass.EMPTY_BUFFER
        return CaptureResult(captured_out, captured_err)
```

--------------------------------

### CaptureFixture: Checking Capture Status

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

The `_is_started` method checks if the capture fixture is actively capturing. It returns `True` if the internal capture object is active and capturing, and `False` otherwise.

```python
    def _is_started(self) -> bool:
        """Whether actively capturing -- not disabled or closed."""
        if self._capture is not None:
            return self._capture.is_started()
        return False
```

--------------------------------

### Pytest Test Execution with Parametrized Fixtures

Source: https://docs.pytest.org/en/stable/how-to/fixtures

This section shows the output of running pytest tests that utilize a parametrized fixture. The output demonstrates how pytest executes each test function multiple times, once for each parameter defined in the fixture. It highlights test failures and the specific parametrized test case that failed, including the server configuration used.

```bash
$ pytest -q test_module.py
FFFF                                                                 [100%]
================================= FAILURES =================================
________________________ test_ehlo[smtp.gmail.com] _________________________

smtp_connection = <smtplib.SMTP object at 0xdeadbeef0004>

    def test_ehlo(smtp_connection):
        response, msg = smtp_connection.ehlo()
        assert response == 250
        assert b"smtp.gmail.com" in msg
>       assert 0  # for demo purposes
        ^^^^^^^^
E       assert 0

test_module.py:7: AssertionError
________________________ test_noop[smtp.gmail.com] _________________________

smtp_connection = <smtplib.SMTP object at 0xdeadbeef0004>

    def test_noop(smtp_connection):
        response, msg = smtp_connection.noop()
        assert response == 250
>       assert 0  # for demo purposes
        ^^^^^^^^
E       assert 0

test_module.py:13: AssertionError
________________________ test_ehlo[mail.python.org] ________________________

smtp_connection = <smtplib.SMTP object at 0xdeadbeef0005>

    def test_ehlo(smtp_connection):
        response, msg = smtp_connection.ehlo()
        assert response == 250
>       assert b"smtp.gmail.com" in msg
E       AssertionError: assert b'smtp.gmail.com' in b'mail.python.org\nPIPELINING\nSIZE 51200000\nETRN\nSTARTTLS\nAUTH DIGEST-MD5 NTLM CRAM-MD5\nENHANCEDSTATUSCODES\n8BITMIME\nDSN\nSMTPUTF8\nCHUNKING'

test_module.py:6: AssertionError
-------------------------- Captured stdout setup ---------------------------
finalizing <smtplib.SMTP object at 0xdeadbeef0004>
________________________ test_noop[mail.python.org] ________________________

smtp_connection = <smtplib.SMTP object at 0xdeadbeef0005>

    def test_noop(smtp_connection):
        response, msg = smtp_connection.noop()
        assert response == 250
>       assert 0  # for demo purposes
        ^^^^^^^^
E       assert 0

test_module.py:13: AssertionError
------------------------- Captured stdout teardown -------------------------
finalizing <smtplib.SMTP object at 0xdeadbeef0005>
========================= short test summary info ==========================
FAILED test_module.py::test_ehlo[smtp.gmail.com] - assert 0
FAILED test_module.py::test_noop[smtp.gmail.com] - assert 0
FAILED test_module.py::test_ehlo[mail.python.org] - AssertionError: asser...
FAILED test_module.py::test_noop[mail.python.org] - assert 0
4 failed in 0.12s
```

--------------------------------

### Initialize Pytest Configuration

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Initializes the Pytest configuration object, setting up internal caches, handling environment variables for debugging, and registering core hooks. It also initializes a dummy rewrite hook and prepares for plugin discovery.

```python
self._dirpath2confmods: dict[pathlib.Path, list[types.ModuleType]] = {}
        # Cutoff directory above which conftests are no longer discovered.
        self._confcutdir: pathlib.Path | None = None
        # If set, conftest loading is skipped.
        self._noconftest = False

        # _getconftestmodules()'s call to _get_directory() causes a stat
        # storm when it's called potentially thousands of times in a test
        # session (#9478), often with the same path, so cache it.
        self._get_directory = lru_cache(256)(_get_directory)

        # plugins that were explicitly skipped with pytest.skip
        # list of (module name, skip reason)
        # previously we would issue a warning when a plugin was skipped, but
        # since we refactored warnings as first citizens of Config, they are
        # just stored here to be used later.
        self.skipped_plugins: list[tuple[str, str]] = []

        self.add_hookspecs(_pytest.hookspec)
        self.register(self)
        if os.environ.get("PYTEST_DEBUG"):
            err: IO[str] = sys.stderr
            encoding: str = getattr(err, "encoding", "utf8")
            try:
                err = open(
                    os.dup(err.fileno()),
                    mode=err.mode,
                    buffering=1,
                    encoding=encoding,
                )
            except Exception:
                pass
            self.trace.root.setwriter(err.write)
            self.enable_tracing()

        # Config._consider_importhook will set a real object if required.
        self.rewrite_hook: RewriteHook = DummyRewriteHook()
        # Used to know when we are importing conftests after the pytest_configure stage.
        self._configured = False
```

--------------------------------

### Pytest Fixture Usage Example (test_foo.py)

Source: https://docs.pytest.org/en/stable/changelog

This snippet shows how to use a fixture defined in conftest.py within a test file. The 'foo' fixture from conftest.py is injected into another fixture, which then multiplies its value by 2. This illustrates fixture dependency.

```python
import pytest


@pytest.fixture
def foo(foo):
    return foo * 2
```

--------------------------------

### Pytest CI Detection and Behavior Example

Source: https://docs.pytest.org/en/stable/explanation/ci

This Python code snippet demonstrates a failing test case designed to show the difference in output when pytest runs in a CI environment versus locally. Pytest's behavior changes when CI-related environment variables are set.

```python
import pytest

def test_db_initialized():
    pytest.fail(
        "deliberately failing for demo purpose, Lorem ipsum dolor sit amet, "
        "consectetur adipiscing elit. Cras facilisis, massa in suscipit "
        "dignissim, mauris lacus molestie nisi, quis varius metus nulla ut ipsum."
    )

```

--------------------------------

### pytest.raises with PEP-678 Notes Matching

Source: https://docs.pytest.org/en/stable/_modules/_pytest/raises

This example shows how pytest.raises can match against exception messages that include PEP-678 notes. The `match` argument searches the formatted exception string, including any added notes, allowing for assertions on richer exception information.

```python
>>> with pytest.raises(ValueError, match=r"had a note added"):  # doctest: +SKIP
...     e = ValueError("value must be 42")
...     e.add_note("had a note added")
...     raise e
```

--------------------------------

### Pytest Fixture Example (conftest.py)

Source: https://docs.pytest.org/en/stable/changelog

This snippet demonstrates how to define a pytest fixture named 'foo' in conftest.py. The fixture is parameterized to yield values 1 and 2. It's intended for use in test files within the same directory.

```python
import pytest


@pytest.fixture(params=[1, 2])
def foo(request):
    return request.param
```

--------------------------------

### Get Paths of Previously Failed Tests

Source: https://docs.pytest.org/en/stable/_modules/_pytest/cacheprovider

Retrieves a set of file paths corresponding to previously failed tests and their parent directories. This is used to efficiently locate and rerun failed tests.

```python
def get_last_failed_paths(self) -> set[Path]:
        """Return a set with all Paths of the previously failed nodeids and
        their parents."""
        rootpath = self.config.rootpath
        result = set()
        for nodeid in self.lastfailed:
            path = rootpath / nodeid.split("::")[0]
            result.add(path)
            result.update(path.parents)
        return {x for x in result if x.exists()}
```

--------------------------------

### Configure Plugin Disabling (INI)

Source: https://docs.pytest.org/en/stable/how-to/plugins

Unconditionally disables a plugin for a project by adding the '-p no:NAME' option to the pytest configuration file in INI format. This is an alternative to TOML for project-specific configurations.

```ini
[pytest]
addopts = -p no:NAME
```

--------------------------------

### Pytest Module Importing and Test Directory Layouts

Source: https://docs.pytest.org/en/stable/announce/release-2.5.0

This documentation clarifies how Pytest imports modules, discusses common test directory layouts, and explains interactions with PEP420-namespace packages.

```python
# Example of a common test directory layout:
# project/
# ├── src/
# │   └── my_module/
# │       └── __init__.py
# └── tests/
#     ├── __init__.py
#     └── test_my_module.py
```

--------------------------------

### Configure Plugin Autoloading Disabling (TOML)

Source: https://docs.pytest.org/en/stable/how-to/plugins

Configures pytest to disable plugin autoloading and specify plugins to load using the addopts setting in a TOML configuration file. This allows for project-specific control over plugin loading behavior.

```toml
[pytest]
addopts = ["--disable-plugin-autoload", "-p", "NAME", "-p", "NAME2"]
```

--------------------------------

### Base Class for System Stream Capture (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

An abstract base class for capturing standard system streams (stdin, stdout, stderr). It handles the redirection of file descriptors and manages the state of the capture process. It supports optional teeing to write to the original stream as well.

```python
patchsysdict = {0: "stdin", 1: "stdout", 2: "stderr"}

class SysCaptureBase(CaptureBase[AnyStr]):
    def __init__( 
        self, fd: int, tmpfile: TextIO | None = None, *, tee: bool = False 
    ) -> None:
        name = patchsysdict[fd]
        self._old: TextIO = getattr(sys, name)
        self.name = name
        if tmpfile is None:
            if name == "stdin":
                tmpfile = DontReadFromInput()
            else:
                tmpfile = CaptureIO() if not tee else TeeCaptureIO(self._old)
        self.tmpfile = tmpfile
        self._state = "initialized"

    def repr(self, class_name: str) -> str:
        return "<{} {} _old={} _state={!r} tmpfile={!r}>".format(
            class_name,
            self.name,
            (hasattr(self, "_old") and repr(self._old)) or "<UNSET>",
            self._state,
            self.tmpfile,
        )

    def __repr__(self) -> str:
        return "<{} {} _old={} _state={!r} tmpfile={!r}>".format(
            self.__class__.__name__,
            self.name,
            (hasattr(self, "_old") and repr(self._old)) or "<UNSET>",
            self._state,
            self.tmpfile,
        )

    def _assert_state(self, op: str, states: tuple[str, ...]) -> None:
        assert self._state in states, (
            "cannot {} in state {!r}: expected one of {}".format(
                op, self._state, ", ".join(states)
            )
        )

    def start(self) -> None:
        self._assert_state("start", ("initialized",))
        setattr(sys, self.name, self.tmpfile)
        self._state = "started"

    def done(self) -> None:
        self._assert_state("done", ("initialized", "started", "suspended", "done"))
        if self._state == "done":
            return
        setattr(sys, self.name, self._old)
        del self._old
        self.tmpfile.close()
        self._state = "done"

    def suspend(self) -> None:
        self._assert_state("suspend", ("started", "suspended"))
        setattr(sys, self.name, self._old)
        self._state = "suspended"

    def resume(self) -> None:
        self._assert_state("resume", ("started", "suspended"))
        if self._state == "started":
            return
        setattr(sys, self.name, self.tmpfile)
        self._state = "started"

```

--------------------------------

### Unconditionally Skip All Pytest Tests in a Module

Source: https://docs.pytest.org/en/stable/how-to/skipping

Provides an example of unconditionally skipping all tests within a module using pytestmark and pytest.mark.skip. This is typically used when tests are under development or temporarily disabled.

```python
pytestmark = pytest.mark.skip("all tests still WIP")
```

--------------------------------

### Get Command Line Option Value - Python

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Retrieves the value of a command-line option. It can handle option names or their 'dest' equivalents. If an option is not declared or has a None value, it can either return a default or raise a pytest.skip exception.

```python
def getoption(self, name: str, default: Any = notset, skip: bool = False):
    """Return command line option value.

    :param name: Name of the option. You may also specify
        the literal ``--OPT`` option instead of the "dest" option name.
    :param default: Fallback value if no option of that name is **declared** via :hook:`pytest_addoption`.
        Note this parameter will be ignored when the option is **declared** even if the option's value is ``None``.
    :param skip: If ``True``, raise :func:`pytest.skip` if option is undeclared or has a ``None`` value.
        Note that even if ``True``, if a default was specified it will be returned instead of a skip.
    """
    name = self._opt2dest.get(name, name)
    try:
        val = getattr(self.option, name)
        if val is None and skip:
            raise AttributeError(name)
        return val
    except AttributeError as e:
        if default is not notset:
            return default
        if skip:
            import pytest

            pytest.skip(f"no {name!r} option found")
        raise ValueError(f"no option named {name!r}") from e

```

--------------------------------

### Disable Plugin Autoloading (Command Line)

Source: https://docs.pytest.org/en/stable/how-to/plugins

Disables the automatic loading of plugins. You can then manually specify plugins to load using '-p' or '--disable-plugin-autoload'. This provides fine-grained control over which plugins are active.

```bash
pytest --disable-plugin-autoload -p NAME,NAME2
```

--------------------------------

### FDCaptureBinary Snap and WriteOrg Methods (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Implements binary capture functionality. The `snap` method retrieves captured data as bytes, and `writeorg` writes data directly to the original file descriptor.

```python
class FDCaptureBinary(FDCaptureBase[bytes]):
    """Capture IO to/from a given OS-level file descriptor.

    snap() produces `bytes`.
    """

    EMPTY_BUFFER = b""

    def snap(self) -> bytes:
        self._assert_state("snap", ("started", "suspended"))
        self.tmpfile.seek(0)
        res = self.tmpfile.buffer.read()
        self.tmpfile.seek(0)
        self.tmpfile.truncate()
        return res  # type: ignore[return-value]

    def writeorg(self, data: bytes) -> None:
        """Write to original file descriptor."""
        self._assert_state("writeorg", ("started", "suspended"))
        os.write(self.targetfd_save, data)
```

--------------------------------

### Pytest Configuration in pyproject.toml (INI Options)

Source: https://docs.pytest.org/en/stable/reference/customize

Example of configuring pytest using pyproject.toml with INI-style options, supported since pytest 6.0. This allows specifying minimum version, additional options, and test paths.

```toml
# pyproject.toml
[tool.pytest.ini_options]
minversion = "6.0"
addopts = "-ra -q"
testpaths = [
    "tests",
    "integration",
]
```

--------------------------------

### Pytest Fixtures for Session-Scoped Imports

Source: https://docs.pytest.org/en/stable/example/parametrize

Demonstrates session-scoped fixtures in conftest.py to import modules once per test session. It includes examples for importing a base module and parameterized optional modules, along with a test module that utilizes these fixtures. This approach is efficient for resources that don't need re-initialization.

```python
# content of conftest.py

import pytest


@pytest.fixture(scope="session")
def basemod(request):
    return pytest.importorskip("base")


@pytest.fixture(scope="session", params=["opt1", "opt2"])
def optmod(request):
    return pytest.importorskip(request.param)

```

```python
# content of base.py
def func1():
    return 1

```

```python
# content of opt1.py
def func1():
    return 1.0001

```

```python
# content of test_module.py


def test_func1(basemod, optmod):
    assert round(basemod.func1(), 3) == round(optmod.func1(), 3)

```

--------------------------------

### Configure Plugin Disabling (TOML)

Source: https://docs.pytest.org/en/stable/how-to/plugins

Unconditionally disables a plugin for a project by adding the '-p no:NAME' option to the pytest configuration file in TOML format. This ensures the plugin is never loaded for the project.

```toml
[pytest]
addopts = ["-p", "no:NAME"]
```

--------------------------------

### Configure Plugin Autoloading Disabling (INI)

Source: https://docs.pytest.org/en/stable/how-to/plugins

Configures pytest to disable plugin autoloading and specify plugins to load using the addopts setting in an INI configuration file. This provides a clear, multi-line way to define plugin loading options.

```ini
[pytest]
addopts =
    --disable-plugin-autoload
    -p NAME
    -p NAME2
```

--------------------------------

### Initialize and Manage Live Logging Handler (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/logging

Initializes a live logging handler, integrating with a TerminalReporter and an optional CaptureManager. It provides methods to reset the handler, set the current test phase (setup, call, teardown), and emit log records, ensuring proper formatting and output to the stream.

```python
class LiveLoggingHandler(logging.Handler):
    """A logging handler that displays logs in real-time during test execution."""

    # Officially stream needs to be a IO[str], but TerminalReporter
    # isn't. So force it.
    stream: TerminalReporter = None  # type: ignore

    def __init__(
        self,
        terminal_reporter: TerminalReporter,
        capture_manager: CaptureManager | None,
    ) -> None:
        super().__init__(stream=terminal_reporter)  # type: ignore[arg-type]
        self.capture_manager = capture_manager
        self.reset()
        self.set_when(None)
        self._test_outcome_written = False

    def reset(self) -> None:
        """Reset the handler; should be called before the start of each test."""
        self._first_record_emitted = False

    def set_when(self, when: str | None) -> None:
        """Prepare for the given test phase (setup/call/teardown)."""
        self._when = when
        self._section_name_shown = False
        if when == "start":
            self._test_outcome_written = False

    def emit(self, record: logging.LogRecord) -> None:
        ctx_manager = (
            self.capture_manager.global_and_fixture_disabled()
            if self.capture_manager
            else nullcontext()
        )
        with ctx_manager:
            if not self._first_record_emitted:
                self.stream.write("\n")
                self._first_record_emitted = True
            elif self._when in ("teardown", "finish"):
                if not self._test_outcome_written:
                    self._test_outcome_written = True
                    self.stream.write("\n")
            if not self._section_name_shown and self._when:
                self.stream.section("live log " + self._when, sep="-", bold=True)
                self._section_name_shown = True
            super().emit(record)

    def handleError(self, record: logging.LogRecord) -> None:
        # Handled by LogCaptureHandler.
        pass
```

--------------------------------

### Show Slowest Test Durations in Pytest

Source: https://docs.pytest.org/en/stable/reference/reference

Displays the N slowest test setup and execution durations. Setting N to 0 shows all durations. This helps in identifying performance bottlenecks in tests.

```bash
pytest --durations=10
```

```bash
pytest --durations=0
```

--------------------------------

### Web Application Test Fixtures (Python)

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Demonstrates a set of pytest fixtures for testing a web application's login functionality. It includes fixtures for admin client, user creation/deletion, Selenium WebDriver, login process, and landing page access.

```python
from uuid import uuid4
from urllib.parse import urljoin

from selenium.webdriver import Chrome
import pytest

from src.utils.pages import LoginPage, LandingPage
from src.utils import AdminApiClient
from src.utils.data_types import User


@pytest.fixture
def admin_client(base_url, admin_credentials):
    return AdminApiClient(base_url, **admin_credentials)


@pytest.fixture
def user(admin_client):
    _user = User(name="Susan", username=f"testuser-{uuid4()}", password="P4$$word")
    admin_client.create_user(_user)
    yield _user
    admin_client.delete_user(_user)


@pytest.fixture
def driver():
    _driver = Chrome()
    yield _driver
    _driver.quit()


@pytest.fixture
def login(driver, base_url, user):
    driver.get(urljoin(base_url, "/login"))
    page = LoginPage(driver)
    page.login(user)


@pytest.fixture
def landing_page(driver, login):
    return LandingPage(driver)


def test_name_on_landing_page_after_login(landing_page, user):
    assert landing_page.header == f"Welcome, {user.name}!"
```

--------------------------------

### pytest_deselected

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

This hook is called for test items that have been deselected, for example, due to keyword filtering. It can be implemented to be notified of deselected items and must be called from `pytest_collection_modifyitems` when items are deselected.

```APIDOC
## POST /pytest_deselected

### Description
Called for deselected test items. This hook is important for plugins that need to be aware of items that were excluded from the test run, potentially due to filtering.

### Method
POST

### Endpoint
/pytest_deselected

### Parameters
#### Query Parameters
- **items** (Sequence[Item]) - Required - A sequence of deselected test items.

### Request Example
```json
{
  "items": [
    { /* Item object */ },
    { /* Item object */ }
  ]
}
```

### Response
#### Success Response (200)
- **None** - This hook does not return a value.

#### Response Example
```json
{
  "message": "Deselected items processed."
}
```
```

--------------------------------

### Exception Formatting for Test Failures (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/reports

Handles the formatting of exception information into a long representation suitable for test failure reports. It distinguishes between exceptions occurring during the test call and those during setup or teardown phases, applying appropriate representation styles.

```python
def _format_failed_longrepr(
    item: Item,
    call: CallInfo[None],
    excinfo: ExceptionInfo[BaseException]
):
    if call.when == "call":
        longrepr = item.repr_failure(excinfo)
    else:
        # Exception in setup or teardown.
        longrepr = item._repr_failure_py(
            excinfo,
            style=item.config.getoption("tbstyle", "auto")
        )
    return longrepr

```

--------------------------------

### Handle Unknown Configuration Type (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Raises a ValueError for configuration options with an unrecognized type. This is intended for monkeypatching and typically not called directly.

```python
def _getini_unknown_type(self, name: str, type: str, value: object):
    msg = (
        f"Option {name} has unknown configuration type {type} with value {value!r}"
    )
    raise ValueError(msg)  # pragma: no cover
```

--------------------------------

### Considering Plugin Arguments in Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

This function handles individual plugin arguments. If an argument starts with 'no:', it attempts to disable the specified plugin, with a check to prevent disabling essential plugins. This is part of the plugin management system.

```python
def consider_pluginarg(self, arg: str) -> None:
        """:meta private:"""
        if arg.startswith("no:"):
            name = arg[3:]
            if name in essential_plugins:
                raise UsageError(f"plugin {name} cannot be disabled")

            # PR #4304: remove stepwise if cacheprovider is blocked.

```

--------------------------------

### Pytest Fixture Configuration in pytest.toml

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Illustrates how to configure fixtures that are required by all tests in a project using a `pytest.toml` configuration file. This centralizes fixture management for the entire project.

```toml
[pytest]
usefixtures = ["cleandir"]
```

--------------------------------

### Deactivate Plugin by Name (Command Line)

Source: https://docs.pytest.org/en/stable/how-to/plugins

Prevents a specific plugin from loading by using the '-p no:NAME' flag. Subsequent attempts to activate the plugin will fail. This is useful for temporarily disabling plugins.

```bash
pytest -p no:NAME
```

--------------------------------

### Pytest Parametrization with Marks and IDs

Source: https://docs.pytest.org/en/stable/example/parametrize

Illustrates how to use pytest.mark.parametrize with pytest.param to apply custom marks (e.g., 'basic') and set explicit test IDs for individual parametrized tests. This allows for finer control over test selection and reporting, as shown in the example test_eval function.

```python
# content of test_pytest_param_example.py
import pytest


@pytest.mark.parametrize(
    "test_input,expected",
    [
        ("3+5", 8),
        pytest.param("1+7", 8, marks=pytest.mark.basic),
        pytest.param("2+4", 6, marks=pytest.mark.basic, id="basic_2+4"),
        pytest.param(
            "6*9", 42, marks=[pytest.mark.basic, pytest.mark.xfail], id="basic_6*9"
        ),
    ],
)
def test_eval(test_input, expected):
    assert eval(test_input) == expected

```

--------------------------------

### Skip Tests Based on Platform Markers

Source: https://docs.pytest.org/en/stable/example/markers

Implements a pytest plugin in conftest.py to skip tests based on platform-specific markers (e.g., 'darwin', 'win32', 'linux'). The `pytest_runtest_setup` hook checks if a test has any platform markers and if the current system's platform is not among them. If so, the test is skipped with a descriptive message. The example includes test files demonstrating marked tests for different platforms and a test that runs everywhere.

```python
# content of conftest.py
#
import sys

import pytest

ALL = set("darwin linux win32".split())


def pytest_runtest_setup(item):
    supported_platforms = ALL.intersection(mark.name for mark in item.iter_markers())
    plat = sys.platform
    if supported_platforms and plat not in supported_platforms:
        pytest.skip(f"cannot run on platform {plat}")
```

```python
# content of test_plat.py

import pytest


@pytest.mark.darwin
def test_if_apple_is_evil():
    pass


@pytest.mark.linux
def test_if_linux_works():
    pass


@pytest.mark.win32
def test_if_win32_crashes():
    pass


def test_runs_everywhere():
    pass
```

--------------------------------

### Abstract Base Class for Capturing Streams (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Defines the abstract interface for stream capturing. It outlines methods for initialization, starting, stopping, suspending, resuming, writing, and snapping captured data. This class uses generics for type hinting of string types.

```python
import abc
import sys
import os
from typing import AnyStr, TextIO, Generic

class CaptureBase(abc.ABC, Generic[AnyStr]):
    EMPTY_BUFFER: AnyStr

    @abc.abstractmethod
    def __init__(self, fd: int) -> None:
        raise NotImplementedError()

    @abc.abstractmethod
    def start(self) -> None:
        raise NotImplementedError()

    @abc.abstractmethod
    def done(self) -> None:
        raise NotImplementedError()

    @abc.abstractmethod
    def suspend(self) -> None:
        raise NotImplementedError()

    @abc.abstractmethod
    def resume(self) -> None:
        raise NotImplementedError()

    @abc.abstractmethod
    def writeorg(self, data: AnyStr) -> None:
        raise NotImplementedError()

    @abc.abstractmethod
    def snap(self) -> AnyStr:
        raise NotImplementedError()

```

--------------------------------

### Initialize Pytest Configuration

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Initializes the Pytest configuration object, setting up plugin managers, hooks, and parsing command-line arguments. It registers the 'pytestconfig' plugin and handles initial hook calls.

```python
self.trace = self.pluginmanager.trace.root.get("config")
self.hook: pluggy.HookRelay = PathAwareHookProxy(self.pluginmanager.hook)  # type: ignore[assignment]
self._inicache: dict[str, Any] = {}
self._opt2dest: dict[str, str] = {}
self._cleanup_stack = contextlib.ExitStack()
self.pluginmanager.register(self, "pytestconfig")
self._configured = False
self.hook.pytest_addoption.call_historic(
    kwargs=dict(parser=self._parser, pluginmanager=self.pluginmanager)
)
self.args_source = Config.ArgsSource.ARGS
self.args: list[str] = []
```

--------------------------------

### Pytest Function Instance Creation

Source: https://docs.pytest.org/en/stable/_modules/_pytest/python

A helper method to create a new instance of the class if the test function is part of a class. It ensures each test function gets a fresh instance.

```python
def _getinstance(self):
    if isinstance(self.parent, Class):
        # Each Function gets a fresh class instance.
        return self.parent.newinstance()
    else:
        return None
```

--------------------------------

### FDCapture Snap and WriteOrg Methods (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Implements text capture functionality. The `snap` method retrieves captured data as a string, and `writeorg` writes string data to the original file descriptor after encoding it.

```python
class FDCapture(FDCaptureBase[str]):
    """Capture IO to/from a given OS-level file descriptor.

    snap() produces text.
    """

    EMPTY_BUFFER = ""

    def snap(self) -> str:
        self._assert_state("snap", ("started", "suspended"))
        self.tmpfile.seek(0)
        res = self.tmpfile.read()
        self.tmpfile.seek(0)
        self.tmpfile.truncate()
        return res

    def writeorg(self, data: str) -> None:
        """Write to original file descriptor."""
        self._assert_state("writeorg", ("started", "suspended"))
        # XXX use encoding of original stream
        os.write(self.targetfd_save, data.encode("utf-8"))
```

--------------------------------

### Access Logs from Different Test Stages with get_records()

Source: https://docs.pytest.org/en/stable/how-to/logging

Explains how to access log records from specific test stages (setup, call, teardown) using the `caplog.get_records(when)` method. This is valuable for ensuring no unexpected warnings or errors occur during different phases of a test, especially when using fixtures.

```python
import pytest
import logging

def create_window():
    # Placeholder for window creation
    return object()

@pytest.fixture
def window(caplog):
    window = create_window()
    yield window
    for when in ("setup", "call"):
        messages = [
            x.message for x in caplog.get_records(when) if x.levelno == logging.WARNING
        ]
        if messages:
            pytest.fail(f"warning messages encountered during testing: {messages}")
```

--------------------------------

### Get First Non-Fixture Function (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/python

Retrieves the first attribute from an object that matches a given name and is not marked as a pytest fixture. This is used to find xUnit-style setup/teardown methods.

```python
from typing import Iterable

# Assuming fixtures and getattr are defined elsewhere
# import fixtures
# from some_module import getattr

def _get_first_non_fixture_func(obj: object, names: Iterable[str]) -> object | None:
    """Return the attribute from the given object to be used as a setup/teardown
    xunit-style function, but only if not marked as a fixture to avoid calling it twice.
    """
    for name in names:
        meth: object | None = getattr(obj, name, None)
        if meth is not None and fixtures.getfixturemarker(meth) is None:
            return meth
    return None
```

--------------------------------

### Pin setuptools version for setup.cfg support

Source: https://docs.pytest.org/en/stable/changelog

Pins the `setuptools` version to `>=40.0` to ensure support for `py_modules` specified in `setup.cfg`. This is important for projects using `setup.cfg` for package configuration.

```python
# This is a dependency version change, not a code snippet.
```

--------------------------------

### Pytest Run Test Protocol Hook (pytest_runtest_protocol)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

The `pytest_runtest_protocol` hook defines the sequence of actions for running a single test item, including setup, call, and teardown phases. It involves calling other hooks like `pytest_runtest_setup`, `pytest_runtest_call`, `pytest_runtest_teardown`, and `pytest_runtest_makereport`. The hook stops at the first non-None result.

```python
from _pytest.nodes import Item
from pluggy import Hookspec

@Hookspec(firstresult=True)
def pytest_runtest_protocol(item: Item, nextitem: Item | None) -> object | None:
    """Perform the runtest protocol for a single test item."""
    pass
```

--------------------------------

### Illustrating Type Checking Benefits for Production Code

Source: https://docs.pytest.org/en/stable/explanation/types

Provides an example of production code where type hints can catch bugs that might be missed by tests. This highlights how type checkers can identify potential `None` return values, even with 100% test coverage.

```python
def get_caption(target: int, items: list[tuple[int, str]]) -> str:
    for value, caption in items:
        if value == target:
            return caption
```

--------------------------------

### Corrected Pytest Test with Assert Statement

Source: https://docs.pytest.org/en/stable/how-to/assert

Provides the corrected version of the previous example, replacing the incorrect `return` statement with an `assert` statement. This ensures the test fails as expected based on the assertion's outcome.

```python
@pytest.mark.parametrize(
    ["a", "b", "result"],
    [
        [1, 2, 5],
        [2, 3, 8],
        [5, 3, 18],
    ],
)
def test_foo(a, b, result):
    assert foo(a, b) == result
```

--------------------------------

### Get Closest Marker by Name (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

Retrieves the first marker matching the specified name, searching from the closest node (e.g., function) up to the farthest (e.g., module). Returns `None` or a default value if no marker is found.

```python
@overload
def get_closest_marker(self, name: str) -> Mark | None: ...

@overload
def get_closest_marker(self, name: str, default: Mark) -> Mark: ...

def get_closest_marker(self, name: str, default: Mark | None = None) -> Mark | None:
    """Return the first marker matching the name, from closest (for
    example function) to farther level (for example module level).

    :param default: Fallback return value if no marker was found.
    :param name: Name to filter by.
    """
    return next(self.iter_markers(name=name), default)
```

--------------------------------

### Create Hook Recorder for Plugin Manager

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Creates and returns a HookRecorder instance associated with a PytestPluginManager. It also registers a finalizer to finish recording when the test session ends.

```python
def make_hook_recorder(self, pluginmanager: PytestPluginManager) -> HookRecorder:
    """Create a new :class:`HookRecorder` for a :class:`PytestPluginManager`. """
    pluginmanager.reprec = reprec = HookRecorder(pluginmanager, _ispytest=True)  # type: ignore[attr-defined]
    self._request.addfinalizer(reprec.finish_recording)
    return reprec
```

--------------------------------

### Example test file test_first.py for Custom Directory Collection

Source: https://docs.pytest.org/en/stable/example/customdirectory

A simple Python test file containing a single test function `test_1`. This file is intended to be collected by a custom pytest directory collector.

```python
# content of test_first.py
from __future__ import annotations


def test_1():
    pass

```

--------------------------------

### Add Pytest Options and Configuration

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

The `pytest_addoption` hook is called once at the start of a test run to register command-line options and configuration values. Use `parser.addoption` for command-line options and `parser.addini` for configuration files. Options are accessed via `config.getoption` and `config.getini`. This hook is incompatible with hook wrappers and is called for initial conftests.

```python
@hookspec(historic=True)
def pytest_addoption(parser: Parser, pluginmanager: PytestPluginManager) -> None:
    """Register argparse-style options and config-style config values,
    called once at the beginning of a test run.

    :param parser:
        To add command line options, call
        :py:func:`parser.addoption(...) <pytest.Parser.addoption>`.
        To add config-file values call :py:func:`parser.addini(...)
        <pytest.Parser.addini>`.

    :param pluginmanager:
        The pytest plugin manager, which can be used to install :py:func:`~pytest.hookspec`'s
        or :py:func:`~pytest.hookimpl`'s and allow one plugin to call another plugin's hooks
        to change how command line options are added.

    Options can later be accessed through the
    :py:class:`config <pytest.Config>` object, respectively:

    - :py:func:`config.getoption(name) <pytest.Config.getoption>` to
      retrieve the value of a command line option.

    - :py:func:`config.getini(name) <pytest.Config.getini>` to retrieve
      a value read from a configuration file.

    The config object is passed around on many internal objects via the ``.config``
    attribute or can be retrieved as the ``pytestconfig`` fixture.

    .. note::
        This hook is incompatible with hook wrappers.

    Use in conftest plugins
    =======================

    If a conftest plugin implements this hook, it will be called immediately
    when the conftest is registered.

    This hook is only called for :ref:`initial conftests <pluginorder>`.
    """
    pass
```

--------------------------------

### Testing Expected Exceptions - Did Not Raise (Python)

Source: https://docs.pytest.org/en/stable/example/reportingdemo

This example demonstrates a 'Failed: DID NOT RAISE' error. It occurs when a test expects a specific exception (OSError) to be raised, but the code under test does not raise any exception.

```python
raises(OSError, int, "3")
```

--------------------------------

### Get Unpacked Marks from Object in Python

Source: https://docs.pytest.org/en/stable/_modules/_pytest/mark/structures

Shows how to retrieve all marks applied to a Python object (function or class) using `get_unpacked_marks`. It supports considering the Method Resolution Order (MRO) for classes.

```python
import pytest

@pytest.mark.MARK_A
@pytest.mark.MARK_B(value=1)
class MyClass:
    @pytest.mark.MARK_C
    def test_method(self):
        pass

# Get marks for the class (including MRO if applicable)
class_marks = pytest.get_unpacked_marks(MyClass)

# Get marks for a method
method_marks = pytest.get_unpacked_marks(MyClass.test_method)

print(f"Class marks: {class_marks}")
print(f"Method marks: {method_marks}")

```

--------------------------------

### Example test file test_second.py for Custom Directory Collection

Source: https://docs.pytest.org/en/stable/example/customdirectory

A simple Python test file containing a single test function `test_2`. This file is intended to be collected by a custom pytest directory collector.

```python
# content of test_second.py
from __future__ import annotations


def test_2():
    pass

```

--------------------------------

### Add Directories to Python Search Path (TOML)

Source: https://docs.pytest.org/en/stable/reference/reference

Configures directories to be added to Python's search path for modules. This TOML example adds 'src1' and 'src2' to the head of sys.path for the test session.

```toml
[pytest]
pythonpath = ["src1", "src2"]

```

--------------------------------

### Pytest Configuration in pytest.ini

Source: https://docs.pytest.org/en/stable/reference/customize

Example of configuring pytest using a pytest.ini file. This format takes precedence over most other files (except .toml) and allows specifying minimum version, additional options, and test paths. Supports INI-style configuration.

```ini
# pytest.ini or .pytest.ini
[pytest]
minversion = 6.0
addopts = -ra -q
testpaths =
    tests
    integration
```

--------------------------------

### Pytest Cache Command Line Main Entry

Source: https://docs.pytest.org/en/stable/_modules/_pytest/cacheprovider

This Python function, `pytest_cmdline_main`, acts as an entry point for pytest commands related to the cache. It specifically handles the `--cache-show` option, wrapping the session with the `cacheshow` function if the option is present and the help flag is not set.

```python
def pytest_cmdline_main(config: Config) -> int | ExitCode | None:
    if config.option.cacheshow and not config.option.help:
        from _pytest.main import wrap_session

        return wrap_session(config, cacheshow)
    return None
```

--------------------------------

### Clear Captured Log Records and Text

Source: https://docs.pytest.org/en/stable/_modules/_pytest/logging

Resets the list of captured log records and any captured log text. This is useful for starting fresh within a test.

```python
self.handler.clear()
```

--------------------------------

### Get Pytest Worker Information Line

Source: https://docs.pytest.org/en/stable/_modules/_pytest/reports

Retrieves and formats worker information for a pytest node. It caches the formatted string to avoid repeated computations. This function is crucial for displaying worker-specific details in test reports.

```python
def getworkerinfoline(node):
    try:
        return node._workerinfocache
    except AttributeError:
        d = node.workerinfo
        ver = "{}.{}.{}".format(*d["version_info"][:3])
        node._workerinfocache = s = "[{}] {} -- Python {} {}".format(
            d["id"], d["sysplatform"], ver, d["executable"]
        )
        return s
```

--------------------------------

### Load Initial Conftests in Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Loads initial conftest files early in the pytest startup process. It pre-parses command-line arguments to determine test paths and other necessary information for discovering and loading conftest modules. This hook ensures that configuration from conftest files is available before the full argument parsing is complete.

```python
@hookimpl(trylast=True)
def pytest_load_initial_conftests(self, early_config: Config) -> None:
    # We haven't fully parsed the command line arguments yet, so
    # early_config.args it not set yet. But we need it for
    # discovering the initial conftests. So "pre-run" the logic here.
    # It will be done for real in `parse()`.
    args, _args_source = early_config._decide_args(
        args=early_config.known_args_namespace.file_or_dir,
        pyargs=early_config.known_args_namespace.pyargs,
        testpaths=early_config.getini("testpaths"),
        invocation_dir=early_config.invocation_params.dir,
        rootpath=early_config.rootpath,
        warn=False,
    )
    self.pluginmanager._set_initial_conftests(
        args=args,
        pyargs=early_config.known_args_namespace.pyargs,
        noconftest=early_config.known_args_namespace.noconftest,
        rootpath=early_config.rootpath,
        confcutdir=early_config.known_args_namespace.confcutdir,
        invocation_dir=early_config.invocation_params.dir,
        importmode=early_config.known_args_namespace.importmode,
        consider_namespace_packages=early_config.getini(
            "consider_namespace_packages"
        ),
    )
```

--------------------------------

### Pytest Fixture Scope Example

Source: https://docs.pytest.org/en/stable/reference/fixtures

Demonstrates fixture availability within different classes and modules in pytest. Fixtures defined within a class are local to that class, while module-scoped fixtures are available to all tests in the module.

```python
from __future__ import annotations

import pytest


@pytest.fixture
def order():
    return []


@pytest.fixture
def outer(order, inner):
    order.append("outer")


class TestOne:
    @pytest.fixture
    def inner(self, order):
        order.append("one")

    def test_order(self, order, outer):
        assert order == ["one", "outer"]


class TestTwo:
    @pytest.fixture
    def inner(self, order):
        order.append("two")

    def test_order(self, order, outer):
        assert order == ["two", "outer"]

```

--------------------------------

### Pytest Configuration in pyproject.toml (Native TOML)

Source: https://docs.pytest.org/en/stable/reference/customize

Example of configuring pytest using pyproject.toml with native TOML types, supported since pytest 9.0. This allows specifying minimum version, additional options, and test paths.

```toml
# pyproject.toml
[tool.pytest]
minversion = "9.0"
addopts = ["-ra", "-q"]
testpaths = [
    "tests",
    "integration",
]
```

--------------------------------

### Deprecated Inicfg Proxy for Config Compatibility

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

This class provides a compatibility layer for a deprecated `Config.inicfg` attribute. It implements the MutableMapping interface to allow dictionary-like access to the underlying configuration values, translating get, set, and delete operations to the new configuration structure.

```python
class _DeprecatedInicfgProxy(MutableMapping[str, Any]):
    """Compatibility proxy for the deprecated Config.inicfg."""

    __slots__ = ("_config",)

    def __init__(self, config: Config) -> None:
        self._config = config

    def __getitem__(self, key: str) -> Any:
        return self._config._inicfg[key].value

    def __setitem__(self, key: str, value: Any) -> None:
        self._config._inicfg[key] = ConfigValue(value, origin="override", mode="toml")

    def __delitem__(self, key: str) -> None:
        del self._config._inicfg[key]

    def __iter__(self) -> Iterator[str]:
        return iter(self._config._inicfg)

    def __len__(self) -> int:
        return len(self._config._inicfg)
```

--------------------------------

### Using pytest features in unittest.TestCase subclasses

Source: https://docs.pytest.org/en/stable/contents

Demonstrates how to integrate pytest's advanced features, such as fixtures and marks, directly into existing Python unittest.TestCase classes. This allows for a gradual migration or leveraging pytest's capabilities within a unittest structure.

```python
import pytest
import unittest

class MyTests(unittest.TestCase):

    @pytest.fixture
    def my_fixture(self):
        return 42

    @pytest.mark.skip(reason="demonstrating marks")
    def test_with_fixture_and_mark(self, my_fixture):
        self.assertEqual(my_fixture, 42)

```

--------------------------------

### Pytest Hook: pytest_collectstart

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

Implements the pytest_collectstart hook, which is called when a collector starts its collection process. It receives the collector object as an argument. This hook can be used in conftest plugins to react to the beginning of collection for a specific collector.

```python
def pytest_collectstart(collector: Collector) -> None:
    """Collector starts collecting.

    :param collector:
        The collector.

    Use in conftest plugins
    =======================

    Any conftest file can implement this hook. For a given collector, only
    conftest files in the collector's directory and its parent directories are
    consulted.
    """
    pass
```

--------------------------------

### Get Modules for cx_freeze with pytest.freeze_includes

Source: https://docs.pytest.org/en/stable/reference/reference

Returns a list of module names that pytest uses, intended for inclusion in cx_freeze builds. This function helps ensure that necessary pytest modules are packaged correctly.

```python
pytest.freeze_includes()
```

--------------------------------

### Create Python Files with pytester.makepyfile

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `makepyfile` method is a shortcut for `makefile` with a `.py` extension. It defaults to creating a file named after the test function, overwriting existing files. It can create multiple files using keyword arguments.

```python
def makepyfile(self, *args, **kwargs) -> Path:
    r"""Shortcut for .makefile() with a .py extension.

    Defaults to the test name with a '.py' extension, e.g test_foobar.py, overwriting
    existing files.

    Examples:

    .. code-block:: python

        def test_something(pytester):
            # Initial file is created test_something.py.
            pytester.makepyfile("foobar")
            # To create multiple files, pass kwargs accordingly.
            pytester.makepyfile(custom="foobar")
            # At this point, both 'test_something.py' & 'custom.py' exist in the test directory.

    """
    return self._makefile(".py", args, kwargs)
```

--------------------------------

### Pytest Configure Hook for Namespace Injection (Python)

Source: https://docs.pytest.org/en/stable/deprecations

An alternative to `pytest_namespace`, this example shows how to inject symbols into pytest's namespace during the `pytest_configure` hook. This method is recommended for plugin authors as a stopgap measure.

```python
import pytest


def pytest_configure():
    pytest.my_symbol = MySymbol()
```

--------------------------------

### Get Verbosity Level - Python

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Retrieves the verbosity level for a specific type or the global level. It checks for type-specific configurations in the ini file and falls back to the global verbosity if no specific configuration is found or if 'auto' is specified.

```python
def get_verbosity(self, verbosity_type: str | None = None) -> int:
    r"""Retrieve the verbosity level for a fine-grained verbosity type.

    :param verbosity_type: Verbosity type to get level for. If a level is
        configured for the given type, that value will be returned. If the
        given type is not a known verbosity type, the global verbosity
        level will be returned. If the given type is None (default), the
        global verbosity level will be returned.

    To configure a level for a fine-grained verbosity type, the
    configuration file should have a setting for the configuration name
    and a numeric value for the verbosity level. A special value of "auto"
    can be used to explicitly use the global verbosity level.

    Example:

    .. tab:: toml

        .. code-block:: toml

            [tool.pytest]
            verbosity_assertions = 2

    .. tab:: ini

        .. code-block:: ini

            [pytest]
            verbosity_assertions = 2

    .. code-block:: console

        pytest -v

    .. code-block:: python

        print(config.get_verbosity())  # 1
        print(config.get_verbosity(Config.VERBOSITY_ASSERTIONS))  # 2
    """
    global_level = self.getoption("verbose", default=0)
    assert isinstance(global_level, int)
    if verbosity_type is None:
        return global_level

    ini_name = Config._verbosity_ini_name(verbosity_type)
    if ini_name not in self._parser._inidict:
        return global_level

    level = self.getini(ini_name)
    if level == Config._VERBOSITY_INI_DEFAULT:
        return global_level

    return int(level)

```

--------------------------------

### Add Directories to Python Search Path (INI)

Source: https://docs.pytest.org/en/stable/reference/reference

Configures directories to be added to Python's search path for modules. This INI example adds 'src1' and 'src2' to the head of sys.path for the test session.

```ini
[pytest]
pythonpath = src1 src2

```

--------------------------------

### Create and write to a temporary file using tmp_path fixture in Python

Source: https://docs.pytest.org/en/stable/how-to/tmp_path

Demonstrates how to use the `tmp_path` fixture to create a temporary directory, a subdirectory, write content to a file within it, and then read and assert its content. This fixture provides a `pathlib.Path` object unique to each test function. It also shows how to inspect the contents of the temporary directory.

```python
# content of test_tmp_path.py
CONTENT = "content"

def test_create_file(tmp_path):
    d = tmp_path / "sub"
    d.mkdir()
    p = d / "hello.txt"
    p.write_text(CONTENT, encoding="utf-8")
    assert p.read_text(encoding="utf-8") == CONTENT
    assert len(list(tmp_path.iterdir())) == 1
    assert 0

```

--------------------------------

### Mark a test function to be skipped unconditionally

Source: https://docs.pytest.org/en/stable/how-to/skipping

This example demonstrates how to mark a test function with the `pytest.mark.skip` decorator. An optional reason can be provided to explain why the test is being skipped. This is useful for tests that are not currently testable.

```python
import pytest

@pytest.mark.skip(reason="no way of currently testing this")
def test_the_unknown():
    ... 
```

--------------------------------

### Pytest Fixture Execution and Caching

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

Manages the execution of a fixture, including checking for cached results, setting up dependent fixtures, running the fixture function, and caching the result. It ensures finalizers are added even if setup fails.

```python
[docs]
    def execute(self, request: SubRequest) -> FixtureValue:
        """Return the value of this fixture, executing it if not cached."""
        # Ensure that the dependent fixtures requested by this fixture are loaded.
        # This needs to be done before checking if we have a cached value, since
        # if a dependent fixture has their cache invalidated, e.g. due to
        # parametrization, they finalize themselves and fixtures depending on it
        # (which will likely include this fixture) setting `self.cached_result = None`.
        # See #4871
        requested_fixtures_that_should_finalize_us = []
        for argname in self.argnames:
            fixturedef = request._get_active_fixturedef(argname)
            # Saves requested fixtures in a list so we later can add our finalizer
            # to them, ensuring that if a requested fixture gets torn down we get torn
            # down first. This is generally handled by SetupState, but still currently
            # needed when this fixture is not parametrized but depends on a parametrized
            # fixture.
            requested_fixtures_that_should_finalize_us.append(fixturedef)

        # Check for (and return) cached value/exception.
        if self.cached_result is not None:
            request_cache_key = self.cache_key(request)
            cache_key = self.cached_result[1]
            try:
                # Attempt to make a normal == check: this might fail for objects
                # which do not implement the standard comparison (like numpy arrays -- #6497).
                cache_hit = bool(request_cache_key == cache_key)
            except (ValueError, RuntimeError):
                # If the comparison raises, use 'is' as fallback.
                cache_hit = request_cache_key is cache_key

            if cache_hit:
                if self.cached_result[2] is not None:
                    exc, exc_tb = self.cached_result[2]
                    raise exc.with_traceback(exc_tb)
                else:
                    return self.cached_result[0]
            # We have a previous but differently parametrized fixture instance
            # so we need to tear it down before creating a new one.
            self.finish(request)
            assert self.cached_result is None

        # Add finalizer to requested fixtures we saved previously.
        # We make sure to do this after checking for cached value to avoid
        # adding our finalizer multiple times. (#12135)
        finalizer = functools.partial(self.finish, request=request)
        for parent_fixture in requested_fixtures_that_should_finalize_us:
            parent_fixture.addfinalizer(finalizer)

        ihook = request.node.ihook
        try:
            # Setup the fixture, run the code in it, and cache the value
            # in self.cached_result.
            result: FixtureValue = ihook.pytest_fixture_setup(
                fixturedef=self, request=request
            )
        finally:
            # Schedule our finalizer, even if the setup failed.
            request.node.addfinalizer(finalizer)

        return result
```

--------------------------------

### Binary Stream Capture (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Captures binary data from system streams. It extends SysCaptureBase and provides implementations for `snap` to retrieve binary data and `writeorg` to write binary data to the original stream.

```python
class SysCaptureBinary(SysCaptureBase[bytes]):
    EMPTY_BUFFER = b""

    def snap(self) -> bytes:
        self._assert_state("snap", ("started", "suspended"))
        self.tmpfile.seek(0)
        res = self.tmpfile.buffer.read()
        self.tmpfile.seek(0)
        self.tmpfile.truncate()
        return res

    def writeorg(self, data: bytes) -> None:
        self._assert_state("writeorg", ("started", "suspended"))
        self._old.flush()
        self._old.buffer.write(data)
        self._old.buffer.flush()

```

--------------------------------

### Pytest Session Start Hook: pytest_sessionstart

Source: https://docs.pytest.org/en/stable/reference/reference

Called after the Session object has been created and before performing collection and entering the run test loop. This hook is only called for initial conftests and receives the pytest session object as a parameter.

```python
def pytest_sessionstart(session):
    """Called after the Session object has been created and before performing collection and entering the run test loop."""
    pass
```

--------------------------------

### Example of a Missed Bug Without Type Checking

Source: https://docs.pytest.org/en/stable/explanation/types

Demonstrates a test case with 100% coverage that fails to catch a bug related to a potential `None` return value, illustrating the importance of type checking for robustness.

```python
def test_get_caption() -> None:
    assert get_caption(10, [(1, "foo"), (10, "bar")]) == "bar"
```

--------------------------------

### Create Reusable Mock Environment Fixtures

Source: https://docs.pytest.org/en/stable/how-to/monkeypatch

Illustrates how to encapsulate environment variable patching into pytest fixtures. This promotes code reusability and makes tests cleaner by abstracting the mocking logic. Separate fixtures are created for setting and unsetting the 'USER' environment variable.

```python
# contents of our test file e.g. test_code.py
import pytest


@pytest.fixture
def mock_env_user(monkeypatch):
    monkeypatch.setenv("USER", "TestingUser")


@pytest.fixture
def mock_env_missing(monkeypatch):
    monkeypatch.delenv("USER", raising=False)


# notice the tests reference the fixtures for mocks
def test_upper_to_lower(mock_env_user):
    assert get_os_user_lower() == "testinguser"


def test_raise_exception(mock_env_missing):
    with pytest.raises(OSError):
        _ = get_os_user_lower()
```

--------------------------------

### Integrate pytest fixtures into unittest.TestCase subclasses

Source: https://docs.pytest.org/en/stable/how-to/unittest

This example demonstrates how to use a pytest fixture (db_class) within a unittest.TestCase subclass. The fixture is defined in conftest.py and provides a class-cached database object that can be referenced in tests.

```python
# content of conftest.py

# we define a fixture function below and it will be "used" by
```

--------------------------------

### String Representation of Pytester

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Returns a string representation of the Pytester instance, including the path to its temporary directory.

```python
def __repr__(self) -> str:
    return f"<Pytester {self.path!r}>"
```

--------------------------------

### Inline Doctest Option: Ignore Exception Detail

Source: https://docs.pytest.org/en/stable/how-to/doctest

This example illustrates how to apply a doctest option directly within a docstring using an inline comment. The '# doctest: +IGNORE_EXCEPTION_DETAIL' flag tells doctest to ignore the specifics of the exception traceback during comparison.

```python
>>> something_that_raises()  # doctest: +IGNORE_EXCEPTION_DETAIL
Traceback (most recent call last):
ValueError: ...

```

--------------------------------

### Create Config from Dictionary Arguments

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

A class method to create a `Config` object, typically used when running Pytest in a subprocess. It initializes a config object and updates its options from a dictionary.

```python
@classmethod
def fromdictargs(cls, option_dict: Mapping[str, Any], args: list[str]) -> Config:
    """Constructor usable for subprocesses."""
    config = get_config(args)
    config.option.__dict__.update(option_dict)
```

--------------------------------

### Implement a Pytest Hook in conftest.py

Source: https://docs.pytest.org/en/stable/how-to/writing_hook_functions

This snippet illustrates how a user or another plugin can implement a pytest hook by defining the function with the correct signature in their `conftest.py` file. This example implements the `pytest_my_hook` hook to print active hooks.

```python
def pytest_my_hook(config):
    """
    Print all active hooks to the screen.
    """
    print(config.hook)

```

--------------------------------

### Integrate Pytest into a Frozen Application

Source: https://docs.pytest.org/en/stable/example/simple

This Python code illustrates how to embed pytest execution within a frozen application (e.g., created with PyInstaller). It checks command-line arguments to determine if pytest should be run and allows passing plugins like 'pytest-timeout' to pytest.main.

```python
# contents of app_main.py
import sys

import pytest_timeout  # Third party plugin

if len(sys.argv) > 1 and sys.argv[1] == "--pytest":
    import pytest

    sys.exit(pytest.main(sys.argv[2:], plugins=[pytest_timeout]))
else:
    # normal application execution: at this point argv can be parsed
    # by your argument-parsing library of choice as usual
    ...

```

--------------------------------

### Get Representation of Expected Exception (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/raises

This static method provides a string representation for expected exceptions. If the input is a type, it returns the type's name; otherwise, it returns the standard representation of the object.

```python
    @staticmethod
    def _repr_expected(e: type[BaseException] | AbstractRaises[BaseException]) -> str:
        """Get the repr of an expected type/RaisesExc/RaisesGroup, but we only want
        the name if it's a type"""
        if isinstance(e, type):
            return _exception_type_name(e)
        return repr(e)
```

--------------------------------

### Run Command with Timeout and Input Handling in Python

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Executes a command using subprocess.Popen, capturing stdout and stderr, and handling timeouts. It converts path-like arguments to strings and manages standard input based on the provided `stdin` parameter. This is the recommended method for running external commands.

```python
def run(
        self,
        *cmdargs: str | os.PathLike[str],
        timeout: float | None = None,
        stdin: NotSetType | bytes | IO[Any] | int = CLOSE_STDIN,
    ) -> RunResult:
        """Run a command with arguments.

        Run a process using :py:class:`subprocess.Popen` saving the stdout and
        stderr.

        :param cmdargs:
            The sequence of arguments to pass to :py:class:`subprocess.Popen`,
            with path-like objects being converted to :py:class:`str`
            automatically.
        :param timeout:
            The period in seconds after which to timeout and raise
            :py:class:`Pytester.TimeoutExpired`.
        :param stdin:
            Optional standard input.

            - If it is ``CLOSE_STDIN`` (Default), then this method calls
              :py:class:`subprocess.Popen` with ``stdin=subprocess.PIPE``, and
              the standard input is closed immediately after the new command is
              started.

            - If it is of type :py:class:`bytes`, these bytes are sent to the
              standard input of the command.

            - Otherwise, it is passed through to :py:class:`subprocess.Popen`.
              For further information in this case, consult the document of the
              ``stdin`` parameter in :py:class:`subprocess.Popen`.
        :type stdin: _pytest.compat.NotSetType | bytes | IO[Any] | int
        :returns:
            The result.

        """
        __tracebackhide__ = True

        cmdargs = tuple(os.fspath(arg) for arg in cmdargs)
        p1 = self.path.joinpath("stdout")
        p2 = self.path.joinpath("stderr")
        print("running:", *cmdargs)
        print("     in:", Path.cwd())

        with p1.open("w", encoding="utf8") as f1, p2.open("w", encoding="utf8") as f2:
            instant = timing.Instant()
            popen = self.popen(
                cmdargs,
                stdin=stdin,
                stdout=f1,
                stderr=f2,
            )
            if popen.stdin is not None:
                popen.stdin.close()

            def handle_timeout() -> None:
                __tracebackhide__ = True

                timeout_message = f"{timeout} second timeout expired running: {cmdargs}"

                popen.kill()
                popen.wait()
                raise self.TimeoutExpired(timeout_message)

            if timeout is None:
                ret = popen.wait()
            else:
                try:
                    ret = popen.wait(timeout)
                except subprocess.TimeoutExpired:
                    handle_timeout()
            f1.flush()
            f2.flush()

        with p1.open(encoding="utf8") as f1, p2.open(encoding="utf8") as f2:
            out = f1.read().splitlines()
            err = f2.read().splitlines()

        self._dump_lines(out, sys.stdout)
        self._dump_lines(err, sys.stderr)

        with contextlib.suppress(ValueError):
            ret = ExitCode(ret)
        return RunResult(ret, out, err, instant.elapsed().seconds)
```

--------------------------------

### Invoke pytest from the command line or Python

Source: https://docs.pytest.org/en/stable/announce/release-2.0.0

Demonstrates how to run pytest tests. It can be invoked directly from the command line using `python -m pytest` or programmatically from a Python script using `pytest.main()`.

```bash
python -m pytest      # on all pythons >= 2.5

```

```python
import pytest ; pytest.main(arglist, pluginlist)

```

--------------------------------

### Get Raw Skip Reason from Test Report (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

Extracts the raw reason string for a skipped or xfailed/xpassed test report. It handles different report structures and formats the reason string for clarity. This is useful for reporting or debugging skipped tests.

```python
def _get_raw_skip_reason(report: TestReport) -> str:
    """Get the reason string of a skip/xfail/xpass test report.

    The string is just the part given by the user.
    """
    if hasattr(report, "wasxfail"):
        reason = report.wasxfail
        if reason.startswith("reason: "):
            reason = reason[len("reason: ") :]
        return reason
    else:
        assert report.skipped
        assert isinstance(report.longrepr, tuple)
        _, _, reason = report.longrepr
        if reason.startswith("Skipped: "):
            reason = reason[len("Skipped: ") :]
        elif reason == "Skipped":
            reason = ""
        return reason
```

--------------------------------

### Configure JUnit XML Reporting (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/junitxml

Illustrates the `pytest_configure` hook, which is responsible for setting up the JUnit XML logger when pytest starts. It checks if an output path is provided and if the current node is not a worker node (to prevent duplicate reports with pytest-xdist). If conditions are met, it initializes the `LogXML` object and registers it as a plugin.

```python
def pytest_configure(config: Config) -> None:
    xmlpath = config.option.xmlpath
    # Prevent opening xmllog on worker nodes (xdist).
    if xmlpath and not hasattr(config, "workerinput"):
        junit_family = config.getini("junit_family")
        config.stash[xml_key] = LogXML(
            xmlpath,
            config.option.junitprefix,
            config.getini("junit_suite_name"),
            config.getini("junit_logging"),
            config.getini("junit_duration_report"),
            junit_family,
            config.getini("junit_log_passing_tests"),
        )
        config.pluginmanager.register(config.stash[xml_key])
```

--------------------------------

### Parametrize All Tests in a Module (Python)

Source: https://docs.pytest.org/en/stable/how-to/parametrize

Demonstrates how to parametrize all tests within a Python module by assigning a parametrize marker to the global `pytestmark` variable. This applies the specified parameters to every test function and method in the module.

```python
import pytest

pytestmark = pytest.mark.parametrize("n,expected", [(1, 2), (3, 4)])


class TestClass:
    def test_simple_case(self, n, expected):
        assert n + 1 == expected

    def test_weird_simple_case(self, n, expected):
        assert (n * 1) + 1 == expected
```

--------------------------------

### Pytest Hooks for Capture Management

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

This snippet demonstrates various Pytest hooks used to manage and integrate capture functionality within the testing process. It includes hooks for collecting reports, running test phases (setup, call, teardown), and handling internal errors or keyboard interrupts.

```python
    self.resume_global_capture()
    self.activate_fixture()
    try:
        yield
    finally:
        self.deactivate_fixture()
        self.suspend_global_capture(in_=False)

        out, err = self.read_global_capture()
        item.add_report_section(when, "stdout", out)
        item.add_report_section(when, "stderr", err)
```

```python
@hookimpl(wrapper=True)
def pytest_make_collect_report(
    self, collector: Collector
) -> Generator[None, CollectReport, CollectReport]:
    if isinstance(collector, File):
        self.resume_global_capture()
        try:
            rep = yield
        finally:
            self.suspend_global_capture()
        out, err = self.read_global_capture()
        if out:
            rep.sections.append(("Captured stdout", out))
        if err:
            rep.sections.append(("Captured stderr", err))
    else:
        rep = yield
    return rep
```

```python
@hookimpl(wrapper=True)
def pytest_runtest_setup(self, item: Item) -> Generator[None]:
    with self.item_capture("setup", item):
        return (yield)
```

```python
@hookimpl(wrapper=True)
def pytest_runtest_call(self, item: Item) -> Generator[None]:
    with self.item_capture("call", item):
        return (yield)
```

```python
@hookimpl(wrapper=True)
def pytest_runtest_teardown(self, item: Item) -> Generator[None]:
    with self.item_capture("teardown", item):
        return (yield)
```

```python
@hookimpl(tryfirst=True)
def pytest_keyboard_interrupt(self) -> None:
    self.stop_global_capturing()
```

```python
@hookimpl(tryfirst=True)
def pytest_internalerror(self) -> None:
    self.stop_global_capturing()
```

--------------------------------

### Pytest Hook Wrapper Example

Source: https://docs.pytest.org/en/stable/how-to/writing_hook_functions

Demonstrates how to define a pytest hook wrapper using a generator function. The wrapper executes code before yielding, then executes the next hook implementation, and finally executes code after the yield point, processing the result or exception.

```python
import pytest


@pytest.hookimpl(wrapper=True)
def pytest_pyfunc_call(pyfuncitem):
    do_something_before_next_hook_executes()

    # If the outcome is an exception, will raise the exception.
    res = yield

    new_res = post_process_result(res)

    # Override the return value to the plugin system.
    return new_res

```

--------------------------------

### Get Pytest Option Group

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config/argparsing

Retrieves or creates a named option group for organizing command-line arguments. It allows specifying a description and ordering relative to other groups. The returned group object has an `addoption` method.

```python
    @property
    def prog(self) -> str:
        return self.optparser.prog

    @prog.setter
    def prog(self, value: str) -> None:
        self.optparser.prog = value

    def processoption(self, option: Argument) -> None:
        if self._processopt:
            if option.dest:
                self._processopt(option)




    def getgroup(
        self,
        name: str,
        description: str = "",
        after: str | None = None
    ) -> OptionGroup:
        """Get (or create) a named option Group.

        :param name: Name of the option group.
        :param description: Long description for --help output.
        :param after: Name of another group, used for ordering --help output.
        :returns: The option group.

        The returned group object has an ``addoption`` method with the same
        signature as :func:`parser.addoption <pytest.Parser.addoption>` but
        will be shown in the respective group in the output of
        ``pytest --help``.
        """
        for group in self._groups:
            if group.name == name:
                return group

        arggroup = self.optparser.add_argument_group(description or name)
        group = OptionGroup(arggroup, name, self, _ispytest=True)
        i = 0
        for i, grp in enumerate(self._groups):
            if grp.name == after:
                break
        self._groups.insert(i + 1, group)
        # argparse doesn't provide a way to control `--help` order, so must
        # access its internals ☹.
        self.optparser._action_groups.insert(i + 1, self.optparser._action_groups.pop())
        return group

```

--------------------------------

### Get Base Temporary Directory

Source: https://docs.pytest.org/en/stable/_modules/_pytest/tmpdir

Returns the base temporary directory path. If the base directory has not been set yet, it will be created. This method ensures that a base directory is available for creating temporary subdirectories.

```python
    def getbasetemp(self) -> Path:
        """Return the base temporary directory, creating it if needed.

        :returns:
            The base temporary directory.
        """
        if self._basetemp is not None:
            return self._basetemp

        if self._given_basetemp is not None:
            basetemp = self._given_basetemp

```

--------------------------------

### Use Fixtures from Other Projects with pytest_plugins

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Shows how to make fixtures from external projects available in your tests by defining `pytest_plugins` in your `conftest.py`. This is useful for projects that do not use entry points for fixture discovery.

```python
pytest_plugins = "mylibrary.fixtures"
```

--------------------------------

### Specify minimum required pytest version

Source: https://docs.pytest.org/en/stable/reference/reference

Sets the minimum pytest version required to run the tests. If the current pytest version is lower, the test run will fail. Example shows requiring version 3.0.

```toml
[pytest]
minversion = 3.0  # will fail if we run with pytest-2.8

```

```ini
[pytest]
minversion = 3.0  # will fail if we run with pytest-2.8

```

--------------------------------

### Get recorded hook calls by name

Source: https://docs.pytest.org/en/stable/reference/reference

Retrieves all recorded calls to hooks that match the specified names. This method allows filtering hook calls based on their names, returning a list of matching calls.

```python
getcalls(_names_)
```

--------------------------------

### Pytest Fixture Usage at Module Level with pytestmark

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Shows how to apply fixtures to all tests within a module by using `pytestmark = pytest.mark.usefixtures(...)`. This is a convenient way to ensure common fixtures are available across multiple tests in a file.

```python
import pytest


pytestmark = pytest.mark.usefixtures("cleandir")

def test_something():
    pass

def test_another_thing():
    pass
```

--------------------------------

### Inspect PYTEST_CURRENT_TEST with psutil

Source: https://docs.pytest.org/en/stable/example/simple

This Python snippet demonstrates how to iterate through running processes and inspect their environment variables to find the PYTEST_CURRENT_TEST, which indicates the currently executing pytest test. It requires the 'psutil' library.

```python
import psutil

for pid in psutil.pids():
    environ = psutil.Process(pid).environ()
    if "PYTEST_CURRENT_TEST" in environ:
        print(f'pytest process {pid} running: {environ["PYTEST_CURRENT_TEST"]}')

```

--------------------------------

### Iterate Fixture Chain (Pytest)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

Yields all `SubRequest` objects in the fixture chain, starting from the current request and moving up to the parent requests. This method is useful for traversing the hierarchy of fixtures. It explicitly excludes the `TopRequest` from the iteration.

```python
def _iter_chain(self) -> Iterator[SubRequest]:
        """Yield all SubRequests in the chain, from self up.

        Note: does *not* yield the TopRequest.
        """
        current = self
        while isinstance(current, SubRequest):
            yield current
            current = current._parent_request
```

--------------------------------

### Get or Create Node Reporter

Source: https://docs.pytest.org/en/stable/_modules/_pytest/junitxml

Retrieves an existing node reporter for a given report or creates a new one if it doesn't exist. It uses a tuple of nodeid and workernode as the key, accommodating xdist's distributed execution.

```python
def node_reporter(self, report: TestReport | str) -> _NodeReporter:
        nodeid: str | TestReport = getattr(report, "nodeid", report)
        # Local hack to handle xdist report order.
        workernode = getattr(report, "node", None)

        key = nodeid, workernode

        if key in self.node_reporters:
            # TODO: breaks for --dist=each
            return self.node_reporters[key]

        reporter = _NodeReporter(nodeid, self)

        self.node_reporters[key] = reporter
        self.node_reporters_ordered.append(reporter)

        return reporter
```

--------------------------------

### Invoke Hooks with pluginmanager in pytest_addoption

Source: https://docs.pytest.org/en/stable/changelog

The `pytest_addoption` hook now receives the `pluginmanager` as an argument, enabling hooks to be invoked during command-line option setup. This facilitates inter-plugin communication for sharing default values or option sets.

```python
def pytest_addoption(parser, pluginmanager):
    parser.addoption("--my-option", action="store", default="val", help="My option")
    # Use pluginmanager here to interact with other plugins
```

--------------------------------

### Create Python Packages with pytester.mkpydir

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `mkpydir` method creates a new Python package directory. This involves creating a directory and an empty `__init__.py` file within it, ensuring it's recognized as a package.

```python
def mkpydir(self, name: str | os.PathLike[str]) -> Path:
    """Create a new python package.

    This creates a (sub)directory with an empty ``__init__.py`` file so it
    gets recognised as a Python package.
    """
    p = self.path / name
    p.mkdir()
    p.joinpath("__init__.py").touch()
    return p
```

--------------------------------

### Get Fail Reason for Exception Matching

Source: https://docs.pytest.org/en/stable/_modules/_pytest/raises

Provides a property to retrieve the reason why an exception match failed. This is useful for debugging and providing informative error messages when the expected exception pattern or check condition is not met.

```python
@property
def fail_reason(self) -> str | None:
    """Set after a call to :meth:`matches` to give a human-readable reason for why the match failed.
    When used as a context manager the string will be printed as the reason for the
    test failing."""
    return self._fail_reason
```

--------------------------------

### Getting Collection Node from File Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Retrieves the collection node for a given file path using a Pytest config. It initializes a Pytest session and performs collection, returning the root collector or item. Requires a valid Pytest Config object.

```python
def getnode(self, config: Config, arg: str | os.PathLike[str]) -> Collector | Item:
    """Get the collection node of a file.

    :param config:
       A pytest config.
       See :py:meth:`parseconfig` and :py:meth:`parseconfigure` for creating it.
    :param arg:
        Path to the file.
    :returns:
        The node.
    """
    session = Session.from_config(config)
    assert "::" not in str(arg)
    p = Path(os.path.abspath(arg))
    config.hook.pytest_sessionstart(session=session)
    res = session.perform_collect([str(p)], genitems=False)[0]
    config.hook.pytest_sessionfinish(session=session, exitstatus=ExitCode.OK)
    return res

```

--------------------------------

### Pytest Compatibility Namespace (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Defines a compatibility namespace `cmdline` that exposes the `main` function as a static method. This is primarily for backward compatibility purposes.

```Python
class cmdline:
    main = staticmethod(main)
```

--------------------------------

### Get Fixture Callable - Pytest Internal

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

Retrieves the actual callable function for a fixture, ensuring it's bound to the correct instance. Handles cases where fixtures are defined outside of test classes.

```python
def get_actual_fixture_func(
    fixturedef: FixtureDef[FixtureValue],
    request: FixtureRequest
) -> _FixtureFunc[FixtureValue]:
    """Get the actual callable that can be called to obtain the fixture
    value."""
    fixturefunc = fixturedef.func
    # The fixture function needs to be bound to the actual
    # request.instance so that code working with "fixturedef" behaves
    # as expected.
    instance = request.instance
    if instance is not None:
        # Handle the case where fixture is defined not in a test class, but some other class
        # (for example a plugin class with a fixture), see #2270.
        if hasattr(fixturefunc, "__self__") and not isinstance(
            instance,
            fixturefunc.__self__.__class__,
        ):
            return fixturefunc
        fixturefunc = getimfunc(fixturedef.func)
        if fixturefunc != fixturedef.func:
            fixturefunc = fixturefunc.__get__(instance)
    return fixturefunc
```

--------------------------------

### Retrieve Verbosity Level in Pytest (Python)

Source: https://docs.pytest.org/en/stable/reference/reference

Shows how to get the current verbosity level using the pytest config object. It covers retrieving the global verbosity and specific verbosity types like assertions.

```python
print(config.get_verbosity())  # 1
print(config.get_verbosity(Config.VERBOSITY_ASSERTIONS))  # 2
```

--------------------------------

### Pytest FunctionDefinition: Non-Runnable Test Definitions

Source: https://docs.pytest.org/en/stable/_modules/_pytest/python

A temporary class representing function definitions within pytest. It inherits from Function but overrides `runtest` and `setup` to prevent execution, as these are not meant to be run as tests.

```python
class FunctionDefinition(Function):
    """This class is a stop gap solution until we evolve to have actual function
    definition nodes and manage to get rid of ``metafunc``."""

    def runtest(self) -> None:
        raise RuntimeError("function definitions are not supposed to be run as tests")

    setup = runtest
```

--------------------------------

### Example manifest.json for Custom Directory Collection

Source: https://docs.pytest.org/en/stable/example/customdirectory

This JSON file specifies a list of test files to be collected within a directory. It is used in conjunction with a custom pytest collector to control which files pytest discovers and runs.

```json
{
    "files": [
        "test_first.py",
        "test_second.py"
    ]
}

```

--------------------------------

### Parametrizing Fixtures with Iterators in Pytest

Source: https://docs.pytest.org/en/stable/changelog

Pytest now supports directly parametrizing fixtures using iterators. This is achieved by exploding the iterator into a list early in the process, allowing for more flexible fixture setup. This addresses issue #122.

```python
import pytest

@pytest.fixture(params=range(3))
def my_fixture(request):
    return request.param

def test_with_fixture(my_fixture):
    assert my_fixture in [0, 1, 2]
```

--------------------------------

### Skip an entire module conditionally

Source: https://docs.pytest.org/en/stable/how-to/skipping

This example demonstrates how to skip an entire Python module at import time using `pytest.skip()` with `allow_module_level=True`. The skip condition is checked using `sys.platform` to skip Windows-specific tests on non-Windows platforms.

```python
import sys
import pytest

if not sys.platform.startswith("win"):
    pytest.skip("skipping windows-only tests", allow_module_level=True)
```

--------------------------------

### Initialize Pytest Parser

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config/argparsing

Initializes the Parser for command-line arguments and config-file values. It sets up argument groups and registers options. Dependencies include `argparse`, `_pytest._io`, and `_pytest.deprecated`.

```python
from __future__ import annotations

import argparse
from collections.abc import Callable
from collections.abc import Mapping
from collections.abc import Sequence
import os
import sys
from typing import Any
from typing import final
from typing import Literal
from typing import NoReturn

from .exceptions import UsageError
import _pytest._io
from _pytest.deprecated import check_ispytest


FILE_OR_DIR = "file_or_dir"


class NotSet:
    def __repr__(self) -> str:
        return "<notset>"


NOT_SET = NotSet()




@final
class Parser:
    """Parser for command line arguments and config-file values.

    :ivar extra_info: Dict of generic param -> value to display in case
        there's an error processing the command line arguments.
    """

    def __init__(
        self,
        usage: str | None = None,
        processopt: Callable[[Argument], None] | None = None,
        *,
        _ispytest: bool = False,
    ) -> None:
        check_ispytest(_ispytest)

        from _pytest._argcomplete import filescompleter

        self._processopt = processopt
        self.extra_info: dict[str, Any] = {}
        self.optparser = PytestArgumentParser(self, usage, self.extra_info)
        anonymous_arggroup = self.optparser.add_argument_group("Custom options")
        self._anonymous = OptionGroup(
            anonymous_arggroup, "_anonymous", self, _ispytest=True
        )
        self._groups = [self._anonymous]
        file_or_dir_arg = self.optparser.add_argument(FILE_OR_DIR, nargs="*")
        file_or_dir_arg.completer = filescompleter  # type: ignore

        self._inidict: dict[str, tuple[str, str, Any]] = {}
        # Maps alias -> canonical name.
        self._ini_aliases: dict[str, str] = {}

```

--------------------------------

### Configure Warning Filters in pyproject.toml

Source: https://docs.pytest.org/en/stable/how-to/capture-warnings

Configure warning filters using the 'filterwarnings' option within the '[pytest]' section of your pyproject.toml file. This example demonstrates ignoring all UserWarnings and specific DeprecationWarnings, while treating other warnings as errors. Note the use of single quotes for raw strings in TOML.

```toml
[pytest]
filterwarnings = [
    "error",
    "ignore::UserWarning",
    'ignore:function ham\(\)\, is deprecated:DeprecationWarning',
]
```

--------------------------------

### Pytest Console Entry Point (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Provides the primary command-line entry point for pytest. This function is intended for direct execution and not for programmatic use. It handles standard output flushing and gracefully manages broken pipe errors.

```Python
def console_main() -> int:
    """The CLI entry point of pytest.

    This function is not meant for programmable use; use `main()` instead.
    """
    # https://docs.python.org/3/library/signal.html#note-on-sigpipe
    try:
        code = main()
        sys.stdout.flush()
        return code
    except BrokenPipeError:
        # Python flushes standard streams on exit; redirect remaining output
        # to devnull to avoid another BrokenPipeError at shutdown
        devnull = os.open(os.devnull, os.O_WRONLY)
        os.dup2(devnull, sys.stdout.fileno())
        return 1  # Python exits with error code 1 on EPIPE
```

--------------------------------

### MultiCapture Class for Managing Capture Streams in Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Manages multiple capture streams (input, output, error) for Pytest. It provides methods to start, suspend, resume, stop, and read from these streams. This class is crucial for handling complex capture scenarios.

```python
class MultiCapture(Generic[AnyStr]):
    _state = None
    _in_suspended = False

    def __init__(
        self,
        in_: CaptureBase[AnyStr] | None,
        out: CaptureBase[AnyStr] | None,
        err: CaptureBase[AnyStr] | None,
    ) -> None:
        self.in_: CaptureBase[AnyStr] | None = in_
        self.out: CaptureBase[AnyStr] | None = out
        self.err: CaptureBase[AnyStr] | None = err

    def __repr__(self) -> str:
        return (
            f"<MultiCapture out={self.out!r} err={self.err!r} in_={self.in_!r} "
            f"_state={self._state!r} _in_suspended={self._in_suspended!r}>"
        )

    def start_capturing(self) -> None:
        self._state = "started"
        if self.in_:
            self.in_.start()
        if self.out:
            self.out.start()
        if self.err:
            self.err.start()

    def pop_outerr_to_orig(self) -> tuple[AnyStr, AnyStr]:
        """Pop current snapshot out/err capture and flush to orig streams."""
        out, err = self.readouterr()
        if out:
            assert self.out is not None
            self.out.writeorg(out)
        if err:
            assert self.err is not None
            self.err.writeorg(err)
        return out, err

    def suspend_capturing(self, in_: bool = False) -> None:
        self._state = "suspended"
        if self.out:
            self.out.suspend()
        if self.err:
            self.err.suspend()
        if in_ and self.in_:
            self.in_.suspend()
            self._in_suspended = True

    def resume_capturing(self) -> None:
        self._state = "started"
        if self.out:
            self.out.resume()
        if self.err:
            self.err.resume()
        if self._in_suspended:
            assert self.in_ is not None
            self.in_.resume()
            self._in_suspended = False

    def stop_capturing(self) -> None:
        """Stop capturing and reset capturing streams."""
        if self._state == "stopped":
            raise ValueError("was already stopped")
        self._state = "stopped"
        if self.out:
            self.out.done()
        if self.err:
            self.err.done()
        if self.in_:
            self.in_.done()

    def is_started(self) -> bool:
        """Whether actively capturing -- not suspended or stopped."""
        return self._state == "started"

    def readouterr(self) -> CaptureResult[AnyStr]:
        out = self.out.snap() if self.out else ""
        err = self.err.snap() if self.err else ""
        # TODO: This type error is real, need to fix.
        return CaptureResult(out, err)  # type: ignore[arg-type]

```

--------------------------------

### Directly Use RaisesGroup.matches() to Check Exception Groups

Source: https://docs.pytest.org/en/stable/reference/reference

Provides an example of using the `RaisesGroup.matches()` method directly to validate a standalone exception group against the defined criteria. This is useful for testing exception groups outside of a context manager.

```python
with pytest.raises(TypeError) as excinfo:
    ...
assert RaisesGroup(ValueError).matches(excinfo.value.__cause__)
# the above line is equivalent to
myexc = excinfo.value.__cause__
assert isinstance(myexc, BaseExceptionGroup)
assert len(myexc.exceptions) == 1
assert isinstance(myexc.exceptions[0], ValueError)
```

--------------------------------

### Class-level setup/teardown in pytest

Source: https://docs.pytest.org/en/stable/how-to/xunit_setup

These methods are called before and after all test methods within a class. They are class methods and require the `@classmethod` decorator.

```python
@classmethod
def setup_class(cls):
    """setup any state specific to the execution of the given class (which
    usually contains tests).
    """


@classmethod
def teardown_class(cls):
    """teardown any state that was previously setup with a call to
    setup_class.
    """

```

--------------------------------

### Check for File Descriptor Leaks with lsof

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Implements a file descriptor leak checker using the 'lsof' command. It retrieves currently open files, filters out irrelevant ones, and compares the list before and after a test to detect leaks. This class requires 'lsof' to be installed and available on the system.

```python
class LsofFdLeakChecker:
    def get_open_files(self) -> list[tuple[str, str]]:
        if sys.version_info >= (3, 11):
            # New in Python 3.11, ignores utf-8 mode
            encoding = locale.getencoding()
        else:
            encoding = locale.getpreferredencoding(False)
        out = subprocess.run(
            ("lsof", "-Ffn0", "-p", str(os.getpid())),
            stdout=subprocess.PIPE,
            stderr=subprocess.DEVNULL,
            check=True,
            text=True,
            encoding=encoding,
        ).stdout

        def isopen(line: str) -> bool:
            return line.startswith("f") and (
                "deleted" not in line
                and "mem" not in line
                and "txt" not in line
                and "cwd" not in line
            )

        open_files = []

        for line in out.split("\n"):
            if isopen(line):
                fields = line.split("\0")
                fd = fields[0][1:]
                filename = fields[1][1:]
                if filename in IGNORE_PAM:
                    continue
                if filename.startswith("/"):
                    open_files.append((fd, filename))

        return open_files

    def matching_platform(self) -> bool:
        try:
            subprocess.run(("lsof", "-v"), check=True)
        except (OSError, subprocess.CalledProcessError):
            return False
        else:
            return True

    @hookimpl(wrapper=True, tryfirst=True)
    def pytest_runtest_protocol(self, item: Item) -> Generator[None, object, object]:
        lines1 = self.get_open_files()
        try:
            return (yield)
        finally:
            if hasattr(sys, "pypy_version_info"):
                gc.collect()
            lines2 = self.get_open_files()
```

--------------------------------

### Imperatively Xfail a Test with Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/outcomes

The `xfail` object allows for imperative xfailing of a test or setup function during execution. It raises a `pytest.xfail.Exception` with a specified reason. It's recommended to use the `pytest.mark.xfail` marker when possible.

```python
class _XFail:
    Exception: ClassVar[type[XFailed]] = XFailed

    def __call__(self, reason: str = "") -> NoReturn:
        __tracebackhide__ = True
        raise XFailed(msg=reason)

xfail: _XFail = _XFail()
```

--------------------------------

### Migrating Legacy to Native Namespace Packages in Python

Source: https://docs.pytest.org/en/stable/deprecations

Demonstrates the code difference between legacy and native namespace packages. Legacy packages use an `__init__.py` file with `pkg_resources.declare_namespace()`, while native packages (recommended for Python 3.3+) omit the `__init__.py` file entirely.

```python
# Legacy namespace package (deprecated):
# mypkg/__init__.py
__import__("pkg_resources").declare_namespace(__name__)

```

```python
# Native namespace package (recommended):
# Simply remove the __init__.py file entirely.
# Python 3.3+ natively supports namespace packages without __init__.py.

```

--------------------------------

### Handling ImportError During Plugin Loading

Source: https://docs.pytest.org/en/stable/changelog

Pytest will no longer hide `ImportError` exceptions that occur when loading plugins. This makes it easier to diagnose issues related to missing or improperly installed plugins, fixing issue #375.

```python
# Example of a plugin that might raise ImportError:
# try:
#     import non_existent_plugin
# except ImportError:
#     pass

# Pytest will now properly report this ImportError if it occurs during plugin discovery.
```

--------------------------------

### Write a Pytest to Ensure a Simple Test Passes

Source: https://docs.pytest.org/en/stable/contributing

This snippet demonstrates how to use the pytester fixture to write a test that verifies a simple assertion passes. It creates a Python file with a passing test and then runs pytest to check the outcome.

```python
def test_true_assertion(pytester):
    pytester.makepyfile(
        """
        def test_foo():
            assert True
    """
    )
    result = pytester.runpytest()
    result.assert_outcomes(failed=0, passed=1)

```

--------------------------------

### Get Hook Proxy with Path Awareness (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/main

Retrieves a hook proxy for a given file system path. It optimizes by checking if the path is already a `Path` object and efficiently determines the appropriate hook relay based on active conftest modules.

```python
    def gethookproxy(self, fspath: os.PathLike[str]) -> pluggy.HookRelay:
        # Optimization: Path(Path(...)) is much slower than isinstance.
        path = fspath if isinstance(fspath, Path) else Path(fspath)
        pm = self.config.pluginmanager
        # Check if we have the common case of running
        # hooks with all conftest.py files.
        my_conftestmodules = pm._getconftestmodules(path)
        remove_mods = pm._conftest_plugins.difference(my_conftestmodules)
        proxy: pluggy.HookRelay
        if remove_mods:
            # One or more conftests are not in use at this path.
            proxy = PathAwareHookProxy(FSHookProxy(pm, remove_mods))  # type: ignore[arg-type,assignment]
        else:
            # All plugins are active for this fspath.
            proxy = self.config.hook
        return proxy
```

--------------------------------

### Report Test Status in Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/runner

Implements the pytest_report_teststatus hook to customize the reporting of test status for setup and teardown phases. It returns a category, short letter, and verbose word based on whether the test failed, was skipped, or passed.

```python
from _pytest.reports import BaseReport

# Assuming BaseReport is defined elsewhere
# class BaseReport:
#     def __init__(self, when, failed=False, skipped=False):
#         self.when = when
#         self.failed = failed
#         self.skipped = skipped

def pytest_report_teststatus(report: BaseReport) -> tuple[str, str, str] | None:
    if report.when in ("setup", "teardown"):
        if report.failed:
            #      category, shortletter, verbose-word
            return "error", "E", "ERROR"
        elif report.skipped:
            return "skipped", "s", "SKIPPED"
        else:
            return "", "", ""
    return None
```

--------------------------------

### Parametrize Test Function with Input/Output Pairs (Python)

Source: https://docs.pytest.org/en/stable/how-to/parametrize

Demonstrates how to use pytest.mark.parametrize to run a single test function multiple times with different input values and their corresponding expected outputs. This is useful for testing simple functions or expressions against a set of known cases.

```python
import pytest


@pytest.mark.parametrize("test_input,expected", [("3+5", 8), ("2+4", 6), ("6*9", 42)])
def test_eval(test_input, expected):
    assert eval(test_input) == expected
```

--------------------------------

### Pytest Session Lifecycle Management

Source: https://docs.pytest.org/en/stable/_modules/_pytest/main

A Python function that acts as a skeleton for a command-line program, managing the pytest session lifecycle. It handles configuration, session start hooks, and exceptions like UsageError, Failed, and KeyboardInterrupt.

```python
def wrap_session(
    config: Config, doit: Callable[[Config, Session], int | ExitCode | None]
) -> int | ExitCode:
    """Skeleton command line program."""
    session = Session.from_config(config)
    session.exitstatus = ExitCode.OK
    initstate = 0
    try:
        try:
            config._do_configure()
            initstate = 1
            config.hook.pytest_sessionstart(session=session)
            initstate = 2
            session.exitstatus = doit(config, session) or 0
        except UsageError:
            session.exitstatus = ExitCode.USAGE_ERROR
            raise
        except Failed:
            session.exitstatus = ExitCode.TESTS_FAILED
        except (KeyboardInterrupt, exit.Exception):
            excinfo = _pytest._code.ExceptionInfo.from_current()
            exitstatus: int | ExitCode = ExitCode.INTERRUPTED
            if isinstance(excinfo.value, exit.Exception):
                if excinfo.value.returncode is not None:
                    exitstatus = excinfo.value.returncode
                if initstate < 2:

```

--------------------------------

### Running Test Source Code In-Process

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Executes test code provided as a string within the current process using `pytest.main()`. The source code is written to a temporary file, and `pytest.main()` is invoked with the file path and any additional command-line arguments. Returns a `HookRecorder` instance.

```python
def inline_runsource(self, source: str, *cmdlineargs) -> HookRecorder:
    """Run a test module in process using ``pytest.main()``.

    This run writes "source" into a temporary file and runs
    ``pytest.main()`` on it, returning a :py:class:`HookRecorder` instance
    for the result.

    :param source: The source code of the test module.
    :param cmdlineargs: Any extra command line arguments to use.
    """
    p = self.makepyfile(source)
    values = [*list(cmdlineargs), p]
    return self.inline_run(*values)

```

--------------------------------

### Patch os.getcwd function using monkeypatch in Python

Source: https://docs.pytest.org/en/stable/reference/reference

Shows how to replace the os.getcwd function with a lambda function using monkeypatch.setattr. This example illustrates patching a specific function to return a predefined value, useful for testing code that relies on the current working directory.

```python
import os

monkeypatch.setattr(os, "getcwd", lambda: "/")

```

--------------------------------

### Pytest Command Line Parsing and Plugin Handling

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Internal function to prepare Pytest configuration by parsing arguments and handling plugins. It includes type checking for arguments and uses hook-based parsing.

```python
def _prepareconfig(
    args: list[str] | os.PathLike[str],
    plugins: Sequence[str | _PluggyPlugin] | None = None,
) -> Config:
    if isinstance(args, os.PathLike):
        args = [os.fspath(args)]
    elif not isinstance(args, list):
        msg = (
            "`args` parameter expected to be a list of strings, got: {!r} (type: {})"
        )
        raise TypeError(msg.format(args, type(args)))

    initial_config = get_config(args, plugins)
    pluginmanager = initial_config.pluginmanager
    try:
        if plugins:
            for plugin in plugins:
                if isinstance(plugin, str):
                    pluginmanager.consider_pluginarg(plugin)
                else:
                    pluginmanager.register(plugin)
        config: Config = pluginmanager.hook.pytest_cmdline_parse(
            pluginmanager=pluginmanager, args=args
        )
        return config
    except BaseException:
        initial_config._ensure_unconfigure()
        raise
```

--------------------------------

### Configure Warning Filters in pytest.ini

Source: https://docs.pytest.org/en/stable/how-to/capture-warnings

Set warning filters in the 'filterwarnings' option within the '[pytest]' section of your pytest.ini configuration file. This example ignores all UserWarnings and specific DeprecationWarnings matching a regex, while treating all other warnings as errors. Filters are processed in order, with the last matching filter taking precedence.

```ini
[pytest]
filterwarnings =
    error
    ignore::UserWarning
    ignore:function ham\(\)\, is deprecated:DeprecationWarning
```

--------------------------------

### Set Python Path for Tests (INI)

Source: https://docs.pytest.org/en/stable/explanation/goodpractices

Configures pytest to include the 'src' directory in the Python path, allowing tests to import modules from the application's source code when not using an editable install.

```ini
[pytest]
pythonpath = src
```

--------------------------------

### Set Python Path for Tests (TOML)

Source: https://docs.pytest.org/en/stable/explanation/goodpractices

Configures pytest to include the 'src' directory in the Python path, allowing tests to import modules from the application's source code when not using an editable install.

```toml
[pytest]
pythonpath = ["src"]
```

--------------------------------

### Execute Pytest Hooks and Generate Reports (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/runner

The `call_and_report` function executes specified Pytest hooks (setup, call, teardown) for a given test item. It captures the outcome, generates a test report, and optionally logs the report and handles interactive exceptions. Dependencies include `Item`, `Literal`, `TestReport`, `Callable`, `CallInfo`, `get_reraise_exceptions`, and `check_interactive_exception`.

```python
def call_and_report(
    item: Item, when: Literal["setup", "call", "teardown"], log: bool = True, **kwds
) -> TestReport:
    ihook = item.ihook
    if when == "setup":
        runtest_hook: Callable[..., None] = ihook.pytest_runtest_setup
    elif when == "call":
        runtest_hook = ihook.pytest_runtest_call
    elif when == "teardown":
        runtest_hook = ihook.pytest_runtest_teardown
    else:
        assert False, f"Unhandled runtest hook case: {when}"

    call = CallInfo.from_call(
        lambda: runtest_hook(item=item, **kwds),
        when=when,
        reraise=get_reraise_exceptions(item.config),
    )
    report: TestReport = ihook.pytest_runtest_makereport(item=item, call=call)
    if log:
        ihook.pytest_runtest_logreport(report=report)
    if check_interactive_exception(call, report):
        ihook.pytest_exception_interact(node=item, call=call, report=report)
    return report
```

--------------------------------

### Pytest Fixture Decorator

Source: https://docs.pytest.org/en/stable/reference/reference

The @pytest.fixture decorator is used to mark a function as a pytest fixture. Fixtures can provide setup and teardown code for tests and can be configured with various options like scope, parameters, and autouse behavior.

```APIDOC
## @pytest.fixture

### Description
Decorator to mark a fixture factory function. This decorator can be used, with or without parameters, to define a fixture function. The name of the fixture function can later be referenced to cause its invocation ahead of running tests. Test functions can directly use fixture names as input arguments. Fixtures can provide their values to test functions using `return` or `yield` statements.

### Method
Decorator

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```python
@pytest.fixture
def my_fixture():
    return "fixture value"
```

### Response
#### Success Response (200)
N/A (This is a decorator, not an endpoint)

#### Response Example
N/A
```

--------------------------------

### Create Directory with Legacy Path in Cache

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

The `Cache_makedir` function creates a directory path object with a given name. It functions like `mkdir` but returns a legacy `py.path.local` instance.

```python
def Cache_makedir(self: Cache, name: str) -> LEGACY_PATH:
    """Return a directory path object with the given name.

    Same as :func:`mkdir`, but returns a legacy py path instance.
    """
    return legacy_path(self.mkdir(name))
```

--------------------------------

### Return Original Text as String (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Returns the entire original captured text as a string. This method allows retrieval of the complete log content.

```python
def str(self) -> str:
    """Return the entire original text."""
    return str(self)
```

--------------------------------

### Testing Tuple Unpacking Error (Python)

Source: https://docs.pytest.org/en/stable/example/reportingdemo

This example demonstrates a ValueError occurring during tuple unpacking. The error message 'not enough values to unpack' indicates that the list on the right-hand side did not contain the expected number of elements.

```python
a, b = [1]
```

--------------------------------

### Get Specific Test Item by Function Name

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `getitem` method collects all test items from a given source code and returns the specific test item matching the provided function name. It raises an assertion error if the function name is not found.

```python
def getitem(
        self,
        source: str | os.PathLike[str],
        funcname: str = "test_func",
    ) -> Item:
    """Return the test item for a test function.

    Writes the source to a python file and runs pytest's collection on
    the resulting module, returning the test item for the requested
    function name.

    :param source:
        The module source.
    :param funcname:
        The name of the test function for which to return a test item.
    :returns:
        The test item.
    """
    items = self.getitems(source)
    for item in items:
        if item.name == funcname:
            return item
    assert 0, f"{funcname!r} item not found in module:\n{source}\nitems: {items}"
```

--------------------------------

### Legacy Testdir Fixture

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Provides a Testdir instance that returns legacy LEGACY_PATH objects. This fixture is intended for backward compatibility and new code should prefer the 'pytester' fixture.

```python
@staticmethod
@fixture
def testdir(pytester: Pytester) -> Testdir:
    """
    Identical to :fixture:`pytester`, and provides an instance whose methods return
    legacy ``LEGACY_PATH`` objects instead when applicable.

    New code should avoid using :fixture:`testdir` in favor of :fixture:`pytester`.
    """
    return Testdir(pytester, _ispytest=True)
```

--------------------------------

### FixtureFunctionDefinition Class for Pytest Fixtures

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

The FixtureFunctionDefinition class wraps a fixture function, managing its name, scope, and invocation. It handles method binding and prevents direct calls to fixtures, guiding users to the correct usage patterns.

```python
class FixtureFunctionDefinition:
    def __init__(
        self,
        *,
        function: Callable[..., Any],
        fixture_function_marker: FixtureFunctionMarker,
        instance: object | None = None,
        _ispytest: bool = False,
    ) -> None:
        check_ispytest(_ispytest)
        self.name = fixture_function_marker.name or function.__name__
        self.__name__ = self.name
        self._fixture_function_marker = fixture_function_marker
        if instance is not None:
            self._fixture_function = cast(
                Callable[..., Any], function.__get__(instance)
            )
        else:
            self._fixture_function = function
        functools.update_wrapper(self, function)

    def __repr__(self) -> str:
        return f"<pytest_fixture({self._fixture_function})>"

    def __get__(self, instance, owner=None):
        return FixtureFunctionDefinition(
            function=self._fixture_function,
            fixture_function_marker=self._fixture_function_marker,
            instance=instance,
            _ispytest=True,
        )

    def __call__(self, *args: Any, **kwds: Any) -> Any:
        message = (
            f'Fixture "{self.name}" called directly. Fixtures are not meant to be called directly,\n'
            "but are created automatically when test functions request them as parameters.\n"
            "See https://docs.pytest.org/en/stable/explanation/fixtures.html for more information about fixtures, and\n"
            "https://docs.pytest.org/en/stable/deprecations.html#calling-fixtures-directly"
        )
        fail(message, pytrace=False)

    def _get_wrapped_function(self) -> Callable[..., Any]:
        return self._fixture_function
```

--------------------------------

### Run Pytest with Src Layout

Source: https://docs.pytest.org/en/stable/explanation/goodpractices

Executes pytest while setting the PYTHONPATH environment variable to 'src'. This is a common method to ensure tests can find and import application modules when using the 'src' layout without an editable install.

```bash
PYTHONPATH=src pytest
```

--------------------------------

### Pytest Options for Reporting and Debugging

Source: https://docs.pytest.org/en/stable/changelog

Illustrates various command-line options for Pytest, including `-r` for detailed test reporting, `--tb=line` for concise tracebacks, and `--funcargs` to display available function arguments and their help strings.

```bash
# Example usage of reporting and debugging options:
py.test -r xfsX  # Detailed reporting
py.test --tb=line # Single-line traceback for failures
py.test --funcargs # Show available funcargs and their docstrings
```

--------------------------------

### Registering plugins with pytest_plugins (sequence of strings)

Source: https://docs.pytest.org/en/stable/reference/reference

Illustrates registering multiple plugins by declaring `pytest_plugins` as a sequence (e.g., a tuple) of strings, where each string represents a plugin to be loaded.

```python
pytest_plugins = ("myapp.testsupport.tools", "myapp.testsupport.regression")
```

--------------------------------

### Pytest Fixture for Doctest Namespace

Source: https://docs.pytest.org/en/stable/_modules/_pytest/doctest

A pytest fixture that provides a dictionary to be injected into the namespace of doctests. This allows users to easily make variables, modules, or other objects available within their doctest examples, often used with an 'autouse' fixture.

```python
@fixture(scope="session")
def doctest_namespace() -> dict[str, Any]:
    """Fixture that returns a :py:class:`dict` that will be injected into the
    namespace of doctests.

    Usually this fixture is used in conjunction with another ``autouse`` fixture:

    .. code-block:: python

        @pytest.fixture(autouse=True)
        def add_np(doctest_namespace):
            doctest_namespace["np"] = numpy

    For more details: :ref:`doctest_namespace`.
    """
    return dict()
```

--------------------------------

### Asserting Attribute Value (Python)

Source: https://docs.pytest.org/en/stable/example/reportingdemo

This example shows an AssertionError when asserting that an object's attribute 'b' equals a specific value. The output clearly indicates the expected versus actual values, aiding in debugging.

```python
class Foo:
    b = 1

i = Foo()
assert i.b == 2
```

--------------------------------

### Clear Captured Log Records with caplog.clear()

Source: https://docs.pytest.org/en/stable/how-to/logging

Shows how to reset the captured log records during a test using the `caplog.clear()` method. This is useful when you need to start capturing logs from a specific point in your test or after certain operations.

```python
import logging

def some_method_that_creates_log_records():
    logging.info("Creating logs")

def your_test_method():
    logging.info("Test log")

def test_something_with_clearing_records(caplog):
    some_method_that_creates_log_records()
    caplog.clear()
    your_test_method()
    assert [rec.message for rec in caplog.records] == ["Test log"]
```

--------------------------------

### Pytest Node Collection: Collect One Node

Source: https://docs.pytest.org/en/stable/_modules/_pytest/runner

Collects a single pytest node, initiating the collection process and reporting the outcome. It calls pytest hooks for collection start and report generation, handling interactive exceptions.

```python
def collect_one_node(collector: Collector) -> CollectReport:
    ihook = collector.ihook
    ihook.pytest_collectstart(collector=collector)
    rep: CollectReport = ihook.pytest_make_collect_report(collector=collector)
    call = rep.__dict__.pop("call", None)
    if call and check_interactive_exception(call, rep):
        ihook.pytest_exception_interact(node=collector, call=call, report=rep)
    return rep
```

--------------------------------

### Clone Pytest Repository and Create Branch (Git)

Source: https://docs.pytest.org/en/stable/contributing

This snippet demonstrates how to clone the pytest GitHub repository, fetch tags, and create a new branch for development using Git.

```bash
$ git clone git@github.com:YOUR_GITHUB_USERNAME/pytest.git
$ cd pytest
$ git fetch --tags https://github.com/pytest-dev/pytest
# now, create your own branch off "main":

    $ git checkout -b your-bugfix-branch-name main
```

--------------------------------

### Represent Local Variables for Pytest Tracebacks (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/_code/code

Generates a formatted representation of local variables within a given scope. It filters out internal variables (starting with '@'), sorts them, and formats their string representations, with options for truncation.

```Python
def repr_locals(self, locals: Mapping[str, object]) -> ReprLocals | None:
        if self.showlocals:
            lines = []
            keys = [loc for loc in locals if loc[0] != "@"]
            keys.sort()
            for name in keys:
                value = locals[name]
                if name == "__builtins__":
                    lines.append("__builtins__ = <builtins>")
                else:
                    # This formatting could all be handled by the
                    # _repr() function, which is only reprlib.Repr in
                    # disguise, so is very configurable.
                    if self.truncate_locals:
                        str_repr = saferepr(value)
                    else:
                        str_repr = safeformat(value)
                    # if len(str_repr) < 70 or not isinstance(value, (list, tuple, dict)):
                    lines.append(f"{name:<10} = {str_repr}")
                    # else:
                    #    self._line("%-10s =\\") % (name,)
                    #    # XXX
                    #    pprint.pprint(value, stream=self.excinfowriter)
            return ReprLocals(lines)
        return None
```

--------------------------------

### Pytest Collection Finish Hook (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

Implements the pytest_collection_finish hook for the TerminalProgressPlugin. Called after test collection is complete, this method transitions the progress display from 'indeterminate' to 'normal' with 0% progress if tests were collected. It ensures the terminal reflects the start of test execution.

```python
@hookimpl
def pytest_collection_finish(self) -> None:
    assert self._session is not None
    if self._session.testscollected > 0:
        # Switch from indeterminate to 0% progress.
        self._emit_progress("normal", 0)
```

--------------------------------

### Configure Build System and Project Metadata (TOML)

Source: https://docs.pytest.org/en/stable/explanation/goodpractices

This TOML snippet defines the build system requirements and project metadata for a Python package. It specifies 'hatchling' as the build backend and sets the package name and version. This is crucial for packaging and distribution.

```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "PACKAGENAME"
version = "PACKAGEVERSION"

```

--------------------------------

### Test function reacting to command-line options via cmdopt fixture

Source: https://docs.pytest.org/en/stable/example/simple

This Python snippet defines a test function `test_answer` that uses a `cmdopt` fixture to receive values based on command-line options. It prints different output ('first' or 'second') depending on whether `cmdopt` is 'type1' or 'type2'. The `assert 0` is used to make the test fail and display the printed output.

```python
# content of test_sample.py
def test_answer(cmdopt):
    if cmdopt == "type1":
        print("first")
    elif cmdopt == "type2":
        print("second")
    assert 0  # to see what was printed

```

--------------------------------

### Define and Use a Hook for Default Option Values

Source: https://docs.pytest.org/en/stable/how-to/writing_hook_functions

This example demonstrates using hooks to dynamically set default values for command-line options. `pytest_config_file_default_value` hook is defined to return a default config file path. `pytest_addoption` then uses this hook's result to set the default for the `--config-file` option.

```python
# contents of hooks.py


# Use firstresult=True because we only want one plugin to define this
# default value
@hookspec(firstresult=True)
def pytest_config_file_default_value():
    """Return the default value for the config file command line option."""


# contents of myplugin.py


def pytest_addhooks(pluginmanager):
    """This example assumes the hooks are grouped in the 'hooks' module."""
    from . import hooks

    pluginmanager.add_hookspecs(hooks)


def pytest_addoption(parser, pluginmanager):
    default_value = pluginmanager.hook.pytest_config_file_default_value()
    parser.addoption(
        "--config-file",
        help="Config file to use, defaults to %(default)s",
        default=default_value,
    )

```

--------------------------------

### Handle Pytest Test Log Report (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/junitxml

Processes setup, call, and teardown reports for individual tests. It handles passed, failed, and skipped tests, appending appropriate information to the reporter. Special handling is included for failures during teardown and for compatibility with the xdist plugin, ensuring correct XML generation.

```python
def pytest_runtest_logreport(self, report: TestReport) -> None:
        """Handle a setup/call/teardown report, generating the appropriate
        XML tags as necessary.

        Note: due to plugins like xdist, this hook may be called in interlaced
        order with reports from other nodes. For example:

        Usual call order:
            -> setup node1
            -> call node1
            -> teardown node1
            -> setup node2
            -> call node2
            -> teardown node2

        Possible call order in xdist:
            -> setup node1
            -> call node1
            -> setup node2
            -> call node2
            -> teardown node2
            -> teardown node1
        """
        close_report = None
        if report.passed:
            if report.when == "call":  # ignore setup/teardown
                reporter = self._opentestcase(report)
                reporter.append_pass(report)
        elif report.failed:
            if report.when == "teardown":
                # The following vars are needed when xdist plugin is used.
                report_wid = getattr(report, "worker_id", None)
                report_ii = getattr(report, "item_index", None)
                close_report = next(
                    (
                        rep
                        for rep in self.open_reports
                        if (
                            rep.nodeid == report.nodeid
                            and getattr(rep, "item_index", None) == report_ii
                            and getattr(rep, "worker_id", None) == report_wid
                        )
                    ),
                    None,
                )
                if close_report:
                    # We need to open new testcase in case we have failure in
                    # call and error in teardown in order to follow junit
                    # schema.
                    self.finalize(close_report)
                    self.cnt_double_fail_tests += 1
            reporter = self._opentestcase(report)
            if report.when == "call":
                reporter.append_failure(report)
                self.open_reports.append(report)
                if not self.log_passing_tests:
                    reporter.write_captured_output(report)
            else:
                reporter.append_error(report)
        elif report.skipped:
            reporter = self._opentestcase(report)
            reporter.append_skipped(report)
        self.update_testcase_duration(report)
        if report.when == "teardown":
            reporter = self._opentestcase(report)
            reporter.write_captured_output(report)

            self.finalize(report)
            report_wid = getattr(report, "worker_id", None)
            report_ii = getattr(report, "item_index", None)
            close_report = next(
                (
                    rep
                    for rep in self.open_reports
                    if (
                        rep.nodeid == report.nodeid
                        and getattr(rep, "item_index", None) == report_ii
                        and getattr(report, "worker_id", None) == report_wid
                    )
                ),
                None,
            )
            if close_report:
                self.open_reports.remove(close_report)
```

--------------------------------

### Another Pytest Test Using Package-Scoped Fixture

Source: https://docs.pytest.org/en/stable/example/simple

This Python code presents another pytest test module that also uses the 'db' fixture. This illustrates how a package-scoped fixture defined in a conftest.py file can be accessed by multiple test modules within the same scope.

```python
# content of a/test_db2.py
def test_a2(db):
    assert 0, db  # to show value
```

--------------------------------

### Remove Dictionary Items with Monkeypatch

Source: https://docs.pytest.org/en/stable/how-to/monkeypatch

Illustrates how to use `monkeypatch.delitem` to remove a key-value pair from a dictionary during tests. This is helpful for testing scenarios where a required configuration key might be missing. The example shows removing the 'user' key from `DEFAULT_CONFIG` and expecting a `KeyError`.

```python
# contents of test_app.py
import pytest

# app.py with the connection string function
import app


def test_missing_user(monkeypatch):
    # patch the DEFAULT_CONFIG t be missing the 'user' key
    monkeypatch.delitem(app.DEFAULT_CONFIG, "user", raising=False)

    # Key error expected because a config is not passed, and the
    # default is now missing the 'user' entry.
    with pytest.raises(KeyError):
        _ = app.create_connection_string()
```

--------------------------------

### Text Stream Capture (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Captures text data from system streams. It inherits from SysCaptureBase and implements `snap` to retrieve text and `writeorg` to write text to the original stream. It asserts that the temporary file is a CaptureIO instance.

```python
class SysCapture(SysCaptureBase[str]):
    EMPTY_BUFFER = ""

    def snap(self) -> str:
        self._assert_state("snap", ("started", "suspended"))
        assert isinstance(self.tmpfile, CaptureIO)
        res = self.tmpfile.getvalue()
        self.tmpfile.seek(0)
        self.tmpfile.truncate()
        return res

    def writeorg(self, data: str) -> None:
        self._assert_state("writeorg", ("started", "suspended"))
        self._old.write(data)
        self._old.flush()

```

--------------------------------

### Yield Fixture Teardown Order in Python

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Illustrates the teardown order of yield fixtures in pytest. The example shows that the teardown code for fixtures is executed in a last-in, first-out (LIFO) order, meaning the last fixture defined or yielded from will have its teardown code run first.

```python
import pytest


def test_bar(fix_w_yield1, fix_w_yield2):
    print("test_bar")


@pytest.fixture
def fix_w_yield1():
    yield
    print("after_yield_1")


@pytest.fixture
def fix_w_yield2():
    yield
    print("after_yield_2")

```

--------------------------------

### Select Tests by Node ID using Pytest

Source: https://docs.pytest.org/en/stable/example/markers

Provides examples of selecting tests using their unique node IDs. Node IDs can specify modules, classes, methods, or functions. This method is useful for precise test selection, including parametrized tests.

```bash
$ pytest -v test_server.py::TestClass::test_method
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y -- $PYTHON_PREFIX/bin/python
cachedir: .pytest_cache
rootdir: /home/sweet/project
collecting ... collected 1 item

test_server.py::TestClass::test_method PASSED                        [100%]

============================ 1 passed in 0.12s =============================

```

```bash
$ pytest -v test_server.py::TestClass
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y -- $PYTHON_PREFIX/bin/python
cachedir: .pytest_cache
rootdir: /home/sweet/project
collecting ... collected 1 item

test_server.py::TestClass::test_method PASSED                        [100%]

============================ 1 passed in 0.12s =============================

```

```bash
$ pytest -v test_server.py::TestClass test_server.py::test_send_http
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-9.x.y, pluggy-1.x.y -- $PYTHON_PREFIX/bin/python
cachedir: .pytest_cache
rootdir: /home/sweet/project
collecting ... collected 2 items

test_server.py::TestClass::test_method PASSED                        [ 50%]
test_server.py::test_send_http PASSED                                [100%]

============================ 2 passed in 0.12s =============================

```

--------------------------------

### Test Classes with `callme` Method for Fixture Execution (pytest)

Source: https://docs.pytest.org/en/stable/example/special

Demonstrates how test classes can define a `callme` class method. This method is intended to be called by a session-scoped pytest fixture before tests within that class are executed. Examples include standard Python classes and `unittest.TestCase` subclasses.

```python
# content of test_module.py


class TestHello:
    @classmethod
    def callme(cls):
        print("callme called!")

    def test_method1(self):
        print("test_method1 called")

    def test_method2(self):
        print("test_method2 called")


class TestOther:
    @classmethod
    def callme(cls):
        print("callme other called")

    def test_other(self):
        print("test other")


# works with unittest as well ...
import unittest


class SomeTest(unittest.TestCase):
    @classmethod
    def callme(self):
        print("SomeTest callme called")

    def test_unit1(self):
        print("test_unit1 method called")

```

--------------------------------

### LoggingPlugin Initialization

Source: https://docs.pytest.org/en/stable/_modules/_pytest/logging

Initializes the LoggingPlugin, setting up various logging handlers for capturing, reporting, file output, and CLI output. It configures formatters and log levels based on pytest configuration options.

```python
class LoggingPlugin:
    """Attaches to the logging module and captures log messages for each test."""

    def __init__(self, config: Config) -> None:
        """Create a new plugin to capture log messages.

        The formatter can be safely shared across all handlers so
        create a single one for the entire test session here.
        """
        self._config = config

        # Report logging.
        self.formatter = self._create_formatter(
            get_option_ini(config, "log_format"),
            get_option_ini(config, "log_date_format"),
            get_option_ini(config, "log_auto_indent"),
        )
        self.log_level = get_log_level_for_setting(config, "log_level")
        self.caplog_handler = LogCaptureHandler()
        self.caplog_handler.setFormatter(self.formatter)
        self.report_handler = LogCaptureHandler()
        self.report_handler.setFormatter(self.formatter)

        # File logging.
        self.log_file_level = get_log_level_for_setting(
            config, "log_file_level", "log_level"
        )
        log_file = get_option_ini(config, "log_file") or os.devnull
        if log_file != os.devnull:
            directory = os.path.dirname(os.path.abspath(log_file))
            if not os.path.isdir(directory):
                os.makedirs(directory)

        self.log_file_mode = get_option_ini(config, "log_file_mode") or "w"
        self.log_file_handler = _FileHandler(
            log_file, mode=self.log_file_mode, encoding="UTF-8"
        )
        log_file_format = get_option_ini(config, "log_file_format", "log_format")
        log_file_date_format = get_option_ini(
            config, "log_file_date_format", "log_date_format"
        )

        log_file_formatter = DatetimeFormatter(
            log_file_format, datefmt=log_file_date_format
        )
        self.log_file_handler.setFormatter(log_file_formatter)

        # CLI/live logging.
        self.log_cli_level = get_log_level_for_setting(
            config, "log_cli_level", "log_level"
        )
        if self._log_cli_enabled():
            terminal_reporter = config.pluginmanager.get_plugin("terminalreporter")
            # Guaranteed by `_log_cli_enabled()`.
            assert terminal_reporter is not None
            capture_manager = config.pluginmanager.get_plugin("capturemanager")
            # if capturemanager plugin is disabled, live logging still works.
            self.log_cli_handler: (
                _LiveLoggingStreamHandler | _LiveLoggingNullHandler
            ) = _LiveLoggingStreamHandler(terminal_reporter, capture_manager)
        else:
            self.log_cli_handler = _LiveLoggingNullHandler()
        log_cli_formatter = self._create_formatter(
            get_option_ini(config, "log_cli_format", "log_format"),
            get_option_ini(config, "log_cli_date_format", "log_date_format"),
            get_option_ini(config, "log_auto_indent"),
        )
        self.log_cli_handler.setFormatter(log_cli_formatter)
        self._disable_loggers(loggers_to_disable=config.option.logger_disable)

    def _log_cli_enabled(self):
        # Placeholder for actual implementation
        return True

```

--------------------------------

### Get Pytest Item Location Information

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

The `reportinfo` method provides basic location details for a test item, returning a tuple containing the test path, line number, and test name. This information is primarily used for generating test reports.

```python
def reportinfo(self) -> tuple[os.PathLike[str] | str, int | None, str]:
    """Get location information for this item for test reports.

    Returns a tuple with three elements:

    - The path of the test (default ``self.path``)
    - The 0-based line number of the test (default ``None``)
    - A name of the test to be shown (default ``""``)

    .. seealso:: :ref:`non-python tests`
    """
    return self.path, None, ""
```

--------------------------------

### Declare a Pytest Hook

Source: https://docs.pytest.org/en/stable/how-to/writing_hook_functions

This snippet shows how to declare a basic pytest hook function. Hooks are recognized by pytest if their names start with 'pytest_'. They typically contain documentation explaining their purpose and expected return values.

```python
def pytest_my_hook(config):
    """
    Receives the pytest config and does things with it
    """

```

--------------------------------

### Run Command

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Runs a command with given arguments and an optional timeout. It returns a RunResult. This method is a general utility for executing shell commands and capturing their output.

```python
def run(self, *cmdargs, timeout=None, stdin=CLOSE_STDIN) -> RunResult:
    """See :meth:`Pytester.run`."""
    return self._pytester.run(*cmdargs, timeout=timeout, stdin=stdin)
```

--------------------------------

### Run Python Command with -c

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Executes a Python command string using 'python -c'. It takes a command string as input and returns a RunResult. This is useful for running short Python snippets directly.

```python
def runpython_c(self, command: str) -> RunResult:
    """Run ``python -c \"command\"``."""
    return self.run(sys.executable, "-c", command)
```

--------------------------------

### Apply Warning Filters to a Module with pytestmark

Source: https://docs.pytest.org/en/stable/how-to/capture-warnings

Set the `pytestmark` variable in a module to apply a warning filter to all tests within that module. This example configures all warnings to be treated as errors for the entire module. When assigning a list of filters to `pytestmark`, use the traditional `warnings.filterwarnings()` ordering where later filters take precedence.

```python
# turns all warnings into errors for this module
pytestmark = pytest.mark.filterwarnings("error")
```

--------------------------------

### Defer Hook Implementation to a Separate Plugin

Source: https://docs.pytest.org/en/stable/how-to/writing_hook_functions

This approach shows how to defer the implementation of hooks from third-party plugins to a new plugin. This is useful for managing dependencies and avoiding validation errors if the third-party plugin is not installed. The `DeferPlugin` class contains the hook implementations.

```python
# contents of myplugin.py


class DeferPlugin:
    """Simple plugin to defer pytest-xdist hook functions."""

    def pytest_testnodedown(self, node, error):
        """standard xdist hook function."""


def pytest_configure(config):
    if config.pluginmanager.hasplugin("xdist"):
        config.pluginmanager.register(DeferPlugin())

```

--------------------------------

### LineMatcher Fixture for Text Output Testing

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The LineMatcher fixture returns a reference to the LineMatcher class, which is useful for testing large text outputs, such as command results. It can be instantiated with a list of lines (excluding trailing newlines) for easy comparison.

```python
@fixture(name="LineMatcher")
def LineMatcher_fixture(request: FixtureRequest) -> type[LineMatcher]:
    """A reference to the :class: `LineMatcher`.

    This is instantiable with a list of lines (without their trailing newlines).
    This is useful for testing large texts, such as the output of commands.
    """
    return LineMatcher
```

--------------------------------

### Get Invocation Path with Session.startpath (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/main

Retrieves the path from which pytest was invoked using the `startpath` property of the session object. This property is available from version 7.0.0 onwards and returns a `Path` object representing the invocation directory.

```python
    @property
    def startpath(self) -> Path:
        """The path from which pytest was invoked.

        .. versionadded:: 7.0.0
        """
        return self.config.invocation_params.dir
```

--------------------------------

### Run Pytest In-Process and Get RunResult

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Provides a similar interface to self.runpytest() but executes pytest in-process. It captures stdout and stderr, measures execution time, and returns a RunResult object containing the exit code, captured output lines, and elapsed time. It can optionally insert paths into sys.path.

```python
syspathinsert = kwargs.pop("syspathinsert", False)

if syspathinsert:
    self.syspathinsert()
instant = timing.Instant()
capture = _get_multicapture("sys")
capture.start_capturing()
try:
    try:
        reprec = self.inline_run(*args, **kwargs)
    except SystemExit as e:
        ret = e.args[0]
        try:
            ret = ExitCode(e.args[0])
        except ValueError:
            pass

        class reprec:  # type: ignore
            ret = ret

    except Exception:
        traceback.print_exc()

        class reprec:  # type: ignore
            ret = ExitCode(3)

finally:
    out, err = capture.readouterr()
    capture.stop_capturing()
    sys.stdout.write(out)
    sys.stderr.write(err)

assert reprec.ret is not None
res = RunResult(
    reprec.ret, out.splitlines(), err.splitlines(), instant.elapsed().seconds
)
```

--------------------------------

### List Node Names (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

Returns a list of names of the current node and all its parent nodes, effectively providing the names in the collection hierarchy from root to the current node.

```python
def listnames(self) -> list[str]:
    return [x.name for x in self.listchain()]
```

--------------------------------

### Python: pytest Configuration for JUnit Duration Report

Source: https://docs.pytest.org/en/stable/changelog

This snippet shows how to configure pytest to report only test call durations, excluding setup and teardown times, by adding the `junit_duration_report` parameter to the `pytest.ini` file. This is useful for adhering to specific reporting requirements.

```ini
[pytest]
junit_duration_report = call
```

--------------------------------

### Generate a session-scoped temporary directory using tmp_path_factory in Python

Source: https://docs.pytest.org/en/stable/how-to/tmp_path

Illustrates the use of the `tmp_path_factory` fixture to create a temporary directory that persists for the entire test session. This is useful for generating resources like images once and reusing them across multiple tests, saving computation time. The example shows creating a fixture that generates an image file and returns its path.

```python
# contents of conftest.py
import pytest


@pytest.fixture(scope="session")
def image_file(tmp_path_factory):
    img = compute_expensive_image() # Assume this function exists
    fn = tmp_path_factory.mktemp("data") / "img.png"
    img.save(fn)
    return fn


# contents of test_image.py
def test_histogram(image_file):
    img = load_image(image_file) # Assume this function exists
    # compute and test histogram

```

--------------------------------

### Define Fast and Slow Tests in Pytest

Source: https://docs.pytest.org/en/stable/example/simple

This snippet shows how to define test functions in pytest, including marking a test as 'slow' using the custom marker. This allows for the selective execution of tests based on their duration or importance, as configured in conftest.py.

```python
# content of test_module.py
import pytest


def test_func_fast():
    pass


@pytest.mark.slow
def test_func_slow():
    pass
```

--------------------------------

### Basic Floating-Point Comparison with pytest.approx

Source: https://docs.pytest.org/en/stable/_modules/_pytest/python_api

Demonstrates the fundamental usage of `pytest.approx` for comparing floating-point numbers, showing how it handles the precision issues inherent in floating-point arithmetic.

```python
>>> from pytest import approx
>>> 0.1 + 0.2 == approx(0.3)
True
```

--------------------------------

### Access Legacy Path Properties from Pytester

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Provides properties like tmpdir, test_tmproot, request, plugins, and monkeypatch by forwarding calls to an internal Pytester instance and converting the results to legacy_path objects where applicable.

```python
@property
def tmpdir(self) -> LEGACY_PATH:
    """Temporary directory where tests are executed."""
    return legacy_path(self._pytester.path)

@property
def test_tmproot(self) -> LEGACY_PATH:
    return legacy_path(self._pytester._test_tmproot)

@property
def request:
    return self._pytester._request

@property
def plugins:
    return self._pytester.plugins

@plugins.setter
def plugins(self, plugins):
    self._pytester.plugins = plugins

@property
def monkeypatch(self) -> MonkeyPatch:
    return self._pytester._monkeypatch
```

--------------------------------

### Call Pytest Hooks from a Fixture

Source: https://docs.pytest.org/en/stable/how-to/writing_hook_functions

This example shows how to call a registered pytest hook from within a pytest fixture. The `pytestconfig` fixture provides access to the `hook` object, which is used to invoke hooks like `pytest_my_hook`. The result is typically a list of return values from all registered hook implementations.

```python
@pytest.fixture()
def my_fixture(pytestconfig):
    # call the hook called "pytest_my_hook"
    # 'result' will be a list of return values from all registered functions.
    result = pytestconfig.hook.pytest_my_hook(config=pytestconfig)

```

--------------------------------

### Implement Incremental Testing Marker in Pytest

Source: https://docs.pytest.org/en/stable/example/simple

This Python code snippet for conftest.py sets up an 'incremental' marker for pytest. This marker is intended to be used on test classes to enable incremental testing, where subsequent steps are skipped if an earlier step fails.

```python
# content of conftest.py

from typing import Dict, Tuple

import pytest

```

--------------------------------

### Determine Progress Info Display in Pytest TerminalReporter

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

Determines whether to display progress information in the Pytest terminal output. This method considers various configuration options, such as capture settings, fixture setup display, and the console output style ini setting.

```python
    def _determine_show_progress_info(
        self,
    ) -> Literal["progress", "count", "times", False]:
        """Return whether we should display progress information based on the current config."""
        # do not show progress if we are not capturing output (#3038) unless explicitly
        # overridden by progress-even-when-capture-no
        if (
            self.config.getoption("capture", "no") == "no"
            and self.config.getini("console_output_style")
            != "progress-even-when-capture-no"
        ):
            return False
        # do not show progress if we are showing fixture setup/teardown
        if self.config.getoption("setupshow", False):
            return False
        cfg: str = self.config.getini("console_output_style")
        if cfg in {"progress", "progress-even-when-capture-no"}:
            return "progress"
        elif cfg == "count":
            return "count"
        elif cfg == "times":
            return "times"
        else:
            return False

```

--------------------------------

### Get Pytest Cache Directory Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/cacheprovider

Retrieves the absolute path to the cache directory configured for pytest. It resolves the path based on the `cache_dir` setting in the pytest configuration and the project's root path. This is an internal helper method.

```python
Cache.cache_dir_from_config(config, _ispytest=True)
```

--------------------------------

### Asserting Equality of Attributes Between Different Object Types (Python)

Source: https://docs.pytest.org/en/stable/example/reportingdemo

This example demonstrates an AssertionError when comparing the attribute 'b' of instances from two different classes, 'Foo' and 'Bar'. Pytest clearly shows the differing values and the origin of each value.

```python
class Foo:
    b = 1

class Bar:
    b = 2

assert Foo().b == Bar().b
```

--------------------------------

### Control Warnings with pytest -W Flag

Source: https://docs.pytest.org/en/stable/how-to/capture-warnings

Use the '-W' command-line flag to control warning behavior, similar to Python's built-in warning filters. This example shows how to treat all UserWarnings as errors. The flag accepts options like 'error', 'ignore', 'always', 'default', and 'module'.

```bash
$ pytest -q test_show_warnings.py -W error::UserWarning
```

--------------------------------

### Collect and Run YAML Tests with pytest

Source: https://docs.pytest.org/en/stable/example/nonpython

This Python code snippet demonstrates how to extend pytest to collect and run tests defined in YAML files. It defines custom collectors and test items, requiring the PyYAML library for parsing. The example shows how to load YAML, iterate through test specifications, and execute custom test logic, including custom failure reporting.

```python
# content of conftest.py
from __future__ import annotations

import pytest


def pytest_collect_file(parent, file_path):
    if file_path.suffix == ".yaml" and file_path.name.startswith("test"):
        return YamlFile.from_parent(parent, path=file_path)


class YamlFile(pytest.File):
    def collect(self):
        # We need a yaml parser, e.g. PyYAML.
        import yaml

        raw = yaml.safe_load(self.path.open(encoding="utf-8"))
        for name, spec in sorted(raw.items()):
            yield YamlItem.from_parent(self, name=name, spec=spec)


class YamlItem(pytest.Item):
    def __init__(self, *, spec, **kwargs):
        super().__init__(**kwargs)
        self.spec = spec

    def runtest(self):
        for name, value in sorted(self.spec.items()):
            # Some custom test execution (dumb example follows).
            if name != value:
                raise YamlException(self, name, value)

    def repr_failure(self, excinfo):
        """Called when self.runtest() raises an exception."""
        if isinstance(excinfo.value, YamlException):
            return "\n".join(
                [
                    "usecase execution failed",
                    "   spec failed: {1!r}: {2!r}".format(*excinfo.value.args),
                    "   no further details known at this point.",
                ]
            )
        return super().repr_failure(excinfo)

    def reportinfo(self):
        return self.path, 0, f"usecase: {self.name}"


class YamlException(Exception):
    """Custom exception for error reporting."""

```

--------------------------------

### Pytest Collection Hook: pytest_collection

Source: https://docs.pytest.org/en/stable/reference/reference

Performs the collection phase for the given session. This hook is only called for initial conftests. It can be implemented to perform actions before collection, such as starting a collection counter. It receives the pytest session object as a parameter.

```python
def pytest_collection(session):
    """Perform the collection phase for the given session."""
    pass
```

--------------------------------

### Create Test Files with pytester.makefile

Source: https://docs.pytest.org/en/stable/reference/reference

The `makefile` method creates new text files in the test directory. It accepts an extension and content strings. For binary files, use `pathlib.Path.write_bytes()` directly.

```python
pytester.makefile(".txt", "line1", "line2")

pytester.makefile(".ini", pytest="[pytest]\naddopts=-rs\n")

filename = pytester.path.joinpath("foo.bin")
filename.write_bytes(b"...")

```

--------------------------------

### Testing Connection String with Missing User Config

Source: https://docs.pytest.org/en/stable/how-to/monkeypatch

This test case checks the behavior of `app.create_connection_string()` when the 'user' configuration is missing. It uses the `mock_missing_default_user` fixture to remove the 'user' key from `DEFAULT_CONFIG` and asserts that a `KeyError` is raised, indicating proper error handling for incomplete configurations.

```python
import app
import pytest

def test_missing_user(mock_missing_default_user):
    with pytest.raises(KeyError):
        _ = app.create_connection_string()

```

--------------------------------

### Check if Plugin Exists (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Checks if a plugin with the specified name is currently registered with the configuration manager. Returns a boolean value indicating the presence of the plugin.

```python
def hasplugin(self, name: str) -> bool:
        """Return whether a plugin with the given name is registered."""
        return bool(self.get_plugin(name))
```

--------------------------------

### Handle Plugin Registration and Fixture Discovery

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

Processes plugin registration, specifically identifying conftest.py files to determine their scope. It then calls parsefactories to discover fixtures defined by the plugin.

```python
def pytest_plugin_registered(self, plugin: _PluggyPlugin, plugin_name: str) -> None:
    # Fixtures defined in conftest plugins are only visible to within the
    # conftest's directory. This is unlike fixtures in non-conftest plugins
    # which have global visibility. So for conftests, construct the base
    # nodeid from the plugin name (which is the conftest path).
    if plugin_name and plugin_name.endswith("conftest.py"):
        # Note: we explicitly do *not* use `plugin.__file__` here -- The
        # difference is that plugin_name has the correct capitalization on
        # case-insensitive systems (Windows) and other normalization issues
        # (issue #11816).
        conftestpath = absolutepath(plugin_name)
        try:
            nodeid = str(conftestpath.parent.relative_to(self.config.rootpath))
        except ValueError:
            nodeid = ""
        if nodeid == ".":
            nodeid = ""
        if os.sep != nodes.SEP:
            nodeid = nodeid.replace(os.sep, nodes.SEP)
    else:
        nodeid = None

    self.parsefactories(plugin, nodeid)
```

--------------------------------

### Parse and Configure

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Parses and applies pytest configuration from arguments. It returns a Config object. This is useful for simulating the configuration phase of a pytest run.

```python
def parseconfigure(self, *args) -> Config:
    """See :meth:`Pytester.parseconfigure`."""
    return self._pytester.parseconfigure(*args)
```

--------------------------------

### Use Package-Scoped Fixture in Pytest Test

Source: https://docs.pytest.org/en/stable/example/simple

This Python code shows a pytest test function that utilizes the 'db' fixture defined in a conftest.py file. The 'db' fixture, scoped to the package, is injected into the test function, demonstrating its availability.

```python
# content of a/test_db.py
def test_a1(db):
    assert 0, db  # to show value
```

--------------------------------

### Pytest Report Generation Hook

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

The `pytest_runtest_makereport` hook is invoked to generate a `pytest.TestReport` for each of the setup, call, and teardown phases of a test item. It stops at the first non-None result. This hook can be implemented in conftest files within the item's directory or parent directories.

```python
@hookspec(firstresult=True)
def pytest_runtest_makereport(item: Item, call: CallInfo[None]) -> TestReport | None:
    """Called to create a :class:`~pytest.TestReport` for each of
    the setup, call and teardown runtest phases of a test item.

    See :hook:`pytest_runtest_protocol` for a description of the runtest protocol.

    :param item: The item.
    :param call: The :class:`~pytest.CallInfo` for the phase.

    Stops at first non-None result, see :ref:`firstresult`.

    Use in conftest plugins
    =======================

    Any conftest file can implement this hook. For a given item, only conftest
    files in the item's directory and its parent directories are consulted.
    """
    pass
```

--------------------------------

### Dynamically Add Pytest Markers Based on Test Names

Source: https://docs.pytest.org/en/stable/example/markers

Demonstrates how to automatically define pytest markers based on the names of test functions. This is achieved by implementing a hook in `conftest.py` that inspects test function names and registers markers accordingly. The example test module contains functions like `test_interface_simple`, `test_interface_complex`, `test_event_simple`, and `test_something_else`. The corresponding `conftest.py` would dynamically create markers like 'interface' and 'event'.

```python
# content of test_module.py


def test_interface_simple():
    assert 0


def test_interface_complex():
    assert 0


def test_event_simple():
    assert 0


def test_something_else():
    assert 0
```

--------------------------------

### Configure Pytest for Slow Tests with Custom Markers

Source: https://docs.pytest.org/en/stable/example/simple

This snippet demonstrates how to add a command-line option '--runslow' and a custom marker 'slow' to pytest. It includes logic to skip tests marked as 'slow' unless the '--runslow' option is provided during test execution. This allows for selective running of tests.

```python
import pytest

def pytest_addoption(parser):
    parser.addoption(
        "--runslow", action="store_true", default=False, help="run slow tests"
    )

def pytest_configure(config):
    config.addinivalue_line("markers", "slow: mark test as slow to run")

def pytest_collection_modifyitems(config, items):
    if config.getoption("--runslow"):
        # --runslow given in cli: do not skip slow tests
        return
    skip_slow = pytest.mark.skip(reason="need --runslow option to run")
    for item in items:
        if "slow" in item.keywords:
            item.add_marker(skip_slow)
```

--------------------------------

### Patch Dictionary Items with Monkeypatch

Source: https://docs.pytest.org/en/stable/how-to/monkeypatch

Demonstrates using `monkeypatch.setitem` to modify specific key-value pairs within a dictionary during tests. This is useful for testing functions that rely on configuration dictionaries without altering the original data. The example shows patching 'user' and 'database' in a 'DEFAULT_CONFIG' dictionary.

```python
# contents of app.py to generate a simple connection string
DEFAULT_CONFIG = {"user": "user1", "database": "db1"}


def create_connection_string(config=None):
    """Creates a connection string from input or defaults."""
    config = config or DEFAULT_CONFIG
    return f"User Id={config['user']}; Location={config['database']};"

# contents of test_app.py
# app.py with the connection string function (prior code block)
import app


def test_connection(monkeypatch):
    # Patch the values of DEFAULT_CONFIG to specific
    # testing values only for this test.
    monkeypatch.setitem(app.DEFAULT_CONFIG, "user", "test_user")
    monkeypatch.setitem(app.DEFAULT_CONFIG, "database", "test_db")

    # expected result based on the mocks
    expected = "User Id=test_user; Location=test_db;"

    # the test uses the monkeypatched dictionary settings
    result = app.create_connection_string()
    assert result == expected
```

--------------------------------

### Pytest Fixture Custom IDs with Strings and Functions

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Demonstrates how to assign custom IDs to parametrized fixtures using a list of strings or a function. The function can return a string or None, in which case pytest generates an ID. This helps in identifying specific test runs more clearly.

```python
import pytest


@pytest.fixture(params=[0, 1], ids=["spam", "ham"])
def a(request):
    return request.param


def test_a(a):
    pass


def idfn(fixture_value):
    if fixture_value == 0:
        return "eggs"
    else:
        return None


@pytest.fixture(params=[0, 1], ids=idfn)
def b(request):
    return request.param

def test_b(b):
    pass
```

--------------------------------

### Example of Node ID Format Change in Pytest

Source: https://docs.pytest.org/en/stable/changelog

Illustrates the change in how test class instances are represented in node IDs. The `::()` notation, previously used to denote a test class instance, has been removed for clarity and consistency. This change affects how tests are identified and potentially selected.

```text
Previous node id format: test_foo.py::Test::()::test_bar
New node id format: test_foo.py::Test::test_bar
```

--------------------------------

### Define Package-Scoped Fixture in Pytest

Source: https://docs.pytest.org/en/stable/example/simple

This Python code defines a package-scoped fixture named 'db' within a conftest.py file. This fixture will be available to all tests within the same directory and its subdirectories, providing a shared instance of the DB class.

```python
# content of a/conftest.py
import pytest


class DB:
    pass


@pytest.fixture(scope="package")
def db():
    return DB()
```

--------------------------------

### TestReport Object

Source: https://docs.pytest.org/en/stable/reference/reference

The TestReport object encapsulates the results of a single test item's execution, including setup, call, and teardown phases. It provides detailed information about the test's outcome, location, keywords, and captured output.

```APIDOC
## TestReport Class

### Description
Basic test report object, also used for setup and teardown calls if they fail. Reports can contain arbitrary extra attributes.

### Attributes
- **nodeid** (str) - Normalized collection nodeid.
- **location** (tuple[str, int | None, str]) - A (filesystempath, lineno, domaininfo) tuple indicating the actual location of a test item.
- **keywords** (Mapping[str, Any]) - A name -> value dictionary containing all keywords and markers associated with a test invocation.
- **outcome** (Literal['passed', 'failed', 'skipped']) - Test outcome.
- **longrepr** (None | ExceptionInfo[BaseException] | tuple[str, int, str] | str | TerminalRepr_) - None or a failure representation.
- **when** (Literal['setup', 'call', 'teardown']) - Indicates the runtest phase.
- **user_properties** (list[tuple[str, str]]) - User properties as a list of (name, value) tuples.
- **sections** (list[tuple[str, str]]) - Tuples of str `(heading, content)` with extra information for the test report.
- **duration** (float) - Time it took to run just the test.
- **start** (float) - The system time when the call started.
- **stop** (float) - The system time when the call ended.

### Properties
- **caplog** (str) - Return captured log lines, if log capturing is enabled. (Added in version 3.5)
- **capstderr** (str) - Return captured text from stderr, if capturing is enabled. (Added in version 3.0)
- **capstdout** (str) - Return captured text from stdout, if capturing is enabled. (Added in version 3.0)
- **_count_towards_summary** (bool) - Experimental: Whether this report should be counted towards the totals shown at the end of the test session.
- **_failed** (bool) - Whether the outcome is failed.
- **_fspath** (str) - The path portion of the reported node, as a string.
- **_head_line** (str | None) - Experimental: The head line shown with longrepr output for this report.
- **_longreprtext** (str) - Read-only property that returns the full string representation of `longrepr`. (Added in version 3.0)
- **_passed** (bool) - Whether the outcome is passed.
- **_skipped** (bool) - Whether the outcome is skipped.

### Class Methods
- **from_item_and_call**(_item_ , _call_) - Create and fill a TestReport with standard item and call info.
```

--------------------------------

### Open Process

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Opens a subprocess with specified command arguments and I/O redirection options. It returns a Popen object. This allows for fine-grained control over external process execution.

```python
def popen(
        self,
        cmdargs,
        stdout=subprocess.PIPE,
        stderr=subprocess.PIPE,
        stdin=CLOSE_STDIN,
        **kw,
    ):
        """See :meth:`Pytester.popen`."""
        return self._pytester.popen(cmdargs, stdout, stderr, stdin, **kw)
```

--------------------------------

### Update PYTEST_CURRENT_TEST Environment Variable

Source: https://docs.pytest.org/en/stable/_modules/_pytest/runner

Manages the PYTEST_CURRENT_TEST environment variable to reflect the current test item and its execution stage (setup, call, or teardown). If 'when' is None, the variable is removed from the environment. Handles potential null byte issues.

```python
import os
from typing import Literal

# Assuming 'Item' and 'Literal' are defined elsewhere in the context
# class Item:
#     def __init__(self, nodeid):
#         self.nodeid = nodeid
#         self.session = type('obj', (object,), {'_setupstate': type('obj', (object,), {'teardown_exact': lambda self, nextitem: None})})()

def _update_current_test_var(
    item: Item, when: Literal["setup", "call", "teardown"] | None
) -> None:
    """Update :envvar:`PYTEST_CURRENT_TEST` to reflect the current item and stage.

    If ``when`` is None, delete ``PYTEST_CURRENT_TEST`` from the environment.
    """
    var_name = "PYTEST_CURRENT_TEST"
    if when:
        value = f"{item.nodeid} ({when})"
        # don't allow null bytes on environment variables (see #2644, #2957)
        value = value.replace("\x00", "(null)")
        os.environ[var_name] = value
    else:
        os.environ.pop(var_name, None) # Use pop with default to avoid KeyError if not set
```

--------------------------------

### Pytest Function Class for Test Execution

Source: https://docs.pytest.org/en/stable/_modules/_pytest/python

Represents a Python test function within pytest. It handles setup, execution, and parameterization details, including managing markers and original function names. It inherits from PyobjMixin and nodes.Item.

```python
class Function(PyobjMixin, nodes.Item):
    """Item responsible for setting up and executing a Python test function.

    :param name:
        The full function name, including any decorations like those
        added by parametrization (``my_func[my_param]``).
    :param parent:
        The parent Node.
    :param config:
        The pytest Config object.
    :param callspec:
        If given, this function has been parametrized and the callspec contains
        meta information about the parametrization.
    :param callobj:
        If given, the object which will be called when the Function is invoked,
        otherwise the callobj will be obtained from ``parent`` using ``originalname``.
    :param keywords:
        Keywords bound to the function object for "-k" matching.
    :param session:
        The pytest Session object.
    :param fixtureinfo:
        Fixture information already resolved at this fixture node..
    :param originalname:
        The attribute name to use for accessing the underlying function object.
        Defaults to ``name``.
        Set this if name is different from the original name, for example when it contains decorations like those added by parametrization (``my_func[my_param]``).
    """

    # Disable since functions handle it themselves.
    _ALLOW_MARKERS = False

    def __init__(
        self,
        name: str,
        parent,
        config: Config | None = None,
        callspec: CallSpec2 | None = None,
        callobj=NOTSET,
        keywords: Mapping[str, Any] | None = None,
        session: Session | None = None,
        fixtureinfo: FuncFixtureInfo | None = None,
        originalname: str | None = None,
    ) -> None:
        super().__init__(name, parent, config=config, session=session)

        if callobj is not NOTSET:
            self._obj = callobj
            self._instance = getattr(callobj, "__self__", None)

        #: Original function name, without any decorations (for example
        #: parametrization adds a ``"[...]"`` suffix to function names), used to access
        #: the underlying function object from ``parent`` (in case ``callobj`` is not given
        #: explicitly).
        #: 
        #: .. versionadded:: 3.0
        self.originalname = originalname or name

        # Note: when FunctionDefinition is introduced, we should change ``originalname``
        # to a readonly property that returns FunctionDefinition.name.

        self.own_markers.extend(get_unpacked_marks(self.obj))
        if callspec:
            self.callspec = callspec
            self.own_markers.extend(callspec.marks)

        # todo: this is a hell of a hack
        # https://github.com/pytest-dev/pytest/issues/4569
        # Note: the order of the updates is important here; indicates what
        # takes priority (ctor argument over function attributes over markers).

```

--------------------------------

### Calling pytest.warns() on Functions or Code Strings

Source: https://docs.pytest.org/en/stable/how-to/capture-warnings

Demonstrates alternative ways to use pytest.warns() by directly passing a function with its arguments or a string representing code to be executed. This offers flexibility in testing different scenarios.

```python
import pytest

# Assuming 'my_function' and 'some_code_string' are defined elsewhere
# pytest.warns(expected_warning, my_function, arg1, arg2)
# pytest.warns(expected_warning, "my_function(arg1, arg2)")
```

--------------------------------

### Pytest Hook for Post-processing Test Reports

Source: https://docs.pytest.org/en/stable/example/simple

Implements a Pytest hook `pytest_runtest_makereport` to intercept test reports. This hook can be used to write failing test details, including accessed fixtures like `tmp_path`, to a file named 'failures'.

```python
import os.path

import pytest


@pytest.hookimpl(wrapper=True, tryfirst=True)
def pytest_runtest_makereport(item, call):
    # execute all other hooks to obtain the report object
    rep = yield

    # we only look at actual failing test calls, not setup/teardown
    if rep.when == "call" and rep.failed:
        mode = "a" if os.path.exists("failures") else "w"
        with open("failures", mode, encoding="utf-8") as f:
            # let's also access a fixture for the fun of it
            if "tmp_path" in item.fixturenames:
                extra = " ({})".format(item.funcargs["tmp_path"])
            else:
                extra = ""

            f.write(rep.nodeid + extra + "\n")

    return rep

```

--------------------------------

### Mark Plugins for Rewrite in Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Marks top-level modules and packages within pytest plugin distributions for assertion rewriting. It iterates through installed distributions, identifies plugins registered via the 'pytest11' entry point, and uses the provided assertion rewriting hook to mark them. Autoloading is disabled if specified.

```python
def _mark_plugins_for_rewrite(
    self,
    hook: AssertionRewritingHook,
    disable_autoload: bool,
) -> None:
    """Given an importhook, mark for rewrite any top-level
    modules or packages in the distribution package for
    all pytest plugins."""
    self.pluginmanager.rewrite_hook = hook

    if disable_autoload:
        # We don't autoload from distribution package entry points,
        # no need to continue.
        return

    package_files = (
        str(file)
        for dist in importlib.metadata.distributions()
        if any(ep.group == "pytest11" for ep in dist.entry_points)
        for file in dist.files or []
    )

    for name in _iter_rewritable_modules(package_files):
        hook.mark_rewrite(name)
```

--------------------------------

### Apply Multiple Warning Filters with Decorators

Source: https://docs.pytest.org/en/stable/how-to/capture-warnings

Specify multiple warning filters using separate `@pytest.mark.filterwarnings` decorators. This example ignores 'api v1' warnings but fails on all other warnings. Remember that decorators are processed in reverse order, so the filter listed first in the code will be applied last.

```python
# Ignore "api v1" warnings, but fail on all other warnings
@pytest.mark.filterwarnings("ignore:api v1")
@pytest.mark.filterwarnings("error")
def test_one():
    assert api_v1() == 1
```

--------------------------------

### Log Pytest Test Execution Report

Source: https://docs.pytest.org/en/stable/reference/reference

The `pytest_runtest_logreport` hook is a central point for processing `TestReport` objects generated during the setup, call, and teardown phases of test item execution. It allows for detailed inspection and handling of test results.

```python
def pytest_runtest_logreport(report):
    """Process the `TestReport` produced for each of the setup, call and teardown runtest phases of an item."""
    # Process the test report
```

--------------------------------

### Pytest Test Run Hooks and Logging Management

Source: https://docs.pytest.org/en/stable/_modules/_pytest/logging

Manages logging during the test execution loop and individual test phases (setup, call, teardown). It conditionally enables verbose output and uses custom context managers to capture and store log records associated with each test item.

```python
    @hookimpl(wrapper=True, tryfirst=True)
    def pytest_runtestloop(self, session: Session) -> Generator[None, object, object]:
        if session.config.option.collectonly:
            return (yield)

        if self._log_cli_enabled() and self._config.get_verbosity() < 1:
            # The verbose flag is needed to avoid messy test progress output.
            self._config.option.verbose = 1

        with catching_logs(self.log_cli_handler, level=self.log_cli_level):
            with catching_logs(self.log_file_handler, level=self.log_file_level):
                return (yield)  # Run all the tests.

    @hookimpl
    def pytest_runtest_logstart(self) -> None:
        self.log_cli_handler.reset()
        self.log_cli_handler.set_when("start")

    @hookimpl
    def pytest_runtest_logreport(self) -> None:
        self.log_cli_handler.set_when("logreport")

    @contextmanager
    def _runtest_for(self, item: nodes.Item, when: str) -> Generator[None]:
        """Implement the internals of the pytest_runtest_xxx() hooks."""
        with (
            catching_logs(
                self.caplog_handler,
                level=self.log_level,
            ) as caplog_handler,
            catching_logs(
                self.report_handler,
                level=self.log_level,
            ) as report_handler,
        ):
            caplog_handler.reset()
            report_handler.reset()
            item.stash[caplog_records_key][when] = caplog_handler.records
            item.stash[caplog_handler_key] = caplog_handler

            try:
                yield
            finally:
                log = report_handler.stream.getvalue().strip()
                item.add_report_section(when, "log", log)

    @hookimpl(wrapper=True)
    def pytest_runtest_setup(self, item: nodes.Item) -> Generator[None]:
        self.log_cli_handler.set_when("setup")

        empty: dict[str, list[logging.LogRecord]] = {}
        item.stash[caplog_records_key] = empty
        with self._runtest_for(item, "setup"):
            yield

    @hookimpl(wrapper=True)
    def pytest_runtest_call(self, item: nodes.Item) -> Generator[None]:
        self.log_cli_handler.set_when("call")

        with self._runtest_for(item, "call"):
            yield

    @hookimpl(wrapper=True)
    def pytest_runtest_teardown(self, item: nodes.Item) -> Generator[None]:
        self.log_cli_handler.set_when("teardown")

        try:
            with self._runtest_for(item, "teardown"):
                yield
        finally:
            del item.stash[caplog_records_key]
            del item.stash[caplog_handler_key]

    @hookimpl
    def pytest_runtest_logfinish(self) -> None:
        self.log_cli_handler.set_when("finish")
```

--------------------------------

### Pytester Class for Plugin Testing

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The Pytester class provides facilities for writing tests and configuration files, executing pytest in isolation, and matching expected output. It's ideal for black-box testing of pytest plugins by isolating the test run.

```python
from typing import List, Union, Callable, Dict, Final
from _pytest.main import ExitCode
from _pytest.pytester import LineMatcher, Pytester
from _pytest.nodes import Item
from _pytest.config.argparsing import Parser
from _pytest.main import Session
from _pytest.fixtures import FixtureRequest
import sys

@final
class Pytester:
    """
    Facilities to write tests/configuration files, execute pytest in isolation, and match
    against expected output, perfect for black-box testing of pytest plugins.

    It attempts to isolate the test run from external factors as much as possible, modifying
    the current working directory to :attr:`path` and environment variables during initialization.
    """

    __test__ = False

    CLOSE_STDIN: Final = object() # Using object() as a placeholder for NOTSET

    class TimeoutExpired(Exception):
        pass

    def __init__(
        self,
        request: FixtureRequest,
    ):
        # Initialization logic would go here
        pass
```

--------------------------------

### Get Log Messages from Records

Source: https://docs.pytest.org/en/stable/_modules/_pytest/logging

Retrieves log messages from captured records, excluding adornments like levels and timestamps for reliable comparison. Traceback or stack info is not included as it's added by the handler's formatter.

```python
return [r.getMessage() for r in self.records]
```

--------------------------------

### Get Current User Name (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/tmpdir

This function retrieves the current user's name. It handles potential import errors or OS/Key errors that might occur in certain environments, returning None if the username cannot be determined.

```python
def get_user() -> str | None:
    """Return the current user name, or None if getuser() does not work
    in the current environment (see #1010)."""
    try:
        # In some exotic environments, getpass may not be importable.
        import getpass

        return getpass.getuser()
    except (ImportError, OSError, KeyError):
        return None
```

--------------------------------

### Deprecate request.cached_setup

Source: https://docs.pytest.org/en/stable/changelog

Marks `request.cached_setup` as deprecated. This was a precursor to the fixture setup/teardown mechanism. Users should refer to the funcarg comparison section in the documentation.

```python
# This is a deprecation notice, no direct code snippet to show.
```

--------------------------------

### pytest_load_initial_conftests

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

This hook is called to load initial conftest files before command-line option parsing. It allows for early configuration and option registration.

```APIDOC
## pytest_load_initial_conftests

### Description
Called to implement the loading of :ref:`initial conftest files <pluginorder>` ahead of command line option parsing.

### Method
Standard hook

### Endpoint
N/A (Internal Pytest Hook)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```python
# This is a hook, not typically called directly.
# Example of internal usage:
pytest_load_initial_conftests(early_config, parser, args)
```

### Response
#### Success Response (200)
None (This hook does not return a value).

#### Response Example
```json
// No response body for this hook.
```
```

--------------------------------

### Pytester Methods

Source: https://docs.pytest.org/en/stable/reference/reference

Methods available on the Pytester fixture for creating files, directories, and running pytest.

```APIDOC
## Pytester Methods

### `make_hook_recorder(_pluginmanager_)`

#### Description
Create a new `HookRecorder` for a `PytestPluginManager`.

### `chdir()`

#### Description
Cd into the temporary directory. This is done automatically upon instantiation.

### `makefile(_ext_, *args, **kwargs)`

#### Description
Create new text file(s) in the test directory.

#### Parameters
- **ext** (_str_) - The extension the file(s) should use, including the dot, e.g. `.py`.
- **args** (_str_) - All args are treated as strings and joined using newlines. The result is written as contents to the file. The name of the file is based on the test function requesting this fixture.
- **kwargs** (_str_) - Each keyword is the name of a file, while the value of it will be written as contents of the file.

#### Returns
- The first created file (`pathlib.Path`).

#### Examples
```python
pytester.makefile(".txt", "line1", "line2")
pytester.makefile(".ini", pytest="[pytest]\naddopts=-rs\n")
```

*Note: To create binary files, use `pathlib.Path.write_bytes()` directly.*

### `makeconftest(_source_)`

#### Description
Write a `conftest.py` file.

#### Parameters
- **source** (_str_) - The contents of the file.

#### Returns
- The `conftest.py` file (`pathlib.Path`).

### `makeini(_source_)`

#### Description
Write a `tox.ini` file.

#### Parameters
- **source** (_str_) - The contents of the file.

#### Returns
- The `tox.ini` file (`pathlib.Path`).

### `maketoml(_source_)`

#### Description
Write a `pytest.toml` file.

#### Parameters
- **source** (_str_) - The contents of the file.

#### Returns
- The `pytest.toml` file (`pathlib.Path`).

### `getinicfg(_source_)`

#### Description
Return the pytest section from the tox.ini config file.

### `makepyprojecttoml(_source_)`

#### Description
Write a `pyproject.toml` file.

#### Parameters
- **source** (_str_) - The contents of the file.

#### Returns
- The `pyproject.toml` file (`pathlib.Path`).

### `makepyfile(*args, **kwargs)`

#### Description
Shortcut for `.makefile()` with a `.py` extension. Defaults to the test name with a `.py` extension, e.g `test_foobar.py`, overwriting existing files.

#### Examples
```python
def test_something(pytester):
    pytester.makepyfile("foobar") # Creates test_something.py
    pytester.makepyfile(custom="foobar") # Creates custom.py
```

### `maketxtfile(*args, **kwargs)`

#### Description
Shortcut for `.makefile()` with a `.txt` extension. Defaults to the test name with a `.txt` extension, e.g `test_foobar.txt`, overwriting existing files.

#### Examples
```python
def test_something(pytester):
    pytester.maketxtfile("foobar") # Creates test_something.txt
    pytester.maketxtfile(custom="foobar") # Creates custom.txt
```

### `syspathinsert(_path=None_)`

#### Description
Prepend a directory to `sys.path`, defaults to `path`. This is undone automatically when this object dies at the end of each test.

#### Parameters
- **path** (_str_ | _PathLike_ | _None_) - The path to prepend.

### `mkdir(_name_)`

#### Description
Create a new (sub)directory.

#### Parameters
- **name** (_str_ | _PathLike_) - The name of the directory, relative to the pytester path.

#### Returns
- The created directory (`pathlib.Path`).

### `mkpydir(_name_)`

#### Description
Create a new python package. This creates a (sub)directory with an empty `__init__.py` file so it gets recognised as a Python package.

#### Parameters
- **name** (_str_ | _PathLike_) - The name of the package directory.

### `copy_example(_name=None_)`

#### Description
Copy file from project’s directory into the testdir.

#### Parameters
- **name** (_str_ | _None_) - The name of the file to copy. If None, it copies the example file associated with the test.

```

--------------------------------

### Configure Import Mode for Pytest (TOML)

Source: https://docs.pytest.org/en/stable/explanation/goodpractices

This TOML snippet configures the import mode for pytest, recommending the use of 'importlib' import mode for new projects. This setting influences how pytest imports and discovers modules, impacting test execution and environment setup.

```toml
# Add this to your configuration file (e.g., pyproject.toml)
# For importlib import mode

```

--------------------------------

### Parse and Configure Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

The `parseconfigure` method extends `parseconfig` by also calling the `pytest_configure` hook. This ensures that the pytest configuration is fully set up and ready for test execution.

```python
def parseconfigure(self, *args: str | os.PathLike[str]) -> Config:
    """Return a new pytest configured Config instance.

    Returns a new :py:class:`pytest.Config` instance like
    :py:meth:`parseconfig`, but also calls the :hook:`pytest_configure`
    hook.
    """
    config = self.parseconfig(*args)
    config._do_configure()
    return config
```

--------------------------------

### Capture stdout/stderr as text with tee-ing enabled via capteesys

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

The `capteesys` fixture captures text output from `sys.stdout` and `sys.stderr` while also allowing the output to be passed through. This means output can be captured for testing and simultaneously displayed live. It returns a `CaptureFixture` instance.

```python
import pytest
from typing import Generator

class CaptureFixture:
    def readouterr(self) -> tuple[str, str]:
        pass

class SysCapture:
    pass

class CaptureManager:
    def set_fixture(self, fixture):
        pass
    def unset_fixture(self):
        pass

class SubRequest:
    config: object

@pytest.fixture
def capteesys(request: SubRequest) -> Generator[CaptureFixture, None, None]:
    r"""Enable simultaneous text capturing and pass-through of writes ... """
    capman: CaptureManager = request.config.pluginmanager.getplugin("capturemanager")
    capture_fixture = CaptureFixture(
        SysCapture, request, config=dict(tee=True), _ispytest=True
    )
    capman.set_fixture(capture_fixture)
    capture_fixture._start()
    yield capture_fixture
    capture_fixture.close()
    capman.unset_fixture()

# Example usage:
def test_output(capteesys):
    print("hello")
    captured = capteesys.readouterr()
    assert captured.out == "hello\n"
```

--------------------------------

### Get Default Ini Value by Type in Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config/argparsing

Provides the default value for a given pytest configuration option type when no default is explicitly supplied. This function handles various types including strings, lists, booleans, integers, and floats.

```python
def get_ini_default_for_type(
    type: Literal[
        "string", "paths", "pathlist", "args", "linelist", "bool", "int", "float"
    ],
) -> Any:
    """
    Used by addini to get the default value for a given config option type, when
    default is not supplied.
    """
    if type in ("paths", "pathlist", "args", "linelist"):
        return []
    elif type == "bool":
        return False
    elif type == "int":
        return 0
    elif type == "float":
        return 0.0
    else:
        return ""
```

--------------------------------

### Spawn Pytest Process

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Spawns a pytest process using pexpect and returns the spawn object. It takes a string command and an optional timeout. This is useful for interactive testing of pytest command-line behavior.

```python
def spawn_pytest(self, string: str, expect_timeout: float = 10.0) -> pexpect.spawn:
    """See :meth:`Pytester.spawn_pytest`."""
    return self._pytester.spawn_pytest(string, expect_timeout=expect_timeout)
```

--------------------------------

### Add Project Dependencies to Pytest Report Header

Source: https://docs.pytest.org/en/stable/example/simple

This Python code snippet for conftest.py defines a pytest hook to add custom information, such as project dependencies, to the pytest test session header. It takes a config object and returns a string to be displayed.

```python
# content of conftest.py


def pytest_report_header(config):
    return "project deps: mylib-1.1"
```

--------------------------------

### Node.fspath

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Provides the file system path of a node (e.g., test file or directory), as a legacy path object.

```APIDOC
## GET /node/fspath

### Description
(deprecated) Returns a legacy path copy of the node's path. This is typically the path to a test file or directory.

### Method
GET

### Endpoint
/node/fspath

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **fspath** (LEGACY_PATH) - The legacy path object of the node.

#### Response Example
```json
{
  "fspath": "/path/to/test_node"
}
```
```

--------------------------------

### Add Report Section to Pytest Item

Source: https://docs.pytest.org/en/stable/_modules/_pytest/nodes

The `add_report_section` method allows adding custom content to test reports. It takes a capture state ('setup', 'call', 'teardown'), a section key, and the content string. This is useful for including additional information like captured stdout or stderr.

```python
def add_report_section(self, when: str, key: str, content: str) -> None:
    """Add a new report section, similar to what's done internally to add
    stdout and stderr captured output::

        item.add_report_section("call", "stdout", "report section contents")

    :param str when:
        One of the possible capture states, ``"setup"``, ``"call"``, ``"teardown"``.
    :param str key:
        Name of the section, can be customized at will. Pytest uses ``"stdout"`` and
        ``"stderr"`` internally.
    :param str content:
        The full contents as a string.
    """
    if content:
        self._report_sections.append((when, key, content))
```

--------------------------------

### Execute Test Item Logic with runtestprotocol

Source: https://docs.pytest.org/en/stable/_modules/_pytest/runner

The core function that orchestrates the execution of a test item's setup, call, and teardown phases. It handles request object initialization for re-run tests and ensures proper cleanup of request-related attributes after execution. It also checks for session failure or stop signals to manage teardown.

```python
import pytest
from _pytest.main import Item, call_and_report
from _pytest.reports import TestReport

def runtestprotocol(
    item: Item, log: bool = True, nextitem: Item | None = None
) -> list[TestReport]:
    hasrequest = hasattr(item, "_request")
    if hasrequest and not item._request:  # type: ignore[attr-defined]
        item._initrequest()  # type: ignore[attr-defined]
    rep = call_and_report(item, "setup", log)
    reports = [rep]
    if rep.passed:
        if item.config.getoption("setupshow", False):
            show_test_item(item)
        if not item.config.getoption("setuponly", False):
            reports.append(call_and_report(item, "call", log))
    if item.session.shouldfail or item.session.shouldstop:
        nextitem = None
    reports.append(call_and_report(item, "teardown", log, nextitem=nextitem))
    if hasrequest:
        item._request = False  # type: ignore[attr-defined]
        item.funcargs = None  # type: ignore[attr-defined]
    return reports
```

--------------------------------

### Pytest End-to-End Login Test with Multiple Asserts

Source: https://docs.pytest.org/en/stable/how-to/fixtures

This Python code defines pytest fixtures for setting up an admin client, creating a user, managing a Selenium WebDriver instance, and initializing page objects. It then defines a test class `TestLandingPageSuccess` that uses an autouse login fixture to perform login before tests. Individual test methods verify the presence of a welcome message, a sign-out button, and a profile link.

```python
# contents of tests/end_to_end/test_login.py
from uuid import uuid4
from urllib.parse import urljoin

from selenium.webdriver import Chrome
import pytest

from src.utils.pages import LoginPage, LandingPage
from src.utils import AdminApiClient
from src.utils.data_types import User


@pytest.fixture(scope="class")
def admin_client(base_url, admin_credentials):
    return AdminApiClient(base_url, **admin_credentials)


@pytest.fixture(scope="class")
def user(admin_client):
    _user = User(name="Susan", username=f"testuser-{uuid4()}", password="P4$$word")
    admin_client.create_user(_user)
    yield _user
    admin_client.delete_user(_user)


@pytest.fixture(scope="class")
def driver():
    _driver = Chrome()
    yield _driver
    _driver.quit()


@pytest.fixture(scope="class")
def landing_page(driver, login):
    return LandingPage(driver)


class TestLandingPageSuccess:
    @pytest.fixture(scope="class", autouse=True)
    def login(self, driver, base_url, user):
        driver.get(urljoin(base_url, "/login"))
        page = LoginPage(driver)
        page.login(user)

    def test_name_in_header(self, landing_page, user):
        assert landing_page.header == f"Welcome, {user.name}!"

    def test_sign_out_button(self, landing_page):
        assert landing_page.sign_out_button.is_displayed()

    def test_profile_link(self, landing_page, user):
        profile_href = urljoin(base_url, f"/profile?id={user.profile_id}")
        assert landing_page.profile_link.get_attribute("href") == profile_href

```

--------------------------------

### Plain Assertion Example in Pytest History

Source: https://docs.pytest.org/en/stable/history

This code snippet illustrates the principle of using plain Python assertions, a core idea that influenced pytest's design. It emphasizes the desire for detailed feedback on assertion failures, moving beyond simple 'assertion failed' messages.

```python
assert x == y
```

--------------------------------

### Configure JUnit XML Duration Report (TOML, INI)

Source: https://docs.pytest.org/en/stable/how-to/output

Control how test durations are reported in JUnit XML. Configure 'junit_duration_report' to 'call' to report just call durations instead of total execution times. Supports TOML and INI formats.

```toml
[pytest]
junit_duration_report = "call"

```

```ini
[pytest]
junit_duration_report = call

```

--------------------------------

### Define Custom Pytest Marker with Arguments

Source: https://docs.pytest.org/en/stable/example/markers

Demonstrates how to define a custom pytest marker named 'my_marker' and attach a callable function 'hello_world' as an argument to it. This is achieved using pytest.mark.my_marker.with_args(). The output shows the marker's name and its arguments, confirming the function was successfully attached.

```python
import pytest

def hello_world(*args, **kwargs):
    return "Hello World"

@pytest.mark.my_marker.with_args(hello_world)
def test_with_args():
    pass
```

--------------------------------

### Get Test Reports by Name in Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

The `getreports` method retrieves a list of test reports associated with a specific outcome name (e.g., 'error', 'failed'). It filters out reports where `_pdbshown` is true, typically indicating they were already handled by the debugger.

```python
    def getreports(self, name: str):
        return [x for x in self.stats.get(name, ()) if not hasattr(x, "_pdbshown")]
```

--------------------------------

### Pytester Class

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

Facilities to write tests/configuration files, execute pytest in isolation, and match against expected output.

```APIDOC
## Pytester Class

### Description
Facilities to write tests/configuration files, execute pytest in isolation, and match against expected output, perfect for black-box testing of pytest plugins. It attempts to isolate the test run from external factors as much as possible.

### Attributes

- **__test__** (bool): Set to False to prevent this class from being collected as a test.
- **CLOSE_STDIN**: A constant, likely used for managing stdin.

### Inner Classes

#### TimeoutExpired(Exception)
An exception raised when a timeout occurs during a test run.

### Methods

#### __init__(self, request: FixtureRequest)
Initializes the Pytester instance. This method is part of the class constructor.

- **request** (FixtureRequest): The pytest FixtureRequest object.
```

--------------------------------

### Implement pytest_collection_modifyitems hook function

Source: https://docs.pytest.org/en/stable/how-to/writing_hook_functions

This example shows a typical implementation of the `pytest_collection_modifyitems` hook. This hook is called after all test items have been collected and allows for modification of the collected items list. Pytest validates the function signature during plugin registration.

```python
def pytest_collection_modifyitems(config, items):
    # called after collection is completed
    # you can modify the ``items`` list
    ...
```

--------------------------------

### Pytest Fixture with Cache

Source: https://docs.pytest.org/en/stable/how-to/cache

Demonstrates how to create a pytest fixture that utilizes the config.cache object to store and retrieve computed values. If a value is not found in the cache, an expensive computation is performed, and the result is stored for future use. This reduces redundant computations across test runs.

```python
import pytest

def expensive_computation():
    print("running expensive computation...")


@pytest.fixture
def mydata(pytestconfig):
    val = pytestconfig.cache.get("example/value", None)
    if val is None:
        expensive_computation()
        val = 42
        pytestconfig.cache.set("example/value", val)
    return val


def test_function(mydata):
    assert mydata == 23

```

--------------------------------

### pytest_cmdline_main

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

This hook is invoked to perform the main command-line action after configuration. The default implementation calls configure hooks and `pytest_runtestloop`. It stops at the first non-None result.

```APIDOC
## pytest_cmdline_main

### Description
Called for performing the main command line action. The default implementation will invoke the configure hooks and :hook:`pytest_runtestloop`.

Stops at first non-None result, see :ref:`firstresult`.

This hook is only called for :ref:`initial conftests <pluginorder>`.

### Method
`hookspec` (firstresult=True)

### Endpoint
N/A (Internal Pytest Hook)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```python
# This is a hook, not typically called directly.
# Example of internal usage:
pytest_cmdline_main(config)
```

### Response
#### Success Response (200)
- **exit_code** (`ExitCode` | `int` | `None`) - The exit code of the test run, or None if the hook chain did not determine an exit code.

#### Response Example
```json
{
  "exit_code": 0
}
```
```

--------------------------------

### Get Progress Information Message - Pytest

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

Generates a string representing the current test progress. It supports different modes, such as displaying the count of reported tests versus collected tests, or showing time-based progress. This message is used to update the progress indicator during test execution.

```python
def _get_progress_information_message(self) -> str:
        assert self._session
        collected = self._session.testscollected
        if self._show_progress_info == "count":
            if collected:
                progress = self.reported_progress
                counter_format = f"{{:{len(str(collected))}d}}"
                format_string = f" [{{counter_format}}/{{}}]"
                return format_string.format(progress, collected)
            return f" [ {collected} / {collected} ]"
        if self._show_progress_info == "times":
            if not collected:
                return ""
            all_reports = (
                self._get_reports_to_display("passed")
                + self._get_reports_to_display("xpassed")
                + self._get_reports_to_display("failed")
```

--------------------------------

### Pytest Test Definitions and Fixtures in Python

Source: https://docs.pytest.org/en/stable/how-to/output

This Python code defines various pytest test functions, including a fixture that raises an error, a passing test, a failing test, a test that errors during setup, a skipped test, an expected failure (xfail), and an expected pass (xpass). It showcases different test outcomes and how to mark tests.

```python
import pytest


@pytest.fixture
def error_fixture():
    assert 0


def test_ok():
    print("ok")


def test_fail():
    assert 0


def test_error(error_fixture):
    pass


def test_skip():
    pytest.skip("skipping this test")


def test_xfail():
    pytest.xfail("xfailing this test")


@pytest.mark.xfail(reason="always xfail")
def test_xpass():
    pass
```

--------------------------------

### Assert Only Specific Warnings with recwarn Fixture

Source: https://docs.pytest.org/en/stable/how-to/capture-warnings

Demonstrates how to use the recwarn fixture to assert that only a specific type of warning is issued and to retrieve and inspect that warning.

```python
def test_warning(recwarn):
    ...
    assert len(recwarn) == 1
    user_warning = recwarn.pop(UserWarning)
    assert issubclass(user_warning.category, UserWarning)
```

--------------------------------

### Keyword Matching for Marker Expressions in Pytest

Source: https://docs.pytest.org/en/stable/changelog

Enables selection of tests using marker keyword arguments. This feature allows for more flexible test targeting by supporting integer, string, boolean, and None values for marker keywords. Refer to the Pytest documentation for detailed examples on using this functionality.

```bash
# Select tests with a marker 'my_marker' and keyword argument 'version=1'
pytest -m "my_marker(version=1)"

# Select tests with a marker 'feature' and keyword argument 'enabled=True'
pytest -m "feature(enabled=True)"

# Select tests with a marker 'config' and keyword argument 'mode=None'
pytest -m "config(mode=None)"
```

--------------------------------

### Get Full Source Code (TracebackEntry)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/_code/code

Returns the source code of the failing statement. This method attempts to retrieve the source code using an AST cache if provided, otherwise it parses the source directly. It handles potential `SyntaxError` exceptions during parsing and returns a `Source` object representing the relevant code block.

```python
def getsource(
        self,
        astcache: dict[str | Path, ast.AST] | None = None
    ) -> Source | None:
        """Return failing source code."""
        # we use the passed in astcache to not reparse asttrees
        # within exception info printing
        source = self.frame.code.fullsource
        if source is None:
            return None
        key = astnode = None
        if astcache is not None:
            key = self.frame.code.path
            if key is not None:
                astnode = astcache.get(key, None)
        start = self.getfirstlinesource()
        try:
            astnode, _, end = getstatementrange_ast(
                self.lineno, source, astnode=astnode
            )
        except SyntaxError:
            end = self.lineno + 1
        else:
            if key is not None and astcache is not None:
                astcache[key] = astnode
        return source[start:end]

    source = property(getsource)
```

--------------------------------

### Set Node File System Path with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

The `Node_fspath_set` function allows setting the node's path using a legacy `py.path.local` object. It converts the input to a `pathlib.Path` object.

```python
def Node_fspath_set(self: Node, value: LEGACY_PATH) -> None:
    self.path = Path(value)
```

--------------------------------

### Pytest Test Report Stashing

Source: https://docs.pytest.org/en/stable/_modules/_pytest/tmpdir

This hook intercepts the creation of test reports. It stashes the 'passed' status of a test report for each phase ('setup', 'call', 'teardown') into the item's stash, keyed by the tmppath_result_key. This allows for later retrieval of test outcomes.

```python
@hookimpl(wrapper=True, tryfirst=True)
def pytest_runtest_makereport(
    item: Item,
    call
) -> Generator[None, TestReport, TestReport]:
    rep = yield
    assert rep.when is not None
    empty: dict[str, bool] = {}
    item.stash.setdefault(tmppath_result_key, empty)[rep.when] = rep.passed
    return rep
```

--------------------------------

### Node Reporter Initialization and Property Management

Source: https://docs.pytest.org/en/stable/_modules/_pytest/junitxml

Initializes a `_NodeReporter` instance, setting up attributes for XML reporting. It includes methods for adding custom properties and attributes, which are then escaped for XML compatibility.

```python
class _NodeReporter:
    def __init__(self, nodeid: str | TestReport, xml: LogXML) -> None:
        self.id = nodeid
        self.xml = xml
        self.add_stats = self.xml.add_stats
        self.family = self.xml.family
        self.duration = 0.0
        self.properties: list[tuple[str, str]] = []
        self.nodes: list[ET.Element] = []
        self.attrs: dict[str, str] = {}

    def append(self, node: ET.Element) -> None:
        self.xml.add_stats(node.tag)
        self.nodes.append(node)

    def add_property(self, name: str, value: object) -> None:
        self.properties.append((str(name), bin_xml_escape(value)))

    def add_attribute(self, name: str, value: object) -> None:
        self.attrs[str(name)] = bin_xml_escape(value)
```

--------------------------------

### Python Dictionary Deletion and Assignment

Source: https://docs.pytest.org/en/stable/_modules/_pytest/monkeypatch

Demonstrates safe deletion of a key from a dictionary using a try-except block to handle KeyErrors. Also shows how to assign a value to a key, with type ignore comments for potential compatibility issues with certain mapping types like TypedDict.

```python
del dictionary[key]  # type: ignore[attr-defined]
                except KeyError:
                    pass  # Was already deleted, so we have the desired state.
            else:
                # Not all Mapping types support indexing, but MutableMapping doesn't support TypedDict
                dictionary[key] = value  # type: ignore[index]
```

--------------------------------

### Pytest: Multiline Assertion Failure with Custom Message

Source: https://docs.pytest.org/en/stable/example/reportingdemo

This example demonstrates a Pytest test case with a multiline assertion failure. The custom error message spans multiple lines, providing a more detailed explanation of the discrepancy. Pytest formats the multiline message for readability.

```python
def test_multiline(self):
    class A:
        a = 1

    b = 2
    assert A.a == b,
        (
            "A.a appears not to be b\nor does not appear to be b\none of those"
        )
```

--------------------------------

### Parametrize Tests with Metafunc

Source: https://docs.pytest.org/en/stable/reference/reference

The `parametrize` method of the Metafunc object allows for dynamic generation of test cases. It takes argument names and their corresponding values, enabling multiple test invocations with different inputs. The `indirect` parameter can be used to defer expensive setup to fixture execution time.

```python
def pytest_generate_tests(metafunc):
    if "my_fixture" in metafunc.fixturenames:
        metafunc.parametrize("my_fixture", [1, 2, 3])
    if "x" in metafunc.fixturenames and "y" in metafunc.fixturenames:
        metafunc.parametrize("x,y", [("a", 1), ("b", 2)], indirect=["y"])
```

--------------------------------

### Control Test Skipping with Command-Line Option in Pytest

Source: https://docs.pytest.org/en/stable/example/simple

This snippet illustrates how to use a conftest.py file to add a '--runslow' command-line option. This option can then be used to control the execution of tests marked with '@pytest.mark.slow', allowing users to selectively run or skip slow tests.

```python
# content of conftest.py
import pytest


def pytest_addoption(parser):
    parser.addoption("--runslow", action="store_true", default=False, help="run slow tests")


@pytest.fixture(scope="session")
def runslow(request):
    return request.config.getoption("--runslow")


# Example usage in a test file (test_example.py):
# import pytest
# 
# @pytest.mark.slow
# def test_slow_operation():
#     assert True
# 
# def test_fast_operation():
#     assert True

```

--------------------------------

### Pytest Fixtures: Multiple Tests with Independent Fixture Instances

Source: https://docs.pytest.org/en/stable/how-to/fixtures

Illustrates how pytest provides independent instances of fixtures to different test functions, ensuring test isolation. 'test_string' and 'test_int' both use the 'order' fixture, demonstrating that modifications in one test do not affect the other.

```python
# contents of test_append.py
import pytest


# Arrange
@pytest.fixture
def first_entry():
    return "a"


# Arrange
@pytest.fixture
def order(first_entry):
    return [first_entry]


def test_string(order):
    # Act
    order.append("b")

    # Assert
    assert order == ["a", "b"]


def test_int(order):
    # Act
    order.append(2)

    # Assert
    assert order == ["a", 2]

```

--------------------------------

### Set Environment Variable (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/monkeypatch

Sets an environment variable to a specified value. Optionally prepends a value and a separator to the existing environment variable if it exists. Includes a warning and conversion to string if the value is not a string.

```python
import os
import warnings
from _pytest.main import PytestWarning

# Assuming 'self' is an instance of a class that has setitem and delitem methods
# For demonstration, we'll simulate these methods or use direct os.environ operations

class MockMonkeyPatch:
    def __init__(self):
        self._setitem = []

    def setitem(self, dic, name, value):
        self._setitem.append((dic, name, value))
        dic[name] = value

    def delitem(self, dic, name, raising=True):
        if name not in dic:
            if raising:
                raise KeyError(name)
        else:
            del dic[name]

    def setenv(self, name: str, value: str, prepend: str | None = None) -> None:
        """Set environment variable ``name`` to ``value``. 

        If ``prepend`` is a character, read the current environment variable
        value and prepend the ``value`` adjoined with the ``prepend``
        character.
        """
        if not isinstance(value, str):
            warnings.warn(
                PytestWarning(
                    f"Value of environment variable {name} type should be str, but got "
                    f"{value!r} (type: {type(value).__name__}); converted to str implicitly"
                ),
                stacklevel=2,
            )
            value = str(value)
        if prepend and name in os.environ:
            value = value + prepend + os.environ[name]
        self.setitem(os.environ, name, value)

# Example Usage:
mp = MockMonkeyPatch()
mp.setenv("MY_VAR", "my_value")
print(f"MY_VAR: {os.environ.get('MY_VAR')}")

mp.setenv("PREPEND_VAR", "new_value", prepend="|")
print(f"PREPEND_VAR: {os.environ.get('PREPEND_VAR')}")

# Example with non-string value
mp.setenv("INT_VAR", 123)
print(f"INT_VAR: {os.environ.get('INT_VAR')}")

```

--------------------------------

### Pytest Test Discovery and Class Structure in Python

Source: https://docs.pytest.org/en/stable/getting-started

Demonstrates how Pytest discovers test functions within a class. It shows a simple test class with two methods, 'test_one' and 'test_two'. Pytest automatically finds these tests if they follow naming conventions. The example also illustrates how classes prefixed with 'Test' are discovered, while others are skipped.

```python
class TestClass:
    def test_one(self):
        x = "this"
        assert "h" in x

    def test_two(self):
        x = "hello"
        assert hasattr(x, "check")
```

--------------------------------

### Pytest: Applying Indirect Parametrization to Specific Arguments

Source: https://docs.pytest.org/en/stable/example/parametrize

This snippet shows how to apply indirect parametrization to specific arguments when a test uses multiple fixtures. By passing a list or tuple of argument names to `indirect`, you can control which fixtures receive the indirect parametrization, allowing for selective setup at test run time.

```python
# content of test_indirect_list.py

import pytest


@pytest.fixture(scope="function")
def x(request):
    return request.param * 3


@pytest.fixture(scope="function")
def y(request):
    return request.param * 2


@pytest.mark.parametrize("x, y", [("a", "b")], indirect=["x"])
def test_indirect(x, y):
    assert x == "aaa"
    assert y == "b"

```

--------------------------------

### Configure Pytest Command-Line Options for Test Selection

Source: https://docs.pytest.org/en/stable/_modules/_pytest/mark

Shows how to add command-line options to pytest using `pytest_addoption`. This includes options for keyword expression matching (`-k`) and mark expression matching (`-m`), allowing users to filter tests during execution. It also covers the `--markers` option to display available markers.

```python
from _pytest.config.argparsing import Parser

def pytest_addoption(parser: Parser) -> None:
    group = parser.getgroup("general")
    group._addoption(
        "-k",
        action="store",
        dest="keyword",
        default="",
        metavar="EXPRESSION",
        help="Only run tests which match the given substring expression."
    )
    group._addoption(
        "-m",
        action="store",
        dest="markexpr",
        default="",
        metavar="MARKEXPR",
        help="Only run tests matching given mark expression."
    )
    group.addoption(
        "--markers",
        action="store_true",
        help="show markers (builtin, plugin and per-project ones)."
    )
    parser.addini("markers", "Register new markers for test functions", "linelist")
    parser.addini(EMPTY_PARAMETERSET_OPTION, "Default marker for empty parametersets")

```

--------------------------------

### Add Command-Line Options for JUnit XML (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/junitxml

Shows how to use `pytest_addoption` to register command-line arguments for controlling JUnit XML report generation. This includes options for the output file path (`--junitxml`), a prefix for classnames (`--junitprefix`), and various INI settings for suite name, logging, and duration reporting.

```python
def pytest_addoption(parser: Parser) -> None:
    group = parser.getgroup("terminal reporting")
    group.addoption(
        "--junitxml",
        "--junit-xml",
        action="store",
        dest="xmlpath",
        metavar="path",
        type=functools.partial(filename_arg, optname="--junitxml"),
        default=None,
        help="Create junit-xml style report file at given path",
    )
    group.addoption(
        "--junitprefix",
        "--junit-prefix",
        action="store",
        metavar="str",
        default=None,
        help="Prepend prefix to classnames in junit-xml output",
    )
    parser.addini(
        "junit_suite_name", "Test suite name for JUnit report", default="pytest"
    )
    parser.addini(
        "junit_logging",
        "Write captured log messages to JUnit report: "
        "one of no|log|system-out|system-err|out-err|all",
        default="no",
    )
    parser.addini(
        "junit_log_passing_tests",
        "Capture log information for passing tests to JUnit report: ",
        type="bool",
        default=True,
    )
    parser.addini(
        "junit_duration_report",
        "Duration time to report: one of total|call",
        default="total",
    )  # choices=['total', 'call'])
    parser.addini(
        "junit_family",
        "Emit XML for schema: one of legacy|xunit1|xunit2",
        default="xunit2",
    )
```

--------------------------------

### Get Python Frame Summary (TracebackEntry)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/_code/code

Retrieves a FrameSummary object for the current traceback entry. This method leverages Python's built-in `extract_tb` function to obtain detailed information about the frame, including column numbers, which are crucial for precise error reporting.

```python
def get_python_framesummary(self) -> FrameSummary:
    # Python's built-in traceback module implements all the nitty gritty
    # details to get column numbers of out frames.
    stack_summary = extract_tb(self._rawentry, limit=1)
    return stack_summary[0]
```

--------------------------------

### Session Fixture to Call Class Methods Before Tests (pytest)

Source: https://docs.pytest.org/en/stable/example/special

This pytest fixture, `callattr_ahead_of_alltests`, is session-scoped and automatically executed. It iterates through all collected test items, identifies their parent test classes, and if a class has a `callme` method, it invokes it. This allows for setup logic to be executed once per test session before any tests run.

```python
# content of conftest.py

import pytest


@pytest.fixture(scope="session", autouse=True)
def callattr_ahead_of_alltests(request):
    print("callattr_ahead_of_alltests called")
    seen = {None}
    session = request.node
    for item in session.items:
        cls = item.getparent(pytest.Class)
        if cls not in seen:
            if hasattr(cls.obj, "callme"):
                cls.obj.callme()
            seen.add(cls)

```

--------------------------------

### Testing Connection String Generation with Mocked Config

Source: https://docs.pytest.org/en/stable/how-to/monkeypatch

This test function verifies the `app.create_connection_string()` function by utilizing mocked user and database configurations provided by pytest fixtures. It asserts that the generated connection string matches the expected format based on the mocked settings. The test ensures the function correctly interpolates configuration values.

```python
import app
import pytest

def test_connection(mock_test_user, mock_test_database):
    expected = "User Id=test_user; Location=test_db;"

    result = app.create_connection_string()
    assert result == expected

```

--------------------------------

### Record Warnings with pytest.warns() Context Manager

Source: https://docs.pytest.org/en/stable/how-to/capture-warnings

Demonstrates how to use the pytest.warns() context manager to record warnings without asserting specific types. It captures warnings and allows assertions on the number and content of the recorded messages.

```python
import warnings

with pytest.warns() as record:
    warnings.warn("user", UserWarning)
    warnings.warn("runtime", RuntimeWarning)

assert len(record) == 2
assert str(record[0].message) == "user"
assert str(record[1].message) == "runtime"
```

--------------------------------

### Inspect Exception Value in Pytest Raises Context

Source: https://docs.pytest.org/en/stable/changelog

This example demonstrates how to correctly access the exception value within a `pytest.raises` context manager. Previously, directly inspecting the string representation of the exception info object (`str(e)`) was common. However, due to changes in `ExceptionInfo`'s string representation, it's now necessary to access the actual exception value via `e.value`.

```python
with pytest.raises(SomeException) as e:
    ...
assert "some message" in str(e.value)

```

--------------------------------

### Parse ini configuration with Legacy Path

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Parses an ini configuration string and returns it as a SectionWrapper object. This method delegates the parsing to the internal Pytester instance.

```python
def getinicfg(self, source: str) -> SectionWrapper:
    """See :meth:`Pytester.getinicfg`."""
    return self._pytester.getinicfg(source)
```

--------------------------------

### Check if Running within Pytest Session using PYTEST_VERSION

Source: https://docs.pytest.org/en/stable/changelog

The `PYTEST_VERSION` environment variable is now available at the start of a pytest session. This variable holds the pytest version string and can be used to determine if the current code execution is within a pytest run. It is undefined after the session ends.

```python
import os

if "PYTEST_VERSION" in os.environ:
    print(f"Running under pytest version: {os.environ['PYTEST_VERSION']}")
else:
    print("Not running under pytest.")
```

--------------------------------

### Pytest Log Report Processing Hook

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

The `pytest_runtest_logreport` hook is used to process the `pytest.TestReport` generated for each phase (setup, call, teardown) of a test item. It allows for custom handling of test reports. This hook can be implemented in conftest files within the item's directory or parent directories.

```python
def pytest_runtest_logreport(report: TestReport) -> None:
    """Process the :class:`~pytest.TestReport` produced for each
    of the setup, call and teardown runtest phases of an item.

    See :hook:`pytest_runtest_protocol` for a description of the runtest protocol.

    Use in conftest plugins
    =======================

    Any conftest file can implement this hook. For a given item, only conftest
    files in the item's directory and its parent directories are consulted.
    """
    pass
```

--------------------------------

### Register Method Setup/Teardown Fixture (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/python

Registers an autouse, function-scoped fixture to manage xUnit-style `setup_method` and `teardown_method`. It ensures these methods are called correctly for each test method within a class.

```python
from typing import Self, Iterable, Generator

# Assuming PyCollector, nodes, PytestCollectionWarning, safe_getattr, hasinit, hasnew, getimfunc, fixtures are defined elsewhere
# from pytest.collector import PyCollector
# from pytest.nodes import Item, Collector
# from pytest.warnings import PytestCollectionWarning
# from _pytest.main import safe_getattr
# from _pytest.python import hasinit, hasnew, getimfunc
# from _pytest.fixtures import getfixturemarker


class Class(PyCollector):
    """Collector for test methods (and nested classes) in a Python class."""



    @classmethod
    def from_parent(cls, parent, *, name, obj=None, **kw) -> Self:  # type: ignore[override]
        """The public constructor."""
        return super().from_parent(name=name, parent=parent, **kw)



    def newinstance(self):
        return self.obj()



    def collect(self) -> Iterable[nodes.Item | nodes.Collector]:
        if not safe_getattr(self.obj, "__test__", True):
            return []
        if hasinit(self.obj):
            assert self.parent is not None
            self.warn(
                PytestCollectionWarning(
                    f"cannot collect test class {self.obj.__name__!r} because it has a "
                    f"__init__ constructor (from: {self.parent.nodeid})"
                )
            )
            return []
        elif hasnew(self.obj):
            assert self.parent is not None
            self.warn(
                PytestCollectionWarning(
                    f"cannot collect test class {self.obj.__name__!r} because it has a "
                    f"__new__ constructor (from: {self.parent.nodeid})"
                )
            )
            return []

        self._register_setup_class_fixture()
        self._register_setup_method_fixture()

        self.session._fixturemanager.parsefactories(self.newinstance(), self.nodeid)

        return super().collect()



    def _register_setup_class_fixture(self) -> None:
        """Register an autouse, class scoped fixture into the collected class object
        that invokes setup_class/teardown_class if either or both are available.

        Using a fixture to invoke this methods ensures we play nicely and unsurprisingly with
        other fixtures (#517).
        """
        setup_class = _get_first_non_fixture_func(self.obj, ("setup_class",))
        teardown_class = _get_first_non_fixture_func(self.obj, ("teardown_class",))
        if setup_class is None and teardown_class is None:
            return

        def xunit_setup_class_fixture(request) -> Generator[None]:
            cls = request.cls
            if setup_class is not None:
                func = getimfunc(setup_class)
                _call_with_optional_argument(func, cls)
            yield
            if teardown_class is not None:
                func = getimfunc(teardown_class)
                _call_with_optional_argument(func, cls)

        self.session._fixturemanager._register_fixture(
            # Use a unique name to speed up lookup.
            name=f"_xunit_setup_class_fixture_{self.obj.__qualname__}",
            func=xunit_setup_class_fixture,
            nodeid=self.nodeid,
            scope="class",
            autouse=True,
        )

    def _register_setup_method_fixture(self) -> None:
        """Register an autouse, function scoped fixture into the collected class object
        that invokes setup_method/teardown_method if either or both are available.

        Using a fixture to invoke these methods ensures we play nicely and unsurprisingly with
        other fixtures (#517).
        """
        setup_name = "setup_method"
        setup_method = _get_first_non_fixture_func(self.obj, (setup_name,))
        teardown_name = "teardown_method"
        teardown_method = _get_first_non_fixture_func(self.obj, (teardown_name,))
        if setup_method is None and teardown_method is None:
            return

        def xunit_setup_method_fixture(request) -> Generator[None]:
            instance = request.instance
            method = request.function
            if setup_method is not None:
                func = getattr(instance, setup_name)
                _call_with_optional_argument(func, method)
            yield
            if teardown_method is not None:
                func = getattr(instance, teardown_name)
                _call_with_optional_argument(func, method)

        self.session._fixturemanager._register_fixture(
            # Use a unique name to speed up lookup.
            name=f"_xunit_setup_method_fixture_{self.obj.__qualname__}",
            func=xunit_setup_method_fixture,
            nodeid=self.nodeid,
            scope="function",
            autouse=True,
        )
```

--------------------------------

### Get Active Fixture Definition (Pytest)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

Finds and returns the `FixtureDef` object for a given argument name. It handles special cases like the 'request' fixture and checks for already computed fixtures. If a fixture is not found or not applicable, it raises a `FixtureLookupError`. It also manages fixture overriding and parametrization.

```python
def _get_active_fixturedef(self, argname: str) -> FixtureDef[object]:
        if argname == "request":
            return RequestFixtureDef(self)

        # If we already finished computing a fixture by this name in this item,
        # return it.
        fixturedef = self._fixture_defs.get(argname)
        if fixturedef is not None:
            self._check_scope(fixturedef, fixturedef._scope)
            return fixturedef

        # Find the appropriate fixturedef.
        fixturedefs = self._arg2fixturedefs.get(argname, None)
        if fixturedefs is None:
            # We arrive here because of a dynamic call to
            # getfixturevalue(argname) which was naturally
            # not known at parsing/collection time.
            fixturedefs = self._fixturemanager.getfixturedefs(argname, self._pyfuncitem)
            if fixturedefs is not None:
                self._arg2fixturedefs[argname] = fixturedefs
        # No fixtures defined with this name.
        if fixturedefs is None:
            raise FixtureLookupError(argname, self)
        # The are no fixtures with this name applicable for the function.
        if not fixturedefs:
            raise FixtureLookupError(argname, self)

        # A fixture may override another fixture with the same name, e.g. a
        # fixture in a module can override a fixture in a conftest, a fixture in
        # a class can override a fixture in the module, and so on.
        # An overriding fixture can request its own name (possibly indirectly); 
        # in this case it gets the value of the fixture it overrides, one level
        # up.
        # Check how many `argname`s deep we are, and take the next one.
        # `fixturedefs` is sorted from furthest to closest, so use negative
        # indexing to go in reverse.
        index = -1
        for request in self._iter_chain():
            if request.fixturename == argname:
                index -= 1
        # If already consumed all of the available levels, fail.
        if -index > len(fixturedefs):
            raise FixtureLookupError(argname, self)
        fixturedef = fixturedefs[index]

        # Prepare a SubRequest object for calling the fixture.
        try:
            callspec = self._pyfuncitem.callspec
        except AttributeError:
            callspec = None
        if callspec is not None and argname in callspec.params:
            param = callspec.params[argname]
            param_index = callspec.indices[argname]
            # The parametrize invocation scope overrides the fixture's scope.
            scope = callspec._arg2scope[argname]
        else:
            param = NOTSET
            param_index = 0
            scope = fixturedef._scope
            self._check_fixturedef_without_param(fixturedef)
        # The parametrize invocation scope only controls caching behavior while
        # allowing wider-scoped fixtures to keep depending on the parametrized
        # fixture. Scope control is enforced for parametrized fixtures
        # by recreating the whole fixture tree on parameter change.
        # Hence `fixturedef._scope`, not `scope`.
        self._check_scope(fixturedef, fixturedef._scope)
        subrequest = SubRequest(
            self, scope, param, param_index, fixturedef, _ispytest=True
        )

        # Make sure the fixture value is cached, running it if it isn't
        fixturedef.execute(request=subrequest)

        self._fixture_defs[argname] = fixturedef
        return fixturedef
```

--------------------------------

### Reorder Pytest Items Based on Scopes and Parameters

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

The `reorder_items` function orchestrates the reordering of Pytest items. It first collects parameter keys for each item across different high scopes and then uses `reorder_items_atscope` to recursively sort items based on these keys, starting from the session scope.

```python
from typing import Sequence, Iterator, Mapping, OrderedDict, TypeVar, Dict
from collections import defaultdict, deque
import sys

# Assuming nodes.Item, Scope, ParamArgKey, HIGH_SCOPES, OrderedSet, reorder_items_atscope are defined

def reorder_items(items: Sequence[nodes.Item]) -> list[nodes.Item]:
    argkeys_by_item: dict[Scope, dict[nodes.Item, OrderedSet[ParamArgKey]]] = {}
    items_by_argkey: dict[Scope, dict[ParamArgKey, OrderedDict[nodes.Item, None]]] = {}
    for scope in HIGH_SCOPES:
        scoped_argkeys_by_item = argkeys_by_item[scope] = {}
        scoped_items_by_argkey = items_by_argkey[scope] = defaultdict(OrderedDict)
        for item in items:
            argkeys = dict.fromkeys(get_param_argkeys(item, scope))
            if argkeys:
                scoped_argkeys_by_item[item] = argkeys
                for argkey in argkeys:
                    scoped_items_by_argkey[argkey][item] = None

    items_set = dict.fromkeys(items)
    return list(
        reorder_items_atscope(
            items_set, argkeys_by_item, items_by_argkey, Scope.Session
        )
    )

```

--------------------------------

### Forward Pytester Hook Recorder Creation

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Creates a hook recorder for managing pytest hooks, delegating the actual creation to the internal Pytester instance. This method ensures compatibility with legacy path handling.

```python
def make_hook_recorder(self, pluginmanager) -> HookRecorder:
    """See :meth:`Pytester.make_hook_recorder`."""
    return self._pytester.make_hook_recorder(pluginmanager)
```

--------------------------------

### Run Python Command

Source: https://docs.pytest.org/en/stable/_modules/_pytest/legacypath

Executes a Python command and returns a RunResult. This method is suitable for running short Python commands or expressions.

```python
def runpython_c(self, command):
    """See :meth:`Pytester.runpython_c`."""
    return self._pytester.runpython_c(command)
```

--------------------------------

### Capture file descriptor output as bytes with capfdbinary fixture

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

The `capfdbinary` fixture captures raw bytes written to file descriptors 1 and 2. The captured output is accessible via `readouterr()`, returning a namedtuple of bytes objects. This is suitable for testing scenarios involving binary data streams at the file descriptor level.

```python
import pytest
import os
from typing import Generator

class CaptureFixture:
    def readouterr(self) -> tuple[bytes, bytes]:
        pass

class FDCaptureBinary:
    pass

class CaptureManager:
    def set_fixture(self, fixture):
        pass
    def unset_fixture(self):
        pass

class SubRequest:
    config: object

@pytest.fixture
def capfdbinary(request: SubRequest) -> Generator[CaptureFixture, None, None]:
    r"""Enable bytes capturing of writes to file descriptors ``1`` and ``2``. ... """
    capman: CaptureManager = request.config.pluginmanager.getplugin("capturemanager")
    capture_fixture = CaptureFixture(FDCaptureBinary, request, _ispytest=True)
    capman.set_fixture(capture_fixture)
    capture_fixture._start()
    yield capture_fixture
    capture_fixture.close()
    capman.unset_fixture()

# Example usage:
def test_system_echo(capfdbinary):
    os.system('echo "hello"')
    captured = capfdbinary.readouterr()
    assert captured.out == b"hello\n"
```

--------------------------------

### Manage test state across runs with config.cache

Source: https://docs.pytest.org/en/stable/reference/reference

The config.cache fixture, accessed via pytestconfig.cache, allows plugins and fixtures to store and retrieve data between test runs. It utilizes the json module for serialization and deserialization. Key methods include mkdir for creating directories, get for retrieving values, and set for storing values.

```python
# Example usage within a fixture:
@pytest.fixture
def my_fixture(pytestconfig):
    cache = pytestconfig.cache
    # Use cache.get(), cache.set(), cache.mkdir()
    pass
```

--------------------------------

### Add Line to Configuration Option

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Appends a line to a configuration option that is expected to be a list of strings. If the option has not been set yet, this line becomes the first entry in its value.

```APIDOC
## POST /config/ini/{name}/append

### Description
Appends a given line to the value of a configuration option. This is typically used for options that store multiple lines or items, such as path lists or argument lists. The option must have been previously declared.

### Method
POST

### Endpoint
/config/ini/{name}/append

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the configuration option to modify.

#### Query Parameters
None

#### Request Body
- **line** (string) - Required - The line or item to append to the configuration option's value.

### Request Example
```json
{
  "line": "new_setting_value"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the line was added successfully.

#### Response Example
```json
{
  "message": "Line added successfully to configuration option 'option_name'."
}
```

#### Error Response (400)
- **error** (string) - Description of the error, e.g., "Configuration option 'option_name' is not a list."

#### Error Response Example
```json
{
  "error": "Configuration option 'option_name' is not a list."
}
```
```

--------------------------------

### Get ParamArgKeys for Pytest Items by Scope

Source: https://docs.pytest.org/en/stable/_modules/_pytest/fixtures

This Python function retrieves all `ParamArgKey` instances for a given Pytest `item` that match a specified high `scope`. It handles different scopes (Session, Package, Module, Class) by determining the appropriate `scoped_item_path` and `item_cls`. It returns an iterator of `ParamArgKey` objects.

```python
from typing import Iterator, Type, Optional
from pathlib import Path

# Assuming ParamArgKey, Scope, nodes.Item, CallSpec2, assert_never are defined elsewhere

def get_param_argkeys(item: nodes.Item, scope: Scope) -> Iterator[ParamArgKey]:
    """Return all ParamArgKeys for item matching the specified high scope."""
    assert scope is not Scope.Function

    try:
        callspec: CallSpec2 = item.callspec  # type: ignore[attr-defined]
    except AttributeError:
        return

    item_cls = None
    if scope is Scope.Session:
        scoped_item_path = None
    elif scope is Scope.Package:
        # Package key = module's directory.
        scoped_item_path = item.path.parent
    elif scope is Scope.Module:
        scoped_item_path = item.path
    elif scope is Scope.Class:
        scoped_item_path = item.path
        item_cls = item.cls  # type: ignore[attr-defined]
    else:
        assert_never(scope)

    for argname in callspec.indices:
        if callspec._arg2scope[argname] != scope:
            continue
        param_index = callspec.indices[argname]
        yield ParamArgKey(argname, param_index, scoped_item_path, item_cls)

```

--------------------------------

### Record Warnings with WarningsRecorder (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/recwarn

The WarningsRecorder class is a context manager that records raised warnings. It adapts the standard library's warnings.catch_warnings to store warnings as WarningMessage objects. It provides methods to access, iterate, and pop recorded warnings, and can be cleared.

```python
import warnings
from typing import Iterator, Self


def check_ispytest(value: bool) -> None:
    if not value:
        raise TypeError("This is an internal pytest API, and should not be called from user code.")


class WarningsRecorder(warnings.catch_warnings):
    """A context manager to record raised warnings.

    Each recorded warning is an instance of :class:`warnings.WarningMessage`.

    Adapted from `warnings.catch_warnings`.

    .. note::
        ``DeprecationWarning`` and ``PendingDeprecationWarning`` are treated
        differently; see :ref:`ensuring_function_triggers`.

    """

    def __init__(self, *, _ispytest: bool = False) -> None:
        check_ispytest(_ispytest)
        super().__init__(record=True)
        self._entered = False
        self._list: list[warnings.WarningMessage] = []

    @property
    def list(self) -> list[warnings.WarningMessage]:
        """The list of recorded warnings."""
        return self._list


    def __getitem__(self, i: int) -> warnings.WarningMessage:
        """Get a recorded warning by index."""
        return self._list[i]


    def __iter__(self) -> Iterator[warnings.WarningMessage]:
        """Iterate through the recorded warnings."""
        return iter(self._list)


    def __len__(self) -> int:
        """The number of recorded warnings."""
        return len(self._list)


    def pop(self, cls: type[Warning] = Warning) -> warnings.WarningMessage:
        """Pop the first recorded warning which is an instance of ``cls``,
        but not an instance of a child class of any other match.
        Raises ``AssertionError`` if there is no match.
        """
        best_idx: int | None = None
        for i, w in enumerate(self._list):
            if w.category == cls:
                return self._list.pop(i)  # exact match, stop looking
            if issubclass(w.category, cls) and (
                best_idx is None
                or not issubclass(w.category, self._list[best_idx].category)
            ):
                best_idx = i
        if best_idx is not None:
            return self._list.pop(best_idx)
        __tracebackhide__ = True
        raise AssertionError(f"{cls!r} not found in warning list")


    def clear(self) -> None:
        """Clear the list of recorded warnings."""
        self._list[:] = []

    # Type ignored because we basically want the `catch_warnings` generic type
    # parameter to be ourselves but that is not possible(?).
    def __enter__(self) -> Self:  # type: ignore[override]
        if self._entered:
            __tracebackhide__ = True
            raise RuntimeError(f"Cannot enter {self!r} twice")
        _list = super().__enter__()
        # record=True means it's None.
        assert _list is not None
        self._list = _list
        warnings.simplefilter("always")
        return self

    def __exit__(
        self,
        exc_type: type[BaseException] | None,
        exc_val: BaseException | None,
        exc_tb: TracebackType | None,
    ) -> None:
        if not self._entered:
            __tracebackhide__ = True
            raise RuntimeError(f"Cannot exit {self!r} without entering first")

        super().__exit__(exc_type, exc_val, exc_tb)

        # Built-in catch_warnings does not reset entered state so we do it
        # manually here for this context manager to become reusable.
        self._entered = False

```

--------------------------------

### Conditionally Display Verbose Information in Pytest Report Header

Source: https://docs.pytest.org/en/stable/example/simple

This Python code demonstrates how to conditionally add lines to the pytest report header based on the verbosity level. If the verbosity is greater than 0 (e.g., when using `pytest -v`), it returns a list of strings; otherwise, it returns nothing.

```python
# content of conftest.py


def pytest_report_header(config):
    if config.get_verbosity() > 0:
        return ["info1: did you know that ...", "did you?"]
```

--------------------------------

### Configure Pytest Truncation Limits (TOML, INI)

Source: https://docs.pytest.org/en/stable/how-to/output

Set custom truncation limits for pytest output to control the maximum number of lines or characters displayed. Setting limits to 0 disables truncation. Configuration can be done via TOML or INI files.

```toml
[pytest]
truncation_limit_lines = 10
truncation_limit_chars = 90

```

```ini
[pytest]
truncation_limit_lines = 10
truncation_limit_chars = 90

```

--------------------------------

### Handle INI Mode Configuration Values (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/config

Processes configuration values read in INI mode. It coerces string values into the appropriate type based on the registered configuration type, handling both single strings and lists of strings.

```python
def _getini_ini(
    self,
    name: str,
    canonical_name: str,
    type: str,
    value: str | list[str],
    default: Any,
):
    """Handle config values read in INI mode.

    In INI mode, values are stored as str or list[str] only, and coerced
    from string based on the registered type.
    """
    # Note: some coercions are only required if we are reading from .ini
    # files, because the file format doesn't contain type information, but
    # when reading from toml (in ini mode) we will get either str or list of
    # str values (see load_config_dict_from_file). For example:
    #
    #   ini:
    #     a_line_list = "tests acceptance"
    #
    # in this case, we need to split the string to obtain a list of strings.
    #
    #   toml (ini mode):
    #     a_line_list = ["tests", "acceptance"]
    #
    # in this case, we already have a list ready to use.
    
```

--------------------------------

### Generate Pytest Version and Environment Info

Source: https://docs.pytest.org/en/stable/_modules/_pytest/terminal

Constructs a message string containing Pytest version, PyPy version (if applicable), and Python executable path. This information is useful for debugging and reporting test environments.

```python
verinfo = ".".join(map(str, pypy_version_info[:3]))
msg += f"[pypy-{verinfo}-{pypy_version_info[3]}]"
msg += f", pytest-{_pytest._version.version}, pluggy-{pluggy.__version__}"
if (
    self.verbosity > 0
    or self.config.option.debug
    or getattr(self.config.option, "pastebin", None)
):
    msg += " -- " + str(sys.executable)
self.write_line(msg)
```

--------------------------------

### Pytest Report Filtering and Outcome Analysis

Source: https://docs.pytest.org/en/stable/_modules/_pytest/pytester

This Python code demonstrates methods for filtering and analyzing pytest test reports. It includes functions to get specific reports by name, filter by outcome (failed, passed, skipped), and count different outcomes. These are internal utilities for testing pytest's reporting mechanisms.

```python
def getfailures( 
    self,
    names: str | Iterable[str] = (
        "pytest_collectreport",
        "pytest_runtest_logreport",
    ),
) -> Sequence[CollectReport | TestReport]:
    return [rep for rep in self.getreports(names) if rep.failed]

def getfailedcollections(self) -> Sequence[CollectReport]:
    return self.getfailures("pytest_collectreport")

def listoutcomes(
    self,
) -> tuple[
    Sequence[TestReport],
    Sequence[CollectReport | TestReport],
    Sequence[CollectReport | TestReport],
]:
    passed = []
    skipped = []
    failed = []
    for rep in self.getreports(
        ("pytest_collectreport", "pytest_runtest_logreport")
    ):
        if rep.passed:
            if rep.when == "call":
                assert isinstance(rep, TestReport)
                passed.append(rep)
        elif rep.skipped:
            skipped.append(rep)
        else:
            assert rep.failed, f"Unexpected outcome: {rep!r}"
            failed.append(rep)
    return passed, skipped, failed

def countoutcomes(self) -> list[int]:
    return [len(x) for x in self.listoutcomes()]

def assertoutcome(self, passed: int = 0, skipped: int = 0, failed: int = 0) -> None:
    __tracebackhide__ = True
    from _pytest.pytester_assertions import assertoutcome

    outcomes = self.listoutcomes()
    assertoutcome(
        outcomes,
        passed=passed,
        skipped=skipped,
        failed=failed,
    )

def clear(self) -> None:
    self.calls[:] = []
```

--------------------------------

### CaptureFixture Class Initialization and Configuration

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Initializes the CaptureFixture, which is returned by Pytest's capsys and capfd fixtures. It takes a capture class, request object, and optional configuration. The constructor sets up internal state for capturing output.

```python
class CaptureFixture(Generic[AnyStr]):
    """Object returned by the :fixture:`capsys`, :fixture:`capsysbinary`,
    :fixture:`capfd` and :fixture:`capfdbinary` fixtures."""

    def __init__(
        self,
        captureclass: type[CaptureBase[AnyStr]],
        request: SubRequest,
        *, 
        config: dict[str, Any] | None = None,
        _ispytest: bool = False,
    ) -> None:
        check_ispytest(_ispytest)
        self.captureclass: type[CaptureBase[AnyStr]] = captureclass
        self.request = request
        self._config = config if config else {}
        self._capture: MultiCapture[AnyStr] | None = None
        self._captured_out: AnyStr = self.captureclass.EMPTY_BUFFER
        self._captured_err: AnyStr = self.captureclass.EMPTY_BUFFER
```

--------------------------------

### Store Incremental Test Failures in Pytest

Source: https://docs.pytest.org/en/stable/example/simple

This Python code implements pytest hooks to track failures within incrementally marked test classes. It stores the class name, parametrize index, and original test name for any failed test, allowing subsequent tests in the same class to be skipped.

```python
from typing import Dict, Tuple

_test_failed_incremental: Dict[str, Dict[Tuple[int, ...], str]] = {}

def pytest_runtest_makereport(item, call):
    if "incremental" in item.keywords:
        # incremental marker is used
        if call.excinfo is not None:
            # the test has failed
            # retrieve the class name of the test
            cls_name = str(item.cls)
            # retrieve the index of the test (if parametrize is used in combination with incremental)
            parametrize_index = (
                tuple(item.callspec.indices.values())
                if hasattr(item, "callspec")
                else ()
            )
            # retrieve the name of the test function
            test_name = item.originalname or item.name
            # store in _test_failed_incremental the original name of the failed test
            _test_failed_incremental.setdefault(cls_name, {}).setdefault(
                parametrize_index, test_name
            )

def pytest_runtest_setup(item):
    if "incremental" in item.keywords:
        # retrieve the class name of the test
        cls_name = str(item.cls)
        # check if a previous test has failed for this class
        if cls_name in _test_failed_incremental:
            # retrieve the index of the test (if parametrize is used in combination with incremental)
            parametrize_index = (
                tuple(item.callspec.indices.values())
                if hasattr(item, "callspec")
                else ()
            )
            # retrieve the name of the first test function to fail for this class name and index
            test_name = _test_failed_incremental[cls_name].get(parametrize_index, None)
            # if name found, test has failed for the combination of class name & test name
            if test_name is not None:
                pytest.xfail(f"previous test failed ({test_name})")
```

--------------------------------

### Parametrizing tests with pytest

Source: https://docs.pytest.org/en/stable/contents

Shows how to use pytest's parametrize decorator to run a test function multiple times with different arguments. This is a powerful technique for reducing code duplication and testing various scenarios efficiently.

```python
import pytest

@pytest.mark.parametrize("input, expected", [
    (1, 2),
    (3, 4),
    pytest.param(5, 6, marks=pytest.mark.xfail)
])
def test_addition(input, expected):
    assert input + 1 == expected

```

--------------------------------

### Implement pytest_leave_pdb Hook for PDB Exit Actions

Source: https://docs.pytest.org/en/stable/_modules/_pytest/hookspec

The pytest_leave_pdb hook is called immediately after the Python debugger (pdb) leaves interactive mode, for example, when continuing execution after a pdb.set_trace(). Plugins can utilize this hook to perform cleanup or post-debugging actions. It receives the pytest config object and the Pdb instance.

```python
import pdb
from pytest import Config

def pytest_leave_pdb(config: Config, pdb: pdb.Pdb) -> None:
    """Called when leaving pdb (e.g. with continue after pdb.set_trace()).

    Can be used by plugins to take special action just after the python
    debugger leaves interactive mode.

    :param config: The pytest config object.
    :param pdb: The Pdb instance.

    Use in conftest plugins
    =======================

    Any conftest plugin can implement this hook.
    """
    # Implementation details would go here
    pass
```

--------------------------------

### Apply Warning Filters with @pytest.mark.filterwarnings Decorator

Source: https://docs.pytest.org/en/stable/how-to/capture-warnings

Use the `@pytest.mark.filterwarnings` decorator to apply warning filters to specific test items, classes, or modules. This example ignores 'api v1' warnings for a specific test function. Decorators are evaluated in reverse order, meaning earlier decorators take precedence.

```python
import warnings


def api_v1():
    warnings.warn(UserWarning("api v1, should use functions from v2"))
    return 1


@pytest.mark.filterwarnings("ignore:api v1")
def test_one():
    assert api_v1() == 1
```

--------------------------------

### Add Custom Command-Line Option in Pytest conftest.py

Source: https://docs.pytest.org/en/stable/example/simple

This snippet shows how to add a custom command-line option '--cmdopt' to pytest using the pytest_addoption hook in conftest.py. It defines the option's action, default value, and help text. The fixture 'cmdopt' then retrieves the value of this option for use in tests.

```python
import pytest

def pytest_addoption(parser):
    parser.addoption(
        "--cmdopt", action="store", default="type1", help="my option: type1 or type2"
    )


@pytest.fixture
def cmdopt(request):
    return request.config.getoption("--cmdopt")
```

--------------------------------

### Pytest Command-Line Options for Configuration

Source: https://docs.pytest.org/en/stable/_modules/_pytest/main

Defines command-line arguments for pytest to control test collection, configuration loading, and debugging. These options allow users to specify directories, disable conftest files, manage duplicate tests, and set base temporary directories.

```python
group.addoption(
        "--confcutdir",
        type=functools.partial(directory_arg, optname="--confcutdir"),
        help="Only load conftest.py's relative to specified dir",
    )
    group.addoption(
        "--noconftest",
        action="store_true",
        dest="noconftest",
        default=False,
        help="Don't load any conftest.py files",
    )
    group.addoption(
        "--keepduplicates",
        "--keep-duplicates",
        action="store_true",
        dest="keepduplicates",
        default=False,
        help="Keep duplicate tests",
    )
    group.addoption(
        "--collect-in-virtualenv",
        action="store_true",
        dest="collect_in_virtualenv",
        default=False,
        help="Don't ignore tests in a local virtualenv directory",
    )
    group.addoption(
        "--continue-on-collection-errors",
        action="store_true",
        default=False,
        dest="continue_on_collection_errors",
        help="Force test execution even if collection errors occur",
    )
    group.addoption(
        "--import-mode",
        default="prepend",
        choices=["prepend", "append", "importlib"],
        dest="importmode",
        help="Prepend/append to sys.path when importing test modules and conftest "
        "files. Default: prepend.",
    )
    group._addoption(  # private to use reserved lower-case short option
        "-c",
        "--config-file",
        metavar="FILE",
        type=str,
        dest="inifilename",
        help="Load configuration from `FILE` instead of trying to locate one of the "
        "implicit configuration files.",
    )
    group.addoption(
        "--rootdir",
        action="store",
        dest="rootdir",
        help="Define root directory for tests. Can be relative path: 'root_dir', './root_dir', "
        "'root_dir/another_dir/'; absolute path: '/home/user/root_dir'; path with variables: "
        "'$HOME/root_dir'.",
    )
    group.addoption(
        "--basetemp",
        dest="basetemp",
        default=None,
        type=validate_basetemp,
        metavar="dir",
        help=(
            "Base temporary directory for this test run. "
            "(Warning: this directory is removed if it exists.)"
        ),
    )
```

--------------------------------

### Detect Pytest Execution Environment

Source: https://docs.pytest.org/en/stable/example/simple

This code snippet shows how to detect if the current execution environment is within a pytest run. It checks for the presence of the 'PYTEST_VERSION' environment variable, which pytest sets. This allows application code to conditionally execute different logic based on whether it's being run by pytest or in a standard environment.

```python
import os


if os.environ.get("PYTEST_VERSION") is not None:
    # Things you want to to do if your code is called by pytest.
    ...
else:
    # Things you want to to do if your code is not called by pytest.
    ...
```

--------------------------------

### Get Log Level from Pytest Configuration

Source: https://docs.pytest.org/en/stable/_modules/_pytest/logging

This function retrieves a log level from pytest configuration options or ini files. It iterates through provided setting names, checks for the log level in options and then ini files. It handles string representations of log levels (e.g., 'INFO', 'DEBUG') and converts them to integer values, raising a UsageError for unrecognized levels.

```python
from _pytest.config import Config
from _pytest.main import UsageError
import logging

def get_log_level_for_setting(config: Config, *setting_names: str) -> int | None:
    for setting_name in setting_names:
        log_level = config.getoption(setting_name)
        if log_level is None:
            log_level = config.getini(setting_name)
        if log_level:
            break
    else:
        return None

    if isinstance(log_level, str):
        log_level = log_level.upper()
    try:
        return int(getattr(logging, log_level, log_level))
    except ValueError as e:
        raise UsageError(
            f"'{log_level}' is not recognized as a logging level name for "
            f"'{setting_name}'. Please consider passing the "
            "logging level num instead."
        ) from e
```

--------------------------------

### Define and Use Pytest Fixtures

Source: https://docs.pytest.org/en/stable/explanation/fixtures

This Python code demonstrates how to define and use pytest fixtures. It includes a simple class `Fruit`, two fixtures (`my_fruit` and `fruit_basket`) where `fruit_basket` depends on `my_fruit`, and a test function that uses both fixtures to assert a condition.

```python
import pytest


class Fruit:
    def __init__(self, name):
        self.name = name

    def __eq__(self, other):
        return self.name == other.name


@pytest.pytest.fixture
def my_fruit():
    return Fruit("apple")


@pytest.pytest.fixture
def fruit_basket(my_fruit):
    return [Fruit("banana"), my_fruit]


def test_my_fruit_in_basket(my_fruit, fruit_basket):
    assert my_fruit in fruit_basket

```

--------------------------------

### Get Source Code Statement (TracebackEntry)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/_code/code

Retrieves the source code for the current statement within the traceback entry. It utilizes the `fullsource` attribute of the frame's code object and the `getstatement` method to pinpoint the exact line of code that caused the error. An optional AST cache can be provided to optimize parsing.

```python
@property
    def statement(self) -> Source:
        """_pytest._code.Source object for the current statement."""
        source = self.frame.code.fullsource
        assert source is not None
        return source.getstatement(self.lineno)
```

--------------------------------

### Initialize Last Failed Plugin

Source: https://docs.pytest.org/en/stable/_modules/_pytest/cacheprovider

Initializes the plugin, loading previously failed test information from the cache if the '--lf' option is enabled. It also registers a wrapper plugin for collection.

```python
self.lastfailed: dict[str, bool] = config.cache.get("cache/lastfailed", {})
        self._previously_failed_count: int | None = None
        self._report_status: str | None = None
        self._skipped_files = 0  # count skipped files during collection due to --lf

        if config.getoption("lf"):
            self._last_failed_paths = self.get_last_failed_paths()
            config.pluginmanager.register(
                LFPluginCollWrapper(self), "lfplugin-collwrapper"
            )
```

--------------------------------

### CaptureFixture: Suspending and Resuming Capture

Source: https://docs.pytest.org/en/stable/_modules/_pytest/capture

Helper methods `_suspend` and `_resume` allow for temporary suspension and resumption of the capture fixture's own capturing. This is useful for scenarios where capturing needs to be temporarily halted.

```python
    def _suspend(self) -> None:
        """Suspend this fixture's own capturing temporarily."""
        if self._capture is not None:
            self._capture.suspend_capturing()
```

```python
    def _resume(self) -> None:
        """Resume this fixture's own capturing temporarily."""
        if self._capture is not None:
            self._capture.resume_capturing()
```

--------------------------------

### Custom Type Validation for Command-Line Option in Pytest

Source: https://docs.pytest.org/en/stable/example/simple

This snippet demonstrates advanced command-line option validation in pytest. It defines a custom function 'type_checker' that raises a pytest.UsageError for invalid input formats. This function is then used as the 'type' for the '--cmdopt' option, allowing for more specific error messages.

```python
import pytest


def type_checker(value):
    msg = "cmdopt must specify a numeric type as typeNNN"
    if not value.startswith("type"):
        raise pytest.UsageError(msg)
    try:
        int(value[4:])
    except ValueError:
        raise pytest.UsageError(msg)

    return value


def pytest_addoption(parser):
    parser.addoption(
        "--cmdopt",
        action="store",
        default="type1",
        help="my option: type1 or type2",
        type=type_checker,
    )
```

--------------------------------

### Create Cache Directory and Supporting Files (Python)

Source: https://docs.pytest.org/en/stable/_modules/_pytest/cacheprovider

This function ensures the cache directory exists and creates necessary supporting files like README.md, .gitignore, and CACHEDIR.TAG. It handles potential race conditions during directory creation and renaming.

```python
def _ensure_cache_dir_and_supporting_files(self) -> None:
    """Create the cache dir and its supporting files."""
    if self._cachedir.is_dir():
        return

    self._cachedir.parent.mkdir(parents=True, exist_ok=True)
    with tempfile.TemporaryDirectory(
        prefix="pytest-cache-files-",
        dir=self._cachedir.parent,
    ) as newpath:
        path = Path(newpath)

        # Reset permissions to the default, see #12308.
        # Note: there's no way to get the current umask atomically, eek.
        umask = os.umask(0o022)
        os.umask(umask)
        path.chmod(0o777 - umask)

        with open(path.joinpath("README.md"), "x", encoding="UTF-8") as f:
            f.write(README_CONTENT)
        with open(path.joinpath(".gitignore"), "x", encoding="UTF-8") as f:
            f.write("# Created by pytest automatically.\n*")
        with open(path.joinpath("CACHEDIR.TAG"), "xb") as f:
            f.write(CACHEDIR_TAG_CONTENT)

        try:
            path.rename(self._cachedir)
        except OSError as e:
            # If 2 concurrent pytests both race to the rename, the loser
            # gets "Directory not empty" from the rename. In this case,
            # everything is handled so just continue (while letting the
            # temporary directory be cleaned up).
            # On Windows, the error is a FileExistsError which translates to EEXIST.
            if e.errno not in (errno.ENOTEMPTY, errno.EEXIST):
                raise
        else:
            # Create a directory in place of the one we just moved so that
            # `TemporaryDirectory`'s cleanup doesn't complain.
            #
            # TODO: pass ignore_cleanup_errors=True when we no longer support python < 3.10.
            # See https://github.com/python/cpython/issues/74168. Note that passing
            # delete=False would do the wrong thing in case of errors and isn't supported
            # until python 3.12.
            path.mkdir()
```

--------------------------------

### Configure Doctest Options in Pytest (TOML)

Source: https://docs.pytest.org/en/stable/how-to/doctest

This snippet shows how to configure pytest to use specific doctest options by setting the 'doctest_optionflags' in a TOML configuration file. It enables ignoring trailing whitespace and detailed exception stack traces.

```toml
[pytest]
doctest_optionflags = ["NORMALIZE_WHITESPACE", "IGNORE_EXCEPTION_DETAIL"]

```

--------------------------------

### Handling ExceptionGroups with RaisesGroup in Python

Source: https://docs.pytest.org/en/stable/_modules/_pytest/raises

Demonstrates how to use the `RaisesGroup` class to assert conditions on `ExceptionGroup` instances. It covers initialization with expected exceptions, handling nested structures, and matching exceptions within a context manager. The `allow_unwrapped` flag and `flatten_subgroups` parameter are explained.

```python
from typing import TypeVar, Sequence, TypeGuard
from types import GenericAlias

from _pytest.python_api import ExceptionInfo
from _pytest.main import ExitCode

# Assuming these classes are defined elsewhere in the library
class BaseExcT_co: pass
class BaseExcT_1: pass
class BaseExcT_2: pass
class ExcT_1: pass
class BaseException: pass
class BaseExceptionGroup(BaseException):
    exceptions: Sequence[BaseException]
    def __init__(self, msg, excs):
        super().__init__(msg)
        self.exceptions = excs

class ExceptionGroup(BaseExceptionGroup):
    exceptions: Sequence[BaseException]
    def __init__(self, msg, excs):
        super().__init__(msg, excs)


class RaisesExc[BaseExcT_co]:
    is_baseexception: bool
    _nested: bool
    def __init__(self, *args, **kwargs):
        pass

class RaisesGroup[BaseExcT_co]:
    allow_unwrapped: bool
    flatten_subgroups: bool
    match: object
    check: object
    is_baseexception: bool
    expected_exceptions: tuple
    excinfo: ExceptionInfo[BaseExceptionGroup[BaseExcT_co]]

    def __init__(
        self,
        expected_exception: type[BaseExcT_co] | RaisesExc[BaseExcT_1] | RaisesGroup[BaseExcT_2] | tuple,
        *other_exceptions: type[BaseExcT_co] | RaisesExc[BaseExcT_1] | RaisesGroup[BaseExcT_2],
        allow_unwrapped: bool = False,
        flatten_subgroups: bool = False,
        match: object = None,
        check: object = None,
    ):
        """RaisesGroup constructor.

        If `allow_unwrapped` is True, the `match` and `check` parameters are bypassed
        if the exception is unwrapped. If you intended to match/check the
        exception you should use a `RaisesExc` object. If you want to match/check
        the exceptiongroup when the exception *is* wrapped you need to
        do e.g. `if isinstance(exc.value, ExceptionGroup):
        assert RaisesGroup(...).matches(exc.value)` afterwards.
        """
        self.expected_exceptions: tuple[
            type[BaseExcT_co] | RaisesExc[BaseExcT_1] | RaisesGroup[BaseExcT_2], ...
        ] = tuple(
            self._parse_excgroup(e, "a BaseException type, RaisesExc, or RaisesGroup")
            for e in (
                expected_exception,
                *other_exceptions,
            )
        )

    def _parse_excgroup(
        self,
        exc: (
            type[BaseExcT_co]
            | GenericAlias
            | RaisesExc[BaseExcT_1]
            | RaisesGroup[BaseExcT_2]
        ),
        expected: str,
    ) -> type[BaseExcT_co] | RaisesExc[BaseExcT_1] | RaisesGroup[BaseExcT_2]:
        # verify exception type and set `self.is_baseexception`
        if isinstance(exc, RaisesGroup):
            if self.flatten_subgroups:
                raise ValueError(
                    "You cannot specify a nested structure inside a RaisesGroup with"
                    " `flatten_subgroups=True`. The parameter will flatten subgroups"
                    " in the raised exceptiongroup before matching, which would never"
                    " match a nested structure."
                )
            self.is_baseexception |= exc.is_baseexception
            exc._nested = True
            return exc
        elif isinstance(exc, RaisesExc):
            self.is_baseexception |= exc.is_baseexception
            exc._nested = True
            return exc
        elif isinstance(exc, tuple):
            raise TypeError(
                f"Expected {expected}, but got {type(exc).__name__!r}.\n"
                "RaisesGroup does not support tuples of exception types when expecting one of "
                "several possible exception types like RaisesExc.\n"
                "If you meant to expect a group with multiple exceptions, list them as separate arguments."
            )
        else:
            return super()._parse_exc(exc, expected)

    @overload
    def __enter__(
        self: "RaisesGroup[ExcT_1]",
    ) -> ExceptionInfo[ExceptionGroup[ExcT_1]]: ...
    @overload
    def __enter__(
        self: "RaisesGroup[BaseExcT_1]",
    ) -> ExceptionInfo[BaseExceptionGroup[BaseExcT_1]]: ...

    def __enter__(self) -> ExceptionInfo[BaseExceptionGroup[BaseException]]:
        self.excinfo: ExceptionInfo[BaseExceptionGroup[BaseExcT_co]] = (
            ExceptionInfo.for_later()
        )
        return self.excinfo

    def __repr__(self) -> str:
        reqs = [
            e.__name__ if isinstance(e, type) else repr(e)
            for e in self.expected_exceptions
        ]
        if self.allow_unwrapped:
            reqs.append(f"allow_unwrapped={self.allow_unwrapped}")
        if self.flatten_subgroups:
            reqs.append(f"flatten_subgroups={self.flatten_subgroups}")
        if self.match is not None:
            # If no flags were specified, discard the redundant re.compile() here.
            reqs.append(f"match={_match_pattern(self.match)!r}")
        if self.check is not None:
            reqs.append(f"check={repr_callable(self.check)}")
        return f"RaisesGroup({', '.join(reqs)})"

    def _unroll_exceptions(
        self,
        exceptions: Sequence[BaseException],
    ) -> Sequence[BaseException]:
        """Used if `flatten_subgroups=True`."""
        res: list[BaseException] = []
        for exc in exceptions:
            if isinstance(exc, BaseExceptionGroup):
                res.extend(self._unroll_exceptions(exc.exceptions))

            else:
                res.append(exc)
        return res

    @overload
    def matches(
        self: "RaisesGroup[ExcT_1]",
        exception: BaseException | None,
    ) -> TypeGuard[ExceptionGroup[ExcT_1]]: ...
    @overload
    def matches(
        self: "RaisesGroup[BaseExcT_1]",
        exception: BaseException | None,
    ) -> TypeGuard[BaseExceptionGroup[BaseExcT_1]]: ...



    def matches(
        self,
        exception: BaseException | None,
    ) -> bool:
        """Check if an exception matches the requirements of this RaisesGroup.
        If it fails, `RaisesGroup.fail_reason` will be set.

        Example::

            with pytest.raises(TypeError) as excinfo:
                ...
            assert RaisesGroup(ValueError).matches(excinfo.value.__cause__)
            # the above line is equivalent to
            myexc = excinfo.value.__cause
            assert isinstance(myexc, BaseExceptionGroup)
            assert len(myexc.exceptions) == 1
        """
        # Placeholder for actual matching logic
        return False

# Dummy implementations for functions used in __repr__
def _match_pattern(pattern):
    return pattern

def repr_callable(callable_obj):
    return repr(callable_obj)

# Dummy implementation for super()._parse_exc
class BaseClass:
    def _parse_exc(self, exc, expected):
        return exc

# Example usage (conceptual, requires pytest and actual exception raising)
# class MockExceptionInfo:
#     def __init__(self, value):
#         self.value = value
#
# class MockPytest:
#     class raises:
#         def __init__(self, exc_type):
#             self.exc_type = exc_type
#             self.value = None
#         def __enter__(self):
#             return self
#         def __exit__(self, exc_type, exc_val, exc_tb):
#             if exc_type is not None and issubclass(exc_type, self.exc_type):
#                 self.value = exc_val
#                 return True
#             return False
#
# pytest = MockPytest()
#
# try:
#     raise TypeError("Outer error", (ValueError("Inner error 1"), TypeError("Inner error 2")))
# except TypeError as e:
#     excinfo = MockExceptionInfo(e)
#     # Example 1: Matching a specific inner exception
#     assert RaisesGroup(ValueError).matches(excinfo.value.__cause__)
#
#     # Example 2: Matching an ExceptionGroup with specific inner exceptions
#     assert RaisesGroup(ValueError, TypeError).matches(excinfo.value.__cause__)
#
#     # Example 3: Using flatten_subgroups (conceptual)
#     # assert RaisesGroup(ValueError, TypeError, flatten_subgroups=True).matches(excinfo.value.__cause__)

```