# Liskov Substitution Principle (LSP) -- Deep Dive Notes

## 1. What is LSP?

A child class should be usable anywhere its parent class is expected,
without breaking the program.
If replacing a parent with a child changes the behavior in unexpected
ways → **LSP is broken**.

------------------------------------------------------------------------

## 2. Three Categories of Rules

### 2.1 Signature Rules

Ensure the method "shape" (arguments, return type, exceptions) stays
compatible.

-   **Method Argument Rule**
    -   Child must accept the same or wider arguments than the parent.
        ✅ Parent accepts `String`, child can accept `String` or
        `Object`.
        ❌ Child cannot suddenly require `Integer`.
-   **Return Type Rule**
    -   Child can return the same type or a narrower type.
        ✅ Parent returns `Animal`, child can return `Dog`.
        ❌ Child cannot return `Object`.
-   **Exception Rule**
    -   Child can throw fewer or narrower exceptions, but never
        broader.
        ✅ Parent throws `RuntimeException`, child can throw
        `ArithmeticException`.
        ❌ Child cannot suddenly throw `IOException`.

------------------------------------------------------------------------

### 2.2 Property Rules

Preserve the rules/invariants of the parent's data.

-   **Class Invariant Rule**
    ✅ Parent: Bank account balance can't go below 0.
    ❌ Child: Allows negative balance → breaks the invariant.

-   **History Constraint Rule**
    ✅ Parent: All accounts allow withdrawal.
    ❌ Child: A FixedDeposit account overrides `withdraw()` to always
    throw error.

------------------------------------------------------------------------

### 2.3 Method Rules

-   **Preconditions (Before Execution)**
    -   Child can make requirements weaker (easier to satisfy), but not
        stronger.
        ✅ Parent requires password ≥ 8 chars, child allows ≥ 6 chars.
        ❌ Child suddenly requires ≥ 12 chars → breaks existing clients.
-   **Postconditions (After Execution)**
    -   Child can make guarantees stronger but not weaker.
        ✅ Parent's `brake()` guarantees speed decreases; child's
        `brake()` also recharges battery → fine.
        ❌ Child's `brake()` sometimes increases speed → violation.

------------------------------------------------------------------------

# Interface Segregation Principle (ISP) -- Notes

## 1. Definition

"Clients should not be forced to depend on methods they do not use."
👉 Break big interfaces into smaller, role-specific ones.

------------------------------------------------------------------------

## 2. The Problem with "Fat" Interfaces

-   A single interface tries to cover too many responsibilities.
-   Example: One `Shape` interface had both `area()` and `volume()`.
    ✅ Works fine for 3D shapes like Cube.
    ❌ But 2D shapes (Square, Rectangle) don't have `volume()`.

⚠️ Issues:
- Clients depend on unused methods.
- Violates **SRP**.
- Leads to brittle code (lots of "not applicable" methods).

------------------------------------------------------------------------

## 3. ISP Solution -- Split into Smaller Interfaces

-   `TwoDimensionalShape` → only `area()`.
-   `ThreeDimensionalShape` → `area()` + `volume()`.

✅ Benefits:
- Each class implements only what it needs.
- Cleaner design, avoids exceptions.
- Easier to maintain, extend, and test.

------------------------------------------------------------------------

# Dependency Inversion Principle (DIP) -- Notes

## 1. Definition

Two golden rules:
1. High-level modules should not depend on low-level modules; both
should depend on **abstractions**.
2. Abstractions should not depend on details; details should depend on
**abstractions**.

------------------------------------------------------------------------

## 2. The Problem with Direct Coupling

-   `UserService` directly calls `MySQLDatabase` or `MongoDBDatabase`.
-   Creates **tight coupling**.
-   Violates **OCP**: new DB → must edit `UserService`.

------------------------------------------------------------------------

## 3. DIP Solution -- Use an Abstraction Layer

1.  Create interface `Database` with `save()`.
2.  Low-level modules (`MySQL`, `MongoDB`) implement it.
3.  `UserService` depends only on `Database`.
4.  Use **Dependency Injection** to decide DB at runtime.

✅ Benefits:
- Easy to extend (new DB = new class).
- No changes in `UserService`.
- Business logic stays clean.

------------------------------------------------------------------------

## 4. Real-World Analogy 🏢

-   **CEO (high-level)** doesn't manage devs directly.
-   **Manager (abstraction)** communicates requirements.
-   **Developers (MySQL/Mongo)** follow manager.
-   Replace one dev → CEO unaffected.

------------------------------------------------------------------------

## 5. Final Thoughts & Trade-Offs

-   SOLID principles are **guidelines**, not rigid laws.
-   Sometimes performance/business needs may override them.
-   But generally, DIP leads to:
    -   Flexible code
    -   Easier scaling
    -   Fewer ripple-effect bugs

------------------------------------------------------------------------
