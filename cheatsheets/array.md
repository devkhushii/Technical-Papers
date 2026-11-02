# Python Arrays – Quick Revision Cheat Sheet

## 1. Creating an Array

Python commonly uses lists and the `array` module.

**List:**
```python
>>> numbers = [10, 20, 30, 40]
>>> numbers
[10, 20, 30, 40]
```

**Array module:**
```python
>>> from array import array
>>> numbers = array('i', [10, 20, 30])
>>> numbers
array('i', [10, 20, 30])
```

**Common type codes:**

| Code | Data Type |
|---|---|
| `'i'` | Integer |
| `'f'` | Float |
| `'d'` | Double |

## 2. Accessing Elements

```python
>>> numbers = [10, 20, 30, 40, 50]
>>> numbers[0]
10
>>> numbers[-1]
50
>>> numbers[1:4]
[20, 30, 40]
>>> numbers[::-1]
[50, 40, 30, 20, 10]
```

## 3. Updating Elements

```python
>>> numbers = [10, 20, 30]
>>> numbers[1] = 50
>>> numbers
[10, 50, 30]
```

## 4. Adding Elements

```python
>>> numbers = [10, 20, 30]
>>> numbers.append(40)     # Add one element at the end
>>> numbers
[10, 20, 30, 40]

>>> numbers.insert(1, 15)    # Add element at a specific index
>>> numbers
[10, 15, 20, 30, 40]

>>> numbers.extend([50, 60])     # Add multiple elements 
>>> numbers
[10, 15, 20, 30, 40, 50, 60]
```

## 5. Removing Elements

```python
>>> numbers = [10, 20, 30, 40]
>>> numbers.remove(20)        # Remove first occurrence of a value 
>>> numbers
[10, 30, 40]

>>> numbers.pop()           # Remove and return last element
40
>>> numbers.pop(0)         # Remove and return element at index
10

>>> numbers
[30]

>>> numbers.clear()       # Remove all elements
```

## 6. Searching and Counting


```python
>>> numbers = [10, 20, 30, 20]
>>> numbers.index(20)        # Find index of first occurrence
1
>>> numbers.count(20)        # Count occurrences
2
>>> 30 in numbers           # Check whether an element exists 
True
>>> 50 in numbers
False
```

## 7. Sorting and Reversing

```python
>>> numbers = [40, 10, 30, 20]
>>> numbers.sort()       # Sort original list 
>>> numbers
[10, 20, 30, 40]

>>> numbers.sort(reverse=True)   
>>> numbers
[40, 30, 20, 10]

>>> sorted(numbers)      # Return a new sorted list
[10, 20, 30, 40]

>>> numbers.reverse()     # Reverse original list
>>> numbers
[20, 30, 10, 40]
```

## 8. Useful Built-in Functions


```python
>>> numbers = [10, 20, 30, 40]
>>> len(numbers)   # Number of elements
4
>>> min(numbers)   # Smallest element
10
>>> max(numbers)   #  Largest element
40
>>> sum(numbers)       # Sum of elements
100
>>> any(numbers)      # True if at least one element is truthy
True
>>> all(numbers)         # True if all elements are truthy
True
```

## 9. Looping Through a List

```python
>>> numbers = [10, 20, 30]
>>> for num in numbers:
...     print(num)
10
20
30
```

**Using `enumerate()`:**

```python
>>> for index, value in enumerate(numbers):
...     print(index, value)
0 10
1 20
2 30
```

## 10. List Comprehension

```python
>>> numbers = [1, 2, 3, 4, 5]
>>> squares = [num ** 2 for num in numbers]
>>> squares
[1, 4, 9, 16, 25]
```

**With condition:**

```python
>>> even = [num for num in numbers if num % 2 == 0]
>>> even
[2, 4]
```

## 11. Copying a List

```python
>>> a = [10, 20, 30]
>>> b = a
>>> b.append(40)
>>> a
[10, 20, 30, 40]
```

Both variables refer to the same list.

**Using `copy()`:**

```python
>>> a = [10, 20, 30]
>>> b = a.copy()
>>> b.append(40)
>>> a
[10, 20, 30]
>>> b
[10, 20, 30, 40]
```

`copy()` creates a shallow copy.


## 13. Time Complexity

| Operation | Complexity |
|---|---|
| Access by index | O(1) |
| Update by index | O(1) |
| Append | O(1) amortized |
| Insert at beginning | O(n) |
| Delete from beginning | O(n) |
| Search | O(n) |
| Remove by value | O(n) |
| Sorting | O(n log n) |
