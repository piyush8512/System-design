# Inheritance in Object-Oriented Programming (OOP)

## 1.1 What is Inheritance?
Inheritance is a **fundamental concept in Object-Oriented Programming (OOP)** that allows a class (**child**) to acquire the properties (**fields**) and behaviors (**methods**) of another class (**parent**).

It promotes:
- **Code reusability** – avoid rewriting the same code in multiple classes.
- **Class hierarchy clarity** – create logical relationships between classes.

**Real-world analogy:**
> A `Dog` inherits traits from `Animal` (like `eat()`), but can also have unique traits (like `bark()`).

---

## 1.2 Key Terms & Concepts

- **Superclass / Parent / Base Class** → The class whose members are inherited.
- **Subclass / Child / Derived Class** → The class that inherits from the parent class.
- **extends** (Java) / `:` with `public`/`protected`/`private` (C++) → Used to create an inheritance relationship.
- **"is-a" Relationship** → Dog **is an** Animal, ElectricCar **is a** Car.

---

## 1.3 Types of Inheritance

| Type | Description | Example |
|------|-------------|---------|
| **Single Inheritance** | One class inherits from one parent. | `class Dog extends Animal` |
| **Multilevel Inheritance** | A class inherits from a class that itself inherits from another. | `A → B → C` |
| **Hierarchical Inheritance** | Multiple child classes inherit from a single parent. | `Dog, Cat, Cow` all extend `Animal` |
| **Multiple Inheritance (C++)** | A class inherits from more than one parent. *(Not supported for classes in Java to avoid diamond problem)* | `class C : public A, public B` |

---

## 1.4 Access Specifiers in Inheritance

### **In Java**
- **Public members** → stay public.
- **Protected members** → accessible in subclass & same package.
- **Private members** → never directly inherited (can be accessed via public/protected methods).

### **In C++**

| Mode | Public Members Become | Protected Members Become |
|------|-----------------------|--------------------------|
| **public inheritance** | public | protected |
| **protected inheritance** | protected | protected |
| **private inheritance** | private | private |

---

## 1.5 Real-Life Example: Car Hierarchy

**Parent Class:** `Car` *(Generic)*  
**Attributes:**
- `brand`
- `model`
- `isEngineOn`
- `currentSpeed`

**Behaviors:**
- `startEngine()`
- `stopEngine()`
- `accelerate()`
- `brake()`

---

**Child Class 1:** `ManualCar` *(inherits Car)*  
- Attribute: `currentGear`  
- Behavior: `shiftGear()`

**Child Class 2:** `ElectricCar` *(inherits Car)*  
- Attribute: `batteryPercentage`  
- Behavior: `chargeBattery()`

---

## 1.6 Java Example

```java
// Superclass
class Car {
    String brand;
    String model;
    boolean isEngineOn;
    int currentSpeed;

    void startEngine() { isEngineOn = true; }
    void stopEngine() { isEngineOn = false; }
    void accelerate() { currentSpeed += 10; }
    void brake() { currentSpeed -= 10; }
}

// Subclass 1
class ManualCar extends Car {
    int currentGear;
    void shiftGear(int gear) { currentGear = gear; }
}

// Subclass 2
class ElectricCar extends Car {
    int batteryPercentage;
    void chargeBattery() { batteryPercentage = 100; }
}

public class Main {
    public static void main(String[] args) {
        ElectricCar tesla = new ElectricCar();
        tesla.brand = "Tesla";
        tesla.startEngine();
        tesla.accelerate();
        tesla.chargeBattery();
    }
}
z