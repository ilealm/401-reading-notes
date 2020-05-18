# Read 08 - Decorators and List Comprehensions

> Decorators provide a simple syntax for calling higher-order functions.

## First-Class Objects

* In Python, functions are first-class objects.
* This means that functions can be passed around and used as arguments.

```
def say_hello(name):
    return f"Hello {name}"

def be_awesome(name):
    return f"Yo {name}, together we are the awesomest!"

def greet_bob(greeter_func):
    return greeter_func("Bob")

>>> greet_bob(say_hello)
'Hello Bob'

>>> greet_bob(be_awesome)
'Yo Bob, together we are the awesomest!'
```

## Inner Functions

* It’s possible to define functions inside other functions.
* Such functions are called inner functions. 
* The inner functions are not defined until the parent function is called. 
* They are locally scoped to parent(): they only exist inside the parent() function as local variables.

_Example of a function with two inner functions:_

```
def parent():
    print("Printing from the parent() function")

    def first_child():
        print("Printing from the first_child() function")

    def second_child():
        print("Printing from the second_child() function")

    second_child()
    first_child()

>>> parent()
Printing from the parent() function
Printing from the second_child() function
Printing from the first_child() function

```

## Returning Functions From Functions
* Python also allows you to use functions as return values. 

_Example returns one of the inner functions from the outer parent() function:_

```
def parent(num):
    def first_child():
        return "Hi, I am Emma"

    def second_child():
        return "Call me Liam"

    if num == 1:
        return first_child
    else:
        return second_child


>>> first = parent(1)
>>> second = parent(2)

>>> first
<function parent.<locals>.first_child at 0x7f599f1e2e18>

>>> second
<function parent.<locals>.second_child at 0x7f599dad5268>

# You can now use first and second as if they are regular functions, even though the functions they point to #can’t be accessed directly:

>>> first()
'Hi, I am Emma'

>>> second()
'Call me Liam'

```

* Note that you are **returning** first_child **without the parentheses**. 
* Recall that this means that you are returning a **reference to the function** first_child. In contrast first_child() with parentheses refers to the result of evaluating the function.

## Simple Decorators
> Decorators wrap a function, modifying its behavior.

* Do something else before and/or after the function is called.

```
def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

def say_whee():
    print("Whee!")

say_whee = my_decorator(say_whee)

>>> say_whee()
Something is happening before the function is called.
Whee!
Something is happening after the function is called.
```

## Syntactic Sugar!
* Python allows you to use decorators in a simpler way with the @ symbol, sometimes called the “pie” syntax. 
* To have inner function and decorators keeped apart, we’ll name the inner function with the same name as the decorator but with a wrapper_ prefix.

```
def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

@my_decorator
def say_whee():
    print("Whee!")
```

###  Keyword Arguments
* When a **final** formal parameter of the form **name is present, it receives a dictionary containing all keyword arguments except for those corresponding to a formal parameter. 
* This may be combined with a formal parameter of the form name which receives a tuple containing the positional arguments beyond the formal parameter list. 
* *param must occur before **param.

```
def cheeseshop(kind, *arguments, **keywords):
    print("-- Do you have any", kind, "?")
    print("-- I'm sorry, we're all out of", kind)
    for arg in arguments:
        print(arg)
    print("-" * 40)
    for kw in keywords:
        print(kw, ":", keywords[kw])

#It could be called like this:

cheeseshop("Limburger", "It's very runny, sir.",
           "It's really very, VERY runny, sir.",
           shopkeeper="Michael Palin",
           client="John Cleese",
           sketch="Cheese Shop Sketch")
# and of course it would print:

-- Do you have any Limburger ?
-- I'm sorry, we're all out of Limburger
It's very runny, sir.
It's really very, VERY runny, sir.
----------------------------------------
shopkeeper : Michael Palin
client : John Cleese
sketch : Cheese Shop Sketch
```

## Decorating Functions With Arguments
* Wrapped functions don't allow optional arguments. 
* The solution is to use *args and **kwargs in the inner wrapper function. Then it will accept an arbitrary number of positional and keyword arguments. 

```
    def wrapper_do_twice(*args, **kwargs):
        func(*args, **kwargs)
        func(*args, **kwargs)
    return wrapper_do_twice
```

## Introspection 
* Is the ability of an object to know about its own attributes at runtime.
* Decorators should use the @functools.wraps decorator, which will preserve information about the original function.

```
import functools

def do_twice(func):
    @functools.wraps(func)
    def wrapper_do_twice(*args, **kwargs):
        func(*args, **kwargs)
        return func(*args, **kwargs)
    return wrapper_do_twice
```

##  Boilerplate template for building more complex decorators.

```
import functools

def decorator(func):
    @functools.wraps(func)
    def wrapper_decorator(*args, **kwargs):
        # Do something before
        value = func(*args, **kwargs)
        # Do something after
        return value
    return wrapper_decorator
```

## Example with all together

_Timing Functions_

```
import functools
import time

def timer(func):
    """Print the runtime of the decorated function"""
    @functools.wraps(func)
    def wrapper_timer(*args, **kwargs):
        start_time = time.perf_counter()    # 1
        value = func(*args, **kwargs)
        end_time = time.perf_counter()      # 2
        run_time = end_time - start_time    # 3
        print(f"Finished {func.__name__!r} in {run_time:.4f} secs")
        return value
    return wrapper_timer

@timer
def waste_some_time(num_times):
    for _ in range(num_times):
        sum([i**2 for i in range(10000)])


>>> waste_some_time(1)
Finished 'waste_some_time' in 0.0010 secs

>>> waste_some_time(999)
Finished 'waste_some_time' in 0.3260 secs
```

________
# List Comprehensions

> List comprehensions provide a concise way to create lists. 

* It consists of brackets containing an expression followed by a for clause, then
zero or more for or if clauses. 
* The expressions can be anything, meaning you can put in all kinds of objects in lists.
* The list comprehension always returns a result list. 

### Old way to create a list:
```
new_list = []
for i in old_list:
    if filter(i):
        new_list.append(expressions(i))
```

### New way to create a list:
> [ expression for item in list if conditional ]
>
> [*transform*    *iteration*         *filter*     ]
```
new_list = [expression(i) for i in old_list if filter(i)]

```

* The list comprehension starts with a '[' and ']', to help you remember that the
result is going to be a list.
* If filter(i) : Apply a filter with an If-statement.
* expression(i) : Expression is based on the variable used for each element in the old list.

```
[ expression for item in list if conditional ]
```

means
```
for item in list:
    if conditional:
        expression
``  