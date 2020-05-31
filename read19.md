[ HOME ](README.md)
# Read - Automation
 > Regular expressions are used to identify whether a pattern exists in a given sequence of characters (string) or not. 

 - In Python, regular expressions are supported by the re module. 
 ```
 import re
 ```

 ### Basic Patterns: Ordinary Characters

 - Ordinary characters are the simplest regular expressions. They match themselves exactly and do not have a special meaning in their regular expression syntax.
 - The match() function returns a match object if the text matches the pattern. Otherwise it returns None.
 
 ```
pattern = r"Cookie"
sequence = "Cookie"

if re.match(pattern, sequence):
  print("Match!")
else: print("Not a match!")
```

- Tthe r at the start of the pattern Cookie? This is called a raw string literal. It changes how the string literal is interpreted. Such literals are stored as they appear. For example, \ is just a backslash when prefixed with a r rather than being interpreted as an escape sequence.

### Wild Card Characters: Special Characters
- Special characters are characters which do not match themselves as seen but actually have a special meaning when used in a regular expression.

_The most widely used special characters are:_
- . - A period. Matches any single character except newline character.
```
re.search(r'Co.k.e', 'Cookie').group()
'Cookie'
```

- \w - Lowercase w. Matches any single letter, digit or underscore.
- \W - Uppercase w. Matches any character not part of \w (lowercase w).
- \s - Lowercase s. Matches a single whitespace character like: space, newline, tab, return.
- \S - Uppercase s. Matches any character not part of \s (lowercase s).
- \t - Lowercase t. Matches tab.
- \n - Lowercase n. Matches newline.
- \r - Lowercase r. Matches return.
- \d - Lowercase d. Matches decimal digit 0-9.
- ^ - Caret. Matches a pattern at the start of the string.
- $ - Matches a pattern at the end of string.
- [abc] - Matches a or b or c.
- [a-zA-Z0-9] - Matches any letter from (a to z) or (A to Z) or (0 to 9)
- \A - Uppercase a. Matches only at the start of the string. Works across multiple lines as well.
- \b - Lowercase b. Matches only the beginning or end of the word.
- \ - Backslash. If the character following the backslash is a recognized escape character, then the special meaning of the term is taken.

### Repetitions
- + - Checks for one or more characters to its left.
- * - Checks for zero or more characters to its left.
- ? - Checks for exactly zero or one character to its left.
- {x} - Repeat exactly x number of times.
- {x,} - Repeat at least x times or more.
- {x, y} - Repeat at least x times but no more than y times.
- The + and * qualifiers are said **to be greedy.**

### Groups and Grouping using Regular Expressions

- It allows you to pick up parts of the matching text.
- Parts of a regular expression pattern bounded by parenthesis() are called groups. The parenthesis does not change what the expression matches, but rather forms groups within the matched sequence. 

```
email_address = 'Please contact us at: support@datacamp.com'
match = re.search(r'([\w\.-]+)@([\w\.-]+)', ____________)
if _____:
  print(match.group()) # The whole matched text
  print(match.group(1)) # The username (group 1)
  print(match.group(2)) # The host (group 2)
```

## re Python Library

**search(pattern, string, flags=0)**

With this function, you scan through the given string/sequence looking for the first location where the regular expression produces a match. It returns a corresponding match object if found, else returns None if no position in the string matches the pattern. Note that None is different from finding a zero-length match at some point in the string.
```
match(pattern, string, flags=0)
```

 **search() versus match()**

 - The match() function checks for a match only at the beginning of the string (by default).
 - Search() function checks for a match anywhere in the string.
 - findall(pattern, string, flags=0) Finds all the possible matches in the entire sequence and returns them as a list of strings. Each returned string represents one match.
 - substitute function. It returns the string obtained by replacing or substituting the leftmost non-overlapping occurrences of pattern in string by the replacement repl
 - compile(pattern, flags=0) Compiles a regular expression pattern into a regular expression object. 

 #### Tip
 An expression's behavior can be modified by specifying a flags value. You can add flag as an extra argument to the various functions that you have seen in this tutorial. Some of the flags used are: IGNORECASE, DOTALL, MULTILINE, VERBOSE, etc.

 ___
 ## Source

 [Source](https://www.datacamp.com/community/tutorials/python-regular-expression-tutorial)