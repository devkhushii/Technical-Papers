#  Strings 


## What is a String?

- A string is a sequence of characters enclosed within single quotes (' '), double quotes (" ") or triple quotes (''' ''').
- Strings are used to store text.
- Strings are immutable, which means their characters cannot be changed after creation.


## 1. Creating a String


```python
>>> text = "Python"
>>> text
'Python'

>>> message = 'Hello World'
>>> message
'Hello World'

>>> text = """This is
... a multiline string"""
>>> text
'This is\n a multiline string'
```

## 2. Accessing Characters


```python
>>> text = "Python"
>>> text[0]
'P'
>>> text[2]
't'
>>> text[-1]
'n'
>>> text[-2]
'o'
```

## 3. String Slicing

**Syntax:** `string[start:end:step]`

```python
>>> text = "Python"
>>> text[0:3]
'Pyt'

>>> text[2:]
'thon'

>>> text[:4]
'Pyth'

>>> text[::2]
'Pto'

>>> text[::-1]       # Reverse string
'nohtyP'
```

## 4. Updating a String

Strings are immutable, which means we cannot directly modify individual characters.

```python
>>> text = "Python"
>>> text[0] = 'J'
TypeError: 'str' object does not support item assignment
```

**Using `replace()`:**

```python
>>> text = "Python"
>>> text = text.replace("P", "J")
>>> text
'Jython'
```

## 5. String Operators

```python
>>> "Hello" + " World"    # Concatenation
'Hello World'

>>> "Hi " * 3           # Repetition
'Hi Hi Hi '

>>> "Py" in "Python"           #  Checks whether substring exists
True

>>> "Java" not in "Python"          # Checks whether substring does not exist
True
```

## 6. Case Conversion Methods

```python
>>> text = "hello world"

>>> text.upper()             # Convert to uppercase
'HELLO WORLD'

>>> text.lower()             # Convert to lowercase
'hello world'

>>> text.capitalize()        # Capitalize first character
'Hello world'

>>> text.title()             # Capitalize each word
'Hello World'

>>> "HeLLo".swapcase()       # Swap uppercase and lowercase
'hEllO'

>>> "HELLO".casefold()       # Convert for case-insensitive comparison
'hello'
```

## 7. Searching and Counting

```python
>>> text = "hello hello"

>>> text.find("o")           # First occurrence index
4

>>> text.rfind("o")          # Last occurrence index
10

>>> text.index("w")          # Find index
ValueError: substring not found

>>> text.rindex("hello")     # Last occurrence index
6

>>> text.count("l")          # Count occurrences
4

>>> text.startswith("hello")
True

>>> text.endswith("hello")
True
```

**Difference between `find()` and `index()`:**
- `find()` returns `-1` if the substring is not found.
- `index()` raises `ValueError` if the substring is not found.

Similarly:
- `rfind()` searches from the right and returns `-1` if not found.
- `rindex()` searches from the right and raises `ValueError` if not found.

## 8. Removing Spaces and Replacing Characters

```python
>>> text = "  Hello World  "

>>> text.strip()             # Remove spaces from both ends
'Hello World'

>>> text.lstrip()            # Remove spaces from left
'Hello World  '

>>> text.rstrip()            # Remove spaces from right
'  Hello World'

>>> "Hello".replace("H", "Y")
'Yello'

>>> "Python".removeprefix("Py")
'thon'

>>> "Python".removesuffix("on")
'Pyth'
```

## 9. Splitting and Joining

**split():** Converts a string into a list.

```python
>>> text = "Python Java C++"
>>> text.split()
['Python', 'Java', 'C++']

>>> text = "apple,banana,mango"
>>> text.split(",")
['apple', 'banana', 'mango']
```

**rsplit():** Splits from the right side.

```python
>>> "a-b-c".rsplit("-", 1)
['a-b', 'c']
```

**splitlines():** Splits a string at line breaks.

```python
>>> "Hello\nWorld".splitlines()
['Hello', 'World']
```

**join():** Joins elements of an iterable into a string.

```python
>>> words = ["Python", "Java", "C++"]
>>> " ".join(words)
'Python Java C++'

>>> "-".join(words)
'Python-Java-C++'
```

## 10. Checking String Characters

These methods return `True` or `False`.

