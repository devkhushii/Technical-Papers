# Python General Cheat Sheet


### What is Python?
Python is a high-level, interpreted, general-purpose programming language.

```python
>>> print("Hello Khushi")
Hello Khushi
```

### Comments in Python

```python
# This is a single-line comment.
```

### Docstrings
- Used to document modules, classes, and functions.

```python
"""Description of the module."""
```

### Keywords
- Reserved words with special meanings in Python.
Examples: `if`, `else`, `for`, `while`, `break`, `continue`, `def`, `return`, `class`, `True`, `False`, `None`.
To get all Python keywords:

```python
import keyword

print(keyword.kwlist)
print(keyword.iskeyword("if"))  # True
```

### Identifiers
- Names given to variables, functions, classes, etc.

### Variables

Variables are names that refer to objects in Python.

```python
name = "Khushi"       # Variable assignment
x = 20

x += 5                # Increment
print(x)              # 25

a, b, c = 10, 20, 30  # Multiple assignment
x = y = z = 0         # Same value assignment

a, b = b, a           # Swapping variables

x = 10
x = "Python"          # Reassignment

PI = 3.14             # Constant naming convention

print(id(x))          # Object identity
print(type(x))        # <class 'str'>

del x                 # Deletes the variable reference

print(isinstance(3.14, float))  # True
print(issubclass(int, object))  # True
```



## 2. Data Types

| Category | Data Type | Example | Description |
|---|---|---|---|
| Numeric | `int` | `age = 21` | Stores whole numbers without decimal points. |
| Numeric | `float` | `price = 99.50` | Stores floating-point numbers. |
| Numeric | `complex` | `num = 3 + 4j` | Stores complex numbers with real and imaginary parts. |
| Text | `str` | `name = "Khushi"` | Stores a sequence of characters. |
| Boolean | `bool` | `is_active = True` | Stores either `True` or `False`. |
| Sequence | `list` | `[1, 2, 3]` | Ordered, mutable collection. |
| Sequence | `tuple` | `(1, 2, 3)` | Ordered, immutable collection. |
| Sequence | `range` | `range(1, 5)` | Represents a sequence of integers. |
| Mapping | `dict` | `{"name": "Khushi"}` | Stores data in key-value pairs. |
| Set | `set` | `{1, 2, 3}` | Stores unique elements in an unordered collection. |
| Set | `frozenset` | `frozenset({1, 2})` | Immutable collection of unique elements. |
| Binary | `bytes` | `b"Hello"` | Stores immutable binary data. |
| Binary | `bytearray` | `bytearray(5)` | Stores mutable binary data. |
| Binary | `memoryview` | `memoryview(b"abc")` | Provides access to binary data without copying it. |
| None | `NoneType` | `result = None` | Represents the absence of a value. |

### Mutable vs Immutable

| Mutable | Immutable |
|---|---|
| Can be modified after creation. | Cannot be modified after creation. |
| `list`, `dict`, `set`, `bytearray` | `int`, `float`, `complex`, `bool`, `str`, `tuple`, `range`, `bytes`, `frozenset` |



## 3. Type Conversion (Casting)

```python
# Explicit conversion
int("10")       # 10
float("3")      # 3.0
str(45)         # '45'
bool(4)         # True
bool(0)         # False
complex(2)      # (2+0j)

# Implicit conversion
x = 5 + 2.5
print(x)        # 7.5
```

**Important Notes:**

```python
int(5.9)       # 5
int(-5.9)      # -5

# int("5.9")   # ValueError
float("5.9")   # 5.9

bool("")       # False
bool("False")  # True
```

### Python Operators

| Category | Operator | Example | Description |
|---|---|---|---|
| Arithmetic | `+` | `5 + 2 = 7` | Adds two values. |
| Arithmetic | `-` | `5 - 2 = 3` | Subtracts two values. |
| Arithmetic | `*` | `5 * 2 = 10` | Multiplies two values. |
| Arithmetic | `/` | `5 / 2 = 2.5` | Performs division and returns a float. |
| Arithmetic | `//` | `5 // 2 = 2` | Performs floor division. |
| Arithmetic | `%` | `5 % 2 = 1` | Returns the remainder. |
| Arithmetic | `**` | `5 ** 2 = 25` | Performs exponentiation. |
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
| Assignment | `>>=` | `x >>= 1` | Performs right shift and assigns the result. |
| Assignment | `<<=` | `x <<= 1` | Performs left shift and assigns the result. |
| Comparison | `==` | `5 == 5` | Checks whether two values are equal. |
| Comparison | `!=` | `5 != 2` | Checks whether two values are not equal. |
| Comparison | `>` | `5 > 2` | Checks whether the left value is greater. |
| Comparison | `<` | `2 < 5` | Checks whether the left value is smaller. |
| Comparison | `>=` | `5 >= 5` | Checks whether the left value is greater than or equal to the right. |
| Comparison | `<=` | `2 <= 5` | Checks whether the left value is smaller than or equal to the right. |
| Logical | `and` | `True and False` | Returns one of its operands; both must be truthy to return the second operand. |
| Logical | `or` | `True or False` | Returns the first truthy operand, or the last operand if none is truthy. |
| Logical | `not` | `not True` | Reverses the truth value and returns a Boolean. |
| Identity | `is` | `x is y` | Checks whether two references point to the same object. |
| Identity | `is not` | `x is not y` | Checks whether two references point to different objects. |
| Membership | `in` | `"a" in "apple"` | Checks whether a value exists in a collection. |
| Membership | `not in` | `"z" not in "apple"` | Checks whether a value does not exist in a collection. |
| Bitwise | `&` | `5 & 3 = 1` | Performs bitwise AND. |
| Bitwise | `\|` | `5 \| 3 = 7` | Performs bitwise OR. |
| Bitwise | `^` | `5 ^ 3 = 6` | Performs bitwise XOR. |
| Bitwise | `~` | `~5 = -6` | Performs bitwise NOT. |
| Bitwise | `<<` | `5 << 1 = 10` | Shifts bits to the left. |
| Bitwise | `>>` | `5 >> 1 = 2` | Shifts bits to the right. |


