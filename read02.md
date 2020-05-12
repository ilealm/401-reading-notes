# Read 02, Testing, Modules and Recursion

* Python modules and Python packages, two mechanisms that facilitate modular programming:
  * Simplicity
  * Maintainability
  * Reusability
  * Scoping
* Python Modules: There are actually three different ways to define a module in Python:
  1. A module can be written in Python itself.
  1. A module can be written in C and loaded dynamically at run-time, like the re (regular expression) module.
  1. A built-in module is intrinsically contained in the interpreter
* A module’s contents are accessed the same way in all three cases: **with the import statement.**

> To build modules written in Python,  you need to do is create a file that contains legitimate Python code and then give the file a name with a .py extension.

## The Module Search Path

```
import mod
```

When the interpreter executes the above import statement, it searches for mod.py in a list of directories assembled from the following sources:

The directory from which the input script was run or the current directory if the interpreter is being run interactively
The list of directories contained in the PYTHONPATH environment variable, if it is set. (The format for PYTHONPATH is OS-dependent but should mimic the PATH environment variable.)
An installation-dependent list of directories configured at the time Python is installed
The resulting search path is accessible in the Python variable sys.path, which is obtained from a module named sys:

The resulting search path is accessible in the Python variable sys.path, which is obtained from a module named sys:

```
>>> import sys
>>> sys.path
```

## The import Statement

```
import <module_name>

import <module_name>[, <module_name> ...]

from <module_name> import <name(s)>

# It is even possible to indiscriminately import everything from a module at one
from <module_name> import *

# It is also possible to import individual objects but enter them into the local symbol table with alternate names:
from <module_name> import <name> as <alt_name>

import <module_name> as <alt_name>
```

  Note that this does not make the module contents directly accessible to the caller. Each module has its own private symbol table, which serves as the global symbol table for all objects defined in the module.

  From the caller, objects in the module are only accessible when prefixed with <module_name> via dot notation

  ```
  >>> mod.s
'If Comrade Napoleon says it, it must be right.'
>>> mod.foo('quux')
arg = quux
```

```
>>> from mod import s, foo
```

* Because this form of import places the object names directly into the caller’s symbol table, any objects that already exist with the same name will be overwritten.

 ### Statement with an except ImportError clause can be used to guard against unsuccessful import attempts

 ```
 >>> try:
...     # Non-existent module
...     import baz
... except ImportError:
...     print('Module not found')
...

Module not found
```

## The dir() Function

> The built-in function dir() returns a list of defined names in a namespace. 

## Executing a Module as a Script
Any .py file that contains a module is essentially also a Python script, and there isn’t any reason it can’t be executed like one.

```
C:\Users\john\Documents>python mod.py
```

## Unit testing
Modules are often designed with the capability to run as a standalone script for purposes of testing the functionality that is contained within the module. This is referred to as unit testing.

```
def fact(n):
    return 1 if n == 1 else n * fact(n-1)

if (__name__ == '__main__'):
    import sys
    if len(sys.argv) > 1:
        print(fact(int(sys.argv[1])))
```

The file can be treated as a module, and the fact() function imported:
```
>>> from fact import fact
>>> fact(6)
```

But it can also be run as a standalone by passing an integer argument on the command-line for testing:

```
C:\Users\john\Documents>python fact.py 6
```

# Python Packages
> Packages allow for a hierarchical structuring of the module namespace using dot notation. In the same way that modules help avoid collisions between global variable names, packages help avoid collisions between module names.

### Package Initialization
If a file named __init__.py is present in a package directory, it is invoked when the package or a module in the package is imported. This can be used for execution of package initialization code, such as initialization of package-level data.

### Importing * From a Package
 Python follows this convention: if the __init__.py file in the package directory contains a list named __all__, it is taken to be a list of modules that should be imported when the statement from <package_name> import * is encountered.

 > In summary, __all__ is used by both packages and modules to control what is imported when import * is specified. But the default behavior differs:

* For a package, when __all__ is not defined, import * does not import anything.
* For a module, when __all__ is not defined, import * imports everything (except—you guessed it—names starting with an underscore).

