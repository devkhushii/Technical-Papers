# Python Dictionary – Quick Revision Cheat Sheet

## 1. Creating a Dictionary

```python
>>> person = {"name": "Kanika", "age": 22}
>>> person
{'name': 'Kanika', 'age': 22}

>>> empty = dict()
>>> empty
{}
```

## 2. Accessing Values

```python
>>> person["name"]
'Kanika'

>>> person.get("age")
22

>>> person.get("city", "Unknown")
'Unknown'
```

## 3. Adding and Updating Items

```python
>>> person["city"] = "Ranchi"
>>> person
{'name': 'Kanika', 'age': 22, 'city': 'Ranchi'}

>>> person.update({"age": 23, "country": "India"})
>>> person
{'name': 'Kanika', 'age': 23, 'city': 'Ranchi', 'country': 'India'}
```

## 4. Removing Items

```python
>>> person = {"name": "Kanika", "age": 22, "city": "Ranchi"}

>>> person.pop("age")
22

>>> person.popitem()
('city', 'Ranchi')

>>> del person["name"]
>>> person
{}

>>> person.clear()
>>> person
{}
```

## 5. All Dictionary Methods

| Method | Purpose |
|---|---|
| `clear()` | Remove all items |
| `copy()` | Create a shallow copy |
| `fromkeys()` | Create dictionary from given keys |
| `get()` | Get value safely |
| `items()` | Get key-value pairs |
| `keys()` | Get all keys |
| `pop()` | Remove key and return its value |
| `popitem()` | Remove last inserted pair |
| `setdefault()` | Get value; add key if missing |
| `update()` | Add or update items |
| `values()` | Get all values |

## 6. Examples of Dictionary Methods

```python
>>> person = {"name": "Kanika", "age": 22}

>>> person.keys()
dict_keys(['name', 'age'])

>>> person.values()
dict_values(['Kanika', 22])

>>> person.items()
dict_items([('name', 'Kanika'), ('age', 22)])

>>> person.copy()
{'name': 'Kanika', 'age': 22}
```

**`fromkeys()`**

```python
>>> dict.fromkeys(["name", "age", "city"], "Unknown")
{'name': 'Unknown', 'age': 'Unknown', 'city': 'Unknown'}
```

**`setdefault()`**

```python
>>> person.setdefault("city", "Ranchi")
'Ranchi'

>>> person
{'name': 'Kanika', 'age': 22, 'city': 'Ranchi'}
```

## 7. Checking Keys and Length

```python
>>> person = {"name": "Kanika", "age": 22}

>>> "name" in person
True

>>> "Kanika" in person
False

>>> "Kanika" in person.values()
True

>>> len(person)
2
```

`in` checks keys by default.

## 8. Looping Through a Dictionary

```python
>>> for key in person:
...     print(key)
name
age
```

```python
>>> for value in person.values():
...     print(value)
Kanika
22
```

```python
>>> for key, value in person.items():
...     print(key, value)
name Kanika
age 22
```

## 9. Dictionary Comprehension

```python
>>> numbers = [1, 2, 3, 4]
>>> squares = {num: num ** 2 for num in numbers}
>>> squares
{1: 1, 2: 4, 3: 9, 4: 16}
```

```python
>>> even_squares = {num: num ** 2 for num in numbers if num % 2 == 0}
>>> even_squares
{2: 4, 4: 16}
```

## 10. Counting Items

```python
>>> words = ["apple", "banana", "apple", "orange", "banana", "apple"]
>>> counts = {}

>>> for word in words:
...     counts[word] = counts.get(word, 0) + 1

>>> counts
{'apple': 3, 'banana': 2, 'orange': 1}
```

## 11. Merging Dictionaries

```python
>>> a = {"name": "Kanika", "age": 22}
>>> b = {"city": "Ranchi", "age": 23}

>>> {**a, **b}
{'name': 'Kanika', 'age': 23, 'city': 'Ranchi'}

>>> a | b
{'name': 'Kanika', 'age': 23, 'city': 'Ranchi'}
```

The second dictionary overwrites duplicate keys. The `|` operator requires Python 3.9+.

## 12. Useful Built-in Functions

```python
>>> person = {"name": "Kanika", "age": 22}

>>> len(person)
2

>>> list(person)
['name', 'age']

>>> sorted(person)
['age', 'name']

>>> type(person)
<class 'dict'>

>>> person = {"name": "Kanika", "age": "22", "city": "Ranchi"}

>>> str(person)
"{'name': 'Kanika', 'age': '22', 'city': 'Ranchi'}"

>>> list(person)
['name', 'age', 'city']

>>> sorted(person)
['age', 'city', 'name']

>>> min(person)
'age'

>>> max(person)
'name'

>>> all(person)
True

>>> any(person)
True

>>> list(reversed(person))
['city', 'age', 'name']
```

## 14. Time Complexity

