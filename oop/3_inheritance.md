# 📚 INHERITANCE 

Inheritance allows a class (**child/subclass**) to acquire properties and behaviors (methods and attributes) from another class (**parent/superclass**). It helps with **code reuse** and **logical hierarchy**.

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):  # Dog inherits from Animal
    pass

dog = Dog()
dog.speak()  # Output: "Animal speaks"
```

### 🧠🔗 What types of inheritance are there?

| Type         | Description                         |
| ------------ | ----------------------------------- |
| Single       | One child inherits one parent       |
| Multilevel   | Chain of inheritance                |
| Hierarchical | Multiple children from one parent   |
| Multiple     | One child inherits multiple parents |
| Hybrid       | Combination of above                |

```python
class A:
    def method(self):
        print("A")

class B(A):
    pass

class C(B):
    pass

c = C()
c.method()  # Output: A
```

### ❓ How do I know if I should use inheritance?

Ask: "**Is \[Child] a \[Parent]?**"
If yes, inheritance is likely valid.

<details><summary>📌 Example</summary>
```python
class Vehicle:
    def move(self):
        print("Moving...")

class Car(Vehicle):  # ✅ Car is a Vehicle
    pass

my_car = Car()
my_car.move()
```
</details>

### ❓ What happens if the child class has the same method as the parent?

The child **overrides** the parent method.
<details><summary>📌 Example</summary>

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Cat(Animal):
    def speak(self):
        print("Meow")

cat = Cat()
cat.speak()  # Output: Meow
```
</details>

### ❓ Can a child class add its own methods?

Yes! Child classes can have **additional behaviors**.

<details><summary>📌 Example</summary>
    
```python

class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def bark(self):
        print("Woof")

dog = Dog()
dog.speak()  # From parent
dog.bark()   # From child
```
</details>

### ❓ What is `super()` and why use it?

`super()` lets the child class call methods from its parent—especially useful when **overriding methods**.

<details><summary>📌 Example</summary>
```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):
        super().speak()
        print("Dog barks")

dog = Dog()
dog.speak()
# Output:
# Animal speaks
# Dog barks
```
</details>

### ❓ What is the Liskov Substitution Principle (LSP)?

Any object of a subclass should be replaceable for its parent class **without breaking the program**.

✅ Valid:

<details><summary>📌 Example</summary>

```python
class Bird:
    def fly(self):
        print("Flying")

class Sparrow(Bird):
    pass

def lift_off(bird):
    bird.fly()

lift_off(Sparrow())  # ✅ Works fine
```
</details>


### ❓ What is method overriding vs overloading?

* **Overriding**: Child class redefines parent's method.
* **Overloading**: Same method name with different parameters (not natively supported in Python).

<details><summary>📌 Example of Overriding</summary>

```python
class Parent:
    def greet(self):
        print("Hello from Parent")

class Child(Parent):
    def greet(self):  # Method override
        print("Hello from Child")

Child().greet()  # Output: Hello from Child
```

</details>

### ❓ Can a child class access private attributes of the parent?

No, private attributes (e.g., `__name`) are not directly accessible in child classes.

<details><summary>📌 Example</summary>

```python
class Parent:
    def __init__(self):
        self.__secret = "hidden"

class Child(Parent):
    def reveal(self):
        return self.__secret  # ❌ Error

c = Child()
c.reveal()
```
</details>

### ❓ What is the diamond problem in multiple inheritance?

When a class inherits from **two classes that share a common parent**, ambiguity arises in method resolution.

<details><summary>📌 Example</summary>

```python
class A:
    def show(self):
        print("A")

class B(A):
    def show(self):
        print("B")

class C(A):
    def show(self):
        print("C")

class D(B, C):
    pass

d = D()
d.show()  # Output: B (MRO rules)
```
</details>

### ❓ What is MRO (Method Resolution Order)?

Python uses **C3 linearization** to determine the order of method lookup.

<details><summary>📌 Example</summary>

```python
print(D.__mro__)
# (<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>)
```
</details>

### ❓ Can constructors be inherited?

Yes, but only if the parent class has a constructor and the child class doesn't override it. If the child **defines its own `__init__`**, you should manually call the parent using `super().__init__()`.

<details><summary>📌 Example</summary>
    
```python
class Person:
    def __init__(self, name):
        self.name = name

class Student(Person):
    def __init__(self, name, roll):
        super().__init__(name)
        self.roll = roll

s = Student("Alice", 101)
print(s.name)  # Output: Alice
print(s.roll)  # Output: 101
```
</details>

### ❓ What happens if I don't call `super()` in the child class?

The parent's constructor or method **won't run**, which could lead to missing initialization or broken behavior.
<details><summary>📌 Example</summary>

```python
class Parent:
    def __init__(self):
        print("Parent init")

class Child(Parent):
    def __init__(self):
        print("Child init")

c = Child()
# Output: Child init
# ❌ Parent init is never called
```
</details>


### ❓ Can I override `__str__()` in inherited classes?

Yes! You can customize object string representations.

<details><summary>📌 Example</summary>

