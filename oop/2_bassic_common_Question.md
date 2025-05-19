#  Python OOP – Commonly Asked Interview Questions and Answers

## 🔐 Basics of Object-Oriented Programming

1. **What is Object-Oriented Programming (OOP)?**
   OOP is a way of programming that uses objects and classes to model real-world things, making code reusable, organized, and easy to manage.

2. **How is everything an object in Python?**
   In Python, all data types (int, str, list, functions, etc.) are implemented as classes. Therefore, every variable or function you use is actually an object of some class.

3. **What is a class in Python?**
   A class is a blueprint for creating objects. It defines attributes (variables) and behaviors (methods) common to all objects of that type.

4. **What is an object? How is it different from a class?**
   An object is an instance of a class. While a class defines the structure and behavior, the object holds actual data and operates based on the class definition.

5. **How do you create a class and instantiate objects in Python?**

```python
class Car:
    def __init__(self, model):
        self.model = model

my_car = Car("Toyota") # instance
```

---

## 🧱 Class & Object Related Questions

6. **What are the key components of a class in Python?**

* Attributes (variables)
* Methods (functions)
* Constructor (`__init__`)
* Self keyword

7. **What is the purpose of the `__init__()` method?**
   It is a special method called automatically when a class object is created. It initializes the object with default or passed values.

8. **Why is `self` used in Python class methods?**
   `self` refers to the current instance of the class and is used to access variables and methods associated with the object.

9. **Can you create multiple objects from the same class?**
   Yes, each object can have its own unique data even if they share the same class structure.

10. **Can you define default values for object attributes in a class?**
    Yes, using default arguments in the constructor.

```python
def __init__(self, name="Guest"):
    self.name = name
```

---

## 🧠 Method and Variable Types

11. **What is the difference between instance variables and class variables?**

* Instance variables are specific to each object.
* Class variables are shared across all objects of the class.

12. **What are instance methods, class methods, and static methods?**

* Instance methods operate on object data using `self`.
* Class methods use `@classmethod` and `cls`, and affect the class itself.
* Static methods use `@staticmethod` and do not access object or class data.

13. **How do you define a private variable or method in Python?**
    Prefix the name with double underscores `__`.

```python
self.__balance = 100
```

14. **How can you access private variables from outside the class?**
    Using name mangling: `_ClassName__variableName` (not recommended).

---

## 🧬 Inheritance & Polymorphism

15. **What is inheritance in Python?**
    A mechanism to derive a new class from an existing class, inheriting attributes and methods.

16. **What are the types of inheritance supported in Python?**
    Single, Multiple, Multilevel, Hierarchical, and Hybrid inheritance.

17. **What is method overriding?**
    Defining a method in the child class with the same name as in the parent class to customize behavior.

18. **What is the `super()` function used for?**
    Used to call a method from the parent class, especially constructors.

19. **Can you override a constructor in a derived class?**
    Yes. You can also call the parent constructor using `super().__init__()`.

---

## 🔐 Encapsulation & Abstraction

20. **What is encapsulation? How is it implemented in Python?**
    Encapsulation is the bundling of data and methods into a single unit (class) and restricting access using private/protected variables.

21. **What is data hiding? How do you hide data in Python classes?**
    Using name mangling with double underscores: `__var`.

22. **What is abstraction and how is it different from encapsulation?**

* Abstraction hides complexity by exposing only essential details.
* Encapsulation hides the internal state using access modifiers.

23. **Does Python support abstract classes? If yes, how?**
    Yes, using the `abc` module and `ABC` base class.

```python
from abc import ABC, abstractmethod
class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
```

---

## 🔄 Difference-Based Questions

24. **Difference between `__init__` and `__new__`?**

* `__new__` creates a new instance; `__init__` initializes it.

25. **Difference between class method and static method?**

* Class method uses `@classmethod` and has access to `cls`.
* Static method uses `@staticmethod` and has no access to either `self` or `cls`.

26. **Difference between procedural programming and object-oriented programming?**

* Procedural: Based on functions and procedures.
* OOP: Based on objects and classes.

27. **Difference between `self.variable` and `variable`?**

* `self.variable`: instance variable
* `variable`: local variable inside a method

28. **Difference between method and function in Python?**

* Method is associated with objects/classes.
* Function is independent and can exist outside a class.

---

## ⚙️ Advanced & Practical

29. **What are magic methods? Can you name a few?**
    Special methods with double underscores used to define object behavior. Examples: `__init__`, `__str__`, `__repr__`, `__add__`, `__len__`.

30. **What does `__str__()` and `__repr__()` do?**

* `__str__()` is used by `print()` and should return a readable string.
* `__repr__()` is for developers and should return a detailed string.

31. **What happens if you don't use `self` in a class method?**
    Python will raise an error because the method cannot access instance attributes.

32. **How do you implement encapsulation using name mangling in Python?**
    Prefix variable names with double underscores `__`. Python changes their names internally to `_ClassName__var`.

33. **Can you write a class to represent a real-world entity like a Bank Account or a Dish?**

```python
class Dish:
    def __init__(self, name, spice_level, garnish):
        self.name = name
        self.spice_level = spice_level
        self.garnish = garnish

    def serve(self):
        print(f"Serving {self.name} with {self.spice_level} spice and {self.garnish} garnish.")
```

34. **How would you design a class to ensure balance can’t go negative in a bank account?**
    Use private attributes and conditionally allow withdrawal:

```python
class Account:
    def __init__(self, balance):
        self.__balance = balance

    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Insufficient balance")
```

---


