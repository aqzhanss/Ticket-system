
__Developed by:__

230317078 Akzhan Nartaikyzy, 230317072 Alibi Yeltay, 230317085 Arystan Sultanbek, 230317069 Zhanerke Satin, 230317052 Madina Abutalipkyzy

# 🎟️SDU Ticket System — OOP Project
This project simulates a ticketing platform for SDU university events, where students and faculty can purchase or access tickets for events organized by student clubs. It demonstrates full use of Object-Oriented Programming (OOP) principles in Python.

__How to Run the Project__

Prerequisites:
- Python 3.x installed on your system. ✅
- A code editor (VS Code, PyCharm, Jupyter Notebook).
_Steps to Run:_

- 1️⃣ Clone or download the project files. 
- 2️⃣ Open the terminal or command prompt in the project directory. 
- 3️⃣ Run the script using: `project_oop(3).py`
- 4️⃣ Observe the output demonstrating different OOP principles.

## 1. Class

Core entities like _User, Student, Teacher, Club, Event, VIPMember, StandardClub and TicketSystem_ are implemented as classes.

```bash
class User(ABC):
    ...

class Student(User):
    ...

class Teacher(User):
    ...

class Club(ABC):
    ...

class StandardClub(Club):
    ...

class Event(Club):
    ...

class VIPMember(Student, StandardClub):
    ...

class TicketSystem(Event):
    ...
```
## 2. Inheritance

Child classes inherit attributes/methods from parent classes.
```bash
# Student inherits from User:

class Student(User):
    def __init__(self, f_name, l_name, id, email, role, password, balance, year):
        super().__init__(f_name, l_name, id, email, role, password, balance)  # Calls User's constructor
        self.year = year

```
```bash
# Teacher inherits from User

class Teacher(User):  
    def __init__(self, f_name, l_name, ID, email, role, password, balance, department):
        super().__init__(f_name, l_name, ID, email, role, password, balance)  # Calls User's constructor
        self.department = department
```
```bash
# StandardClub inherits from Club

class StandardClub(Club):  
    def get_details(self):
        return f"Club: {self.club_name}, Head: {self.head_of_Club}"
```
```bash
# Event inherits from Club

class Event(Club): 
    def __init__(self, club_name, description, head_of_Club, event_name, date, location, ticket_price):
        super().__init__(club_name, description, head_of_Club)  # Calls Club's constructor
        self.event_name = event_name

```
```bash
# TicketSystem inherits from Event

class TicketSystem(Event):  # Inherits from Event
    def __init__(self, club_name, description, head_of_Club, event_name, date, location, ticket_price):
        super().__init__(club_name, description, head_of_Club, event_name, date, location, ticket_price)  # Calls Event's constructor
        self.tickets_sold = 0
```

