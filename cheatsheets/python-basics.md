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

>>> isinstance(3.14,float)      #Check for a specific type
True
>>> issubclass(int,object)          #checks if a class is a subclass
True

```


### Data types

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


### Type Conversion (Casting)

```bash
>>> int("10") # explicit conversion
10
>>> float("3")
3.0
>>> str(45)
'45'
>>> bool(4)
True
>>> bool(0)
False
>>> complex(2)
(2+0j)
>>> x=5+2.5 #implicit conversion
```

### Operators

## Python Operators

| Category | Operator | Example | Description |
|---|---|---|---|
| Arithmetic | `+` | `5 + 2 = 7` | Adds two values. |
| Arithmetic | `-` | `5 - 2 = 3` | Subtracts one value from another. |
| Arithmetic | `*` | `5 * 2 = 10` | Multiplies two values. |
| Arithmetic | `/` | `5 / 2 = 2.5` | Divides and returns a float. |
| Arithmetic | `//` | `5 // 2 = 2` | Performs floor division. |
| Arithmetic | `%` | `5 % 2 = 1` | Returns the remainder. |
| Arithmetic | `**` | `5 ** 2 = 25` | Performs exponentiation (power). |
| Assignment | `=` | `x = 10` | Assigns a value to a variable. |
| Assignment | `+=` | `x += 5` | Adds and assigns the result. |
| Assignment | `-=` | `x -= 5` | Subtracts and assigns the result. |
| Assignment | `*=` | `x *= 5` | Multiplies and assigns the result. |
| Assignment | `/=` | `x /= 5` | Divides and assigns the result. |
| Assignment | `//=` | `x //= 5` | Performs floor division and assigns the result. |
| Assignment | `%=` | `x %= 5` | Finds the remainder and assigns the result. |
| Assignment | `**=` | `x **= 2` | Raises to a power and assigns the result. |
| Assignment | `&=` | `x &= 5` | Performs bitwise AND and assigns the result. |
| Assignment | `\|=` | `x \|= 5` | Performs bitwise OR and assigns the result. |
| Assignment | `^=` | `x ^= 5` | Performs bitwise XOR and assigns the result. |
| Assignment | `>>=` | `x >>= 1` | Right-shifts and assigns the result. |
| Assignment | `<<=` | `x <<= 1` | Left-shifts and assigns the result. |
| Comparison | `==` | `5 == 5` | Checks if two values are equal. |
| Comparison | `!=` | `5 != 2` | Checks if two values are not equal. |
| Comparison | `>` | `5 > 2` | Checks if the left value is greater. |
| Comparison | `<` | `2 < 5` | Checks if the left value is smaller. |
| Comparison | `>=` | `5 >= 5` | Checks if the left value is greater than or equal to the right. |
| Comparison | `<=` | `2 <= 5` | Checks if the left value is smaller than or equal to the right. |
| Logical | `and` | `True and False` | Returns `True` if both conditions are true. |
| Logical | `or` | `True or False` | Returns `True` if at least one condition is true. |
| Logical | `not` | `not True` | Reverses the Boolean result. |
| Identity | `is` | `x is y` | Checks if two variables refer to the same object. |
| Identity | `is not` | `x is not y` | Checks if two variables refer to different objects. |
| Membership | `in` | `"a" in "apple"` | Checks if a value exists in a sequence or collection. |
| Membership | `not in` | `"z" not in "apple"` | Checks if a value does not exist in a sequence or collection. |
| Bitwise | `&` | `5 & 3 = 1` | Performs bitwise AND. |
| Bitwise | `\|` | `5 \| 3 = 7` | Performs bitwise OR. |
| Bitwise | `^` | `5 ^ 3 = 6` | Performs bitwise XOR. |
| Bitwise | `~` | `~5 = -6` | Performs bitwise NOT (inverts bits). |
| Bitwise | `<<` | `5 << 1 = 10` | Shifts bits to the left. |
| Bitwise | `>>` | `5 >> 1 = 2` | Shifts bits to the right. |


