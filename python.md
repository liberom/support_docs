### Example: Per-User Python Installation with Simplified UI

Source: https://docs.python.org/3/using/windows

This example shows how to create a shortcut for a per-user Python installation that uses a simplified UI, disallowing customization. This is useful for end-users who need a quick personal installation.

```batch
installer.exe /simple InstallAllUsers=0 Include_launcher=0 Include_test=0
```

--------------------------------

### Python 3 Installation Options

Source: https://docs.python.org/3/using/windows

Details the choices during Python 3 installation on Windows, differentiating between 'Install Now' and 'Customize installation' for user-specific or all-users setups, including PATH modifications and shortcut availability.

```text
If you select “Install Now”:
  * You will _not_ need to be an administrator (unless a system update for the C Runtime Library is required or you install the [Python Launcher for Windows](https://docs.python.org/3/using/windows.html#launcher) for all users)
  * Python will be installed into your user directory
  * The [Python Launcher for Windows](https://docs.python.org/3/using/windows.html#launcher) will be installed according to the option at the bottom of the first page
  * The standard library, test suite, launcher and pip will be installed
  * If selected, the install directory will be added to your `PATH`
  * Shortcuts will only be visible for the current user

Selecting “Customize installation” will allow you to select the features to install, the installation location and other options or post-install actions. To install debugging symbols or binaries, you will need to use this option.
To perform an all-users installation, you should select “Customize installation”. In this case:
  * You may be required to provide administrative credentials or approval
  * Python will be installed into the Program Files directory
  * The [Python Launcher for Windows](https://docs.python.org/3/using/windows.html#launcher) will be installed into the Windows directory
  * Optional features may be selected during installation
  * The standard library can be pre-compiled to bytecode
  * If selected, the install directory will be added to the system `PATH`
  * Shortcuts are available for all users
```

--------------------------------

### Python unittest.TestCase setUp Example

Source: https://docs.python.org/3/library/unittest

Demonstrates the usage of the setUp() method in Python's unittest.TestCase for preparing test fixtures before each test method execution.

```python
import unittest

class MyTestCase(unittest.TestCase):
    def setUp(self):
        # Prepare test fixture here
        self.data = [1, 2, 3]
        print("Setting up test...")

    def test_example(self):
        # Test logic using self.data
        self.assertEqual(self.data, [1, 2, 3])
        print("Running test...")

    def tearDown(self):
        # Clean up test fixture here
        print("Tearing down test...")
        self.data = None

if __name__ == '__main__':
    unittest.main()
```

--------------------------------

### Extending Python with C/C++: Simple Example

Source: https://docs.python.org/3/contents

Demonstrates a basic example of extending Python with C/C++. This section covers the initial setup and a minimal working extension.

```c
#include <Python.h>

// A simple function to be exposed to Python
static PyObject* my_module_say_hello(PyObject* self, PyObject* args) {
    printf("Hello from C extension!\n");
    Py_RETURN_NONE;
}

// Method definition table
static PyMethodDef MyModuleMethods[] = {
    {"say_hello", my_module_say_hello, METH_NOARGS, "A simple hello function."},
    {NULL, NULL, 0, NULL}        /* Sentinel */
};

// Module definition structure
static struct PyModuleDef mymodule = {
    PyModuleDef_HEAD_INIT,
    "mymodule",   /* name of module */
    "A simple example module.", /* module documentation, may be NULL */
    -1,       /* size of per-interpreter state of the module, or -1 if the module keeps state in the global variables.
                 For a module that does not support per-interpreter state, this should be -1.
                 For a module that does support per-interpreter state, this should be the size of the module’s state structure.
                 The module’s state structure is pointed to by the PyModuleDef.m_slots field.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state structure should be initialized by the module’s initialization function.
                 The module’s initialization function should be called by the interpreter’s initialization function.
                 The module’s initialization function should return a pointer to the module’s state structure.
                 The module’s state
```

--------------------------------

### Python Logging Configuration Server Example

Source: https://docs.python.org/3/howto/logging-cookbook

Illustrates the basic setup for using Python's logging configuration server, which involves reading initial configuration from a file.

```python
importlogging
importlogging.config
importtime
importos

# read initial config file
logging.config.fileConfig('logging.conf')
```

--------------------------------

### Example: Silent System-Wide Python Installation

Source: https://docs.python.org/3/using/windows

This example demonstrates how to perform a silent, system-wide installation of Python using command-line arguments. It's suitable for automated deployments on multiple machines.

```batch
installer.exe /quiet InstallAllUsers=1 PrependPath=1 Include_test=0
```

--------------------------------

### Python Module Installation Guide

Source: https://docs.python.org/3/installing/index

This section provides an overview of installing Python modules, highlighting the benefits of community contributions and the importance of adhering to organizational policies on open-source software. It directs users to further resources for creating and sharing their own projects.

```python
As a popular open source development project, Python has an active supporting community of contributors and users that also make their software available for other Python developers to use under open source license terms.
This allows Python users to share and collaborate effectively, benefiting from the solutions others have already created to common (and sometimes even rare!) problems, as well as potentially contributing their own solutions to the common pool.
This guide covers the installation part of the process. For a guide to creating and sharing your own Python projects, refer to the [Python packaging user guide](https://packaging.python.org/en/latest/tutorials/packaging-projects/).
Note
For corporate and other institutional users, be aware that many organisations have their own policies around using and contributing to open source software. Please take such policies into account when making use of the distribution and installation tools provided with Python.
```

--------------------------------

### Installing Python Modules: Key Terms and Basic Usage

Source: https://docs.python.org/3/contents

This snippet covers essential terminology and fundamental steps for installing Python modules. It's a starting point for users new to Python package management.

```APIDOC
Installing Python Modules:
  Key terms: Defines important vocabulary related to Python package installation.
  Basic usage: Outlines the fundamental commands and procedures for installing packages.
```

--------------------------------

### Python 3.5.10 Documentation Overview

Source: https://docs.python.org/3/.5

This snippet outlines the main sections and resources available in the Python 3.5.10 documentation. It highlights key areas such as 'What's new', 'Tutorial', 'Library Reference', 'Language Reference', and 'Python Setup and Usage'. It also points to installation guides, distribution information, and resources for C/C++ programmers extending Python.

```python
print('Welcome to Python 3.5.10 documentation!')

# Key sections:
# - What's new in Python 3.5?
# - Tutorial
# - Library Reference
# - Language Reference
# - Python Setup and Usage
# - Python HOWTOs
# - Installing Python Modules
# - Distributing Python Modules
# - Extending and Embedding
# - Python/C API
# - FAQs

# Indices and tables:
# - Global Module Index
# - General Index
# - Glossary
# - Search page
# - Complete Table of Contents

# Meta information:
# - Reporting bugs
# - About the documentation
# - History and License of Python
# - Copyright

# Download options:
# - Download these documents

# Version-specific links:
# - Stable (Python 3)
# - In development
# - All versions

# Other resources:
# - PEP Index
# - Beginner's Guide
# - Book List
# - Audio/Visual Talks
# - Python Developer’s Guide
```

--------------------------------

### Python Launcher for Windows - Getting Started

Source: https://docs.python.org/3/using/windows

This section covers the initial steps for using the Python Launcher on Windows, including command-line usage, virtual environments, script execution, and file associations.

```python
# Example of using the Python Launcher from the command-line
# py -3.10 script.py
# py -m venv myenv
# py --list
```

```python
# Example of a shebang line for the Python Launcher
# !/usr/bin/env python3
```

--------------------------------

### Installing Python Modules: How To Install Pip

Source: https://docs.python.org/3/contents

Guidance on installing the `pip` package installer for Python versions prior to 3.4. This addresses a common setup requirement for older Python environments.

```APIDOC
How to install `pip`:
  Instructions for installing pip in Python versions before 3.4.
  Essential for managing packages in older Python installations.
```

--------------------------------

### Cross-Compilation Configuration Example

Source: https://docs.python.org/3/using/configure

An example of setting the CONFIG_SITE environment variable for cross-compilation, specifying the host and target platforms and the Python installation path.

```shell
CONFIG_SITE=config.site-aarch64\
=x86_64-pc-linux-gnu\
=aarch64-unknown-linux-gnu\
=../x86_64/python
```

--------------------------------

### Python Documentation Navigation and Resources

Source: https://docs.python.org/3/howto/webservers

Provides links to various sections of the Python documentation, including version-specific documentation, tutorials, library and language references, installation guides, and community resources like PEPs and developer guides.

```python
https://docs.python.org/3/download.html
https://docs.python.org/3/whatsnew/3.13.html
https://docs.python.org/3/tutorial/index.html
https://docs.python.org/3/library/index.html
https://docs.python.org/3/reference/index.html
https://docs.python.org/3/using/index.html
https://docs.python.org/3/howto/index.html
https://docs.python.org/3/installing/index.html
https://docs.python.org/3/distributing/index.html
https://docs.python.org/3/extending/index.html
https://docs.python.org/3/c-api/index.html
https://docs.python.org/3/faq/index.html
https://docs.python.org/3/deprecations/index.html
https://docs.python.org/3/py-modindex.html
https://docs.python.org/3/genindex.html
https://docs.python.org/3/glossary.html
https://docs.python.org/3/search.html
https://docs.python.org/3/contents.html
https://peps.python.org/
https://wiki.python.org/moin/BeginnersGuide
https://wiki.python.org/moin/PythonBooks
https://www.python.org/doc/av/
https://devguide.python.org/
https://docs.python.org/3/bugs.html
https://devguide.python.org/documentation/help-documenting/
https://docs.python.org/3/license.html
https://docs.python.org/3/copyright.html
https://docs.python.org/3/about.html
```

--------------------------------

### Python 3.9.23 Documentation Overview

Source: https://docs.python.org/3/.9

Provides links to various sections of the Python 3.9.23 documentation, including what's new, tutorials, library and language references, setup guides, HOWTOs, installation, distribution, extending/embedding, Python/C API, and FAQs.

```python
print('Welcome to the Python 3.9.23 documentation!')

# Key documentation sections:
# - What's new in Python 3.9?
# - Tutorial
# - Library Reference
# - Language Reference
# - Python Setup and Usage
# - Python HOWTOs
# - Installing Python Modules
# - Distributing Python Modules
# - Extending and Embedding
# - Python/C API
# - FAQs

# Navigation and indices:
# - Global Module Index
# - General Index
# - Glossary
# - Search page
# - Complete Table of Contents

# Meta information:
# - Reporting bugs
# - Contributing to Docs
# - About the documentation
# - History and License of Python
# - Copyright
```

--------------------------------

### Installing Packages

Source: https://docs.python.org/3/library/venv

After activating a virtual environment, you can use `pip` to install packages. This example shows how to install a package named 'requests'. Packages installed this way are isolated to the current virtual environment.

```bash
pip install requests
```

--------------------------------

### Get All Supported Start Methods

Source: https://docs.python.org/3/library/multiprocessing

Returns a list of all supported methods for starting new processes ('fork', 'spawn', 'forkserver'), with the default method listed first. Not all methods are available on all platforms. Added in version 3.4.

```python
import multiprocessing

supported_methods = multiprocessing.get_all_start_methods()
```

--------------------------------

### Python re.Match.start() and re.Match.end() Examples

Source: https://docs.python.org/3/library/re

Shows how to use the start() and end() methods to get the start and end indices of substrings matched by groups within a re.Match object. Includes handling of groups that did not contribute to the match and matched null strings.

```python
>>> import re
>>> email = "tony@tiremove_thisger.net"
>>> m = re.search("remove_this", email)
>>> email[:m.start()] + email[m.end():]
'tony@tiger.net'
```

--------------------------------

### Install Free-threaded Python Binaries (Command Line)

Source: https://docs.python.org/3/using/windows

This command-line option installs the experimental free-threaded Python binaries. It requires selecting 'Customize installation' during the GUI setup or using this flag for command-line installations. The free-threaded binaries are registered with a 't' suffix.

```cmd
Include_freethreaded=1
```

--------------------------------

### Main Process Setup and Multiprocessing Logging

Source: https://docs.python.org/3/howto/logging-cookbook

Initializes logging in the main process, creates worker processes with their configurations, and starts a listener process to handle logs from the workers. It manages the lifecycle of these processes.

```python
import logging
import logging.config
from multiprocessing import Process, Queue, Event

def worker_process(config):
    logging.config.dictConfig(config)
    logger = logging.getLogger('worker')
    logger.info('Worker started')

def listener_process(queue, stop_event, config):
    logging.config.dictConfig(config)
    logger = logging.getLogger('listener')
    logger.info('Listener started')
    while not stop_event.is_set():
        try:
            record = queue.get()
            if record is None:  # Sentinel value to stop
                break
            logger.handle(record)
        except Exception as e:
            logger.error('Error handling log record: %s', e)
    logger.info('Listener stopped')

def main():
    q = Queue(-1)
    # The initial configuration for the parent process.
    config_initial = {
        'version': 1,
        'disable_existing_loggers': False,
        'formatters': {
            'simple': {
                'format': '%(levelname)s:%(name)s:%(message)s'
            }
        },
        'handlers': {
            'console': {
                'class': 'logging.StreamHandler',
                'formatter': 'simple'
            }
        },
        'root': {
            'handlers': ['console'],
            'level': 'DEBUG'
        }
    }
    # The worker process configuration is just a QueueHandler attached to the
    # root logger, which allows all messages to be sent to the queue.
    # We disable existing loggers to disable the "setup" logger used in the
    # parent process. This is needed on POSIX because the logger will
    # be there in the child following a fork().
    config_worker = {
        'version': 1,
        'disable_existing_loggers': True,
        'handlers': {
            'queue': {
                'class': 'logging.handlers.QueueHandler',
                'queue': q
            }
        },
        'root': {
            'handlers': ['queue'],
            'level': 'DEBUG'
        }
    }
    # The listener process configuration shows that the full flexibility of
    # logging configuration is available to dispatch events to handlers however
    # you want.
    # We disable existing loggers to disable the "setup" logger used in the
    # parent process. This is needed on POSIX because the logger will
    # be there in the child following a fork().
    config_listener = {
        'version': 1,
        'disable_existing_loggers': True,
        'formatters': {
            'detailed': {
                'class': 'logging.Formatter',
                'format': '%(asctime)s%(name)-15s%(levelname)-8s%(processName)-10s%(message)s'
            },
            'simple': {
                'class': 'logging.Formatter',
                'format': '%(name)-15s%(levelname)-8s%(processName)-10s%(message)s'
            }
        },
        'handlers': {
            'console': {
                'class': 'logging.StreamHandler',
                'formatter': 'simple',
                'level': 'INFO'
            },
            'file': {
                'class': 'logging.FileHandler',
                'filename': 'mplog.log',
                'mode': 'w',
                'formatter': 'detailed'
            },
            'foofile': {
                'class': 'logging.FileHandler',
                'filename': 'mplog-foo.log',
                'mode': 'w',
                'formatter': 'detailed'
            },
            'errors': {
                'class': 'logging.FileHandler',
                'filename': 'mplog-errors.log',
                'mode': 'w',
                'formatter': 'detailed',
                'level': 'ERROR'
            }
        },
        'loggers': {
            'foo': {
                'handlers': ['foofile']
            }
        },
        'root': {
            'handlers': ['console', 'file', 'errors'],
            'level': 'DEBUG'
        }
    }
    # Log some initial events, just to show that logging in the parent works
    # normally.
    logging.config.dictConfig(config_initial)
    logger = logging.getLogger('setup')
    logger.info('About to create workers ...')
    workers = []
    for i in range(5):
        wp = Process(target=worker_process, name='worker %d' % (i + 1),
                     args=(config_worker,)) # Pass config_worker here
        workers.append(wp)
        wp.start()
        logger.info('Started worker: %s', wp.name)
    logger.info('About to create listener ...')
    stop_event = Event()
    lp = Process(target=listener_process, name='listener',
                 args=(q, stop_event, config_listener)) # Pass config_listener here
    lp.start()
    logger.info('Started listener')
    # We now hang around for the workers to finish their work.
    for wp in workers:
        wp.join()
    # Workers all done, listening can now stop.
    # Logging in the parent still works normally.
    logger.info('Telling listener to stop ...')
    stop_event.set()
    lp.join()
    logger.info('All done.')

if __name__ == '__main__':
    main()

```

--------------------------------

### Python Extension Setup (setup.py)

Source: https://docs.python.org/3/extending/newtypes_tutorial

A Python script that uses setuptools to build and install a custom C extension module. It defines the extension module 'custom' and links it to the 'custom.c' source file.

```python
from setuptools import Extension, setup

setup(ext_modules=[
    Extension("custom", ["custom.c"])
])

```

--------------------------------

### Python 3.11.13 Documentation Sections

Source: https://docs.python.org/3/.11

Provides links to various sections of the Python 3.11.13 documentation, including 'What's new', tutorials, library and language references, setup and usage guides, HOWTOs, module installation and distribution, extending and embedding Python, and FAQs.

```python
https://docs.python.org/3.11/whatsnew/3.11.html
https://docs.python.org/3.11/tutorial/index.html
https://docs.python.org/3.11/library/index.html
https://docs.python.org/3.11/reference/index.html
https://docs.python.org/3.11/using/index.html
https://docs.python.org/3.11/howto/index.html
https://docs.python.org/3.11/installing/index.html
https://docs.python.org/3.11/distributing/index.html
https://docs.python.org/3.11/extending/index.html
https://docs.python.org/3.11/c-api/index.html
https://docs.python.org/3.11/faq/index.html
```

--------------------------------

### Test Case with setUp and tearDown

Source: https://docs.python.org/3/library/unittest

Illustrates how to use `setUp()` for pre-test setup and `tearDown()` for post-test cleanup within a `unittest.TestCase`. The `setUp` method initializes a widget instance, and `tearDown` disposes of it.

```python
import unittest

class WidgetTestCase(unittest.TestCase):
    def setUp(self):
        self.widget = Widget('The widget')

    def test_default_widget_size(self):
        self.assertEqual(self.widget.size(), (50,50),
                         'incorrect default size')

    def test_widget_resize(self):
        self.widget.resize(100,150)
        self.assertEqual(self.widget.size(), (100,150),
                         'wrong size after resize')

    def tearDown(self):
        self.widget.dispose()
```

--------------------------------

### Python asyncio Queue Usage Example

Source: https://docs.python.org/3/library/asyncio-queue

Demonstrates basic usage of asyncio.Queue, including putting and getting items, and checking queue status.

```python
import asyncio

async def main():
    queue = asyncio.Queue(maxsize=2)

    await queue.put(1)
    await queue.put(2)

    print(f"Queue size: {queue.qsize()}")
    print(f"Is queue full? {queue.full()}")

    item1 = await queue.get()
    item2 = await queue.get()

    print(f"Retrieved item: {item1}")
    print(f"Retrieved item: {item2}")
    print(f"Is queue empty? {queue.empty()}")

asyncio.run(main())
```

--------------------------------

### Multiprocessing Pool Example Setup

Source: https://docs.python.org/3/library/multiprocessing

Sets up helper functions for multiprocessing pool tests. Includes functions for calculating results, performing multiplication, addition, and other mathematical operations with simulated delays.

```python
importmultiprocessing
importtime
importrandom
importsys

#
# Functions used by test code
#

defcalculate(func, args):
    result = func(*args)
    return '%s says that %s%s = %s' % (
        multiprocessing.current_process().name,
        func.__name__,
        args,
        result
        )

defcalculatestar(args):
    return calculate(*args)

defmul(a, b):
    time.sleep(0.5 * random.random())
    return a * b

defplus(a, b):
    time.sleep(0.5 * random.random())
    return a + b

defpow3(x):
    return x ** 3

defnoop(x):
    pass
```

--------------------------------

### Example config.site file

Source: https://docs.python.org/3/using/configure

An example of a config.site file used for configure overrides.

```shell
# Example config.site file:
# Uncomment and modify lines below to override default configure settings.
# CFLAGS="-O2 -march=native"
# LDFLAGS="-L/usr/local/lib"
# --enable-shared
# --prefix=/opt/python3
```

--------------------------------

### Manual Extension Building Example (winsound.vcxproj)

Source: https://docs.python.org/3/extending/windows

This snippet refers to the project file for the 'winsound' standard library module, which serves as an example for manually building extension modules on Windows. It is useful for understanding the underlying build process when setuptools is not sufficient.

```c++
<Project DefaultTargets="Build" ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <ItemGroup Label="ProjectConfigurations">
    <ProjectConfiguration Include="Debug|x64">
      <Configuration>Debug</Configuration>
      <Platform>x64</Platform>
    </ProjectConfiguration>
    <ProjectConfiguration Include="Release|x64">
      <Configuration>Release</Configuration>
      <Platform>x64</Platform>
    </ProjectConfiguration>
  </ItemGroup>
  <ItemGroup>
    <ClCompile Include="winsound.c" />
  </ItemGroup>
  <PropertyGroup Label="Globals">
    <ProjectGuid>{...}</ProjectGuid>
    <Keyword>Win32Proj</Keyword>
    <RootNamespace>winsound</RootNamespace>
  </PropertyGroup>
  <Import Project="$(VCTargetsPath)\Microsoft.Cpp.$(Platform).user.props" Condition="exists('$(VCTargetsPath)\Microsoft.Cpp.$(Platform).user.props')" />
  <PropertyGroup Label="UserMacros" />
  <PropertyGroup />
  <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Debug|x64'">
    <ClCompile>
      <PrecompiledHeader>
      </PrecompiledHeader>
      <WarningLevel>Level3</WarningLevel>
      <Optimization>Disabled</Optimization>
      <PreprocessorDefinitions>_WINDOWS;_USRDLL;WINSOUND_EXPORTS;%(PreprocessorDefinitions)</PreprocessorDefinitions>
      <AdditionalIncludeDirectories>$(ProjectDir)\..\..\Include;%(AdditionalIncludeDirectories)</AdditionalIncludeDirectories>
    </ClCompile>
    <Link>
      <SubSystem>Windows</SubSystem>
      <AdditionalLibraryDirectories>$(ProjectDir)\..\..\libs;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>
    </Link>
  </ItemDefinitionGroup>
  <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Release|x64'">
    <ClCompile>
      <PrecompiledHeader>
      </PrecompiledHeader>
      <WarningLevel>Level3</WarningLevel>
      <Optimization>MaxSpeed</Optimization>
      <PreprocessorDefinitions>_WINDOWS;_USRDLL;WINSOUND_EXPORTS;%(PreprocessorDefinitions)</PreprocessorDefinitions>
      <AdditionalIncludeDirectories>$(ProjectDir)\..\..\Include;%(AdditionalIncludeDirectories)</AdditionalIncludeDirectories>
    </ClCompile>
    <Link>
      <SubSystem>Windows</SubSystem>
      <AdditionalLibraryDirectories>$(ProjectDir)\..\..\libs;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>
    </Link>
  </ItemDefinitionGroup>
  <Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
  <ImportGroup Label="ExtensionSettings">
  </ImportGroup>
  <ImportGroup Label="Shared">
  </ImportGroup>
  <Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
  <ImportGroup Label="ExtensionTargets">
  </ImportGroup>
</Project>
```

--------------------------------

### Python Installation and Configuration Methods

Source: https://docs.python.org/3/genindex-I

This section documents methods related to installing and configuring various components within the Python ecosystem, such as handlers, openers, and scripts.

```python
gettext.NullTranslations.install()
gettext.install(domain='', names=None)
urllib.request.install_opener(opener)
virtualenv.EnvBuilder.install_scripts(context)
unittest.installHandler()
```

--------------------------------

### Python Installer Command-Line Options

Source: https://docs.python.org/3/using/windows

This section details the command-line arguments available for the Python installer, allowing for scripted and non-interactive installations. These options control various aspects of the installation process, from UI behavior to feature selection.

```APIDOC
Installer Command-Line Options:

/passive: Displays progress without requiring user interaction.
/quiet: Installs or uninstalls without displaying any UI.
/simple: Prevents user customization during installation.
/uninstall: Removes Python without confirmation.
/layout [directory]: Pre-downloads all necessary components to a specified directory.
/log [filename]: Specifies the location for log files.

Other options are passed as name=value pairs, where value is typically 0 for disable, 1 for enable, or a path.

Available Options:

InstallAllUsers: Perform a system-wide installation. (Default: 0)
TargetDir: The installation directory. (Default: Varies based on InstallAllUsers)
DefaultAllUsersTargetDir: Default directory for all-user installs. (Default: %ProgramFiles%\Python X.Y or %ProgramFiles(x86)%\Python X.Y)
DefaultJustForMeTargetDir: Default directory for just-for-me installs. (Default: %LocalAppData%\Programs\Python\PythonXY or similar)
DefaultCustomTargetDir: Default custom install directory shown in UI. (Default: empty)
AssociateFiles: Create file associations if the launcher is installed. (Default: 1)
CompileAll: Compile all .py files to .pyc. (Default: 0)
PrependPath: Prepend install and Scripts directories to PATH and add .PY to PATHEXT. (Default: 0)
AppendPath: Append install and Scripts directories to PATH and add .PY to PATHEXT. (Default: 0)
Shortcuts: Create shortcuts for interpreter, documentation, and IDLE. (Default: 1)
Include_doc: Install Python manual. (Default: 1)
Include_debug: Install debug binaries. (Default: 0)
Include_dev: Install developer headers and libraries. (Default: 1)
Include_exe: Install python.exe and related files. (Default: 1)
Include_launcher: Install Python Launcher for Windows. (Default: 1)
InstallLauncherAllUsers: Installs the launcher for all users. Requires Include_launcher=1. (Default: 1)
Include_lib: Install standard library and extension modules. (Default: 1)
Include_pip: Install bundled pip and setuptools. (Default: 1)
Include_symbols: Install debugging symbols (*.pdb). (Default: 0)
Include_tcltk: Install Tcl/Tk support and IDLE. (Default: 1)
Include_test: Install standard library test suite. (Default: 1)
Include_tools: Install utility scripts. (Default: 1)
LauncherOnly: Only installs the launcher, overriding most other options. (Default: 0)
SimpleInstall: Disable most install UI. (Default: 0)
SimpleInstallDescription: Custom message for simplified install UI. (Default: empty)
```

--------------------------------

### OptionParser Setup with Options

Source: https://docs.python.org/3/library/optparse

Demonstrates how to initialize an OptionParser with a custom usage string and add various options with different actions, destinations, defaults, and help messages.

```python
usage = "usage: %prog [options] arg1 arg2"
parser = OptionParser(usage=usage)
parser.add_option("-v", "--verbose",
                  action="store_true", dest="verbose", default=True,
                  help="make lots of noise [default]")
parser.add_option("-q", "--quiet",
                  action="store_false", dest="verbose",
                  help="be vewwy quiet (I'm hunting wabbits)")
parser.add_option("-f", "--filename",
                  metavar="FILE", help="write output to FILE")
parser.add_option("-m", "--mode",
                  default="intermediate",
                  help="interaction mode: novice, intermediate, "
                       "or expert [default: %default]")
```

--------------------------------

### Import and Initialize OptionParser

Source: https://docs.python.org/3/library/optparse

Demonstrates the basic setup for using the optparse library by importing the OptionParser class and creating an instance.

```python
from optparse import OptionParser

parser = OptionParser()
```

--------------------------------

### Python Documentation Navigation and Resources

Source: https://docs.python.org/3/library/fpectl

Provides links to various sections of the Python documentation, including version-specific documentation, tutorials, library and language references, installation guides, and community resources like PEPs and developer guides.

```python
https://docs.python.org/3/download.html
https://docs.python.org/3/whatsnew/3.13.html
https://docs.python.org/3/tutorial/index.html
https://docs.python.org/3/library/index.html
https://docs.python.org/3/reference/index.html
https://docs.python.org/3/using/index.html
https://docs.python.org/3/howto/index.html
https://docs.python.org/3/installing/index.html
https://docs.python.org/3/distributing/index.html
https://docs.python.org/3/extending/index.html
https://docs.python.org/3/c-api/index.html
https://docs.python.org/3/faq/index.html
https://docs.python.org/3/deprecations/index.html
https://docs.python.org/3/py-modindex.html
https://docs.python.org/3/genindex.html
https://docs.python.org/3/glossary.html
https://docs.python.org/3/search.html
https://docs.python.org/3/contents.html
https://peps.python.org/
https://wiki.python.org/moin/BeginnersGuide
https://wiki.python.org/moin/PythonBooks
https://www.python.org/doc/av/
https://devguide.python.org/
https://docs.python.org/3/bugs.html
https://devguide.python.org/documentation/help-documenting/
https://docs.python.org/3/license.html
https://docs.python.org/3/copyright.html
https://docs.python.org/3/about.html
```

--------------------------------

### Main Application Entry Point

Source: https://docs.python.org/3/howto/logging-cookbook

The `main` function sets up the Qt application, initializes the logging level, creates an instance of the `Window` class, shows the window, and starts the Qt event loop. It ensures proper handling of application execution and exit.

```python
def main():
    QtCore.QThread.currentThread().setObjectName('MainThread')
    logging.getLogger().setLevel(logging.DEBUG)
    app = QtWidgets.QApplication(sys.argv)
    example = Window(app)
    example.show()
    if hasattr(app, 'exec'):
        rc = app.exec()
    else:
        rc = app.exec_()
    sys.exit(rc)
```

--------------------------------

### Install Binary Extensions

Source: https://docs.python.org/3/installing/index

Discusses the shift from source-based distributions to binary `wheel` format for easier installation of extensions, especially on Windows and macOS. Mentions that solutions for scientific software may also help with other binary extensions.

```text
With the introduction of support for the binary `wheel` format, and the ability to publish wheels for at least Windows and macOS through the Python Package Index, this problem is expected to diminish over time, as users are more regularly able to install pre-built extensions rather than needing to build them themselves.
```

--------------------------------

### Python Opcode Instructions

Source: https://docs.python.org/3/genindex-S

Documentation for opcode instructions related to setup, including SETUP_ANNOTATIONS, SETUP_CLEANUP, and SETUP_FINALLY, used in bytecode execution for exception handling and annotation setup.

```APIDOC
SETUP_ANNOTATIONS
  - Sets up annotation environment.

SETUP_CLEANUP
  - Sets up a finally block.

SETUP_FINALLY
  - Sets up a finally block.
```

--------------------------------

### curses.setupterm

Source: https://docs.python.org/3/genindex-S

Initializes the curses screen.

```APIDOC
curses.setupterm(term=None, file=None)
  Initializes the curses screen and determines terminal type.
```

--------------------------------

### Sequence Start Attribute

Source: https://docs.python.org/3/genindex-S

Represents the starting value of a sequence or slice. For example, in a `range` object or a `slice` object, `start` indicates the beginning of the sequence.

```python
# For range objects
r = range(2, 10, 2)
print(f"Range start: {r.start}") # Output: 2

# For slice objects
s = slice(1, 5, 2)
print(f"Slice start: {s.start}") # Output: 1
```

--------------------------------

### Validator Class Example

Source: https://docs.python.org/3/howto/descriptor

Presents a practical example of a descriptor used as a validator for class attributes, ensuring data integrity.

```python
class Validator:
    def __init__(self, type_check):
        self.type_check = type_check
        self.name = ''

    def __set_name__(self, owner, name):
        self.name = name

    def __get__(self, instance, owner):
        if instance is None:
            return self
        return instance.__dict__.get(self.name)

    def __set__(self, instance, value):
        if not isinstance(value, self.type_check):
            raise TypeError(f"Expected {self.type_check.__name__}, got {type(value).__name__}")
        instance.__dict__[self.name] = value

class Stock:
    price = Validator(float)

# Usage:
stock = Stock()
try:
    stock.price = 10.5
    print(stock.price)
    stock.price = 'high'
except TypeError as e:
    print(e)
```

--------------------------------

### socketserver.UDPServer Example

Source: https://docs.python.org/3/library/socketserver

Illustrates how to use socketserver.UDPServer to create UDP-based network servers. This example shows the setup for handling UDP datagrams.

```python
import socketserver

class MyUDPHandler(socketserver.BaseRequestHandler):
    """
    This class will be used to handle incoming UDP requests
    """

    def handle(self):
        data = self.request[0].strip()
        socket = self.request[1]
        print(f"Received {data} from {self.client_address}")
        socket.sendto(data.upper(), self.client_address)

if __name__ == "__main__":
    HOST, PORT = "localhost", 9999
    # Create the server, binding to localhost on port 9999
    with socketserver.UDPServer((HOST, PORT), MyUDPHandler) as server:
        server.serve_forever()
```

--------------------------------

### Optparse Example

Source: https://docs.python.org/3/library/optparse

Demonstrates basic command-line argument parsing using Python's `optparse` library. It sets up options for output file and verbosity, then parses arguments.

```python
import optparse

if __name__ == '__main__':
    parser = optparse.OptionParser()
    parser.add_option('-o', '--output')
    parser.add_option('-v', dest='verbose', action='store_true')
    opts, args = parser.parse_args()
    process(args, output=opts.output, verbose=opts.verbose)
```

--------------------------------

### Python POP3 Connection Example

Source: https://docs.python.org/3/library/poplib

A basic example demonstrating how to establish a connection to a POP3 server and retrieve the welcome message using Python's poplib library.

```python
import poplib

# Replace with your POP3 server details
server = "your_pop3_server.com"
port = 110

try:
    # Connect to the POP3 server
    with poplib.POP3(server, port) as server_conn:
        # Get the welcome message
        welcome_message = server_conn.getwelcome()
        print(f"Welcome message: {welcome_message.decode('ascii')}")

        # Further operations like login, stat, list, retr, etc. can be performed here

except poplib.error_proto as e:
    print(f"POP3 protocol error: {e}")
except Exception as e:
    print(f"An error occurred: {e}")

```

--------------------------------

### Python Windows Installer Options

Source: https://docs.python.org/3/using/windows

This section outlines the different installer options available for Python on Windows, each suited for specific use cases. It covers the full installer for developers, the Microsoft Store package for general use, nuget.org packages for CI systems, and the embeddable package for application embedding.

```python
Full installer: Contains all components, best for developers.
Microsoft Store package: Simple installation for scripts and IDEs, requires Windows 10+, safe for other programs.
Nuget.org packages: Lightweight installations for CI systems, not updateable, no UI tools.
Embeddable package: Minimal package for embedding into larger applications.
```

--------------------------------

### Python Documentation Navigation and Resources

Source: https://docs.python.org/3/library/2to3

Provides links to various sections of the Python documentation, including version-specific documentation, tutorials, library and language references, installation guides, and community resources like PEPs and developer guides.

```python
https://docs.python.org/3/download.html
https://docs.python.org/3/whatsnew/3.13.html
https://docs.python.org/3/tutorial/index.html
https://docs.python.org/3/library/index.html
https://docs.python.org/3/reference/index.html
https://docs.python.org/3/using/index.html
https://docs.python.org/3/howto/index.html
https://docs.python.org/3/installing/index.html
https://docs.python.org/3/distributing/index.html
https://docs.python.org/3/extending/index.html
https://docs.python.org/3/c-api/index.html
https://docs.python.org/3/faq/index.html
https://docs.python.org/3/deprecations/index.html
https://docs.python.org/3/py-modindex.html
https://docs.python.org/3/genindex.html
https://docs.python.org/3/glossary.html
https://docs.python.org/3/search.html
https://docs.python.org/3/contents.html
https://peps.python.org/
https://wiki.python.org/moin/BeginnersGuide
https://wiki.python.org/moin/PythonBooks
https://www.python.org/doc/av/
https://devguide.python.org/
https://docs.python.org/3/bugs.html
https://devguide.python.org/documentation/help-documenting/
https://docs.python.org/3/license.html
https://docs.python.org/3/copyright.html
https://docs.python.org/3/about.html
```

--------------------------------

### Asyncio Server Start Serving

Source: https://docs.python.org/3/genindex-S

Starts accepting connections for a server. This method is called on an `asyncio.Server` object to begin listening for incoming client requests.

```python
import asyncio

async def handle_connection(reader, writer):
    pass # Handle connection logic

async def run_server():
    server = await asyncio.start_server(handle_connection, 'localhost', 12345)
    await server.start_serving() # Explicitly start serving
    print("Server started serving")
    # Keep the server running
    await asyncio.Future()

if __name__ == "__main__":
    asyncio.run(run_server())
```

--------------------------------

### Catching Exceptions from __enter__ Methods

Source: https://docs.python.org/3/library/contextlib

This example illustrates how to catch exceptions that might occur during the __enter__ method of a context manager, providing a mechanism to handle setup failures gracefully without disrupting the program flow.

```python
from contextlib import suppress

class FailingContext:
    def __enter__(self):
        raise ValueError("Error during enter")
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Exiting, even with error.")
        return False

with suppress(ValueError):
    with FailingContext():
        print("Inside failing context.")
# The ValueError is suppressed, and the program continues.

```

--------------------------------

### Python unittest.TestCase setUpClass Example

Source: https://docs.python.org/3/library/unittest

Shows how to use the setUpClass() class method in Python's unittest.TestCase for setting up resources once before all tests in a class.

```python
import unittest

class DatabaseTestCase(unittest.TestCase):
    @classmethod
    def setUpClass(cls):
        # Set up database connection or shared resource
        cls.db_connection = "MockDatabaseConnection"
        print("\nSetting up class fixture...")

    def test_db_connection_available(self):
        self.assertIsNotNone(self.db_connection)
        print("Testing DB connection...")

    def test_data_retrieval(self):
        # Use cls.db_connection for tests
        self.assertEqual(self.db_connection, "MockDatabaseConnection")
        print("Testing data retrieval...")

    @classmethod
    def tearDownClass(cls):
        # Clean up database connection or shared resource
        cls.db_connection = None
        print("Tearing down class fixture...")

if __name__ == '__main__':
    unittest.main()
```

--------------------------------

### Database Connection and Usage Example

Source: https://docs.python.org/3/howto/descriptor

Demonstrates connecting to an SQLite database and interacting with the ORM models to retrieve and update data. Shows how descriptor attributes are accessed and modified.

```python
>>> import sqlite3
>>> conn = sqlite3.connect('entertainment.db')

>>> Movie('Star Wars').director
'George Lucas'
>>> jaws = Movie('Jaws')
>>> f'Released in {jaws.year} by {jaws.director}'
'Released in 1975 by Steven Spielberg'

>>> Song('Country Roads').artist
'John Denver'

>>> Movie('Star Wars').director = 'J.J. Abrams'
>>> Movie('Star Wars').director
'J.J. Abrams'
```

--------------------------------

### Python Tutorial and Beginner Resources

Source: https://docs.python.org/3/faq/general

Points to resources for new Python programmers, including the official Python Tutorial and community-curated beginner guides.

```text
Official Python Tutorial: https://docs.python.org/3/tutorial/index.html#tutorial-index
Beginner resources: https://wiki.python.org/moin/BeginnersGuide
```

--------------------------------

### Simple Descriptor Example

Source: https://docs.python.org/3/howto/descriptor

Demonstrates a basic descriptor that returns a constant value. This serves as an introduction to the concept of descriptors in Python.

```python
class SimpleDescriptor:
    def __get__(self, instance, owner):
        return "This is a constant value."

# Usage:
obj = SimpleDescriptor()
print(obj.__get__(None, None))
```

--------------------------------

### Python Modules and Packages

Source: https://docs.python.org/3/tutorial/index

Explains how to execute modules as scripts, the module search path, and the concept of packages. Includes examples of importing from packages and intra-package references.

```python
# Example of executing a module as a script (if __name__ == "__main__":)
# Example of importing from a package
# from my_package import my_module
# Example of intra-package reference
# from . import sibling_module
```

--------------------------------

### Simple Descriptor Example: Constant Value

Source: https://docs.python.org/3/howto/descriptor

Demonstrates a basic descriptor that always returns a constant value when accessed. This is a foundational example for understanding descriptor behavior.

```python
class ConstantDescriptor:
    def __init__(self, value):
        self.value = value

    def __get__(self, instance, owner):
        return self.value

class MyClass:
    constant_attr = ConstantDescriptor(10)
```

--------------------------------

### Descriptor Example: Validator Class

Source: https://docs.python.org/3/howto/descriptor

A practical example of a descriptor used as a validator. This descriptor ensures that assigned values meet certain criteria before being stored.

```python
class Validator:
    def __init__(self, validation_func):
        self.validation_func = validation_func
        self.private_name = '_'

    def __get__(self, instance, owner):
        if instance is None:
            return self
        return getattr(instance, self.private_name)

    def __set__(self, instance, value):
        if not self.validation_func(value):
            raise ValueError(f"Invalid value: {value}")
        setattr(instance, self.private_name, value)
```

--------------------------------

### Building Python Extensions with setuptools

Source: https://docs.python.org/3/extending/index

Provides an example of a setup.py file using setuptools to build C and C++ extensions. This is the standard way to package and distribute Python extensions.

```python
from setuptools import setup, Extension

# Define the extension module
my_extension = Extension('my_module_name', 
                         sources=['src/my_module.c', 'src/another_file.cpp'],
                         include_dirs=['include'],
                         extra_compile_args=['-std=c++11'])

setup(name='MyPythonExtension', 
      version='1.0', 
      description='A sample Python C/C++ extension',
      ext_modules=[my_extension])
```

--------------------------------

### Python 3 Documentation Navigation

Source: https://docs.python.org/3/tutorial/introduction

Provides links to key sections of the Python 3 documentation, such as the general index, module index, and tutorials. It also lists available Python versions and links to specific documentation for each.

```python
Project: /websites/python_3

### Navigation
  * [index](https://docs.python.org/3/genindex.html "General Index")
  * [modules](https://docs.python.org/3/py-modindex.html "Python Module Index") | 
  * [next](https://docs.python.org/3/tutorial/controlflow.html "4. More Control Flow Tools") | 
  * [previous](https://docs.python.org/3/tutorial/interpreter.html "2. Using the Python Interpreter") | 
  * [Python](https://www.python.org/) »
  * Greek | Ελληνικά English Spanish | español French | français Italian | italiano Japanese | 日本語 Korean | 한국어 Polish | polski Brazilian Portuguese | Português brasileiro Turkish | Türkçe Simplified Chinese | 简体中文 Traditional Chinese | 繁體中文
  dev (3.15) pre (3.14) 3.13.7 3.12 3.11 3.10 3.9 3.8 3.7 3.6 3.5 3.4 3.3 3.2 3.1 3.0 2.7 2.6
  * [3.13.7 Documentation](https://docs.python.org/3/index.html) » 
  * [The Python Tutorial](https://docs.python.org/3/tutorial/index.html) »
  * [3. An Informal Introduction to Python](https://docs.python.org/3/tutorial/introduction.html)
  * | 
  * Theme  Auto Light Dark |
```

--------------------------------

### Turtle Graphics Module Introduction

Source: https://docs.python.org/3/contents

Introduces the turtle module for creating graphics, covering its basic usage, tutorials, and how to get started quickly.

```python
import turtle

# Basic turtle graphics usage:
turtle.forward(100)
turtle.left(90)
```

--------------------------------

### Descriptor Usage Example (Python)

Source: https://docs.python.org/3/howto/descriptor

Provides an example of creating and interacting with `Person` objects, demonstrating how the `LoggedAccess` descriptor intercepts attribute assignments and logs the operations. This shows the practical application of descriptors in controlling attribute behavior.

```python
>>> pete = Person('Peter P', 10)
INFO:root:Updating 'name' to 'Peter P'
INFO:root:Updating 'age' to 10
>>> kate = Person('Catherine C', 20)
INFO:root:Updating 'name' to 'Catherine C'
INFO:root:Updating 'age' to 20

```

--------------------------------

### Python Documentation Navigation and Resources

Source: https://docs.python.org/3/index

Provides links to various sections of the Python documentation, including version-specific documentation, tutorials, library and language references, installation guides, and community resources like PEPs and developer guides.

```python
https://docs.python.org/3/download.html
https://docs.python.org/3/whatsnew/3.13.html
https://docs.python.org/3/tutorial/index.html
https://docs.python.org/3/library/index.html
https://docs.python.org/3/reference/index.html
https://docs.python.org/3/using/index.html
https://docs.python.org/3/howto/index.html
https://docs.python.org/3/installing/index.html
https://docs.python.org/3/distributing/index.html
https://docs.python.org/3/extending/index.html
https://docs.python.org/3/c-api/index.html
https://docs.python.org/3/faq/index.html
https://docs.python.org/3/deprecations/index.html
https://docs.python.org/3/py-modindex.html
https://docs.python.org/3/genindex.html
https://docs.python.org/3/glossary.html
https://docs.python.org/3/search.html
https://docs.python.org/3/contents.html
https://peps.python.org/
https://wiki.python.org/moin/BeginnersGuide
https://wiki.python.org/moin/PythonBooks
https://www.python.org/doc/av/
https://devguide.python.org/
https://docs.python.org/3/bugs.html
https://devguide.python.org/documentation/help-documenting/
https://docs.python.org/3/license.html
https://docs.python.org/3/copyright.html
https://docs.python.org/3/about.html
```

--------------------------------

### sysconfig.get_paths() - Get Installation Paths

Source: https://docs.python.org/3/library/sysconfig

Retrieves a dictionary of all installation paths for a given scheme. Supports custom schemes and variable expansion. Raises KeyError if the scheme is not found.

```python
import sysconfig

# Get default installation paths
paths = sysconfig.get_paths()
print(paths)

# Get paths for a specific scheme (e.g., 'nt' for Windows)
# windows_paths = sysconfig.get_paths(scheme='nt')
# print(windows_paths)

# Get paths with custom variables and without expansion
# custom_paths = sysconfig.get_paths(vars={'base': '/my/custom/path'}, expand=False)
# print(custom_paths)
```

--------------------------------

### Example Command-Line Parsing with optparse

Source: https://docs.python.org/3/library/optparse

Provides an example of a typical command-line invocation and breaks down its components into options, option arguments, and positional arguments as understood by optparse.

```python
# Example command-line:
# prog -v --report report.txt foo bar

# Breakdown:
# -v: A short option.
# --report: A long option.
# report.txt: An option argument for --report.
# foo: A positional argument.
# bar: Another positional argument.
```

--------------------------------

### Python Launcher for Windows - Command-line Usage

Source: https://docs.python.org/3/using/windows

Demonstrates how to use the Python launcher from the command line to manage Python installations and virtual environments.

```python
py -0p
# Lists installed Python versions
py -3.11 script.py
# Runs script.py with Python 3.11
py -m venv myenv
# Creates a virtual environment named 'myenv'
```

--------------------------------

### Basic Asyncio Event Loop Example

Source: https://docs.python.org/3/library/asyncio-eventloop

A simple Python example demonstrating how to get the running event loop and print its representation. This illustrates the basic usage of `asyncio.get_running_loop()` within an asynchronous context.

```python
import asyncio

async def main():
    loop = asyncio.get_running_loop()
    print(f"Current running event loop: {loop}")

if __name__ == "__main__":
    asyncio.run(main())
```

--------------------------------

### Python Asyncio Server Example

Source: https://docs.python.org/3/library/asyncio-eventloop

Illustrates how to use the asyncio Server's serve_forever() method to start accepting connections and handle client communication within an asynchronous context.

```python
import asyncio

async def client_connected(reader, writer):
    # Communicate with the client with
    # reader/writer streams.  For example:
    await reader.readline()

async def main(host, port):
    srv = await asyncio.start_server(
        client_connected, host, port)
    await srv.serve_forever()

asyncio.run(main('127.0.0.1', 0))
```

--------------------------------

### Python Documentation Navigation and Resources

Source: https://docs.python.org/3/library/tkinter

Provides links to various sections of the Python documentation, including version-specific documentation, tutorials, library and language references, installation guides, and community resources like PEPs and developer guides.

```python
https://docs.python.org/3/download.html
https://docs.python.org/3/whatsnew/3.13.html
https://docs.python.org/3/tutorial/index.html
https://docs.python.org/3/library/index.html
https://docs.python.org/3/reference/index.html
https://docs.python.org/3/using/index.html
https://docs.python.org/3/howto/index.html
https://docs.python.org/3/installing/index.html
https://docs.python.org/3/distributing/index.html
https://docs.python.org/3/extending/index.html
https://docs.python.org/3/c-api/index.html
https://docs.python.org/3/faq/index.html
https://docs.python.org/3/deprecations/index.html
https://docs.python.org/3/py-modindex.html
https://docs.python.org/3/genindex.html
https://docs.python.org/3/glossary.html
https://docs.python.org/3/search.html
https://docs.python.org/3/contents.html
https://peps.python.org/
https://wiki.python.org/moin/BeginnersGuide
https://wiki.python.org/moin/PythonBooks
https://www.python.org/doc/av/
https://devguide.python.org/
https://docs.python.org/3/bugs.html
https://devguide.python.org/documentation/help-documenting/
https://docs.python.org/3/license.html
https://docs.python.org/3/copyright.html
https://docs.python.org/3/about.html
```

--------------------------------

### Building Python Extensions with setuptools

Source: https://docs.python.org/3/extending/windows

This section describes the recommended approach for building and packaging Python extension modules using the setuptools package. It provides guidance for module authors to control the build process effectively.

```python
from setuptools import setup, Extension

setup(
    name='my_extension',
    version='1.0',
    ext_modules=[
        Extension('my_extension', sources=['my_extension.c'])
    ]
)
```

--------------------------------

### Virtual Environment Creation and Usage

Source: https://docs.python.org/3/installing/index

Demonstrates the creation and activation of a virtual environment using the `venv` module, which is the recommended way to manage project dependencies.

```bash
# Create a virtual environment
python -m venv myenv

# Activate the virtual environment (Windows)
myenv\Scripts\activate.bat

# Activate the virtual environment (POSIX)
source myenv/bin/activate
```

--------------------------------

### Descriptor Lookup Example

Source: https://docs.python.org/3/howto/descriptor

An interactive session demonstrating the difference between normal attribute lookup (a.x) and descriptor lookup (a.y), highlighting that descriptor values are computed on demand.

```python
>>> a = A()                     # Make an instance of class A
>>> a.x                         # Normal attribute lookup
5
>>> a.y                         # Descriptor lookup
10
```

--------------------------------

### Python Logging Configuration Example

Source: https://docs.python.org/3/howto/logging

Demonstrates a basic configuration for the Python logging module, setting up a root logger with a specific format and handler.

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler("app.log"),
        logging.StreamHandler()
    ]
)

logger = logging.getLogger(__name__)
logger.info("This is an informational message.")
logger.warning("This is a warning message.")
```

--------------------------------

### Python Basic Authentication Setup

Source: https://docs.python.org/3/howto/urllib2

Demonstrates how to set up basic HTTP authentication in Python using `urllib.request`. It shows the creation of a password manager and adding credentials for a given URL and realm.

```python
import urllib.request

# create a password manager
password_mgr = urllib.request.HTTPPasswordMgrWithDefaultRealm()

# Add the username and password.
# password_mgr.add_password(None, url, user, password)
```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/howto/webservers

Lists essential external resources for Python developers, including the Python Enhancement Proposal (PEP) index, guides for beginners, book recommendations, audio/visual talks, and the Python Developer's Guide.

```markdown
* [PEP Index](https://peps.python.org/)
* [Beginner's Guide](https://wiki.python.org/moin/BeginnersGuide)
* [Book List](https://wiki.python.org/moin/PythonBooks)
* [Audio/Visual Talks](https://www.python.org/doc/av/)
* [Python Developer’s Guide](https://devguide.python.org/)
```

--------------------------------

### itertools.islice() Examples

Source: https://docs.python.org/3/howto/functional

Explains itertools.islice(), which returns a slice of an iterator. It covers slicing with stop, start and stop, and start, stop, and step arguments. Note that negative indices are not supported.

```python
import itertools

# Slice with stop
print(list(itertools.islice(range(10), 8)))

# Slice with start and stop
print(list(itertools.islice(range(10), 2, 8)))

# Slice with start, stop, and step
print(list(itertools.islice(range(10), 2, 8, 2)))
```

--------------------------------

### Python Comments Example

Source: https://docs.python.org/3/tutorial/introduction

Demonstrates how to use comments in Python. Comments start with '#' and are ignored by the interpreter. They can be used to explain code or to prevent execution of code.

```python
# this is the first comment
spam = 1  # and this is the second comment
          # ... and now a third!
text = "# This is not a comment because it's inside quotes."
```

--------------------------------

### Optparse Example: Adding Options and Help

Source: https://docs.python.org/3/library/optparse

Demonstrates how to create an OptionParser, add various options (including suppressing help for specific options), and configure the parser to handle help messages.

```python
from optparse import OptionParser, SUPPRESS_HELP

# usually, a help option is added automatically, but that can
# be suppressed using the add_help_option argument
parser = OptionParser(add_help_option=False)

parser.add_option("-h", "--help", action="help")
parser.add_option("-v", action="store_true", dest="verbose",
                  help="Be moderately verbose")
parser.add_option("--file", dest="filename",
                  help="Input file to read data from")
parser.add_option("--secret", help=SUPPRESS_HELP)
```

--------------------------------

### Python Configuration Options - Install

Source: https://docs.python.org/3/using/configure

Options controlling the installation process of Python, including installation directories and permissions.

```APIDOC
Configure Options - Install Options:
  --install-base=DIR
    Install Python base system in DIR.
  --install-platbase=DIR
    Install Python platform specific files in DIR.
  --install-scripts=DIR
    Install scripts in DIR.
  --install-data=DIR
    Install data files in DIR.
  --install-headers=DIR
    Install C header files in DIR.
```

--------------------------------

### Dynamic Descriptor Lookup Example

Source: https://docs.python.org/3/howto/descriptor

An interactive session showcasing the dynamic nature of the 'DirectorySize' descriptor. It shows how the 'size' attribute updates automatically when the directory contents change.

```python
>>> s = Directory('songs')
>>> g = Directory('games')
>>> s.size                              # The songs directory has twenty files
20
>>> g.size                              # The games directory has three files
3
>>> os.remove('games/chess')            # Delete a game
>>> g.size                              # File count is automatically updated
2
```

--------------------------------

### Python 3.7.17 Documentation Overview

Source: https://docs.python.org/3/.7

This snippet outlines the main sections of the Python 3.7.17 documentation, including 'What's new', 'Tutorial', 'Library Reference', 'Language Reference', 'Python Setup and Usage', 'Python HOWTOs', 'Installing Python Modules', 'Distributing Python Modules', 'Extending and Embedding', 'Python/C API', and 'FAQs'. It also points to related resources like indices, glossaries, and search functionality.

```python
# Python 3.7.17 Documentation

# Main Sections:
# - What's new in Python 3.7?
# - Tutorial
# - Library Reference
# - Language Reference
# - Python Setup and Usage
# - Python HOWTOs
# - Installing Python Modules
# - Distributing Python Modules
# - Extending and Embedding
# - Python/C API
# - FAQs

# Indices and tables:
# - Global Module Index
# - General Index
# - Glossary
# - Search page
# - Complete Table of Contents

# Meta information:
# - Reporting bugs
# - About the documentation
# - History and License of Python
# - Copyright
```

--------------------------------

### Dictionary-Based Configuration Example

Source: https://docs.python.org/3/howto/logging-cookbook

Demonstrates how to configure the logging system using a dictionary, which is a flexible and powerful way to manage logging settings. This approach is particularly useful for complex configurations.

```python
import logging
import logging.config

LOGGING_CONFIG = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'standard': {
            'format': '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
        },
    },
    'handlers': {
        'console': {
            'level': 'INFO',
            'class': 'logging.StreamHandler',
            'formatter': 'standard'
        },
        'file': {
            'level': 'DEBUG',
            'class': 'logging.FileHandler',
            'filename': 'app.log',
            'formatter': 'standard'
        },
    },
    'loggers': {
        '': {  # root logger
            'handlers': ['console', 'file'],
            'level': 'DEBUG',
            'propagate': True
        },
        'my_module': {
            'handlers': ['console'],
            'level': 'INFO',
            'propagate': False
        }
    }
}

logging.config.dictConfig(LOGGING_CONFIG)

logger = logging.getLogger(__name__)
logger.debug('This is a debug message.')
logger.info('This is an info message.')

my_module_logger = logging.getLogger('my_module')
my_module_logger.warning('This is a warning from my_module.')
```

--------------------------------

### Python Class and Method Access Example

Source: https://docs.python.org/3/howto/descriptor

Demonstrates how Python's descriptor protocol works for methods. It shows accessing a function directly from the class and how it becomes a bound method when accessed through an instance.

```python
class D:
    def f(self):
         return self

class D2:
    pass

# Accessing through class dictionary
# print(D.__dict__['f']) # Output: <function D.f at ...>

# Accessing directly from class
# print(D.f) # Output: <function D.f at ...>

# Accessing through instance
# d = D()
# print(d.f) # Output: <bound method D.f of <__main__.D object at ...>>
# print(d.f.__func__) # Output: <function D.f at ...>
# print(d.f.__self__) # Output: <__main__.D object at ...>
```

--------------------------------

### Download All Python Installer Components

Source: https://docs.python.org/3/using/windows

This command downloads all necessary components for a complete Python installation, enabling offline installations regardless of selected features. It's useful for large-scale deployments. The `/quiet` option can be used to suppress the progress display.

```cmd
python-3.9.0.exe /layout

```

--------------------------------

### Python enumerate Function Example

Source: https://docs.python.org/3/library/functions

Demonstrates the usage of the enumerate function to iterate over a sequence with an index, starting from a specified number.

```python
>>> list(enumerate(seasons, start=1))
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
```

--------------------------------

### Managed Attributes with Descriptors

Source: https://docs.python.org/3/howto/descriptor

Illustrates how descriptors can be used to manage attributes, providing custom logic for getting, setting, or deleting them.

```python
class ManagedAttribute:
    def __init__(self, name):
        self.name = name
        self.storage = {}

    def __get__(self, instance, owner):
        if instance is None:
            return self
        return self.storage.get(self.name, None)

    def __set__(self, instance, value):
        self.storage[self.name] = value

class MyClass:
    attr = ManagedAttribute('attr')

# Usage:
obj = MyClass()
obj.attr = 10
print(obj.attr)
```

--------------------------------

### Test Examples in a Text File with Verbose Output

Source: https://docs.python.org/3/library/doctest

This demonstrates running doctests from a text file with verbose output. Similar to `testmod()`, the `-v` command-line flag or the `verbose=True` argument in `doctest.testfile()` can be used to get a detailed report of the testing process.

```python
# Command line execution:
# python -m doctest example.txt -v

# Programmatic execution:
import doctest

doctest.testfile("example.txt", verbose=True)
```

--------------------------------

### Python Dictionary-Based Logging Configuration

Source: https://docs.python.org/3/howto/logging-cookbook

An example of a logging configuration dictionary that can be passed to `logging.config.dictConfig()`. It defines formatters, handlers, filters, and loggers for a complex logging setup.

```python
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'verbose': {
            'format': '{levelname}{asctime}{module}{process:d}{thread:d}{message}',
            'style': '{',
        },
        'simple': {
            'format': '{levelname}{message}',
            'style': '{',
        },
    },
    'filters': {
        'special': {
            '()': 'project.logging.SpecialFilter',
            'foo': 'bar',
        },
    },
    'handlers': {
        'console': {
            'level': 'INFO',
            'class': 'logging.StreamHandler',
            'formatter': 'simple',
        },
        'mail_admins': {
            'level': 'ERROR',
            'class': 'django.utils.log.AdminEmailHandler',
            'filters': ['special']
        }
    },
    'loggers': {
        'django': {
            'handlers': ['console'],
            'propagate': True,
        },
        'django.request': {
            'handlers': ['mail_admins'],
            'level': 'ERROR',
            'propagate': False,
        },
        'myproject.custom': {
            'handlers': ['console', 'mail_admins'],
            'level': 'INFO',
            'filters': ['special']
        }
    }
}
```

--------------------------------

### ensurepip Module and Command Line Options

Source: https://docs.python.org/3/genindex-E

Information about the 'ensurepip' module, which bootstraps the pip installer for Python. Includes details on its command-line options for installation control.

```APIDOC
ensurepip module
  - Bootstraps the pip installer.

ensurepip command line options:
  --altinstall: Install pip and setuptools without overwriting existing packages.
  --default-pip: Ensure pip is installed as the default package installer.
  --root <dir>: Install packages into <dir> instead of the default location.
  --user: Install packages into the user site-packages directory.
```

--------------------------------

### Shell Script for Framework Signing and Python Extension Installation

Source: https://docs.python.org/3/using/ios

This shell script snippet demonstrates how to sign frameworks and install Python standard library extension modules. It involves setting up back references, identifying Python versions, and iterating through .so files for installation. It also includes commands for cleaning up dylib templates and signing frameworks with specified identities and flags.

```shell
echo"${RELATIVE_EXT%.so}.fwork""$CODESIGNING_FOLDER_PATH/$FRAMEWORK_FOLDER/$FULL_MODULE_NAME.origin"

PYTHON_VER=$(ls"$CODESIGNING_FOLDER_PATH/python/lib")
echo"Install Python $PYTHON_VER standard library extension modules..."
"$CODESIGNING_FOLDER_PATH/python/lib/$PYTHON_VER/lib-dynload""*.so"|whileread;do
$PYTHON_VER/lib-dynload/"$FULL_EXT"
done

# Clean up dylib template
"$CODESIGNING_FOLDER_PATH/dylib-Info-template.plist"

echo"Signing frameworks as $EXPANDED_CODE_SIGN_IDENTITY_NAME ($EXPANDED_CODE_SIGN_IDENTITY)..."
"$CODESIGNING_FOLDER_PATH/Frameworks""*.framework""$EXPANDED_CODE_SIGN_IDENTITY""$OTHER_CODE_SIGN_FLAGS:-}=none=identifier,entitlements,flags"{}
```

--------------------------------

### Basic Argparse Example

Source: https://docs.python.org/3/howto/argparse

A minimal example demonstrating the creation of an ArgumentParser and parsing arguments. It shows the default help message and how unrecognized arguments are handled.

```python
import argparse

parser = argparse.ArgumentParser()
parser.parse_args()
```

--------------------------------

### Python Resources and Navigation

Source: https://docs.python.org/3/.9

Lists important Python resources such as the PEP Index, Beginner's Guide, Book List, Audio/Visual Talks, and the Python Developer's Guide. Also includes navigation links for the documentation index, module index, and the main Python website.

```python
# Other resources
print('PEP Index: https://peps.python.org/')
print('Beginner\'s Guide: https://wiki.python.org/moin/BeginnersGuide')
print('Book List: https://wiki.python.org/moin/PythonBooks')
print('Audio/Visual Talks: https://www.python.org/doc/av/')
print('Python Developer\'s Guide: https://devguide.python.org/')

# Navigation
print('General Index: https://docs.python.org/3.9/genindex.html')
print('Python Module Index: https://docs.python.org/3.9/py-modindex.html')
print('Python Website: https://www.python.org/')
```

--------------------------------

### Unattended Installation Configuration (unattend.xml)

Source: https://docs.python.org/3/using/windows

This XML file specifies installation options for unattended installations, mirroring command-line arguments. It allows for declarative configuration of the Python installation process.

```APIDOC
<Options>
  <Option Name="InstallAllUsers" Value="no"/>
  <Option Name="Include_launcher" Value="0"/>
  <Option Name="Include_test" Value="no"/>
  <Option Name="SimpleInstall" Value="yes"/>
  <Option Name="SimpleInstallDescription">Just</Option>
</Options>
```

--------------------------------

### Descriptor Validation Examples

Source: https://docs.python.org/3/howto/descriptor

These Python examples demonstrate how the custom descriptors in the Component class prevent the creation of invalid instances. They show various scenarios where validation fails due to incorrect data types, out-of-range values, or unmet predicates, resulting in ValueErrors or TypeErrors.

```python
>>> Component('Widget', 'metal', 5)      # Blocked: 'Widget' is not all uppercase
Traceback (most recent call last):
...ValueError: Expected <method 'isupper' of 'str' objects> to be true for 'Widget'

>>> Component('WIDGET', 'metle', 5)      # Blocked: 'metle' is misspelled
Traceback (most recent call last):
...ValueError: Expected 'metle' to be one of {'metal', 'plastic', 'wood'}

>>> Component('WIDGET', 'metal', -5)     # Blocked: -5 is negative
Traceback (most recent call last):
...ValueError: Expected -5 to be at least 0

>>> Component('WIDGET', 'metal', 'V')    # Blocked: 'V' isn't a number
Traceback (most recent call last):
...TypeError: Expected 'V' to be an int or float

>>> c = Component('WIDGET', 'metal', 5)  # Allowed:  The inputs are valid
```

--------------------------------

### Python turtle Module Setup Function

Source: https://docs.python.org/3/genindex-S

Documentation for the setup function in the turtle module, used to initialize the turtle graphics screen.

```APIDOC
turtle.setup(width=0.5, height=0.75, startx=None, starty=None)
  - Initialize the turtle screen.
  - width: The width of the screen in pixels or fraction of screen.
  - height: The height of the screen in pixels or fraction of screen.
  - startx: The x coordinate of the top-left corner.
  - starty: The y coordinate of the top-left corner.
```

--------------------------------

### Dictionary-Based Configuration Example

Source: https://docs.python.org/3/howto/logging-cookbook

Demonstrates how to configure the logging system using a dictionary, which is a flexible and powerful way to manage logging settings. This approach is particularly useful for complex configurations.

```python
import logging
import logging.config

LOGGING_CONFIG = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'standard': {
            'format': '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
        },
    },
    'handlers': {
        'console': {
            'level': 'INFO',
            'class': 'logging.StreamHandler',
            'formatter': 'standard'
        },
        'file': {
            'level': 'DEBUG',
            'class': 'logging.FileHandler',
            'filename': 'app.log',
            'formatter': 'standard'
        },
    },
    'loggers': {
        '': {  # root logger
            'handlers': ['console', 'file'],
            'level': 'DEBUG',
            'propagate': True
        },
        'my_module': {
            'handlers': ['console'],
            'level': 'INFO',
            'propagate': False
        }
    }
}

logging.config.dictConfig(LOGGING_CONFIG)

logger = logging.getLogger(__name__)
logger.debug('This is a debug message.')
logger.info('This is an info message.')

my_module_logger = logging.getLogger('my_module')
my_module_logger.warning('This is a warning from my_module.')
```

--------------------------------

### Python distutils Module

Source: https://docs.python.org/3/genindex-M

The distutils module provides support for building and installing Python packages. It is used for creating setup scripts and managing package distribution.

```python
# Example setup.py using distutils
from distutils.core import setup, Extension

setup(name='MyPackage', version='1.0', 
      ext_modules=[Extension('my_module', sources=['my_module.c'])])
```

--------------------------------

### Basic XML Parsing with Event Handlers

Source: https://docs.python.org/3/library/pyexpat

An example of using the pyexpat module to parse XML. It defines handler functions for start elements, end elements, and character data, and then associates them with a parser instance. The example demonstrates parsing a simple XML string.

```python
import xml.parsers.expat

# 3 handler functions
def start_element(name, attrs):
    print('Start element:', name, attrs)
def end_element(name):
    print('End element:', name)
def char_data(data):
    print('Character data:', repr(data))

p = xml.parsers.expat.ParserCreate()

p.StartElementHandler = start_element
p.EndElementHandler = end_element
p.CharacterDataHandler = char_data

p.Parse("""<?xml version="1.0"?>
<parent id="top"><child1 name="paul">Text goes here</child1>
<child2 name="fred">More text</child2>
</parent>""", 1)
```

--------------------------------

### pprint.saferepr Example

Source: https://docs.python.org/3/library/pprint

Demonstrates the usage of pprint.saferepr to get a string representation of an object, handling potential recursion.

```python
import pprint

stuff = ['spam', 'eggs', 'lumberjack', 'knights', 'ni']
# Simulate recursion for demonstration
stuff.append(stuff)

print(pprint.saferepr(stuff))
```

--------------------------------

### Python Documentation Copyright and Licensing

Source: https://docs.python.org/3/tutorial/introduction

Details the copyright and licensing information for the Python documentation. It specifies the license under which the page content and code examples are provided.

```python
© [ Copyright ](https://docs.python.org/3/copyright.html) 2001-2025, Python Software Foundation.   
This page is licensed under the Python Software Foundation License Version 2.   
Examples, recipes, and other code in the documentation are additionally licensed under the Zero Clause BSD License.   
See [History and License](https://docs.python.org/license.html) for more information.  

The Python Software Foundation is a non-profit corporation. [Please donate.](https://www.python.org/psf/donations/)
```

--------------------------------

### Python Static Method Example

Source: https://docs.python.org/3/howto/descriptor

Demonstrates a simple class with a static method. Static methods can be called on the class itself or an instance without needing access to instance-specific data.

```python
class E:
    @staticmethod
    def f(x):
        return x * 10
```

--------------------------------

### Install Python Packages with pip

Source: https://docs.python.org/3/tutorial/venv

Demonstrates installing, upgrading, and uninstalling Python packages using pip. It covers installing the latest version, a specific version, and upgrading.

```bash
python -m pip install <package-name>
python -m pip install <package-name>==<version-number>
python -m pip install --upgrade <package-name>
```

--------------------------------

### Building C/C++ Extensions with setuptools

Source: https://docs.python.org/3/extending/building

This section details how to use the setuptools package to build C and C++ extensions for Python. It covers the necessary configurations and steps involved in integrating compiled code with Python projects.

```python
from setuptools import setup, Extension

setup(
    name='my_extension',
    version='1.0',
    ext_modules=[
        Extension('my_extension', sources=['my_extension.c'])
    ]
)
```

--------------------------------

### Python Logging Example

Source: https://docs.python.org/3/howto/logging-cookbook

Basic usage of Python's logging module to get loggers and log messages at different levels (debug, info, warning, error).

```python
import logging

logger1 = logging.getLogger('myapp.area1')
logger2 = logging.getLogger('myapp.area2')

logger1.debug('Quick zephyrs blow, vexing daft Jim.')
logger1.info('How quickly daft jumping zebras vex.')
logger2.warning('Jail zesty vixen who grabbed pay from quack.')
logger2.error('The five boxing wizards jump quickly.')
```

--------------------------------

### ConfigParser Initialization and Usage Example

Source: https://docs.python.org/3/library/configparser

Demonstrates how to initialize a ConfigParser object, set default values, write to a file, and read multiple configuration files with overriding behavior. It shows how to access values from the parsed configuration.

```python
import configparser

config_override = configparser.ConfigParser()
config_override['DEFAULT'] = {'ServerAliveInterval': '-1'}
with open('override.ini', 'w') as configfile:
    config_override.write(configfile)

config_override = configparser.ConfigParser()
config_override.read(['example.ini', 'override.ini'])
print(config_override.get('DEFAULT', 'ServerAliveInterval'))
```

--------------------------------

### Subclassing QueueHandler and QueueListener (pynng Example)

Source: https://docs.python.org/3/howto/logging-cookbook

Demonstrates subclassing `QueueHandler` and `QueueListener` using the `pynng` library for efficient message queuing in a logging system. This is an alternative to ZeroMQ for high-performance messaging.

```python
import logging
import logging.handlers
import queue
import threading
from pynng import Push0, Pull0

class NngHandler(logging.handlers.QueueHandler):
    def __init__(self, address='tcp://127.0.0.1:5558'):
        super().__init__(queue.Queue(-1))
        self.sock = Push0(dial=address)

    def emit(self, record):
        try:
            self.sock.send(self.format(record).encode('utf-8'))
        except Exception:
            self.handleError(record)

class NngListener(logging.handlers.QueueListener):
    def __init__(self, handlers, address='tcp://127.0.0.1:5558', respect_handler_level=False):
        super().__init__([], respect_handler_level=respect_handler_level)
        self.sock = Pull0(listen=address)
        self.handlers = handlers
        self._stop_event = threading.Event()

    def _monitor(self):
        while not self._stop_event.is_set():
            try:
                log_message = self.sock.recv().decode('utf-8')
                for handler in self.handlers:
                    try:
                        # Assuming handlers can process string messages
                        handler.handle(logging.LogRecord(name='', level=logging.INFO, pathname='', 
                                                         lineno=0, msg=log_message, args=(), exc_info=None))
                    except Exception:
                        logging.Error('Error processing log message in listener', exc_info=True)
            except Exception:
                logging.Error('Error receiving log message', exc_info=True)

# Example Usage:
# logger = logging.getLogger('nng_logger')
# nng_handler = NngHandler()
# logger.addHandler(nng_handler)
# logger.setLevel(logging.INFO)

# listener_handlers = [logging.StreamHandler()]
# listener = NngListener(listener_handlers)
# listener.start()

# logger.info('Sending log message via pynng')
# time.sleep(2) # Give time for listener to process
# listener.stop()
```

--------------------------------

### Python unittest.TestCase Method

Source: https://docs.python.org/3/genindex-S

Documentation for the setUp method in unittest.TestCase, called before each test method.

```APIDOC
unittest.TestCase.setUp()
  - Called before each test method. Can be overridden.
```

--------------------------------

### Python gettext.NullTranslations Class Example

Source: https://docs.python.org/3/library/gettext

Demonstrates how to use the gettext.NullTranslations class and its install method to make translation functions available in the global namespace.

```python
import gettext

# Example of making '_' available globally
t = gettext.translation('mymodule', '/path/to/locale', languages=['en'])
_ = t.gettext

# Or using the install method
# gettext.NullTranslations().install(['gettext', 'ngettext'])

# Usage example:
# print(_('Hello, world!'))
```

--------------------------------

### Wrapping Existing Test Functions with FunctionTestCase

Source: https://docs.python.org/3/library/unittest

This example shows how to use unittest.FunctionTestCase to wrap standalone test functions, allowing them to be integrated into the unittest framework. It also illustrates how to provide optional setUp and tearDown methods for managing test environment setup and cleanup.

```python
import unittest

def testSomething():
    something = makeSomething()
    assert something.name is not None
    # ...

testcase = unittest.FunctionTestCase(testSomething,
                                     setUp=makeSomethingDB,
                                     tearDown=deleteSomethingDB)
```

--------------------------------

### Descriptor Example: Constant Return

Source: https://docs.python.org/3/howto/descriptor

A simple descriptor that always returns a constant value when accessed. This illustrates the basic functionality of the __get__ method.

```python
class ConstantDescriptor:
    def __init__(self, value):
        self.value = value

    def __get__(self, instance, owner):
        return self.value
```

--------------------------------

### Get Bytecode Line Ranges (co_lines)

Source: https://docs.python.org/3/reference/datamodel

Provides an iterator yielding information about bytecode ranges and their corresponding line numbers. Each item is a tuple (start, end, lineno), where 'start' and 'end' are bytecode offsets and 'lineno' is the line number. Ranges are non-decreasing and consecutive, with the last range ending at the bytecode size.

```python
codeobject.co_lines()
# Returns an iterator yielding tuples: (start_offset, end_offset, lineno)
```

--------------------------------

### Subclassing QueueHandler and QueueListener (pynng Example)

Source: https://docs.python.org/3/howto/logging-cookbook

Demonstrates subclassing `QueueHandler` and `QueueListener` using the `pynng` library for efficient message queuing in a logging system. This is an alternative to ZeroMQ for high-performance messaging.

```python
import logging
import logging.handlers
import queue
import threading
from pynng import Push0, Pull0

class NngHandler(logging.handlers.QueueHandler):
    def __init__(self, address='tcp://127.0.0.1:5558'):
        super().__init__(queue.Queue(-1))
        self.sock = Push0(dial=address)

    def emit(self, record):
        try:
            self.sock.send(self.format(record).encode('utf-8'))
        except Exception:
            self.handleError(record)

class NngListener(logging.handlers.QueueListener):
    def __init__(self, handlers, address='tcp://127.0.0.1:5558', respect_handler_level=False):
        super().__init__([], respect_handler_level=respect_handler_level)
        self.sock = Pull0(listen=address)
        self.handlers = handlers
        self._stop_event = threading.Event()

    def _monitor(self):
        while not self._stop_event.is_set():
            try:
                log_message = self.sock.recv().decode('utf-8')
                for handler in self.handlers:
                    try:
                        # Assuming handlers can process string messages
                        handler.handle(logging.LogRecord(name='', level=logging.INFO, pathname='', 
                                                         lineno=0, msg=log_message, args=(), exc_info=None))
                    except Exception:
                        logging.Error('Error processing log message in listener', exc_info=True)
            except Exception:
                logging.Error('Error receiving log message', exc_info=True)

# Example Usage:
# logger = logging.getLogger('nng_logger')
# nng_handler = NngHandler()
# logger.addHandler(nng_handler)
# logger.setLevel(logging.INFO)

# listener_handlers = [logging.StreamHandler()]
# listener = NngListener(listener_handlers)
# listener.start()

# logger.info('Sending log message via pynng')
# time.sleep(2) # Give time for listener to process
# listener.stop()
```

--------------------------------

### Python Optparse Tutorial and Reference

Source: https://docs.python.org/3/contents

This documentation details the `optparse` module for command-line option parsing in Python. It covers the tutorial aspects like understanding option actions (store, boolean flags), default values, generating help messages, and printing version strings. The reference guide explains creating and populating parsers, defining options with attributes, standard actions and types, parsing arguments, and handling option conflicts.

```python
from optparse import OptionParser

parser = OptionParser()
parser.add_option('-f', '--file', dest='filename', help='write report to FILE', metavar='FILE')
parser.add_option('-q', '--quiet', action='store_false', dest='verbose', default=True, help='don't print status messages to stdout')

(options, args) = parser.parse_args()

if options.filename:
    print(f"Writing to file: {options.filename}")

if options.verbose:
    print("Verbose mode enabled")
else:
    print("Quiet mode enabled")
```

--------------------------------

### Basic optparse Script Example

Source: https://docs.python.org/3/library/optparse

Demonstrates a typical structure for a Python script using the optparse library to handle command-line arguments, including adding options and parsing them.

```python
from optparse import OptionParser

def main():
    usage = "usage: %prog [options] arg"
    parser = OptionParser(usage)
    parser.add_option("-f", "--file", dest="filename",
                      help="read data from FILENAME")
    parser.add_option("-v", "--verbose",
                      action="store_true", dest="verbose")
    parser.add_option("-q", "--quiet",
                      action="store_false", dest="verbose")

    (options, args) = parser.parse_args()
    if len(args) != 1:
        parser.error("incorrect number of arguments")
    if options.verbose:
        print("reading %s..." % options.filename)

if __name__ == "__main__":
    main()
```

--------------------------------

### unittest.TestCase.setUpClass

Source: https://docs.python.org/3/genindex-S

Class method to run setup for a test class.

```APIDOC
unittest.TestCase.setUpClass()
  A class method that is run once before any tests in the class are run.
```

--------------------------------

### Install Packages from Requirements File

Source: https://docs.python.org/3/tutorial/venv

Installs all packages listed in a 'requirements.txt' file into the current virtual environment. This is useful for replicating project dependencies.

```bash
python -m pip install -r requirements.txt
```

--------------------------------

### Python Multiprocessing Process Management Example

Source: https://docs.python.org/3/library/multiprocessing

Demonstrates starting, checking the status of, and terminating a multiprocessing Process object. It also shows how to verify the exit status after termination.

```python
>>> p.start()
>>> print(p, p.is_alive())
<...Process ... started> True
>>> p.terminate()
>>> time.sleep(0.1)
>>> print(p, p.is_alive())
<...Process ... stopped exitcode=-SIGTERM> False
>>> p.exitcode == -signal.SIGTERM
True
```

--------------------------------

### Start Command Module (start.py)

Source: https://docs.python.org/3/howto/logging-cookbook

This Python module implements the 'start' command for the CLI application. It logs debug information before starting a service and an info message upon successful completion.

```python
# start.py
import logging

logger = logging.getLogger(__name__)

defcommand(options):
    logger.debug('About to start %s', options.name)
    # actually do the command processing here ...
    logger.info('Started the \'%s\' service.', options.name)

```

--------------------------------

### Alternate Class Constructor using Class Method

Source: https://docs.python.org/3/howto/descriptor

Shows how to use a class method to create an alternate constructor for a class. This example emulates the behavior of `dict.fromkeys()` by creating a new dictionary instance from an iterable.

```python
class Dict(dict):
    @classmethod
    def fromkeys(cls, iterable, value=None):
        """Emulate dict_fromkeys() in Objects/dictobject.c"""
        d = cls()
        for key in iterable:
            d[key] = value
        return d
```

```python
>>> d = Dict.fromkeys('abracadabra')
>>> type(d) is Dict
True
>>> d
{'a': None, 'b': None, 'r': None, 'c': None, 'd': None}
```

--------------------------------

### Work with Multiple Python Versions (POSIX)

Source: https://docs.python.org/3/installing/index

Demonstrates how to use versioned Python commands with the `-m` switch to run the appropriate copy of pip on Linux, macOS, and other POSIX systems.

```bash
python3.9 -m pip install <package>
python3.10 -m pip install <package>
```

--------------------------------

### venv.EnvBuilder Methods

Source: https://docs.python.org/3/genindex-S

Documentation for `setup_python` and `setup_scripts` methods within the `venv.EnvBuilder` class, used for setting up Python virtual environments.

```APIDOC
venv.EnvBuilder.setup_python()
  Sets up the Python interpreter for the virtual environment.

virtualenv.EnvBuilder.setup_scripts(env_dir, symlink=True)
  Sets up the script directory for the virtual environment.
```

--------------------------------

### Get Installation Prefix

Source: https://docs.python.org/3/c-api/init

Returns the prefix for installed platform-independent files. This is derived from the program name and environment variables. The returned string points into static storage and should not be modified. This corresponds to the prefix variable in the Makefile and the --prefix argument to the configure script. The value is available to Python code as sys.base_prefix. It is only useful on Unix. This function should not be called before Py_Initialize(), otherwise it returns NULL.

```c
wchar_t* Py_GetPrefix();
/* Deprecated since version 3.13, will be removed in version 3.15: Get sys.base_prefix instead, or sys.prefix if virtual environments need to be handled. */
```

--------------------------------

### Basic optparse Usage Example

Source: https://docs.python.org/3/library/optparse

Demonstrates the fundamental usage of the optparse library to create an OptionParser, add options with help messages and destinations, and parse command-line arguments. It shows how to define options like '--file' and '--quiet' and access the parsed values.

```python
from optparse import OptionParser

parser = OptionParser()
parser.add_option("-f", "--file", dest="filename",
                  help="write report to FILE", metavar="FILE")
parser.add_option("-q", "--quiet",
                  action="store_false", dest="verbose", default=True,
                  help="don't print status messages to stdout")

(options, args) = parser.parse_args()
```

--------------------------------

### venv.EnvBuilder.post_setup Method

Source: https://docs.python.org/3/genindex-P

This method is part of the venv.EnvBuilder class and is called after the environment has been set up. It is intended for custom setup actions.

```APIDOC
venv.EnvBuilder.post_setup()
  - Called after the environment has been set up.
  - Intended for custom setup actions.
```

--------------------------------

### ensurepip Module API

Source: https://docs.python.org/3/library/distribution

Provides functions for bootstrapping the pip installer into Python environments. It allows for the installation of pip and setuptools.

```APIDOC
ensurepip Module API:
  ensurepip.bootstrap(level=EnsurePip.INSTALL, 
                      																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																																			
```

--------------------------------

### Python unicodedata.category() Example

Source: https://docs.python.org/3/library/unicodedata

Demonstrates how to use `unicodedata.category()` to get the general category of a Unicode character. This is useful for classifying characters based on their type.

```python
import unicodedata

char1 = 'A'
char2 = '€'
char3 = ' ' # Space character

print(f"Category of '{char1}': {unicodedata.category(char1)}")
print(f"Category of '{char2}': {unicodedata.category(char2)}")
print(f"Category of '{char3}': {unicodedata.category(char3)}")
```

--------------------------------

### HTTP Basic Authentication with Urllib

Source: https://docs.python.org/3/howto/urllib2

Demonstrates how to set up HTTP Basic Authentication using `HTTPBasicAuthHandler` and `build_opener` to handle requests with username and password.

```python
import urllib.request

top_level_url = "http://example.com/foo/"
username = "user"
password = "pass"

password_mgr = urllib.request.HTTPPasswordMgrWithDefaultRealm()
password_mgr.add_password(None, top_level_url, username, password)

handler = urllib.request.HTTPBasicAuthHandler(password_mgr)

# create "opener" (OpenerDirector instance)
opener = urllib.request.build_opener(handler)

# use the opener to fetch a URL
a_url = "http://example.com/protected"
# opener.open(a_url)

# Install the opener.
# Now all calls to urllib.request.urlopen use our opener.
urllib.request.install_opener(opener)
```

--------------------------------

### Invoke DTrace Script for Python Function Calls

Source: https://docs.python.org/3/howto/instrumentation

Example command to invoke a DTrace script that traces the call/return hierarchy of a Python script, focusing on functions named 'start'.

```bash
sudo"python3.6 script.py"
```

--------------------------------

### Install Pip if Not Installed

Source: https://docs.python.org/3/installing/index

Provides a command to ensure pip is installed, addressing scenarios where pip might not be included by default.

```bash
python -m ensurepip --upgrade
```

--------------------------------

### Python enumerate() Function

Source: https://docs.python.org/3/library/functions

The enumerate() function adds a counter to an iterable and returns it as an enumerate object. This can be used for example to get both the index and the value of an item.

```python
for i, item in enumerate(['a', 'b', 'c']):
    print(i, item)
```

--------------------------------

### Context Manager Examples and Recipes

Source: https://docs.python.org/3/library/contextlib

This part of the documentation provides practical examples and recipes for using context managers, demonstrating how to solve common programming problems. It includes patterns for supporting multiple context managers, catching exceptions, and using context managers as decorators.

```python
# Examples of using context managers for various scenarios
# e.g., replacing try-finally blocks, decorator usage
```

--------------------------------

### Python Turtle Basic Usage Example

Source: https://docs.python.org/3/library/turtle

A simple example demonstrating how to create a turtle, move it, and change its color.

```python
import turtle

# Create a screen object
screen = turtle.Screen()

# Create a turtle object
t = turtle.Turtle()

# Move the turtle
t.forward(100)

# Change the turtle's color
t.color("blue")

# Keep the window open until closed
screen.mainloop()
```

--------------------------------

### Python unicodedata.combining() Example

Source: https://docs.python.org/3/library/unicodedata

Shows how to use `unicodedata.combining()` to get the canonical combining class of a character. This value indicates how a character should be combined with preceding characters.

```python
import unicodedata

char_with_combining = 'é' # LATIN SMALL LETTER E WITH ACUTE (U+00E9)
char_base = 'e' # LATIN SMALL LETTER E (U+0065)
char_combining_mark = '\u0301' # COMBINING ACUTE ACCENT (U+0301)
char_no_combining = 'A'

# The precomposed character 'é' has a combining class of 0
print(f"Combining class of '{char_with_combining}': {unicodedata.combining(char_with_combining)}")
# The base character 'e' has a combining class of 0
print(f"Combining class of '{char_base}': {unicodedata.combining(char_base)}")
# The combining accent itself has a combining class of 230
print(f"Combining class of combining accent '{char_combining_mark}': {unicodedata.combining(char_combining_mark)}")
print(f"Combining class of '{char_no_combining}': {unicodedata.combining(char_no_combining)}")
```

--------------------------------

### Using the Object simulation with a derived class

Source: https://docs.python.org/3/howto/descriptor

This example shows how to inherit from the simulated `Object` class and define `slot_names` to create a class with slotted attributes. It demonstrates initialization and attribute assignment.

```python
class H(Object, metaclass=Type):
    'Instance variables stored in slots'

    slot_names = ['x', 'y']

    def __init__(self, x, y):
        self.x = x
        self.y = y
```

--------------------------------

### Python C API Initialization Configuration

Source: https://docs.python.org/3/contents

Details on configuring Python initialization, including examples, PyWideStringList, PyStatus, and PyPreConfig structures, and how to pre-initialize Python using PyPreConfig.

```APIDOC
APIDOC:
  Python Initialization Configuration:
    Example: A practical example of Python initialization configuration.
    PyWideStringList: Structure for managing wide strings during initialization.
    PyStatus: Structure for reporting initialization status.
    PyPreConfig: Structure for pre-configuring Python before full initialization.
    Preinitialize Python with PyPreConfig: Function to initialize Python using PyPreConfig.
```

--------------------------------

### site.PREFIXES Variable

Source: https://docs.python.org/3/genindex-P

A tuple containing the standard installation prefixes for Python.

```APIDOC
site.PREFIXES
  - A tuple of standard installation prefixes.
```

--------------------------------

### Import Turtle Module

Source: https://docs.python.org/3/library/turtle

Imports all objects from the turtle module to start using turtle graphics. Ensure the Tk interface package is installed if you encounter a 'No module named _tkinter' error.

```python
from turtle import *

```

--------------------------------

### Exploring Python Modules with dir() and help()

Source: https://docs.python.org/3/tutorial/stdlib

Shows how to use the built-in dir() and help() functions to inspect Python modules like 'os'. dir() lists module contents, while help() provides detailed documentation.

```python
import os
dir(os)
help(os)
```

--------------------------------

### Accessing instance attributes with the simulation

Source: https://docs.python.org/3/howto/descriptor

This example shows how instances created with the `Object` simulation store their attributes in a `_slotvalues` list. It demonstrates direct access and modification of slotted attributes.

```python
>>> h = H(10, 20)
>>> vars(h)
{'_slotvalues': [10, 20]}
>>> h.x = 55
>>> vars(h)
{'_slotvalues': [55, 20]}
```

--------------------------------

### Python Timer Example

Source: https://docs.python.org/3/library/threading

Demonstrates how to create and start a Timer object in Python to execute a function after a specified delay. The Timer class is a subclass of Thread.

```python
def hello():
    print("hello, world")

t = Timer(30.0, hello)
t.start()  # after 30 seconds, "hello, world" will be printed
```

--------------------------------

### Install IDLE on SUSE/OpenSUSE

Source: https://docs.python.org/3/using/unix

Installs the IDLE development environment for Python on SUSE and OpenSUSE systems.

```bash
sudo zypper install python3-idle
```

--------------------------------

### Get Multiprocessing Context

Source: https://docs.python.org/3/library/multiprocessing

Returns a context object that mirrors the attributes of the main multiprocessing module. This allows for managing different process start methods and configurations.

```python
import multiprocessing

context = multiprocessing.get_context('spawn') # or 'fork', 'forkserver'
```

--------------------------------

### Multi-Process Logging with QueueHandler and Listener

Source: https://docs.python.org/3/howto/logging-cookbook

Illustrates a pattern for logging from multiple processes to a single destination. It involves worker processes sending log records to a central listener process via a queue. This approach requires the `logging`, `logging.handlers`, and `multiprocessing` modules. The example outlines the setup for both listener and worker processes, emphasizing the need for separate logging configurations.

```python
# You'll need these imports in your own code
import logging
import logging.handlers
import multiprocessing

# Next two import lines for this demo only
from random import choice, random
import time

#
# Because you'll want to define the logging configurations for listener and workers, the
# listener and worker process functions take a configurer parameter which is a callable
# for configuring logging for that process. These functions are also passed the queue,
# which they use for communication.
#
# In practice, you can configure the listener however you want, but note that in this
# simple example, the listener does not apply level or filter logic to received records.
# In practice, you would probably want to do this logic in the worker processes, to avoid
# sending events which would be filtered out between processes.
#
```

--------------------------------

### Python Standard Library Modules Overview

Source: https://docs.python.org/3/tutorial/stdlib2

This section of the Python tutorial provides an overview of advanced standard library modules. It covers various aspects of professional programming, including output formatting, templating, working with binary data, multi-threading, logging, weak references, tools for lists, and decimal floating-point arithmetic.

```python
import sys

# Example of output formatting (not directly shown in text, but implied)
print(f"Value: {123.456:.2f}")

# Example of multi-threading (conceptual)
# import threading
# def worker():
#     pass
# t = threading.Thread(target=worker)
# t.start()

# Example of logging (conceptual)
# import logging
# logging.basicConfig(level=logging.INFO)
# logging.info('This is an informational message.')

# Example of weak references (conceptual)
# import weakref
# class MyObject:
#     pass
# obj = MyObject()
# wr = weakref.ref(obj)

# Example of tools for working with lists (conceptual)
# from collections import deque
# d = deque()

# Example of decimal arithmetic (conceptual)
# from decimal import Decimal
# d1 = Decimal('1.1')
# d2 = Decimal('2.2')
# print(d1 + d2)
```

--------------------------------

### Example: Process Creation and Start

Source: https://docs.python.org/3/library/multiprocessing

Demonstrates a common error when creating a multiprocessing.Process with a target function defined in the main REPL session. This leads to an AttributeError in the child process because the target is not importable.

```python
import multiprocessing as mp

def knigit():
    print("Ni!")

process = mp.Process(target=knigit)
process.start()
# This will likely result in an AttributeError in the child process
# Example error:
# Traceback (most recent call last):
#   File ".../multiprocessing/spawn.py", line ..., in spawn_main
#     ...
# AttributeError: module '__main__' has no attribute 'knigit'

print(process)
```

--------------------------------

### Python tempfile Module Examples

Source: https://docs.python.org/3/library/tempfile

Examples demonstrating the typical usage of the Python tempfile module for creating and managing temporary files and directories.

```python
import tempfile

# create a temporary file and write some data to it
fp = tempfile.TemporaryFile()
fp.write(b'Hello world!')
# read data from file
fp.seek(0)
fp.read()
# close the file, it will be removed
fp.close()

# create a temporary file using a context manager
with tempfile.TemporaryFile() as fp:
    fp.write(b'Hello world!')
    fp.seek(0)
    fp.read()
# file is now closed and removed

# create a temporary file using a context manager
# close the file, use the name to open the file again
with tempfile.NamedTemporaryFile(delete_on_close=False) as fp:
    fp.write(b'Hello world!')
    fp.close()
# the file is closed, but not removed
# open the file again by using its name
    with open(fp.name, mode='rb') as f:
        f.read()
# file is now removed

# create a temporary directory using the context manager
with tempfile.TemporaryDirectory() as tmpdirname:
    print('created temporary directory', tmpdirname)
# directory and contents have been removed

```

--------------------------------

### Example Usage of linecache.getline

Source: https://docs.python.org/3/library/linecache

Demonstrates how to use the `getline` function to retrieve a specific line from a file, using `linecache.__file__` to get the path to the linecache module itself.

```python
import linecache
linecache.getline(linecache.__file__, 8)
# Expected output: 'import sys\n'
```

--------------------------------

### Legacy API: Reading Configuration from a File

Source: https://docs.python.org/3/library/configparser

Provides an example of using the legacy API to read a configuration file that was previously written. It initializes a RawConfigParser and reads the 'example.cfg' file, demonstrating basic file reading capabilities.

```python
import configparser

config = configparser.RawConfigParser()
config.read('example.cfg')

# Example of accessing values (though the snippet focuses on reading)
# print(config.get('Section1', 'an_int'))
# print(config.get('Section1', 'foo'))

print("Configuration read from example.cfg")
```

--------------------------------

### unittest Basic Example

Source: https://docs.python.org/3/library/unittest

Demonstrates a fundamental usage of the unittest framework, showing how to define test cases and run them.

```python
import unittest

class MyTestCase(unittest.TestCase):
    def test_example(self):
        self.assertEqual(1 + 1, 2)

if __name__ == '__main__':
    unittest.main()
```

--------------------------------

### Python venv Environment Creation Example

Source: https://docs.python.org/3/library/venv

Demonstrates the basic usage of creating a virtual environment using the `EnvBuilder` class in Python. This involves instantiating the builder and calling its methods to set up the environment.

```python
from venv import EnvBuilder

# Create an EnvBuilder instance
builder = EnvBuilder(with_pip=True, clear=False)

# Create the virtual environment and get the context object
context = builder.create('/path/to/your/venv')

# The context object contains attributes like env_dir, executable, etc.
print(f"Virtual environment created at: {context.env_dir}")
print(f"Python executable: {context.executable}")
```

--------------------------------

### Python 3.13.7 Documentation Sections

Source: https://docs.python.org/3/.13

Provides links to various sections of the Python 3.13.7 documentation, including 'What's new', tutorials, library and language references, setup guides, HOWTOs, distribution, C API, FAQs, and deprecations.

```python
What's new in Python 3.13? (https://docs.python.org/3.13/whatsnew/3.13.html)
All "What's new" documents since Python 2.0 (https://docs.python.org/3.13/whatsnew/index.html)
Tutorial (https://docs.python.org/3.13/tutorial/index.html)
Library reference (https://docs.python.org/3.13/library/index.html)
Language reference (https://docs.python.org/3.13/reference/index.html)
Python setup and usage (https://docs.python.org/3.13/using/index.html)
Python HOWTOs (https://docs.python.org/3.13/howto/index.html)
Installing Python modules (https://docs.python.org/3.13/installing/index.html)
Distributing Python modules (https://docs.python.org/3.13/distributing/index.html)
Extending and embedding (https://docs.python.org/3.13/extending/index.html)
Python's C API (https://docs.python.org/3.13/c-api/index.html)
FAQs (https://docs.python.org/3.13/faq/index.html)
Deprecated functionality (https://docs.python.org/3.13/deprecations/index.html)
```

--------------------------------

### itertools.count() Examples

Source: https://docs.python.org/3/howto/functional

Demonstrates the itertools.count() function, which returns an infinite stream of evenly spaced values. It shows default behavior and usage with custom start and step values.

```python
import itertools

# Default count
print(list(itertools.islice(itertools.count(), 10)))

# Count starting from 10
print(list(itertools.islice(itertools.count(10), 10)))

# Count starting from 10 with a step of 5
print(list(itertools.islice(itertools.count(10, 5), 10)))
```

--------------------------------

### PEP 432 Documentation

Source: https://docs.python.org/3/genindex-P

References PEP 432, related to initialization configuration. It links to C API documentation and 'whatsnew' sections for Python 3.7 and changelog.

```python
https://docs.python.org/3/c-api/init_config.html#index-42
https://docs.python.org/3/c-api/init_config.html#index-43
https://docs.python.org/3/whatsnew/3.7.html#index-39
https://docs.python.org/3/whatsnew/changelog.html#index-358
```

--------------------------------

### Python optparse 'store' action example

Source: https://docs.python.org/3/library/optparse

Demonstrates the 'store' action for options that require arguments. It shows how to specify argument types, the number of arguments to consume (nargs), and the destination variable. The example illustrates parsing command-line arguments and the resulting option values.

```python
parser.add_option("-f")
parser.add_option("-p", type="float", nargs=3, dest="point")
```

--------------------------------

### Setup for Threading Tests

Source: https://docs.python.org/3/library/test

Returns the current thread count and a copy of any dangling threads. This is useful for establishing a baseline before starting new threads in a test.

```python
test.support.threading_helper.threading_setup()
```

--------------------------------

### Work with Multiple Python Versions (Windows)

Source: https://docs.python.org/3/installing/index

Shows how to use the `py` Python launcher with the `-m` switch to manage multiple Python versions on Windows.

```powershell
py -3.9 -m pip install <package>
py -3.10 -m pip install <package>
```

--------------------------------

### Control ensurepip installation location and scripts

Source: https://docs.python.org/3/library/ensurepip

Options to control where pip is installed and which scripts are created. --root specifies an alternative installation directory. --user installs to user site packages. --altinstall prevents the 'pipX' script from being installed. --default-pip installs the 'pip' script in addition to 'pipX' and 'pipX.Y'. Providing both --altinstall and --default-pip raises a ValueError.

```python
python -m ensurepip --root <dir>
python -m ensurepip --user
python -m ensurepip --altinstall
python -m ensurepip --default-pip
```

--------------------------------

### Example Usage of xml.parsers.expat

Source: https://docs.python.org/3/library/pyexpat

This snippet demonstrates a basic example of how to use the xml.parsers.expat module for parsing XML content. It shows the initialization of a parser and handling of parsing events, illustrating the fundamental usage pattern.

```python
import xml.parsers.expat

def start_element(name, attrs):
    print(f"Start element: {name}")

def end_element(name):
    print(f"End element: {name}")

def char_data(data):
    print(f"Character data: {data}")

parser = xml.parsers.expat.ParserCreate()
parser.StartElementHandler = start_element
parser.EndElementHandler = end_element
parser.CharacterDataHandler = char_data

xml_string = "<root><child>data</child></root>"
parser.Parse(xml_string)
```

--------------------------------

### Install SystemTap Development Tools (Alternative)

Source: https://docs.python.org/3/howto/instrumentation

Installs the necessary development tools for SystemTap on Linux systems using an alternative method, likely apt or similar.

```bash
$ sudo
```

--------------------------------

### EnvBuilder Core Methods

Source: https://docs.python.org/3/library/venv

These methods are part of the `EnvBuilder` class and are responsible for the core functionality of creating and setting up a Python virtual environment. They handle configuration file creation, Python executable setup, and script installation.

```APIDOC
EnvBuilder Methods:

create_configuration(_context_)
  Creates the pyvenv.cfg configuration file in the environment.

setup_python(_context_)
  Creates a copy or symlink to the Python executable in the environment. On POSIX systems, symlinks to 'python' and 'python3' are created if they don't exist.

setup_scripts(_context_)
  Installs activation scripts appropriate to the platform into the virtual environment.

post_setup(_context_)
  A placeholder method for third-party implementations to pre-install packages or perform other post-creation steps.
```

--------------------------------

### Get Arguments of a Generic Type

Source: https://docs.python.org/3/library/typing

Retrieves the type arguments of a generic type after performing all substitutions. For example, for Dict[str, int], it returns (str, int).

```python
typing.get_args(_tp_)

# Example:
from typing import Dict, Union, Literal

print(typing.get_args(Dict[str, int]))
# Output: (<class 'str'>, <class 'int'>)

print(typing.get_args(Union[int, str]))
# Output: (<class 'int'>, <class 'str'>)

print(typing.get_args(Literal["a", "b"]))
# Output: ('a', 'b')
```

--------------------------------

### ORM Model Definitions

Source: https://docs.python.org/3/howto/descriptor

Example model classes (Movie and Song) that utilize the Field descriptor to map database columns to class attributes. Each model specifies its table name and primary key.

```python
class Movie:
    table = 'Movies'                    # Table name
    key = 'title'                       # Primary key
    director = Field()
    year = Field()

    def __init__(self, key):
        self.key = key

class Song:
    table = 'Music'
    key = 'title'
    artist = Field()
    year = Field()
    genre = Field()

    def __init__(self, key):
        self.key = key
```

--------------------------------

### splitext Function Examples

Source: https://docs.python.org/3/library/os

Demonstrates the usage of the `splitext` function from the `os.path` module, which splits a pathname into a pair (root, ext). It shows how `splitext` handles filenames starting with periods and multiple periods.

```python
>>> import os
>>> os.path.splitext('.cshrc')
('.cshrc', '')
>>> os.path.splitext('/foo/....jpg')
('/foo/....jpg', '')
```

--------------------------------

### Get Path Suffixes

Source: https://docs.python.org/3/library/pathlib

Retrieves the list of suffixes for a given path. For example, '.tar.gz' will result in ['.tar', '.gz']. An empty list is returned if there are no suffixes.

```python
>>> PurePosixPath('my/library.tar.gz').suffixes
['.tar', '.gz']
>>> PurePosixPath('my/library').suffixes
[]
```

--------------------------------

### venv create() and create_configuration() Methods

Source: https://docs.python.org/3/genindex-C

Methods for creating virtual environments. create() builds the environment, and create_configuration() handles configuration details.

```python
import venv

# Using venv.create
venv.create('myenv', symlinks=True)

# Using venv.EnvBuilder
builder = venv.EnvBuilder('myenv')
builder.create()
builder.create_configuration('myconfig')
```

--------------------------------

### Python/C API Introduction

Source: https://docs.python.org/3/c-api/index

This introduction provides an overview of the Python/C API, explaining its purpose, fundamental concepts, and how it enables interoperability between Python and C/C++. It serves as a starting point for understanding how to extend Python's functionality.

```c
// Include the Python header file
#include <Python.h>

// Function to create a Python string from a C string
PyObject* py_string_from_cstring(const char* c_str) {
    return PyUnicode_FromString(c_str);
}
```

--------------------------------

### Running doctest with verbose output

Source: https://docs.python.org/3/library/doctest

Demonstrates how to run the doctest module with the `-v` flag to get a detailed log of test execution and a summary of results. This is useful for debugging and understanding test coverage.

```bash
$ python -v
Trying:
    factorial(5)
Expecting:
    120
ok
Trying:
    [factorial(n) for n in range(6)]
Expecting:
    [1, 1, 2, 6, 24, 120]
ok


```

--------------------------------

### Extend EnvBuilder for Package Installation

Source: https://docs.python.org/3/library/venv

This Python script demonstrates how to extend the `venv.EnvBuilder` class to automatically install setuptools and pip into a virtual environment after its creation. It includes methods for downloading scripts, managing subprocess output for progress reporting, and handling the installation process.

```python
import os
import os.path
from subprocess import Popen, PIPE
import sys
from threading import Thread
from urllib.parse import urlparse
from urllib.request import urlretrieve
import venv

class ExtendedEnvBuilder(venv.EnvBuilder):
    """
    This builder installs setuptools and pip so that you can pip or
    easy_install other packages into the created virtual environment.

    :param nodist: If true, setuptools and pip are not installed into the
                   created virtual environment.
    :param nopip: If true, pip is not installed into the created
                  virtual environment.
    :param progress: If setuptools or pip are installed, the progress of the
                     installation can be monitored by passing a progress
                     callable. If specified, it is called with two
                     arguments: a string indicating some progress, and a
                     context indicating where the string is coming from.
                     The context argument can have one of three values:
                     'main', indicating that it is called from virtualize() 
                     itself, and 'stdout' and 'stderr', which are obtained
                     by reading lines from the output streams of a subprocess
                     which is used to install the app.

                     If a callable is not specified, default progress
                     information is output to sys.stderr.
    """

    def __init__(self, *args, **kwargs):
        self.nodist = kwargs.pop('nodist', False)
        self.nopip = kwargs.pop('nopip', False)
        self.progress = kwargs.pop('progress', None)
        self.verbose = kwargs.pop('verbose', False)
        super().__init__(*args, **kwargs)

    def post_setup(self, context):
        """
        Set up any packages which need to be pre-installed into the
        virtual environment being created.

        :param context: The information for the virtual environment
                        creation request being processed.
        """
        os.environ['VIRTUAL_ENV'] = context.env_dir
        if not self.nodist:
            self.install_setuptools(context)
        # Can't install pip without setuptools
        if not self.nopip and not self.nodist:
            self.install_pip(context)

    def reader(self, stream, context):
        """
        Read lines from a subprocess' output stream and either pass to a progress
        callable (if specified) or write progress information to sys.stderr.
        """
        progress = self.progress
        while True:
            s = stream.readline()
            if not s:
                break
            if progress is not None:
                progress(s, context)
            else:
                if not self.verbose:
                    sys.stderr.write('.')
                else:
                    sys.stderr.write(s.decode('utf-8'))
                sys.stderr.flush()
        stream.close()

    def install_script(self, context, name, url):
        _, _, path, _, _, _ = urlparse(url)
        fn = os.path.split(path)[-1]
        binpath = context.bin_path
        distpath = os.path.join(binpath, fn)
        # Download script into the virtual environment's binaries folder
        urlretrieve(url, distpath)
        progress = self.progress
        if self.verbose:
            term = '\n'
        else:
            term = ''
        if progress is not None:
            progress('Installing %s ...%s' % (name, term), 'main')
        else:
            sys.stderr.write('Installing %s ...%s' % (name, term))
            sys.stderr.flush()
        # Install in the virtual environment
        args = [context.env_exe, fn]
        p = Popen(args, stdout=PIPE, stderr=PIPE, cwd=binpath)
        t1 = Thread(target=self.reader, args=(p.stdout, 'stdout'))
        t1.start()
        t2 = Thread(target=self.reader, args=(p.stderr, 'stderr'))
        t2.start()
        p.wait()
        t1.join()
        t2.join()
        if progress is not None:
            progress('done.', 'main')
        else:
            sys.stderr.write('done.\n')
        # Clean up - no longer needed
        os.unlink(distpath)

    def install_setuptools(self, context):
        """
        Install setuptools in the virtual environment.

        :param context: The information for the virtual environment
                        creation request being processed.
        """
        url = "https://bootstrap.pypa.io/ez_setup.py"
        self.install_script(context, 'setuptools', url)
        # clear up the setuptools archive which gets downloaded

```

--------------------------------

### Turtle Graphics Usage Scenarios

Source: https://docs.python.org/3/library/tk

This section provides practical examples of using the turtle module, including quick start methods, namespace management, integrating turtle graphics into scripts, and employing object-oriented approaches.

```python
# Using turtle graphics in a script
import turtle

turtle.forward(50)
turtle.left(90)
turtle.forward(50)

# Object-oriented turtle graphics
my_turtle = turtle.Turtle()
my_turtle.circle(50)
```

--------------------------------

### Python gettext Catalog Constructor Usage

Source: https://docs.python.org/3/library/gettext

Demonstrates how to use the gettext.Catalog constructor to create a translation catalog and retrieve translated strings. This example shows the basic setup for internationalization in Python.

```python
import gettext
cat = gettext.Catalog(domain, localedir)
_ = cat.gettext
print(_('hello world'))
```

--------------------------------

### Python unicodedata.name() Example

Source: https://docs.python.org/3/library/unicodedata

Shows how to use the `unicodedata.name()` function to get the official Unicode name of a character. It also demonstrates handling cases where a character might not have a defined name.

```python
import unicodedata

char_with_name = 'é'
char_without_name = '\u0001'

print(f"Name of '{char_with_name}': {unicodedata.name(char_with_name)}")

try:
    print(f"Name of '{char_without_name}': {unicodedata.name(char_without_name)}")
except ValueError as e:
    print(f"Error getting name for '{char_without_name}': {e}")

# Using default value
print(f"Name of '{char_without_name}' (default): {unicodedata.name(char_without_name, 'N/A')}")
```

--------------------------------

### Python TimedRotatingFileHandler Example

Source: https://docs.python.org/3/library/logging

A basic example demonstrating how to instantiate and use the TimedRotatingFileHandler in Python for logging. This example sets up hourly log rotation with a backup count.

```python
import logging
import logging.handlers

# Create logger
logger = logging.getLogger('my_app')
logger.setLevel(logging.INFO)

# Create handler
# Rotate log file every hour, keep 5 backup files
handler = logging.handlers.TimedRotatingFileHandler(
    'app.log', when='H', interval=1, backupCount=5
)

# Create formatter and add it to the handler
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
handler.setFormatter(formatter)

# Add the handler to the logger
logger.addHandler(handler)

# Log some messages
logger.info('This is an info message.')
logger.warning('This is a warning message.')
```

--------------------------------

### Python Locale Management Example

Source: https://docs.python.org/3/library/locale

Demonstrates how to get, set, and restore locale settings in Python. It shows comparing strings using `locale.strcoll` and switching between different locale configurations.

```python
import locale
loc = locale.getlocale()  # get current locale
# use German locale; name might vary with platform
locale.setlocale(locale.LC_ALL, 'de_DE')
locale.strcoll('f\xe4n', 'foo')  # compare a string containing an umlaut
locale.setlocale(locale.LC_ALL, '')   # use user's preferred locale
locale.setlocale(locale.LC_ALL, 'C')  # use default (C) locale
locale.setlocale(locale.LC_ALL, loc)  # restore saved locale
```

--------------------------------

### FTP Request Example

Source: https://docs.python.org/3/howto/urllib2

Demonstrates creating a Request object for an FTP URL.

```python
req = urllib.request.Request('ftp://example.com/')
```

--------------------------------

### Setup.py for Custom Python Modules

Source: https://docs.python.org/3/extending/newtypes_tutorial

Configures the `setup.py` file to build and package custom Python extension modules. It specifies the module name and the source C files. This example shows how to include both 'custom' and 'custom2' modules.

```python
from setuptools import Extension, setup

setup(
    ext_modules=[
        Extension("custom", ["custom.c"]),
        Extension("custom2", ["custom2.c"]),
    ]
)
```

--------------------------------

### Doctest Directive Syntax

Source: https://docs.python.org/3/library/doctest

Defines the grammar for doctest directives, including their structure and allowed options. Directives are Python comments starting with '# doctest:' followed by option flags.

```APIDOC
directive ::= "#" "doctest:" [directive_options]
directive_options ::= directive_option ("," directive_option)*
directive_option ::= on_or_off directive_option_name
on_or_off ::= "+" | "-"
directive_option_name ::= "DONT_ACCEPT_BLANKLINE" | "NORMALIZE_WHITESPACE" | ...

```

--------------------------------

### Get HTTP Headers using asyncio Streams

Source: https://docs.python.org/3/library/asyncio-stream

Illustrates how to retrieve HTTP headers from a web server using asyncio streams. This example demonstrates making an HTTP request and parsing the response headers.

```python
import asyncio

async def get_http_headers(host, port, path='/'):
    reader, writer = await asyncio.open_connection(host, port)

    request = f'GET {path} HTTP/1.1\r\nHost: {host}\r\nConnection: close\r\n\r\n'
    writer.write(request.encode())
    await writer.drain()

    response_header = b''
    while True:
        data = await reader.read(100)
        if not data:
            break
        response_header += data
        if b'\r\n\r\n' in response_header:
            break

    writer.close()
    await writer.wait_closed()

    headers_str = response_header.decode()
    print(headers_str)

if __name__ == '__main__':
    host = 'www.python.org'
    port = 80
    path = '/'
    asyncio.run(get_http_headers(host, port, path))

```

--------------------------------

### Python Dictionary Creation Examples

Source: https://docs.python.org/3/library/stdtypes

Demonstrates multiple ways to create Python dictionaries, including using key-value pairs, dictionary comprehensions, and the dict() constructor with various inputs.

```python
dict()

dict([('foo', 100), ('bar', 200)])

dic(foo=100, bar=200)

{'jack': 4098, 'sjoerd': 4127}

{x: x ** 2 for x in range(10)}
```

--------------------------------

### Python Multiprocessing Start Methods

Source: https://docs.python.org/3/genindex-G

Retrieves all available start methods for multiprocessing.

```APIDOC
multiprocessing.get_all_start_methods()
  Return a list of all valid start methods for this platform.
```

--------------------------------

### ExitStack Example Usage

Source: https://docs.python.org/3/library/contextlib

An example demonstrating how to use ExitStack to manage multiple file openings as an 'all or nothing' operation. It shows how to defer closing files until explicitly requested.

```python
with ExitStack() as stack:
    files = [stack.enter_context(open(fname)) for fname in filenames]
    # Hold onto the close method, but don't call it yet.
    close_files = stack.pop_all().close
    # If opening any file fails, all previously opened files will be
    # closed automatically. If all files are opened successfully,
    # they will remain open even after the with statement ends.
    # close_files() can then be invoked explicitly to close them all.
```

--------------------------------

### Python String Slicing Examples

Source: https://docs.python.org/3/tutorial/introduction

Demonstrates various ways to slice strings in Python, including accessing characters from the beginning, end, and specific ranges. It highlights that the start index is inclusive and the end index is exclusive.

```python
word = "Python"
>>> word[:2]   # character from the beginning to position 2 (excluded)
'Py'
>>> word[4:]   # characters from position 4 (included) to the end
'on'
>>> word[-2:]  # characters from the second-last (included) to the end
'on'
```

```python
word = "Python"
>>> word[:2] + word[2:]
'Python'
>>> word[:4] + word[4:]
'Python'
```

--------------------------------

### Get Origin of a Generic Type

Source: https://docs.python.org/3/library/typing

Returns the unsubscripted version of a type. For example, for Dict[str, int], it returns dict. It also normalizes typing aliases and handles ParamSpec.

```python
typing.get_origin(_tp_)

# Example:
from typing import Dict, Annotated
from typing import ParamSpec

print(typing.get_origin(Dict[str, int]))
# Output: <class 'dict'>

print(typing.get_origin(Annotated[str, "metadata"]))
# Output: typing.Annotated

P = ParamSpec('P')
print(typing.get_origin(P.args))
# Output: P
```

--------------------------------

### Python 3.4.10 Documentation Structure

Source: https://docs.python.org/3/.4

This snippet outlines the main sections and resources available in the Python 3.4.10 documentation. It includes links to specific topics such as the tutorial, library reference, language reference, and installation guides.

```python
# Python 3.4.10 documentation
# Welcome! This is the documentation for Python 3.4.10, last updated Jun 16, 2019.

# Parts of the documentation:
# What's new in Python 3.4?
# or all "What's new" documents since 2.0
# Tutorial
# Library Reference
# Language Reference
# Python Setup and Usage
# Python HOWTOs
# Installing Python Modules
# Distributing Python Modules
# Extending and Embedding
# Python/C API
# FAQs

# Indices and tables:
# Global Module Index
# General Index
# Glossary
# Search page
# Complete Table of Contents

# Meta information:
# Reporting bugs
# About the documentation
# History and License of Python
# Copyright

# Download:
# Download these documents

# Docs for other versions:
# Python 2.7 (stable)
# Python 3.6 (stable)
# Python 3.7 (in development)
# Old versions

# Other resources:
# PEP Index
# Beginner's Guide
# Book List
# Audio/Visual Talks

# Quick search:
# Enter search terms or a module, class or function name.
```

--------------------------------

### Example Usage of PyStatus

Source: https://docs.python.org/3/c-api/init_config

Demonstrates how to use the PyStatus functions within a C code snippet. It shows creating a status, checking for exceptions, and handling errors or exits appropriately.

```c
PyStatusalloc(void**ptr,size_tsize)
{
  *ptr=PyMem_RawMalloc(size);
  if(*ptr==NULL){
    returnPyStatus_NoMemory();
  }
  returnPyStatus_Ok();
}

intmain(intargc,char**argv)
{
  void*ptr;
  PyStatusstatus=alloc(&ptr,16);
  if(PyStatus_Exception(status)){
    Py_ExitStatusException(status);
  }
  PyMem_Free(ptr);
  return0;
}
```

--------------------------------

### Python Installation Options

Source: https://docs.python.org/3/using/configure

Options to control the installation directory and behavior of Python modules during the build process. This includes specifying installation prefixes and managing test modules and pip.

```APIDOC
--prefix=PREFIX
  Description: Install architecture-independent files in PREFIX.
  Default on Unix: /usr/local.
  Runtime retrieval: sys.prefix.
  Example: --prefix="$HOME/.local/"

--exec-prefix=EPREFIX
  Description: Install architecture-dependent files in EPREFIX.
  Default: --prefix.
  Runtime retrieval: sys.exec_prefix.

--disable-test-modules
  Description: Do not build nor install test modules (e.g., test package, _testcapi extension).
  Default: Build and install test modules.
  Added in version: 3.10.

--with-ensurepip=[upgrade|install|no]
  Description: Select the ensurepip command run on Python installation.
  Options:
    upgrade: run python -m ensurepip --altinstall --upgrade (default).
    install: run python -m ensurepip --altinstall.
    no: do not run ensurepip.
  Added in version: 3.6.
```

--------------------------------

### Python String format() - Formatted Output

Source: https://docs.python.org/3/tutorial/inputoutput

Provides an example of using str.format() with field width and alignment specifiers to create neatly formatted columns of numbers.

```python
for x in range(1, 11):
    print('{0:2d}{1:3d}{2:4d}'.format(x, x*x, x*x*x))

```

--------------------------------

### Using @property Decorator for Recalculation

Source: https://docs.python.org/3/howto/descriptor

An example of using the @property decorator to wrap attribute access, enabling method calls (like recalculation) upon access without altering client code.

```python
class Cell:
    ...

    @property
    def value(self):
        """Recalculate the cell before returning value"""
        self.recalc()
        return self._value
```

--------------------------------

### Instantiating Custom LoggerAdapter

Source: https://docs.python.org/3/howto/logging-cookbook

Shows how to instantiate the custom LoggerAdapter with a logger and contextual information.

```python
logger = logging.getLogger(__name__)
adapter = CustomAdapter(logger, {'connid': some_conn_id})
```

--------------------------------

### Using a Context Manager as a Function Decorator

Source: https://docs.python.org/3/library/contextlib

This example demonstrates how to leverage contextlib to use a context manager as a decorator for functions. This allows the setup and teardown logic of the context manager to be applied automatically to function calls.

```python
from contextlib import contextmanager

@contextmanager
def timer():
    import time
    start_time = time.time()
    yield
    end_time = time.time()
    print(f"Function took {end_time - start_time:.4f} seconds")

@timer
def slow_function():
    import time
    time.sleep(1)

slow_function()

```

--------------------------------

### Sending Email with smtplib

Source: https://docs.python.org/3/faq/library

Provides a basic example of sending email using Python's smtplib module. It shows how to get sender and recipient addresses, read the message body from standard input, and send the email.

```python
import sys, smtplib

fromaddr = input("From: ")
tow = input("To: ").split(',')
print("Enter message, end with ^D:")
msg = ''
while True:
    line = sys.stdin.readline()
    if not line:
        break
    msg += line

# Example of sending (requires a running SMTP server)
# server = smtplib.SMTP('localhost')
# server.sendmail(fromaddr, tow, msg)
# server.quit()
```

--------------------------------

### Install Specific Package Version

Source: https://docs.python.org/3/installing/index

Installs a specific or minimum version of a package. Package name and version should be enclosed in double quotes if using comparator operators.

```bash
pip install "package-name>=1.0.4"
```

```bash
pip install "package-name<2.0"
```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/.9

Links to essential Python resources beyond version-specific documentation. This includes the Python Enhancement Proposals (PEP) index, beginner guides, book recommendations, audio/visual talks, and the Python Developer's Guide.

```python
print("PEP Index: https://peps.python.org/")
print("Beginner's Guide: https://wiki.python.org/moin/BeginnersGuide")
print("Book List: https://wiki.python.org/moin/PythonBooks")
print("Audio/Visual Talks: https://www.python.org/doc/av/")
print("Python Developer’s Guide: https://devguide.python.org/")
```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/library/fpectl

Lists essential external resources for Python developers, including the Python Enhancement Proposal (PEP) index, guides for beginners, book recommendations, audio/visual talks, and the Python Developer's Guide.

```markdown
* [PEP Index](https://peps.python.org/)
* [Beginner's Guide](https://wiki.python.org/moin/BeginnersGuide)
* [Book List](https://wiki.python.org/moin/PythonBooks)
* [Audio/Visual Talks](https://www.python.org/doc/av/)
* [Python Developer’s Guide](https://devguide.python.org/)
```

--------------------------------

### Python 3.3.7 Documentation Structure

Source: https://docs.python.org/3/.3

This snippet outlines the main sections and resources available within the Python 3.3.7 documentation. It covers core areas like tutorials, references, and installation guides, as well as supplementary materials.

```python
# Main Sections:
# - What's new in Python 3.3?
# - Tutorial
# - Library Reference
# - Language Reference
# - Python Setup and Usage
# - Python HOWTOs
# - Extending and Embedding
# - Python/C API
# - Installing Python Modules
# - Distributing Python Modules
# - FAQs

# Indices and tables:
# - Global Module Index
# - General Index
# - Glossary
# - Search page
# - Complete Table of Contents

# Meta information:
# - Reporting bugs
# - About the documentation
# - History and License of Python
# - Copyright

# Download and Other Versions:
# - Download these documents
# - Docs for other versions (Python 2.7, 3.4, Old versions)

# Other resources:
# - PEP Index
# - Beginner's Guide
# - Book List
# - Audio/Visual Talks
```

--------------------------------

### Python Multiprocessing Start Methods

Source: https://docs.python.org/3/library/concurrency

Explains the different methods for starting new processes in Python's multiprocessing module, including 'fork', 'spawn', and 'forkserver'. It details their implications for process creation and resource management.

```python
import multiprocessing

# Get all available start methods
print(multiprocessing.get_all_start_methods())

# Set the start method
multiprocessing.set_start_method('spawn')

# Get the current start method
print(multiprocessing.get_start_method())
```

--------------------------------

### Python Launcher for Windows Commands

Source: https://docs.python.org/3/using/windows

Demonstrates how to use the Python launcher to execute specific Python versions from the command line.

```cmd
py

```

```cmd
py -3.7

```

```cmd
py -2

```

```cmd
py --list

```

```cmd
py -V:Company/Tag

```

```cmd
py -3

```

```cmd
py -V:3

```

--------------------------------

### Python Thread Native ID

Source: https://docs.python.org/3/library/threading

Gets the OS-assigned Thread ID (TID) for a thread. This is a non-negative integer or None if the thread hasn't started. It can be used for system-wide identification until the thread terminates.

```python
import threading

thread = threading.Thread()
# thread.native_id is available after thread.start()
# print(f"Native Thread ID: {thread.native_id}")
```

--------------------------------

### Python Package __main__.py Example

Source: https://docs.python.org/3/library/__main__

Illustrates a typical __main__.py file for a Python package, showing how to handle command-line arguments and perform actions like searching for data using relative imports.

```python
# bandclass/__main__.py

import sys
from.studentimport search_students

student_name = sys.argv[1] if len(sys.argv) >= 2 else ''
print(f'Found student: {search_students(student_name)}')
```

--------------------------------

### Python Application Deployment Options

Source: https://docs.python.org/3/using/windows

Discusses two primary methods for deploying Python applications on Windows: using a specialized executable launcher for a transparent user experience, and using batch files or shortcuts for a simpler approach. The former allows for custom icons and file associations, while the latter is simpler but less transparent.

```windows
Custom Launcher:
  - Calls Py_Main with a hard-coded command line.
  - Allows customization of icons, company info, and file associations.
  - Provides a transparent user experience.

Batch File/Shortcut:
  - Directly calls python.exe or pythonw.exe.
  - Application appears as 'Python', not its actual name.
  - Simpler to implement but less transparent.
```

--------------------------------

### Create and Bind Server Socket

Source: https://docs.python.org/3/howto/sockets

Illustrates the creation of a server socket, binding it to a host and port, and setting it up to listen for incoming connections. This is the fundamental setup for a server application.

```python
import socket

# create an INET, STREAMing socket
serversocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
# bind the socket to a public host, and a well-known port
serversocket.bind((socket.gethostname(), 80))
# become a server socket
serversocket.listen(5)
```

--------------------------------

### Basic timeit Python Interface Usage

Source: https://docs.python.org/3/library/timeit

Shows how to use the timeit.timeit() function programmatically to measure the execution time of Python code snippets. Includes examples with setup statements.

```python
import timeit
timeit.timeit('char in text', setup='text = "sample string"; char = "g"')
0.41440500499993504
timeit.timeit('text.find(char)', setup='text = "sample string"; char = "g"')
1.7246671520006203
```

--------------------------------

### Basic Logging Example

Source: https://docs.python.org/3/howto/logging

A simple example demonstrating the fundamental usage of Python's logging module. It shows how to log messages at different levels.

```python
import logging

logging.warning('This is a warning message')
logging.error('This is an error message')
logging.critical('This is a critical message')
```

--------------------------------

### Install IDLE on Debian/Ubuntu

Source: https://docs.python.org/3/using/unix

Installs the IDLE development environment for Python on Debian-based systems.

```bash
sudo apt-get install idle
```

--------------------------------

### Python Future Example

Source: https://docs.python.org/3/library/asyncio-future

A basic example demonstrating how to use an asyncio Future to set a result and check its status.

```python
import asyncio

async def main():
    loop = asyncio.get_running_loop()
    fut = loop.create_future()

    # Set a result after some delay (simulated)
    loop.call_later(1, fut.set_result, "Operation Complete")

    print(f"Future done before await? {fut.done()}")
    result = await fut
    print(f"Future done after await? {fut.done()}")
    print(f"Result: {result}")

asyncio.run(main())
```

--------------------------------

### TopologicalSorter Static Order Example

Source: https://docs.python.org/3/library/graphlib

Demonstrates how to use the static_order method of the TopologicalSorter class to get a topological sort of a graph. The graph is represented as a dictionary where keys are nodes and values are sets of their predecessors.

```python
graph = {"D": {"B", "C"}, "C": {"A"}, "B": {"A"}}
ts = TopologicalSorter(graph)
tuple(ts.static_order())
```

--------------------------------

### Install IDLE on Alpine Linux

Source: https://docs.python.org/3/using/unix

Installs the IDLE development environment for Python on Alpine Linux systems.

```bash
sudo apk add python3-idle
```

--------------------------------

### Python 3.1.5 Documentation Structure

Source: https://docs.python.org/3/.1

Overview of the Python 3.1.5 documentation, including sections on new features, tutorials, library and language references, setup, HOWTOs, extending and embedding, Python/C API, installation, distribution, and documentation guidelines.

```APIDOC
Python v3.1.5 documentation:
  - What's new in Python 3.1?
  - Tutorial
  - Library Reference
  - Language Reference
  - Python Setup and Usage
  - Python HOWTOs
  - Extending and Embedding
  - Python/C API
  - Installing Python Modules
  - Distributing Python Modules
  - Documenting Python
  - FAQs
  - Indices and tables (Global Module Index, General Index, Glossary, Search page, Complete Table of Contents)
  - Meta information (Reporting bugs, About the documentation, History and License, Copyright)
  - Download
  - Docs for other versions (Python 2.7, Python 3.2, Old versions)
  - Other resources (FAQs, Guido's Essays, New-style Classes, PEP Index, Beginner's Guide, Book List, Audio/Visual Talks, Other Doc Collections, Report a Bug)
```

--------------------------------

### Python Installation Path Schemes

Source: https://docs.python.org/3/library/sysconfig

Describes the various installation path schemes used by Python across different platforms (POSIX, Windows, macOS) and installation types (default, home, user, virtual environment). These schemes dictate where Python components and packages are installed.

```APIDOC
Python Installation Path Schemes:

POSIX Schemes:
  - posix_prefix: Default scheme for POSIX platforms (Linux, macOS).
  - posix_home: Scheme for POSIX platforms using a specific home prefix.
  - posix_user: Scheme for POSIX platforms, paths under user's home directory.
  - posix_venv: Scheme for virtual environments on POSIX platforms.

Windows Schemes:
  - nt: Default scheme for Windows.
  - nt_user: Scheme for Windows, paths under user's home directory.
  - nt_venv: Scheme for virtual environments on Windows.

Other Schemes:
  - venv: Platform-dependent scheme for virtual environments (posix_venv or nt_venv).
  - osx_framework_user: Scheme for macOS, paths under user's home directory.

Path Identifiers within Schemes:
  - stdlib: Standard Python library files (non-platform-specific).
  - platstdlib: Standard Python library files (platform-specific).
  - platlib: Site-specific, platform-specific files.
  - purelib: Site-specific, non-platform-specific files.
  - include: Non-platform-specific C-API header files.
  - platinclude: Platform-specific C-API header files.
  - scripts: Script files directory.
  - data: Data files directory.
```

--------------------------------

### Calculate Total Seconds in a Timedelta

Source: https://docs.python.org/3/library/datetime

Demonstrates how to use the `total_seconds()` method to get the total duration of a timedelta object in seconds. It also shows an example of timedelta normalization and comparison.

```python
from datetime import timedelta
year = timedelta(days=365)
another_year = timedelta(weeks=40, days=84, hours=23,
                         minutes=50, seconds=600)
print(year == another_year)
print(year.total_seconds())
```

--------------------------------

### Topological Sort Example

Source: https://docs.python.org/3/library/graphlib

Demonstrates a typical workflow for using TopologicalSorter to process nodes in a task queue. It shows how to add nodes, prepare the graph, get ready nodes, put them into a task queue, and mark them as done.

```python
import graphlib

topological_sorter = graphlib.TopologicalSorter()
task_queue = queue.Queue()
finalized_tasks_queue = queue.Queue()

topological_sorter.prepare()
while topological_sorter.is_active():
    for node in topological_sorter.get_ready():
        task_queue.put(node)

    node = finalized_tasks_queue.get()
topological_sorter.done(node)
```

--------------------------------

### Simple WSGI Application and Server

Source: https://docs.python.org/3/library/wsgiref

Demonstrates a basic WSGI application that prints environment details and a simple HTTP server using wsgiref.simple_server. It utilizes setup_testing_defaults to populate the WSGI environment.

```python
fromwsgiref.utilimport setup_testing_defaults
fromwsgiref.simple_serverimport make_server

# A relatively simple WSGI application. It's going to print out the
# environment dictionary after being updated by setup_testing_defaults
defsimple_app(environ, start_response):
    setup_testing_defaults(environ)

    status = '200 OK'
    headers = [('Content-type', 'text/plain; charset=utf-8')]

    start_response(status, headers)

    ret = [("%s: %s\n" % (key, value)).encode("utf-8")
           for key, value in environ.items()]
    return ret

with make_server('', 8000, simple_app) as httpd:
    print("Serving on port 8000...")
    httpd.serve_forever()

```

--------------------------------

### Install pip using ensurepip CLI

Source: https://docs.python.org/3/library/ensurepip

Installs or upgrades pip in the current Python environment. Use --upgrade to ensure the latest version is installed. By default, pip is installed in the active virtual environment or system site packages.

```python
python -m ensurepip
python -m ensurepip --upgrade
```

--------------------------------

### Asyncio Queue Workload Distribution Example

Source: https://docs.python.org/3/library/asyncio-queue

Demonstrates how to use asyncio queues to distribute workload among concurrent worker tasks. It includes creating a queue, populating it with work items, starting worker tasks, and waiting for the queue to be fully processed.

```python
import asyncio
import random
import time


async def worker(name, queue):
    while True:
        # Get a "work item" out of the queue.
        sleep_for = await queue.get()

        # Sleep for the "sleep_for" seconds.
        await asyncio.sleep(sleep_for)

        # Notify the queue that the "work item" has been processed.
        queue.task_done()

        print(f'{name} has slept for {sleep_for:.2f} seconds')


async def main():
    # Create a queue that we will use to store our "workload".
    queue = asyncio.Queue()

    # Generate random timings and put them into the queue.
    total_sleep_time = 0
    for _ in range(20):
        sleep_for = random.uniform(0.05, 1.0)
        total_sleep_time += sleep_for
        queue.put_nowait(sleep_for)

    # Create three worker tasks to process the queue concurrently.
    tasks = []
    for i in range(3):
        task = asyncio.create_task(worker(f'worker-{i}', queue))
        tasks.append(task)

    # Wait until the queue is fully processed.
    started_at = time.monotonic()
    await queue.join()
    total_slept_for = time.monotonic() - started_at

    # Cancel our worker tasks.
    for task in tasks:
        task.cancel()
    # Wait until all worker tasks are cancelled.
    await asyncio.gather(*tasks, return_exceptions=True)

    print('====')
    print(f'3 workers slept in parallel for {total_slept_for:.2f} seconds')
    print(f'total expected sleep time: {total_sleep_time:.2f} seconds')


asyncio.run(main())

```

--------------------------------

### Asyncio Server API Documentation

Source: https://docs.python.org/3/library/asyncio-eventloop

Provides a comprehensive reference for the asyncio Server class methods, detailing their functionality, parameters, return values, and usage examples. This includes methods for closing connections, starting and stopping serving, and checking server status.

```APIDOC
Server:
  close():
    Stops serving connections by closing listening sockets. Existing client connections are left open. Use wait_closed() to wait for completion.
    Changed in version 3.7: Server object is an asynchronous context manager.
    Changed in version 3.11: Exposed publicly as asyncio.Server.

  close_clients():
    Closes all existing incoming client connections by calling close() on their transports. Should be called after close() to avoid race conditions.
    Added in version 3.13.

  abort_clients():
    Closes all existing incoming client connections immediately without waiting for pending operations. Calls abort() on transports. Should be called after close() to avoid race conditions.
    Added in version 3.13.

  get_loop():
    Returns the event loop associated with the server.
    Added in version 3.7.

  start_serving():
    Starts accepting connections. Idempotent; can be called when the server is already serving. Used when a server is created without accepting connections initially.
    Added in version 3.7.

  serve_forever():
    Starts accepting connections until the coroutine is cancelled. Cancellation closes the server. Can be called if the server is already accepting connections. Only one serve_forever task per server.
    Example:
    async def client_connected(reader, writer):
        await reader.readline()

    async def main(host, port):
        srv = await asyncio.start_server(client_connected, host, port)
        await srv.serve_forever()

    asyncio.run(main('127.0.0.1', 0))
    Added in version 3.7.

  is_serving():
    Returns True if the server is accepting new connections, False otherwise.
    Added in version 3.7.

  wait_closed():
    Waits until the close() method completes and all active connections have finished.
```

--------------------------------

### Python Initialization Configuration Options

Source: https://docs.python.org/3/c-api/init_config

Details various configuration options for Python initialization, including user site directory, verbose mode, warning options, bytecode writing, and extended options.

```APIDOC
PyConfig.user_site_directory:
  Type: int
  Description: If non-zero, add the user site directory to sys.path. If zero, it is not added. Set to 0 by -s and -I command line options, and PYTHONNOUSERSITE environment variable. Default: 1 in Python mode, 0 in isolated mode.

PyConfig.verbose:
  Type: int
  Description: Verbose mode. If greater than 0, print a message each time a module is imported. If greater than or equal to 2, print messages for each file checked during module search and information on module cleanup. Incremented by the -v command line option. Set by PYTHONVERBOSE environment variable. Default: 0.

PyConfig.warnoptions:
  Type: PyWideStringList
  Description: Options for the warnings module to build warnings filters. The last item in this list becomes the first item in warnings.filters (highest priority). Added to by the -W command line option (can be used multiple times) and PYTHONWARNINGS environment variable (comma-separated).
  Default: empty list.

PyConfig.write_bytecode:
  Type: int
  Description: If 0, Python won't try to write .pyc files on import. Set to 0 by -B command line option and PYTHONDONTWRITEBYTECODE environment variable. sys.dont_write_bytecode is initialized to the inverted value of this setting. Default: 1.

PyConfig.xoptions:
  Type: PyWideStringList
  Description: Values of the -X command line options, equivalent to sys._xoptions. If parse_argv is non-zero, arguments are parsed as regular Python command line arguments, and Python arguments are stripped from argv. Default: empty list.
  Note: The show_alloc_count field was removed in version 3.9.
```

--------------------------------

### ensurepip Module API

Source: https://docs.python.org/3/library/ensurepip

Programmatic interface for ensurepip. `version()` returns the available pip version. `bootstrap()` installs pip with various configuration options.

```APIDOC
ensurepip.version()
  Returns a string specifying the available version of pip that will be installed.

ensurepip.bootstrap(_root=None, _upgrade=False, _user=False, _altinstall=False, _default_pip=False, _verbosity=0)
  Bootstraps pip into the current or designated environment.
  Parameters:
    _root (str, optional): Alternative root directory for installation. Defaults to None.
    _upgrade (bool, optional): Whether to upgrade an existing pip installation. Defaults to False.
    _user (bool, optional): Whether to install into user site packages. Defaults to False.
    _altinstall (bool, optional): If True, the 'pipX' script will not be installed. Defaults to False.
    _default_pip (bool, optional): If True, the 'pip' script will be installed in addition to regular scripts. Defaults to False.
    _verbosity (int, optional): Controls the level of output to sys.stdout. Defaults to 0.
  Raises:
    ValueError: If both _altinstall and _default_pip are set to True.
  Auditing:
    Emits an auditing event 'ensurepip.bootstrap' with argument 'root'.
```

--------------------------------

### Python sysconfig Module Functions

Source: https://docs.python.org/3/library/sysconfig

This section outlines key functions within the sysconfig module that can be programmatically called in Python to retrieve configuration details. These include getting the platform, Python version, installation paths, and configuration variables.

```APIDOC
sysconfig.get_platform()
  - Returns the current platform tag.

sysconfig.get_python_version()
  - Returns the Python version as a string (e.g., '3.2').

sysconfig.get_path(scheme, vars=None, expand=True)
  - Returns an installation path for a given scheme and optional variables.
  - Parameters:
    - scheme: The installation scheme (e.g., 'posix_prefix', 'nt').
    - vars: A dictionary of configuration variables to use for expansion.
    - expand: Whether to expand environment variables in the path.
  - Returns: The installation path string.

sysconfig.get_config_vars(*names)
  - Returns configuration variables. If no names are given, all variables are returned as a dictionary.
  - Parameters:
    - names: Variable names to retrieve.
  - Returns: A string or dictionary of configuration variables.
```

--------------------------------

### Using Proxies

Source: https://docs.python.org/3/howto/urllib2

Explains how to configure and use proxy servers for making requests through a proxy.

```python
import urllib.request

url = 'http://example.com'
proxy_handler = urllib.request.ProxyHandler({'http': 'http://proxy.example.com:8080'})
opener = urllib.request.build_opener(proxy_handler)

with opener.open(url) as response:
    print(response.read().decode('utf-8'))
```

--------------------------------

### Installing Python Modules: Pip Not Installed

Source: https://docs.python.org/3/contents

Troubleshooting steps for situations where `pip` is not installed or not found in the system's PATH. This is a common hurdle for new Python users.

```APIDOC
Pip not installed:
  Addresses the scenario where pip is missing or inaccessible.
  Offers solutions for installing or making pip available in the environment.
```

--------------------------------

### Creating Executables from Python Scripts

Source: https://docs.python.org/3/contents

Guides on packaging Python scripts into standalone executable files (e.g., using PyInstaller or cx_Freeze) for distribution on Windows.

```bash
# Using PyInstaller:
# pyinstaller your_script.py

```

--------------------------------

### Custom OpenSSL Configuration and Build

Source: https://docs.python.org/3/using/unix

This section details the process of building Python with a custom OpenSSL installation. It covers finding OpenSSL configuration, downloading, building, and installing OpenSSL, and then configuring Python with specific flags.

```bash
# Find OpenSSL configuration
$ find /etc/ssl

# Download, build, and install OpenSSL
$ curl
$ tar
$ pushd
$ ./config --prefix=/usr/local/custom-openssl \
  --libdir=lib \
  --openssldir=/etc/ssl
$ make
$ make install_sw
$ popd

# Build Python with custom OpenSSL
$ pushd
$ ./configure --with-openssl=/usr/local/custom-openssl \
  --with-openssl-rpath=auto \
  --prefix=/usr/local/python-3.x.x
$ make
$ make install
```

--------------------------------

### Python C Extension Example with Keyword Arguments

Source: https://docs.python.org/3/extending/extending

A C extension module example demonstrating the use of PyArg_ParseTupleAndKeywords to handle keyword arguments for a 'parrot' function. It parses integer and string arguments and prints formatted output.

```c
#define PY_SSIZE_T_CLEAN
#include<Python.h>

static PyObject*
keywdarg_parrot(PyObject*self, PyObject*args, PyObject*keywds)
{
    int voltage;
    const char*state = "a stiff";
    const char*action = "voom";
    const char*type = "Norwegian Blue";

    static char*kwlist[] = {"voltage", "state", "action", "type", NULL};

    if(!PyArg_ParseTupleAndKeywords(args, keywds, "i|sss", kwlist,
                                     &voltage, &state, &action, &type))
        return NULL;

    printf("-- This parrot wouldn't %s if you put %i Volts through it.\n",
           action, voltage);
    printf("-- Lovely plumage, the %s -- It's %s!\n", type, state);

    Py_RETURN_NONE;
}

static PyMethodDef keywdarg_methods[] = {
    /* The cast of the function is necessary since PyCFunction values
     * only take two PyObject* parameters, and keywdarg_parrot() takes
     * three.
     */
    {"parrot", (PyCFunction)(void(*)(void))keywdarg_parrot, METH_VARARGS | METH_KEYWORDS,
     "Print a lovely skit to standard output."},
    {NULL, NULL, 0, NULL} /* sentinel */
};

static struct PyModuleDef keywdarg_module = {
    .m_base = PyModuleDef_HEAD_INIT,
    .m_name = "keywdarg",
    .m_size = 0,
    .m_methods = keywdarg_methods,
};

PyMODINIT_FUNC
PyInit_keywdarg(void)
{
    return PyModuleDef_Init(&keywdarg_module);
}

```

--------------------------------

### IDLE Documentation Overview

Source: https://docs.python.org/3/contents

Provides links to various sections of the IDLE documentation, covering help sources, preference settings, macOS specific information, and extensions.

```python
import idle

# Accessing IDLE documentation sections:
# help_sources = idle.help_sources
# setting_preferences = idle.setting_preferences
# idle_on_macos = idle.idle_on_macos
# extensions = idle.extensions
```

--------------------------------

### Python re.Match.span() Example

Source: https://docs.python.org/3/library/re

Demonstrates the span() method, which returns a tuple of the start and end indices for a given group within a re.Match object. It also shows the behavior for groups that did not participate in the match.

```python
>>> import re
>>> m = re.search('b(c?)', 'cba')
>>> m.span(0)
(1, 2)
>>> m.span(1)
(2, 2)
>>> m.span(2)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: no such group
```

--------------------------------

### Test Support Threading Helper Start Threads

Source: https://docs.python.org/3/genindex-S

Starts multiple threads for testing purposes. This utility function from `test.support` is used to manage the creation and starting of several threads concurrently.

```python
import test.support.threading_helper
import threading

def thread_func():
    print(threading.current_thread().name)

threads = [threading.Thread(target=thread_func) for _ in range(3)]

test.support.threading_helper.start_threads(threads)

for t in threads:
    t.join()
```

--------------------------------

### Turtle Graphics Introduction and Basics

Source: https://docs.python.org/3/library/tk

This section introduces the turtle graphics module and provides guidance on getting started with basic drawing. It covers setting up a turtle environment, fundamental drawing commands, pen control, and understanding the turtle's position.

```python
import turtle

# Get started with basic drawing
screen = turtle.Screen()
turtle_obj = turtle.Turtle()

# Pen control
turtle_obj.penup()  # Lift the pen
turtle_obj.pendown() # Put the pen down

# Turtle motion
turtle_obj.forward(100)
turtle_obj.left(90)
```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/library/2to3

Lists essential external resources for Python developers, including the Python Enhancement Proposal (PEP) index, guides for beginners, book recommendations, audio/visual talks, and the Python Developer's Guide.

```markdown
* [PEP Index](https://peps.python.org/)
* [Beginner's Guide](https://wiki.python.org/moin/BeginnersGuide)
* [Book List](https://wiki.python.org/moin/PythonBooks)
* [Audio/Visual Talks](https://www.python.org/doc/av/)
* [Python Developer’s Guide](https://devguide.python.org/)
```

--------------------------------

### Dynamic C Extension Example (_asyncio module)

Source: https://docs.python.org/3/using/configure

Shows an example of a C extension built as a dynamic library, such as '_asyncio'. These modules have a '__file__' attribute pointing to their shared object file.

```python
>>> import _asyncio
>>> _asyncio
<module '_asyncio' from '/usr/lib64/python3.9/lib-dynload/_asyncio.cpython-39-x86_64-linux-gnu.so'>
>>> _asyncio.__file__
'/usr/lib64/python3.9/lib-dynload/_asyncio.cpython-39-x86_64-linux-gnu.so'

```

--------------------------------

### BLAKE2 Tree Mode Hashing

Source: https://docs.python.org/3/library/hashlib

An example of hashing a minimal tree structure with two leaf nodes using BLAKE2b in tree mode. It demonstrates the parameters for leaf and inner nodes, and how to combine them to get the final digest.

```python
from hashlib import blake2b

FANOUT = 2
DEPTH = 2
LEAF_SIZE = 4096
INNER_SIZE = 64

buf = bytearray(6000)

# Left leaf
h00 = blake2b(buf[0:LEAF_SIZE], fanout=FANOUT, depth=DEPTH,
              leaf_size=LEAF_SIZE, inner_size=INNER_SIZE,
              node_offset=0, node_depth=0, last_node=False)
# Right leaf
h01 = blake2b(buf[LEAF_SIZE:], fanout=FANOUT, depth=DEPTH,
              leaf_size=LEAF_SIZE, inner_size=INNER_SIZE,
              node_offset=1, node_depth=0, last_node=True)
# Root node
h10 = blake2b(digest_size=32, fanout=FANOUT, depth=DEPTH,
              leaf_size=LEAF_SIZE, inner_size=INNER_SIZE,
              node_offset=0, node_depth=1, last_node=True)
h10.update(h00.digest())
h10.update(h01.digest())
print(h10.hexdigest())
```

--------------------------------

### Python Documentation Navigation and Resources

Source: https://docs.python.org/3/.12

This snippet outlines the structure and key resources available in the Python 3.12.10 documentation. It highlights sections for new features, tutorials, library references, installation guides, and more, along with navigation aids and project information.

```APIDOC
Python 3.12.10 Documentation:
  Welcome! This is the official documentation for Python 3.12.10. 
  Documentation sections:
  [What's new in Python 3.12?](https://docs.python.org/3.12/whatsnew/3.12.html)
  Or [all "What's new" documents since Python 2.0](https://docs.python.org/3.12/whatsnew/index.html)
  [Tutorial](https://docs.python.org/3.12/tutorial/index.html)
    Start here: a tour of Python's syntax and features
  [Library reference](https://docs.python.org/3.12/library/index.html)
    Standard library and builtins
  [Language reference](https://docs.python.org/3.12/reference/index.html)
    Syntax and language elements
  [Python setup and usage](https://docs.python.org/3.12/using/index.html)
    How to install, configure, and use Python
  [Python HOWTOs](https://docs.python.org/3.12/howto/index.html)
    In-depth topic manuals
  [Installing Python modules](https://docs.python.org/3.12/installing/index.html)
    Third-party modules and PyPI.org
  [Distributing Python modules](https://docs.python.org/3.12/distributing/index.html)
    Publishing modules for use by other people
  [Extending and embedding](https://docs.python.org/3.12/extending/index.html)
    For C/C++ programmers
  [Python's C API](https://docs.python.org/3.12/c-api/index.html)
    C API reference
  [FAQs](https://docs.python.org/3.12/faq/index.html)
    Frequently asked questions (with answers!)
  [Deprecations](https://docs.python.org/3.12/deprecations/index.html)
    Deprecated functionality

  Indices, glossary, and search:
  [Global module index](https://docs.python.org/3.12/py-modindex.html)
    All modules and libraries
  [General index](https://docs.python.org/3.12/genindex.html)
    All functions, classes, and terms
  [Glossary](https://docs.python.org/3.12/glossary.html)
    Terms explained
  [Search page](https://docs.python.org/3.12/search.html)
    Search this documentation
  [Complete table of contents](https://docs.python.org/3.12/contents.html)
    Lists all sections and subsections

  Project information:
  [Reporting issues](https://docs.python.org/3.12/bugs.html)
  [Contributing to Docs](https://devguide.python.org/documentation/help-documenting/)
  [Download the documentation](https://docs.python.org/3.12/download.html)
  [History and license of Python](https://docs.python.org/3.12/license.html)
  [Copyright](https://docs.python.org/3.12/copyright.html)
  [About the documentation](https://docs.python.org/3.12/about.html)
```

--------------------------------

### Install SystemTap Development Tools (Linux)

Source: https://docs.python.org/3/howto/instrumentation

Installs the necessary development tools for SystemTap on Linux systems using yum.

```bash
$ yum
```

--------------------------------

### Calling Static Methods

Source: https://docs.python.org/3/howto/descriptor

Shows how to call a static method using both the class and an instance. The behavior is identical in both cases.

```python
>>> E.f(3)
30
>>> E().f(3)
30
```

--------------------------------

### Verify Python Installation

Source: https://docs.python.org/3/using/windows

Verifies the installed Python version by executing the python executable from the tools directory within the nuget package installation. Demonstrates output with and without the -ExcludeVersion flag.

```bash
# Without -ExcludeVersion
> .\python.3.5.2\tools\python.exe -V
Python 3.5.2

# With -ExcludeVersion
> .\python\tools\python.exe -V
Python 3.5.2
```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/.11

Lists essential resources for Python developers, including the Python Enhancement Proposals (PEP) index, a guide for beginners, a curated book list, audio/visual talks, and the Python Developer's Guide.

```text
PEP Index: https://peps.python.org/
Beginner's Guide: https://wiki.python.org/moin/BeginnersGuide
Book List: https://wiki.python.org/moin/PythonBooks
Audio/Visual Talks: https://www.python.org/doc/av/
Python Developer’s Guide: https://devguide.python.org/
```

--------------------------------

### Python Multiprocessing Connection Server Example

Source: https://docs.python.org/3/library/multiprocessing

This example demonstrates how to set up a server using multiprocessing.connection.Listener to accept connections, send various data types like lists, bytes, and arrays, and handle client interactions.

```python
from multiprocessing.connection import Listener
from array import array

address = ('localhost', 6000)     # family is deduced to be 'AF_INET'

with Listener(address, authkey=b'secret password') as listener:
    with listener.accept() as conn:
        print('connection accepted from', listener.last_accepted)

        conn.send([2.25, None, 'junk', float])

        conn.send_bytes(b'hello')

        conn.send_bytes(array('i', [42, 1729]))

```

--------------------------------

### Asyncio Unix Server Start

Source: https://docs.python.org/3/genindex-S

Starts a Unix domain socket server. This function creates a server that listens on a Unix domain socket path, accepting incoming connections.

```python
import asyncio
import os

SOCKET_PATH = '/tmp/my_unix_socket'

async def handle_unix_client(reader, writer):
    print("Unix client connected")
    writer.write(b"Hello from Unix socket!")
    await writer.drain()
    writer.close()

async def main():
    # Remove socket file if it already exists
    if os.path.exists(SOCKET_PATH):
        os.remove(SOCKET_PATH)

    server = await asyncio.start_unix_server(
        handle_unix_client, SOCKET_PATH)

    print(f'Serving on {SOCKET_PATH}')
    async with server:
        await server.serve_forever()

if __name__ == "__main__":
    asyncio.run(main())
```

--------------------------------

### Asyncio Stream Server Start

Source: https://docs.python.org/3/genindex-S

Starts a TCP server. This function creates a server that listens on a specified host and port, accepting incoming connections.

```python
import asyncio

async def handle_client(reader, writer):
    data = await reader.read(100)
    message = data.decode()
    addr = writer.get_extra_info('peername')
    print(f"Received {message} from {addr}")

    writer.write(b"Hello Client!")
    await writer.drain()
    writer.close()

async def main():
    server = await asyncio.start_server(
        handle_client, '127.0.0.1', 8888)

    addr = server.sockets[0].getsockname()
    print(f'Serving on {addr}')

    async with server:
        await server.serve_forever()

if __name__ == "__main__":
    asyncio.run(main())
```

--------------------------------

### Turtle Configuration File Example (turtle.cfg)

Source: https://docs.python.org/3/library/turtle

An example configuration file (`turtle.cfg`) for customizing the appearance and behavior of Python's turtle graphics module. Settings include screen dimensions, colors, shapes, and language preferences.

```cfg
width=0.5
height=0.75
leftright=None
topbottom=None
canvwidth=400
canvheight=300
mode=standard
colormode=1.0
delay=10
undobuffersize=1000
shape=classic
pencolor=black
fillcolor=black
resizemode=noresize
visible=True
language=english
exampleturtle=turtle
examplescreen=screen
title=Python Turtle Graphics
using_IDLE=False
```

--------------------------------

### Python Initialization Configuration

Source: https://docs.python.org/3/c-api/index

Details on configuring Python's initialization process, including pre-initialization with PyPreConfig and isolated configuration options. It also covers Python path configuration and multi-phase initialization.

```APIDOC
Python Initialization Configuration:

PyPreConfig:
  Structure for pre-initializing Python.
  Fields include options for configuration.

Preinitialize Python with PyPreConfig:
  Use Py_PreInitialize() to initialize Python with a PyPreConfig structure.

PyConfig:
  Structure for full Python initialization.
  Contains detailed configuration settings.

Initialization with PyConfig:
  Use Py_InitializeConfig() to initialize Python with a PyConfig structure.

Isolated Configuration:
  Configure Python to run in an isolated environment, affecting module searching and site-specific configurations.

Python Path Configuration:
  Manage the Python module search path during initialization.

Py_GetArgcArgv():
  Retrieves the argument count and values passed to the Python interpreter.

Multi-Phase Initialization Private Provisional API:
  APIs for advanced, multi-phase initialization of the Python interpreter. Use with caution as it's provisional.
```

--------------------------------

### Prefix Scheme Installation Directories (POSIX)

Source: https://docs.python.org/3/library/sysconfig

Details the installation paths for the prefix scheme on POSIX systems. This scheme is useful for installing modules into a different Python installation's third-party module directory.

```python
Path | Installation directory
_stdlib_ | _prefix_/lib/python_X.Y_
_platstdlib_ | _prefix_/lib/python_X.Y_
_platlib_ | _prefix_/lib/python_X.Y_/site-packages
_purelib_ | _prefix_/lib/python_X.Y_/site-packages
_include_ | _prefix_/include/python_X.Y_
_platinclude_ | _prefix_/include/python_X.Y_
_scripts_ | _prefix_/bin
_data_ | _prefix_
```

--------------------------------

### Simulated Member Descriptor in Python

Source: https://docs.python.org/3/howto/descriptor

Provides a Python implementation of a Member descriptor class, simulating the behavior of C-level member access for attributes defined in __slots__. It handles getting, setting, deleting, and representing slot values.

```python
null = object()

class Member:

    def __init__(self, name, clsname, offset):
        'Emulate PyMemberDef in Include/structmember.h'
        # Also see descr_new() in Objects/descrobject.c
        self.name = name
        self.clsname = clsname
        self.offset = offset

    def __get__(self, obj, objtype=None):
        'Emulate member_get() in Objects/descrobject.c'
        # Also see PyMember_GetOne() in Python/structmember.c
        if obj is None:
            return self
        value = obj._slotvalues[self.offset]
        if value is null:
            raise AttributeError(self.name)
        return value

    def __set__(self, obj, value):
        'Emulate member_set() in Objects/descrobject.c'
        obj._slotvalues[self.offset] = value

    def __delete__(self, obj):
        'Emulate member_delete() in Objects/descrobject.c'
        value = obj._slotvalues[self.offset]
        if value is null:
            raise AttributeError(self.name)
        obj._slotvalues[self.offset] = null

    def __repr__(self):
        'Emulate member_repr() in Objects/descrobject.c'
        return f'<Member {self.name!r} of {self.clsname!r}>'

```

--------------------------------

### Installing Python Modules: User-Specific Installation

Source: https://docs.python.org/3/contents

Instructions on how to install Python packages for the current user only, without affecting the system-wide Python installation. This is useful for development environments.

```APIDOC
Install packages just for the current user:
  Details the process of installing Python packages on a per-user basis.
  Avoids modifying the system's global Python environment.
```

--------------------------------

### wsgiref.simple_server API Documentation

Source: https://docs.python.org/3/library/wsgiref

This section details the core components of the wsgiref.simple_server module, including the `make_server` function for creating server instances, the `demo_app` for testing, and the `WSGIServer` class with its methods for managing the WSGI application.

```APIDOC
wsgiref.simple_server.make_server(_host_, _port_, _app_, _server_class=WSGIServer_, _handler_class=WSGIRequestHandler_)
  Creates a new WSGI server listening on _host_ and _port_, accepting connections for _app_.
  _app_ must be a WSGI application object.
  Returns an instance of _server_class_.

wsgiref.simple_server.demo_app(_environ_, _start_response_)
  A simple WSGI application that returns "Hello world!" and environment details.
  _start_response_ callable should follow the StartResponse protocol.

wsgiref.simple_server.WSGIServer(_server_address_, _RequestHandlerClass_)
  Creates a WSGIServer instance.
  _server_address_ is a (host, port) tuple.
  _RequestHandlerClass_ is a subclass of http.server.BaseHTTPRequestHandler.
  This class is a subclass of http.server.HTTPServer and provides WSGI-specific methods.

  WSGIServer.set_app(_application_)
    Sets the callable _application_ as the WSGI application.

  WSGIServer.get_app()
    Returns the currently set application callable.
```

--------------------------------

### Install Dependencies into Testbed

Source: https://docs.python.org/3/using/ios

Installs additional project dependencies into the app testbed's package directory. This ensures that your project's dependencies are available when running tests on iOS.

```bash
pip install --target app-testbed/iOSTestbed/app_packages your_package_name
```

--------------------------------

### Setting All Items in a Mutable Sequence

Source: https://docs.python.org/3/c-api/intro

Provides an example of a C function that sets all items in a mutable Python sequence (like a list) to a given item. It uses PyObject_Length to get the sequence size and iterates to set each item.

```c
int
set_all(PyObject*target,PyObject*item)
{
Py_ssize_ti,n;

n=PyObject_Length(target);
if(n<0)
return-1;
for(i=0;i<n;i++){

```

--------------------------------

### DocTestRunner Reporting Methods

Source: https://docs.python.org/3/library/doctest

Provides methods for reporting the progress and results of doctest execution. These methods are intended for subclassing to customize output. They include reporting the start of a test, success, unexpected exceptions, and failures.

```python
report_start(_out_, _test_, _example_)
    Report that the test runner is about to process the given example.

report_success(_out_, _test_, _example_, _got_)
    Report that an example executed successfully.
```

--------------------------------

### Introduction Section Navigation

Source: https://docs.python.org/3/library/intro

Provides links to the introduction section of the Python 3 documentation, including notes on availability for various platforms.

```text
[Introduction](https://docs.python.org/3/library/intro.html)
    * [Notes on availability](https://docs.python.org/3/library/intro.html#notes-on-availability)
      * [WebAssembly platforms](https://docs.python.org/3/library/intro.html#webassembly-platforms)
      * [Mobile platforms](https://docs.python.org/3/library/intro.html#mobile-platforms)
```

--------------------------------

### IMAP4 Example

Source: https://docs.python.org/3/contents

Provides an example of using the IMAP4 protocol client in Python.

```python
from imaplib import IMAP4

# Example usage (details not provided in source text)
# imap_server = IMAP4('your_imap_server.com')
# imap_server.login('your_email', 'your_password')
# imap_server.select('inbox')
# ... other IMAP operations
```

--------------------------------

### Python Documentation Links

Source: https://docs.python.org/3/using/configure

Contains navigation links for the Python documentation, including general index, module index, and links to specific platform usage guides.

```html
<ul>
  <li><a href="https://docs.python.org/3/genindex.html">General Index</a></li>
  <li><a href="https://docs.python.org/3/py-modindex.html">Python Module Index</a></li>
  <li><a href="https://docs.python.org/3/using/windows.html">4. Using Python on Windows</a></li>
  <li><a href="https://docs.python.org/3/using/unix.html">2. Using Python on Unix platforms</a></li>
  <li><a href="https://www.python.org/">Python</a></li>
</ul>
```

--------------------------------

### Install Python 3.13b2 with Free-Threaded Interpreter on macOS

Source: https://docs.python.org/3/using/mac

This snippet demonstrates how to download the Python 3.13b2 macOS installer package using `curl`, create a `choicechanges.plist` file to enable the free-threaded interpreter, and then install the package using `sudo installer` with the custom choices applied. It targets the root directory for installation.

```shell
RELEASE="python-3.130b2-macos11.pkg"

# download installer pkg
curl -O https://www.python.org/ftp/python/3.13.0/${RELEASE}

# create installer choicechanges to customize the install:
#    enable the PythonTFramework-3.13 package
#    while accepting the other defaults (install all other packages)
cat > ./choicechanges.plist <<EOF
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<array>
        <dict>
                <key>attributeSetting</key>
                <integer>1</integer>
                <key>choiceAttribute</key>
                <string>selected</string>
                <key>choiceIdentifier</key>
                <string>org.python.Python.PythonTFramework-3.13</string>
        </dict>
</array>
</plist>
EOF

sudo installer -pkg ./${RELEASE} -applyChoiceChangesXML ./choicechanges.plist -target /

```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<array>
        <dict>
                <key>attributeSetting</key>
                <integer>1</integer>
                <key>choiceAttribute</key>
                <string>selected</string>
                <key>choiceIdentifier</key>
                <string>org.python.Python.PythonTFramework-3.13</string>
        </dict>
</array>
</plist>
```

--------------------------------

### Recommended Third-Party Tools for Python Extensions

Source: https://docs.python.org/3/c-api/intro

A list of popular third-party tools that simplify the creation of C, C++, and Rust extensions for Python. These tools can help avoid version-specific code, manage reference counting errors, and leverage newer APIs.

```APIDOC
Third-Party Tools for Python Extensions:

- Cython: For writing C extensions using Python-like syntax.
- cffi: Foreign Function Interface for Python.
- HPy: A new, more performant API for C extensions.
- nanobind: Modern C++ bindings for Python.
- Numba: JIT compiler that translates Python and NumPy code into fast machine code.
- pybind11: Seamlessly interoperates between C++11 and Python.
- PyO3: Rust bindings for Python.
- SWIG: Simplified Wrapper and Interface Generator.
```

--------------------------------

### Bash Script to Prepare Logging Environment

Source: https://docs.python.org/3/howto/logging-cookbook

A Bash script to set up the necessary environment for testing the logging socket listener and web application. This includes creating directories and installing dependencies.

```bash
prepare.sh
```

--------------------------------

### Python sysconfig Installation Directories (Windows)

Source: https://docs.python.org/3/library/sysconfig

This table details the installation directories for various Python components on Windows systems, as provided by the sysconfig module. It maps logical installation paths to their physical locations within the Python installation prefix.

```python
Path | Installation directory
---|---
_stdlib_ | `_prefix_\Lib`
_platstdlib_ | `_prefix_\Lib`
_platlib_ | `_prefix_\Lib\site-packages`
_purelib_ | `_prefix_\Lib\site-packages`
_include_ | `_prefix_\Include`
_platinclude_ | `_prefix_\Include`
_scripts_ | `_prefix_\Scripts`
_data_ | `_prefix_`
```

--------------------------------

### Asynchronous Context Manager Example

Source: https://docs.python.org/3/reference/datamodel

An example class demonstrating an asynchronous context manager. It defines __aenter__ and __aexit__ methods that are awaitable, suitable for use with the 'async with' statement.

```python
class AsyncContextManager:
    async def __aenter__(self):
        await log('entering context')

    async def __aexit__(self, exc_type, exc, tb):
        await log('exiting context')
```

--------------------------------

### Decorate-Sort-Undecorate (DSU) Idiom

Source: https://docs.python.org/3/howto/sorting

Demonstrates the Decorate-Sort-Undecorate (DSU) idiom for sorting. It involves decorating items with sort keys, sorting the decorated list, and then undecorating to get the final sorted list. This example sorts student data by grade.

```python
>>> decorated = [(student.grade, i, student) for i, student in enumerate(student_objects)]
>>> decorated.sort()
>>> [student for grade, i, student in decorated]               # undecorate
[('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
```

--------------------------------

### Differ Example: Comparing Texts

Source: https://docs.python.org/3/library/difflib

This Python code snippet demonstrates how to use the `difflib.Differ` class to compare two multi-line texts. It shows the setup of text sequences, instantiation of the `Differ` object, and the process of comparing and displaying the resulting differences.

```python
import difflib
import pprint
import sys

text1 = '''  1. Beautiful is better than ugly.
...   2. Explicit is better than implicit.
...   3. Simple is better than complex.
...   4. Complex is better than complicated.
... '''.splitlines(keepends=True)
text2 = '''  1. Beautiful is better than ugly.
...   3.   Simple is better than complex.
...   4. Complicated is better than complex.
...   5. Flat is better than nested.
... '''.splitlines(keepends=True)

d = difflib.Differ()
result = list(d.compare(text1, text2))

pprint.pprint(result)

sys.stdout.writelines(result)
```

--------------------------------

### Python File I/O Operations

Source: https://docs.python.org/3/tutorial/inputoutput

Provides examples of basic file input and output operations in Python, including reading from and writing to files. It covers opening, reading, writing, and closing files.

```python
# Writing to a file
with open("output.txt", "w") as f:
    f.write("Hello, world!\n")

# Reading from a file
with open("output.txt", "r") as f:
    content = f.read()
    print(content)
```

--------------------------------

### Inspecting Descriptor Attributes (Python)

Source: https://docs.python.org/3/howto/descriptor

Shows how to inspect the internal attributes of descriptor instances after they have been assigned to class variables. This example uses `vars()` to access the `public_name` and `private_name` stored within the descriptor instances associated with the `Person` class.

```python
>>> vars(vars(Person)['name'])
{'public_name': 'name', 'private_name': '_name'}
>>> vars(vars(Person)['age'])
{'public_name': 'age', 'private_name': '_age'}

```

--------------------------------

### Install Package for Current User

Source: https://docs.python.org/3/installing/index

Installs a package only for the current user, rather than system-wide. This is useful for avoiding permission issues.

```bash
python -m pip install --user <package-name>
```

--------------------------------

### Python 3 Navigation Links

Source: https://docs.python.org/3/howto/sockets

Provides links to key sections of the Python 3 documentation, such as the general index, module index, and various HOWTO guides.

```python
index: https://docs.python.org/3/genindex.html
modules: https://docs.python.org/3/py-modindex.html
sorting: https://docs.python.org/3/howto/sorting.html
regex: https://docs.python.org/3/howto/regex.html
python_home: https://www.python.org/
```

--------------------------------

### String Templating with Template and substitute

Source: https://docs.python.org/3/tutorial/stdlib2

Demonstrates basic string templating using the string.Template class and its substitute method. It shows how to create templates with placeholders and replace them with provided values.

```python
from string import Template
t = Template('${village}folk send $$10 to $cause.')
print(t.substitute(village='Nottingham', cause='the ditch fund'))
```

--------------------------------

### ensurepip Module API

Source: https://docs.python.org/3/library/ensurepip

The `ensurepip` module provides support for bootstrapping the `pip` installer into an existing Python installation or virtual environment. It bundles the latest stable version of `pip` with CPython releases. This module is typically not invoked directly by end-users but may be necessary if `pip` was skipped during installation or uninstalled.

```python
import ensurepip

# To bootstrap pip into the current environment:
ensurepip.bootstrap()

# To bootstrap pip into a specific user directory:
# ensurepip.bootstrap(user=True)

# To bootstrap pip with a specific version of setuptools:
# ensurepip.bootstrap(version='setuptools<50')

# To bootstrap pip with a specific version of pip:
# ensurepip.bootstrap(pip_version='21.0.1')

# To bootstrap pip with a specific version of wheel:
# ensurepip.bootstrap(wheel_version='0.36.2')

# To bootstrap pip with a specific version of setuptools and wheel:
# ensurepip.bootstrap(version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip and setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50')

# To bootstrap pip with a specific version of pip, setuptools and wheel:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap pip with a specific version of pip, setuptools and wheel, and a specific version of setuptools:
# ensurepip.bootstrap(pip_version='21.0.1', version='setuptools<50', wheel_version='0.36.2')

# To bootstrap
```

--------------------------------

### Doctest Test Runner Example

Source: https://docs.python.org/3/library/doctest

A minimal example of a Python test runner using the doctest module. It demonstrates how to run specific docstring examples or the entire module with various flags, including reporting differences and failing fast.

```python
if __name__ == '__main__':
    import doctest
    import sys
    flags = doctest.REPORT_NDIFF | doctest.FAIL_FAST
    if len(sys.argv) > 1:
        name = sys.argv[1]
        if name in globals():
            obj = globals()[name]
        else:
            obj = __test__[name]
        doctest.run_docstring_examples(obj, globals(), name=name,
                                       optionflags=flags)
    else:
        fail, total = doctest.testmod(optionflags=flags)
        print(f"{fail} failures out of {total} tests")
```

--------------------------------

### Manage Python Packages with pip

Source: https://docs.python.org/3/tutorial/venv

Shows how to uninstall, display information about, list installed packages, and freeze installed packages into a requirements file using pip.

```bash
python -m pip uninstall <package-name>
python -m pip show <package-name>
python -m pip list
python -m pip freeze
```

--------------------------------

### Python 3 Standard Library Introduction

Source: https://docs.python.org/3/contents

An introduction to the Python 3 Standard Library, covering its organization and availability on different platforms.

```python
# Importing modules from the standard library
import os
import math

# Example usage of a standard library function
print(os.getcwd())
print(math.sqrt(16))
```

--------------------------------

### Python AST MatchSingleton Example

Source: https://docs.python.org/3/library/ast

Illustrates the AST for a 'match' statement comparing against the 'None' singleton.

```python
print(ast.dump(ast.parse("""
match x:
    case None:
        ...
""", indent=4)))

```

--------------------------------

### os.startfile() Method

Source: https://docs.python.org/3/genindex-S

Opens a file with its associated application. This is a platform-specific function, primarily for Windows.

```APIDOC
os:
  startfile(path, operation=None)
    Opens a file with its associated application.
    Parameters:
      path: The path to the file.
      operation: The operation to perform (e.g., 'print').
```

--------------------------------

### Python SSL Server Setup

Source: https://docs.python.org/3/library/ssl

Demonstrates the initial steps for setting up a server-side SSL context and binding a socket. It involves creating an SSL context for client authentication, loading the server's certificate and private key, and binding the socket to a specific address and port.

```python
import socket, ssl

context = ssl.create_default_context(ssl.Purpose.CLIENT_AUTH)
context.load_cert_chain(certfile="mycertfile", keyfile="mykeyfile")

bindsocket = socket.socket()
bindsocket.bind(('myaddr.example.com', 10023))
bindsocket.listen(5)
```

--------------------------------

### Install SSL Certificates

Source: https://docs.python.org/3/using/mac

This command is executed after the main Python installation to download and install necessary SSL root certificates for Python's use. It ensures secure communication for network-related operations.

```bash
Install Certificates.command
```

--------------------------------

### itertools.product Examples

Source: https://docs.python.org/3/whatsnew/2

Illustrates the use of itertools.product for generating Cartesian products of iterables, including examples with and without the 'repeat' argument.

```python
import itertools

# Cartesian product of two iterables
print(list(itertools.product([1,2,3], [4,5,6]))) 

# Cartesian product with repeat
print(list(itertools.product([1,2], repeat=3)))

# Cartesian product of two iterables with repeat
print(list(itertools.product([1,2], [3,4], repeat=2)))
```

--------------------------------

### Install Latest Package

Source: https://docs.python.org/3/installing/index

Installs the latest version of a specified package and its dependencies from the Python Package Index.

```bash
pip install <package-name>
```

--------------------------------

### Install Specific Python Version on OpenBSD (i386)

Source: https://docs.python.org/3/using/unix

Installs version 2.5.1 of Python for i386 architecture on OpenBSD.

```bash
pkg_add -i python-2.5.1p1
```

--------------------------------

### Install Scientific Python Packages

Source: https://docs.python.org/3/installing/index

Addresses the difficulty of installing scientific Python packages with complex binary dependencies directly via pip. Recommends alternative installation methods for such packages.

```text
It will often be easier for users to install these packages by other means rather than attempting to install them with pip.
```

--------------------------------

### Python Tutorial Navigation and Links

Source: https://docs.python.org/3/tutorial/index

This section outlines the structure of the Python Tutorial, providing links to various chapters and sub-sections. It also includes navigation links for previous and next topics, as well as links for reporting bugs and viewing the source code.

```python
# Previous topic
# [Changelog](https://docs.python.org/3/whatsnew/changelog.html "previous chapter")

# Next topic
# [1. Whetting Your Appetite](https://docs.python.org/3/tutorial/appetite.html "next chapter")

### This page
  * [Report a bug](https://docs.python.org/3/bugs.html)
  * [Show source ](https://github.com/python/cpython/blob/main/Doc/tutorial/index.rst?plain=1)

«
### Navigation
  * [index](https://docs.python.org/3/genindex.html "General Index")
  * [modules](https://docs.python.org/3/py-modindex.html "Python Module Index") |
  * [next](https://docs.python.org/3/tutorial/appetite.html "1. Whetting Your Appetite") |
  * [previous](https://docs.python.org/3/whatsnew/changelog.html "Changelog") |
  * [Python](https://www.python.org/) »
  * Greek | Ελληνικά English Spanish | español French | français Italian | italiano Japanese | 日本語 Korean | 한국어 Polish | polski Brazilian Portuguese | Português brasileiro Turkish | Türkçe Simplified Chinese | 简体中文 Traditional Chinese | 繁體中文
dev (3.15) pre (3.14) 3.13.7 3.12 3.11 3.10 3.9 3.8 3.7 3.6 3.5 3.4 3.3 3.2 3.1 3.0 2.7 2.6
  * [3.13.7 Documentation](https://docs.python.org/3/index.html) » 
  * [The Python Tutorial](https://docs.python.org/3/tutorial/index.html)
  * | 
  * Theme  Auto Light Dark |

© [ Copyright ](https://docs.python.org/3/copyright.html) 2001-2025, Python Software Foundation.   
This page is licensed under the Python Software Foundation License Version 2.   
Examples, recipes, and other code in the documentation are additionally licensed under the Zero Clause BSD License.   
See [History and License](https://docs.python.org/license.html) for more information.  
  
The Python Software Foundation is a non-profit corporation. [Please donate.](https://www.python.org/psf/donations/)   
  
Last updated on Aug 17, 2025 (07:57 UTC). [Found a bug](https://docs.python.org/bugs.html)?   
Created using [Sphinx](https://www.sphinx-doc.org/) 8.2.3.
```

--------------------------------

### Command-line Parsing with optparse

Source: https://docs.python.org/3/library/getopt

Demonstrates an alternative to getopt using the optparse module for declarative command-line option parsing. This example shows how to create an OptionParser, add options with short and long forms, and parse arguments. It's presented as a more concise and informative alternative for certain use cases.

```python
import optparse

def process(args, output, verbose):
    print(f"Arguments: {args}")
    print(f"Output file: {output}")
    print(f"Verbose: {verbose}")

if __name__ == '__main__':
    parser = optparse.OptionParser()
    parser.add_option('-o', '--output')
    parser.add_option('-v', dest='verbose', action='store_true')
    opts, args = parser.parse_args()
    process(args, output=opts.output, verbose=opts.verbose)
```

--------------------------------

### Start Logging Listener

Source: https://docs.python.org/3/howto/logging-cookbook

This snippet demonstrates how to create and start a logging listener on a specified port. It logs messages at various levels and includes cleanup logic for graceful shutdown.

```python
import logging
import logging.config
import time

# create and start listener on port 9999
t = logging.config.listen(9999)
t.start()

logger = logging.getLogger('simpleExample')

try:
    # loop through logging calls to see the difference
    # new configurations make, until Ctrl+C is pressed
    while True:
        logger.debug('debug message')
        logger.info('info message')
        logger.warning('warn message')
        logger.error('error message')
        logger.critical('critical message')
        time.sleep(5)
except KeyboardInterrupt:
    # cleanup
    logging.config.stopListening()
    t.join()
```

--------------------------------

### Building Python on Unix

Source: https://docs.python.org/3/using/unix

Instructions for compiling Python from source on Unix-like systems. It highlights the use of 'make altinstall' to avoid overwriting system binaries and recommends checking the README.rst for platform-specific details.

```bash
# Recommended installation command to avoid overwriting system python3 binary
make altinstall
```

--------------------------------

### PrettyPrinter Constructor and Usage Examples

Source: https://docs.python.org/3/library/pprint

Demonstrates how to create PrettyPrinter instances with different configurations for indentation, width, and compactness, and how to use the pprint method to display complex data structures. Includes examples with lists and tuples, showcasing depth limiting.

```python
>>> import pprint
>>> stuff = ['spam', 'eggs', 'lumberjack', 'knights', 'ni']
>>> stuff.insert(0, stuff[:])
>>> pp = pprint.PrettyPrinter(indent=4)
>>> pp.pprint(stuff)
[   ['spam', 'eggs', 'lumberjack', 'knights', 'ni'],
    'spam',
    'eggs',
    'lumberjack',
    'knights',
    'ni']
>>> pp = pprint.PrettyPrinter(width=41, compact=True)
>>> pp.pprint(stuff)
[['spam', 'eggs', 'lumberjack',
  'knights', 'ni'],
 'spam', 'eggs', 'lumberjack', 'knights',
 'ni']
>>> tup = ('spam', ('eggs', ('lumberjack', ('knights', ('ni', ('dead',
... ('parrot', ('fresh fruit',))))))))
>>> pp = pprint.PrettyPrinter(depth=6)
>>> pp.pprint(tup)
('spam', ('eggs', ('lumberjack', ('knights', ('ni', ('dead', (...)))))))
```

--------------------------------

### Output of script_from_examples

Source: https://docs.python.org/3/library/doctest

The resulting Python script generated by `doctest.script_from_examples()` from the provided doctest examples. Doctest examples are now regular code, and descriptive text is commented out.

```python
# Set x and y to 1 and 2.
x, y = 1, 2
#
# Print their sum:
print(x+y)
# Expected:

```

--------------------------------

### Install IDLE on Fedora/RHEL/CentOS

Source: https://docs.python.org/3/using/unix

Installs the IDLE development environment for Python on Fedora, RHEL, and CentOS systems.

```bash
sudo dnf install python3-idle
```

--------------------------------

### Internet Access with urllib.request and smtplib

Source: https://docs.python.org/3/tutorial/stdlib

Shows how to retrieve data from a URL using `urllib.request` and send an email using `smtplib`. The `urllib` example fetches and prints a datetime string, while the `smtplib` example demonstrates sending a simple message (requires a running mail server).

```python
from urllib.request import urlopen
>>> with urlopen('http://worldtimeapi.org/api/timezone/etc/UTC.txt') as response:
...     for line in response:
...         line = line.decode()             # Convert bytes to a str
...         if line.startswith('datetime'):
...             print(line.rstrip())         # Remove trailing newline
...
datetime: 2022-01-01T01:36:47.689215+00:00

import smtplib
>>> server = smtplib.SMTP('localhost')
>>> server.sendmail('soothsayer@example.org', 'jcaesar@example.org',
... """To: jcaesar@example.org
From: soothsayer@example.org

Beware the Ides of March.
""")
>>> server.quit()
```

--------------------------------

### Robust HTTP Server with Custom SIGINT Handler

Source: https://docs.python.org/3/library/signal

An example of an HTTP server that avoids issues with KeyboardInterrupt by installing a custom SIGINT handler. This handler uses a socketpair to signal the main loop, allowing for a clean shutdown without directly catching KeyboardInterrupt.

```python
import signal
import socket
from selectors import DefaultSelector, EVENT_READ
from http.server import HTTPServer, SimpleHTTPRequestHandler

interrupt_read, interrupt_write = socket.socketpair()

def handler(signum, frame):
    print('Signal handler called with signal', signum)
    interrupt_write.send(b'\0')
signal.signal(signal.SIGINT, handler)

def serve_forever(httpd):
    sel = DefaultSelector()
    sel.register(interrupt_read, EVENT_READ)
    sel.register(httpd, EVENT_READ)

    while True:
        for key, _ in sel.select():
            if key.fileobj == interrupt_read:
                interrupt_read.recv(1)
                return
            if key.fileobj == httpd:
                httpd.handle_request()

print("Serving on port 8000")
httpd = HTTPServer(('', 8000), SimpleHTTPRequestHandler)
serve_forever(httpd)
print("Shutdown...")
```

--------------------------------

### dis.SETUP_WITH Opcode

Source: https://docs.python.org/3/genindex-S

Represents the SETUP_WITH opcode in Python's bytecode.

```APIDOC
SETUP_WITH
  Opcode for handling 'with' statements.
```

--------------------------------

### Python Multiprocessing Logging with Logging Thread and dictConfig

Source: https://docs.python.org/3/howto/logging-cookbook

This example showcases a more advanced multiprocessing logging setup using a separate logging thread in the main process. It leverages `logging.config.dictConfig` for flexible logging configuration, allowing different handlers and formatters for various loggers and levels. Worker processes send logs to a queue, which the logging thread processes and dispatches to the configured handlers.

```python
import logging
import logging.config
import logging.handlers
from multiprocessing import Process, Queue
import random
import threading
import time

def logger_thread(q):
    while True:
        record = q.get()
        if record is None:
            break
        logger = logging.getLogger(record.name)
        logger.handle(record)

def worker_process(q):
    qh = logging.handlers.QueueHandler(q)
    root = logging.getLogger()
    root.setLevel(logging.DEBUG)
    root.addHandler(qh)
    levels = [logging.DEBUG, logging.INFO, logging.WARNING, logging.ERROR,
              logging.CRITICAL]
    loggers = ['foo', 'foo.bar', 'foo.bar.baz',
               'spam', 'spam.ham', 'spam.ham.eggs']
    for i in range(100):
        lvl = random.choice(levels)
        logger = logging.getLogger(random.choice(loggers))
        logger.log(lvl, 'Message no. %d', i)

if __name__ == '__main__':
    q = Queue()
    d = {
        'version': 1,
        'formatters': {
            'detailed': {
                'class': 'logging.Formatter',
                'format': '%(asctime)s%(name)-15s%(levelname)-8s%(processName)-10s%(message)s'
            }
        },
        'handlers': {
            'console': {
                'class': 'logging.StreamHandler',
                'level': 'INFO',
            },
            'file': {
                'class': 'logging.FileHandler',
                'filename': 'mplog.log',
                'mode': 'w',
                'formatter': 'detailed',
            },
            'foofile': {
                'class': 'logging.FileHandler',
                'filename': 'mplog-foo.log',
                'mode': 'w',
                'formatter': 'detailed',
            },
            'errors': {
                'class': 'logging.FileHandler',
                'filename': 'mplog-errors.log',
                'mode': 'w',
                'level': 'ERROR',
                'formatter': 'detailed',
            },
        },
        'loggers': {
            'foo': {
                'handlers': ['foofile']
            }
        },
        'root': {
            'level': 'DEBUG',
            'handlers': ['console', 'file', 'errors']
        },
    }
    workers = []
    for i in range(5):
        wp = Process(target=worker_process, name='worker %d' % (i + 1), args=(q,)) # Corrected args
        workers.append(wp)
        wp.start()
    logging.config.dictConfig(d)
    lp = threading.Thread(target=logger_thread, args=(q,))
    lp.start()
    for wp in workers:
        wp.join()
    q.put(None)
    lp.join()
```

--------------------------------

### Reusable Context Manager Example with ExitStack (Reusing Instance)

Source: https://docs.python.org/3/library/contextlib

Illustrates the behavior of `ExitStack` when the same instance is reused across multiple `with` statements, showing how callbacks are executed.

```python
from contextlib import ExitStack

stack = ExitStack()

with stack:
    stack.callback(print, "Callback: from first context")
    print("Leaving first context")

with stack:
    stack.callback(print, "Callback: from second context")
    print("Leaving second context")

with stack:
    stack.callback(print, "Callback: from outer context")
    with stack:
        stack.callback(print, "Callback: from inner context")
        print("Leaving inner context")
    print("Leaving outer context")
```

--------------------------------

### Start HTTP Documentation Server

Source: https://docs.python.org/3/library/pydoc

Starts an HTTP server to serve documentation to web browsers. Specify a port number to listen on.

```shell
python -m pydoc -p <port_number>
```

--------------------------------

### Populating OptionParser with Option List

Source: https://docs.python.org/3/library/optparse

Demonstrates how to initialize an OptionParser by passing a list of pre-constructed Option instances. Each Option instance is created using the make_option() factory function, specifying arguments like short/long flags, action, type, and destination.

```python
option_list = [
    make_option("-f", "--filename",
                action="store", type="string", dest="filename"),
    make_option("-q", "--quiet",
                action="store_false", dest="verbose"),
    ]
parser = OptionParser(option_list=option_list)
```

--------------------------------

### Installing Additional Python Packages

Source: https://docs.python.org/3/using/mac

This snippet demonstrates how to install Python packages using pip, the standard package installer. It's crucial for extending Python's functionality.

```bash
# Install a package using pip
pip install package_name

# Upgrade pip
pip install --upgrade pip
```

--------------------------------

### Binary Extension Modules on iOS

Source: https://docs.python.org/3/using/ios

Explains the process of converting `.so` binary modules to dynamic frameworks for App Store compliance on iOS. Includes file structure and naming conventions.

```python
# Example: Importing a binary extension module '_whiz'
# Original .so file: sources/foo/bar/_whiz.abi3.so
# Distributed as framework: Frameworks/foo.bar._whiz.framework/foo.bar._whiz
# Marker file: sources/foo/bar/_whiz.abi3.fwork (contains path to framework)
# Origin file: Frameworks/foo.bar._whiz.framework/foo.bar._whiz.origin (contains path to .fwork file)

# When imported, __file__ will point to the .fwork file location.
# The ModuleSpec's origin will point to the framework binary location.

# Python interpreter uses AppleFrameworkLoader to handle .fwork files.
```

--------------------------------

### Main CLI Application Script (app.py)

Source: https://docs.python.org/3/howto/logging-cookbook

This Python script sets up argument parsing for a CLI application, including subcommands for 'start', 'stop', and 'restart'. It also configures basic logging and dispatches commands to dynamically imported modules.

```python
import argparse
import importlib
import logging
import os
import sys

defmain(args=None):
    scriptname = os.path.basename(__file__)
    parser = argparse.ArgumentParser(scriptname)
    levels = ('DEBUG', 'INFO', 'WARNING', 'ERROR', 'CRITICAL')
    parser.add_argument('--log-level', default='INFO', choices=levels)
    subparsers = parser.add_subparsers(dest='command',
                                       help='Available commands:')
    start_cmd = subparsers.add_parser('start', help='Start a service')
    start_cmd.add_argument('name', metavar='NAME',
                           help='Name of service to start')
    stop_cmd = subparsers.add_parser('stop',
                                     help='Stop one or more services')
    stop_cmd.add_argument('names', metavar='NAME', nargs='+',
                          help='Name of service to stop')
    restart_cmd = subparsers.add_parser('restart',
                                        help='Restart one or more services')
    restart_cmd.add_argument('names', metavar='NAME', nargs='+',
                             help='Name of service to restart')
    options = parser.parse_args()
    # the code to dispatch commands could all be in this file. For the purposes
    # of illustration only, we implement each command in a separate module.
    try:
        mod = importlib.import_module(options.command)
        cmd = getattr(mod, 'command')
    except (ImportError, AttributeError):
        print('Unable to find the code for command \'%s\'' % options.command)
        return 1
    # Could get fancy here and load configuration from file or dictionary
    logging.basicConfig(level=options.log_level,
                        format='%(levelname)s%(name)s%(message)s')
    cmd(options)

if __name__ == '__main__':
    sys.exit(main())

```

--------------------------------

### PEP 7: C API Introduction

Source: https://docs.python.org/3/genindex-P

Provides an introduction to the Python C API, covering its fundamental aspects and usage. Includes references to the C API introduction and configuration.

```python
PEP 7: https://docs.python.org/3/c-api/intro.html#index-0
References: https://docs.python.org/3/c-api/intro.html#index-1, https://docs.python.org/3/c-api/intro.html#index-2, https://docs.python.org/3/using/configure.html#index-0, https://docs.python.org/3/whatsnew/3.6.html#index-34
```

--------------------------------

### Python Memory Allocator Setup

Source: https://docs.python.org/3/c-api/memory

This section describes the process of installing a custom memory allocator in Python. It specifies that the custom allocator should be set up between Py_PreInitialize() and Py_InitializeFromConfig(). It also notes that if called after Python initialization, the custom allocator must wrap the existing one, and substituting it is not supported. Allocators must be thread-safe since Python 3.12.

```python
from ctypes import *

# Load the Python C API library (adjust path as needed)
libpython = cdll.LoadLibrary("libpython3.12.so") # Example for Linux

# Define function signatures (simplified for demonstration)
Py_PreInitialize = libpython.Py_PreInitialize
Py_InitializeFromConfig = libpython.Py_InitializeFromConfig

# Example of setting up a custom allocator (conceptual)
# In a real scenario, you would provide a C function pointer
# to your custom allocator implementation.
# PyMem_SetupCustomAllocator(domain, allocator)

# Example usage flow:
# Py_PreInitialize()
# ... setup custom allocator ...
# Py_InitializeFromConfig(config)

```

--------------------------------

### Installing Python using the Command Line

Source: https://docs.python.org/3/using/mac

This section details how to install Python and its related components directly from the command line interface on macOS, often using package managers.

```bash
# Example using Homebrew (a common macOS package manager)
brew install python

# Or to install a specific version
brew install python@3.11
```

--------------------------------

### ftplib FTP Client Example

Source: https://docs.python.org/3/library/ftplib

Demonstrates connecting to an FTP server, logging in anonymously, changing directories, listing contents, downloading a file, and quitting the connection.

```python
from ftplib import FTP

ftp = FTP('ftp.us.debian.org')  # connect to host, default port
ftp.login()                     # user anonymous, passwd anonymous@
ftp.cwd('debian')               # change into "debian" directory
ftp.retrlines('LIST')           # list directory contents

with open('README', 'wb') as fp:
    ftp.retrbinary('RETR README', fp.write)

ftp.quit()
```

--------------------------------

### Python Multiprocessing Logging with Listener Process

Source: https://docs.python.org/3/howto/logging-cookbook

This snippet demonstrates a multiprocessing setup where a dedicated listener process handles log messages from worker processes. It uses a `multiprocessing.Queue` to pass log records from workers to the listener. The main process starts the listener and worker processes, waits for workers to complete, and then signals the listener to finish.

```python
import multiprocessing

def listener_process(queue, configurer):
    # Listener process logic would go here
    pass

def worker_process(queue, configurer):
    # Worker process logic would go here
    pass

def main():
    queue = multiprocessing.Queue(-1)
    listener = multiprocessing.Process(target=listener_process,
                                       args=(queue, listener_configurer))
    listener.start()
    workers = []
    for i in range(10):
        worker = multiprocessing.Process(target=worker_process,
                                           args=(queue, worker_configurer))
        workers.append(worker)
        worker.start()
    for w in workers:
        w.join()
    queue.put_nowait(None)
    listener.join()

if __name__ == '__main__':
    main()
```

--------------------------------

### Formatted Output with print()

Source: https://docs.python.org/3/tutorial/introduction

Shows how to use the print() function to display variables and strings with custom formatting. It illustrates printing a string literal followed by the value of a variable, separated by a space.

```python
>>> i = 256*256
>>> print('The value of i is', i)
The value of i is 65536
```

--------------------------------

### Timing Functions with Setup Import

Source: https://docs.python.org/3/library/timeit

Shows how to time a function defined in the main script by using a setup statement with an import from __main__.

```python
def test():
    """Stupid test function"""
    L = [i for i in range(100)]

if __name__ == '__main__':
    import timeit
    print(timeit.timeit("test()", setup="from __main__ import test"))
```

--------------------------------

### Embedding Python in a C/C++ Application

Source: https://docs.python.org/3/using/windows

Provides a basic C code snippet demonstrating how to initialize the Python interpreter and run a simple Python string.

```c
#include <Python.h>

int main(int argc, char *argv[]) {
    Py_Initialize();
    PyRun_SimpleString("print('Hello from embedded Python!')");
    Py_Finalize();
    return 0;
}
```

--------------------------------

### Get Executable Prefix (Python C API)

Source: https://docs.python.org/3/c-api/init

Retrieves the exec-prefix for installed platform-dependent files. This value is derived from the program name and environment variables. It points to static storage and should not be modified. The value is available in Python as sys.base_exec_prefix. It is only meaningful on Unix-like systems. This function should be called after Py_Initialize().

```c
wchar_t* Py_GetExecPrefix();
```

--------------------------------

### Python Path Configuration Options

Source: https://docs.python.org/3/c-api/init_config

Details various configuration settings for Python 3's startup and path management, including environment variables and command-line arguments.

```APIDOC
Python Path Configuration:

  PYTHONEXECUTABLE: Environment variable to specify the Python executable on macOS.

  WITH_NEXT_FRAMEWORK: Macro that checks for __PYVENV_LAUNCHER__ environment variable.

  argv[0]: Uses argv[0] of PyConfig.argv if available and non-empty.

  Default executable: L"python" on Windows, L"python3" on other platforms.

Python Path Configuration:

  pycache_prefix: Directory for cached .pyc files. Set by -X pycache_prefix=PATH or PYTHONPYCACHEPREFIX environment variable. Command-line option takes precedence. If NULL, sys.pycache_prefix is None. Default: NULL.

  quiet: Quiet mode. If > 0, suppresses copyright and version at startup in interactive mode. Incremented by -q command line option. Default: 0.

  run_command: Value of the -c command line option. Used by Py_RunMain(). Default: NULL.

  run_filename: Filename passed on the command line (trailing argument without -c or -m). Used by Py_RunMain(). Example: 'script.py' for 'python3 script.py arg'. See also PyConfig.skip_source_first_line. Default: NULL.

  run_module: Value of the -m command line option. Used by Py_RunMain(). Default: NULL.

  run_presite: 'package.module' path to import before site.py. Set by -X presite=package.module or PYTHON_PRESITE environment variable. Command-line option takes precedence. Requires a debug build of Python (Py_DEBUG macro defined). Default: NULL.

  show_ref_count: Show total reference count at exit (excluding immortal objects)? Set to 1 by -X showrefcount command line option. Requires a debug build of Python (Py_REF_DEBUG macro defined). Default: 0.

  site_import: Import the site module at startup? If zero, disables site module import and site-dependent sys.path manipulations.
```

--------------------------------

### Python Shebang Line Example

Source: https://docs.python.org/3/using/windows

Demonstrates a basic shebang line for executing a Python script on Unix-like systems and Windows.

```python
#! /usr/bin/python


```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/.10

Lists essential external resources for Python developers, including the Python Enhancement Proposals (PEP) index, guides for beginners, book recommendations, talks, and the developer's guide.

```text
### Other resources
  * [PEP Index](https://peps.python.org/)
  * [Beginner's Guide](https://wiki.python.org/moin/BeginnersGuide)
  * [Book List](https://wiki.python.org/moin/PythonBooks)
  * [Audio/Visual Talks](https://www.python.org/doc/av/)
  * [Python Developer’s Guide](https://devguide.python.org/)
```

--------------------------------

### Python Installation on Windows (No UI)

Source: https://docs.python.org/3/contents

This snippet demonstrates how to perform a silent installation of Python on Windows without a user interface. This is useful for automated deployments or scripting.

```powershell
msiexec /i python-3.x.msi /quiet InstallAllUsers=1 PrependPath=1
```

--------------------------------

### Multiprocessing Start Method Management

Source: https://docs.python.org/3/library/multiprocessing

Provides functions to control how child processes are started in Python's multiprocessing module. This includes setting the executable path, retrieving the current start method, and defining the start method for new processes.

```APIDOC
multiprocessing.get_start_method(_allow_none =False_)
    Return the name of start method used for starting processes.
    If the global start method has not been set and _allow_none_ is `False`, then the start method is set to the default and the name is returned. If the start method has not been set and _allow_none_ is `True` then `None` is returned.
    The return value can be `'fork'`, `'spawn'`, `'forkserver'` or `None`.
    Added in version 3.4.
    Changed in version 3.8: On macOS, the _spawn_ start method is now the default. The _fork_ start method should be considered unsafe as it can lead to crashes of the subprocess.

multiprocessing.set_executable(_executable_)
    Set the path of the Python interpreter to use when starting a child process. (By default [`sys.executable`](https://docs.python.org/3/library/sys.html#sys.executable "sys.executable") is used).
    Changed in version 3.4: Now supported on POSIX when the `'spawn'` start method is used.
    Changed in version 3.11: Accepts a [path-like object](https://docs.python.org/3/glossary.html#term-path-like-object).

multiprocessing.set_forkserver_preload(_module_names_)
    Set a list of module names for the forkserver main process to attempt to import so that their already imported state is inherited by forked processes. Any [`ImportError`](https://docs.python.org/3/library/exceptions.html#ImportError "ImportError") when doing so is silently ignored. This can be used as a performance enhancement to avoid repeated work in every process.
    For this to work, it must be called before the forkserver process has been launched.
    Only meaningful when using the `'forkserver'` start method.
    Added in version 3.4.

multiprocessing.set_start_method(_method_ , _force =False_)
    Set the method which should be used to start child processes. The _method_ argument can be `'fork'`, `'spawn'` or `'forkserver'`. Raises [`RuntimeError`](https://docs.python.org/3/library/exceptions.html#RuntimeError "RuntimeError") if the start method has already been set and _force_ is not `True`. If _method_ is `None` and _force_ is `True` then the start method is set to `None`. If _method_ is `None` and _force_ is `False` then the context is set to the default context.
    Note that this should be called at most once, and it should be protected inside the `if __name__ == '__main__'` clause of the main module.
    Added in version 3.4.
    Note: If _method_ is `None` then the default context is returned. Note that if the global start method has not been set, this will set it to the default method. Otherwise _method_ should be `'fork'`, `'spawn'`, `'forkserver'`. [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError "ValueError") is raised if the specified start method is not available.
```

--------------------------------

### Multiprocessing Task Execution with Queues

Source: https://docs.python.org/3/library/multiprocessing

This Python code demonstrates a common pattern for parallel task execution using the `multiprocessing` module. It sets up a task queue and a results queue, starts multiple worker processes, distributes tasks, and collects results. The example includes a mechanism to signal workers to terminate.

```python
from multiprocessing import Process, Queue
from multiprocessing.context import freeze_support

def mul(x, y):
    return x * y

def plus(x, y):
    return x + y

def worker(task_queue, done_queue):
    while True:
        task = task_queue.get()
        if task == 'STOP':
            break
        func, args = task
        result = func(*args)
        done_queue.put(result)

def test():
    NUMBER_OF_PROCESSES = 4
    TASKS1 = [(mul, (i, 7)) for i in range(20)]
    TASKS2 = [(plus, (i, 8)) for i in range(10)]

    task_queue = Queue()
    done_queue = Queue()

    for task in TASKS1:
        task_queue.put(task)

    for i in range(NUMBER_OF_PROCESSES):
        Process(target=worker, args=(task_queue, done_queue)).start()

    print('Unordered results:')
    for i in range(len(TASKS1)):
        print('\t', done_queue.get())

    for task in TASKS2:
        task_queue.put(task)

    for i in range(len(TASKS2)):
        print('\t', done_queue.get())

    for i in range(NUMBER_OF_PROCESSES):
        task_queue.put('STOP')


if __name__ == '__main__':
    freeze_support()
    test()
```

--------------------------------

### Python Other Resources

Source: https://docs.python.org/3/.14

Lists additional resources for Python developers, including the PEP Index, Beginner's Guide, Book List, Audio/Visual Talks, and the Python Developer's Guide.

```python
print("PEP Index")
# Link: https://peps.python.org/

print("Beginner's Guide")
# Link: https://wiki.python.org/moin/BeginnersGuide

print("Book List")
# Link: https://wiki.python.org/moin/PythonBooks

print("Audio/Visual Talks")
# Link: https://www.python.org/doc/av/

print("Python Developer’s Guide")
# Link: https://devguide.python.org/
```

--------------------------------

### Python Doctest Example Recognition

Source: https://docs.python.org/3/library/doctest

Demonstrates how doctest recognizes code examples and their expected output from Python docstrings. It shows multi-line statements, conditional logic, and how output is captured.

```python
>>> # comments are ignored
>>> x = 12
>>> x
12
>>> if x == 13:
...     print("yes")
... else:
...     print("no")
...     print("NO")
...     print("NO!!!")
... 
no
NO
NO!!!
>>>
```

--------------------------------

### Bundling Python Applications

Source: https://docs.python.org/3/using/windows

Provides advice for developers bundling Python into their applications to prevent conflicts with existing installations.

```python
# Use a ._pth file alongside your executable to specify include directories.
# This ignores registry and environment variables, and site unless 'import site' is listed.
```

```python
# When loading python3.dll or python37.dll, explicitly set PyConfig.module_search_paths
# before calling Py_InitializeFromConfig().
```

```python
# Clear/overwrite PYTHONPATH and set PYTHONHOME before launching python.exe from your application.
```

```python
# Ensure the landmark file (Lib\os.py) exists in your install directory if other suggestions cannot be used.
```

--------------------------------

### Other Python Resources Links

Source: https://docs.python.org/3/.12

Provides links to essential Python resources beyond version-specific documentation, including the PEP Index, beginner guides, book lists, talks, and the developer's guide.

```python
print("PEP Index: https://peps.python.org/")
print("Beginner's Guide: https://wiki.python.org/moin/BeginnersGuide")
print("Book List: https://wiki.python.org/moin/PythonBooks")
print("Audio/Visual Talks: https://www.python.org/doc/av/")
print("Python Developer’s Guide: https://devguide.python.org/")
```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/.15

Lists important external resources for Python developers, including the PEP Index, Beginner's Guide, Book List, Audio/Visual Talks, and the Python Developer's Guide.

```python
print('PEP Index: https://peps.python.org/')
print('Beginner\'s Guide: https://wiki.python.org/moin/BeginnersGuide')
print('Book List: https://wiki.python.org/moin/PythonBooks')
print('Audio/Visual Talks: https://www.python.org/doc/av/')
print('Python Developer\'s Guide: https://devguide.python.org/')
```

--------------------------------

### Create and Send Simple Text Email

Source: https://docs.python.org/3/library/email-examples

Demonstrates creating a simple text email message using the `EmailMessage` class and sending it via `smtplib`. It handles reading content from a file and setting email headers like Subject, From, and To. The example assumes `textfile`, `me`, and `you` are defined elsewhere.

```python
import smtplib
from email.message import EmailMessage

# Assuming textfile, me, and you are defined
# with open(textfile) as fp:
#     msg = EmailMessage()
#     msg.set_content(fp.read())

# msg['Subject'] = f'The contents of {textfile}'
# msg['From'] = me
# msg['To'] = you

# s = smtplib.SMTP('localhost')
# s.send_message(msg)
# s.quit()
```

--------------------------------

### Porting to Python 3.3 Guide

Source: https://docs.python.org/3/contents

This guide provides essential information and steps for porting existing Python codebases to Python 3.3, addressing potential compatibility issues.

```python
# Porting to Python 3.3
# Guidance and best practices for migrating code to Python 3.3.
```

--------------------------------

### Debugging Doctest Example with pdb.set_trace()

Source: https://docs.python.org/3/library/doctest

Demonstrates how to insert `pdb.set_trace()` within a doctest example to enter the Python debugger for post-mortem analysis of variables and execution flow.

```python
"""
>>> def f(x):
...     g(x*2)
>>> def g(x):
...     print(x+3)
...     import pdb; pdb.set_trace()
>>> f(3)
9
"""

```

--------------------------------

### IDLE Startup and Code Execution

Source: https://docs.python.org/3/library/idle

Explains how to start IDLE, execute Python code, and manage user output within the shell. It also covers command-line usage, handling startup failures, developing tkinter applications, and running IDLE without a subprocess.

```python
Startup and Code Execution:
- Command line usage
- Startup failure
- Running user code
- User output in Shell
- Developing tkinter applications
- Running without a subprocess
```

--------------------------------

### Python String format() - Dictionary Unpacking

Source: https://docs.python.org/3/tutorial/inputoutput

Shows how to use the ** operator to unpack a dictionary as keyword arguments for str.format().

```python
table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table))
```

--------------------------------

### DocTestParser API

Source: https://docs.python.org/3/library/doctest

Provides methods to parse doctest examples from strings and create DocTest objects. It handles extraction of interactive examples and their organization.

```APIDOC
DocTestParser:
  get_doctest(_string_, _globs_, _name_, _filename_, _lineno_)
    Extracts all doctest examples from a string into a DocTest object.
    Parameters:
      _string_: The string containing doctest examples.
      _globs_: Attributes for the new DocTest object.
      _name_: Name for the DocTest object.
      _filename_: Filename associated with the doctest.
      _lineno_: Starting line number for the doctest.
    Returns: A DocTest object containing the extracted examples.

  get_examples(_string_, _name='<string>')
    Extracts all doctest examples from a string and returns them as a list of Example objects.
    Parameters:
      _string_: The string containing doctest examples.
      _name_: An optional name for the string, used for error messages.
    Returns: A list of Example objects.

  parse(_string_, _name='<string>')
    Divides a string into examples and intervening text, returning a list of alternating Example objects and strings.
    Parameters:
      _string_: The string to parse.
      _name_: An optional name for the string, used for error messages.
    Returns: A list of alternating Example objects and strings.
```

--------------------------------

### Python Installation Path Configuration

Source: https://docs.python.org/3/using/windows

This section discusses ensuring system-wide installations do not override application-bundled standard libraries. It mentions support for `._pth` files and changes related to `python_XX_.zip` landmarks and registry-based module finding.

```text
These will ensure that the files in a system-wide installation will not take precedence over the copy of the standard library bundled with your application. Otherwise, your users may experience problems using your application. Note that the first suggestion is the best, as the others may still be susceptible to non-standard paths in the registry and user site-packages.
Changed in version 3.6: Add `._pth` file support and removes `applocal` option from `pyvenv.cfg`.
Changed in version 3.6: Add `python_XX_.zip`as a potential landmark when directly adjacent to the executable.
Deprecated since version 3.6: Modules specified in the registry under `Modules` (not `PythonPath`) may be imported by [`importlib.machinery.WindowsRegistryFinder`](https://docs.python.org/3/library/importlib.html#importlib.machinery.WindowsRegistryFinder "importlib.machinery.WindowsRegistryFinder"). This finder is enabled on Windows in 3.6.0 and earlier, but may need to be explicitly added to [`sys.meta_path`](https://docs.python.org/3/library/sys.html#sys.meta_path "sys.meta_path") in the future.
```

--------------------------------

### Python sysconfig Installation Path Functions

Source: https://docs.python.org/3/library/sysconfig

Provides functions to determine Python installation paths and configuration schemes. These functions are useful for understanding where Python packages and modules are installed.

```python
import sysconfig

# Get all supported scheme names
scheme_names = sysconfig.get_scheme_names()
print(f"Supported schemes: {scheme_names}")

# Get the default scheme name for the current platform
default_scheme = sysconfig.get_default_scheme()
print(f"Default scheme: {default_scheme}")

# Get a preferred scheme name for a given key
prefix_scheme = sysconfig.get_preferred_scheme("prefix")
print(f"Preferred scheme for 'prefix': {prefix_scheme}")

# Get all supported path names
path_names = sysconfig.get_path_names()
print(f"Supported path names: {path_names}")

# Get a specific installation path for a given name and scheme
stdlib_path = sysconfig.get_path("stdlib", "posix_prefix")
print(f"Standard library path (posix_prefix): {stdlib_path}")

# Get a path with custom variables and without expansion
custom_vars = {"base": "/my/custom/path"}
custom_path = sysconfig.get_path("purelib", "posix_prefix", custom_vars, False)
print(f"Custom purelib path (not expanded): {custom_path}")
```

--------------------------------

### IDLE Startup and Code Execution

Source: https://docs.python.org/3/contents

Information on how IDLE starts up, executes user code, and handles output. Covers command-line usage, startup failures, running code in subprocesses, and developing Tkinter applications.

```APIDOC
IDLE Startup and Code Execution:

Command Line Usage:
  idle [options]
  Options include -n (no default config), -r <file> (run file), -s <file> (run file in shell).

Startup Failure:
  Troubleshooting steps for when IDLE fails to start.

Running User Code:
  Executing Python scripts from the editor or interactively in the shell.

User Output in Shell:
  Displaying output from executed code, including print statements and exceptions.

Developing Tkinter Applications:
  Tips for using IDLE to develop GUI applications with Tkinter.

Running Without a Subprocess:
  Option to run user code in the main IDLE process, useful for debugging.
```

--------------------------------

### Installing Python Modules: System Python on Linux

Source: https://docs.python.org/3/contents

Specific advice for installing Python packages into the system's default Python installation on Linux systems. This often requires elevated privileges and careful consideration.

```APIDOC
Installing into the system Python on Linux:
  Provides guidance on installing packages into the system-wide Python installation on Linux.
  Highlights potential permission issues and best practices.
```

--------------------------------

### Convert Doctest Examples to Python Script

Source: https://docs.python.org/3/library/doctest

Utilizes the `doctest.script_from_examples()` function to convert a string containing doctest examples into a runnable Python script. Non-example text is converted to comments.

```python
import doctest
print(doctest.script_from_examples(r"""
    Set x and y to 1 and 2.
    >>> x, y = 1, 2

    Print their sum:
    >>> print(x+y)
    3
"""))

```

--------------------------------

### Python Instrumentation HOWTO

Source: https://docs.python.org/3/howto/instrumentation

This section provides links to various aspects of instrumenting CPython, including enabling static markers, understanding static DTrace probes, static SystemTap markers, available static markers, SystemTap tapsets, and examples.

```python
# This is a documentation reference, not executable code.
# Links to specific sections within the HOWTO:
# - Enabling the static markers
# - Static DTrace probes
# - Static SystemTap markers
# - Available static markers
# - SystemTap Tapsets
# - Examples
```

--------------------------------

### Python Documentation Metadata

Source: https://docs.python.org/3/tutorial/introduction

Provides metadata about the Python documentation, including the last updated date and the tool used to generate the documentation.

```python
Last updated on Aug 17, 2025 (07:57 UTC). [Found a bug](https://docs.python.org/bugs.html)?   
Created using [Sphinx](https://www.sphinx-doc.org/) 8.2.3.
```

--------------------------------

### Doctest Example with Ellipsis on Separate Line

Source: https://docs.python.org/3/library/doctest

Provides an example where the '...' directive is placed on a separate line, followed by the actual output with the ellipsis. This is useful for long examples where directives might clutter the code line.

```python
>>> print(list(range(5)) + list(range(10, 20)) + list(range(30, 40)))
... # doctest: +ELLIPSIS
[0, ..., 4, 10, ..., 19, 30, ..., 39]

```

--------------------------------

### Python String format() - Combined Arguments

Source: https://docs.python.org/3/tutorial/inputoutput

Demonstrates the flexibility of str.format() by combining positional and keyword arguments in a single call.

```python
print('The story of {0}, {1}, and {other}.'.format('Bill', 'Manfred',
                                                     other='Georg'))
```

--------------------------------

### __format__ Method Implementation Example

Source: https://docs.python.org/3/whatsnew/2

Provides an example of how a class can implement the `__format__()` method to customize its string formatting behavior based on the provided format specifier.

```python
def __format__(self, format_spec):
    if isinstance(format_spec, unicode):
        return unicode(str(self))
    else:
        return str(self)
```

--------------------------------

### Python 3 Documentation Navigation

Source: https://docs.python.org/3/tutorial/whatnow

Provides links to various sections of the Python 3 documentation, including the general index, module index, and specific tutorial chapters. It also lists available Python versions and theme options.

```python
## Navigation
  * [index](https://docs.python.org/3/genindex.html "General Index")
  * [modules](https://docs.python.org/3/py-modindex.html "Python Module Index") | 
  * [next](https://docs.python.org/3/tutorial/interactive.html "14. Interactive Input Editing and History Substitution") | 
  * [previous](https://docs.python.org/3/tutorial/venv.html "12. Virtual Environments and Packages") | 
  * [Python](https://www.python.org/) »
  * Greek | Ελληνικά English Spanish | español French | français Italian | italiano Japanese | 日本語 Korean | 한국어 Polish | polski Brazilian Portuguese | Português brasileiro Turkish | Türkçe Simplified Chinese | 简体中文 Traditional Chinese | 繁體中文
  dev (3.15) pre (3.14) 3.13.7 3.12 3.11 3.10 3.9 3.8 3.7 3.6 3.5 3.4 3.3 3.2 3.1 3.0 2.7 2.6
  * [3.13.7 Documentation](https://docs.python.org/3/index.html) » 
  * [The Python Tutorial](https://docs.python.org/3/tutorial/index.html) »
  * [13. What Now?](https://docs.python.org/3/tutorial/whatnow.html)
  * | 
  * Theme  Auto Light Dark |
```

--------------------------------

### Complete Script for Custom Handler Example

Source: https://docs.python.org/3/howto/logging-cookbook

A full Python script demonstrating the use of a custom file handler with dictConfig to set file ownership. It includes the handler function, the logging configuration, and a sample log message.

```python
import logging
import logging.config
import os
import shutil

def owned_file_handler(filename, mode='a', encoding=None, owner=None):
    if owner:
        if not os.path.exists(filename):
            open(filename, 'a').close()
        shutil.chown(filename, *owner)
    return logging.FileHandler(filename, mode, encoding)

LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'default': {
            'format': '%(asctime)s%(levelname)s%(name)s%(message)s'
        },
    },
    'handlers': {
        'file':{
            '()': owned_file_handler,
            'level':'DEBUG',
            'formatter': 'default',
            'owner': ['pulse', 'pulse'],
            'filename': 'chowntest.log',
            'mode': 'w',
            'encoding': 'utf-8',
        },
    },
    'root': {
        'handlers': ['file'],
        'level': 'DEBUG',
    },
}

logging.config.dictConfig(LOGGING)
logger = logging.getLogger('mylogger')
logger.debug('A debug message')
```

--------------------------------

### Python socketserver.BaseRequestHandler Method

Source: https://docs.python.org/3/genindex-S

Documentation for the setup method in socketserver.BaseRequestHandler, called before handling a request.

```APIDOC
socketserver.BaseRequestHandler.setup()
  - Called before handling a request. Can be overridden.
```

--------------------------------

### ast.dump Output Example

Source: https://docs.python.org/3/library/ast

Provides an example output of ast.dump when used with specific formatting options on an async function definition.

```python
Module(
    body=[
        AsyncFunctionDef(
            name='f',
            args=arguments(
                posonlyargs=[],
                args=[],
                kwonlyargs=[],
                kw_defaults=[],
                defaults=[]),
            body=[
                Expr(
                    value=Await(
                        value=Call(
                            func=Name(id='other_func', ctx=Load()),
                            args=[],
                            keywords=[])))
            ],
            decorator_list=[],
            type_params=[])
    ],
    type_ignores=[])
```

--------------------------------

### Python IMAP4 Example

Source: https://docs.python.org/3/library/imaplib

A minimal Python example demonstrating how to connect to an IMAP server, log in, select a mailbox, search for all messages, fetch and print each message's content, and then close the connection.

```python
importgetpass,imaplib

M = imaplib.IMAP4(host='example.org')
M.login(getpass.getuser(), getpass.getpass())
M.select()
typ, data = M.search(None, 'ALL')
for num in data[0].split():
    typ, data = M.fetch(num, '(RFC822)')
    print('Message %s\n%s\n' % (num, data[0][1]))
M.close()
M.logout()
```

--------------------------------

### Importing a Source File Directly

Source: https://docs.python.org/3/library/modules

Provides an example of importing a Python source file directly using `importlib.util.spec_from_file_location` and `importlib.util.module_from_spec`.

```python
import importlib.util
import sys

file_path = "/path/to/your/module.py"
module_name = "my_custom_module"

spec = importlib.util.spec_from_file_location(module_name, file_path)

if spec and spec.loader:
    my_module = importlib.util.module_from_spec(spec)
    sys.modules[module_name] = my_module
    spec.loader.exec_module(my_module)
    # Now you can use my_module
    # my_module.some_function()
else:
    print(f"Could not load module from {file_path}")
```

--------------------------------

### Asyncio Stream Functions API Documentation

Source: https://docs.python.org/3/library/asyncio-stream

API documentation for asyncio stream functions, detailing their parameters, return values, and usage for establishing network connections and starting servers.

```APIDOC
asyncio.open_connection(_host=None, _port=None, *_ , _limit=None, _ssl=None, _family=0, _proto=0, _flags=0, _sock=None, _local_addr=None, _server_hostname=None, _ssl_handshake_timeout=None, _ssl_shutdown_timeout=None, _happy_eyeballs_delay=None, _interleave=None)
    Establish a network connection and return a pair of (reader, writer) objects.
    Parameters:
        _host_: The host to connect to.
        _port_: The port to connect to.
        _limit_: Buffer size limit for StreamReader. Defaults to 64 KiB.
        _ssl_: SSL context for the connection.
        _family_: Address family (e.g., socket.AF_INET).
        _proto_: Protocol.
        _flags_: Socket flags.
        _sock_: Existing socket object.
        _local_addr_: Local address to bind to.
        _server_hostname_: Server hostname for SSL.
        _ssl_handshake_timeout_: Timeout for SSL handshake.
        _ssl_shutdown_timeout_: Timeout for SSL shutdown.
        _happy_eyeballs_delay_: Delay for Happy Eyeballs algorithm.
        _interleave_: Interleave parameter for Happy Eyeballs.
    Returns: A tuple of (StreamReader, StreamWriter) objects.
    Note: The _sock_ argument transfers ownership of the socket.
    Changed in version 3.7: Added _ssl_handshake_timeout_.
    Changed in version 3.8: Added _happy_eyeballs_delay_ and _interleave_.
    Changed in version 3.10: Removed _loop_ parameter.
    Changed in version 3.11: Added _ssl_shutdown_timeout_.

asyncio.start_server(_client_connected_cb_, _host=None, _port=None, *_ , _limit=None, _family=socket.AF_UNSPEC, _flags=socket.AI_PASSIVE, _sock=None, _backlog=100, _ssl=None, _reuse_address=None, _reuse_port=None, _keep_alive=None, _ssl_handshake_timeout=None, _ssl_shutdown_timeout=None, _start_serving=True)
    Start a socket server.
    Parameters:
        _client_connected_cb_: Callback for new client connections, receives (reader, writer).
        _host_: The host to bind the server to.
        _port_: The port to bind the server to.
        _limit_: Buffer size limit for StreamReader. Defaults to 64 KiB.
        _family_: Address family.
        _flags_: Socket flags.
        _sock_: Existing socket object.
        _backlog_: Maximum number of queued connections.
        _ssl_: SSL context for the server.
        _reuse_address_: Whether to reuse the address.
        _reuse_port_: Whether to reuse the port.
        _keep_alive_: Keep-alive setting.
        _ssl_handshake_timeout_: Timeout for SSL handshake.
        _ssl_shutdown_timeout_: Timeout for SSL shutdown.
        _start_serving_: Whether to start serving immediately.
    Note: The _sock_ argument transfers ownership of the socket.
    Changed in version 3.7: Added _ssl_handshake_timeout_ and _start_serving_.
    Changed in version 3.10: Removed _loop_ parameter.
```

--------------------------------

### Python Language Reference - Introduction

Source: https://docs.python.org/3/reference/introduction

This section provides an overview of the Python programming language reference manual. It clarifies the manual's purpose, its balance between precision and readability, and the inclusion of implementation-specific notes for CPython. It also mentions the interaction with built-in and standard modules.

```python
This reference manual describes the Python programming language. It is not intended as a tutorial.
While I am trying to be as precise as possible, I chose to use English rather than formal specifications for everything except syntax and lexical analysis. This should make the document more understandable to the average reader, but will leave room for ambiguities.
Consequently, if you were coming from Mars and tried to re-implement Python from this document alone, you might have to guess things and in fact you would probably end up implementing quite a different language. On the other hand, if you are using Python and wonder what the precise rules about a particular area of the language are, you should definitely be able to find them here. If you would like to see a more formal definition of the language, maybe you could volunteer your time — or invent a cloning machine :-).
It is dangerous to add too many implementation details to a language reference document — the implementation may change, and other implementations of the same language may work differently. On the other hand, CPython is the one Python implementation in widespread use (although alternate implementations continue to gain support), and its particular quirks are sometimes worth being mentioned, especially where the implementation imposes additional limitations. Therefore, you’ll find short “implementation notes” sprinkled throughout the text.
Every Python implementation comes with a number of built-in and standard modules. These are documented in [The Python Standard Library](https://docs.python.org/3/library/index.html#library-index). A few built-in modules are mentioned when they interact in a significant way with the language definition.
```

--------------------------------

### Asyncio Future Usage Example

Source: https://docs.python.org/3/library/asyncio-future

An example demonstrating the creation of an asyncio Future, scheduling a coroutine to set its result, and awaiting the Future's completion.

```python
import asyncio
import functools

async def set_after(fut, delay, value):
    # Sleep for *delay* seconds.
    await asyncio.sleep(delay)

    # Set *value* as a result of *fut* Future.
    fut.set_result(value)

async def main():
    # Get the current event loop.
    loop = asyncio.get_running_loop()

    # Create a new Future object.
    fut = loop.create_future()

    # Run "set_after()" coroutine in a parallel Task.
    loop.create_task(
        set_after(fut, 1, '... world'))

    print('hello ...')

    # Wait until *fut* has a result (1 second) and print it.
    print(await fut)

asyncio.run(main())
```

--------------------------------

### MSIE 6 User Agent String Example

Source: https://docs.python.org/3/howto/urllib2

This entry provides an example of the User-Agent string commonly used by Internet Explorer 6 on Windows NT 5.1. This information is relevant for understanding browser sniffing and how websites might differentiate content based on the client's browser.

```text
Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)
```

--------------------------------

### Python/C API Navigation and Versioning

Source: https://docs.python.org/3/c-api/sys

Provides links to different sections of the Python/C API documentation, including general index, module index, and specific versions of Python. Also includes language selection and theme options.

```APIDOC
Navigation:
  - General Index: https://docs.python.org/3/genindex.html
  - Module Index: https://docs.python.org/3/py-modindex.html
  - Previous Section: https://docs.python.org/3/c-api/utilities.html
  - Next Section: https://docs.python.org/3/c-api/import.html

Python Versions:
  - Latest (3.13.7):
    - Full Documentation: https://docs.python.org/3/index.html
    - C API Reference: https://docs.python.org/3/c-api/index.html
  - Other Supported Versions: 3.12, 3.11, 3.10, 3.9, 3.8, 3.7, 3.6, 3.5, 3.4, 3.3, 3.2, 3.1, 3.0, 2.7, 2.6

Language Options:
  - Greek | Ελληνικά
  - English
  - Spanish | español
  - French | français
  - Italian | italiano
  - Japanese | 日本語
  - Korean | 한국어
  - Polish | polski
  - Brazilian Portuguese | Português brasileiro
  - Turkish | Türkçe
  - Simplified Chinese | 简体中文
  - Traditional Chinese | 繁體中文

Theme Options:
  - Auto
  - Light
  - Dark
```

--------------------------------

### Python Site Module - User Customization

Source: https://docs.python.org/3/library/python

Explains how to use 'usercustomize' for user-specific Python environment customizations, allowing individual users to modify their Python setup.

```python
# usercustomize.py - Example for user-specific configuration

import os

print('Running usercustomize.py')
os.environ['MY_CUSTOM_VAR'] = 'user_value'
```

--------------------------------

### PEP 636 - More `match` Statement Examples

Source: https://docs.python.org/3/genindex-P

Provides additional examples and use cases for the `match` statement, introduced by PEP 636, enhancing control flow in Python.

```python
See PEP 636 for more match statement examples.
```

--------------------------------

### Doctest Example with Multiple Directives

Source: https://docs.python.org/3/library/doctest

Illustrates combining multiple doctest directives on a single line, separated by commas. This example uses both '+ELLIPSIS' and '+NORMALIZE_WHITESPACE' to manage output variations.

```python
>>> print(list(range(20)))  # doctest: +ELLIPSIS, +NORMALIZE_WHITESPACE
[0,    1, ...,   18,    19]

```

--------------------------------

### Doctest Example with ELLIPSIS

Source: https://docs.python.org/3/library/doctest

Shows how to use the '+ELLIPSIS' directive to allow for variable parts in the output of a doctest example. The '...' placeholder matches any sequence of characters, making the test more flexible.

```python
>>> print(list(range(20)))  # doctest: +ELLIPSIS
[0, 1, ..., 18, 19]

```

--------------------------------

### Installing Python Modules: Common Issues

Source: https://docs.python.org/3/contents

This section addresses common problems encountered during Python module installation, including system-specific issues and dependency conflicts.

```APIDOC
Common installation issues:
  Covers typical challenges faced during Python package installation.
  Includes troubleshooting steps for system Python, pip, and binary extensions.
```

--------------------------------

### unittest setUpClass and tearDownClass Fixtures

Source: https://docs.python.org/3/library/unittest

Explains the use of `setUpClass` and `tearDownClass` methods for setting up and tearing down resources once per test class.

```python
import unittest

class FixtureExample(unittest.TestCase):
    @classmethod
    def setUpClass(cls):
        cls.resource = "Shared Resource"
        print("\nSetting up class")

    @classmethod
    def tearDownClass(cls):
        print("\nTearing down class")

    def test_one(self):
        self.assertIn("Resource", self.resource)

    def test_two(self):
        self.assertIn("Resource", self.resource)
```

--------------------------------

### Examples of bisect Usage

Source: https://docs.python.org/3/library/bisect

Illustrative examples demonstrating how to use the bisect module for common tasks like inserting multiple items, finding elements, and managing sorted lists.

```python
import bisect

data = []
for _ in range(5):
    bisect.insort(data, int(input('Enter an integer: ')))

print('Sorted list:', data)

search_val = int(input('Enter a value to find: '))
index = bisect.bisect_left(data, search_val)

if index < len(data) and data[index] == search_val:
    print(f'{search_val} found at index {index}')
else:
    print(f'{search_val} not found, would be inserted at index {index}')
```

--------------------------------

### Enabling Python UTF-8 Mode via Preinitialization

Source: https://docs.python.org/3/c-api/init_config

This example demonstrates how to use the Python C API to preinitialize the interpreter and enable UTF-8 mode. It shows the steps of configuring PyPreConfig, calling Py_PreInitialize, and then proceeding with the standard Python initialization.

```c
PyStatus status;
PyPreConfig preconfig;
PyPreConfig_InitPythonConfig(&preconfig);

preconfig.utf8_mode=1;

status=Py_PreInitialize(&preconfig);
if(PyStatus_Exception(status)){
Py_ExitStatusException(status);
}

/* at this point, Python speaks UTF-8 */

Py_Initialize();
/* ... use Python API here ... */
Py_Finalize();

```

--------------------------------

### Doctest Example with Directives on Separate Lines

Source: https://docs.python.org/3/library/doctest

Demonstrates how to use multiple directive comments for a single example when the directives do not fit on the same line as the code. This approach combines directives from different comment lines.

```python
>>> print(list(range(20)))  # doctest: +ELLIPSIS
...                         # doctest: +NORMALIZE_WHITESPACE
[0,    1, ...,   18,    19]

```

--------------------------------

### socketserver.UDPServer Example

Source: https://docs.python.org/3/library/socketserver

Illustrates how to create a UDP server using the socketserver.UDPServer class. This example shows handling incoming UDP datagrams and sending responses.

```python
import socketserver

class MyUDPHandler(socketserver.BaseRequestHandler):
    """
    This class provides the handle() method - the individual
    handling of an incoming request.
    """

    def handle(self):
        data = self.request[0].strip()
        socket = self.request[1]
        print(f"{self.client_address[0]} wrote: {data.decode()}")
        socket.sendto(data.upper(), self.client_address)

if __name__ == "__main__":
    HOST, PORT = "localhost", 9999
    # Create the server, binding to localhost on port 9999
    with socketserver.UDPServer((HOST, PORT), MyUDPHandler) as server:
        # Activate the server; this will keep running until you
        # interrupt the program with Ctrl-C
        server.serve_forever()
```

--------------------------------

### Python Standard Library Overview

Source: https://docs.python.org/3/tutorial/stdlib

This section outlines the key areas covered by the Python standard library, including modules for interacting with the operating system, handling files, processing command-line arguments, managing errors, pattern matching, mathematical operations, network access, date and time manipulation, data compression, performance analysis, and quality assurance.

```python
import os
import sys
import re
import math
import urllib.request
import datetime
import zlib
import time
import unittest

```

--------------------------------

### Python Interpreter Invocation and Modes

Source: https://docs.python.org/3/tutorial/index

Demonstrates how to invoke the Python interpreter, pass arguments, and utilize interactive mode. Covers environment setup and source code encoding.

```python
python [option] ... [-c cmd | -m mod | file | -] [arg] ...

# Example of invoking the interpreter with a script:
python my_script.py arg1 arg2

# Example of interactive mode:
python
>>> print('Hello, Python!')
Hello, Python!
>>> exit()

# Example of source code encoding:
# -*- coding: utf-8 -*-
print("Hello with unicode!")
```

--------------------------------

### Upgrade Existing Package

Source: https://docs.python.org/3/installing/index

Explicitly requests to upgrade an already installed package to the latest version.

```bash
pip install --upgrade <package-name>
```

--------------------------------

### Example Python Script for Profiling

Source: https://docs.python.org/3/howto/perf_profiling

A sample Python script demonstrating nested function calls, suitable for testing with the perf profiler.

```python
def foo(n):
    result = 0
    for _ in range(n):
        result += 1
    return result

def bar(n):
    foo(n)

def baz(n):
    bar(n)

if __name__ == "__main__":
    baz(1000000)

```

--------------------------------

### Python File I/O - Reading and Writing

Source: https://docs.python.org/3/contents

Provides examples of reading from and writing to files in Python. It covers opening files, reading content, writing data, and the importance of closing files or using `with` statements.

```python
# Writing to a file
with open('example.txt', 'w') as f:
    f.write('Hello, world!\n')
    f.write('This is a second line.\n')

# Reading from a file
with open('example.txt', 'r') as f:
    content = f.read()
    print(content)
# Output:
# Hello, world!
# This is a second line.
```

--------------------------------

### str.format() Method for Output Formatting

Source: https://docs.python.org/3/tutorial/inputoutput

Illustrates the str.format() method for substituting values into strings with detailed formatting directives. It shows how to format numbers and percentages.

```python
>>> yes_votes = 42_572_654
>>> total_votes = 85_705_149
>>> percentage = yes_votes / total_votes
>>> '{:-9} YES votes  {:2.2%}'.format(yes_votes, percentage)
' 42572654 YES votes  49.67%'
```

--------------------------------

### Doctest Unexpected Exception

Source: https://docs.python.org/3/library/doctest

The `doctest.UnexpectedException` exception signals that a doctest example raised an exception that was not anticipated. It includes the test, the example, and the exception information.

```APIDOC
doctest.UnexpectedException(_test_, _example_, _exc_info_)
  - Exception raised when a doctest example raised an unexpected exception.
  - Attributes:
    - test: The DocTest object that was being run when the example failed.
    - example: The Example that failed.
    - exc_info: A tuple containing information about the unexpected exception, as returned by sys.exc_info().
```

--------------------------------

### User Scheme Installation Directories (NT)

Source: https://docs.python.org/3/library/sysconfig

Details the installation paths for the user scheme on Windows (NT) systems. This scheme is for users without write permissions to the global site-packages directory.

```python
Path | Installation directory
_stdlib_ | _userbase_\Python_XY_
_platstdlib_ | _userbase_\Python_XY_
_platlib_ | _userbase_\Python_XY_\site-packages
_purelib_ | _userbase_\Python_XY_\site-packages
_include_ | _userbase_\Python_XY_\Include
_scripts_ | _userbase_\Python_XY_\Scripts
_data_ | _userbase_
```

--------------------------------

### Migrating C Extensions Guide

Source: https://docs.python.org/3/howto/cporting

This resource guides users through the process of porting C extension modules to Python 3. It covers general migration strategies and specific considerations for C extensions.

```python
import sys

def migrate_c_extensions():
    # Code to handle C extension migration
    pass
```

--------------------------------

### Test Examples in a Text File

Source: https://docs.python.org/3/library/doctest

This code snippet illustrates how to use the `doctest.testfile()` function to test interactive Python examples embedded within a separate text file. The function treats the file's content as a single large docstring, executing and verifying all found examples.

```python
import doctest

doctest.testfile("example.txt")
```

--------------------------------

### Trivial Optparse Callback Example

Source: https://docs.python.org/3/library/optparse

A simple example demonstrating a callback function that sets a flag in the parser's values when a specific option is encountered. This illustrates basic callback functionality.

```python
def record_foo_seen(option, opt_str, value, parser):
    parser.values.saw_foo = True

parser.add_option("--foo", action="callback", callback=record_foo_seen)
```

--------------------------------

### Context Manager to Start and Join Threads

Source: https://docs.python.org/3/library/test

A context manager for starting a sequence of threads and attempting to join them upon exiting the context. It can also execute a function after threads are started, even if an exception occurs.

```python
test.support.threading_helper.start_threads(_threads_ , _unlock =None_)
```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/.10

Lists additional resources for Python developers, including the PEP Index, Beginner's Guide, Book List, Audio/Visual Talks, and the Python Developer's Guide.

```APIDOC
Other resources:
  * [PEP Index](https://peps.python.org/)
  * [Beginner's Guide](https://wiki.python.org/moin/BeginnersGuide)
  * [Book List](https://wiki.python.org/moin/PythonBooks)
  * [Audio/Visual Talks](https://www.python.org/doc/av/)
  * [Python Developer’s Guide](https://devguide.python.org/)
```

--------------------------------

### Doctest Example with NORMALIZE_WHITESPACE

Source: https://docs.python.org/3/library/doctest

Demonstrates using the '+NORMALIZE_WHITESPACE' directive to handle variations in whitespace within the output of a doctest example. This allows the test to pass even if the actual output has different spacing than expected.

```python
>>> print(list(range(20)))  # doctest: +NORMALIZE_WHITESPACE
[0,   1,  2,  3,  4,  5,  6,  7,  8,  9,
10,  11, 12, 13, 14, 15, 16, 17, 18, 19]

```

--------------------------------

### Python Basic Logging Configuration

Source: https://docs.python.org/3/howto/logging

Sets up a basic logger with a console handler and a custom formatter. This example shows how to create, configure, and add handlers to a logger, and how to log messages at different severity levels.

```python
import logging

# create logger
logger = logging.getLogger('simple_example')
logger.setLevel(logging.DEBUG)

# create console handler and set level to debug
ch = logging.StreamHandler()
ch.setLevel(logging.DEBUG)

# create formatter
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# add formatter to ch
ch.setFormatter(formatter)

# add ch to logger
logger.addHandler(ch)

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warning('warn message')
logger.error('error message')
logger.critical('critical message')
```

--------------------------------

### Custom LoggerAdapter Example

Source: https://docs.python.org/3/howto/logging-cookbook

An example of a custom LoggerAdapter that prepends a 'connid' from its extra dictionary to the log message.

```python
classCustomAdapter(logging.LoggerAdapter):
    """
    This example adapter expects the passed in dict-like object to have a
    'connid' key, whose value in brackets is prepended to the log message.
    """
    defprocess(self, msg, kwargs):
        return '[%s] %s' % (self.extra['connid'], msg), kwargs
```

--------------------------------

### Third-Party Porting Guides

Source: https://docs.python.org/3/howto/pyporting

This section lists various third-party resources that offer additional guidance on porting Python 2 code to Python 3. These include guides from Fedora, DigitalOcean, and ActiveState, as well as a PyCon tutorial.

```APIDOC
Third-Party Python 2 to 3 Porting Resources:

1. Fedora Guide:
   - URL: https://portingguide.readthedocs.io

2. PyCon 2020 Tutorial:
   - URL: https://www.youtube.com/watch?v=JgIgEjASOlk

3. DigitalOcean Guide:
   - URL: https://www.digitalocean.com/community/tutorials/how-to-port-python-2-code-to-python-3

4. ActiveState Guide:
   - URL: https://www.activestate.com/blog/how-to-migrate-python-2-applications-to-python-3
```

--------------------------------

### Exponentiation in Python

Source: https://docs.python.org/3/tutorial/introduction

Shows how to calculate powers using the exponentiation operator (**). Examples include squaring a number and raising a number to a higher power.

```python
>>> 5 ** 2
25
>>> 2 ** 7
128
```

--------------------------------

### sysconfig Installation Paths

Source: https://docs.python.org/3/library/sysconfig

This section details how to access different installation paths provided by the sysconfig module. It covers various schemes like posix_user, nt_user, osx_framework_user, posix_home, posix_prefix, and nt.

```python
# Accessing specific installation paths
print(f"POSIX User Scheme: {sysconfig.get_path('posix_user')}")
print(f"NT User Scheme: {sysconfig.get_path('nt_user')}")
print(f"OSX Framework User Scheme: {sysconfig.get_path('osx_framework_user')}")
print(f"POSIX Home Scheme: {sysconfig.get_path('posix_home')}")
print(f"POSIX Prefix Scheme: {sysconfig.get_path('posix_prefix')}")
print(f"NT Scheme: {sysconfig.get_path('nt')}")
```

--------------------------------

### Python `importlib.metadata` Entry Points

Source: https://docs.python.org/3/contents

Explains how to access and manage entry points defined by Python distributions using the `importlib.metadata` module. Entry points are used for plugin discovery and extension mechanisms.

```python
from importlib.metadata import entry_points

# Get all entry points
all_eps = entry_points()

# Get entry points for a specific group
console_scripts = entry_points(group='console_scripts')

# Iterate through entry points
for ep in console_scripts:
    print(f"Name: {ep.name}, Value: {ep.value}")
```

--------------------------------

### FTP Class Constructor and Usage

Source: https://docs.python.org/3/library/ftplib

Demonstrates how to instantiate the `FTP` class, connect to an FTP server, log in, and list directory contents. It also shows how to use the `FTP` class with a `with` statement for automatic resource management.

```python
from ftplib import FTP

# Example using the with statement
with FTP("ftp1.at.proftpd.org") as ftp:
    ftp.login()
    ftp.dir()
```

--------------------------------

### Logging Configuration with basicConfig (Python)

Source: https://docs.python.org/3/howto/logging

Demonstrates the use of `logging.basicConfig()` to set up basic logging configuration. This function can set a default handler (e.g., to the console) and a default format if no handlers are already configured. It's a convenient way to start logging.

```python
import logging

logging.basicConfig(
    level=logging.DEBUG,  # Set the minimum logging level
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)
```

--------------------------------

### socketserver.TCPServer Example

Source: https://docs.python.org/3/library/socketserver

Demonstrates the usage of socketserver.TCPServer for creating TCP-based network servers. It outlines the basic structure for setting up a server to handle client connections.

```python
import socketserver

class MyTCPHandler(socketserver.BaseRequestHandler):
    """The request handler class for our server."""

    def handle(self):
        # self.request is the TCP connection that returned
        self.data = self.request.recv(1024).strip()
        print(f"Received {self.client_address[0]} wrote: {self.data}")

        # just send back the same data, but upper-cased
        self.request.sendall(self.data.upper())

if __name__ == "__main__":
    HOST, PORT = "localhost", 9999
    # Create the server, binding to localhost on port 9999
    with socketserver.TCPServer((HOST, PORT), MyTCPHandler) as server:
        # Activate the server; this will keep running until you
        # interrupt the program with Ctrl-C
        server.serve_forever()
```

--------------------------------

### Asyncio Event API and Example

Source: https://docs.python.org/3/library/asyncio-sync

Provides documentation and an example for using asyncio.Event to signal events between tasks.

```APIDOC
asyncio.Event
    An event object. Not thread-safe. An asyncio event can be used to notify multiple asyncio tasks that some event has happened. An Event object manages an internal flag that can be set to true with the set() method and reset to false with the clear() method. The wait() method blocks until the flag is set to true. The flag is set to false initially.
    Changed in version 3.10: Removed the _loop_ parameter.

asyncio.Event.wait()
    Wait until the event is set.
    If the event is set, return True immediately. Otherwise block until another task calls set().

asyncio.Event.set()
    Set the event.
    All tasks waiting for event to be set will be immediately awakened.

asyncio.Event.clear()
    Clear (unset) the event.
    Subsequent tasks awaiting on wait() will now block until the set() method is called again.

asyncio.Event.is_set()
    Return True if the event is set.

Example:
async defwaiter(event):
    print('waiting for it ...')
    await event.wait()
    print('... got it!')

async defmain():
    # Create an Event object.
    event = asyncio.Event()

    # Spawn a Task to wait until 'event' is set.
    waiter_task = asyncio.create_task(waiter(event))

    # Sleep for 1 second and set the event.
    await asyncio.sleep(1)
    event.set()

    # Wait until the waiter task is finished.
    await waiter_task

asyncio.run(main())
```

--------------------------------

### Configuring Python Environment Variables

Source: https://docs.python.org/3/using/windows

Details how to configure Windows environment variables like PATH and PATHEXT for convenient Python command-line usage. It highlights the installer's option for system-wide installations and recommends the Python Launcher for Windows when using multiple Python versions.

```windows
# Environment Variables for Python:
# PATH: Adds Python directories to the system's executable search path.
# PATHEXT: Includes .PY and .PYW extensions for running Python scripts directly.

# Recommendation for multiple Python versions:
# Use the Python Launcher for Windows (py.exe) for easier management.
```

--------------------------------

### Python Asyncio Event Loop Examples

Source: https://docs.python.org/3/library/asyncio-eventloop

Illustrative examples demonstrating the usage of the asyncio event loop for common asynchronous programming patterns.

```python
# Hello World with call_soon()
import asyncio

def hello():
    print('Hello world')

loop = asyncio.get_event_loop()
loop.call_soon(hello)
loop.run_forever()

# Display the current date with call_later()
import asyncio
import datetime

def display_date():
    print(f'The current date is {datetime.date.today()}')

loop = asyncio.get_event_loop()
loop.call_later(1, display_date) # Call after 1 second
loop.run_forever()

# Watch a file descriptor for read events
import asyncio
import os

async def watch_fd(loop, fd):
    while True:
        await loop.sock_recv(fd, 1024)
        print('Data received')

loop = asyncio.get_event_loop()
# Example: watching stdin (replace with actual fd)
# fd = sys.stdin.fileno()
# loop.create_task(watch_fd(loop, fd))
# loop.run_forever()

# Set signal handlers for SIGINT and SIGTERM
import asyncio
import signal

def handle_signal(sig):
    print(f'Received signal {sig}, shutting down...')
    loop = asyncio.get_event_loop()
    loop.stop()

loop = asyncio.get_event_loop()
loop.add_signal_handler(signal.SIGINT, handle_signal, signal.SIGINT)
loop.add_signal_handler(signal.SIGTERM, handle_signal, signal.SIGTERM)
# loop.run_forever()
```

--------------------------------

### Python Implementation-Specific Options (-X)

Source: https://docs.python.org/3/using/cmdline

Provides access to various implementation-specific features. This includes enabling fault handlers, showing reference counts, tracing memory allocations, configuring integer string conversion limits, and measuring import times.

```python
-X faulthandler
-X showrefcount
-X tracemalloc[=NFRAME]
-X int_max_str_digits=<value>
-X importtime
```

--------------------------------

### Install gettext with Default Locale Directory

Source: https://docs.python.org/3/library/gettext

Installs the '_' function globally into the built-in namespace for application-wide localization. This allows all application files to use '_' without explicit installation in each file.

```python
import gettext
gettext.install('myapplication')
```

--------------------------------

### Basic doctest Usage: Checking Examples in Docstrings

Source: https://docs.python.org/3/library/doctest

Demonstrates how to use the `doctest` module to find and run tests embedded within Python docstrings. This is useful for ensuring that code examples in your documentation are accurate and functional.

```python
import doctest

def factorial(n):
    """Computes the factorial of a non-negative integer.

    >>> factorial(0)
    1
    >>> factorial(1)
    1
    >>> factorial(5)
    120
    """
    if n < 0:
        raise ValueError("factorial() not defined for negative numbers")
    elif n == 0:
        return 1
    else:
        return n * factorial(n-1)

if __name__ == "__main__":
    doctest.testmod()

```

--------------------------------

### Python asyncio UDP Echo Server Example

Source: https://docs.python.org/3/library/asyncio-protocol

Provides an example of an asyncio UDP echo server. It listens for incoming datagrams and sends them back to the sender.

```python
import asyncio

class EchoServerProtocol(asyncio.DatagramProtocol):
    def connection_made(self, transport):
        self.transport = transport

    def datagram_received(self, data, addr):
        message = data.decode()
        print(f'Received {message!r} from {addr}')
        self.transport.sendto(data, addr)
        print(f'Sent {message!r} to {addr}')

async def main():
    loop = asyncio.get_running_loop()
    transport, protocol = await loop.create_datagram_endpoint(
        EchoServerProtocol,
        local_addr=('127.0.0.1', 9999)
    )

    try:
        await asyncio.sleep(3600)  # Serve for one hour
    finally:
        transport.close()

asyncio.run(main())
```

--------------------------------

### Command-line Usage of sysconfig

Source: https://docs.python.org/3/library/sysconfig

Demonstrates how to use the sysconfig module as a script from the command line to display Python's configuration information, including platform, version, installation scheme, paths, and variables.

```bash
python -m sysconfig
# Example Output:
# Platform: "macosx-10.4-i386"
# Python version: "3.2"
# Current installation scheme: "posix_prefix"
#
# Paths:
#         data = "/usr/local"
#         include = "/Users/tarek/Dev/svn.python.org/py3k/Include"
#         platinclude = "."
#         platlib = "/usr/local/lib/python3.2/site-packages"
#         platstdlib = "/usr/local/lib/python3.2"
#         purelib = "/usr/local/lib/python3.2/site-packages"
#         scripts = "/usr/local/bin"
#         stdlib = "/usr/local/lib/python3.2"
#
# Variables:
#         AC_APPLE_UNIVERSAL_BUILD = "0"
#         AIX_GENUINE_CPLUSPLUS = "0"
#         AR = "ar"
#         ARFLAGS = "rc"
#         ...

```

--------------------------------

### Python wsgiref.handlers.BaseHandler Method

Source: https://docs.python.org/3/genindex-S

Documentation for the setup_environ method in wsgiref.handlers.BaseHandler, used to set up the WSGI environment dictionary.

```APIDOC
wsgiref.handlers.BaseHandler.setup_environ()
  - Set up the WSGI environment dictionary. Can be overridden.
```

--------------------------------

### Custom LogRecord Factory Example

Source: https://docs.python.org/3/howto/logging-cookbook

An example demonstrating how to set and use a custom log record factory in Python 3.2+. This allows for more control over LogRecord creation, such as returning a subclass or adding attributes.

```python
import logging

def custom_log_record_factory(**kwargs):
    # Example: Create a custom LogRecord subclass or add attributes
    # For demonstration, we'll just use the default LogRecord constructor
    return logging.LogRecord(**kwargs)

# Set the custom factory
logging.setLogRecordFactory(custom_log_record_factory)

# You can also retrieve the current factory
# current_factory = logging.getLogRecordFactory()

# Example usage (assuming a logger is configured)
# logger = logging.getLogger('my_app')
# logger.warning('This is a test message.')
```

--------------------------------

### Basic doctest Usage: Checking Examples in a Text File

Source: https://docs.python.org/3/library/doctest

Shows how to use the `doctest` module to test examples contained within a separate text file. This is helpful for organizing tests that are separate from the main code.

```python
import doctest

# Assume 'my_tests.txt' contains:
# >>> 2 + 2
# 4

if __name__ == "__main__":
    doctest.testfile("my_tests.txt")

```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/.13

A collection of links to other valuable resources for Python developers, including the PEP Index, Beginner's Guide, Book List, Audio/Visual Talks, and the Python Developer's Guide.

```python
PEP Index (https://peps.python.org/)
Beginner's Guide (https://wiki.python.org/moin/BeginnersGuide)
Book List (https://wiki.python.org/moin/PythonBooks)
Audio/Visual Talks (https://www.python.org/doc/av/)
Python Developer’s Guide (https://devguide.python.org/)
```

--------------------------------

### LS Command Usage and Help Text

Source: https://docs.python.org/3/howto/argparse

Illustrates the usage of the 'ls' command in a Unix-like environment, showing its default output, output with arguments, and its help message. This serves as a conceptual example for command-line interfaces.

```bash
$ ls
cpython  devguide  prog.py  pypy  rm-unused-function.patch
$ lsctypes_configure  demo  dotviewer  include  lib_pypy  lib-python ...
$ lstotal 20
drwxr-xr-x 19 wena wena 4096 Feb 18 18:51 cpython
drwxr-xr-x  4 wena wena 4096 Feb  8 12:04 devguide
-rwxr-xr-x  1 wena wena  535 Feb 19 00:05 prog.py
drwxr-xr-x 14 wena wena 4096 Feb  7 00:59 pypy
-rw-r--r--  1 wena wena  741 Feb 18 01:01 rm-unused-function.patch
$ lsUsage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.
...
```

--------------------------------

### Subprocess StartupInfo and Creation Flags

Source: https://docs.python.org/3/library/subprocess

Explains the use of `_startupinfo_` for passing `STARTUPINFO` objects and `_creationflags_` for specifying process creation flags on Windows. Lists available flags.

```python
If given, _startupinfo_ will be a [`STARTUPINFO`](https://docs.python.org/3/library/subprocess.html#subprocess.STARTUPINFO "subprocess.STARTUPINFO") object, which is passed to the underlying `CreateProcess` function.
If given, _creationflags_ , can be one or more of the following flags:
  * [`CREATE_NEW_CONSOLE`](https://docs.python.org/3/library/subprocess.html#subprocess.CREATE_NEW_CONSOLE "subprocess.CREATE_NEW_CONSOLE")
  * [`CREATE_NEW_PROCESS_GROUP`](https://docs.python.org/3/library/subprocess.html#subprocess.CREATE_NEW_PROCESS_GROUP "subprocess.CREATE_NEW_PROCESS_GROUP")
  * [`ABOVE_NORMAL_PRIORITY_CLASS`](https://docs.python.org/3/library/subprocess.html#subprocess.ABOVE_NORMAL_PRIORITY_CLASS "subprocess.ABOVE_NORMAL_PRIORITY_CLASS")
  * [`BELOW_NORMAL_PRIORITY_CLASS`](https://docs.python.org/3/library/subprocess.html#subprocess.BELOW_NORMAL_PRIORITY_CLASS "subprocess.BELOW_NORMAL_PRIORITY_CLASS")
  * [`HIGH_PRIORITY_CLASS`](https://docs.python.org/3/library/subprocess.html#subprocess.HIGH_PRIORITY_CLASS "subprocess.HIGH_PRIORITY_CLASS")
  * [`IDLE_PRIORITY_CLASS`](https://docs.python.org/3/library/subprocess.html#subprocess.IDLE_PRIORITY_CLASS "subprocess.IDLE_PRIORITY_CLASS")
  * [`NORMAL_PRIORITY_CLASS`](https://docs.python.org/3/library/subprocess.html#subprocess.NORMAL_PRIORITY_CLASS "subprocess.NORMAL_PRIORITY_CLASS")
  * [`REALTIME_PRIORITY_CLASS`](https://docs.python.org/3/library/subprocess.html#subprocess.REALTIME_PRIORITY_CLASS "subprocess.REALTIME_PRIORITY_CLASS")
  * [`CREATE_NO_WINDOW`](https://docs.python.org/3/library/subprocess.html#subprocess.CREATE_NO_WINDOW "subprocess.CREATE_NO_WINDOW")
  * [`DETACHED_PROCESS`](https://docs.python.org/3/library/subprocess.html#subprocess.DETACHED_PROCESS "subprocess.DETACHED_PROCESS")
  * [`CREATE_DEFAULT_ERROR_MODE`](https://docs.python.org/3/library/subprocess.html#subprocess.CREATE_DEFAULT_ERROR_MODE "subprocess.CREATE_DEFAULT_ERROR_MODE")
  * [`CREATE_BREAKAWAY_FROM_JOB`](https://docs.python.org/3/library/subprocess.html#subprocess.CREATE_BREAKAWAY_FROM_JOB "subprocess.CREATE_BREAKAWAY_FROM_JOB")
```

--------------------------------

### Sending Directory Contents as Email

Source: https://docs.python.org/3/library/email-examples

This example demonstrates sending the contents of a directory as a MIME message. It requires importing the 'os' module to interact with the file system.

```python
#!/usr/bin/env python3

"""Send the contents of a directory as a MIME message."""

import os
import smtplib

# This is a placeholder for the actual logic to read directory contents
# and construct the MIME message, which would typically involve
# iterating through os.listdir() and adding files as attachments.
# The provided text only includes the shebang and import statements for this example.
```

--------------------------------

### Zipfile Command-Line Interface

Source: https://docs.python.org/3/library/zipfile

Provides examples of using the zipfile module from the command line for basic ZIP archive operations like creating, listing, and extracting.

```bash
# Create a ZIP archive
python -m zipfile -c my_archive.zip file1.txt file2.txt

# List contents of a ZIP archive
python -m zipfile -l my_archive.zip

# Extract contents of a ZIP archive
python -m zipfile -e my_archive.zip destination_folder/
```

--------------------------------

### Logging QueueListener Start

Source: https://docs.python.org/3/genindex-S

Starts the listener thread for a `QueueHandler`. This allows log records to be processed asynchronously by a separate thread.

```python
import logging
import logging.handlers
import queue

log_queue = queue.Queue(-1)
listener = logging.handlers.QueueListener(log_queue, logging.StreamHandler())

listener.start() # Starts the listener thread

# ... send log records to log_queue ...

listener.stop() # Stops the listener thread
```

--------------------------------

### Python Site Module Initialization and Configuration

Source: https://docs.python.org/3/library/site

Explains how the `site` module is automatically imported during Python startup to configure the module search path and built-in namespace. It details how site-specific directories are constructed using `sys.prefix` and `sys.exec_prefix`, and how `.pth` files are processed to add custom paths.

```python
import sys

# The site module is automatically imported during initialization.
# Importing it appends site-specific paths to sys.path and adds callables like help() to builtins.
# The -S command-line option suppresses this automatic import.

# To explicitly trigger the usual site-specific additions, call the main() function:
site.main()

# Site-specific directories are constructed from sys.prefix and sys.exec_prefix
# with tails like 'lib/site-packages' or 'lib/pythonX.Y/site-packages'.

# Path configuration files (.pth) in these directories can add more items to sys.path.
# Lines starting with 'import' in .pth files are executed.

# Example .pth file content:
# /path/to/my/packages
# import site_custom_init

# Handling of pyvenv.cfg for virtual environments:
# If 'pyvenv.cfg' exists above sys.executable, sys.prefix and sys.exec_prefix are set to that directory.
# The 'include-system-site-packages' key in pyvenv.cfg controls whether system-level prefixes are searched.
```

--------------------------------

### Python asyncio TCP Echo Server Example

Source: https://docs.python.org/3/library/asyncio-protocol

Demonstrates how to create a TCP echo server using Python's asyncio library. This example showcases the basic structure of an asyncio server, handling client connections and echoing received data back.

```python
import asyncio

class EchoServerProtocol(asyncio.Protocol):
    def connection_made(self, transport):
        self.transport = transport
        print('Connection from', transport.get_extra_info('peername'))

    def datagram_received(self, data):
        message = data.decode()
        print('Received %r' % message)
        print('Send %r to %r' % (message, self.transport.get_extra_info('peername')))
        self.transport.sendto(data)

async def main():
    print("Starting UDP server")

    loop = asyncio.get_running_loop()

    # One strategy is to run echo server in a subprocess
    transport, protocol = await loop.create_datagram_endpoint(
        lambda: EchoServerProtocol(),
        local_addr=('127.0.0.1', 9999))

    try:
        await asyncio.Future()  # run forever
    finally:
        transport.close()

asyncio.run(main())
```

--------------------------------

### User Scheme Installation Directories (macOS Framework)

Source: https://docs.python.org/3/library/sysconfig

Details the installation paths for the user scheme on macOS when using the framework build. This scheme is for users without write permissions to the global site-packages directory.

```python
Path | Installation directory
_stdlib_ | _userbase_/lib/python
_platstdlib_ | _userbase_/lib/python
_platlib_ | _userbase_/lib/python/site-packages
_purelib_ | _userbase_/lib/python/site-packages
_include_ | _userbase_/include/python_X.Y_
_scripts_ | _userbase_/bin
_data_ | _userbase_
```

--------------------------------

### Running Python Code Between Initialization Phases

Source: https://docs.python.org/3/c-api/init_config

An example demonstrating how to run Python code between the 'Core' and 'Main' initialization phases using the C-API. It shows how to configure Python to stop after the 'Core' phase and execute Python code before proceeding to the 'Main' phase.

```c
voidinit_python(void)
{
PyStatusstatus;

PyConfigconfig;
PyConfig_InitPythonConfig(&config);
config._init_main=0;

/* ... customize 'config' configuration ... */

status=Py_InitializeFromConfig(&config);
PyConfig_Clear(&config);
if(PyStatus_Exception(status)){
Py_ExitStatusException(status);
}

/* Use sys.stderr because sys.stdout is only created
       by _Py_InitializeMain() */
intres=PyRun_SimpleString(
"import sys; "
"print('Run Python code before _Py_InitializeMain', "
"file=sys.stderr)");
if(res<0){
exit(1);
}

/* ... put more configuration code here ... */

status=_Py_InitializeMain();
if(PyStatus_Exception(status)){
Py_ExitStatusException(status);
}
}
```

--------------------------------

### Python Launcher for Windows - Diagnostics and Return Codes

Source: https://docs.python.org/3/using/windows

Information on diagnosing issues with the Python Launcher and understanding its return codes for various operations.

```python
# Example of checking return codes from the Python Launcher
# py --version
# echo %errorlevel%
```

--------------------------------

### Python Documentation Navigation and Resources

Source: https://docs.python.org/3/.8

Outlines navigation elements like indices and glossaries, and lists other important resources such as PEPs, beginner's guides, and contributing information.

```APIDOC
Navigation:
  - Global Module Index
  - General Index
  - Glossary
  - Search page
  - Complete Table of Contents

Other Resources:
  - PEP Index
  - Beginner's Guide
  - Book List
  - Audio/Visual Talks
  - Python Developer’s Guide
  - Reporting bugs
  - Contributing to Docs
  - About the documentation
  - History and License of Python
  - Copyright
```

--------------------------------

### Python doctest Module Classes and Attributes

Source: https://docs.python.org/3/genindex-E

The doctest module is used to write doctests, which are examples embedded in docstrings. It includes classes like Example and DocTestFailure, and attributes like example and exc_msg for managing test cases and their results.

```python
import doctest

class MyClass:
    def my_method(self):
        """This is a doctest.

        >>> MyClass().my_method()
        'Success'
        """
        return 'Success'

# To run doctests:
# doctest.testmod()
```

--------------------------------

### itertools.chain.from_iterable Example

Source: https://docs.python.org/3/whatsnew/2

Provides an example of using itertools.chain.from_iterable to flatten a list of iterables into a single sequence.

```python
import itertools

print(list(itertools.chain.from_iterable([[1,2,3], [4,5,6]])))
```

--------------------------------

### Usage Examples for Immutable Subclasses

Source: https://docs.python.org/3/faq/programming

Shows practical examples of using the custom immutable subclasses `FirstOfMonthDate`, `NamedInt`, and `TitleStr`.

```python
>>> FirstOfMonthDate(2012, 2, 14)
FirstOfMonthDate(2012, 2, 1)
>>> NamedInt('ten')
10
>>> NamedInt(20)
20
>>> TitleStr('Blog: Why Python Rocks')
'blog-why-python-rocks'
```

--------------------------------

### Python resource Module Get Functions

Source: https://docs.python.org/3/genindex-G

Provides access to system resources. Includes functions for getting resource usage and limits.

```APIDOC
resource Module:

getrusage(who)
  Returns a tuple of resource usage information for the specified who.
  Parameters:
    who: The resource usage category (e.g., RUSAGE_SELF).
  Returns: A tuple of resource usage statistics.
```

--------------------------------

### Logging Output Examples

Source: https://docs.python.org/3/howto/logging-cookbook

Illustrates the console output of a Python logging system under different log levels (INFO, DEBUG) and configurations. It shows how log messages are displayed, including the logging level and the source module.

```bash
$ pythonINFO start Started the 'foo' service.

$ pythonINFO stop Stopped the 'foo' and 'bar' services.

$ pythonINFO restart Restarted the 'foo', 'bar' and 'baz' services.

$ pythonDEBUG start About to start foo
INFO start Started the 'foo' service.

$ pythonDEBUG stop About to stop 'foo' and 'bar'
INFO stop Stopped the 'foo' and 'bar' services.

$ pythonDEBUG restart About to restart 'foo', 'bar' and 'baz'
INFO restart Restarted the 'foo', 'bar' and 'baz' services.
```

--------------------------------

### Doctest Failure Exception

Source: https://docs.python.org/3/library/doctest

The `doctest.DocTestFailure` exception is raised when a doctest example's actual output does not match its expected output. It stores the test, the failing example, and the actual output received.

```APIDOC
doctest.DocTestFailure(_test_, _example_, _got_)
  - Exception raised when a doctest example's actual output does not match its expected output.
  - Attributes:
    - test: The DocTest object that was being run when the example failed.
    - example: The Example that failed.
    - got: The example's actual output.
```

--------------------------------

### Enum Usage Examples

Source: https://docs.python.org/3/howto/enum

Provides examples of calling custom methods on an Enum instance and a class method on the Enum itself.

```python
Mood.favorite_mood()
Mood.HAPPY.describe()
str(Mood.FUNKY)
```

--------------------------------

### Install Python Package on FreeBSD

Source: https://docs.python.org/3/using/unix

Adds the Python package to a FreeBSD system.

```bash
pkg install python
```

--------------------------------

### pty Module Example

Source: https://docs.python.org/3/library/pty

Demonstrates the usage of the pty module for pseudo-terminal utilities. This example showcases how to spawn a process in a new pseudo-terminal.

```python
import pty
import os

pid, fd = pty.fork()

if pid == 0:  # Child process
    # Execute a command, e.g., 'ls -l'
    os.execlp('ls', 'ls', '-l')
else:  # Parent process
    # Read from the pseudo-terminal
    while True:
        try:
            line = os.read(fd, 1024).decode('utf-8')
            if not line:
                break
            print(f"Received: {line.strip()}")
        except OSError as e:
            print(f"Error reading from fd: {e}")
            break
    
    # Wait for the child process to finish
    os.waitpid(pid, 0)
    print("Child process finished.")

# Close the file descriptor
os.close(fd)
```

--------------------------------

### Python str.format() Examples

Source: https://docs.python.org/3/library/string

Illustrates basic usage of Python's str.format() method with positional arguments and implicit referencing.

```python
"First, thou shalt count to {0}".format(10)
"Bring me a {}".format('apple')
```

--------------------------------

### Python Heapq Module for Priority Queues

Source: https://docs.python.org/3/tutorial/stdlib2

Shows how to use the heapq module to implement a min-heap (priority queue) using a standard Python list. Functions like heapify, heappush, and heappop are demonstrated.

```python
from heapq import heapify, heappop, heappush

data = [1, 3, 5, 7, 9, 2, 4, 6, 8, 0]
heapify(data)                      # rearrange the list into heap order
heappush(data, -5)                 # add a new entry
print([heappop(data) for i in range(3)])  # fetch the three smallest entries
```

--------------------------------

### Installing Python Modules: Binary Extensions

Source: https://docs.python.org/3/contents

Guidance on installing Python packages that include compiled binary extensions. This often involves specific compiler requirements and build processes.

```APIDOC
Installing binary extensions:
  Explains the process and potential issues when installing Python packages with compiled components.
  Covers build prerequisites and common compilation errors.
```

--------------------------------

### Multiprocessing Process Start

Source: https://docs.python.org/3/genindex-S

Starts the execution of a process. This method is called on a `multiprocessing.Process` object to begin its run method in a new process.

```python
import multiprocessing

def worker():
    print("Worker process started")

if __name__ == "__main__":
    p = multiprocessing.Process(target=worker)
    p.start() # Starts the process
    p.join()  # Wait for the process to finish
```

--------------------------------

### Python Logging Message Format Example

Source: https://docs.python.org/3/howto/logging

An example of a message format string for the logging.Formatter, specifying the order of timestamp, severity level, and message content.

```python
'%(asctime)s - %(levelname)s - %(message)s'
```

--------------------------------

### doctest.Example Class Documentation

Source: https://docs.python.org/3/library/doctest

Provides details on the doctest.Example class, used to represent interactive Python examples within doctests. It outlines the constructor arguments and the attributes that store the example's source code, expected output, exception messages, line number, indentation, and options.

```APIDOC
class doctest.Example(_source_, _want_, _exc_msg_=None, _lineno_=0, _indent_=0, _options_=None)
  A single interactive example, consisting of a Python statement and its expected output.

  Attributes:
    source (str): The example's source code, a single Python statement ending with a newline.
    want (str): The expected output from running the example's source code, ending with a newline unless no output is expected.
    exc_msg (str or None): The exception message generated by the example, or None if no exception is expected. Compared against traceback.format_exception_only().
    lineno (int): The line number within the containing string where the example begins (zero-based).
    indent (int): The example's indentation in the containing string (number of preceding spaces).
    options (dict): A dictionary mapping option flags to True/False to override default options for this example.
```

--------------------------------

### User Scheme Installation Directories (POSIX)

Source: https://docs.python.org/3/library/sysconfig

Details the installation paths for the user scheme on POSIX systems. This scheme is for users without write permissions to the global site-packages directory.

```python
Path | Installation directory
_stdlib_ | _userbase_/lib/python_X.Y_
_platstdlib_ | _userbase_/lib/python_X.Y_
_platlib_ | _userbase_/lib/python_X.Y_/site-packages
_purelib_ | _userbase_/lib/python_X.Y_/site-packages
_include_ | _userbase_/include/python_X.Y_
_scripts_ | _userbase_/bin
_data_ | _userbase_
```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/library/tkinter

Lists essential external resources for Python developers, including the Python Enhancement Proposal (PEP) index, guides for beginners, book recommendations, audio/visual talks, and the Python Developer's Guide.

```markdown
* [PEP Index](https://peps.python.org/)
* [Beginner's Guide](https://wiki.python.org/moin/BeginnersGuide)
* [Book List](https://wiki.python.org/moin/PythonBooks)
* [Audio/Visual Talks](https://www.python.org/doc/av/)
* [Python Developer’s Guide](https://devguide.python.org/)
```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/.11

A collection of links to other valuable resources for Python developers, including the PEP Index, Beginner's Guide, Book List, Audio/Visual Talks, and the Python Developer's Guide.

```python
https://peps.python.org/
https://wiki.python.org/moin/BeginnersGuide
https://wiki.python.org/moin/PythonBooks
https://www.python.org/doc/av/
https://devguide.python.org/
```

--------------------------------

### Install Dependencies with Pip

Source: https://docs.python.org/3/library/zipapp

Demonstrates installing application dependencies into a directory using pip, typically from a requirements file.

```shell
python -m pip install -r requirements.txt --target myapp
```

--------------------------------

### Python 3 Documentation Navigation

Source: https://docs.python.org/3/tutorial/floatingpoint

Provides links to key sections of the Python 3 documentation, such as the general index, module index, and specific tutorials. It also lists available Python versions.

```python
Project: /websites/python_3

### Navigation
  * [index](https://docs.python.org/3/genindex.html "General Index")
  * [modules](https://docs.python.org/3/py-modindex.html "Python Module Index") | 
  * [next](https://docs.python.org/3/tutorial/appendix.html "16. Appendix") | 
  * [previous](https://docs.python.org/3/tutorial/interactive.html "14. Interactive Input Editing and History Substitution") | 
  * [Python](https://www.python.org/) »
  * Greek | Ελληνικά English Spanish | español French | français Italian | italiano Japanese | 日本語 Korean | 한국어 Polish | polski Brazilian Portuguese | Português brasileiro Turkish | Türkçe Simplified Chinese | 简体中文 Traditional Chinese | 繁體中文
  dev (3.15) pre (3.14) 3.13.7 3.12 3.11 3.10 3.9 3.8 3.7 3.6 3.5 3.4 3.3 3.2 3.1 3.0 2.7 2.6
  * [3.13.7 Documentation](https://docs.python.org/3/index.html) » 
  * [The Python Tutorial](https://docs.python.org/3/tutorial/index.html) »
  * [15. Floating-Point Arithmetic: Issues and Limitations](https://docs.python.org/3/tutorial/floatingpoint.html)
  * | 
  * Theme  Auto Light Dark |
```

--------------------------------

### Asyncio Event Loop Examples

Source: https://docs.python.org/3/contents

Demonstrates basic usage of the asyncio event loop with functions like call_soon() and call_later(). It also covers watching file descriptors for read events and setting signal handlers.

```python
import asyncio

async def main():
    loop = asyncio.get_running_loop()
    # Example using call_soon()
    loop.call_soon(print, 'Hello from call_soon!')
    # Example using call_later()
    loop.call_later(1, print, 'Hello after 1 second')
    # Example watching a file descriptor (conceptual)
    # fd = ... # get a file descriptor
    # loop.add_reader(fd, print, 'File descriptor event')
    # Example setting signal handlers (conceptual)
    # loop.add_signal_handler(signal.SIGINT, print, 'SIGINT received')

asyncio.run(main())
```

--------------------------------

### Platform Module and Options

Source: https://docs.python.org/3/genindex-P

Documentation for the 'platform' module and its command-line options. Includes information on getting platform-specific data and controlling output format.

```python
import platform

# Get detailed platform information
print(platform.platform())

# Example of using command-line options (conceptual, not direct code)
# platform --nonaliased
# platform --terse
```

--------------------------------

### Python Await Syntax

Source: https://docs.python.org/3/howto/a-conceptual-overview-of-asyncio

Demonstrates the two common syntaxes for using the 'await' keyword in Python with asyncio.

```python
await task
await coroutine
```

--------------------------------

### Install Python Package on OpenBSD

Source: https://docs.python.org/3/using/unix

Adds the Python package to an OpenBSD system.

```bash
pkg_add python
```

--------------------------------

### AsyncExitStack Usage Example

Source: https://docs.python.org/3/library/contextlib

Demonstrates how to use AsyncExitStack to manage multiple asynchronous context managers, ensuring all resources are released even if errors occur.

```python
async with AsyncExitStack() as stack:
    connections = [await stack.enter_async_context(get_connection())
        for i in range(5)]
    # All opened connections will automatically be released at the end of
    # the async with statement, even if attempts to open a connection
    # later in the list raise an exception.
```

--------------------------------

### WSGI Request Handling Methods

Source: https://docs.python.org/3/library/wsgiref

Provides methods for determining the request scheme and setting up the WSGI environment. get_scheme guesses the URL scheme, while setup_environ initializes the WSGI environment dictionary.

```APIDOC
get_scheme():
  Returns: str
  Description: Guesses the URL scheme ('http' or 'https') based on request environ variables.

setup_environ():
  Description: Sets up the WSGI environment for the current request.
```

--------------------------------

### Python locale Module Get Functions

Source: https://docs.python.org/3/genindex-G

Facilitates internationalization and localization. Includes a function to get the preferred encoding.

```APIDOC
locale Module:

getpreferredencoding(do_setlocale=True)
  Returns the preferred encoding for text files.
  Parameters:
    do_setlocale: If True, also sets the locale.
  Returns: The preferred encoding.
```

--------------------------------

### Using Mock Helpers: sentinel, call, ANY

Source: https://docs.python.org/3/library/development

Introduces useful helper objects provided by `unittest.mock`. `sentinel` creates unique objects for comparisons, `call` helps assert method calls, and `ANY` matches any object.

```python
from unittest.mock import Mock, call, ANY, sentinel

mock = Mock()
mock.method(1, 2)
mock.other_method(sentinel.arg1, 'literal')

mock.assert_any_call(call.method(ANY, 2))
mock.assert_called_with(call.other_method(sentinel.arg1, 'literal'))
```

--------------------------------

### Site Module getsitepackages()

Source: https://docs.python.org/3/genindex-G

Returns a list of directory names where third-party packages are installed. This is useful for understanding Python's package installation paths.

```python
import site

# Get the site-packages directories
site_packages_dirs = site.getsitepackages()
print("Site-packages directories:")
for dir in site_packages_dirs:
    print(f"- {dir}")
```

--------------------------------

### Python Logging Handlers Example

Source: https://docs.python.org/3/howto/logging

Shows different types of handlers available in Python's logging module, such as FileHandler and StreamHandler, for directing log output.

```python
import logging

# File handler to write logs to a file
file_handler = logging.FileHandler('activity.log')
file_handler.setLevel(logging.INFO)
file_handler.setFormatter(logging.Formatter('%(asctime)s: %(message)s'))

# Stream handler to output logs to the console
stream_handler = logging.StreamHandler()
stream_handler.setLevel(logging.WARNING)
stream_handler.setFormatter(logging.Formatter('WARNING: %(message)s'))

root_logger = logging.getLogger()
root_logger.addHandler(file_handler)
root_logger.addHandler(stream_handler)
root_logger.setLevel(logging.DEBUG)

root_logger.debug('This debug message will not be shown.')
root_logger.info('This info message will be written to activity.log.')
root_logger.warning('This warning message will be shown on the console and written to activity.log.')
```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/.14

Lists important external resources for Python developers, including the PEP Index for Python Enhancement Proposals, a Beginner's Guide, a Book List, Audio/Visual Talks, and the Python Developer's Guide.

```python
print('PEP Index: https://peps.python.org/')
print('Beginner\'s Guide: https://wiki.python.org/moin/BeginnersGuide')
print('Book List: https://wiki.python.org/moin/PythonBooks')
print('Audio/Visual Talks: https://www.python.org/doc/av/')
print('Python Developer\'s Guide: https://devguide.python.org/')
```

--------------------------------

### sysconfig Module Methods

Source: https://docs.python.org/3/genindex-G

Provides access to Python installation configuration information.

```APIDOC
sysconfig.get_path(name, scheme=None, vars=None, expand=True)
  Return the path for a given scheme and name.
  Parameters:
    name: The name of the path (e.g., 'include', 'platinclude').
    scheme: The installation scheme to use.
    vars: Dictionary of variables to substitute.
    expand: Whether to expand variables.
  Returns: The path string.
```

```APIDOC
sysconfig.get_path_names()
  Return a list of all known path names.
  Returns: A list of path name strings.
```

```APIDOC
sysconfig.get_paths(scheme=None, vars=None, expand=True)
  Return a dictionary of all paths for a given scheme.
  Parameters:
    scheme: The installation scheme to use.
    vars: Dictionary of variables to substitute.
    expand: Whether to expand variables.
  Returns: A dictionary mapping path names to path strings.
```

```APIDOC
sysconfig.get_platform()
  Return the current platform identifier.
  Returns: The platform string.
```

```APIDOC
sysconfig.get_preferred_scheme(platform=None)
  Return the preferred installation scheme for a given platform.
  Parameters:
    platform: The platform identifier.
  Returns: The preferred scheme name.
```

```APIDOC
sysconfig.get_python_version()
  Return the Python version as a string.
  Returns: The version string (e.g., '3.9').
```

```APIDOC
sysconfig.get_scheme_names()
  Return a list of all known scheme names.
  Returns: A list of scheme name strings.
```

--------------------------------

### Logging to a File

Source: https://docs.python.org/3/howto/logging

This example illustrates how to configure the logging module to direct output to a file instead of the console. It includes basic file configuration.

```python
import logging

logging.basicConfig(filename='example.log', level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')
```

--------------------------------

### Module Setup and Teardown Functions

Source: https://docs.python.org/3/library/unittest

Defines functions for module-level setup and teardown. setUpModule is called before any tests in the module, and tearDownModule is called after. Exceptions in setUpModule prevent tests from running and tearDownModule from being called.

```python
def setUpModule():
    createConnection()

def tearDownModule():
    closeConnection()
```

--------------------------------

### Python SSLContext Example Usage

Source: https://docs.python.org/3/library/ssl

An example demonstrating how to create an SSLContext, disable hostname checking, set the verify mode to none, and specify the maximum TLS version.

```python
context = ssl.SSLContext(ssl.PROTOCOL_TLS_CLIENT)
context.check_hostname = False
context.verify_mode = ssl.CERT_NONE
context.maximum_version = ssl.TLSVersion.TLSv1_2

```

--------------------------------

### Logging to a File with Basic Configuration

Source: https://docs.python.org/3/howto/logging

Shows how to configure logging to write messages to a file named 'example.log'. It sets the logging level to DEBUG, ensuring all messages are recorded. The `encoding` argument is used for UTF-8 compatibility.

```python
import logging
logger = logging.getLogger(__name__)
logging.basicConfig(filename='example.log', encoding='utf-8', level=logging.DEBUG)
logger.debug('This message should go to the log file')
logger.info('So should this')
logger.warning('And this, too')
logger.error('And non-ASCII stuff, too, like Øresund and Malmö')
```

--------------------------------

### Argparse Example

Source: https://docs.python.org/3/library/optparse

Illustrates command-line argument parsing with Python's `argparse` library. It defines options for output and verbosity, and also handles positional arguments.

```python
import argparse

if __name__ == '__main__':
    parser = argparse.ArgumentParser()
    parser.add_argument('-o', '--output')
    parser.add_argument('-v', dest='verbose', action='store_true')
    parser.add_argument('rest', nargs='*')
    args = parser.parse_args()
    process(args.rest, output=args.output, verbose=args.verbose)
```

--------------------------------

### Python ConfigParser Usage Example

Source: https://docs.python.org/3/library/configparser

Demonstrates basic usage of Python's configparser to access values from a configuration structure.

```python
print(parser['hashes']['extensions'])
print(parser['hashes']['interpolation not necessary'])
print(parser['hashes']['even in multiline values'])
```

--------------------------------

### Multiprocessing with Spawn Context

Source: https://docs.python.org/3/library/multiprocessing

Demonstrates how to use the 'spawn' start method for multiprocessing and exchange data using a Queue. This approach is recommended for cross-platform compatibility.

```python
import multiprocessing as mp

def foo(q):
    q.put('hello')

if __name__ == '__main__':
    ctx = mp.get_context('spawn')
    q = ctx.Queue()
    p = ctx.Process(target=foo, args=(q,))
    p.start()
    print(q.get())
    p.join()
```

--------------------------------

### Get Execution Prefix

Source: https://docs.python.org/3/c-api/init

Returns the prefix for installed platform-specific files. This is derived through a number of complicated rules from the program name set with PyConfig.program_name and some environment variables. The returned string points into static storage; the caller should not modify its value. This corresponds to the exec_prefix variable in the top-level Makefile and the --exec-prefix argument to the configure script. The value is available to Python code as sys.base_exec_prefix. This function should not be called before Py_Initialize(), otherwise it returns NULL.

```c
wchar_t* Py_GetExecPrefix();
/* Deprecated since version 3.13, will be removed in version 3.15: Get sys.base_exec_prefix instead, or sys.exec_prefix if virtual environments need to be handled. */
```

--------------------------------

### Tkinter Progressbar Start

Source: https://docs.python.org/3/genindex-S

Starts the progress bar animation. This is typically used for indeterminate progress bars, where the progress is not known.

```python
import tkinter as tk
from tkinter.ttk import Progressbar

root = tk.Tk()

progressbar = Progressbar(root, orient='horizontal', length=200, mode='indeterminate')
progressbar.pack(pady=20)

progressbar.start(10) # Start animation, update every 10ms

# To stop: progressbar.stop()

root.mainloop()
```

--------------------------------

### Installing Python Modules: Scientific Packages

Source: https://docs.python.org/3/contents

Guidance on installing scientific Python packages, which often have complex dependencies. This is relevant for data science and numerical computing.

```APIDOC
Install scientific Python packages:
  Provides methods and considerations for installing scientific libraries like NumPy and SciPy.
  Addresses potential challenges with complex dependencies.
```

--------------------------------

### Floor Division and Modulo Operations

Source: https://docs.python.org/3/tutorial/introduction

Illustrates the use of floor division (//) to discard the fractional part of a division and the modulo operator (%) to find the remainder of a division. Shows how these operators work with integers.

```python
>>> 17 / 3
5.666666666666667
>>> 17 // 3
5
>>> 17 % 3
2
>>> 5 * 3 + 2
17
```

--------------------------------

### Pathlib Globbing Examples

Source: https://docs.python.org/3/library/pathlib

Provides examples of how to use the '**' wildcard for recursive globbing in pathlib, demonstrating various matching scenarios.

```python
Examples:
  "**/*" : Any path with at least one segment.
  "**/*.py" : Any path ending with ".py".
  "assets/**" : Any path starting with "assets/".
  "assets/**/*" : Any path starting with "assets/", excluding "assets/" itself.
```

--------------------------------

### Asyncio Transports and Protocols Examples

Source: https://docs.python.org/3/contents

Illustrates the use of transports and protocols in asyncio for building network applications. Examples include TCP and UDP echo servers and clients, connecting existing sockets, and using subprocesses.

```python
import asyncio

# TCP Echo Server Example (Conceptual)
class EchoServerProtocol(asyncio.Protocol):
    def connection_made(self, transport):
        self.transport = transport

    def data_received(self, data):
        self.transport.write(data)

async def tcp_echo_server():
    loop = asyncio.get_running_loop()
    server = await loop.create_server(EchoServerProtocol, '127.0.0.1', 8888)
    async with server:
        await server.serve_forever()

# UDP Echo Server Example (Conceptual)
class EchoServerDatagramProtocol(asyncio.DatagramProtocol):
    def connection_made(self, transport):
        self.transport = transport

    def datagram_received(self, data, addr):
        self.transport.sendto(data, addr)

async def udp_echo_server():
    loop = asyncio.get_running_loop()
    transport, protocol = await loop.create_datagram_endpoint(
        EchoServerDatagramProtocol, local_addr=('127.0.0.1', 9999))
    async with transport:
        await transport.serve_forever()

# asyncio.run(tcp_echo_server())
# asyncio.run(udp_echo_server())
```

--------------------------------

### Register Open Socket to Wait for Data using Streams

Source: https://docs.python.org/3/library/asyncio-stream

This Python code snippet demonstrates how to register an open socket to wait for data using asyncio streams. It utilizes `asyncio.open_connection` with a socket pair to simulate data reception and processing. The example shows how to get the event loop, create connected sockets, register the socket for reading, simulate data sending, read the data, and properly close the connections.

```python
import asyncio
import socket

async def wait_for_data():
    # Get a reference to the current event loop because
    # we want to access low-level APIs.
    loop = asyncio.get_running_loop()

    # Create a pair of connected sockets.
    rsock, wsock = socket.socketpair()

    # Register the open socket to wait for data.
    reader, writer = await asyncio.open_connection(sock=rsock)

    # Simulate the reception of data from the network
    loop.call_soon(wsock.send, 'abc'.encode())

    # Wait for data
    data = await reader.read(100)

    # Got data, we are done: close the socket
    print("Received:", data.decode())
    writer.close()
    await writer.wait_closed()

    # Close the second socket
    wsock.close()

asyncio.run(wait_for_data())

```

--------------------------------

### Python Contextlib: Creating a Simple Context Manager

Source: https://docs.python.org/3/library/python

Provides an example of creating a custom context manager using the `contextlib.contextmanager` decorator. This allows for easy management of resources using the `with` statement.

```python
from contextlib import contextmanager

@contextmanager
def managed_resource(name):
    print(f"Acquiring resource: {name}")
    try:
        yield f"Resource {name} acquired"
    finally:
        print(f"Releasing resource: {name}")

with managed_resource("Database Connection") as resource:
    print(f"Using: {resource}")
```

--------------------------------

### Python Dictionary Comprehension Example

Source: https://docs.python.org/3/glossary

Illustrates a concise method for creating dictionaries in Python using comprehensions. This example shows how to generate a dictionary where keys are numbers and values are their squares.

```python
results = {n: n ** 2 for n in range(10)}
```

--------------------------------

### Socket Programming HOWTO

Source: https://docs.python.org/3/howto/sockets

Link to the HOWTO guide for socket programming in Python.

```python
sockets_howto: https://docs.python.org/3/howto/sockets.html
```

--------------------------------

### Python C-API: Unicode Exception Start Attribute

Source: https://docs.python.org/3/c-api/exceptions

Functions to set the 'start' attribute of Unicode exception objects. These functions are part of the Stable ABI and are used to modify the starting position associated with a Unicode encoding or decoding error.

```c
intPyUnicodeTranslateError_SetStart([PyObject](https://docs.python.org/3/c-api/structures.html#c.PyObject "PyObject")*exc, [Py_ssize_t](https://docs.python.org/3/c-api/intro.html#c.Py_ssize_t "Py_ssize_t")start)
     _Part of the[ Stable ABI](https://docs.python.org/3/c-api/stable.html#stable)._
Set the _start_ attribute of the given exception object to _start_. Return `0` on success, `-1` on failure.
```

--------------------------------

### Python Managing Packages with pip

Source: https://docs.python.org/3/contents

Explains how to use the 'pip' package installer to manage Python libraries within a project or virtual environment.

```python
# Install a package
# pip install requests
# List installed packages
# pip list
```

--------------------------------

### Basic Unix-style Option Parsing with getopt

Source: https://docs.python.org/3/library/getopt

Demonstrates how to use the getopt() function with Unix-style short options. It parses a list of arguments, separating them into option-argument pairs and remaining arguments. This example shows the basic usage and output format.

```python
import getopt

args = '-a -b -cfoo -d bar a1 a2'.split()
optlist, args = getopt.getopt(args, 'abc:d:')
print(optlist)
print(args)
```

--------------------------------

### PEP 552 Documentation Links

Source: https://docs.python.org/3/genindex-P

Provides links to official Python documentation and changelogs related to PEP 552, focusing on C-API initialization and importlib.

```python
importlib
py_compile
__future__
typing
contextvars
asyncio

```

--------------------------------

### Multiprocessing BaseManager Start

Source: https://docs.python.org/3/genindex-S

Starts the server process for a managed namespace. This allows sharing Python objects between processes using a manager.

```python
from multiprocessing.managers import BaseManager

class MyManager(BaseManager):
    pass

MyManager.register('get_list')

manager = MyManager()
manager.start() # Starts the manager server process

# Now you can access managed objects, e.g., shared_list = manager.get_list()

# To stop the manager:
# manager.shutdown()
```

--------------------------------

### Python Import Examples

Source: https://docs.python.org/3/reference/simple_stmts

Demonstrates various ways to import modules and attributes in Python, including aliasing and importing specific attributes.

```python
importfoo                 # foo imported and bound locally
importfoo.bar.baz         # foo, foo.bar, and foo.bar.baz imported, foo bound locally
importfoo.bar.bazasfbb  # foo, foo.bar, and foo.bar.baz imported, foo.bar.baz bound as fbb
fromfoo.barimport baz    # foo, foo.bar, and foo.bar.baz imported, foo.bar.baz bound as baz
fromfooimport attr       # foo imported and foo.attr bound as attr
```

--------------------------------

### Example: Creating an Isolated Sub-Interpreter

Source: https://docs.python.org/3/c-api/init

Demonstrates how to configure and create a new sub-interpreter with specific isolation settings, such as disabling fork, exec, and using its own GIL.

```c
PyInterpreterConfig config = {
    .use_main_obmalloc = 0,
    .allow_fork = 0,
    .allow_exec = 0,
    .allow_threads = 1,
    .allow_daemon_threads = 0,
    .check_multi_interp_extensions = 1,
    .gil = PyInterpreterConfig_OWN_GIL,
};
PyThreadState* tstate = NULL;
PyStatus status = Py_NewInterpreterFromConfig(&tstate, &config);
if (PyStatus_Exception(status)) {
    Py_ExitStatusException(status);
}
```

--------------------------------

### INI File Structure Example

Source: https://docs.python.org/3/library/configparser

Demonstrates the structure of a typical INI configuration file, including sections, key-value pairs, multiline values, and comments.

```ini
[Simple Values]
key=value
spaces in keys=allowed
spaces in values=allowed as well
spaces around the delimiter=obviously
you can also use:to delimit keys from values

[All Values Are Strings]
values like this:1000000
or this:3.14159265359
are they treated as numbers?:no
integers, floats and booleans are held as:strings
can use the API to get converted values directly:true

[Multiline Values]
chorus:I'm a lumberjack, and I'm okay
I sleep all night and I work all day

[No Values]
key_without_value
empty string value here=

[You can use comments]
# like this
; or this

# By default only in an empty line.
# Inline comments can be harmful because they prevent users
# from using the delimiting characters as parts of values.
# That being said, this can be customized.

[Sections Can Be Indented]
can_values_be_as_well=True
does_that_mean_anything_special=False
purpose=formatting for readability
multiline_values=are
handled just fine as
long as they are indented
deeper than the first line
of a value
# Did I mention we can indent comments, too?

```

--------------------------------

### Python http.client Module Get Functions

Source: https://docs.python.org/3/genindex-G

Implements the client side of the HTTP protocol. Includes a method to get the response from a connection.

```APIDOC
http.client.HTTPConnection Method:

getresponse()
  Reads and returns the next response from the server.
  Returns: An HTTPResponse object.
```

--------------------------------

### Python urllib.request Module Get Functions

Source: https://docs.python.org/3/genindex-G

Extends the urllib.request module for opening URLs. Includes a function to get a dictionary of proxies.

```APIDOC
urllib.request Module:

getproxies()
  Returns a dictionary of protocol-to-proxy mappings.
  Returns: A dictionary of proxies.
```

--------------------------------

### Client Socket Example (Custom Context)

Source: https://docs.python.org/3/library/ssl

Illustrates creating a client socket with a custom SSL context, specifying the TLS protocol and loading a certificate bundle for verification. This example focuses on IPv4 connections.

```python
hostname = 'www.python.org'
# PROTOCOL_TLS_CLIENT requires valid cert chain and hostname
context = ssl.SSLContext(ssl.PROTOCOL_TLS_CLIENT)
context.load_verify_locations('path/to/cabundle.pem')

with socket.socket(socket.AF_INET, socket.SOCK_STREAM, 0) as sock:
    with context.wrap_socket(sock, server_hostname=hostname) as ssock:
        print(ssock.version())
```

--------------------------------

### Python threading Module Get Functions

Source: https://docs.python.org/3/genindex-G

Supports creating and managing threads. Includes a function to get the current profiling function.

```APIDOC
threading Module:

getprofile()
  Returns the current profiling function, or None if profiling is not enabled.
  Returns: The current profiling function or None.
```

--------------------------------

### Python Multiprocessing Pool Example

Source: https://docs.python.org/3/library/multiprocessing

Demonstrates the creation and basic usage of a multiprocessing Pool in Python. This snippet shows how to initialize a pool and submit tasks using apply_async.

```python
import multiprocessing

def worker_function(x):
    return x * x

if __name__ == "__main__":
    # Create a pool of 4 worker processes
    with multiprocessing.Pool(processes=4) as pool:
        # Submit tasks asynchronously
        results = [pool.apply_async(worker_function, (i,)) for i in range(10)]
        
        # Get results from the async tasks
        for res in results:
            print(res.get())

```

--------------------------------

### Home Scheme Installation Directories (POSIX)

Source: https://docs.python.org/3/library/sysconfig

Details the installation paths for the home scheme on POSIX systems. This scheme allows users to build and maintain a personal stash of Python modules.

```python
Path | Installation directory
_stdlib_ | _home_/lib/python
_platstdlib_ | _home_/lib/python
_platlib_ | _home_/lib/python
_purelib_ | _home_/lib/python
_include_ | _home_/include/python
_platinclude_ | _home_/include/python
_scripts_ | _home_/bin
_data_ | _home_
```

--------------------------------

### Installing Python Development Files (Debian/Red Hat)

Source: https://docs.python.org/3/faq/extending

Instructions for installing necessary development files for compiling Python extensions on Debian and Red Hat-based Linux systems. These packages provide header files and libraries required for building C extensions.

```bash
# For Red Hat:
sudo yum install python3-devel

# For Debian:
sudo apt-get install python3-dev
```

--------------------------------

### Python String format() - Keyword Arguments

Source: https://docs.python.org/3/tutorial/inputoutput

Shows how to use keyword arguments in str.format() by referencing argument names within the format fields.

```python
print('This {food} is {adjective}.'.format(
      food='spam', adjective='absolutely horrible'))
```

--------------------------------

### XML SAX ContentHandler Methods

Source: https://docs.python.org/3/genindex-S

Methods for handling content events during XML parsing with the SAX ContentHandler. This includes document start, element start, and prefix mapping.

```APIDOC
xml.sax.handler.ContentHandler:
  startDocument()
    Called at the beginning of the XML document.
  startElement(name, attrs)
    Called when an element starts.
    Parameters:
      name: The element name.
      attrs: The element attributes.
  startElementNS(name, qname, attrs)
    Called when an element with namespace information starts.
    Parameters:
      name: The element name with namespace.
      qname: The qualified name of the element.
      attrs: The element attributes.
  startPrefixMapping(prefix, uri)
    Called when a namespace prefix mapping starts.
```

--------------------------------

### Convert Doctest to Script Example

Source: https://docs.python.org/3/library/doctest

Demonstrates how to use doctest.testsource to convert an object's doctests into a Python script.

```python
import doctest

# Assuming 'a' is a module with a function 'f'
# print(doctest.testsource(a, "a.f"))

```

--------------------------------

### Archived Porting Guide

Source: https://docs.python.org/3/howto/pyporting

This entry points to the archived version of the original porting guide, which is no longer maintained but may contain useful information for users who need to refer to older documentation. It's relevant for those working with older Python 3 versions or seeking historical context.

```APIDOC
Archived Python 2 to 3 Porting Guide:
  - Location: https://docs.python.org/3.10/howto/pyporting.html
  - Note: Discontinued since Python 3.11, but may contain useful guidance.
```

--------------------------------

### unittest setUpModule and tearDownModule Fixtures

Source: https://docs.python.org/3/library/unittest

Details the use of `setUpModule` and `tearDownModule` functions for setting up and tearing down resources once per module.

```python
import unittest

shared_resource = None

def setUpModule():
    global shared_resource
    shared_resource = "Module Resource"
    print("\nSetting up module")

def tearDownModule():
    print("\nTearing down module")

class ModuleFixtureExample(unittest.TestCase):
    def test_module_resource(self):
        self.assertIsNotNone(shared_resource)
```

--------------------------------

### socketserver.TCPServer Example - Client Side

Source: https://docs.python.org/3/library/socketserver

A Python example demonstrating the client-side implementation for connecting to a `socketserver.TCPServer`. It imports the `socket` and `sys` modules to establish a connection and send data.

```python
import socket
import sys

HOST, PORT = "localhost", 9999
data = " ".join(sys.argv[1:])

# Create a socket (should be TCP)
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as sock:
    # Connect to server and send data
    sock.connect((HOST, PORT))
    sock.sendall(bytes(data + "\n", "utf-8"))

    # Receive data from the server and shut down
    received = str(sock.recv(1024), "utf-8")

print(f"Sent:     {data}")
print(f"Received: {received}")

```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/index

A collection of links to essential Python resources, including the PEP Index, guides for beginners and developers, and a list of Python-related talks and books.

```markdown
* [PEP Index](https://peps.python.org/)
* [Beginner's Guide](https://wiki.python.org/moin/BeginnersGuide)
* [Book List](https://wiki.python.org/moin/PythonBooks)
* [Audio/Visual Talks](https://www.python.org/doc/av/)
* [Python Developer’s Guide](https://devguide.python.org/)
```

--------------------------------

### Start HTTP Server and Open Browser

Source: https://docs.python.org/3/library/pydoc

Starts an HTTP server and automatically opens a web browser to the module index page.

```shell
python -m pydoc -b
```

--------------------------------

### Test Discovery with Package Name as Start Directory

Source: https://docs.python.org/3/library/unittest

Shows how to use a package name instead of a file path for the start directory in test discovery. The unittest module will import the package and use its filesystem location.

```bash
python -m unittest discover -s myproject.subpackage.test
```

--------------------------------

### XML ElementTree TreeBuilder Start Namespace

Source: https://docs.python.org/3/genindex-S

Starts a new namespace declaration in the XML tree. This is used when defining or using XML namespaces.

```python
from xml.etree.ElementTree import TreeBuilder

builder = TreeBuilder()
builder.start('root', {'xmlns': 'http://example.com/ns'})
builder.start_ns('prefix', 'http://example.com/other_ns') # Declare a new namespace
builder.start('element', {'prefix:attr': 'value'})
builder.end('element')
builder.end('root')
```

--------------------------------

### Python optparse Callback Examples

Source: https://docs.python.org/3/contents

Demonstrates callback functionalities within the optparse module for handling fixed and variable arguments during command-line option parsing.

```python
import optparse

parser = optparse.OptionParser()

# Callback example 5: fixed arguments
def callback_fixed(option, opt, value, parser):
    setattr(parser.values, option.dest, value.upper())

parser.add_option("--uc", action="callback", callback=callback_fixed, 
                  callback_args=(), # No extra args passed to callback
                  help="Convert value to uppercase")

# Callback example 6: variable arguments
def callback_variable(option, opt, value, parser):
    args = value.split(",")
    setattr(parser.values, option.dest, args)

parser.add_option("--csv", action="callback", callback=callback_variable, 
                  help="Comma-separated values")

(options, args) = parser.parse_args()

print(f"Uppercase value: {options.uc}")
print(f"CSV values: {options.csv}")
```

--------------------------------

### Python tracemalloc Usage Examples

Source: https://docs.python.org/3/library/tracemalloc

Illustrates practical examples of using the tracemalloc module to analyze memory usage, including displaying top allocations and computing differences.

```python
import tracemalloc

# Start tracing memory allocations
tracemalloc.start()

# Example 1: Display the top 10 memory allocations
print("--- Example 1: Top 10 Memory Allocations ---")
# Simulate some memory allocations
list_a = [i for i in range(1000)]
dict_b = {str(i): i for i in range(500)}

snapshot = tracemalloc.take_snapshot()
top_stats = snapshot.statistics('lineno')

print("Top 10 memory blocks:")
for stat in top_stats[:10]:
    print(stat)

# Example 2: Compute differences between two snapshots
print("\n--- Example 2: Memory Allocation Differences ---")
# First snapshot
snapshot1 = tracemalloc.take_snapshot()

# Simulate more memory allocations
list_c = [i * 2 for i in range(2000)]
dict_d = {str(i): i * 2 for i in range(1000)}

# Second snapshot
snapshot2 = tracemalloc.take_snapshot()

# Compare snapshots
top_stats_diff = snapshot2.compare_to(snapshot1, 'lineno')

print("[ Top 10 differences ]")
for stat in top_stats_diff[:10]:
    print(stat)

# Example 3: Get the traceback of a memory block
print("\n--- Example 3: Traceback of a Memory Block ---")
large_list = [0] * 10000
traceback = tracemalloc.get_object_traceback(large_list)

if traceback:
    print("Traceback for 'large_list':")
    for frame in traceback.walk():
        print(f"  File \"{frame.filename}\", line {frame.lineno}, in {frame.name}")
else:
    print("'large_list' traceback not found.")

# Stop tracing
tracemalloc.stop()

```

--------------------------------

### Example tp_traverse Handler Implementation

Source: https://docs.python.org/3/c-api/gcsupport

A C code example demonstrating how to implement a `tp_traverse` handler for a custom Python object using the `Py_VISIT` macro.

```c
static int
my_traverse(Noddy* self, visitproc visit, void* arg)
{
  Py_VISIT(self->foo);
  Py_VISIT(self->bar);
  return 0;
}
```

--------------------------------

### Python C API Initialization Configuration

Source: https://docs.python.org/3/using/windows

Details the use of PyConfig.module_search_paths for embedding Python.

```APIDOC
PyConfig.module_search_paths:
  Type: list[str]
  Description: A list of paths to be added to the module search path. This should be set before calling Py_InitializeFromConfig().

Py_InitializeFromConfig():
  Description: Initializes the Python interpreter using a PyConfig structure.
  Parameters:
    - config: A pointer to a PyConfig structure containing initialization settings.
```

--------------------------------

### Asyncio Loop Start TLS

Source: https://docs.python.org/3/genindex-S

Starts a Transport Layer Security (TLS) handshake for a stream. This is used to secure network communication over a stream.

```python
import asyncio

async def secure_stream():
    # Assuming 'transport' and 'protocol' are already set up
    # For example, from asyncio.create_connection or asyncio.start_server
    transport, protocol = await asyncio.get_event_loop().create_connection(
        lambda: asyncio.Protocol(), 'example.com', 443)

    # Start TLS handshake
    await transport.start_tls(ssl=None) # Use default SSL context or provide your own
    print("TLS handshake started")

    # ... send/receive encrypted data ...

    transport.close()

if __name__ == "__main__":
    asyncio.run(secure_stream())
```

--------------------------------

### C Extension Module Setup

Source: https://docs.python.org/3/extending/extending

Initial C code required for a Python extension module, including necessary headers and definitions.

```c
#define PY_SSIZE_T_CLEAN
#include<Python.h>
```

--------------------------------

### Python Signal Handler Installation

Source: https://docs.python.org/3/c-api/init_config

Determines whether Python installs its signal handlers. The default behavior varies between standard Python mode and isolated mode.

```APIDOC
PyConfig.install_signal_handlers:
  Type: int
  Description: Install Python signal handlers?
  Default: 1 (Python mode), 0 (isolated mode)
```

--------------------------------

### Starting the Python Interpreter

Source: https://docs.python.org/3/faq/windows

Demonstrates how to launch the Python interpreter in interactive mode from the Windows command prompt. This allows for direct execution of Python statements.

```windows-cmd
C:\Users\YourName> py
```

```python
Python 3.6.4 (v3.6.4:d48eceb, Dec 19 2017, 06:04:45) [MSC v.1900 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

--------------------------------

### Install Python using nuget.exe

Source: https://docs.python.org/3/using/windows

Installs the latest version of Python for 64-bit or 32-bit machines using the nuget.exe command-line tool. You can specify a particular version using the -Version flag and an output directory with the -OutputDirectory flag.

```powershell
nuget install python -Source https://api.nuget.org/v3/index.json
```

--------------------------------

### ensurepip Command Line Options

Source: https://docs.python.org/3/genindex-Symbols

Options for the `ensurepip` module to manage package installation.

```APIDOC
--root ROOT
  Specifies the root directory for package installation.

--user
  Installs packages in the user site-packages directory.
```

--------------------------------

### Python Multiprocessing Connection Client Example

Source: https://docs.python.org/3/library/multiprocessing

This example shows how to connect to a server using multiprocessing.connection.Client, receive data including lists, bytes, and arrays, and process the received information.

```python
from multiprocessing.connection import Client
from array import array

address = ('localhost', 6000)

with Client(address, authkey=b'secret password') as conn:
    print(conn.recv())                  # => [2.25, None, 'junk', float]

    print(conn.recv_bytes())            # => 'hello'

    arr = array('i', [0, 0, 0, 0, 0])
    print(conn.recv_bytes_into(arr))    # => 8
    print(arr)                          # => array('i', [42, 1729, 0, 0, 0])

```

--------------------------------

### Python Installation and Removal Guidance

Source: https://docs.python.org/3/faq/installed

Provides advice on how to remove Python based on its installation source and the potential consequences. It covers removal via Control Panel for user-installed versions, using application uninstallers for bundled Python, and strongly advises against removing OS-included Python to avoid breaking dependent tools.

```python
# On Windows, use the Add/Remove Programs icon in the Control Panel.
# If Python was installed by a third-party application, use that application’s uninstaller.
# Removing OS-included Python is not recommended as it may break Python-dependent tools.
```

--------------------------------

### Python Version Navigation

Source: https://docs.python.org/3/library/intro

Lists available Python versions for documentation access, including development and stable releases.

```text
dev (3.15) pre (3.14) 3.13.7 3.12 3.11 3.10 3.9 3.8 3.7 3.6 3.5 3.4 3.3 3.2 3.1 3.0 2.7 2.6
```

--------------------------------

### Installing Python Modules: Parallel Python Versions

Source: https://docs.python.org/3/contents

Information on managing multiple versions of Python installed concurrently on the same system. This is crucial for projects with different Python version requirements.

```APIDOC
Work with multiple versions of Python installed in parallel:
  Explains strategies and tools for managing several Python installations simultaneously.
  Facilitates switching between different Python environments for various projects.
```

--------------------------------

### XML ElementTree TreeBuilder Start

Source: https://docs.python.org/3/genindex-S

Starts a new element in the XML tree. This method is part of the `TreeBuilder` class, used for constructing XML documents.

```python
from xml.etree.ElementTree import TreeBuilder

builder = TreeBuilder()
builder.start('root', {'attr': 'value'})
builder.start('child', {}) # Starts a child element
builder.end('child')
builder.end('root')

# The resulting XML can be obtained from the builder
```

--------------------------------

### Python Initialization Phases

Source: https://docs.python.org/3/c-api/init_config

Describes the two main phases of Python initialization: 'Core' and 'Main'. The 'Core' phase initializes built-in types, exceptions, and frozen modules, while the 'Main' phase completes initialization by configuring importlib, applying path configuration, installing signal handlers, and enabling optional features.

```APIDOC
Multi-Phase Initialization:
  Core Phase:
    - Builtin types
    - Builtin exceptions
    - Builtin and frozen modules
    - Partially initialized sys module (e.g., sys.path not yet available)
  Main Phase:
    - Install and configure importlib
    - Apply Path Configuration
    - Install signal handlers
    - Finish sys module initialization (e.g., create sys.stdout, sys.path)
    - Enable optional features (e.g., faulthandler, tracemalloc)
    - Import the site module

PyConfig._init_main:
  - If set to 0, Py_InitializeFromConfig() stops at the 'Core' initialization phase.

PyStatus_Py_InitializeMain():
  - Moves to the 'Main' initialization phase, completing Python initialization.
  - Path Configuration is applied during this phase.
  - Allows customization of Python in Python before the Main phase.
  - API is private and provisional, subject to change.
```

--------------------------------

### Python __future__ Module Example

Source: https://docs.python.org/3/glossary

Illustrates the usage of the __future__ module to enable features from future Python releases. This example shows how to check the version of the 'division' feature.

```python
>>> import __future__
>>> __future__.division
_Feature((2, 2, 0, 'alpha', 2), (3, 0, 0, 'alpha', 0), 8192)
```

--------------------------------

### OS Module get Functions

Source: https://docs.python.org/3/genindex-G

Provides functions for interacting with the operating system, including getting process IDs, signal handlers, file sizes, and user IDs.

```python
import os
import os.path
import signal

# Get process ID
pid = os.getpid()
print(f"Current Process ID: {pid}")

# Get parent process ID
ppid = os.getppid()
print(f"Parent Process ID: {ppid}")

# Get user ID
uid = os.getuid()
print(f"User ID: {uid}")

# Get process group ID
gid = os.getpgrp()
print(f"Process Group ID: {gid}")

# Get session ID
sid = os.getsid(0) # 0 refers to the current process
print(f"Session ID: {sid}")

# Get signal handler (example for SIGINT)
signal_handler = signal.getsignal(signal.SIGINT)
print(f"Signal handler for SIGINT: {signal_handler}")

# Get file size (example)
# Create a dummy file for demonstration
file_path = "temp_file.txt"
with open(file_path, "w") as f:
    f.write("This is a test file.")

file_size = os.path.getsize(file_path)
print(f"Size of '{file_path}': {file_size} bytes")

os.remove(file_path) # Clean up the dummy file
```

--------------------------------

### socketserver.BaseServer Methods

Source: https://docs.python.org/3/genindex-S

Provides documentation for key methods of the socketserver.BaseServer class, including server activation, binding, and closing.

```APIDOC
server_activate()
  Activates the server.

server_bind()
  Binds the server to an address.

server_close()
  Closes the server.

service_actions()
  Performs service-specific actions.
```

--------------------------------

### Regex Match Start Position

Source: https://docs.python.org/3/genindex-S

Returns the starting index of the substring that matched the regular expression. This is a method of a match object returned by `re.search()` or `re.match()`.

```python
import re

text = "Hello world"
match = re.search("world", text)

if match:
    start_index = match.start()
    print(f"Match found starting at index: {start_index}") # Output: 6
```

--------------------------------

### EnvBuilder Dependency Management and Script Installation

Source: https://docs.python.org/3/library/venv

This section covers methods related to managing dependencies within the virtual environment and assisting in the installation of custom scripts.

```APIDOC
EnvBuilder Advanced Methods:

upgrade_dependencies(_context_)
  Upgrades the core venv dependency packages (e.g., pip) in the environment by shelling out to the environment's pip executable. (Added in 3.9, setuptools no longer a core dependency since 3.12).

install_scripts(_context_, _path_)
  Assists in installing custom scripts into the virtual environment. Can be called from setup_scripts() or post_setup() in subclasses.
```

--------------------------------

### Variable Annotation Example

Source: https://docs.python.org/3/glossary

Illustrates the use of variable annotations in Python for type hinting. This example shows how to declare a variable with an expected integer type and an initial value.

```python
class C:
    field: 'annotation'

count: int = 0
```

--------------------------------

### os.path.relpath()

Source: https://docs.python.org/3/genindex-R

The `relpath()` function in the `os.path` module computes a relative path. It takes a starting directory and an ending directory and returns the path from the start to the end.

```python
import os

start = '/home/user/project'
end = '/home/user/project/src/main.py'

relative_path = os.path.relpath(end, start)
print(relative_path)  # Output: src/main.py
```

--------------------------------

### SocketHandler Initialization and Methods

Source: https://docs.python.org/3/library/logging

Details the constructor and key methods of the SocketHandler class, including socket creation, emission, closing, and error handling.

```APIDOC
class logging.handlers.SocketHandler(_host_, _port_)
  Initializes a SocketHandler to communicate with a remote machine.
  Parameters:
    _host_: The hostname or IP address of the remote machine.
    _port_: The port number to connect to. If None, a Unix domain socket is created.

  close()
    Closes the underlying socket connection.

  emit(_record_)
    Serializes the log record and sends it over the socket. Re-establishes connection if lost.

  handleError()
    Handles errors during emission, typically by closing the socket to allow reconnection.

  makeSocket()
    Factory method to create the socket. Subclasses can override this to create different socket types.

  makePickle(_record_)
    Serializes the log record's attribute dictionary into a binary format with a length prefix for transmission.
    Example:
    data = pickle.dumps(record_attr_dict, 1)
    datalen = struct.pack('>L', len(data))
    return datalen + data
    Note: Pickles are not completely secure; consider signing or disabling global unpickling.

  send(_packet_)
    Sends a pickled byte string packet over the socket. Handles partial sends.

  createSocket()
    Attempts to create a socket with exponential back-off on failure. Controls retry behavior via:
      retryStart: Initial delay (default: 1.0 seconds).
      retryFactor: Multiplier for delay (default: 2.0).
      retryMax: Maximum delay (default: 30.0 seconds).
```

--------------------------------

### Python asyncio Subprocess Protocol Example

Source: https://docs.python.org/3/library/asyncio-protocol

Shows how to use `loop.subprocess_exec()` with a custom `SubprocessProtocol` to interact with a child process. This example demonstrates reading output from a subprocess.

```python
import asyncio

class SleepProtocol(asyncio.SubprocessProtocol):
    def __init__(self):
        self.data = b''

    def connection_made(self, transport):
        print('Process started')

    def pipe_data_received(self, fd, data):
        print(f'Received data: {data.decode()}\n')
        self.data += data

    def process_exited(self, status):
        print(f'Process exited with status: {status}\n')

async def main():
    loop = asyncio.get_running_loop()

    # Example: Run 'echo Hello World' command
    transport, protocol = await loop.subprocess_exec(
        SleepProtocol,
        'echo',
        'Hello World',
        stdout=asyncio.subprocess.PIPE
    )

    # Wait for the process to complete
    await asyncio.wait([asyncio.create_task(asyncio.sleep(0.1))]) # Small delay to allow output
    
    # You can access the collected data from the protocol instance
    print(f'Collected data: {protocol.data.decode()}\n')

asyncio.run(main())
```

--------------------------------

### Python List Methods Example

Source: https://docs.python.org/3/tutorial/datastructures

An example demonstrating the usage of various Python list methods like count, index, reverse, append, sort, and pop.

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.count('apple')
2
>>> fruits.count('tangerine')
0
>>> fruits.index('banana')
3
>>> fruits.index('banana', 4)  # Find next banana starting at position 4
6
>>> fruits.reverse()
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
>>> fruits.append('grape')
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']
>>> fruits.sort()
>>> fruits
['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange', 'pear']
>>> fruits.pop()
'pear'
```

--------------------------------

### Subclassing QueueHandler and QueueListener (ZeroMQ Example)

Source: https://docs.python.org/3/howto/logging-cookbook

Illustrates subclassing `QueueHandler` and `QueueListener` to create a robust logging system using ZeroMQ for inter-process communication. This is useful for distributed logging.

```python
import logging
import logging.handlers
import queue
import threading
import zmq

class ZeroMQHandler(logging.handlers.QueueHandler):
    def __init__(self, context=None, socket_type=zmq.PUSH):
        super().__init__(queue.Queue(-1))
        self.context = context or zmq.Context()
        self.socket = self.context.socket(socket_type)
        self.socket.bind("tcp://127.0.0.1:5557")

    def emit(self, record):
        try:
            self.socket.send_pyobj(self.format(record))
        except Exception:
            self.handleError(record)

class ZeroMQListener(logging.handlers.QueueListener):
    def __init__(self, handlers, respect_handler_level=False, context=None, socket_type=zmq.PULL):
        super().__init__([], respect_handler_level=respect_handler_level)
        self.context = context or zmq.Context()
        self.socket = self.context.socket(socket_type)
        self.socket.connect("tcp://127.0.0.1:5557")
        self.handlers = handlers
        self._stop_event = threading.Event()

    def _monitor(self):
        while not self._stop_event.is_set():
            try:
                log_record_str = self.socket.recv_pyobj()
                for handler in self.handlers:
                    try:
                        # Reconstruct LogRecord if needed, or just process the string
                        # For simplicity, we'll assume handlers can process strings
                        handler.handle(logging.LogRecord(name='', level=logging.INFO, pathname='', 
                                                         lineno=0, msg=log_record_str, args=(), exc_info=None))
                    except Exception:
                        logging.Error('Error processing log record in listener', exc_info=True)
            except zmq.Again:
                continue
            except Exception:
                logging.Error('Error receiving log record', exc_info=True)

# Example Usage:
# logger = logging.getLogger('zmq_logger')
# zmq_handler = ZeroMQHandler()
# logger.addHandler(zmq_handler)
# logger.setLevel(logging.INFO)

# listener_handlers = [logging.StreamHandler()]
# listener = ZeroMQListener(listener_handlers)
# listener.start()

# logger.info('Sending log message via ZeroMQ')
# time.sleep(2) # Give time for listener to process
# listener.stop()
```

--------------------------------

### Pure Python Equivalents: Methods

Source: https://docs.python.org/3/howto/descriptor

Explains how functions and methods, including static methods and class methods, are implemented using the descriptor protocol.

```python
# Instance method (descriptor)
def instance_method(self, arg):
    pass

# Static method (descriptor)
@staticmethod
def static_method(arg):
    pass

# Class method (descriptor)
@classmethod
def class_method(cls, arg):
    pass
```

--------------------------------

### PDB Alias Example

Source: https://docs.python.org/3/library/pdb

An example of creating a custom alias 'pi' in PDB to print instance variables of an object.

```python
# Print instance variables (usage "pi classInst")
alias pi for k in %1.__dict__.keys(): print(f"%1.{k} = {%1.__dict__[k]}")
```

--------------------------------

### socketserver.TCPServer Example

Source: https://docs.python.org/3/library/socketserver

Demonstrates the creation and usage of a TCP server using the socketserver.TCPServer class. This example typically involves setting up a request handler and binding the server to a specific address and port.

```python
import socketserver

class MyTCPHandler(socketserver.BaseRequestHandler):
    """The request handler class for our server."""

    def handle(self):
        # self.request is the TCP socket connected to the client
        self.data = self.request.recv(1024).strip()
        print(f"{self.client_address[0]} wrote: {self.data.decode()}")

        # just send back the same data, but upper-cased
        self.request.sendall(self.data.upper())

if __name__ == "__main__":
    HOST, PORT = "localhost", 9999
    # Create the server, binding to localhost on port 9999
    with socketserver.TCPServer((HOST, PORT), MyTCPHandler) as server:
        # Activate the server; this will keep running until you
        # interrupt the program with Ctrl-C
        server.serve_forever()
```

--------------------------------

### Running unittest Tests from Command Line

Source: https://docs.python.org/3/library/unittest

Demonstrates how to execute tests using the `unittest` module from the command line. You can specify test modules, classes, or methods directly. It also shows how to run tests using file paths and enable verbose output.

```python
python -m unittest test_module1 test_module2
python -m unittest test_module.TestClass
python -m unittest test_module.TestClass.test_method
python -m unittest tests/test_something.py
python -m unittest -v test_module
python -m unittest
python -m unittest -h
```

--------------------------------

### itertools.cycle() Example

Source: https://docs.python.org/3/howto/functional

Illustrates the itertools.cycle() function, which repeats elements from an iterable indefinitely. The example shows cycling through a list.

```python
import itertools

my_list = [1, 2, 3, 4, 5]
cycle_iterator = itertools.cycle(my_list)

# Get the first 10 elements from the cycle
print([next(cycle_iterator) for _ in range(10)])
```

--------------------------------

### Python AST Set Comprehension Example

Source: https://docs.python.org/3/library/ast

Provides an example of the AST representation for a Python set comprehension. It parses a set comprehension and outputs its detailed AST structure.

```python
import ast

numbers = [1, 2, 3]
print(ast.dump(ast.parse('{x for x in numbers}', mode='eval'), indent=4))
```

--------------------------------

### itertools.chain() Example

Source: https://docs.python.org/3/howto/functional

Demonstrates itertools.chain(), which combines multiple iterables into a single iterator. The example chains a list and a tuple.

```python
import itertools

list_a = ['a', 'b', 'c']
tuple_b = (1, 2, 3)

chained_iterator = itertools.chain(list_a, tuple_b)
print(list(chained_iterator))
```

--------------------------------

### Python Readline Completion Example

Source: https://docs.python.org/3/library/rlcompleter

Demonstrates how to use the rlcompleter module to enable tab completion for Python commands in the readline interface. This involves importing both modules, binding the tab key to the completion function, and then showing an example of how completion works.

```python
>>> import rlcompleter
>>> import readline
>>> readline.parse_and_bind("tab: complete")
>>> readline. <TAB PRESSED>
readline.__doc__          readline.get_line_buffer(
readline.__file__         readline.insert_text(
readline.__name__         readline.parse_and_bind(
>>> readline.
```

--------------------------------

### Initialize Curses Application

Source: https://docs.python.org/3/howto/curses

Initializes the curses library, sets up the terminal, and returns the main screen window object (stdscr). This is the first step in any curses application.

```python
import curses
stdscr = curses.initscr()
```

--------------------------------

### Basic Pool Usage Example

Source: https://docs.python.org/3/library/multiprocessing

A simple example demonstrating how to create a multiprocessing Pool, define a worker function, and use the pool to process data asynchronously.

```python
from multiprocessing import Pool
import time

def f(x):
    return x*x

if __name__ == '__main__':
    with Pool(processes=4) as pool:         # start 4 worker processes
        # ... further pool operations ...
```

--------------------------------

### Platform Module Usage

Source: https://docs.python.org/3/library/allos

Demonstrates how to use the platform module to retrieve information about the underlying operating system and hardware.

```python
import platform

print(f"System: {platform.system()}")
print(f"Node Name: {platform.node()}")
print(f"Release: {platform.release()}")
print(f"Version: {platform.version()}")
print(f"Machine: {platform.machine()}")
print(f"Processor: {platform.processor()}")
print(f"Python Version: {platform.python_version()}")
```

--------------------------------

### Interactive Debugging Session with Doctest

Source: https://docs.python.org/3/library/doctest

An example of an interactive Python session demonstrating how to use the debugger (pdb) after hitting a `pdb.set_trace()` call within a doctest.

```python
>>> import doctest
>>> doctest.testmod(a)
--Return--
> <doctest a[1]>(3)g()->None
-> import pdb; pdb.set_trace()
(Pdb) list
  1     def g(x):
  2         print(x+3)
  3  ->     import pdb; pdb.set_trace()
[EOF]
(Pdb) p x
6
(Pdb) step
--Return--
> <doctest a[0]>(2)f()->None
-> g(x*2)
(Pdb) list
  1     def f(x):
  2  ->     g(x*2)
[EOF]
(Pdb) p x
3
(Pdb) step
--Return--
> <doctest a[2]>(1)?()->None
-> f(3)
(Pdb) cont
(0, 3)
>>>

```

--------------------------------

### Python Random Module Command-Line Examples

Source: https://docs.python.org/3/library/random

This section provides practical examples of using the Python random module from the command line. It demonstrates how to select a random item from a list, generate a random integer, and generate a random floating-point number.

```bash
$ python "Lobster Thermidor aux crevettes with a Mornay sauce"
Lobster Thermidor aux crevettes with a Mornay sauce

$ python 6
6

$ python 1.8
1.7080016272295635

$ python -c "Lobster Thermidor aux crevettes with a Mornay sauce"
egg

$ python -i 6
3

$ python -f 1.8
1.5666339105010318

$ python -i 6
5

$ python -f 6
3.1942323316565915
```

--------------------------------

### Python Readline Completion Example

Source: https://docs.python.org/3/library/readline

Illustrates how to set up a custom completer function for Python's readline module. This example shows setting a completer, delimiters, and a display hook.

```python
import readline
import rlcompleter

def my_completer(text, state):
    options = [i for i in __builtins__ if i.startswith(text)]
    if state < len(options):
        return options[state]
    else:
        return None

# Set the completer function
readline.set_completer(my_completer)

# Set delimiters (e.g., to include '.' for attribute completion)
readline.set_completer_delims(' 	
`~!@#$%^&*()-=+[{]}\|;:'",<>/?')

# Optional: Set a hook to display matches
def display_matches(substitution, matches, longest_match_length):
    print('\nPossible completions: {}'.format(matches))

readline.set_completion_display_matches_hook(display_matches)

# Enable tab completion
readline.parse_and_bind('tab: complete')
```

--------------------------------

### Other Python Resources

Source: https://docs.python.org/3/.13

Lists important external resources for Python developers, including the Python Enhancement Proposals (PEP) index, beginner guides, book recommendations, and talks.

```python
# PEP Index
# https://peps.python.org/

# Beginner's Guide
# https://wiki.python.org/moin/BeginnersGuide

# Book List
# https://wiki.python.org/moin/PythonBooks

# Audio/Visual Talks
# https://www.python.org/doc/av/

# Python Developer’s Guide
# https://devguide.python.org/
```

--------------------------------

### Python sys.path Initialization on Windows

Source: https://docs.python.org/3/using/windows

Explains how sys.path is populated on Windows when no ._pth file is found. It covers the order of operations including current directory, PYTHONPATH, registry entries, PYTHONHOME, and default paths.

```python
import sys

# sys.path is populated based on:
# 1. Current directory
# 2. PYTHONPATH environment variable (semicolon-separated on Windows)
# 3. Registry entries (SOFTWARE\Python\PythonCore{version}\PythonPath)
# 4. PYTHONHOME environment variable or deduced Python Home
# 5. Default relative paths if home cannot be located
```

--------------------------------

### Mocking Examples with unittest.mock

Source: https://docs.python.org/3/library/development

Demonstrates various advanced techniques for using the `unittest.mock` library, including checking multiple calls, handling mutable arguments, nesting patches, mocking dictionaries, subclassing mocks, and using `patch.dict` for mocking imports. It also covers tracking call order and more complex argument matching.

```python
from unittest.mock import mock, MagicMock, patch

# Checking multiple calls with mock
# ... example code ...

# Coping with mutable arguments
# ... example code ...

# Nesting Patches
# ... example code ...

# Mocking a dictionary with MagicMock
# ... example code ...

# Mock subclasses and their attributes
# ... example code ...

# Mocking imports with patch.dict
# ... example code ...

# Tracking order of calls and less verbose call assertions
# ... example code ...

# More complex argument matching
# ... example code ...
```

--------------------------------

### WSGI Conformance Validation Example

Source: https://docs.python.org/3/library/wsgiref

Demonstrates how to use wsgiref.validate.validator to wrap a WSGI application and check for conformance. The example includes a non-compliant application to trigger validation errors.

```python
from wsgiref.validate import validator
from wsgiref.simple_server import make_server

# Our callable object which is intentionally not compliant to the
# standard, so the validator is going to break
def simple_app(environ, start_response):
    status = '200 OK'  # HTTP Status
    headers = [('Content-type', 'text/plain')]  # HTTP Headers
    start_response(status, headers)

    # This is going to break because we need to return a list, and
    # the validator is going to inform us
    return b"Hello World"

# This is the application wrapped in a validator
validator_app = validator(simple_app)

with make_server('', 8000, validator_app) as httpd:
    print("Listening on port 8000....")
    httpd.serve_forever()

```

--------------------------------

### Tracemalloc Start

Source: https://docs.python.org/3/genindex-S

Starts tracing memory allocations. This is part of the `tracemalloc` module, which is used for tracing memory leaks and analyzing memory usage in Python programs.

```python
import tracemalloc

tracemalloc.start()

# ... your code that might have memory issues ...

# Get current and peak memory blocks
current, peak = tracemalloc.get_traced_memory()
print(f"Current memory usage: {current / 10**6}MB Peak: {peak / 10**6}MB")

tracemalloc.stop()
```

--------------------------------

### Python 3 Documentation Navigation

Source: https://docs.python.org/3/howto/curses

Provides links to navigate the Python 3 documentation, including the general index, module index, and specific guides like the Descriptor Guide and Porting Extension Modules to Python 3.

```python
from sphinx.application import Sphinx

# Example of how Sphinx might be used internally, not directly user-facing code.
# The actual navigation is handled by HTML generation.
```

--------------------------------

### XML with Namespaces Example

Source: https://docs.python.org/3/library/xml.etree

An example XML structure demonstrating the use of both prefixed and default namespaces.

```xml
<?xml version="1.0"?>
<actors xmlns:fictional="http://characters.example.com"
xmlns="http://people.example.com">
<actor>
<name>John</name>
<fictional:character>Lancelot</fictional:character>
<fictional:character>Archie</fictional:character>
</actor>
<actor>
<name>Eric</name>
<fictional:character>Sir</fictional:character>
<fictional:character>Gunther</fictional:character>
<fictional:character>Commander</fictional:character>
</actor>
</actors>
```

--------------------------------

### Python IMAP4 Client Example

Source: https://docs.python.org/3/library/imaplib

Illustrates basic usage of the IMAP4 client, including connecting, logging in, and performing common operations like fetching emails. This example demonstrates how to interact with an IMAP server using Python's imaplib.

```python
import imaplib

mail = imaplib.IMAP4()
mail.login('user', 'password')
mail.select('inbox')
type, data = mail.search(None, 'ALL')
mail_ids = data[0]

for block in mail_ids.split():
    type, msg_data = mail.fetch(block, '(BODY.PEEK[HEADER])')
    for resp in msg_data:
        if isinstance(resp, tuple):
            print(resp[1].decode('utf-8'))
```

--------------------------------

### SQLite FTS3 Example

Source: https://docs.python.org/3/library/sqlite3

Demonstrates creating a virtual table using FTS3 for full-text searching, inserting data, and querying for specific terms.

```python
import sqlite3

con = sqlite3.connect(':memory:')
con.execute("CREATE VIRTUAL TABLE recipe USING fts3(name, ingredients)")
con.executescript("""
    INSERT INTO recipe (name, ingredients) VALUES('broccoli stew', 'broccoli peppers cheese tomatoes');
    INSERT INTO recipe (name, ingredients) VALUES('pumpkin stew', 'pumpkin onions garlic celery');
    INSERT INTO recipe (name, ingredients) VALUES('broccoli pie', 'broccoli cheese onions flour');
    INSERT INTO recipe (name, ingredients) VALUES('pumpkin pie', 'pumpkin sugar flour butter');
    """)
for row in con.execute("SELECT rowid, name, ingredients FROM recipe WHERE name MATCH 'pie'"):
    print(row)
```

--------------------------------

### Basic Authentication

Source: https://docs.python.org/3/howto/urllib2

Demonstrates how to perform basic HTTP authentication by encoding username and password and adding them to the request headers.

```python
import urllib.request
import urllib.parse

url = 'http://example.com/protected'
username = 'user'
password = 'password'

auth_string = f'{username}:{password}'.encode('utf-8')
encoded_auth = urllib.parse.quote_plus(auth_string)
headers = {'Authorization': f'Basic {encoded_auth.decode()}'}

req = urllib.request.Request(url, headers=headers)

with urllib.request.urlopen(req) as response:
    print(response.read().decode('utf-8'))
```

--------------------------------

### Python re Module Examples

Source: https://docs.python.org/3/library/re

This section contains various practical examples demonstrating the usage of the 're' module in Python. It includes scenarios like checking for pairs, simulating scanf, differentiating between search() and match(), creating a phonebook, text munging, finding adverbs, and writing a tokenizer.

```python
# Example: Checking for a pair
text = 'aabbccddeeff'
match = re.search(r'(..)\1', text)
if match:
    print(f'Found repeating pair: {match.group(1)}')

# Example: Finding all adverbs
import re
text = 'He quickly ran and happily jumped.'
adverbs = re.findall(r'\b\w+ly\b', text)
print(f'Adverbs found: {adverbs}')

```

--------------------------------

### Fetching URLs with urllib

Source: https://docs.python.org/3/howto/urllib2

Demonstrates the basic usage of the urllib package to fetch content from a given URL. This involves opening a URL and reading its data.

```python
import urllib.request

url = 'http://example.com'
with urllib.request.urlopen(url) as response:
    html = response.read()
    print(html.decode('utf-8'))
```

--------------------------------

### Sys Module get Functions

Source: https://docs.python.org/3/genindex-G

Provides access to system-specific parameters and functions, including getting the size of objects, interpreter switch interval, and trace functions.

```python
import sys
import threading

# Get the size of an object in bytes
my_list = [1, 2, 3]
size_in_bytes = sys.getsizeof(my_list)
print(f"Size of the list {my_list}: {size_in_bytes} bytes")

# Get the interpreter's switch interval
switch_interval = sys.getswitchinterval()
print(f"Interpreter switch interval: {switch_interval} seconds")

# Get the current trace function (if any)
trace_func = sys.gettrace()
print(f"Current trace function: {trace_func}")

# Get trace function from threading module (if set)
tracing = threading.gettrace()
print(f"Threading trace function: {tracing}")

# Get the size of interned unicode strings
unicode_interned_size = sys.getunicodeinternedsize()
print(f"Size of interned unicode strings: {unicode_interned_size} bytes")
```

--------------------------------

### Python xml.etree.ElementTree Module Get Functions

Source: https://docs.python.org/3/genindex-G

Provides an API for parsing and creating XML data. Includes a method to get the root element of an XML tree.

```APIDOC
xml.etree.ElementTree.ElementTree Method:

getroot()
  Returns the root element of the XML tree.
  Returns: The root element.
```

--------------------------------

### Python Build System - Main Build Steps

Source: https://docs.python.org/3/using/configure

The primary stages involved in building Python from source code.

```APIDOC
Python Build System - Main Build Steps:
  1. Run ./configure to set up the build environment.
  2. Run make to compile the Python interpreter and modules.
  3. Run make install to install Python on the system.
```

--------------------------------

### ConfigParser with ExtendedInterpolation Example

Source: https://docs.python.org/3/library/configparser

Demonstrates the usage of ConfigParser with ExtendedInterpolation to read configuration strings, specifically showing how to handle comment prefixes and multiline values.

```python
from configparser import ConfigParser, ExtendedInterpolation

parser = ConfigParser(interpolation=ExtendedInterpolation())
# the default BasicInterpolation could be used as well
parser.read_string("""
[DEFAULT]
hash = #

[hashes]
shebang =
  ${hash}!/usr/bin/env python
  ${hash} -*- coding: utf-8 -*-

extensions =
  enabled_extension
  another_extension
  #disabled_by_comment
  yet_another_extension

interpolation not necessary = if # is not at line start
even in multiline values = line #1
  line #2
  line #3
""")

print(parser['hashes']['shebang'])
```

--------------------------------

### Python socket Module Get Functions

Source: https://docs.python.org/3/genindex-G

Provides access to the BSD socket interface. Includes methods for getting peer address information and protocol information.

```APIDOC
socket Module:

getpeername()
  Returns the address to which the socket is connected.
  Returns: A tuple representing the address.

getprotobyname(name)
  Returns the protocol number for the given protocol name.
  Parameters:
    name: The protocol name (e.g., 'tcp', 'udp').
  Returns: The protocol number.
```

--------------------------------

### Server Socket Example (IPv4)

Source: https://docs.python.org/3/library/ssl

Provides an example of setting up a server socket for secure communication using a custom SSL context. It binds to a local address and port, listens for incoming connections, and accepts them with SSL/TLS encryption enabled.

```python
context = ssl.SSLContext(ssl.PROTOCOL_TLS_SERVER)
context.load_cert_chain('/path/to/certchain.pem', '/path/to/private.key')

with socket.socket(socket.AF_INET, socket.SOCK_STREAM, 0) as sock:
    sock.bind(('127.0.0.1', 8443))
    sock.listen(5)
    with context.wrap_socket(sock, server_side=True) as ssock:
        conn, addr = ssock.accept()
        ...
```

--------------------------------

### Starting IDLE from the Terminal

Source: https://docs.python.org/3/library/idle

This command demonstrates how to start IDLE from a terminal or console. This is useful for capturing error messages that might not be displayed when IDLE is launched through other means.

```bash
python -m idlelib
```

--------------------------------

### Python Site Module - Site-Specific Configuration

Source: https://docs.python.org/3/library/python

Covers the 'site' module, which is responsible for site-specific configuration hooks, including customizing the Python environment and managing startup scripts.

```python
# sitecustomize.py - Example for site-specific configuration

import sys

print('Running sitecustomize.py')
sys.path.append('/path/to/custom/modules')
```

--------------------------------

### unittest.main() Output Examples

Source: https://docs.python.org/3/library/unittest

Shows the expected output when running Python unittest scripts with and without the -v (verbose) option.

```text
...
----------------------------------------------------------------------
Ran 3 tests in 0.000s

OK

```

```text
test_isupper (__main__.TestStringMethods.test_isupper) ... ok
test_split (__main__.TestStringMethods.test_split) ... ok
test_upper (__main__.TestStringMethods.test_upper) ... ok

----------------------------------------------------------------------
Ran 3 tests in 0.001s

OK

```

--------------------------------

### Python os.spawn* Functions

Source: https://docs.python.org/3/genindex-S

Documentation for the various spawn functions in the 'os' module, used for executing new programs. This includes functions like spawnl, spawnle, spawnlp, spawnlpe, spawnv, spawnve, spawnvp, and spawnvpe, detailing their parameters and usage for process creation.

```APIDOC
os.spawnl(path, arg0, arg1, ...)
  - Executes a new program in a new process, replacing the current process image.
  - Parameters:
    - path: The path to the executable file.
    - arg0: The name of the program being executed (conventionally the same as path).
    - arg1, ...: A list of arguments for the new program, terminated by a null pointer.
  - Returns: The process ID of the new process.

os.spawnle(path, arg0, arg1, ..., envp)
  - Similar to spawnl, but also allows specifying the environment for the new process.
  - Parameters:
    - path: The path to the executable file.
    - arg0, arg1, ...: Arguments for the new program.
    - envp: A list of strings representing the environment variables for the new process.
  - Returns: The process ID of the new process.

os.spawnlp(file, arg0, arg1, ...)
  - Similar to spawnl, but searches the PATH for the executable file.
  - Parameters:
    - file: The name of the executable file to search for in the PATH.
    - arg0, arg1, ...: Arguments for the new program.
  - Returns: The process ID of the new process.

os.spawnlpe(file, arg0, arg1, ..., envp)
  - Similar to spawnle, but searches the PATH for the executable file.
  - Parameters:
    - file: The name of the executable file to search for in the PATH.
    - arg0, arg1, ...: Arguments for the new program.
    - envp: Environment variables for the new process.
  - Returns: The process ID of the new process.

os.spawnv(path, args)
  - Similar to spawnl, but takes arguments as a list.
  - Parameters:
    - path: The path to the executable file.
    - args: A list of strings representing the program name and arguments, terminated by a null pointer.
  - Returns: The process ID of the new process.

os.spawnve(path, args, envp)
  - Similar to spawnle, but takes arguments as a list.
  - Parameters:
    - path: The path to the executable file.
    - args: A list of strings representing the program name and arguments.
    - envp: Environment variables for the new process.
  - Returns: The process ID of the new process.

os.spawnvp(file, args)
  - Similar to spawnlp, but takes arguments as a list.
  - Parameters:
    - file: The name of the executable file to search for in the PATH.
    - args: A list of strings representing the program name and arguments.
  - Returns: The process ID of the new process.

os.spawnvpe(file, args, envp)
  - Similar to spawnlpe, but takes arguments as a list.
  - Parameters:
    - file: The name of the executable file to search for in the PATH.
    - args: A list of strings representing the program name and arguments.
    - envp: Environment variables for the new process.
  - Returns: The process ID of the new process.
```

--------------------------------

### Python Sequence C API Functions

Source: https://docs.python.org/3/c-api/stable

Functions for manipulating Python sequences at the C level. These include operations for deleting and getting items/slices, checking for membership, in-place concatenation and repetition, indexing, getting length, converting to lists/tuples, setting items/slices, and getting size.

```APIDOC
PySequence_DelSlice(obj, i, j)
  Deletes a slice from a sequence.

PySequence_Fast(obj, i)
  Checks if a sequence is fast.

PySequence_GetItem(obj, i)
  Retrieves an item from a sequence at a given index.

PySequence_GetSlice(obj, i, j)
  Retrieves a slice from a sequence.

PySequence_In(obj, item)
  Checks if an item is present in a sequence.

PySequence_InPlaceConcat(obj, other)
  Performs in-place concatenation of two sequences.

PySequence_InPlaceRepeat(obj, count)
  Performs in-place repetition of a sequence.

PySequence_Index(obj, item)
  Returns the index of the first occurrence of an item in a sequence.

PySequence_Length(obj)
  Returns the length of a sequence.

PySequence_List(obj)
  Converts a sequence to a list.

PySequence_Repeat(obj, count)
  Repeats a sequence a given number of times.

PySequence_SetItem(obj, i, value)
  Sets an item in a sequence at a given index.

PySequence_SetSlice(obj, i, j, value)
  Sets a slice in a sequence.

PySequence_Size(obj)
  Returns the size of a sequence.

PySequence_Tuple(obj)
  Converts a sequence to a tuple.
```

--------------------------------

### Opening a File for Writing

Source: https://docs.python.org/3/tutorial/inputoutput

Demonstrates how to open a file named 'workfile' in write mode ('w') with UTF-8 encoding.

```python
f = open('workfile', 'w', encoding="utf-8")
```

--------------------------------

### Install Package with Free-threaded Python

Source: https://docs.python.org/3/using/mac

Installs a Python package using the free-threaded interpreter's pip. This is useful when not using a virtual environment.

```python
python3.13t -m pip install <package_name>
```

--------------------------------

### Fetch URL to Temporary File

Source: https://docs.python.org/3/howto/urllib2

Shows how to fetch URL content and save it to a temporary file using shutil.copyfileobj and tempfile.NamedTemporaryFile.

```python
import shutil
import tempfile
import urllib.request

with urllib.request.urlopen('http://python.org/') as response:
    with tempfile.NamedTemporaryFile(delete=False) as tmp_file:
        shutil.copyfileobj(response, tmp_file)

with open(tmp_file.name) as html:
    pass
```

--------------------------------

### Parsing No Arguments

Source: https://docs.python.org/3/extending/extending

Example of using PyArg_ParseTuple to parse a function call with no arguments.

```c
int ok;

ok = PyArg_ParseTuple(args, ""); /* No arguments */
/* Python call: f() */
```

--------------------------------

### Asyncio StreamWriter Start TLS

Source: https://docs.python.org/3/genindex-S

Starts a Transport Layer Security (TLS) handshake for a stream writer. This method is called on a `StreamWriter` object to initiate a secure connection.

```python
import asyncio

async def secure_write():
    # Assuming 'reader' and 'writer' are obtained from asyncio.open_connection
    reader, writer = await asyncio.open_connection('example.com', 443)

    # Start TLS on the writer stream
    await writer.start_tls(ssl=None) # Use default SSL context or provide your own
    print("TLS handshake initiated for StreamWriter")

    # ... write data securely ...

    writer.close()

if __name__ == "__main__":
    asyncio.run(secure_write())
```

--------------------------------

### Python String format() - Using vars()

Source: https://docs.python.org/3/tutorial/inputoutput

Demonstrates using the vars() function with dictionary unpacking in str.format() to display local variables.

```python
table = {k: str(v) for k, v in vars().items()}
message = " ".join([f'{k}: ' + '{' + k +'};' for k in table.keys()])
print(message.format(**table))
```

--------------------------------

### Start Element Handler

Source: https://docs.python.org/3/library/pyexpat

Called for the start of every element, providing the element name and its attributes. Attributes can be a list or dictionary based on `ordered_attributes` setting.

```APIDOC
xmlparser.StartElementHandler(_name_, _attributes_)
  - _name_: String, the element name.
  - _attributes_: List or Dictionary, the element's attributes.
```

--------------------------------

### Python json.tool Example Usage

Source: https://docs.python.org/3/library/json

An example of how to use the json.tool command-line utility to pretty-print a JSON array. It shows the expected input format and the resulting formatted output.

```bash
$ python -m json.tool < infile
[
    {
        "title": "And Now for Something Completely Different",
        "year": 1971
    },
    {
        "title": "Monty Python and the Holy Grail",
        "year": 1975
    }
]
```

--------------------------------

### Using Dynamic Descriptors

Source: https://docs.python.org/3/howto/descriptor

Demonstrates the usage of the 'DirectorySize' descriptor within a 'Directory' class. It shows how different instances of 'Directory' can have dynamic size attributes.

```python
class Directory:

    size = DirectorySize()              # Descriptor instance

    def __init__(self, dirname):
        self.dirname = dirname          # Regular instance attribute
```

--------------------------------

### Python bytes.maketrans() Example

Source: https://docs.python.org/3/library/stdtypes

Demonstrates the use of bytes.maketrans() to create a translation table for character deletion. The example shows how to translate a byte string, removing specified characters.

```python
>>> b'read this short text'.translate(None, b'aeiou')
b'rd ths shrt txt'
```

--------------------------------

### Python List Creation

Source: https://docs.python.org/3/reference/datamodel

Provides examples of creating Python lists, including empty lists and lists with various data types.

```python
# List creation
my_list = [1, 'hello', 3.14]
empty_list = []

# Lists support mutable operations like assignment and deletion
my_list[0] = 10
del my_list[1]
print(my_list) # [10, 3.14]
```

--------------------------------

### Python Initialization Configuration

Source: https://docs.python.org/3/contents

Details on configuring Python initialization, including PyConfig, isolated configuration, and path configuration. It also covers accessing command-line arguments and multi-phase initialization.

```c
#include <Python.h>

// Example of using PyConfig
PyConfig config;
PyConfig_InitIsolatedConfig(&config);
// ... modify config ...
Py_InitializeFromConfig(&config);

// Example of Py_GetArgcArgv
int argc;
char **argv;
Py_GetArgcArgv(&argc, &argv);

```

--------------------------------

### Python unittest setUpClass and tearDownClass Example

Source: https://docs.python.org/3/library/unittest

Demonstrates how to implement class methods for setting up and tearing down resources shared across tests within a class. These methods are called once per class.

```python
import unittest

class Test(unittest.TestCase):
    @classmethod
    def setUpClass(cls):
        cls._connection = createExpensiveConnectionObject()

    @classmethod
    def tearDownClass(cls):
        cls._connection.destroy()
```

--------------------------------

### Basic timeit Command-Line Usage

Source: https://docs.python.org/3/library/timeit

Demonstrates timing simple Python expressions using the timeit command-line interface. Shows how to specify setup statements and the code to be timed.

```bash
$ python"text = 'sample string'; char = 'g'""char in text"
5000000 loops, best of 5: 0.0877 usec per loop
$ python"text = 'sample string'; char = 'g'""text.find(char)"
1000000 loops, best of 5: 0.342 usec per loop
```

--------------------------------

### Python optparse add_option Examples

Source: https://docs.python.org/3/library/optparse

Demonstrates how to use the add_option method in Python's optparse library to define command-line options with short or long strings.

```python
parser.add_option("-f", attr=value, ...)
```

```python
parser.add_option("--foo", attr=value, ...)
```

--------------------------------

### Hashlib BLAKE2

Source: https://docs.python.org/3/library/hashlib

Provides examples for using the BLAKE2 hashing algorithm, including creating hash objects, using different digest sizes, and keyed hashing.

```python
# BLAKE2b example with default parameters
blake2b_hash = hashlib.blake2b(digest_size=64)
blake2b_hash.update(b"Data for BLAKE2b")
print(f"BLAKE2b: {blake2b_hash.hexdigest()}")

# BLAKE2s example with a specific digest size
blake2s_hash = hashlib.blake2s(digest_size=16)
blake2s_hash.update(b"Data for BLAKE2s")
print(f"BLAKE2s (16 bytes): {blake2s_hash.hexdigest()}")

# Keyed BLAKE2b hashing
keyed_blake2b = hashlib.blake2b(key=b'mysecretkey', digest_size=32)
keyed_blake2b.update(b"Secret data")
print(f"Keyed BLAKE2b: {keyed_blake2b.hexdigest()}")
```

--------------------------------

### Build System Configuration (pyproject.toml)

Source: https://docs.python.org/3/extending/newtypes_tutorial

Configures the build system requirements and project metadata for a Python package. It specifies that setuptools is required for building the package and defines the project's name and version.

```toml
[build-system]
requires=["setuptools"]
build-backend="setuptools.build_meta"

[project]
name="custom"
version="1"

```

--------------------------------

### itertools.pairwise Example

Source: https://docs.python.org/3/library/itertools

Shows how to use itertools.pairwise to generate successive overlapping pairs from an iterable. The example demonstrates the output format and provides a conceptual equivalent implementation.

```python
# pairwise('ABCDEFG') → AB BC CD DE EF FG
```

```python
def pairwise(iterable):
    iterator = iter(iterable)
    a = next(iterator, None)

    for b in iterator:
        yield a, b
        a = b
```

--------------------------------

### Python Function Annotation Example

Source: https://docs.python.org/3/glossary

Demonstrates how to use function annotations for type hinting in Python. This example shows a function that expects two integer arguments and returns an integer.

```python
def sum_two_numbers(a: int, b: int) -> int:
   return a + b
```

--------------------------------

### Type Alias Example

Source: https://docs.python.org/3/glossary

Demonstrates how to create a type alias in Python for improved readability of type hints. This example shows aliasing a tuple of integers representing a color.

```python
Color = tuple[int, int, int]

def remove_gray_shades(colors: list[Color]) -> list[Color]:
    pass
```

--------------------------------

### SequenceMatcher Junk Handling Example

Source: https://docs.python.org/3/library/difflib

An example of using SequenceMatcher with a custom junk heuristic, where spaces are ignored during comparison. This highlights how to customize the comparison process.

```python
>>> s = SequenceMatcher(lambda x: x == " ",
...                     "private Thread currentThread;",
...                     "private volatile Thread currentThread;")
```

--------------------------------

### Unittest for Comprehensive Testing

Source: https://docs.python.org/3/tutorial/stdlib

Provides an example of using the unittest module to create a test suite for a function. It defines a test class with methods to check the average function's behavior, including error handling.

```python
import unittest

# Assuming the average function is defined elsewhere or above
def average(values):
    return sum(values) / len(values)

class TestStatisticalFunctions(unittest.TestCase):

    def test_average(self):
        self.assertEqual(average([20, 30, 70]), 40.0)
        self.assertEqual(round(average([1, 5, 7]), 1), 4.3)
        with self.assertRaises(ZeroDivisionError):
            average([])
        with self.assertRaises(TypeError):
            average(20, 30, 70)

if __name__ == '__main__':
    unittest.main()
```

--------------------------------

### Python String format() - Basic Usage

Source: https://docs.python.org/3/tutorial/inputoutput

Demonstrates the fundamental use of the str.format() method with positional arguments to insert values into a string.

```python
print('We are the {} who say "{}"!' .format('knights', 'Ni'))
```