# Object Oreinted Programming

## What is OOP?
- OOP (Object Oreinted Programming) is a programming technique in which we organise our code using class and object.
- It helps achieve code reusability, modularity, maintainability and flexibility through concepts such as encapsulation, inheritance, polymorphism and abstraction.

## Class
- Blueprint or template which is used to create object.
- syntax:
    ``` bash 
    class Student:
        pass
   ```

## Object
-  An instance of class.
- syntax:
```bash
class Student:
    pass

student1 = Student()         # object, here student1 is the reference of object
```
- Here `Student()` is the instance of class `Student` and it creates object in memory which reference's is assigned to variable `student1`

``` bash
>>> class Student:
...     pass
... student1=Student()
... print(Student())
... print(student1)
>>>
<__main__.Student object at 0x7072a8a86990>
<__main__.Student object at 0x7072a8a27770>
>>> 
>>> print(type(Student()))
... print(type(student1))
<class '__main__.Student'>
<class '__main__.Student'>
```

### What are Attributes? 
- Attributes are variables associated with an object or class.

### What are methods?
- functions inside class

### What is self?
- self is the naming convention used to reference the current object.

## Types of variable in OOP

### Instance variable
- An instance variable belongs to a particular object.

### class variable
- A class variable belongs to the class itself and is shared by instances unless an instance overrides it with its own attribute.


## Types of methods

### 1. Instance method
- An instance method works with the data of an individual object.
- It takes `self` as its first parameter

### 2. class method
- A class method works with the class rather than a particular object.
- It uses the `@classmethod` decorator and takes `cls` as its first parameter.

### 3. static method
- A static method is a method that doesn't automatically receive self or cls.
- It uses the `@staticmethod` decorator.
- A utility method related to class but doesn't access its instance or class data.

```bash
>>> class Student:
...     school = "ABC School"
...     def __init__(self,name,marks):
...         self.name=name
...         self.marks=marks
...     def display(self):
...         print("Instance method:",self.name,self.marks)
...     @classmethod
...     def change_school(cls,new_school):
...         cls.school=new_school
...         print("class method:",cls.school)
...     @staticmethod
...     def is_pass(marks):
...         print("static method:", marks>=40)
...     @staticmethod
...     def show_college():
...        print(Student.college)
>>> s1=Student("khushi",95)
>>> s1.display()
Instance method: khushi 95
>>> Student.change_school("XYZ School")
class method: XYZ School
>>> Student.is_pass(85)
static method: True
```

## Constructor - ` __init__() `
- It is a special method which is autmatically called when object is intialized.
- It intializes the object's attributes.
- `__init__` should never return anything.

```bash
class Student:
    college="ABC college"  # class variable
    def __init__(self, name="Unknown", age=0):
        self.name = name      # instance variable
        self.age = age


student1 = Student("Khushi", 22)
student2 = Student()

print(student1.name)
print(student2.name)

```
## Types of Constructor

### 1. Non-Parameterized (default) constructor
- if don't define `__init__` at all, python automatically provides default do-nothing constructor behind the scences.

### 2. Parameterized constructor
- Takes parameters to intialize object at creation time.

### 3. Copy constructor
- A copy constructor creates a new object by copying the data of an existing object.
- both objects have the same data but stored as separate objects.
- python does not have built in copy constructor ; we can implement using a class method or the copy module.

```bash
>>> class Student:
... 
...     # 1. Default Constructor
...     def __init__(self):
...         self.name = "Khushi"
...         self.marks = 85
... 
...     # Instance Method
...     def display(self):
...         print(self.name, self.marks)
... 
... # Calling Default Constructor
... s1 = Student()
... s1.display()
Khushi 85

>>> class Employee:
... 
...     # 2. Parameterized Constructor
...     def __init__(self, name, salary):
...         self.name = name
...         self.salary = salary
... 
...     # 3. Copy Constructor (custom implementation)
...     @classmethod
...     def copy_constructor(cls, obj):
...         return cls(obj.name, obj.salary)
... 
...     def display(self):
...         print(self.name, self.salary)
... 
... # Calling Parameterized Constructor
... e1 = Employee("Rahul", 50000)
... e1.display()
... 
... # Calling Copy Constructor
... e2 = Employee.copy_constructor(e1)
... e2.display()
... 
Rahul 50000
Rahul 50000
```