```python
>>> "Hello".isalpha()        # Only alphabets
True

>>> "123".isdigit()          # Only digit characters
True

>>> "123".isnumeric()        # Numeric characters
True

>>> "123".isdecimal()        # Only decimal digits
True

>>> "Hello123".isalnum()     # Alphabets and numbers
True

>>> "   ".isspace()          # Only whitespace
True

>>> "hello".islower()        # Check lowercase
True

>>> "HELLO".isupper()        # Check uppercase
True

>>> "Hello World".istitle()  # Check title case
True

>>> "Hello".isascii()        # Check ASCII characters
True

>>> "hello_world".isidentifier()  # Valid Python identifier
True

>>> "Hello\nWorld".isprintable()  # Check printable characters
False
```

**Difference between `isdecimal()`, `isdigit()` and `isnumeric()`:**

- `isdecimal()` checks decimal digits.
- `isdigit()` also accepts certain special digit characters, such as superscript digits.
- `isnumeric()` accepts an even wider range of numeric characters, including fractions.

## 11. String Alignment and Formatting

```python
>>> "Hi".center(6, "*")      # Center alignment
'**Hi**'

>>> "Hi".ljust(5, "-")       # Left alignment
'Hi---'

>>> "Hi".rjust(5, "-")       # Right alignment
'---Hi'

>>> "42".zfill(5)            # Add zeros to the left
'00042'
```

**String Formatting:**

```python
>>> name = "John"
>>> age = 22

>>> f"My name is {name} and I am {age} years old."
'My name is John and I am 22 years old.'

>>> "My name is {} and I am {} years old.".format(name, age)
'My name is John and I am 22 years old.'
```

**format_map():**

```python
>>> data = {"name": "John", "age": 22}
>>> "My name is {name} and I am {age}".format_map(data)
'My name is John and I am 22'
```

## 12. Partitioning Methods

`partition()` and `rpartition()` divide a string into three parts:
- Part before the separator.
- Separator itself.
- Part after the separator.

**partition():** Splits at the first occurrence.

```python
>>> text = "Python is easy"
>>> text.partition("is")
('Python ', 'is', ' easy')
```

**rpartition():** Splits at the last occurrence.

```python
>>> text = "Python is easy and Python is popular"
>>> text.rpartition("is")
('Python is easy and Python ', 'is', ' popular')
```

## 13. Other Useful String Methods

**expandtabs():** Replaces tab characters with spaces.

```python
>>> "Hello\tWorld".expandtabs(4)
'Hello   World'
```

**encode():** Converts a string into bytes.

```python
>>> text = "Hello"
>>> text.encode()
b'Hello'
```

**maketrans() and translate():** Used to replace multiple characters using a translation table.

```python
>>> table = str.maketrans("ae", "12")
>>> "apple".translate(table)
'1ppl2'
```

## 14. Useful Built-in Functions

```python
>>> text = "Python"

>>> len(text)                 # Number of characters
6

>>> min(text)                 # Smallest Unicode character
'P'

>>> max(text)                 # Largest Unicode character
'y'

>>> sorted(text)              # Return sorted list of characters
['P', 'h', 'n', 'o', 't', 'y']

>>> ord('A')                  # Unicode value of character
65

>>> chr(65)                   # Character from Unicode value
'A'

>>> str(123)                  # Convert into string
'123'

>>> list("abc")               # Convert into list
['a', 'b', 'c']

>>> tuple("abc")              # Convert into tuple
('a', 'b', 'c')

>>> set("hello")              # Return unique characters
{'h', 'e', 'l', 'o'}

>>> any("abc")                # At least one element is truthy
True

>>> all("abc")                # All elements are truthy
True

>>> list(reversed(text))      # Reverse iterator as list
['n', 'o', 'h', 't', 'y', 'P']
```

## 15. Looping Through a String

```python
>>> text = "Python"

>>> for char in text:
...     print(char)
P
y
t
h
o
n
```

**Using `enumerate()`:**

```python
>>> for index, char in enumerate(text):
...     print(index, char)
0 P
1 y
2 t
3 h
4 o
5 n
```

## 16. String Immutability

Strings cannot be modified after creation. String methods return a new string.

```python
>>> text = "hello"
>>> text.upper()
'HELLO'

>>> text
'hello'

>>> text = text.upper()
>>> text
'HELLO'
```

## 17. Time Complexity

Let `n` be the length of the string and `m` be the length of the substring.

| Operation | Complexity |
|---|---|
| Access by index | O(1) |
| Slicing | O(k), where k is slice length |
| Concatenation | O(n + m) |
| Searching for a character | O(n) |
| Counting a character | O(n) |
| Finding a substring | O(n × m) worst case |
| String comparison | O(n) |
| Iteration | O(n) |
| Reversing | O(n) |
| Sorting | O(n log n) |
| Membership check | O(n × m) worst case |
