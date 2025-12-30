# Low-Level Design (LLD) – Day 2

> **Focus:** Class Relationships, UML Diagrams, Core Design Principles, and an Introduction to Design Patterns.


## 1. Class Relationships & UML Representations

Understanding how classes relate to each other is central to Low-Level Design. These relationships define **ownership, lifecycle, coupling, and extensibility**.


### A. Inheritance ("Is-A" Relationship)

**Definition:** A child class derives properties and behavior from a parent class.

**UML Representation:**

* Solid line with an **empty triangle** pointing to the **Base/Parent** class.

**Example:**

* `Manager` is an `Employee`

**LLD Notes:**

* Inheritance implies **substitutability** (LSP).
* Avoid inheritance purely for code reuse.

### B. Implementation (Interface Realization)

**Definition:** A class implements a contract defined by an interface or abstract class.

**UML Representation:**

* **Dashed line** with an empty triangle pointing to the **Interface**.

**Notation Styles:**

* `<<interface>>`
* Italic interface names
* Prefix `I` (e.g., `INotificationSender`)

**Example:**

* `LeaseTimeBasedStrategy` implements `DriverMatchingStrategy`

**LLD Notes:**

* Core to **DIP** and **OCP**
* Preferred over concrete dependencies

### C. Composition (Strong Has-A Relationship)

**Definition:** One class owns another.

**Key Characteristic:**

* **Dependent lifecycle** – child cannot exist without parent.

**UML Representation:**

* Solid line with a **filled diamond (♦)** on the parent side.

**Example:**

* `Restaurant` ♦── `Menu`

**LLD Notes:**

* Strong ownership
* Preferred over inheritance when lifecycle is tightly bound

### D. Aggregation (Weak Has-A Relationship)

**Definition:** One class references another, but does not own its lifecycle.

**Key Characteristic:**

* **Independent lifecycle**

**UML Representation:**

* Solid line with an **empty diamond (◇)** on the parent side.

**Example:**

* `RiderManager` ◇── `Rider`

**LLD Notes:**

* Common in managers, services, repositories


### E. Association (Uses / Calls Relationship)

**Definition:** One class interacts with another without ownership.

**UML Representation:**

* Solid line with open arrow (`→`)

#### 1. Unidirectional Association

* A → B

**Example:**

* `User` → `PaymentGateway`

**Code Context:**

* Passing objects as method parameters

#### 2. Bidirectional Association

* A ↔ B

**Examples:**

* `User` ↔ `Reminder`
* `DeliveryPartner` ↔ `Customer`

**LLD Caution:**

* Increases coupling
* Should be used sparingly

  
## 2. UML Class Diagram Anatomy

A UML class box has **three sections**:

1. Class Name
2. Attributes (Variables)
3. Methods (Functions)

### Visibility Symbols

| Symbol | Meaning   |
| ------ | --------- |
| `+`    | Public    |
| `-`    | Private   |
| `#`    | Protected |

### Additional UML Notations

* **Underline** → Static member
* **Italics** → Abstract class or method
* **Return type** → After colon (`:`)

## 3. General Design Principles (Mindset-Level)

These principles guide **how you think before writing code**, complementing SOLID.

# Uber-Ola-Low-Level-Design
<img width="1926" height="1360" alt="image" src="https://github.com/user-attachments/assets/9fc6140b-44ee-4abd-b84e-b238becc1536" />


### A. KISS (Keep It Simple, Stupid)

* Prefer simplicity over cleverness
* Avoid unnecessary abstractions

**LLD Insight:**

* Do not over-engineer early designs


### B. YAGNI (You Aren’t Gonna Need It)

* Do not build unused features
* Avoid speculative future logic

**Clarification:**

* YAGNI ≠ non-extensible design


### C. DRY (Don’t Repeat Yourself)

* Single source of truth
* Remove duplicated logic

**LLD Insight:**

* Duplication leads to bugs and inconsistency


## 4. Introduction to Design Patterns

### What are Design Patterns?

* Reusable solutions to recurring design problems
* Language-independent
* Based on industry best practices

**Relation to SOLID:**

* Patterns are structured applications of SOLID


### Categories of Design Patterns

#### 1. Creational Patterns

* Object creation
* Examples: Singleton, Factory, Abstract Factory, Builder

#### 2. Structural Patterns

* Object/class composition
* Examples: Adapter, Decorator, Facade

#### 3. Behavioral Patterns

* Communication and responsibility
* Examples: Strategy, Observer, Command

## 5. Important Scenarios Discussed (Interview-Relevant)

### Scenario 1: Driver vs Ride

* Ride persists after Driver removal → **Aggregation**
* Ride deleted with Driver → Composition

**Real-world:** Aggregation


### Scenario 2: Pizza Across Brands

* Same pizza type across brands ≠ same object
* Price, image, description differ

**Conclusion:** Separate objects

### Scenario 3: When to Draw UML

* Ideally before coding
* Useful for interviews, reviews, KT

**Interview Tip:**

* Rough UML with labeled arrows is sufficient

## 6. JavaScript-Specific Notes

* No native interfaces (use conventions / TypeScript)
* UML applies conceptually
* Prefer composition over inheritance
* Enforce discipline manually


## 7. Final Takeaways (Day 2)

* Relationships define lifecycle and ownership
* UML clarifies design thinking
* Composition > inheritance in most cases
* Principles prevent long-term decay


## 8. What’s Next

* Factory & Abstract Factory patterns
