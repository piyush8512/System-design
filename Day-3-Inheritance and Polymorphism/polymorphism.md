# 2. Polymorphism

## 2.1 What is Polymorphism?

- **Meaning**: From Greek — "Poly" (many) + "Morph" (forms) = _many forms_.
- **Concept**: One interface or action can behave differently depending on the object or situation.

**Key Benefits**:

- Promotes flexibility and reusability.
- Enables writing more generic and scalable code.
    
---

## 2.2 Real-Life Analogies

- **Scenario 1**: Different animals (`Duck`, `Human`, `Tiger`) all have a `run()` behavior — but each runs differently.
- **Scenario 2**: The same person can `run()` differently depending on context — slow when tired, fast when being chased.

---

## 2.3 Types of Polymorphism in Programming

| Type                     | Description                            | Achieved By        | Time of Resolution |
| ------------------------ | -------------------------------------- | ------------------ | ------------------ |
| **Static Polymorphism**  | Method is selected at **compile time** | Method Overloading | Compile-time       |
| **Dynamic Polymorphism** | Method is selected at **runtime**      | Method Overriding  | Runtime            |

---

## 3. Static Polymorphism (Method Overloading)

- **Definition**: Same method name but **different parameter lists**.
- **Resolution**: Happens at **compile time**.
- **Purpose**: Allows the same method name to perform different tasks based on arguments.

**Java Example**:

```java
class ManualCar {
    void accelerate() {
        System.out.println("Accelerating by default speed.");
    }
    void accelerate(int speed) {
        System.out.println("Accelerating by " + speed + " km/h.");
    }
}

```

###

Rules:

1.Method name must be the same.

2.Parameters must differ in number, type, or order.

3.Return type can be same or different, but it’s not used to differentiate overloads.

---

## 4. Dynamic Polymorphism (Method Overriding)

Definition: Child class redefines a method already defined in the parent class.

Resolution: Happens at runtime.

Purpose: Allows a subclass to provide its own version of a method.

```
class Car {
    void startEngine() {
        System.out.println("Car engine started.");
    }
}

class ElectricCar extends Car {
    @Override
    void startEngine() {
        System.out.println("Electric motor started silently.");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new ElectricCar(); // Polymorphism
        myCar.startEngine(); // Output: Electric motor started silently.
    }
}
```
