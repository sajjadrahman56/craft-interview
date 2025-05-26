### **What is LSP?**

> If your program works with the parent class, it should also work if you pass a child class — without breaking anything or changing the behavior unexpectedly.

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

**LSP Rule:** Children should do *everything* their parent can do. (If a parent can fly, the child shouldn’t remove flying!)


## 🎉 1. Fun Comic Explanation of Liskov Substitution Principle

**Characters**:

* 🐶 Dog (child class)
* 🐾 Animal (parent class)
* 🐟 Fish (also child class)
* 🤖 Programmer

---

**Scene 1:**

🤖: "Okay, I’ll write a class `Animal` with a `speak()` method!"

```python
class Animal:
    def speak(self):
        print("I make a sound.")
```

---

**Scene 2:**

🐶: "I’m a dog! I can speak!"

```python
class Dog(Animal):
    def speak(self):
        print("Woof!")
```

---

**Scene 3:**

🐟: "I’m a fish... I can't speak!"

```python
class Fish(Animal):
    def speak(self):
        # Fish can't talk!
        raise Exception("Fish can't speak!")
```

---

**Scene 4:**

🤖: "Let’s test all animals!"

```python
def talk_to(animal):
    animal.speak()
```

---

**Scene 5:**

🤖: `talk_to(Dog())` ➜ 🐶 "Woof!" ✅
🤖: `talk_to(Fish())` ➜ 💥 Error: Fish can't speak ❌

---

📣 Moral: Fish should not inherit from Animal if it can't follow the same rules (like speaking).
👉 That breaks the **Liskov Substitution Principle**!

---

## 🧠 2. Simple Visual Diagram

```
        [Animal]     
           |
    -------------------
    |                 |
 [Dog]           [Fish ❌]
speak(): "Woof"   ❌ Can't speak

Violation ❌: Fish is expected to speak because it is an Animal
```

✅ Only subclass if you fully support parent behavior.

---

## ✅ 3. Interactive Quiz

Try answering these to check your understanding!

**Q1: Which child class violates LSP?**

```python
class Bird:
    def fly(self):
        print("Flying!")

class Sparrow(Bird):
    def fly(self):
        print("Sparrow flying!")

class Penguin(Bird):
    def fly(self):
        raise Exception("I can't fly!")
```

* [ ] Sparrow
* [x] Penguin
* [ ] None

**Answer**: ✅ Penguin breaks LSP because `Bird` promises that all birds can fly.

---

**Q2: Fix the LSP issue above**

* A. Let Penguin stay as is
* B. Remove Penguin from inheriting Bird and use a new `Swimmer` class
* C. Make `fly()` optional in Bird

✅ Correct answer: **B**

---

## Summary Checklist ✅

| Question                                     | LSP Safe? |
| -------------------------------------------- | --------- |
| Can child be used wherever parent is used?   | ✅         |
| Does child remove or change parent behavior? | ❌         |
| Does child add errors or surprises?          | ❌         |

---

Would you like:

* A **code sandbox** to play with these examples?
* More **real-life analogies** (like devices, vehicles)?
* A **practice worksheet** with answers?

Let’s build your confidence! 💪