## 3. Multiple Inheritance
A class inherits from more than one parent class.
```bash
class VIPMember(Student, StandardClub):  # Multiple Inheritance
    def __init__(self, f_name, l_name, ID, email, role, password, balance, year, club_name, activation_date):
        Student.__init__(self, f_name, l_name, ID, email, role, password, balance, year)  # Parent 1
        StandardClub.__init__(self, club_name, description=None, head_of_Club=None)      # Parent 2
        self.activation_date = activation_date
```
## 4. Multilevel Inheritance
Inheritance through a chain of classes (parent → child → grandchild)
```bash
class Club(ABC):  # Base Class
    def __init__(self, club_name, description, head_of_Club):
        self.club_name = club_name

class Event(Club):  # Inherits from Club
    def __init__(self, club_name, description, head_of_Club, event_name, date, location, ticket_price):
        super().__init__(club_name, description, head_of_Club)  # Calls Club
        self.event_name = event_name

class TicketSystem(Event):  # Inherits from Event (which inherits from Club)
    def __init__(self, club_name, description, head_of_Club, event_name, date, location, ticket_price):
        super().__init__(club_name, description, head_of_Club, event_name, date, location, ticket_price)  # Calls Event
        self.tickets_sold = 0
```
## 5. Object Creation and Method Calls
```bash
student1 = Student("Alibi", "Yeltay", 230317072, "alibieltai200531@gmail.com", "Student", "Ystyq23", 1500, 2)  # Object Creation
student2 = Student("Madina", "Abutalipkyzy", 230317072, "MadinAbutalip@gmail.com", "Student", "Madina2006", 2000, 2)

print(student1.get_details())  # Method Call
```
```bash
teacher1 = Teacher("Akniyet", "Issain", 190317024, "AkniyetIssain@gmail.com", "Teacher", "Physgram", 2000, "Physics")
teacher2 = Teacher("Nazarali", "Aitzhanov", 170317012, "NazaraliAitzhanov@gmail.com", "Teacher", "Foreverphys", 2500, "Physics")

print(teacher2.get_details())  # Method Call

```
```bash
club1 = StandardClub("Oyan", "Theatre", "Bakbergen")
club2 = StandardClub("Language", "Teaching and learning", "Akbota")

print(club1.get_details())  # Method Call

```
```bash
event1 = TicketSystem("Oyan", "Performance about...", "Bakbergen", "The poor rich people", "2025-04-10", "Blue Hall", 600)
event2 = TicketSystem("Language", "How to learn language efficiently?", "Akbota", "L-luxury style of learning", "2025-04-11", "Mini Red Hall", 500)

print(event1.get_details())  # Method Call

```
## 6. Polymorphism
Polymorphism allows methods in different classes to share the same name but have different implementations. This project demonstrates both method `overriding` and method `overloading`.

__1. Method Overriding__

The `get_details()` method is defined as an abstract method in the parent class User and then overridden in the `Student`, `Teacher`, and `VIPMember` classes, each with a different implementation.


```bash
from abc import ABC, abstractmethod
class User(ABC):  # Abstract class
    def __init__(self, f_name, l_name, ID, email, role, password, balance):
        self.f_name = f_name
        self.l_name = l_name
        self.email = email
        self.role = role
        self._password = None
        self.password = password
        self.balance = balance
        self.ID = ID

    @abstractmethod
    def get_details(self):
        pass  # Abstract method

class Student(User):
    def __init__(self, f_name, l_name, ID, email, role, password, balance, year):
        super().__init__(f_name, l_name, ID, email, role, password, balance)
        self.year = year

    def get_details(self):  # Overriding method
        return f"Student: {self.f_name} {self.l_name}, ID: {self.ID}, Balance: $ {self.balance}, Year: {self.year}"

class Teacher(User):
    def __init__(self, f_name, l_name, ID, email, role, password, balance, department):
        super().__init__(f_name, l_name, ID, email, role, password, balance)
        self.department = department
        self.VIP_access = True

    def get_details(self):  # Overriding method
        return f"Teacher: {self.f_name} {self.l_name}, ID: {self.ID}, Balance: $ {self.balance}, Access: {self.VIP_access}"     
```
Both `Student` and `Teacher` override`get_details()`, but each provides different details.

__2. Operator Overloading (__eq__() for Comparing Objects)__

The `User` class now includes a custom `__eq__()` method, which allows users to be compared based on their ID.
```bash
class User(ABC):
    def __eq__(self, other):
        if isinstance(other, User):
            return self.ID == other.ID
        return False
```
Now, instead of comparing object memory addresses, we compare users based on their unique ID.

Example Usage:
```bash
student1 = Student("Alibi", "Yeltay", 230317072, "email@example.com", "Student", "Pass123", 1500, 2)
student2 = Student("Madina", "Abutalipkyzy", 230317072, "email@example.com", "Student", "Pass456", 2000, 2)
print(student1 == student2)  # True (because they have the same ID)
```
Even though `student1` and `student2` are different objects, they are treated as equal if their ID matches.