| Operation | Average Complexity |
|---|---|
| Access by key | O(1) |
| Insert / Update | O(1) |
| Delete by key | O(1) |
| Check key existence | O(1) |
| Loop through dictionary | O(n) |


## 15. Nested Dictionary (Dictionary of Dictionaries)

A dictionary can contain another dictionary as its value.

```python
>>> students = {
...     "s1": {"name": "Kanika", "age": 22, "marks": 85},
...     "s2": {"name": "Rahul", "age": 21, "marks": 92},
...     "s3": {"name": "Priya", "age": 23, "marks": 78}
... }
```


**Loop through nested dictionary:**

```python
>>> for student_id, details in students.items():
...     print(student_id, details["name"], details["marks"])
s1 Kanika 95
s2 Rahul 21 92
s3 Priya 23 78
```

## 16. Sorting a Dictionary

### Sort by Keys

```python
>>> marks = {"Rahul": 92, "Kanika": 85, "Priya": 78}

>>> sorted(marks)
['Kanika', 'Priya', 'Rahul']
```

**Create a sorted dictionary by keys:**

```python
>>> dict(sorted(marks.items()))
{'Kanika': 85, 'Priya': 78, 'Rahul': 92}
```

### Sort by Values

```python
>>> marks = {"Rahul": 92, "Kanika": 85, "Priya": 78}

>>> sorted(marks.items(), key=lambda item: item[1])
[('Priya', 78), ('Kanika', 85), ('Rahul', 92)]
```

**Descending order:**

```python
>>> sorted(marks.items(), key=lambda item: item[1], reverse=True)
[('Rahul', 92), ('Kanika', 85), ('Priya', 78)]
```

**Create a sorted dictionary:**

```python
>>> dict(sorted(marks.items(), key=lambda item: item[1]))
{'Priya': 78, 'Kanika': 85, 'Rahul': 92}
```

### Important Sorting Parameters

| Parameter | Purpose |
|---|---|
| `key` | Decides what to sort by |
| `reverse=True` | Sort in descending order |
| `item[0]` | Sort by key |
| `item[1]` | Sort by value |

## 17. Sorting a Dictionary of Dictionaries

```python
>>> students = {
...     "s1": {"name": "Kanika", "marks": 85},
...     "s2": {"name": "Rahul", "marks": 92},
...     "s3": {"name": "Priya", "marks": 78}
... }
```

**Sort by marks (ascending):**

```python
>>> sorted(students.items(), key=lambda item: item[1]["marks"])
[('s3', {'name': 'Priya', 'marks': 78}), ('s1', {'name': 'Kanika', 'marks': 85}), ('s2', {'name': 'Rahul', 'marks': 92})]
```

**Sort by marks (descending):**

```python
>>> dict(sorted(students.items(), key=lambda item: item[1]["marks"], reverse=True))
{'s2': {'name': 'Rahul', 'marks': 92}, 's1': {'name': 'Kanika', 'marks': 85}, 's3': {'name': 'Priya', 'marks': 78}}
```

**Sort by name:**

```python
>>> dict(sorted(students.items(), key=lambda item: item[1]["name"]))
{'s1': {'name': 'Kanika', 'marks': 85}, 's3': {'name': 'Priya', 'marks': 78}, 's2': {'name': 'Rahul', 'marks': 92}}
```

## 18. Sorting with `lambda`

A `lambda` is a small anonymous function, commonly used with `sorted()`.

```python
>>> numbers = [40, 10, 30, 20]

>>> sorted(numbers, key=lambda x: x)
[10, 20, 30, 40]

>>> sorted(numbers, key=lambda x: -x)
[40, 30, 20, 10]
```

**Sorting a list of dictionaries:**

```python
>>> employees = [
...     {"name": "Kanika", "salary": 50000},
...     {"name": "Rahul", "salary": 70000},
...     {"name": "Priya", "salary": 60000}
... ]

>>> sorted(employees, key=lambda x: x["salary"])
[{'name': 'Kanika', 'salary': 50000}, {'name': 'Priya', 'salary': 60000}, {'name': 'Rahul', 'salary': 70000}]
```

**Descending order:**

```python
>>> sorted(employees, key=lambda x: x["salary"], reverse=True)
[{'name': 'Rahul', 'salary': 70000}, {'name': 'Priya', 'salary': 60000}, {'name': 'Kanika', 'salary': 50000}]
```

## 19. Important Sorting Patterns

| Requirement | Syntax |
|---|---|
| Sort dictionary by keys | `dict(sorted(d.items()))` |
| Sort dictionary by values | `dict(sorted(d.items(), key=lambda x: x[1]))` |
| Sort by values descending | `dict(sorted(d.items(), key=lambda x: x[1], reverse=True))` |
| Sort nested dictionary | `sorted(d.items(), key=lambda x: x[1]["marks"])` |
| Sort list of dictionaries | `sorted(data, key=lambda x: x["salary"])` |
| Sort by multiple fields | `sorted(data, key=lambda x: (x["marks"], x["age"]))` |