## Destructors and Garbage Collection
1. **Destructor (__del__()):**
        - A special method called when an object is being finalized.
        - Used for cleanup activities.
        - Example: def __del__(self):
2. **Garbage Collection (GC):**
        - The process of automatically identifying and removing objects that are no longer reachable.
        - Helps free unused memory.
        - Python mainly uses:
              - Reference Counting: Tracks how many references point to an object. When the count becomes zero, the object can be destroyed.
              - Cyclic Garbage Collection: Removes unreachable objects that reference each other.
```bash
class Student:
    def __init__(self, name):
        self.name = name

    def __del__(self):
        print("Object destroyed")

s1 = Student("Khushi")
s2 = s1   # Both s1 and s2 refer to the same object (no new object is created).

del s1  # Object is not destroyed because s2 still refers to it.

del s2  # Object becomes eligible for garbage collection.
```

## Encapsulation
- Encapsulation means combining data and the methods that operate on that data inside a single unit (a class), while controlling how that data is accessed or modified.
- Encapsulation = Data Hiding + Data Bundling.

#### Data Hiding (achieved through encapsulation)
- hiding sensitive data from user that should not be visible.
- Achieved using naming convention based access control (`_proctected`, `__private`)

### Access Modifiers
- Access modifiers define how class variables and methods can be accessed from outside or inside a class.

Python has three types of access modifiers:
  1. Public
      - Can be accessed from anywhere (inside and outside the class).
      - No underscore is used.
  2. Protected
      - Intended to be accessed within the class and its child classes.
      - Uses a single underscore _.
  3. Private
      - Intended to be accessed only within the class.
      - Uses double underscores __.
      - Python uses name mangling to make direct access harder.

  
### Getter, Setter & property
##### What are Getter and Setters?
- Sometimes we don't want users to directly modify an object's attributes.
  Instead, we want to control how they access or update them.
  We use:
  - **Getter:** Retrieves an attribute's value.
  - **Setter:** Updates an attribute's value.

##### What is the `@property` decorator?
- The `@property` decorator in Python allows us to access a method like a normal variable (attribute), without using parentheses ().
- It is commonly used in encapsulation to implement getters and setters.

**Example:**
```bash
>>> class Student:
... 
...     def __init__(self, name, age, marks):
...         self.name = name          # Public
...         self._age = age            # Protected
...         self.__marks = marks       # Private
... 
...     # Getter using @property
...     @property
...     def marks(self):
...         return self.__marks
... 
...     # Setter using @marks.setter
...     @marks.setter
...     def marks(self, marks):
...         if 0 <= marks <= 100:
...             self.__marks = marks
...         else:
...             print("Invalid marks!")
... 
...     # Display method
...     def display(self):
...         print("Name:", self.name)
...         print("Age:", self._age)
...         print("Marks:", self.__marks)
... 
... 
... # Creating object
... s1 = Student("Khushi", 22, 85)
... 
>>> # Accessing public variable
... print(s1.name)
Khushi
>>> # Accessing protected variable
>>> print(s1._age)
22
>>> print(s1.display())  # Private variable accessed through class method
Name: Khushi
Age: 22
Marks: 85
>>> # Accessing private variable using property (Getter)
>>> print(s1.marks)
85
>>> # Updating private variable using property (Setter)
>>> s1.marks = 95
>>> print(s1.marks)
95
>>> # Displaying all details
>>> s1.display()
Name: Khushi
Age: 22
Marks: 95
>>> print(s1._Student__marks)  # To access a private variable from outside the class, Python uses name mangling
95
```

