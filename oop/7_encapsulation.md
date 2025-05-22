# **Encapsulation in OOP: A Complete Interview-Focused Guide**
Encapsulation is the process of binding data (variables) and code (methods) together as a single unit and hiding the internal details from external access.

**Analogy**: Think of a car. You can drive it using the pedals and steering wheel without needing to understand how the engine works. The engine is encapsulated.

## **Core Concepts**
* **Data Hiding**: Internal object details hidden from the outside world.
* **Controlled Access**: Through public methods (getters/setters).
* **Encapsulation Layer**: Ensures only valid operations are allowed.

> Encapsulation protects data from accidental modification and enhances code organization.

## **Access Modifiers**
Access modifiers are used across most programming languages to control **visibility and accessibility** of class members (fields, methods, constructors, etc.). While the **concept is common**, the **syntax and enforcement differ** between languages.

### ✅ Java Access Modifiers
Java uses **explicit keywords** to define access levels:

| Modifier  | Class | Package | Subclass | World |
| --------- | ----- | ------- | -------- | ----- |
| public    | Yes   | Yes     | Yes      | Yes   |
| protected | Yes   | Yes     | Yes      | No    |
| default   | Yes   | Yes     | No       | No    |
| private   | Yes   | No      | No       | No    |

<details>
<summary>🟨 Java Code Example</summary>

```java
public class Rectangle {
    public double width;      // Accessible from anywhere
    private double height;    // Accessible only within this class
}
```
</details>

### 🟦 Python Access Modifiers (By Convention)
Python doesn't enforce access modifiers like Java but uses **naming conventions** to indicate the level of access:

* `public_member` → Public (accessible everywhere)
* `_protected_member` → Protected (conventionally internal use or subclass only)
* `__private_member` → Private (name mangled to prevent direct access)

<details>
<summary>🟦 Python Code Example</summary>

```python
class Rectangle:
    def __init__(self):
        self.public_width = 5            # Public
        self._protected_depth = 8        # Protected (convention)
        self.__private_height = 10       # Private (name mangled)
```
</details>

🔍 **Key Differences**:
* Java enforces access through compiler rules.
* Python relies on developer discipline and naming conventions.

## **Getters and Setters** 
Getters and setters are used to **encapsulate** private fields and **control access** to them. This ensures **validation**, **read-only/write-only control**, and **data protection**.

### ✅ Why Use Getters and Setters?

* Prevent direct modification of private data.
* Add validation before updating a value.
* Abstract internal implementation from outside code.

<details>
<summary>🟨 Java Code Example</summary>

```java
public class Person {
    private String name;  // Private field

    // Getter method (read access)
    public String getName() {
        return name;
    }

    // Setter method (write access with validation)
    public void setName(String name) {
        if (!name.isEmpty()) {
            this.name = name;
        }
    }
}
```
</details>

<details>
<summary>🟦 Python Code Example</summary>

```python
class Person:
    def __init__(self, name):
        self.__name = name  # Private field

    # Getter method
    def get_name(self):
        return self.__name

    # Setter method with validation
    def set_name(self, name):
        if name:
            self.__name = name
```
</details>

🔍 **Key Notes**:
* In **Java**, getters/setters are common OOP practice with `private` fields.
* In **Python**, although not enforced, we use `__name` for private fields and expose them via 

## **Benefits of Encapsulation**
Encapsulation bundles data (fields) and methods (functions) that operate on the data into a single unit—usually a class. This not only protects internal states but also provides clear interfaces for interaction.

### ✅ Key Benefits:
* **Data Integrity**: Prevents unintended or invalid changes by restricting direct access.
* **Controlled Modification**: Changes to data go through controlled interfaces (getters/setters) that can include validation logic.
* **Maintainability**: Encapsulated code is easier to maintain, debug, and update since internal details are hidden.
* **Abstraction & Modularity**: Users interact with high-level interfaces without needing to understand the internal workings.
* **Security**: Sensitive data is hidden from external interference, reducing the risk of bugs or malicious access.

## **Encapsulation vs Other Concepts**
Encapsulation is often confused with other OOP principles like abstraction. While they are related, they serve different purposes.

### **Encapsulation vs Abstraction**
| Feature            | **Encapsulation**                         | **Abstraction**                                       |
| ------------------ | ----------------------------------------- | ----------------------------------------------------- |
| **Focus**          | Hiding internal **data**                  | Hiding **implementation complexity**                  |
| **Access Control** | ✅ Yes (via access modifiers)              | ❌ Not necessarily                                     |
| **Goal**           | Protect data integrity                    | Simplify interface to the user                        |
| **Realized By**    | Access modifiers (`private`, `protected`) | Abstract classes & interfaces                         |
| **Example**        | Hiding fields with getters/setters        | Hiding logic behind `interface` or `abstract` methods |

<details>
<summary>🟨 Java Example</summary>