### Subpackage

* A module in one subpackage can reference objects in a sibling subpackage (in the event that the sibling contains some functionality that you need)

___________

# Pytest

> The pytest framework makes it easy to write small tests, yet scales to support complex functional testing for applications and libraries.

```
# content of test_sample.py
def inc(x):
    return x + 1


def test_answer():
    assert inc(3) == 5
```

To execute it:
```
$ pytest
=========================== test session starts ============================
platform linux -- Python 3.x.y, pytest-5.x.y, py-1.x.y, pluggy-0.x.y
cachedir: $PYTHON_PREFIX/.pytest_cache
rootdir: $REGENDOC_TMPDIR
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

### Assertions in PyTest

Assertions are checks that return either True or False status. In pytest, if an assertion fails in a test method, then that method execution is stopped there. The remaining code in that test method is not executed, and pytest will continue with the next test method.

#### How pytest identifies the test files and test methods
By default pytest only identifies the file names starting with test_ or ending with _test as the test files. We can explicitly mention other filenames though (explained later). Pytest requires the test method names to start with "test." 

#### Run multiple tests from a specific file and multiple files

 To run all the tests from all the files in the folder and subfolders we need to just run the pytest command.

```
py.test
```

This will run all the filenames starting with test_ and the filenames ending with _test in that folder and subfolders under that folder.

#### Pytest fixtures
Fixtures are used when we want to run some code before every test method. So instead of repeating the same code in every test we define fixtures. Usually, fixtures are used to initialize database connections, pass the base , etc


```
@pytest.fixture
```

#### Parameterized tests
The purpose of parameterizing a test is to run a test against multiple sets of arguments. We can do this by @pytest.mark.parametrize.

```
import pytest
@pytest.mark.parametrize("input1, input2, output",[(5,5,10),(3,5,12)])
def test_add(input1, input2, output):
	assert input1+input2 == output,"failed"
```

#### Xfail / Skip tests
There will be some situations where we don't want to execute a test, or a test case is not relevant for a particular time. In those situations, we have the option to xfail the test or skip the tests

The xfailed test will be executed, but it will not be counted as part failed or passed tests. There will be no traceback displayed if that test fails. We can xfail tests using

@pytest.mark.xfail.

Skipping a test means that the test will not be executed. We can skip tests using

@pytest.mark.skip.

```
import pytest
@pytest.mark.skip
def test_add_1():
	assert 100+200 == 400,"failed"

@pytest.mark.skip
def test_add_2():
	assert 100+200 == 300,"failed"

@pytest.mark.xfail
def test_add_3():
	assert 15+13 == 28,"failed"

@pytest.mark.xfail
def test_add_4():
	assert 15+13 == 100,"failed"

def test_add_5():
	assert 3+2 == 5,"failed"

def test_add_6():
	assert 3+2 == 6,"failed"
```

____

# Recursion
>The process in which a function calls itself directly or indirectly is called recursion and the corresponding function is called as recursive function. 

```
int fact(int n)
{
    if (n < = 1) // base case
        return 1;
    else    
        return n*fact(n-1);    
}
```

### What is the difference between direct and indirect recursion?
A function fun is called direct recursive if it calls the same function fun. A function fun is called indirect recursive if it calls another function say fun_new and fun_new calls fun directly or indirectly. 

```
/ An example of direct recursion
void directRecFun()
{
    // Some code....

    directRecFun();

    // Some code...
}

// An example of indirect recursion
void indirectRecFun1()
{
    // Some code...

    indirectRecFun2();

    // Some code...
}
void indirectRecFun2()
{
    // Some code...

    indirectRecFun1();

    // Some code...
}
```
#### What is difference between tailed and non-tailed recursion?
A recursive function is tail recursive when recursive call is the last thing executed by the function. 

#### How memory is allocated to different function calls in recursion?
When any function is called from main(), the memory is allocated to it on the stack. A recursive function calls itself, the memory for a called function is allocated on top of memory allocated to calling function and different copy of local variables is created for each function call. When the base case is reached, the function returns its value to the function by whom it is called and memory is de-allocated and the process continues.