## Inheritance
- Inhertiance allows one class to acquire the attributes and methods of another class.
- A chlid class can reuse the functionality of a parent class.
- Python supports multiple inheritance. When multiple parent classes contain methods with the same name, Python uses MRO (Method Resolution Order) to decide which method to call.

### Types of Inheritance
#### 1. Single Inheritance
 - one child inherits from one parent.
```bash 
>>> class Parent:
...     def show(self):
...         print("This is Parent class")
... 
... class Child(Parent):
...     def display(self):
...         print("This is Child class")
... 
... c = Child()
... c.show
...
This is Parent class
>>> c.display()
... 
This is Child class
```

#### 2. Multiple Inheritance
- one class inherits from two or more parent classes.
```bash
>>> class Father:
...     def father_name(self):
...         print("Father: Rahul")
... 
... class Mother:
...     def mother_name(self):
...         print("Mother: Priya")
... 
... class Child(Father, Mother):
...     pass
... 
... c = Child()
... c.father_name()
... c.mother_name()
... 
Father: Rahul
Mother: Priya
```

#### Multilevel Inheritance
- A class inherits from another child class, forming a chain of inheritance.
```bash
>>> class Grandparent:
...     def show(self):
...         print("Grandparent class")
... 
... class Parent(Grandparent):
...     pass
... 
... class Child(Parent):
...     pass
... 
... c = Child()
... c.show()
... 
Grandparent class
>>>
```

#### Hierarchical Inheritance
- Multiple class inherits from the same parent class.
```bash
>>> class Parent:
...     def show(self):
...         print("Parent class")
... 
... class Child1(Parent):
...     pass
... 
... class Child2(Parent):
...     pass
... 
... c1 = Child1()
... c2 = Child2()
... 
... c1.show()
... c2.show()
... 
Parent class
Parent class
>>> 
```

#### Hybrid Inheritance
- A combination of two or more types of inhertiance.
```bash 
>>> class A:
...     def show(self):
...         print("Class A")
... 
... class B(A):
...     pass
... 
... class C(A):
...     pass
... 
... class D(B, C):
...     pass
... 
... d = D()
... d.show()
... 
Class A
>>> 
```

### `super()` Function
- `super()` is used to access methods and constructors of the parent class from the child class.
- It avoids directly referring to the parent class name.
- In multiple inheritance, `super()` follows the Method Resolution Order (MRO).

**Example:**
```python
class Parent:
    def __init__(self):
        print("Parent Constructor")

    def show(self):
        print("Parent Method")


class Child(Parent):
    def __init__(self):
        super().__init__()
        print("Child Constructor")

    def display(self):
        super().show()
        print("Child Method")


c = Child()
c.display()
```

**Output:**
```text
Parent Constructor
Child Constructor
Parent Method
Child Method
```

### Method Resolution Order (MRO)
- MRO defines the order in which Python searches for a method or attribute in a class hierarchy.
- Python uses the C3 Linearization algorithm to determine the MRO.
- We can check MRO using:
    - `ClassName.mro()`
    - `ClassName.__mro__`

**Example:**
```python
class A:
    def show(self):
        print("Class A")

class B(A):
    def show(self):
        print("Class B")

class C(A):
    def show(self):
        print("Class C")

class D(B, C):
    pass

d = D()
d.show()

print(D.mro())
```

**Output:**
```text
Class B

[<class '__main__.D'>,
 <class '__main__.B'>,
 <class '__main__.C'>,
 <class '__main__.A'>,
 <class 'object'>]
```

**Explanation:**

When `d.show()` is called:

1. Python searches in class `D`.
2. It does not find `show()`.
3. It searches in class `B`.
4. It finds `show()` in `B` and executes it.

Therefore, the output is `Class B`.

**Important:** Every Python class ultimately inherits from the built-in `object` class (directly or indirectly).

---

## Polymorphism
- Polymorphism means "many forms".
- It allows the same method, function, or operator to behave differently depending on the object or data type.

### Types of Polymorphism

