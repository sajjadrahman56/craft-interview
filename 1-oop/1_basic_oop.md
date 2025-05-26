# 🐍 Python OOP Full Guide — From Basics to Best Practices

Everything in Python is Object-Oriented

Example:

```python
a = 2  # 'a' is an object of integer type
```

Similarly:

```python
roll = [1, 2, 3, 4]
roll.append(5)  # list method
roll.pop()      # remove last element
```

Here, `roll` is an object of the `list` class.

---

## 🧱 What is a Class?

A class is a **blueprint**. It has:

1. **Data / Properties** → Variables
2. **Functions / Behaviors** → Methods

Example (Structure only):

```python
class Human:
    name
    age
    phone_no

    def demo():
        pass
```

* Class names should be in PascalCase → `ThisIsClass`
* Variable and method names should be in snake\_case → `this_is_variable`

---

## 💡 OOP Benefits

1. ✅ Reusable code
2. ✅ No global variables required
3. ✅ Organized and modular code
4. ✅ Easier debugging
5. ✅ Data protection via encapsulation

---

## 🔁 Procedural vs Object-Oriented (OOP)

🧨 Non-OOP Example (Risky!):

```python
balance = 100

def withdraw(amount):
    global balance
    balance -= amount
```

✅ OOP Version (Cleaner and Safer):

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def withdraw(self, amount):
        self.balance -= amount

# Usage
account1 = BankAccount(100)
account2 = BankAccount(200)

account1.withdraw(50)  # Only affects account1
```

---

## 🔧 Class with Constructor (`__init__()`)

A special method called when the object is created.

Example:

```python
class Atm:
    def __init__(self):
        print("ATM object created")
```

Note:

* It's spelled `__init__`, not `__int__`
* Called automatically when an object is instantiated

---

## 🎓 `__init__()` is a Magic Method

Magic methods in Python have double underscores: `__method__`.
You cannot skip `__init__()` if you want to initialize object attributes.

---

## 🍽 OOP Analogy — Like a Recipe!

| OOP Concept   | Cooking Analogy      |
| ------------- | -------------------- |
| Class         | Recipe               |
| Object        | Cooked Dish          |
| Instantiation | Cooking              |
| Attributes    | Spice Level, Garnish |
| Methods       | Cooking Instructions |

---

## 🍛 Custom Class Example: Dish

Define:

```python
class Dish:
    def __init__(self, name, spice_level, garnish):
        self.name = name
        self.spice_level = spice_level
        self.garnish = garnish

    def serve(self):
        print(f"Serving {self.name} with {self.spice_level} spice and {self.garnish} garnish.")
```

Create objects:

```python
dish1 = Dish("Curry", "Medium", "Cilantro")
dish2 = Dish("Curry", "Spicy", "Mint Leaves")

dish1.serve()
dish2.serve()
```

Output:

```
Serving Curry with Medium spice and Cilantro garnish.
Serving Curry with Spicy spice and Mint Leaves garnish.
```

---

## 🙋 What is `self`?

* Refers to the current object instance.
* Always required as the first parameter in instance methods.

Example:

```python
self.name = name  # means "this object’s name = the given name"
```

---

## 🧬 Inheritance (Optional but Powerful)

Allows a class to inherit properties and methods from another.

```python
class Dish:
    def __init__(self, name):
        self.name = name

class SweetDish(Dish):
    def serve(self):
        print(f"Serving sweet {self.name}")

cake = SweetDish("Cake")
cake.serve()  # Output: Serving sweet Cake
```

---

## 🔐 Rest of the part add soon



 
