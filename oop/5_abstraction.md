# 📘 Abstraction

**🧠Abstraction** is the process of hiding the implementation details from the user and exposing only the **essential features**.

In OOP, abstraction is achieved using:

* **Abstract classes**
* **Interfaces** (in other languages; simulated in Python via abstract base classes)

### **How do you implement abstraction in Python?**

Using:
* `ABC` (Abstract Base Class) from `abc` module.
* `@abstractmethod` decorator to define abstract methods.

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass
```

### **Can we create an object of an abstract class in Python?**

❌ **No.** In both **Python** and **Java**, abstract classes **cannot be instantiated directly**. You must **create a subclass** that implements all abstract methods.

<details>
<summary>🟨 Java Code Example</summary>

```java
abstract class Animal {
    abstract void sound();
}

class Dog extends Animal {
    void sound() {
        System.out.println("Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        // Animal a = new Animal(); // ❌ Compilation error
        Animal dog = new Dog();     // ✅ Valid
        dog.sound();                // Output: Woof!
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

class Dog(Animal):
    def sound(self):
        print("Woof!")

# a = Animal()        # ❌ TypeError: Can't instantiate abstract class
dog = Dog()           # ✅ Valid
dog.sound()           # Output: Woof!
```
</details>

### **What is the difference between abstraction and encapsulation?**

| Abstraction                               | Encapsulation                              |
| ----------------------------------------- | ------------------------------------------ |
| Hides logic                               | Hides data                                 |
| Achieved with abstract classes/interfaces | Achieved with private/protected attributes |
| Focus: What to do                         | Focus: How to protect data                 |


###  **Can an abstract class have concrete (non-abstract) methods?**

✅ **Yes.** An abstract class **can have both**:

* **Abstract methods**: declared but not implemented.
* **Concrete methods**: fully implemented and reusable by subclasses.
<details>
<summary>🟨 Java Code Example</summary>

```java
abstract class Animal {
    // Abstract method
    abstract void sound();

    // Concrete method
    void sleep() {
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

### **What happens if a subclass does not implement all abstract methods?**

❗ **The subclass becomes abstract** and **cannot be instantiated** unless it implements all inherited abstract methods.

<details>
<summary>🟨 Java Code Example</summary>

```java
abstract class Animal {
    abstract void sound();
    abstract void move();
}

// Subclass does not implement all abstract methods
abstract class Dog extends Animal {
    void sound() {
        System.out.println("Bark!");
    }
}

// Cannot do this:
// Dog d = new Dog(); // ❌ Error: Dog is abstract and cannot be instantiated

class Puppy extends Dog {
    void move() {
        System.out.println("Runs!");
    }

    public static void main(String[] args) {
        Puppy p = new Puppy(); // ✅ OK
        p.sound(); // Bark!
        p.move();  // Runs!
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

    @abstractmethod
    def move(self):
        pass

class Dog(Animal):
    def sound(self):
        print("Bark!")

# Cannot instantiate Dog because move() is not implemented
# d = Dog()  # ❌ TypeError

class Puppy(Dog):
    def move(self):
        print("Runs!")

p = Puppy()  # ✅ OK
p.sound()    # Bark!
p.move()     # Runs!
```
</details>

### **Why use abstract classes instead of interfaces in Python?**

✅ **Because Python has no interfaces**, abstract base classes (`ABC`) serve the same purpose — defining **behavior contracts**.

They offer **more flexibility** than traditional interfaces by allowing:

* **Abstract methods** to enforce implementation.
* **Concrete methods** to share reusable logic.

This allows Python developers to achieve **interface-like behavior** with added power.

<details>
<summary>🟨 Java Code Example</summary>

```java
interface Shape {
    void draw();  // Abstract by default
}

class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing Circle");
    }
}
```

</details>
<details>
<summary>🟦 Python Code Example</summary>

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def draw(self):
        pass

class Circle(Shape):
    def draw(self):
        print("Drawing Circle")

c = Circle()
c.draw()  # Output: Drawing Circle
```
</details>

### **Can a Python abstract class have a constructor?**

✅ Yes. Abstract classes can have constructors (`__init__`) and they can be called via `super()` from subclasses.

### **How does abstraction help ?**

* ✅ Reduces complexity
* ✅ Encourages modularity
* ✅ Promotes code reuse
* ✅ Enforces a contract for subclasses
* ✅ Makes large codebases easier to manage

---

### **What is the difference between an abstract class and a concrete class?**

| Abstract Class               | Concrete Class                |
| ---------------------------- | ----------------------------- |
| Cannot be instantiated       | Can be instantiated           |
| Can contain abstract methods | All methods are implemented   |
| Acts as a blueprint          | Used to create actual objects |

### **How do abstract base classes support polymorphism?**

✅ **Abstract base classes enable polymorphism** by allowing you to use **a common interface** to interact with different subclass objects.

This means:

* You can call the **same method** on different objects.
* Each object provides its **own implementation** of that method.
* The calling code stays **generic and reusable**.

<details>
<summary>🟨 Java Code Example</summary>

```java
abstract class Animal {
    abstract void sound();
}

class Dog extends Animal {
    void sound() {
        System.out.println("Bark!");
    }
}

class Cat extends Animal {
    void sound() {
        System.out.println("Meow!");
    }
}

public class Main {
    static void makeSound(Animal a) {
        a.sound();  // polymorphic call
    }

    public static void main(String[] args) {
        makeSound(new Dog());  // Output: Bark!
        makeSound(new Cat());  // Output: Meow!
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

class Dog(Animal):
    def sound(self):
        print("Bark!")

class Cat(Animal):
    def sound(self):
        print("Meow!")

def make_sound(animal: Animal):
    animal.sound()  # polymorphic behavior

make_sound(Dog())  # Output: Bark!
make_sound(Cat())  # Output: Meow!
```
</details>

### **What is the role of `@abstractmethod` in multiple inheritance?**
If any base class includes an abstract method, all subclasses must implement it, or they too become abstract.

### **Can an abstract method call another concrete method in the same class?**
✅ **Yes.** An abstract method **can call** other **concrete methods** within the same class.
This helps organize shared behavior and avoids code duplication, even though the abstract method itself doesn't provide full implementation.

<details>
<summary>🟨 Java Code Example</summary>

```java
abstract class Shape {
    abstract void draw();

    void log(String msg) {
        System.out.println("Log: " + msg);
    }
}

class Circle extends Shape {
    void draw() {
        log("Drawing a Circle");  // Calling concrete method
        System.out.println("⚪");
    }
}

public class Main {
    public static void main(String[] args) {
        Shape s = new Circle();
        s.draw();
    }
}
```

</details>
<details>
<summary>🟦 Python Code Example</summary>

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def draw(self):
        self.log("Preparing to draw")  # Calling concrete method

    def log(self, msg):
        print(f"Log: {msg}")

class Circle(Shape):
    def draw(self):
        super().draw()
        print("⚪")

s = Circle()
s.draw()
```

</details>

### **What if an abstract class has a static method — should it be abstract?**

**Answer:**
Static methods **cannot** be abstract because they do not rely on instance-level behavior. You can define a static method in an abstract class, but you **cannot** make it abstract.

<details>
<summary>🟨 Java Code Example</summary>

```java
abstract class Shape {
    static void info() {
        System.out.println("This is a static method.");
    }
}

class Circle extends Shape {
    // Static method is not abstract, it can be called directly from the class
}

public class Main {
    public static void main(String[] args) {
        Shape.info();  // Output: This is a static method.
    }
}
```

</details>
<details>
<summary>🟦 Python Code Example</summary>

```python
from abc import ABC

class Shape(ABC):
    @staticmethod
    def info():
        print("This is a static method.")

class Circle(Shape):
    pass

Shape.info()  # Output: This is a static method.
```

</details>

### **Can properties (like getters/setters) be abstract in Python?**

**Answer:**
✅ Yes, you can make properties abstract by combining `@property` with `@abstractmethod`.

```python
class Person(ABC):
    @property
    @abstractmethod
    def age(self): 
        pass
```

<details>
<summary>🟨 Java Code Example</summary>

```java
abstract class Person {
    // Abstract getter
    abstract int getAge();
}

class Student extends Person {
    private int age;

    public Student(int age) {
        this.age = age;
    }

    // Concrete getter
    @Override
    public int getAge() {
        return age;
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Student(20);
        System.out.println("Age: " + person.getAge());  // Output: Age: 20
    }
}
```
</details>
<details>
<summary>🟦 Python Code Example</summary>

```python
from abc import ABC, abstractmethod

class Person(ABC):
    @property
    @abstractmethod
    def age(self):
        pass

class Student(Person):
    def __init__(self, age):
        self._age = age
    
    @property
    def age(self):
        return self._age

s = Student(20)
print(f"Age: {s.age}")  # Output: Age: 20
```

</details>

### **How do you check if a class is abstract in Python?**

**Answer:**
You can check if a class is abstract by using the `inspect.isabstract()` method, which returns `True` if the class has abstract methods.

```python
import inspect

print(inspect.isabstract(MyClass))  # True if MyClass has abstract methods
```

<details>
<summary>🟨 Java Code Example</summary>

```java
import java.lang.reflect.Modifier;

abstract class MyClass {
    abstract void myMethod();
}

class ConcreteClass extends MyClass {
    void myMethod() {
        System.out.println("Implemented method");
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println(Modifier.isAbstract(MyClass.class.getModifiers()));  // Output: true
        System.out.println(Modifier.isAbstract(ConcreteClass.class.getModifiers()));  // Output: false
    }
}
```

</details>
<details>
<summary>🟦 Python Code Example</summary>

```python
import inspect

class MyClass(ABC):
    @abstractmethod
    def my_method(self):
        pass

class ConcreteClass(MyClass):
    def my_method(self):
        print("Implemented method")

print(inspect.isabstract(MyClass))  # Output: True
print(inspect.isabstract(ConcreteClass))  # Output: False
```
</details>


