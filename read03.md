# Read 03 -  FileIO & Exceptions

## Reading and Writing Files in Python

* Files on most modern file systems are composed of three main parts:
  1. Header: metadata about the contents of the file (file name, size, type, and so on)
  1. Data: contents of the file as written by the creator or editor
  1. End of file (EOF): special character that indicates the end of the file

### File Paths

> When you access a file on an operating system, a file path is required. 

* It’s broken up into three major parts:
  1. Folder Path: the file folder location on the file system where subsequent folders are separated by a forward slash / (Unix) or backslash \ (Windows)
  1. File Name: the actual name of the file
  1. Extension: the end of the file path pre-pended with a period (.) used to indicate the file type

### Line Endings
> One problem often encountered when working with file data is the representation of a new line or line ending.

* ASA standard states that line endings should use the sequence of the Carriage Return (CR or \r) and the Line Feed (LF or \n) characters (CR+LF or \r\n). The ISO standard however allowed for either the CR+LF characters or just the LF character.
* Windows uses the CR+LF characters to indicate a new line, while Unix and the newer Mac versions use just the LF character. This can cause some complications when you’re processing files on an operating system that is different than the file’s source.

### Character Encodings
* Encoding is a translation from byte data to human readable characters. 
* This is typically done by assigning a numerical value to represent a character. 
* The two most common encodings are the ASCII and UNICODE Formats. ASCII can only store 128 characters, while Unicode can contain up to 1,114,112 characters.
* ASCII is actually a subset of Unicode (UTF-8), meaning that ASCII and Unicode share the same numerical to character values. 
* **It’s important to note that parsing a file with the incorrect character encoding can lead to failures or misrepresentation of the character.** For example, if a file was created using the UTF-8 encoding, and you try to parse it using the ASCII encoding, if there is a character that is outside of those 128 values, then an error will be thrown.

## Opening and Closing a File in Python

> Open: This is done by invoking the open() built-in function. open() has a single required argument that is the path to the file. open() has a single return, the file object:

```
file = open('dog_breeds.txt')
```
> Close: When you’re manipulating a file, there are two ways that you can use to ensure that a file is closed properly, even when encountering an error. The first way to close a file is to use the try-finally block:

```
reader = open('dog_breeds.txt')
try:
    # Further file processing goes here
finally:
    reader.close()
```

The second way to close a file is to use the with statement:

```
with open('dog_breeds.txt') as reader:
    # Further file processing goes here
```

## Reading and Writing Opened Files

There are multiple methods that can be called on a file object to help you out:

* .read(size=-1)	
  * This reads from the file based on the number of size bytes. If no argument is passed or None or -1 is passed, then the entire file is read.
* .readline(size=-1)	
  * This reads at most size number of characters from the line. This continues to the end of the line and then wraps back around. If no argument is passed or None or -1 is passed, then the entire line (or rest of the line) is read.
* .readlines()	
  * This reads the remaining lines from the file object and returns them as a list.

  _Example of how to open and read the entire file using .read():_

 ```
>>> with open('dog_breeds.txt', 'r') as reader:
>>>     # Read & print the first 5 characters of the line 5 times
>>>     print(reader.readline(5))
>>>     # Notice that line is greater than the 5 chars and continues
>>>     # down the line, reading 5 chars each time until the end of the
>>>     # line and then "wraps" around
>>>     print(reader.readline(5))
>>>     print(reader.readline(5))
>>>     print(reader.readline(5))
>>>     print(reader.readline(5))
```

_Here’s an example of how to read the entire file as a list using the Python .readlines() method:_

```
>>> f = open('dog_breeds.txt')
>>> f.readlines()  # Returns a list object
```

_The above example can also be done by using list() to create a list out of the file object:_
```
>>> f = open('dog_breeds.txt')
>>> list(f)
```

##  Writing files
* .write(string)	
  * This writes the string to the file.
* .writelines(seq)	
  * This writes the sequence to the file. No line endings are appended to each sequence item. It’s up to you to add the appropriate line ending(s).

```
with open('dog_breeds.txt', 'r') as reader:
    # Note: readlines doesn't trim the line endings
    dog_breeds = reader.readlines()

with open('dog_breeds_reversed.txt', 'w') as writer:
    # Alternatively you could use
    # writer.writelines(reversed(dog_breeds))

    # Write the dog breeds to the file in reversed order
    for breed in reversed(dog_breeds):
        writer.write(breed)
```

### Appending to a File
* Sometimes, you may want to append to a file or start writing at the end of an already populated file. This is easily done by using the 'a' character for the mode argument:

```
with open('dog_breeds.txt', 'a') as a_writer:
    a_writer.write('\nBeagle')
```

______
# Python Exceptions: An Introduction

* A Python program terminates as soon as it encounters an error. 
* In Python, an error can be a syntax error or an exception.

### Raising an Exception
* We can use raise to throw an exception if a condition occurs. 

```
x = 10
if x > 5:
    raise Exception('x should not exceed 5. The value of x was: {}'.format(x))
```
### The AssertionError Exception

* In this example, throwing an AssertionError exception is the last thing that the program will do. The program will come to halt and will not continue.

```
import sys
assert ('linux' in sys.platform), "This code runs on Linux only."
```
### The try and except Block: Handling Exceptions

*  Python executes code following the try statement as a “normal” part of the program. The code that follows the except statement is the program’s response to any exceptions in the preceding try clause.
```
def linux_interaction():
    assert ('linux' in sys.platform), "Function can only run on Linux systems."
    print('Doing something.')

try:
    linux_interaction()
except:
    pass
```
### The else Clause
* In Python, using the else statement, you can instruct a program to execute a certain block of code only in the absence of exceptions.

```
try:
    linux_interaction()
except AssertionError as error:
    print(error)
else:
    try:
        with open('file.log') as file:
            read_data = file.read()
    except FileNotFoundError as fnf_error:
        print(fnf_error)
```

### Cleaning Up After Using finally
* Imagine that you always had to implement some sort of action to clean up after executing your code. Python enables you to do so using the finally clause.

```
try:
    linux_interaction()
except AssertionError as error:
    print(error)
else:
    try:
        with open('file.log') as file:
            read_data = file.read()
    except FileNotFoundError as fnf_error:
        print(fnf_error)
finally:
    print('Cleaning up, irrespective of any exceptions.')
```