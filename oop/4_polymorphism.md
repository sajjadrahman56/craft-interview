# 🔄 Polymorphism

Polymorphism allows the same interface to be used for different data types or classes. **In simple terms:** One function behaves differently based on the object that invokes it.

**1. The benefit of polymorphism in OOP?**

It allows writing generic, reusable code that can work with different types of objects seamlessly.

**2. How does polymorphism support code extensibility?**

It allows new classes to be integrated without modifying existing code, as long as they follow the expected interface.

**3. Can Python perform compile-time polymorphism? Why or why not?**

No. Python is dynamically typed and doesn't support method overloading natively at compile time.

**4. Why is method overloading not natively supported in Python?**

Python functions are defined in `dictionaries` by name; redefining a method overwrites the previous one.

**5. What happens if two methods with the same name are defined in a Python class?**

Only the last method is retained; the earlier one is overridden.

**7.  Explain how duck typing can lead to more flexible code.**

✅ Code focuses on behavior, not type—any object that implements required methods will work.

<details>
<summary>❓ Duck Typing with Example</summary>

The concept of **duck typing** in Python is captured by the phrase:

> **"If it walks like a duck and quacks like a duck, it's a duck."**

```python
class Bird:
    def fly(self):
        print("Bird is flying")

class Airplane:
    def fly(self):
        print("Airplane is flying")

def start_flying(obj):
    obj.fly()

start_flying(Bird())      # Bird is flying
start_flying(Airplane())  # Airplane is flying
```

You're **not checking the type** of `obj` (whether it’s a `Bird` or `Airplane`).
You're only assuming: _"If it has a `fly()` method, it must be flyable."_

### 🦆 That’s Duck Typing:

Python doesn’t care **what the object is**, only that it **has the method** being called.

### ❌ Not Duck Typing (for contrast):

```python
def start_flying(obj):
    if isinstance(obj, Bird):
        obj.fly()
    elif isinstance(obj, Airplane):
        obj.fly()
```

This checks the type — so it's **not duck typing**.

</details>

**8. What is a potential risk of using duck typing?**

Lack of compile-time checks may lead to runtime errors if expected methods don’t exist.

**9. How does duck typing differ from interface-based polymorphism in Java?**

> Java requires implementing an explicit interface;
> Python only cares if the method exists (duck typing).

<details>
<summary>🔄 Duck Typing vs Interface-Based Polymorphism</summary>

### 🐍 **Python (Duck Typing)**

```python
class Dog:
    def speak(self):
        print("Woof!")

class Cat:
    def speak(self):
        print("Meow!")

def animal_sound(animal):
    animal.speak()

animal_sound(Dog())  # Woof!
animal_sound(Cat())  # Meow!
```

✅ No need to implement a formal interface.
If the object has a `.speak()` method, it works.

 

### ☕ **Java (Interface-Based Polymorphism)**

```java
interface Animal {
    void speak();
}

class Dog implements Animal {
    public void speak() {
        System.out.println("Woof!");
    }
}

class Cat implements Animal {
    public void speak() {
        System.out.println("Meow!");
    }
}

public class Main {
    public static void animalSound(Animal animal) {
        animal.speak();
    }

    public static void main(String[] args) {
        animalSound(new Dog()); // Woof!
        animalSound(new Cat()); // Meow!
    }
}
```

✅ Must **declare and implement** the `Animal` interface
➡️ Enforced at **compile time**


### 🔑 To Sum Up

| Feature                  | Python (Duck Typing) | Java (Interface-Based) |
|          |       -- |        - |
| Type Checking            | Runtime              | Compile-time           |
| Interface Implementation | Not required         | Required               |

## </details>

### ✅ Method Overriding

**10. Can a subclass in Python call the parent’s overridden method? How?**

Yes, using `super().method_name()`.

<details>
<summary>🔄 Calling Parent’s Overridden Method</summary>

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):
        print("Dog barks")
        super().speak()  # Call parent method