#### 1. Method Overriding
- When a child class provides its own implementation of a method inherited from its parent class.

**Example:**
```python
class Animal:
    def sound(self):
        print("Animal makes a sound")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


class Cat(Animal):
    def sound(self):
        print("Cat meows")


d = Dog()
c = Cat()

d.sound()
c.sound()
```

**Output:**
```text
Dog barks
Cat meows
```

#### 2. Duck Typing
- Duck typing is a concept in Python where an object's suitability is determined by the methods and attributes it supports rather than its actual class or type.
- It follows the principle:

  "If it walks like a duck and quacks like a duck, treat it like a duck."

**Example:**
```python
class Dog:
    def sound(self):
        print("Dog barks")


class Cat:
    def sound(self):
        print("Cat meows")


def make_sound(animal):
    animal.sound()


d = Dog()
c = Cat()

make_sound(d)
make_sound(c)
```

**Output:**
```text
Dog barks
Cat meows
```

**Explanation:**
- `make_sound()` does not check whether the object belongs to the `Dog` or `Cat` class.
- It only expects the object to have a `sound()` method.
- Both objects work because they provide the required method.

#### 3. Operator Overloading
- Operator overloading allows operators such as `+`, `-`, `*`, `==` etc. to behave differently for user-defined objects.
- Python implements operator overloading using special methods (magic methods).

**Example:**
```python
class Number:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return self.value + other.value


n1 = Number(10)
n2 = Number(20)

print(n1 + n2)
```

**Output:**
```text
30
```

**Explanation:**
- When we write `n1 + n2`, Python internally calls:
  `n1.__add__(n2)`.
- We define `__add__()` to specify how the `+` operator should work for our objects.

#### 4. Method Overloading
- Method overloading means defining multiple methods with the same name but different numbers or types of parameters.
- Languages like Java support traditional method overloading.
- Python does not support traditional method overloading directly.
- If multiple methods with the same name are defined in a class, the latest definition replaces the previous one.
- We can achieve similar behavior using default arguments, `*args`, or conditional logic.

**Example using default arguments:**
```python
class Calculator:
    def add(self, a, b=0, c=0):
        return a + b + c


obj = Calculator()

print(obj.add(10, 20))
print(obj.add(10, 20, 30))
print(obj.add(10))
```

**Output:**
```text
30
60
10
```

---

# Abstraction
- Abstraction means hiding implementation details and showing only the essential features to the user.
- It focuses on what an object does rather than how it does it.
- In Python, abstraction can be implemented using abstract classes and abstract methods.
- Python provides the `abc` module (Abstract Base Classes) to implement abstraction.

### Abstract Class
- An abstract class is a class that is designed to be inherited by other classes.
- It cannot be instantiated directly if it contains abstract methods that have not been implemented.
- It can contain both abstract and concrete methods.

### Abstract Method
- An abstract method is a method declared in an abstract class but without a complete implementation.
- Child classes are expected to provide its implementation.
- It is created using the `@abstractmethod` decorator.

### `ABC` Module
- `ABC` stands for Abstract Base Class.
- It is provided by Python's built-in `abc` module.
- It is used as a base class for creating abstract classes.

**Example:**
```python
from abc import ABC, abstractmethod

class Animal(ABC):

    @abstractmethod
    def sound(self):
        pass

    def sleep(self):
        print("Animal is sleeping")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


class Cat(Animal):
    def sound(self):
        print("Cat meows")


# a = Animal()  # TypeError: Cannot instantiate abstract class

d = Dog()
c = Cat()

d.sound()
d.sleep()

c.sound()
```

**Output:**
```text
Dog barks
Animal is sleeping
Cat meows
```

**Explanation:**
- `Animal` is an abstract class because it inherits from `ABC` and contains an abstract method.
- `sound()` is an abstract method.
- `sleep()` is a concrete method because it has an implementation.
- `Dog` and `Cat` provide their own implementation of `sound()`.
- We cannot create an object of `Animal` until all its abstract methods are implemented.


