# SOLID Principles

## What are SOLID Principles
- SOLID is a set of five design principles in Object Oreinted Programming.
- These principles help us write clean, maintainable, reusable and flixible code.
- They make software easier to modify, tes, and extend.

| Letter | Principle | Meaning |
|---|---|---|
| S | Single Responsibility Principle | One class, one responsibility |
| O | Open/Closed Principle | Open for extension, closed for modification |
| L | Liskov Substitution Principle | Child classes should replace parent classes |
| I | Interface Segregation Principle | Don't force classes to implement unnecessary methods |
| D | Dependency Inversion Principle | Depend on abstractions, not concrete classes |

## 1. Single Responsibility Principle
- A class should have only one responsiblity or one reason to change.
```bash
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def calculate_average(self):
        return sum(self.marks) / len(self.marks)


class StudentRepository:
    def save(self, student):
        with open("student.txt", "w") as file:
            file.write(student.name)
```

## 2. Open/Closed Principle
- Software entities(classes, functions, modules) should be open for extension and closed for modification.

```bash
class Payment:
    def pay(self, amount):
        pass


class UPI(Payment):
    def pay(self, amount):
        print(f"Paid {amount} using UPI")


class Card(Payment):
    def pay(self, amount):
        print(f"Paid {amount} using Card")


class Cash(Payment):
    def pay(self, amount):
        print(f"Paid {amount} using Cash")
```
**usage**:
```bash
def process_payment(payment, amount):
    payment.pay(amount)


process_payment(UPI(), 1000)
process_payment(Card(), 2000)
process_payment(Cash(), 500)
```

## 3. Liskov Substitution Principle (LSP)
- Objects of a child class should be replaceable with objects of their parent class without breaking the program's expected behavior.

```bash
class Bird:
    def eat(self):
        print("Bird is eating")


class FlyingBird(Bird):
    def fly(self):
        print("Bird is flying")


class Sparrow(FlyingBird):
    pass


class Penguin(Bird):
    def swim(self):
        print("Penguin is swimming")

```
**usage**:
```bash
def make_it_fly(bird):
    bird.fly()


make_it_fly(Sparrow())
```

## 4. Interface Segregation Principle (ISP)
- A class should not be forced to implement methods it does not use.
```bash
from abc import ABC, abstractmethod


class Workable(ABC):

    @abstractmethod
    def work(self):
        pass


class Eatable(ABC):

    @abstractmethod
    def eat(self):
        pass


class Human(Workable, Eatable):

    def work(self):
        print("Human is working")

    def eat(self):
        print("Human is eating")


class Robot(Workable):

    def work(self):
        print("Robot is working")
```

## 5. Dependency Inversion Principle (DIP)
- High-level modules contain business logic.
- Low-level modules handle implementation details.
- Both should communicate through abstractions rather than depending directly on each other.

```bash
from abc import ABC, abstractmethod


class MessageService(ABC):

    @abstractmethod
    def send(self, message):
        pass


class EmailService(MessageService):

    def send(self, message):
        print("Sending email:", message)


class SMSService(MessageService):

    def send(self, message):
        print("Sending SMS:", message)


class Notification:
    def __init__(self, service):
        self.service = service

    def send_notification(self, message):
        self.service.send(message)
```

**usage**:
```bash
email = EmailService()
sms = SMSService()

notification1 = Notification(email)
notification1.send_notification("Hello!")

notification2 = Notification(sms)
notification2.send_notification("Hello!")
```