d = Dog()
d.speak()
```

**Output:**

```
Dog barks
Animal speaks
```

### Explanation:

- The `Dog` class overrides `speak()`.
- Inside the overridden method, `super().speak()` calls the parent class (`Animal`) version.
</details>

**11. What happens if an abstract method is not overridden in a subclass?**

Python raises a `TypeError` when trying to instantiate the subclass.

<details>
<summary>🚫 Abstract Method Not Overridden Example</summary>

```python
from abc import ABC, abstractmethod
class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

class Dog(Animal):
    pass  # forgot to override speak()
# Trying to create an instance will raise an error
try:
    d = Dog()
except TypeError as e:
    print("Error:", e)
```

**Output:**

```
Error: Can't instantiate abstract class Dog with abstract method speak
```

### Explanation:

- `Animal` defines an abstract method `speak()`.
- `Dog` does **not** override `speak()`.
- Instantiating `Dog` raises `TypeError` because the abstract method isn’t implemented.
</details>

### **12. How is method overriding related to runtime polymorphism?**

> The program decides which method to run **while it’s running**, depending on the actual object.

<details>
<summary>Simple Example</summary>

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):
        print("Dog barks")

def make_sound(animal):
    animal.speak()

make_sound(Animal())  # Animal speaks
make_sound(Dog())     # Dog barks
```

**Explanation:**
Even though `make_sound` calls the same method `.speak()`, it runs the version for the real object type (`Animal` or `Dog`) **when the program runs**. This is called **runtime polymorphism**.

</details>

### ✅ Operator Overloading

**14. Why should `__str__` or `__repr__` be defined when overloading operators?**
To provide meaningful string output for objects when printing or debugging.

**15. Which dunder methods are used for `+`, `-`, `*`, and `/` overloading?**

- `__add__`, `__sub__`, `__mul__`, `__truediv__`

**16. What’s the difference between `__eq__` and `__cmp__`?**

- `__eq__` checks equality (`==`)
- `__cmp__` (Python 2 only) returned -1, 0, 1 for comparisons.

### ✅ Multiple Dispatch

**17. What are the limitations of using `@dispatch` in `multipledispatch`?**

- Doesn't work on instance methods inside classes
- Only works with functions

**18. How does multiple dispatch differ from method overloading?**

- Overloading relies on signature differences
- Multiple dispatch chooses functions based on argument types at runtime.

 
## 🧩 **Types of Polymorphism**  
| Type                  | Description                                      | Python Support | Example Use Case            |  
|       --|                --|     -|         --|  
| **Duck Typing**       | Focus on behavior, not type                      | ✅ Native      | `len()` works on lists/strings |  
| **Operator Overloading** | Customize operators (`+`, `-`, etc.) for objects | ✅ Native      | `a + b` (numbers vs. strings) |  
| **Method Overriding** | Subclass redefines a parent method               | ✅ Native      | `ChildClass` modifies `ParentClass.method()` |  
| **Method Overloading** | Same method name, different parameters          | ❌ Not native  | Simulated via `*args`/`**kwargs` |  
| **Multiple Dispatch** | Choose function based on argument types         | 🟡 Library     | `@dispatch` from `multipledispatch` |  


## 🔍 Code Examples

### **Duck Typing**

<details>
<summary>Example</summary>

```python
class Bird:
    def fly(self):
        print("Bird is flying")

class Airplane:
    def fly(self):
        print("Airplane is flying")

def start_flying(obj):
    obj.fly()

start_flying(Bird())      # Bird is flying
start_flying(Airplane())  # Airplane is flying
```

</details>

###  **Operator Overloading**

<details>
<summary>Example</summary>

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"({self.x}, {self.y})"

