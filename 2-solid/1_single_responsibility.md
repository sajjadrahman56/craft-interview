# 📘 Basic Design Principles & Single Responsibility Principle

**Design principles** are best practices that guide how we organize and structure code. Their goal is to make software:
* ✅ Easier to understand
* 🔄 Easier to change
* 🧪 Easier to test
* 🤝 Easier to collaborate on

## 🧱 Types of Logic in a Typical Software System

To apply the **Single Responsibility Principle (SRP)**, you must identify the **reason a class or module might change**.
Typically that **reason comes from the type of logics** it handles:
> ✅ **Each logic type = a unique reason to change.**
 
<details> <summary>📊 Expand different types of Logic </summary>
  
| 💡 Logic Type              | ✅ Responsibility Example                                                                | 🔄 Often Changes When...               |
| -------------------------- | --------------------------------------------------------------------------------------- | -------------------------------------- |
| **Business Logic**         | Pricing rules, tax calculation, workflows. 🧠 *“What should happen?”*                   | Business policy or regulations change. |
| **UI Logic**               | Button clicks, animations, modal toggles. 🎨 *“What does the user see or do?”*          | Designers change UX.                   |
| **Presentation Logic**     | Format currency, date/time, chart transforms. 🖼️ *“How should data look?”*             | Display requirements evolve.           |
| **Persistence Logic**      | Save/load data from DB/API. 💾 *“Where/how is data stored?”*                            | Backend systems change.                |
| **Validation Logic**       | Check correctness of input. ✅ *“Is this input valid?”*                                  | Data rules or security needs evolve.   |
| **Communication Logic**    | Talk to email/SMS/APIs. 📡 *“How do we talk to external systems?”*                      | APIs or message formats change.        |
| **Infrastructure Logic**   | Logging, caching, auth. 🧱 *“How do we ensure performance, security, observability?”*   | Libraries/frameworks change.           |
| **Configuration Logic**    | Feature flags, environment settings. ⚙️ *“How does behavior vary across environments?”* | New features or deployments added.     |
| **Error Handling Logic**   | Fallbacks, retries, error messages. 🚨 *“What happens if something fails?”*             | Failure scenarios evolve.              |
| **Security Logic**         | Permissions, sanitization. 🔐 *“Who can do what?”*                                      | Compliance or threat models evolve.    |
| **Scheduling Logic**       | Cron jobs, polling. ⏰ *“When should this happen?”*                                      | Business rules or infra needs shift.   |
| **Routing Logic**          | Maps URLs to handlers. 🧭 *“Where should this request go?”*                             | Routes or modules change.              |
| **State Management Logic** | Tracks current app state. 📦 *“What does the app remember right now?”*                  | Interactivity or complexity grows.     |

</details>

## ✅ What is the Single Responsibility Principle?
> A class should have **only one reason to change** — meaning it should have **only one job**.
* Not about line count or number of methods.
* A reason does not mean A method
* It’s about **separating concerns** so each class focuses on a single responsibility.

## 🎯 Why SRP Matters

| Benefit           | Why It Matters                                               |
| ----------------- | ------------------------------------------------------------ |
| ✔ Maintainability | Easier to update or debug when logic is focused              |
| ✔ Testability     | Easier to write unit tests when each class does one thing    |
| ✔ Reusability     | Smaller, focused classes can be reused elsewhere             |
| ✔ Collaboration   | Teams can work on separate responsibilities without conflict |

## ❌ SRP Violation Example
🔴 
```java
class Invoice {
    public void calculateTotal() { ... }
    public void printInvoice() { ... }
    public void saveToDatabase() { ... }
}
```
This class mixes:
* Business logic
* Presentation logic
* Persistence logic
  
```python
class Invoice:
    def calculate_total(self):
        pass

    def print_invoice(self):
        pass

    def save_to_db(self):
        pass
```
## ✅ SRP Refactored Example

<details>
<summary>🟢 Java</summary>

```java
class Invoice {
    public void calculateTotal() { ... }
}

class InvoicePrinter {
    public void print(Invoice invoice) { ... }
}

class InvoiceRepository {
    public void save(Invoice invoice) { ... }
}
```