```python
class Product:
    def __str__(self):
        return "Generic Product"

class Book(Product):
    def __str__(self):
        return "This is a Book"

print(Book())  # Output: This is a Book
```
</details>

### ❓ How can I check if a class is a subclass of another?

Use Python's built-in `issubclass()` or `isinstance()`.

<details><summary>📌 Example</summary>
    
```python
class Animal: pass
class Dog(Animal): pass

print(issubclass(Dog, Animal))     # True
print(isinstance(Dog(), Animal))   # True
```
</details>

### ❓ What is abstract inheritance?

Use the `abc` module to define **abstract base classes**. This forces subclasses to implement certain methods.

<details><summary>📌 Example</summary>

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def area(self):
        return 3.14 * 2 * 2

c = Circle()
print(c.area())  # Output: 12.56
```
</details>

### ❓ Can I inherit from built-in types like `list`, `dict`?

Yes! You can extend and customize Python's native types.

<details><summary>📌 Example</summary>

```python
class MyList(list):
    def sum(self):
        return sum(self)

ml = MyList([1, 2, 3])
print(ml.sum())  # Output: 6
```
</details>

### ❓ What's the difference between **interface** and **abstract class**?

| Concept        | Abstract Class            | Interface (via ABC in Python)    |
| -------------- | ------------------------- | -------------------------------- |
| Can have code? | ✅ Yes                     | ❌ No implementation              |
| Multiple?      | 🟡 Python allows multiple | ✅ Multiple inheritance supported |
| Purpose        | Reuse & enforce design    | Only enforce method signatures   |

### ❓ Can I prevent a class from being inherited?

Yes. In Python, mark it as **final** using the `typing` module.

<details><summary>📌 Example</summary>

```python
from typing import Final

class FinalClass:
    pass

class Child(FinalClass):  # ❌ No error, but discouraged
    pass
```

🔐 *Python does not strictly enforce finality at runtime*—use conventions or external linters like `mypy` for enforcement.

</details>

### ❓ What is cooperative multiple inheritance?

This refers to using `super()` in a way that allows all parent classes in a multiple inheritance setup to get initialized **properly**.

<details><summary>📌 Example</summary>

```python
class A:
    def __init__(self):
        print("A init")
        super().__init__()

class B(A):
    def __init__(self):
        print("B init")
        super().__init__()

class C(A):
    def __init__(self):
        print("C init")
        super().__init__()

class D(B, C):
    def __init__(self):
        print("D init")
        super().__init__()

d = D()
# Output:
# D init
# B init
# C init
# A init
```
</details>

### ❓ How does `super()` work in multiple inheritance?

`super()` uses the **MRO** (Method Resolution Order). It moves to the next class in the MRO list.

Use `Class.__mro__` or `help(Class)` to inspect it.


## ✅ Best Practices for Inheritance

* ✅ Use inheritance for **"is-a"** relationships only.
* ✅ Keep the inheritance tree **shallow**.
* ✅ Prefer **composition over inheritance** unless hierarchy is truly required.
* ✅ Document overridden methods.
* ✅ Use `super()` properly to maintain MRO integrity.
* ✅ Understand **Liskov Substitution Principle** and apply it.

### ❓ How does `super()` know where to go next?

Python uses the **MRO (Method Resolution Order)**. It decides which class to call next when using `super()`—especially important in **multiple inheritance**.

<details><summary>📌 Example</summary>
```python
class A:
    def hello(self):
        print("Hello from A")

class B(A):
    def hello(self):
        print("Hello from B")
        super().hello()

class C(A):
    def hello(self):
        print("Hello from C")
        super().hello()

class D(B, C):
    def hello(self):
        print("Hello from D")
        super().hello()

print(D.__mro__)  # Shows MRO order: D → B → C → A → object
D().hello()

# Output:
# Hello from D
# Hello from B
# Hello from C
# Hello from A
```
</details>

### ❓ Can I override class attributes in child classes?

Yes! A child class can override attributes or methods from the parent.

<details><summary>📌 Example</summary>

```python
class Animal:
    sound = "unknown"

    def speak(self):
        print(f"This animal says {self.sound}")

class Dog(Animal):
    sound = "woof"

Dog().speak()  # Output: This animal says woof
```
</details>

### ❓ Can inheritance work with properties and decorators?

Yes, child classes inherit `@property` and `@staticmethod` decorators. They can also override them.

<details><summary>📌 Example</summary>

```python
class Animal:
    @property
    def category(self):
        return "Unknown"

class Dog(Animal):
    @property
    def category(self):
        return "Mammal"

print(Dog().category)  # Output: Mammal
```
</details>

### ❓ What is diamond inheritance and how does Python handle it?

Diamond inheritance occurs when two parent classes inherit from the same base class, and a child inherits from both.

Python uses **C3 Linearization (MRO)** to resolve it.

<details><summary>📌 Example</summary>

```python
class A:
    def greet(self):
        print("A")

class B(A):
    def greet(self):
        print("B")
        super().greet()

class C(A):
    def greet(self):
        print("C")
        super().greet()

class D(B, C):
    def greet(self):
        print("D")
        super().greet()