p1 = Point(1, 2)
p2 = Point(3, 4)
print(p1 + p2)  # (4, 6)
```
</details>

###  **Method Overriding (Runtime Polymorphism)**

<details>
<summary>Example</summary>

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):
        print("Dog barks")

a = Animal()
d = Dog()

a.speak()  # Animal speaks
d.speak()  # Dog barks
```

</details>

### **Method Overloading (Workaround in Python)**

<details>
<summary>Example</summary>

```python
class Greet:
    def hello(self, name=None):
        if name:
            print(f"Hello, {name}!")
        else:
            print("Hello!")

g = Greet()
g.hello()         # Hello!
g.hello("Alice")  # Hello, Alice!
```

</details>

###  **Multiple Dispatch (`multipledispatch`)**

<details>
<summary>Example</summary>

```python
from multipledispatch import dispatch

@dispatch(int, int)
def add(a, b):
    print(f"Integer sum: {a + b}")

@dispatch(str, str)
def add(a, b):
    print(f"String join: {a + ' ' + b}")

add(2, 3)               # Integer sum: 5
add("hello", "AI")      # String join: hello AI
```

⚠️ Does **not** work inside classes!

</details>

### ❌ Invalid Use of `@dispatch` in Classes

<details>
<summary>Example</summary>

```python
from multipledispatch import dispatch

class Add:
    @dispatch(int, int)
    def add(self, a, b):
        print(a + b)

    @dispatch(float, float)
    def add(self, a, b):
        print(a + b)

# This won't work — only one `add` is retained
```

🛑 `@dispatch` works for functions, not instance methods.

</details>

## 🔧 Dynamic Polymorphism Workarounds in Python

- **Default Arguments**

```python
def greet(name="Guest"):
    print("Hello", name)
```

- **Using `*args` and `**kwargs`\*\*

```python
def add(*args):
    return sum(args)
```

## 📐 Abstract Base Classes (ABCs)

Use ABCs to enforce that all child classes implement specific methods.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def area(self):
        return 3.14 * 5 * 5
```

### **Dynamic Dispatch Example**

**Q:** What is the output?

<details>
<summary>Show Answer</summary>

```python
class Parent:
    def show(self):
        print("Parent")

class Child(Parent):
    def show(self):
        print("Child")

def display(p):
    p.show()

obj = Child()
display(obj)
```

✅ **Output:**

```
Child
```

📌 **Why:** Dynamic dispatch calls the method of the actual object type at runtime.

</details>

 

### **Default Parameter Handling**

<details>
<summary>Show Answer</summary>

```python
class X:
    def greet(self, name="Guest"):
        print(f"Hello, {name}")

x = X()
x.greet()
x.greet("Bob")
```

✅ **Output:**

```
Hello, Guest
Hello, Bob
```

📌 **Why:** Default arguments let a single method handle multiple cases.

</details>

 
###  **Method Overloading Failure**

<details>
<summary>Show Answer</summary>

```python
class A:
    def add(self, a):
        print(a)

    def add(self, a, b):
        print(a + b)

A().add(1)
```

❌ **Output:**

```
TypeError: add() missing 1 required positional argument: 'b'
```

📌 **Why:** Python only keeps the last `add()` definition.

</details>

###  **Fix Method Overloading with `*args`**

<details>
<summary>Show Answer</summary>

```python
class Math:
    def multiply(self, *args):
        if len(args) == 1:
            return args[0] * args[0]
        elif len(args) == 2:
            return args[0] * args[1]

m = Math()
print(m.multiply(3))      # 9
print(m.multiply(2, 4))   # 8
```
</details>

### **Polymorphism in a List of Objects**

<details>
<summary>Show Answer</summary>

```python
class Dog:
    def speak(self): print("Bark")

class Cat:
    def speak(self): print("Meow")

animals = [Dog(), Cat()]
for animal in animals:
    animal.speak()
```

✅ **Output:**

```
Bark
Meow
```

📌 **Why:** Both classes implement the same method, so a unified interface works.

</details>

 
