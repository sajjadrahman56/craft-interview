## 🔷 O = Open/Closed Principle (OCP)

> **“Software entities (classes, modules, functions) should be open for extension, but closed for modification.”**

Which means:

- ✅ You **can add new behavior**
- ❌ You **should not change existing working code** to do that

**🧠 Important of OCP**

| Problem 🤔                                             | Solution with OCP ✅                                 |
| ------------------------------------------------------ | ---------------------------------------------------- |
| “Every time I add a new feature, I break the old one.” | OCP stops this from happening.                       |
| “Changing old code causes bugs.”                       | With OCP, you **don't need to change** the old code. |
| “Hard to test big apps.”                               | OCP makes apps **modular**, easier to test.          |

**💡 Think Like a Developer:**

> “Can I add something new **without changing** what's already working?”

If yes → You're using OCP ✅
If no → You're breaking OCP ❌

## Understanding the Definition

> **Definition (OCP)**: _Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification._

The OCP tells us to design our code in such a way that **we can add new functionality without changing existing code**. This creates confusion at first. How can something be both open and closed?

- **Open for extension**: You should be able to change the behavior of a module (class or function) to meet new requirements.
<details>
<summary>🔍 Example (Open for Extension)</summary>

Imagine you have a notification system. Initially, you only support Email.

```python
from abc import ABC, abstractmethod

class Notifier(ABC):
    @abstractmethod
    def send(self, message):
        pass

class EmailNotifier(Notifier):
    def send(self, message):
        print(f"Email: {message}")
```

Later, you want to add SMS notifications.

✅ Instead of modifying existing code, you **add a new class**:

```python
class SMSNotifier(Notifier):
    def send(self, message):
        print(f"SMS: {message}")
```

Now you can use it without changing the existing `Notifier` system:

```python
notifier = SMSNotifier()
notifier.send("Hello via SMS!")

```

✅ This is **Open for Extension**: You extended behavior by adding a new class.

</details>

- **Closed for modification**: You should not change the source code of existing classes or functions that are already working.

<details>
<summary>🔍 Example (Closed for Modification)</summary>

Imagine this is your existing working code:

```python
class EmailNotifier:
    def send(self, message):
        print(f"Email: {message}")
```

Now you want to support SMS too.

❌ **Wrong way** (modifies existing function):

```python
class EmailNotifier:
    def send(self, message, type):
        if type == "email":
            print(f"Email: {message}")
        elif type == "sms":
            print(f"SMS: {message}")  # ← modification!
```

✅ **Right way** (keep old code unchanged):
Keep `EmailNotifier` as-is, and just add:

```python
class SMSNotifier:
    def send(self, message):
        print(f"SMS: {message}")
```

✅ This is **Closed for Modification**: You didn’t touch the working class.

</details>
<br>
This is mainly achieved through abstraction 🧩 and polymorphism 🦎

### Building Logic for OCP

**✅ Ask These Questions:**

- Will this module likely need new behaviors?
- Can future behavior be added without touching this code?
- Is the logic general enough to allow plugging in more features?

## Domain based code example

#### ✅ **Use Case : E-Commerce Discount System**  
**Scenario:** Apply different discounts (Seasonal, Membership, Coupon). Future discounts (Flash Sale, Loyalty) may be added.

**❌ Bad Design (OCP Violation)**

**Problem:** Modifying `apply_discount()` for every new discount type.

<details>
<summary>Show Python Code</summary>

```python
class Discount:
    def apply_discount(self, price, discount_type):
        if discount_type == "seasonal":
            return price * 0.9
        elif discount_type == "membership":
            return price * 0.8
        elif discount_type == "coupon":
            return price * 0.85
        else:
            return price
```

</details>

<details>
<summary>Show Java Code</summary>

```java
public class Discount {
    public double applyDiscount(double price, String discountType) {
        if (discountType.equals("seasonal")) {
            return price * 0.9;
        } else if (discountType.equals("membership")) {
            return price * 0.8;
        } else if (discountType.equals("coupon")) {
            return price * 0.85;
        }
        return price;
    }
}
```

</details>

**Solution:** Abstract `DiscountStrategy` with separate classes.

<details>
<summary>Show Python Code</summary>

```python
from abc import ABC, abstractmethod

class DiscountStrategy(ABC):
    @abstractmethod
    def apply(self, price): pass

class SeasonalDiscount(DiscountStrategy):
    def apply(self, price): return price * 0.9

class MembershipDiscount(DiscountStrategy):
    def apply(self, price): return price * 0.8

class DiscountCalculator:
    def __init__(self, strategy: DiscountStrategy):
        self.strategy = strategy
    def calculate(self, price): return self.strategy.apply(price)

# Usage
calc = DiscountCalculator(SeasonalDiscount())
print(calc.calculate(100))  # Output: 90.0
```

