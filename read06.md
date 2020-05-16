# Read 06, Random Module and Dependency Injection

#### Randint
If we wanted a random integer, we can use the randint function, which accepts two parameters: a lowest and a highest number.

```
import random
print random.randint(0, 5)
```
* If you want a larger number, you can multiply it. 
_For example, a random number between 0 and 100:_

```
import random
random.random() * 100
```

#### Choice
Generate a random value from the sequence sequence.
```
random.choice( ['red', 'black', 'green'] ).
```

The choice function can often be used for choosing a random element from a list.
```
import random
myList = [2, 109, False, 10, "Lorem", 482, "Ipsum"]
random.choice(myList)
```

#### Shuffle
The shuffle function, shuffles the elements in list in place, so they are in a
random order.
```
random.shuffle(list)
```

_Example taken from this post on Stackoverflow_
```
from random import shuffle
x = [[i] for i in range(10)]
shuffle(x)
Output:
# print x  gives  [[9], [2], [7], [0], [4], [5], [3], [1], [8], [6]]
# of course your results will vary
```

#### Randrange
Generate a randomly selected element from range(start, stop, step)
```
import random
for i in range(3):
    print random.randrange(0, 101, 5)

```


____
# Dependency Injection (DI)

>ependency injection is a technique whereby one object (or static method) supplies the dependencies of another object. A dependency is an object that can be used (a service).

1. When class A uses some functionality of class B, then its said that class A has a dependency of class B.

1. In Java, before we can use methods of other classes, we first need to create the object of that class (i.e. class A needs to create an instance of class B).

> Transferring the task of creating the object to someone else and directly using the dependency is called dependency injection.

* Dependencies can be injected at runtime rather than at compile time.

### There are basically three types of dependency injection:
1. Constructor injection: the dependencies are provided through a class constructor.
1. Setter injection: the client exposes a setter method that the injector uses to inject the dependency.
1. Interface injection: the dependency provides an injector method that will inject the dependency into any client passed to it. Clients must implement an interface that exposes a setter method that accepts the dependency.

### Inversion of control —the concept behind DI
* This states that a class should not configure its dependencies statically but should be configured by some other class from outside.