### Operator Precedence

Highest to lowest (simplified):

```text
()
**
+x, -x, ~x
*, /, //, %
+, -
<<, >>
&
^
|
==, !=, <, >, <=, >=, is, is not, in, not in
not
and
or
```


### Input


```python
name = input("Enter your name: ")
age = int(input("Enter your age: "))
```

### Multiple Inputs

```python
a, b = input().split()

# Input: 10 20
# a = "10", b = "20"
```

Using `map()` for integer conversion:

```python
a, b = map(int, input().split())

# Input: 10 20
# a = 10, b = 20
```

### Output

`print()` displays output on the screen.

```python
print("Hello Python")
print(10, 20, 30)
```

### Important `print()` Parameters

| Parameter | Description | Example |
|---|---|---|
| `sep` | Specifies the separator between values. | `print(1, 2, sep="-")` → `1-2` |
| `end` | Specifies what to print at the end. | `print("Hi", end=" ")` |
| `file` | Specifies the output destination. | `print("Hello", file=f)` |
| `flush` | Forces the output buffer to be flushed. | `print("Hi", flush=True)` |

---

## 6. String Formatting

String formatting allows variables and values to be inserted into strings.

### f-Strings (Recommended)

```python
name = "Khushi"
age = 21

print(f"My name is {name} and I am {age} years old.")
```

### Format Specifiers

| Specifier | Description | Example | Result |
|---|---|---|---|
| `:.2f` | Displays 2 decimal places. | `f"{3.14159:.2f}"` | `3.14` |
| `:d` | Integer format. | `f"{10:d}"` | `10` |
| `:b` | Binary format. | `f"{10:b}"` | `1010` |
| `:x` | Hexadecimal format. | `f"{255:x}"` | `ff` |
| `:o` | Octal format. | `f"{8:o}"` | `10` |
| `:.1%` | Percentage format with 1 decimal place. | `f"{0.75:.1%}"` | `75.0%` |
| `:>10` | Right-aligns within width 10. | `f"{'Hi':>10}"` | Right-aligned |
| `:<10` | Left-aligns within width 10. | `f"{'Hi':<10}"` | Left-aligned |
| `:^10` | Center-aligns within width 10. | `f"{'Hi':^10}"` | Centered |

### Other Formatting Methods

```python
# format() method
"Hello {}".format("Khushi")

# Old-style formatting
"Hello %s" % "Khushi"
```


## 7. Important Built-in Functions
``` bash
>>> type(10)
<class 'int'>

>>> isinstance(10, int)
True

>>> x = 10
>>> id(x)
140...

>>> len("Python")
6

>>> abs(-10)
10

>>> round(3.14159, 2)
3.14

>>> pow(2, 3)
8

>>> divmod(10, 3)
(3, 1)

>>> sum([1, 2, 3])
6

>>> min(1, 2, 3)
1

>>> max(1, 2, 3)
3

>>> sorted([3, 1, 2])
[1, 2, 3]

>>> reversed([1, 2, 3])
<list_reverseiterator object at ...>

>>> list(reversed([1, 2, 3]))
[3, 2, 1]

>>> any([0, 1, 0])
True

>>> all([1, 2, 3])
True

>>> bin(10)
'0b1010'

>>> oct(8)
'0o10'

>>> hex(255)
'0xff'

>>> round(2.5)
2

>>> round(3.5)
4

>>> any([False, True])
True

>>> all([True, True])
True

>>> any([])
False

>>> all([])
True

>>> divmod(10, 3)
(3, 1)

>>> sorted([3, 1, 2])
[1, 2, 3]

```



### range(), enumerate() & zip()

#### range()
```python
>>> list(range(5))
[0, 1, 2, 3, 4]

>>> list(range(1, 5))
[1, 2, 3, 4]

>>> list(range(1, 10, 2))
[1, 3, 5, 7, 9]

>>> list(range(5, 0, -1))
[5, 4, 3, 2, 1]
```

#### enumerate()

```python
>>> names = ["Khushi", "Rahul", "Aman"]

>>> list(enumerate(names))
[(0, 'Khushi'), (1, 'Rahul'), (2, 'Aman')]

>>> list(enumerate(names, start=1))
[(1, 'Khushi'), (2, 'Rahul'), (3, 'Aman')]
```


### zip()

```python
>>> names = ["Khushi", "Rahul", "Aman"]

>>> ages = [21, 22, 20]

>>> list(zip(names, ages))
[('Khushi', 21), ('Rahul', 22), ('Aman', 20)]

>>> a = [1, 2, 3]

>>> b = ["A", "B"]

>>> list(zip(a, b))
[(1, 'A'), (2, 'B')]
```


### Iterable vs Iterator


```python
#iterable
>>> numbers = [10, 20, 30]

>>> iter(numbers)
<list_iterator object at ...>

#iterator
>>> numbers = [10, 20, 30]

>>> iterator = iter(numbers)

>>> next(iterator)
10

>>> next(iterator)
20

>>> next(iterator)
30

```
