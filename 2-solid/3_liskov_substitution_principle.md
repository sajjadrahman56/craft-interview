## **What is Liskov Substitution Principle**

If your program works with the parent class, it should also work if you pass a child class — without breaking anything or changing the behavior unexpectedly.

Let's closer look the examples

### 🚫 **Penguins Can’t Fly**
Imagine you have two classes:
```python
class Bird: 
    def fly(self):
        print("Flying! 🦅")

class Penguin(Bird):  # Penguin is a child of Bird
    def fly(self):
        raise Error("Penguins can’t fly! 🐧")  # Breaks the rule!
```

#### What’s Wrong?
- **Parent (Bird):** Can fly.
- **Child (Penguin):** Breaks the `fly()` method.  
If the code expects a `Bird` that can fly, using a `Penguin` crashes the program! ❌


### ✅ Fixing The Penguins Problems**
**Solution:** Don’t force penguins to inherit from `Bird` if they can’t fly. 

Redesign the classes to avoid surprises:

```python
class Bird:
    pass  # General bird stuff

class FlyingBird(Bird):
    def fly(self):
        print("Flying! 🦅")

class Penguin(Bird):  # Penguins are birds but don’t fly
    def swim(self):
        print("Swimming! 🐧")
```

Now:
- `FlyingBird` handles birds that fly.
- `Penguin` is a `Bird` but doesn’t inherit `fly()`.  

**LSP Rule:** Children should do *everything* their parent can do. `If a parent can fly, the child shouldn’t remove flying!`


## 🎉 Look at Another Example


```python
class Animal:
    pass

class SpeakingAnimal(Animal):
    def speak(self):
        pass

class Dog(SpeakingAnimal):
    def speak(self):
        print("Woof!")

class Fish(Animal):
    def swim(self):
        print("Fish is swimming.")
```

---

Now:

```python
def talk_to_animal(animal: SpeakingAnimal):
    animal.speak()

talk_to_animal(Dog())       # ✅ Works
talk_to_animal(Fish())      # ❌ Type error (won't pass type checking)
```

---

> **If a subclass can't behave like the parent class in every context, it shouldn't inherit from it.**

## 🔄 **Conceptual Questions with Examples**

### ❓ **“What is the Liskov Substitution Principle?”**

If you replace a parent class with one of its child classes in your code, everything should work the same — no errors, no unexpected behavior.

### ✅ Code Example:

```python
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    def speak(self):
        print("Bark!")

# Usage
def make_animal_speak(animal: Animal):
    animal.speak()

make_animal_speak(Dog())  # ✅ This works: prints "Bark!"
```

👉 **Follows LSP** because `Dog` behaves like an `Animal`.

### ❓ **What’s wrong with this code?**

```python
class Bird:
    def fly(self):
        print("Flying")

class Ostrich(Bird):
    def fly(self):
        raise Exception("Ostriches can't fly!")
```

❌ **Problem:** If your code expects all `Bird`s to fly, then replacing `Bird` with `Ostrich` breaks the expectation — violating LSP.


### ✅ **LSP-Compliant Redesign**

```python
class Bird:
    def make_sound(self):
        print("Chirp!")

class FlyingBird(Bird):
    def fly(self):
        print("Flying high!")

class Sparrow(FlyingBird):
    pass

class Ostrich(Bird):  # No fly() method
    pass

# Usage
def make_it_fly(bird: FlyingBird):
    bird.fly()

make_it_fly(Sparrow())   # ✅ Works
# make_it_fly(Ostrich()) # ❌ Won't compile or run — we’ve now avoided a runtime surprise
```

✅ Now we use specific subclasses to separate flying and non-flying birds — maintaining LSP.


### ❓ **“How to avoid forcing children to implement unnecessary methods?”**

Use abstract base classes or interfaces instead:

```python
from abc import ABC, abstractmethod

class Printer(ABC):
    @abstractmethod
    def print(self):
        pass

class Scanner(ABC):
    @abstractmethod
    def scan(self):
        pass

class AllInOneMachine(Printer, Scanner):
    def print(self):
        print("Printing")

    def scan(self):
        print("Scanning")

class SimplePrinter(Printer):
    def print(self):
        print("Just printing")
```

👍 This keeps each class focused and avoids violating LSP.


### ❓ **Design a notification system with LSP in mind**

```python
from abc import ABC, abstractmethod

class Notification(ABC):
    @abstractmethod
    def send(self, message):
        pass

class EmailNotification(Notification):
    def send(self, message):
        print(f"Sending email: {message}")

class SMSNotification(Notification):
    def send(self, message):
        print(f"Sending SMS: {message}")

class PushNotification(Notification):
    def send(self, message):
        print(f"Sending Push Notification: {message}")

# Function using LSP
def notify_user(notification: Notification, message: str):
    notification.send(message)

# Usage
notify_user(EmailNotification(), "Hello via Email!")  # ✅
notify_user(SMSNotification(), "Hello via SMS!")      # ✅
```

✅ All subclasses can be used in place of the parent without breaking behavior — this is LSP.





_NB : A simple and basic IDEA of of LSP_