</details>

<details>
<summary>🟢 Python</summary>

```python
class Invoice:
    def calculate_total(self):
        pass

class InvoicePrinter:
    def print(self, invoice):
        pass

class InvoiceRepository:
    def save(self, invoice):
        pass
```

</details>

## 🔍 How to Identify SRP Violations

Ask yourself:
1. **Who would ask for changes to this class?**
   – If it’s more than one type of stakeholder (e.g., UI designer *and* DB admin), SRP is likely violated.
2. **Would different roles need to modify it for different reasons?**
   – Changes driven by unrelated concerns (UI vs. business logic) suggest multiple responsibilities.
3. **Can I describe its purpose in one sentence — without using “and”, “also”, or “but”?**
   – If not, the class probably does too much.

### Can a class have multiple methods and still follow SRP?

**A:** Yes. As long as all the methods belong to the same responsibility.

## 💡 SRP Examples Across Domains

---

### 🧮 Calculator App

**❌ Violates SRP**
Mixes responsibilities: math, logging, and file I/O.

```python
class Calculator:
    def add(self, a, b): return a + b
    def subtract(self, a, b): return a - b
    def log_result(self, result): print(f"Result: {result}")
    def save_to_file(self, result): open("log.txt", "a").write(str(result) + "\n")
```

**✅ Refactored SRP**
Separated into math, logging, and saving classes.

```python
class Calculator:
    def add(self, a, b): return a + b
    def subtract(self, a, b): return a - b

class Logger:
    def log(self, message): print(message)

class FileSaver:
    def save(self, data): open("log.txt", "a").write(data + "\n")
```

---

### 🛒 E-Commerce Order System

**❌ Violates SRP**
Handles business logic, email notifications, and database storage in one class.

```python
class Order:
    def calculate_total(self): pass
    def send_confirmation_email(self): pass
    def save_to_database(self): pass
```

**✅ Refactored SRP**
Split into separate classes for each responsibility.

```python
class Order:
    def calculate_total(self): pass

class EmailService:
    def send_confirmation(self, order): pass

class OrderRepository:
    def save(self, order): pass
```

---

### 🤖 ML Pipeline (Model Training)

**❌ Violates SRP**
Performs data loading, preprocessing, training, and saving in one class.

```python
class ModelTrainer:
    def load_data(self): pass
    def preprocess(self): pass
    def train_model(self): pass
    def save_model(self): pass
```

**✅ Refactored SRP**
Each class handles a specific phase of the ML workflow.

```python
class DataLoader:
    def load(self): pass

class Preprocessor:
    def clean(self, data): pass

class Trainer:
    def train(self, data): pass

class ModelSaver:
    def save(self, model): pass
```

---

### 🧑‍🏫 Education App (Student Progress)

**✅ SRP-Compliant from the Start**
Each class has a clearly defined responsibility.

```python
class Student:
    def __init__(self, name): self.name = name

class ProgressTracker:
    def track_progress(self, student): pass

class ReportGenerator:
    def generate_report(self, student): pass

class EmailNotifier:
    def send_progress_report(self, student): pass
```

### To SUM UP

Here’s a concise and structured **To SUM UP** section for your guide:

---

## 🧾 To SUM UP

> 📝 Note: This note is for **self-learning** and reviewed with assistance from GPT to ensure clarity and correctness. 

| ✅ Principle                   | 📌 Key Insight                                                                  |
| ----------------------------- | ------------------------------------------------------------------------------- |
| **One Responsibility**        | A class should have only **one reason to change**.                              |
| **Separation of Concerns**    | Different types of logic should live in **different classes or modules**.       |
| **Focus Improves Everything** | SRP makes code more **testable**, **maintainable**, and **collaborative**.      |
| **Responsibility ≠ Method**   | A class can have many methods — as long as they serve **one cohesive purpose**. |
| **Violation Symptoms**        | Long classes, mixed logic types, hard-to-test or hard-to-reuse components.      |