D().greet()

# Output:
# D
# B
# C
# A
```
</details>

### ❓ Can child classes access private attributes of the parent?

No. Python uses name mangling to make private attributes harder (not impossible) to access.

<details><summary>📌 Example</summary>

```python
class Base:
    def __init__(self):
        self.__secret = "hidden"

class Sub(Base):
    def reveal(self):
        # print(self.__secret)  # ❌ AttributeError
        print(self._Base__secret)  # ✅ Name mangling workaround

Sub().reveal()  # Output: hidden
```

</details>

### ❓ What if I want to "extend" a method rather than replace it?

Use `super()` in your overridden method to call the base version.

<details><summary>📌 Example: Extending a Method</summary>

```python
class Writer:
    def write(self):
        print("Writing to file...")

class EncryptedWriter(Writer):
    def write(self):
        print("Encrypting data...")
        super().write()

EncryptedWriter().write()
# Output:
# Encrypting data...
# Writing to file...
```
</details>

### ❓ Can a class inherit from multiple unrelated classes?

Yes — that's **multiple inheritance**. Use it carefully to avoid confusion in method resolution.

<details><summary>📌 Example: Multiple Inheritance</summary>

```python
class Flyable:
    def fly(self):
        print("Flying")

class Swimmable:
    def swim(self):
        print("Swimming")

class Duck(Flyable, Swimmable):
    pass

d = Duck()
d.fly()   # Output: Flying
d.swim()  # Output: Swimming
```
</details>

### ❓ What happens if a method is only partially overridden?

Python always uses the most **derived version** of the method. Partial override still overrides fully unless explicitly using `super()`.

<details><summary>📌 Example: Partial Override</summary>

```python
class Vehicle:
    def start(self):
        print("Vehicle started")

class Car(Vehicle):
    def start(self):
        print("Car ready to go")

Car().start()  # Output: Car ready to go
```
</details>

### ❓ What is `__init_subclass__()` and how is it used?

This special method is called automatically **when a class inherits from a base class**. Useful for **validation** or **auto-registration**.

<details><summary>📌 Example: init_subclass Hook</summary>

```python
class Plugin:
    def __init_subclass__(cls):
        print(f"{cls.__name__} registered!")

class MyPlugin(Plugin):
    pass

# Output: MyPlugin registered!
```
</details>

### ❓ How does inheritance interact with `@classmethod` and `@staticmethod`?

Both are inherited, but only `@classmethod` receives the **class as the first argument**, which helps when used in **factories**.

<details><summary>📌 Example: classmethod & staticmethod</summary>

```python
class Animal:
    @classmethod
    def create(cls):
        return cls()  # Flexible for subclasses

    @staticmethod
    def info():
        print("Animals are living beings.")

class Cat(Animal):
    pass

cat = Cat.create()  # Returns a Cat instance
cat.info()          # Output: Animals are living beings.
```
</details>

### ❓ Can I restrict inheritance? (Prevent class from being subclassed)

Yes — Python doesn't enforce it strictly like `final` in Java, but you can use a custom **metaclass** or raise an exception manually.

<details><summary>📌 Example: Preventing Subclassing</summary>

```python
class FinalMeta(type):
    def __new__(cls, name, bases, dct):
        for base in bases:
            if isinstance(base, FinalMeta):
                raise TypeError(f"{base.__name__} is final and cannot be subclassed.")
        return super().__new__(cls, name, bases, dct)

class FinalBase(metaclass=FinalMeta):
    pass

# class Sub(FinalBase):  # ❌ Raises error
#     pass
```
</details>

### ❓❓ What is Delegation vs Inheritance?

Delegation is when a class uses an instance of another class instead of extending it.

<details><summary>📌 Example: Delegation Instead of Inheritance</summary>

```python
class Printer:
    def print_document(self):
        print("Printing...")

class Manager:
    def __init__(self):
        self.printer = Printer()  # Delegation

    def start_print(self):
        self.printer.print_document()

Manager().start_print()
```

</details>

### ❓ What is polymorphism in inheritance?

It means subclasses can provide *different implementations* of a method, and the **caller doesn't need to know the exact type**.

<details><summary>📌 Example: Polymorphism</summary>

```python
class Animal:
    def speak(self):
        raise NotImplementedError

class Dog(Animal):
    def speak(self):
        print("Woof!")

class Cat(Animal):
    def speak(self):
        print("Meow!")

def make_it_talk(animal: Animal):
    animal.speak()  # Doesn't care which type

make_it_talk(Dog())  # Woof!
make_it_talk(Cat())  # Meow!
```
</details>

### ❓ Can I override `__str__`, `__repr__` and other magic methods?

Yes — and it's common to do so in subclasses for customized behavior.

<details><summary>📌 Example: Overriding `__str__` in Subclass</summary>

```python
class Person:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"My name is {self.name}"

class Admin(Person):
    def __str__(self):
        return f"Admin: {self.name}"

print(str(Person("Alice")))  # My name is Alice
print(str(Admin("Bob")))     # Admin: Bob
```
</details>
