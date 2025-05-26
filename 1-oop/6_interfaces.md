# 📘 **Interfaces**

An **interface** is a contract or blueprint that defines a **set of abstract methods** that implementing classes **must provide**.
It focuses on **what** needs to be done — **not how**.
> Think of it like a **to-do list** for classes.

## 🔑 Key Characteristics: Java vs Python (ABC)

| Feature                  | Java                                                   | Python (Using `ABC`)                           |
| ------------------------ | ------------------------------------------------------ | ---------------------------------------------- |
| **Methods**              | Abstract (default), `default`, `static` (since Java 8) | Abstract (`@abstractmethod`) and concrete      |
| **Variables**            | `public static final` only                             | Class-level constants (by convention)          |
| **Multiple Inheritance** | ✅ Yes (via interfaces)                                 | ✅ Yes (via multiple ABCs)                      |
| **Constructors**         | ❌ Not allowed                                          | ✅ Allowed in abstract base classes             |
| **Instantiation**        | ❌ Interfaces cannot be instantiated                    | ❌ Abstract base classes cannot be instantiated |

## 📙 Java Interface Syntax

```java
interface Vehicle {
    void start();
}

class Car implements Vehicle {
    public void start() {
        System.out.println("Car started");
    }
}
```

## 📘 Python Interface Syntax (via `abc` module)

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def start(self):
        pass

class Car(Vehicle):
    def start(self):
        print("Car started")
```

### Can an interface have method implementations?

* **Java:** Since Java 8, interfaces can have `default` and `static` methods with implementations.
* **Python:** Abstract Base Classes (ABCs) can include concrete methods.

### Can a class implement multiple interfaces?

✅ **Yes.** This is one of the **main advantages** of interfaces.

```java
interface Flyable { void fly(); }
interface Swimmable { void swim(); }

class Duck implements Flyable, Swimmable {
    public void fly() { ... }
    public void swim() { ... }
}
```

### Interface vs Abstract Class

| Feature         | Interface                               | Abstract Class                 |
| --------------- | --------------------------------------- | ------------------------------ |
| **Inheritance** | Multiple                                | Single                         |
| **Methods**     | Abstract (default), `default`, `static` | Abstract + Concrete            |
| **Constructor** | ❌ Not allowed                           | ✅ Allowed                      |
| **Variables**   | `public static final` only              | Any access modifier allowed    |
| **Use Case**    | Define capabilities (contract)          | Partial implementation + state |

### Can interfaces extend other interfaces?

✅ **Yes.** One interface can extend one or more interfaces.

```java
interface Animal {
    void eat();
}

interface Mammal extends Animal {
    void walk();
}
```

### What if a class doesn’t implement all interface methods?

❌ In **Java**, it must be declared `abstract` or you’ll get a **compile-time error**.
✅ In **Python**, if you skip an abstract method, you'll get a `TypeError` when instantiating.

### Can interfaces be generic?

✅ **Yes!** In both Java and Python.

```java
interface Container<T> {
    void add(T item);
}
```

## 🚨 Common Mistakes & Fixes

| Mistake                                 | Fix / Solution                                    |
| --------------------------------------- | ------------------------------------------------- |
| ❌ Instantiating an interface            | ✅ Use a concrete class that implements it         |
| ❌ Missing method implementations        | ✅ Mark class as abstract or implement all methods |
| ❌ Using instance variables in interface | ✅ Use constants (`public static final`) in Java   |
| ❌ Mixing abstract and concrete concepts | ✅ Use abstract class for partial implementation   |

### Can abstract classes have concrete methods?
Yes. Abstract classes can:
* Define **abstract methods** (no body, must be implemented by subclasses)
* Define **concrete methods** (reusable logic)
<details>
<summary>🟨 Java Code Example</summary>

```java
abstract class Animal {
    abstract void sound();  // Abstract method

    void sleep() {          // Concrete method
        System.out.println("Sleeping...");
    }
}

class Cat extends Animal {
    void sound() {
        System.out.println("Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a = new Cat();
        a.sound();  // Output: Meow!
        a.sleep();  // Output: Sleeping...
    }
}
```
</details>

<details>
<summary>🟦 Python Code Example</summary>

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

    def sleep(self):
        print("Sleeping...")

class Cat(Animal):
    def sound(self):
        print("Meow!")

a = Cat()
a.sound()  # Output: Meow!
a.sleep()  # Output: Sleeping...
```
</details>