# Magic Methods (Dunder Methods)

- Magic methods are special methods in Python that have double underscores before and after their names.
- They are also called Dunder (Double Underscore) methods.
- They allow us to define how objects behave with built-in operations such as printing, comparison, arithmetic, iteration, and object creation.
- Python automatically calls these methods when the corresponding operation is performed.

### Common Magic Methods

| Magic Method | Purpose |
|---|---|
| `__init__()` | Initializes an object's attributes. |
| `__new__()` | Creates and returns a new object. |
| `__str__()` | Defines the user-friendly string representation of an object. |
| `__repr__()` | Defines the developer-oriented representation of an object. |
| `__len__()` | Defines the behavior of `len()`. |
| `__add__()` | Defines the behavior of `+`. |
| `__sub__()` | Defines the behavior of `-`. |
| `__mul__()` | Defines the behavior of `*`. |
| `__eq__()` | Defines the behavior of `==`. |
| `__lt__()` | Defines the behavior of `<`. |
| `__gt__()` | Defines the behavior of `>`. |
| `__contains__()` | Defines the behavior of `in`. |
| `__getitem__()` | Defines indexing using `[]`. |
| `__setitem__()` | Defines assignment using `[]`. |
| `__delitem__()` | Defines deletion using `del obj[key]`. |
| `__iter__()` | Returns an iterator. |
| `__next__()` | Returns the next item from an iterator. |
| `__call__()` | Allows an object to be called like a function. |
| `__del__()` | Called during object finalization. |

### 1. `__str__()` Method
- Defines the readable or user-friendly string representation of an object.
- It is called automatically when we use `print()` or `str()` on an object.

**Example:**
```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"Student Name: {self.name}, Age: {self.age}"


s1 = Student("Khushi", 22)

print(s1)
```

**Output:**
```text
Student Name: Khushi, Age: 22
```

### 2. `__repr__()` Method
- Provides an unambiguous, developer-oriented representation of an object.
- It is called when we use `repr()` or when an object is inspected in certain interactive contexts.
- Ideally, its output should help developers understand or recreate the object.

**Example:**
```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __repr__(self):
        return f"Student('{self.name}', {self.age})"


s1 = Student("Khushi", 22)

print(repr(s1))
```

**Output:**
```text
Student('Khushi', 22)
```

### 3. `__len__()` Method
- Defines how the built-in `len()` function works for an object.
- It should return a non-negative integer.

**Example:**
```python
class ShoppingCart:
    def __init__(self, items):
        self.items = items

    def __len__(self):
        return len(self.items)


cart = ShoppingCart(["Laptop", "Mouse", "Keyboard"])

print(len(cart))
```

**Output:**
```text
3
```

### 4. `__eq__()` Method
- Defines how two objects are compared using the `==` operator.

**Example:**
```python
class Student:
    def __init__(self, name):
        self.name = name

    def __eq__(self, other):
        return self.name == other.name


s1 = Student("Khushi")
s2 = Student("Khushi")

print(s1 == s2)
```

**Output:**
```text
True
```

### 5. `__call__()` Method
- Allows an object to be called like a normal function.
- When we use parentheses with an object, Python internally calls its `__call__()` method.

**Example:**
```python
class Greeting:
    def __call__(self, name):
        print("Hello", name)


g = Greeting()
g("Khushi")
```

**Output:**
```text
Hello Khushi
```

### 6. `__getitem__()` Method
- Defines how an object behaves when we access an element using square brackets `[]`.

**Example:**
```python
class MyList:
    def __init__(self, items):
        self.items = items

    def __getitem__(self, index):
        return self.items[index]


obj = MyList([10, 20, 30])

print(obj[0])
print(obj[2])
```

**Output:**
```text
10
30
```

---

# Object Relationships

In OOP, classes and objects can be related to one another in different ways.

### 1. Association
- Association represents a relationship between two independent classes.
- Both objects can exist independently of each other.
- One object uses or interacts with another object.