```java
// Encapsulation
public class BankAccount {
    private double balance;

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) balance += amount;
    }
}

// Abstraction
abstract class Animal {
    abstract void sound();  // Abstract method
}
```
</details>

<details>
<summary>🟦 Python Example</summary>

```python
# Encapsulation
class BankAccount:
    def __init__(self):
        self.__balance = 0

    def get_balance(self):
        return self.__balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

# Abstraction
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass
```
</details>

### **Encapsulation vs Containerization**
* **Encapsulation**: Programming concept (OOP)
* **Containerization**: Software deployment strategy

### **Bank Account Example**
<details>
<summary>Python Code</summary>

```python
class BankAccount:
    def __init__(self, account_number, initial_balance=0):
        self.__account_number = account_number
        self.__balance = initial_balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount

    def get_balance(self):
        return self.__balance
```
</details>

<details>
<summary>🟨 Java Example Code</summary>

```java
public class BankAccount {
    private String accountNumber;
    private double balance;

    public BankAccount(String acc, double initial) {
        accountNumber = acc;
        balance = initial;
    }

    public void deposit(double amount) {
        if (amount > 0) balance += amount;
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) balance -= amount;
    }

    public double getBalance() {
        return balance;
    }
}
```
</details>

### **Student Class with Grade Validation**
<details>
<summary>Python</summary>

```python
class Student:
    def __init__(self, name):
        self.__name = name
        self.__grades = []

    def add_grade(self, grade):
        if 0 <= grade <= 100:
            self.__grades.append(grade)

    def get_average(self):
        return sum(self.__grades) / len(self.__grades) if self.__grades else 0
```

</details>

<details>
<summary>🟨 Java Example</summary>

```java
public class Student {
    private String name;
    private List<Double> grades = new ArrayList<>();

    public Student(String name) {
        this.name = name;
    }

    public void addGrade(double grade) {
        if (grade >= 0 && grade <= 100) grades.add(grade);
    }

    public double getAverage() {
        return grades.stream().mapToDouble(Double::doubleValue).average().orElse(0);
    }
}
```

</details>

### **Employee Class with Salary Encapsulation**
In this example, we encapsulate the **salary** field using a setter method with validation to prevent incorrect values.

<details>
<summary>🟦 Python Code Example</summary>

```python
class Employee:
    def __init__(self, name, salary):
        self.__name = name
        self.__salary = 0
        self.set_salary(salary)

    def get_name(self):
        return self.__name

    def get_salary(self):
        return self.__salary

    def set_salary(self, salary):
        if salary > 0:
            self.__salary = salary
        else:
            print("Salary must be positive.")
```

</details>

<details>
<summary>🟨 Java Code Example</summary>

```java
public class Employee {
    private String name;
    private double salary;

    public Employee(String name, double salary) {
        this.name = name;
        setSalary(salary);
    }

    public String getName() {
        return name;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        if (salary > 0) {
            this.salary = salary;
        } else {
            System.out.println("Salary must be positive.");
        }
    }
}
```

</details>

### **Car Class with Speed Control**
Here’s an example of encapsulation where we hide the **speed** field and provide controlled access to modify it through **getter/setter methods**.

<details>
<summary>🟦 Python Code Example</summary>

```python
class Car:
    def __init__(self, model):
        self.__model = model
        self.__speed = 0

    def get_speed(self):
        return self.__speed

    def set_speed(self, speed):
        if 0 <= speed <= 200:  # Speed must be between 0 and 200
            self.__speed = speed
        else:
            print("Speed must be between 0 and 200.")

    def get_model(self):
        return self.__model
```
</details>

<details>
<summary>🟨 Java Code Example</summary>

```java
public class Car {
    private String model;
    private int speed;

    public Car(String model) {
        this.model = model;
        this.speed = 0;
    }

    public String getModel() {
        return model;
    }

    public int getSpeed() {
        return speed;
    }

    public void setSpeed(int speed) {
        if (speed >= 0 && speed <= 200) {
            this.speed = speed;
        } else {
            System.out.println("Speed must be between 0 and 200.");
        }
    }
}
```

</details>

### **Product Class with Price Validation**
This example shows how encapsulation is useful in real-world situations, like maintaining valid price data for a product.

<details>
<summary>🟦 Python Code Example</summary>

```python
class Product:
    def __init__(self, name, price):
        self.__name = name
        self.__price = 0
        self.set_price(price)

    def get_name(self):
        return self.__name

    def get_price(self):
        return self.__price

    def set_price(self, price):
        if price >= 0:
            self.__price = price
        else:
            print("Price must be non-negative.")
```

</details>

<details>
<summary>🟨 Java Code Example</summary>

```java
public class Product {
    private String name;
    private double price;

    public Product(String name, double price) {
        this.name = name;
        setPrice(price);
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        if (price >= 0) {
            this.price = price;
        } else {
            System.out.println("Price must be non-negative.");
        }
    }
}
```
</details>
