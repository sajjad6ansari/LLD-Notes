# Low-Level System Design (LLD) – Day 1

## 1. HLD vs LLD

| Aspect    | HLD (High-Level Design)         | LLD (Low-Level Design)          |
| --------- | ------------------------------- | ------------------------------- |
| Focus     | Architecture, components, infra | Classes, interfaces, logic flow |
| Audience  | Architects, stakeholders        | Developers (SDE I / II)         |
| Questions | How systems connect?            | How code is structured?         |
| Output    | Diagrams, tech stack            | Class diagrams, APIs, code      |

**Goal of LLD**

* Write **maintainable**, **extendable**, and **readable** code
* Code should survive team changes and long timelines


## 2. OOP Foundations (LLD Perspective)

### Class vs Object

* **Class**: Blueprint (no real data)
* **Object**: Real instance with state

## 3. Four Pillars of OOP

### 3.1 Encapsulation

**Idea:** Bundle data + behavior, restrict direct access

| Modifier  | Java                       | C++              | JavaScript                  |
| --------- | -------------------------- | ---------------- | --------------------------- |
| public    | Everywhere                 | Everywhere       | Default                     |
| private   | Class only                 | Class only       | `#field` (ES2022) / closure |
| protected | Class + subclass + package | Class + subclass | Convention only             |

**LLD takeaway:** Protect invariants, expose minimal API

### 3.2 Abstraction

**Idea:** Show *what* an object does, hide *how*

* Java: `interface`, `abstract class`
* C++: Abstract class via pure virtual functions
* JavaScript: No language-level abstraction → achieved via

  * Interfaces by convention
  * Abstract base classes (runtime checks)

### 3.3 Inheritance

**Idea:** Reuse and extend behavior

* Java: `extends`
* C++: `:` with access specifier
* JavaScript: `extends` (prototype-based under the hood)

**LLD rule:** Prefer **composition over inheritance** unless hierarchy is stable


### 3.4 Polymorphism

#### Compile-time (Static Binding)

* Method overloading
* Java / C++ only
* JavaScript ❌ (no true overloading)

#### Runtime (Dynamic Binding)

| Language   | How it works                                                          |
| ---------- | --------------------------------------------------------------------- |
| Java       | All non-static, non-final, non-private methods are virtual by default |
| C++        | Requires `virtual` keyword + vtable                                   |
| JavaScript | Dynamic dispatch via prototype chain                                  |


## 4. Compile Time vs Runtime

| Aspect       | Compile Time | Runtime    |
| ------------ | ------------ | ---------- |
| Binding      | Static       | Dynamic    |
| Errors       | Syntax, type | Exceptions |
| Polymorphism | ❌            | ✅          |

**Key clarification:**

* Overloading → compile time
* Overriding → runtime

## 5. Virtual vs Non-Virtual (C++)

* **Non-virtual**: Compile-time binding
* **Virtual**: Runtime binding via vtable

**Important rules:**

* `override` does NOT make a function virtual
* Base function must be `virtual`
* Virtual dispatch cannot be bypassed at call site


## 6. Calling Parent Method

### C++

```cpp
void send() override {
    Notification::send();
}
```

* No `super` keyword
* Explicit base class name (supports multiple inheritance)

### Java

```java
@Override
void send() {
    super.send();
}
```

* `super` exists because Java has single inheritance

### JavaScript

```js
class Child extends Parent {
  send() {
    super.send();
  }
}
```

**Rule (all languages):** Cannot force parent method from base reference


## 7. Abstract Class vs Interface

### Abstract Class

* Has state + behavior
* Represents **is-a** relationship

### Interface

* Contract only
* Represents **can-do** capability

| Aspect               | Abstract Class | Interface  |
| -------------------- | -------------- | ---------- |
| Multiple inheritance | ❌              | ✅          |
| State                | ✅              | ❌          |
| Use case             | Base logic     | Capability |

**JavaScript:** Interfaces do not exist → use conventions / TypeScript


## 8. Static vs Non-Static

### Static

* Belongs to class
* Shared across instances
* No polymorphism

### Non-static

* Belongs to object
* Supports overriding

**Important clarification:**

* Static members *can* be accessed via object in Java
* But should ALWAYS be accessed via class name


## 9. Static & Final (Class / Method / Variable)

### `final`

| Level    | Meaning                       |
| -------- | ----------------------------- |
| Class    | Cannot be inherited           |
| Method   | Cannot be overridden          |
| Variable | Value/reference cannot change |

### `static`

| Level    | Meaning                                     |
| -------- | ------------------------------------------- |
| Variable | One shared copy                             |
| Method   | Class-level behavior                        |
| Class    | ❌ Java (only nested static classes allowed) |

### C++

* No static classes
* Uses namespaces instead


## 10. Inheritance of Static Members

| Member          | Inherited? | Polymorphic? |
| --------------- | ---------- | ------------ |
| Static variable | ✅          | ❌            |
| Static method   | ✅ (hidden) | ❌            |
| Instance method | ✅          | ✅            |



## 11. SOLID Principles (LLD Core)

### S – Single Responsibility Principle (SRP)

* One reason to change
* Split validators, repositories, services

### O – Open/Closed Principle (OCP)

* Extend, don’t modify
* Achieved via inheritance / composition

### L – Liskov Substitution Principle (LSP)

* Subclass must be usable as base
* Avoid breaking contracts

### I – Interface Segregation Principle (ISP)

* Avoid fat interfaces
* No client should depend on unused methods

### D – Dependency Inversion Principle (DIP)

* Depend on abstractions, not concretes
* Enables loose coupling


## 12. ISP Example (Key Interview Topic)

**Bad (Fat Interface):**

```java
interface User {
    void doKYC();
}
```

**Good (Segregated):**

```java
interface KYCApplicable {
    void doKYC();
}
```

* Customer does NOT implement it
* DeliveryPartner does

**JavaScript:** Use separate service objects / duck typing


## 13. Java vs C++ vs JavaScript (Design Philosophy)

| Language   | Philosophy                            |
| ---------- | ------------------------------------- |
| Java       | Safety-first, managed runtime         |
| C++        | Control-first, zero-cost abstractions |
| JavaScript | Flexibility-first, dynamic            |

> Java gains safety by **restricting power**.
> C++ gains performance by **exposing power**.


## 14. Final Interview Takeaways

* LLD is about **handling change**
* SOLID is about **reducing ripple effects**
* OOP tools + SOLID discipline = good design
* JavaScript needs **extra discipline** to follow LLD principles


## 15. What’s Next

* Composition vs Inheritance
* UML Diagrams
* DRY / KISS / YAGNI
* Real LLD interview problems
