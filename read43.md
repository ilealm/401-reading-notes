[ HOME ](README.md)
# Read 43 - Pythonnisms

# What Are Dunder Methods?



In Python, special methods are a set of predefined methods you can use to enrich your classes. They are easy to recognize because they start and end with double underscores, for example __init__ or __str__. Pythonistas adopted the term “dunder methods”, a short form of “double under.”

> Dunder methods let you emulate the behavior of built-in types.

Example: __len__ dunder method to your class:

This elegant design is known as the Python data model and lets developers tap into rich language features like sequences, iteration, operator overloading, attribute access, etc.

```
class LenSupport:
    def __len__(self):
        return 42

>>> obj = LenSupport()
>>> len(obj)
42
```

### Examples of Dunder methods

**__str__, __repr__**

It’s common practice in Python to provide a string representation of your object for the consumer of your class (a bit like API documentation.) There are two ways to do this using dunder methods:

- **__repr__**: The “official” string representation of an object. This is how you would make an object of the class. The goal of __repr__ is to be unambiguous.

- **__str__**: The “informal” or nicely printable string representation of an object. This is for the enduser.

```
class Account:
    # ... (see above)

    def __repr__(self):
        return 'Account({!r}, {!r})'.format(self.owner, self.amount)

    def __str__(self):
        return 'Account of {} with starting amount: {}'.format(
            self.owner, self.amount)

            
>>> str(acc)
'Account of bob with starting amount: 10'
```
* **_If you wanted to implement just one of these to-string methods on a Python class, make sure it’s __repr__._**

**__call__**

You can make an object callable like a regular function by adding the __call__ dunder method. 

```
class Account:
    # ... (see above)

    def __call__(self):
        print('Start amount: {}'.format(self.amount))
        print('Transactions: ')
        for transaction in self:
            print(transaction)
        print('\nBalance: {}'.format(self.balance))

>>> acc = Account('bob', 10)
>>> acc.add_transaction(20)
>>> acc.add_transaction(-10)
>>> acc.add_transaction(50)
>>> acc.add_transaction(-20)
>>> acc.add_transaction(30)

>>> acc()
Start amount: 10
Transactions:
20
-10
50
-20
30
Balance: 80        
```

**Context Manager Support and the With Statement: __enter__, __exit__**

A context manager is a simple “protocol” (or interface) that your object needs to follow so it can be used with the with statement. Basically all you need to do is add **__enter__** and **__exit__** methods to an object if you want it to function as a context manager.

```
class Account:
    # ... (see above)

    def __enter__(self):
        print('ENTER WITH: Making backup of transactions for rollback')
        self._copy_transactions = list(self._transactions)
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('EXIT WITH:', end=' ')
        if exc_type:
            self._transactions = self._copy_transactions
            print('Rolling back to previous transactions')
            print('Transaction resulted in {} ({})'.format(
                exc_type.__name__, exc_val))
        else:
            print('Transaction OK')


    def validate_transaction(acc, amount_to_add):
        with acc as a:
            print('Adding {} to account'.format(amount_to_add))
            a.add_transaction(amount_to_add)
            print('New balance would be: {}'.format(a.balance))
            if a.balance < 0:
                raise ValueError('sorry cannot go in debt!')

```

# Sources
[Source Dunder](https://dbader.org/blog/python-dunder-methods)
[Iterators](https://dbader.org/blog/python-iterators)
[Generations](https://dbader.org/blog/python-generators)


___________

# Python Iterators

> Objects that support the __iter__ and __next__ dunder methods automatically work with for-in loops.

### How do for-in loops work in Python?

- Iterators provide a sequence interface to Python objects that’s memory efficient and considered Pythonic. Behold the beauty of the for-in loop!
- To support iteration an object needs to implement the iterator protocol by providing the __iter__ and __next__ dunder methods.
- Class-based iterators are only one way to write iterable objects in Python. Also consider generators and generator expressions.


We first initialize the cursor and prepare it for reading, and then we can fetch data into local variables as needed from it, one element at a time.

Because there’s never more than one element “in flight”, this approach is highly memory-efficient. Our Repeater class provides an infinite sequence of elements and we can iterate over it just fine. Emulating the same with a Python list would be impossible—there’s no way we could create a list with an infinite number of elements in the first place. This makes iterators a very powerful concept.

On more abstract terms, iterators provide a common interface that allows you to process every element of a container while being completely isolated from the container’s internal structure.

Whether you’re dealing with a list of elements, a dictionary, an infinite sequence like the one provided by our Repeater class, or another sequence type—all of that is just an implementation detail. Every single one of these objects can be traversed in the same way by the power of iterators.

And as you’ve seen, there’s nothing special about for-in loops in Python. If you peek behind the curtain, it all comes down to calling the right dunder methods at the right time.

___________

# What Are Python Generators?


- Generator functions are syntactic sugar for writing objects that support the iterator protocol. Generators abstract away much of the boilerplate code needed when writing class-based iterators.
- The yield statement allows you to temporarily suspend execution of a generator function and to pass back values from it.
- Generators start raising StopIteration exceptions after control flow leaves the generator function by any means other than a yield statement.