## 7. Encapsulation
Encapsulation is the principle of restricting direct access to an object's data and modifying it through controlled methods. This project demonstrates encapsulation using private attributes, getter and setter methods, and property decorators.

The User class protects the _password attribute using the `@property`and  `@password.setter` decorators.
```bash
class User(ABC):
    def __init__(self, f_name, l_name, ID, email, role, password, balance):
        self.f_name = f_name
        self.l_name = l_name
        self.email = email
        self.role = role
        self._password = None  # Private attribute
        self.password = password  # Uses setter
        self.balance = balance
        self.ID = ID

    @property
    def password(self):  # Getter method
        return "*" * len(self._password)

    @password.setter
    def password(self, new_password):  # Setter method with validation
        if len(new_password) < 6 or len(new_password) > 12:
            raise ValueError("Password must be between 6 and 12 characters long!")
        self._password = new_password

    @password.deleter
    def password(self):  # Prevents password deletion
        raise AttributeError("Password cannot be deleted")
```
This ensures that:

- The password is stored securely.
- It can only be accessed in a masked format (******).
- It cannot be set to an invalid length.
- It cannot be deleted accidentally.

__Protected Attributes__

The `_revenue` attribute in `TicketSystem` is protected, meaning it should not be accessed directly. Instead, a method is used to retrieve its value.
```bash
class TicketSystem(Event):
    def __init__(self, club_name, description, head_of_Club, event_name, date, location, ticket_price):
        super().__init__(club_name, description, head_of_Club, event_name, date, location, ticket_price)
        self.tickets_sold = 0
        self._revenue = 0  # Protected attribute

    def revenue(self):  # Encapsulated method to access revenue
        return self._revenue
```
Encapsulation ensures that `_revenue` is modified only through defined methods, preventing accidental changes.

## 8. Error Handling
Error handling ensures that the program runs smoothly by catching and managing exceptions instead of crashing. This project uses  `try-except` blocks to handle different types of errors, such as invalid input, division by zero, and incorrect object attributes.

__Handling Invalid Password Length (ValueError)__

In the `User` class, the `password` setter prevents users from setting passwords that are too short or too long. If an invalid password is entered, a `ValueError` is raised.
```bash
@password.setter
def password(self, new_password):
    try:
        if len(new_password) < 6 or len(new_password) > 12:
            raise ValueError("Password must be between 6 and 12 characters long!")
        self._password = new_password
    except ValueError as e:
        print(f"Error: {e}")
```
If the password is invalid, an error message is displayed instead of crashing the program.

__Handling Division by Zero (ZeroDivisionError)__

The `calculate_budget_per_event()` method prevents division by zero when calculating the budget per event.
```bash
@staticmethod
def calculate_budget_per_event():
    try:
        return int(Club.total_budget / Club.number_of_events)
    except ZeroDivisionError:
        print("It's impossible to divide by zero")
```

If there are no events, the program will print a message instead of crashing.

__Handling Missing Attributes (AttributeError)__

When purchasing a ticket, an `AttributeError` might occur if the user object is missing required attributes. The `try-except` block prevents the program from breaking.
```bash
def purchase_ticket(self, user):
    try:
        if user.ID in self.attendees:
            print(f"❌ (ID: {user.ID}) is already registered for '{self.event_name}'.")
            return
        if len(self.attendees) < self.capacity:
            self.attendees.append(user.ID)
            print(f"🎟️ {user.f_name} successfully bought a ticket for {self.event_name}.")
    except AttributeError as e:
        print(f"⚠️ Error: Missing required attribute in user object - {e}")
```
If `user.ID` or `user.f_name` is missing, the program prints an error instead of crashing.

## 9. Decoration

Python decorators allow modifying the behavior of functions or methods without changing their structure. This project uses `@property`,`@staticmethod`, and `@classmethod` decorators to enhance code readability and functionality.

__Using @property__