</details>

<details>
<summary>Show Java Code</summary>

```java
interface DiscountStrategy {
    double apply(double price);
}

class SeasonalDiscount implements DiscountStrategy {
    public double apply(double price) { return price * 0.9; }
}

class DiscountCalculator {
    private DiscountStrategy strategy;
    public DiscountCalculator(DiscountStrategy strategy) {
        this.strategy = strategy;
    }
    public double calculate(double price) {
        return strategy.apply(price);
    }
}

// Usage
DiscountCalculator calc = new DiscountCalculator(new SeasonalDiscount());
System.out.println(calc.calculate(100));  // Output: 90.0
```

</details>

#### ✅ **Use Case : File Exporter (PDF, CSV, Excel)**  
**Scenario:** Export data in different formats. Future formats (JSON, XML) may be added.

**❌ Bad Design**  
**Problem:** `export_data()` changes for every new format.

<details>
<summary>Show Python Code</summary>

```python
class DataExporter:
    def export_data(self, data, format_type):
        if format_type == "pdf":
            print(f"Exporting PDF: {data}")
        elif format_type == "csv":
            print(f"Exporting CSV: {data}")
```

</details>

<details>
<summary>Show Java Code</summary>

```java
public class DataExporter {
    public void exportData(String data, String formatType) {
        if (formatType.equals("pdf")) {
            System.out.println("Exporting PDF: " + data);
        } else if (formatType.equals("csv")) {
            System.out.println("Exporting CSV: " + data);
        }
    }
}
```

</details>
<br> 

**✅ Good Design**
**Solution:** `ExportStrategy` interface.

<details>
<summary>Show Python Code</summary>

```python
class ExportStrategy(ABC):
    @abstractmethod
    def export(self, data): pass

class PDFExporter(ExportStrategy):
    def export(self, data): print(f"Exporting PDF: {data}")

class CSVExporter(ExportStrategy):
    def export(self, data): print(f"Exporting CSV: {data}")

class ExportManager:
    def __init__(self, strategy: ExportStrategy):
        self.strategy = strategy
    def run_export(self, data): self.strategy.export(data)

# Usage
manager = ExportManager(PDFExporter())
manager.run_export("Sales Data")  # Output: Exporting PDF: Sales Data
```

</details>

<details>
<summary>Show Java Code</summary>

```java
interface ExportStrategy {
    void export(String data);
}

class PDFExporter implements ExportStrategy {
    public void export(String data) {
        System.out.println("Exporting PDF: " + data);
    }
}

class ExportManager {
    private ExportStrategy strategy;
    public ExportManager(ExportStrategy strategy) {
        this.strategy = strategy;
    }
    public void runExport(String data) {
        strategy.export(data);
    }
}

// Usage
ExportManager manager = new ExportManager(new PDFExporter());
manager.runExport("Sales Data");  // Output: Exporting PDF: Sales Data
```

</details>

#### ✅ **Fitness Tracker (Activities)**  
**Scenario:** Track runs, swims. Future activities (Cycling, HIIT) may be added.

**❌ Bad Design**  
**Problem:** `track_activity()` changes for each new activity.

<details>
<summary>Show Python Code</summary>

```python
class FitnessTracker:
    def track_activity(self, activity_type):
        if activity_type == "run":
            print("Tracking run: 5 km")
        elif activity_type == "swim":
            print("Tracking swim: 10 laps")
```

</details>

<details>
<summary>Show Java Code</summary>

```java
public class FitnessTracker {
    public void trackActivity(String activityType) {
        if (activityType.equals("run")) {
            System.out.println("Tracking run: 5 km");
        } else if (activityType.equals("swim")) {
            System.out.println("Tracking swim: 10 laps");
        }
    }
}
```

</details>

<br>

**✅ Good Design**
**Solution:** `Activity` interface.

<details>
<summary>Show Python Code</summary>

```python
class Activity(ABC):
    @abstractmethod
    def track(self): pass

class RunActivity(Activity):
    def track(self): print("Tracking run: 5 km")

class TrackerApp:
    def __init__(self, activity: Activity):
        self.activity = activity
    def start_tracking(self): self.activity.track()

# Usage
app = TrackerApp(RunActivity())
app.start_tracking()  # Output: Tracking run: 5 km
```

</details>

<details>
<summary>Show Java Code</summary>

```java
interface Activity {
    void track();
}

class RunActivity implements Activity {
    public void track() {
        System.out.println("Tracking run: 5 km");
    }
}

class TrackerApp {
    private Activity activity;
    public TrackerApp(Activity activity) {
        this.activity = activity;
    }
    public void startTracking() {
        activity.track();
    }
}

// Usage
TrackerApp app = new TrackerApp(new RunActivity());
app.startTracking();  // Output: Tracking run: 5 km
```

</details>