**Example:**
```python
class Teacher:
    def teach(self):
        print("Teacher is teaching")


class Student:
    def learn(self):
        print("Student is learning")


teacher = Teacher()
student = Student()

# Teacher and Student are associated through interaction.
teacher.teach()
student.learn()
```

### 2. Aggregation
- Aggregation is a special type of association that represents a HAS-A relationship.
- One class contains a reference to another class's object.
- Both objects can exist independently.
- If the container object is destroyed, the contained object can still exist.

**Example:**
```python
class Department:
    def __init__(self, name):
        self.name = name


class College:
    def __init__(self, department):
        self.department = department


d1 = Department("Computer Science")

c1 = College(d1)

print(c1.department.name)

del c1

print(d1.name)
```

**Output:**
```text
Computer Science
Computer Science
```

**Explanation:**
- `College` contains a reference to the `Department` object.
- Even after deleting `c1`, `d1` still refers to the department.
- Therefore, the department continues to exist.

### 3. Composition
- Composition is a stronger form of association that represents a HAS-A relationship.
- One class owns or manages the objects of another class as its components.
- The contained object's lifecycle is generally managed by the containing object.

**Example:**
```python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self):
        self.engine = Engine()

    def start_car(self):
        self.engine.start()
        print("Car started")


car = Car()
car.start_car()
```

**Output:**
```text
Engine started
Car started
```
---

# Important OOP Concepts

### 1. Dynamic Binding
- Dynamic binding means that the method to be executed is determined at runtime.
- In Python, the method implementation is generally selected based on the actual object's type.

**Example:**
```python
class Animal:
    def sound(self):
        print("Animal sound")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


class Cat(Animal):
    def sound(self):
        print("Cat meows")


def make_sound(animal):
    animal.sound()


make_sound(Dog())
make_sound(Cat())
```

**Output:**
```text
Dog barks
Cat meows
```

### 2. Early Binding vs Late Binding

| Early Binding | Late Binding |
|---|---|
| Method or function selection is determined before runtime. | Method selection is determined at runtime. |
| Commonly associated with static/compile-time binding. | Commonly associated with dynamic/runtime binding. |
| Python is generally dynamically bound. | Python supports late binding for method calls. |

**Note:** Python is a dynamically typed language, and its method dispatch is generally dynamic.


# Object Copying

- Object copying means creating a new object using the data of an existing object.
- Python provides the built-in `copy` module to perform shallow and deep copying.

### 1. Shallow Copy
- Creates a new outer object.
- Copies references to nested objects rather than creating copies of those nested objects.
- Changes to nested mutable objects can affect both the original and copied objects.

**Example:**
```python
import copy

original = [[1, 2], [3, 4]]

shallow = copy.copy(original)

shallow[0][0] = 100

print(original)
print(shallow)
```

**Output:**
```text
[[100, 2], [3, 4]]
[[100, 2], [3, 4]]
```

**Explanation:**
- A new outer list is created.
- The inner lists are shared between the original and copied lists.
- Therefore, modifying an inner list affects both.

### 2. Deep Copy
- Creates a new object and recursively copies nested objects.
- Changes to nested mutable objects in the copied object do not affect the original object.

**Example:**
```python
import copy

original = [[1, 2], [3, 4]]

deep = copy.deepcopy(original)

deep[0][0] = 100

print(original)
print(deep)
```

**Output:**
```text
[[1, 2], [3, 4]]
[[100, 2], [3, 4]]
```

**Important:** Both shallow and deep copying can be customized using `__copy__()` and `__deepcopy__()`.

---

# Nested Classes

- A nested class is a class defined inside another class.
- It is used to logically group related classes together.
- The inner class can be accessed using the outer class name.

**Example:**
```python
class Employee:

    def __init__(self, name):
        self.name = name

    class Department:
        def __init__(self, dept_name):
            self.dept_name = dept_name


e1 = Employee("Rahul")

d1 = Employee.Department("IT")

print(e1.name)
print(d1.dept_name)
```