The `password` attribute in `User` is protected using `@property`, ensuring that it cannot be accessed directly.
```bash
class User(ABC):
    def __init__(self, f_name, l_name, ID, email, role, password, balance):
        self.f_name = f_name
        self.l_name = l_name
        self.email = email
        self.role = role
        self._password = None  # Private attribute
        self.password = password  # Uses setter
        self.balance = balance
        self.ID = ID

    @property
    def password(self):  # Getter method
        return "*" * len(self._password)

    @password.setter
    def password(self, new_password):  # Setter method with validation
        if len(new_password) < 6 or len(new_password) > 12:
            raise ValueError("Password must be between 6 and 12 characters long!")
        self._password = new_password
```

__Using @classmethod__

The `@classmethod` decorator allows modifying class variables without needing an instance.
```bash
class Club(ABC):
    total_budget = 50000  # Shared across all instances

    @classmethod
    def update_budget(cls, new_budget):
        cls.total_budget += new_budget
```
```bash
@classmethod
    def add_revenue_to_budget(cls, amount): # Adds ticket revenue to the SDU life's budget
        """ Transfers ticket revenue to the club's budget """
        Club.update_budget(amount)
        print(f"💰 {amount} added to the SDU life's budget. New total budget: {Club.total_budget}")
```
Using `@classmethod`, we can update the club’s budget at the class level, affecting all instances.

__Using @staticmethod__

Static methods do not modify class or instance attributes but provide useful functions.
```bash
class Club(ABC):
    @staticmethod
    def calculate_budget_per_event():
        try:
            return int(Club.total_budget / Club.number_of_events)
        except ZeroDivisionError:
            print("It's impossible to divide by zero")
```
The `@staticmethod` decorator is used here because this function does not depend on any instance-specific data.

## 10. Super Method
The `super()` function is used to call methods from a parent class in derived classes. This ensures that child classes correctly inherit and extend the behavior of their parent classes without duplicating code.

__Using super() in Constructor Overriding__

In the `Student` and `Teacher` classes, `super().__init__()` is used to call the constructor of the parent class `User`, avoiding redundant code.
```bash
class Student(User):
    def __init__(self, f_name, l_name, ID, email, role, password, balance, year):
        super().__init__(f_name, l_name, ID, email, role, password, balance)  # Calls User's constructor
        self.year = year
```
This ensures that `Student`inherits all attributes from `User` while adding a new attribute year.

__Using super() in Multiple Inheritance__

In the `VIPMember` class, which inherits from both `Student` and `StandardClub`, `super()` helps call methods from multiple parent classes.
```bash
class VIPMember(Student, StandardClub):
    def __init__(self, f_name, l_name, ID, email, role, password, balance, year, club_name, activation_date):
        Student.__init__(self, f_name, l_name, ID, email, role, password, balance, year)  # Calls Student constructor
        StandardClub.__init__(self, club_name, description=None, head_of_Club=None)  # Calls StandardClub constructor
        self.activation_date = activation_date
```
This ensures that `VIPMember` properly initializes attributes from both `Student` and `StandardClub`.

__Using super() to Call Parent Methods__

In the `TicketSystem` class, `super()` is used to call the parent class `Event` constructor.
```bash
class TicketSystem(Event):
    def __init__(self, club_name, description, head_of_Club, event_name, date, location, ticket_price):
        super().__init__(club_name, description, head_of_Club, event_name, date, location, ticket_price)  # Calls Event constructor
        self.tickets_sold = 0
        self._revenue = 0
```
This prevents code duplication and ensures that the `Event` class handles its own initialization.

## 11. Abstraction

Abstraction is the principle of hiding implementation details and only exposing essential functionalities. In Python, abstraction is achieved using the `ABC` module (abc) to define abstract classes and abstract methods that must be implemented in child classes.

__Using Abstract Classes (ABC module)__

