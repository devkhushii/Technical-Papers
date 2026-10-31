# PEP 8 – Quick Revision Cheat Sheet

## 1. What is PEP 8?

PEP 8 is Python’s official style guide. It helps developers write **readable and consistent code**.

## 2. Indentation

Use **4 spaces** for each indentation level. Avoid mixing tabs and spaces.

```python
>>> if True:
...     print("Hello")
Hello
```

## 3. Line Length

- Keep lines to **79 characters**.
- Keep comments and docstrings to **72 characters**.

```python
>>> total = (
...     first_number
...     + second_number
... )
```

## 4. Naming Conventions

| Element | Convention | Example |
|---|---|---|
| Variable | `snake_case` | `user_name` |
| Function | `snake_case` | `calculate_total()` |
| Class | `PascalCase` | `UserAccount` |
| Constant | `UPPER_CASE` | `MAX_RETRIES` |
| Module | Short `snake_case` | `data_loader.py` |
| Package | Short, lowercase | `mypackage` |

## 5. Spaces

Use spaces around operators and after commas.

```python
>>> total = price + tax
>>> numbers = [1, 2, 3]
>>> function(value, other_value)
```

Avoid unnecessary spaces:

```python
>>> numbers[0]
>>> calculate_total()
```

## 6. Blank Lines

- Use **2 blank lines** between top-level functions and classes.
- Use **1 blank line** between methods inside a class.
- Use blank lines to separate logical sections.

## 7. Imports

Place imports at the top of the file, usually in this order:

1. Standard library
2. Third-party packages
3. Local application imports

```python
import os
import sys

import requests

from my_module import calculate_total
```

Avoid wildcard imports:

```python
from module import *
```

## 8. Comments

Write comments that explain **why**, not simply what the code does.

```python
# Retry because the API may temporarily fail
```

Keep comments clear and up to date.

## 9. Strings and Quotes

Use single or double quotes consistently.

```python
>>> name = "Khushi"
>>> message = 'Hello'
```

Use whichever makes the string easier to read, especially when the other quote appears inside it.

## 10. Avoid Common Style Issues

| Avoid | Prefer |
|---|---|
| `x=10` | `x = 10` |
| `def func (x):` | `def func(x):` |
| `if x==10:` | `if x == 10:` |
| `import os, sys` | Separate import lines |
| `myFunction()` | `my_function()` |
| `MAXretry = 3` | `MAX_RETRY = 3` |

## 11. Check PEP 8

Install and run `pycodestyle`:

```bash
$ pip install pycodestyle
$ pycodestyle file.py
```

Check all Python files:

```bash
$ pycodestyle .
```

