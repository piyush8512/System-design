# SOLID Principles in System Design

## Problems Solved by SOLID Principles
1. A class or file does too many things at once, making it hard to fix or update without breaking something else.  
2. Every time you add a new feature, you must edit old code, which can cause bugs.  
3. A child class doesn’t behave like its parent, so when you replace one with the other, the program acts weird or breaks.  
4. A class is forced to use methods it doesn’t need, which makes code bigger and harder to manage.  
5. Big parts of the code depend directly on tiny details, making the system hard to change or test.  

---

## 1. S - Single Responsibility Principle (SRP)

### Definition
A class should have only **one job** or **one reason to change**.  
If a class takes on multiple responsibilities, it becomes harder to maintain and more error-prone.

### 🔴 SRP Violated
**ShoppingCart class** is doing 3 different jobs:
- Managing products & calculating totals (**Cart logic**).
- Printing invoice (**Output/Presentation logic**).
- Saving to database (**Persistence logic**).

👉 Problem: If we change how invoices are printed or how data is stored, we still have to modify the `ShoppingCart` class → higher risk of bugs.

### 🟢 SRP Followed
Responsibilities are split into separate classes:
- `ShoppingCart` → only manages cart items & total calculation.  
- `ShoppingCartPrinter` → only handles printing invoices.  
- `ShoppingCartStorage` → only saves cart data to DB.  

👉 Benefit:
- Each class is focused & easier to maintain.  
- Future changes (e.g., new invoice format, different database) affect only the related class.  

---

## 2. O - Open/Closed Principle (OCP)

### Definition
Software entities (classes, modules, functions) should be:  
- **Open for extension** → You can add new behavior.  
- **Closed for modification** → You don’t need to edit existing, stable code.  

### 🔴 OCP Violated
`ShoppingCartStorage` has separate methods for saving to SQL, Mongo, and File.  
If we want to add another storage type (e.g., Cloud), we must **edit this class** and add a new method.  

👉 Problem: Every new feature forces changes in old code → increases risk of bugs.  

### 🟢 OCP Followed
- Created a `Persistence` interface.  
- Different classes (`SQLPersistence`, `MongoPersistence`, `FilePersistence`) **implement** this interface.  
- When a new storage type is needed (e.g., `CloudPersistence`), we just **add a new class** without touching existing code.  

👉 Benefit: System grows by **extension, not modification**.  

---

## 3. L - Liskov Substitution Principle (LSP)

### Definition
Objects of a superclass should be **replaceable** with objects of its subclasses **without breaking the program**.  
Subtypes must behave in a way that does **not surprise or break client code**.  

### 🔴 LSP Violated
- `Account` interface forces all subclasses to implement both `deposit()` and `withdraw()`.  
- But `FixedTermAccount` doesn’t logically support withdrawal.  
- To satisfy the interface, it throws an **UnsupportedOperationException**.  

👉 Problem: When a `FixedTermAccount` is used in place of an `Account`, the client code breaks → violation of LSP.  

### 🟢 LSP Followed
Interfaces are split logically:  
- `DepositOnlyAccount` → only for deposit-only accounts.  
- `WithdrawableAccount` → extends deposit and adds withdraw.  

`SavingAccount` and `CurrentAccount` implement `WithdrawableAccount`.  
`FixedTermAccount` implements only `DepositOnlyAccount`.  

👉 Benefit: Now all subclasses **perfectly match their behavior** → no surprises, no broken client code.  



If I made a mistake, please email me at prajapatipiyush851@gmail.com.