In this project, the `User` and `Club` classes are abstract classes, meaning they cannot be instantiated directly. They define a structure that all subclasses must follow.
```bash
from abc import ABC, abstractmethod

class User(ABC):  # Abstract class
    def __init__(self, f_name, l_name, ID, email, role, password, balance):
        self.f_name = f_name
        self.l_name = l_name
        self.email = email
        self.role = role
        self._password = None
        self.password = password
        self.balance = balance
        self.ID = ID

    @abstractmethod
    def get_details(self):  # Abstract method
        pass  # Must be implemented in subclasses
```
This ensures that every subclass (`Student, Teacher`) implements `get_details()`.

__Implementing Abstract Methods__

Since `User` is abstract, any class that inherits from it must implement `get_details()`.
```bash
class Student(User):
    def __init__(self, f_name, l_name, ID, email, role, password, balance, year):
        super().__init__(f_name, l_name, ID, email, role, password, balance)
        self.year = year

    def get_details(self):  # Implementation of abstract method
        return f"Student: {self.f_name} {self.l_name}, ID: {self.ID}, Balance: $ {self.balance}, Year: {self.year}"
```
If `Student` does not implement `get_details()`, Python will raise an error.

__Abstract Class for Clubs (Club class)__
The `Club` class is also abstract, ensuring that every club type implements `get_details()`.
```bash
class Club(ABC):
    def __init__(self, club_name, description, head_of_Club):
        self.club_name = club_name
        self.description = description
        self.head_of_Club = head_of_Club

    @abstractmethod
    def get_details(self):  # Abstract method
        pass
```
Now, any subclass (e.g., `StandardClub`) must implement `get_details()`.
```bash
class StandardClub(Club):
    def get_details(self):  # Must be implemented
        return f"Club: {self.club_name}, Head: {self.head_of_Club}, Description: {self.description}"
```
## Examples input/output for the program
Input:
```bash
event1.purchase_ticket(teacher1)
event2.purchase_ticket(teacher2)

event1.purchase_ticket(student1)
event2.purchase_ticket(student2)
event1.purchase_ticket(student2)

event1.purchase_ticket(vip_member1)
event2.purchase_ticket(vip_member2)#All these purchase_ticket methods implement the main idea to buy a ticket

Club.update_budget(50000)#adding money to total budget

print(club1.get_details())  # Club1 details
print(event1.get_details())

print(club2.get_details())  # Club2 details
print(event2.get_details())

print(f'Oyan has revenue from event: {event1.revenue()}')#each club has own revenue according to price of the event
print(f'Language has revenue from event: {event2.revenue()}')

event1.refund_ticket(student1)#refunding ticket in this way our balance remains unchanged
print(student1.balance)

event2.refund_ticket(teacher2)#but the teacher's balance isn't touched totally
print(Club.calculate_budget_per_event())
```
Output:
```bash
✅ Akniyet gets FREE entry to The poor rich people!
✅ Nazarali gets FREE entry to L-luxury style of learning!
💰 600 added to the SDU life's budget. New total budget: 50600
🎟 Alibi successfully bought a ticket for The poor rich people.
💰 500 added to the SDU life's budget. New total budget: 51100
🎟 Madina successfully bought a ticket for L-luxury style of learning.
💰 600 added to the SDU life's budget. New total budget: 51700
🎟 Madina successfully bought a ticket for The poor rich people.
❌  (ID: 230317069) is already registered for 'The poor rich people'.
❌ Sorry, L-luxury style of learning at Mini Red Hall is sold out! 
Oyan has revenue from event: 1200
Language has revenue from event: 500
🔄 Alibi has canceled their ticket for The poor rich people. Refund issued.
1500
🔄 Nazarali has canceled their ticket for L-luxury style of learning. No refund needed.
50550
False
```
__Conclusion__

The SDU Ticket System is a fully functional and object-oriented ticketing platform designed specifically for university events. It allows students, teachers, and VIP members to seamlessly purchase, manage, and refund tickets, while clubs can organize events and track budgets effectively.

This project can serve as the foundation for building a real web-based or mobile application for managing university events and streamlining campus life.