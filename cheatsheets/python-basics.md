# Python Basics

## What is Python?
Python is high level , intrepreted , general purpose programming language.

``` bash
>>> print("Hello Khushi")
Hello Khushi
```

### comments in python

```bash
# This is single line comment.
```

### Docstrings
- used to document modules, classes and functions.

```bash
""" Discription of module """
```

### Keywords
- reserved word with special meaning.
- examples: if,else,for, while, break, continue etc.

### Identifiers
- names given to variables, functions,etc.

### Variables

```bash
    
>>> name="Khushi"    #variable assignment
>>> x=20

>>> x+=5          #variable increment
>>> x
25

>>> a,b,c=10,20,30       # multiple assignment
>>> x=y=z=0    

>>> a,b=b,a          # swapping variables
>>> x=10
>>> x="Python"
>>> PI=3.14
>>> print(id(x))         # object identity
137011433540560
>>> print(type(x))         # data type
<class 'str'>

>>> del x            # delete variable
>>> x
```


### Data types

## Python Data Types

| Category | Data Type | Example | Description |
|---|---|---|---|
| Numeric | `int` | `age = 21` | Stores whole numbers without decimal points. |
| Numeric | `float` | `price = 99.50` | Stores numbers with decimal points. |
| Numeric | `complex` | `num = 3 + 4j` | Stores complex numbers with real and imaginary parts. |
| Text | `str` | `name = "Khushi"` | Stores a sequence of characters (text). |
| Boolean | `bool` | `is_active = True` | Stores either `True` or `False`. |
| Sequence | `list` | `fruits = ["apple", "banana", "mango"]` | Stores multiple items in an ordered, changeable collection. |
| Sequence | `tuple` | `colors = ("red", "green", "blue")` | Stores multiple items in an ordered, unchangeable collection. |
| Sequence | `range` | `numbers = range(1, 5)` | Generates a sequence of numbers. |
| Mapping | `dict` | `student = {"name": "Khushi", "age": 21}` | Stores data in key-value pairs. |
| Set | `set` | `numbers = {1, 2, 3, 4}` | Stores unique items in an unordered collection. |
| Set | `frozenset` | `numbers = frozenset({1, 2, 3})` | Stores unique items in an unchangeable collection. |
| Binary | `bytes` | `data = b"Hello"` | Stores immutable binary data. |
| Binary | `bytearray` | `data = bytearray(5)` | Stores mutable binary data. |
| Binary | `memoryview` | `data = memoryview(bytes(5))` | Provides access to binary data without copying it. |
| None | `NoneType` | `result = None` | Represents the absence of a value. |