**Output:**
```text
Rahul
IT
```

**Important:**
- A nested class does not automatically receive an instance of the outer class.
- It is simply defined within the namespace of the outer class.

---

# Object Creation and `__new__()`

### `__new__()` Method
- `__new__()` is a special method responsible for creating and returning a new object.
- It is called before `__init__()`.
- It is a static method in behavior and receives `cls` as its first argument.
- It is mainly overridden when customizing object creation.

### Difference between `__new__()` and `__init__()`

| `__new__()` | `__init__()` |
|---|---|
| Creates and returns a new object. | Initializes an already-created object. |
| Called first. | Called after `__new__()`. |
| Receives `cls` as its first argument. | Receives `self` as its first argument. |
| Must return an instance (usually of the class). | Must return `None`. |

**Example:**
```python
class Student:

    def __new__(cls):
        print("Object Created")
        return super().__new__(cls)

    def __init__(self):
        print("Object Initialized")


s1 = Student()
```

**Output:**
```text
Object Created
Object Initialized
```

**Explanation:**
1. `__new__()` creates the object.
2. The newly created object is returned.
3. `__init__()` initializes the object's attributes.

---

# Class and Instance Attributes

### Attribute Lookup
- When we access an attribute using an object, Python first checks the object's instance attributes.
- If the attribute is not found, Python searches the class and its parent classes.

**Example:**
```python
class Student:
    school = "ABC School"

    def __init__(self, name):
        self.name = name


s1 = Student("Khushi")
s2 = Student("Rahul")

print(s1.school)
print(s2.school)

s1.school = "XYZ School"

print(s1.school)
print(s2.school)
print(Student.school)
```

**Output:**
```text
ABC School
ABC School
XYZ School
ABC School
ABC School
```

**Explanation:**
- Initially, both objects access the class variable `school`.
- When `s1.school` is assigned a new value, Python creates an instance attribute for `s1`.
- The original class variable remains unchanged.
- `s2` continues to access the class variable.

### `__dict__`
- `__dict__` stores an object's or class's attribute namespace in a dictionary when available.
- It helps inspect attributes.

**Example:**
```python
class Student:
    school = "ABC School"

    def __init__(self, name, age):
        self.name = name
        self.age = age


s1 = Student("Khushi", 22)

print(s1.__dict__)
print(Student.__dict__)
```

**Output (object):**
```text
{'name': 'Khushi', 'age': 22}
```

**Note:** Class-level `__dict__` is a mapping proxy, not an ordinary dictionary. Objects using `__slots__` may not have an instance `__dict__`.

---

# `__slots__`

- `__slots__` is used to explicitly declare the instance attributes allowed on objects of a class.
- It can reduce memory usage when creating a large number of objects.
- It can prevent the automatic creation of an instance `__dict__`, unless `__dict__` is explicitly included.

**Example:**
```python
class Student:
    __slots__ = ("name", "age")

    def __init__(self, name, age):
        self.name = name
        self.age = age


s1 = Student("Khushi", 22)

print(s1.name)
print(s1.age)

# s1.marks = 90  # AttributeError
```

**Output:**
```text
Khushi
22
```

**Explanation:**
- The class allows only `name` and `age` as its declared instance attributes.
- Adding another attribute such as `marks` raises an `AttributeError`.

---

# Dataclasses

- A dataclass is a class designed mainly to store data.
- Python provides the `dataclasses` module to reduce boilerplate code.
- The `@dataclass` decorator automatically generates commonly required methods such as `__init__()`, `__repr__()`, and `__eq__()` by default.

**Example:**
```python
from dataclasses import dataclass


@dataclass
class Student:
    name: str
    age: int
    marks: int


s1 = Student("Khushi", 22, 95)

print(s1)
print(s1.name)
```

**Output:**
```text
Student(name='Khushi', age=22, marks=95)
Khushi
```

**Note:** Type annotations in dataclasses do not automatically enforce runtime type checking.

---
