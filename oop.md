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

### Instance method
- An instance method works with the data of an individual object.
- It takes `self` as its first parameter

### class method
- A class method works with the class rather than a particular object.
- It uses the `@classmethod` decorator and takes `cls` as its first parameter.

### static method
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

### Non-Parameterized (default) constructor
- if don't define `__init__` at all, python automatically provides default do-nothing constructor behind the scences.

### Parameterized constructor
- Takes parameters to intialize object at creation time.

### Copy constructor
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
