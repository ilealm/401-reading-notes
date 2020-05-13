# Read 04, Classes and Objects, Thinking Recursively and Pytest Fixtures and Coverage

## Classes and Objects
> Objects are an encapsulation of variables and functions into a single entity. 

* Objects get their variables and functions from classes. 
* Classes are essentially a template to create your objects.

_A very basic class would look something like this_
```
class MyClass:
    variable = "blah"

    def function(self):
        print("This is a message inside the class.")
```
_to assign the above class(template) to an object you would do the following:_

```
class MyClass:
    variable = "blah"

    def function(self):
        print("This is a message inside the class.")

myobjectx = MyClass()
```

### Accessing Object Variables

To access the variable inside of the newly created object "myobjectx" you would do the following:

```
myobjectx.variable
```
You can create multiple different objects that are of the same class(have the same variables and functions defined). However, each object contains independent copies of the variables defined in the class. For instance, if we were to define another object with the "MyClass" class and then change the string in the variable above:

```
class MyClass:
    variable = "blah"

    def function(self):
        print("This is a message inside the class.")

myobjectx = MyClass()
myobjecty = MyClass()

myobjecty.variable = "yackity"

# Then print out both values
print(myobjectx.variable)  # blah
print(myobjecty.variable)  # yackity
```
### Accessing Object Functions

```
class MyClass:
    variable = "blah"

    def function(self):
        print("This is a message inside the class.")

myobjectx = MyClass()

myobjectx.function()
```

______
# Thinking Recursively in Python

>If the current problem represents a simple case, solve it. If not, divide it into subproblems and apply the same strategy to them.

Recursive Function means that the function will continue to call itself and repeat its behavior until some condition is met to return a result. 

* All recursive functions share a common structure made up of two parts: 
  1. Base case, and 
  1. Recursive case.

```
houses = ["Eric's house", "Kenny's house", "Kyle's house", "Stan's house"]

# Each function call represents an elf doing his work 
def deliver_presents_recursively(houses):
    # Worker elf doing his work
    if len(houses) == 1:
        house = houses[0]
        print("Delivering presents to", house)

    # Manager elf doing his work
    else:
        mid = len(houses) // 2
        first_half = houses[:mid]
        second_half = houses[mid:]

        # Divides his work among two elves
        deliver_presents_recursively(first_half)
        deliver_presents_recursively(second_half)
```

```
>>> deliver_presents_recursively(houses)
Delivering presents to Eric's house
Delivering presents to Kenny's house
Delivering presents to Kyle's house
Delivering presents to Stan's house
```

## Maintaining State
When dealing with recursive functions, keep in mind that each recursive call has its own execution context, so to maintain state during recursion you have to either:

* Thread the state through each recursive call so that the current state is part of the current call’s execution context
* Keep the state in global scope

_Example: 1 + 2 + 3 ⋅⋅⋅⋅ + 10 using recursion._
```
def sum_recursive(current_number, accumulated_sum):
    # Base case
    # Return the final state
    if current_number == 11:
        return accumulated_sum

    # Recursive case
    # Thread the state through the recursive call
    else:
        return sum_recursive(current_number + 1, accumulated_sum + current_number)
  ```

  ## Recursive Data Structures in Python

A data structure is recursive if it can be deﬁned in terms of a smaller version of itself. 

_A list is an example of a recursive data structure. Other examples include set, tree, dictionary, etc._

___
# Python Testing with pytest: Fixtures and Coverage


## Fixtures

Fixtures are when you'll want to have some objects available to all of your tests. Those objects might contain data you want to share across tests, or they might involve the network or filesystem.

In pytest, you define fixtures using a combination of the pytest.fixture decorator, along with a function definition. _fixtures are used differently from global variables._
```
def reverse_lines(f):
   return [one_line.rstrip()[::-1] + '\n'
           for one_line in f]
```