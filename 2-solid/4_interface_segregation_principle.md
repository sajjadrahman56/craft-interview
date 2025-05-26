
# 🧠 Interface Segregation Principle (ISP)

> One word ISP : Don't force a class to implement methods it does not need.

" Clients should not be forced to depend upon interfaces they do not use." — Robert C. Martin (Uncle Bob)

## Understand with Simple Example

Imagine you are using a **printer interface**.

### ❌ Bad Design (One Big Interface):

```python
class MultiFunctionMachine:
    def print(self): pass
    def scan(self): pass
    def fax(self): pass
```

Now imagine we only have a **basic printer** — it can **only print**, but because of this interface, we are **forced to implement scan and fax too**.

```python
class OldPrinter(MultiFunctionMachine):
    def print(self):
        print("Printing...")
    
    def scan(self):
        raise NotImplementedError("This printer cannot scan")
    
    def fax(self):
        raise NotImplementedError("This printer cannot fax")
```

This is **violating ISP**. You're writing code for things you don't need!

---

### ✅ Good Design Using ISP

We **split the interface** into smaller ones.

```python
class Printable:
    def print(self): pass

class Scannable:
    def scan(self): pass

class Faxable:
    def fax(self): pass
```

Now you only implement what you need.

```python
class OldPrinter(Printable):
    def print(self):
        print("Printing...")

class ModernPrinter(Printable, Scannable, Faxable):
    def print(self):
        print("Printing...")
    def scan(self):
        print("Scanning...")
    def fax(self):
        print("Faxing...")
```

✅ Now, classes are **only responsible** for what they need — this follows the **Interface Segregation Principle**.

---

### ✅ ISP with Abstract Base Classes in Python

Python doesn't have interfaces like Java, but you can use **Abstract Base Classes** (`abc` module):

```python
from abc import ABC, abstractmethod

class Printable(ABC):
    @abstractmethod
    def print(self):
        pass

class Scannable(ABC):
    @abstractmethod
    def scan(self):
        pass
```

Now implement as needed:

```python
class Printer(Printable):
    def print(self):
        print("Print job done.")

class Scanner(Scannable):
    def scan(self):
        print("Scanning document.")
```

---

### ✅ ISP in a Practical Example

Let’s say we are building a **Payment System**.

### ❌ Violating ISP:

```python
class Payment:
    def pay_by_bank(self): pass
    def pay_by_loan(self): pass
```

Now both `BankPayment` and `LoanPayment` are **forced** to implement both.

```python
class BankPayment(Payment):
    def pay_by_bank(self):
        print("Paid using bank")
    def pay_by_loan(self):
        raise NotImplementedError("Not supported")

class LoanPayment(Payment):
    def pay_by_bank(self):
        raise NotImplementedError("Not supported")
    def pay_by_loan(self):
        print("Paid loan")
```

### ✅ Better Way (Using ISP):

```python
class BankPayable:
    def pay_by_bank(self): pass

class LoanPayable:
    def pay_by_loan(self): pass

class BankPayment(BankPayable):
    def pay_by_bank(self):
        print("Paid using bank")

class LoanPayment(LoanPayable):
    def pay_by_loan(self):
        print("Paid using loan")
```

Now each class **only depends** on what it actually needs.

### How does ISP help with the Single Responsibility Principle?

**Answer:**
ISP supports **SRP** by ensuring each class/interface handles **only one responsibility**.

### ✅ Example:

```python
class ReportGenerator:
    def generate_pdf(self): pass
    def generate_excel(self): pass

# Split based on responsibility:
class PDFGenerator:
    def generate_pdf(self): pass

class ExcelGenerator:
    def generate_excel(self): pass
```

Now each class has **one reason to change**.


### ❓ How is ISP different from SRP or OCP?

| Principle                   | Focus                                       | Example                              |
| --------------------------- | ------------------------------------------- | ------------------------------------ |
| SRP (Single Responsibility) | One reason to change                        | Split logic of printing & saving     |
| OCP (Open Closed)           | Open for extension, closed for modification | Use inheritance or strategy          |
| ISP (Interface Segregation) | Don’t force unused methods                  | Split big interfaces into small ones |

