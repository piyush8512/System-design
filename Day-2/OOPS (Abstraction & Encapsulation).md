## 1. Modeling Real-World Entities in Code

### 1.1 Objects, Classes, & Instances

- **Object:** A real-world "thing" with attributes and behaviors.
- **Class:** Blueprint defining those attributes (fields) and behaviors (methods).
- **Instance:** Concrete object in memory, created via the class.

### Car Example - Explaining OOP Concepts

Let's use a car as a real-world example to understand objects, classes, and instances:

### 1. The Car as an Object

In the real world, a car is an object with:

- **Attributes (What it has):** color, make, model, engine type, fuel level, mileage
- **Behaviors (What it does):** start, stop, accelerate, brake, turn, honk

### 2. The Car Class (Blueprint)

```java
public class Car {
    // Attributes (fields)
    private String color;
    private String make;
    private String model;
    private double fuelLevel;
    private int mileage;
    private boolean isRunning;
    
    // Constructor
    public Car(String color, String make, String model) {
        this.color = color;
        this.make = make;
        this.model = model;
        this.fuelLevel = 100.0;  // Full tank
        this.mileage = 0;
        this.isRunning = false;
    }
    
    // Behaviors (methods)
    public void start() {
        if (!isRunning && fuelLevel > 0) {
            isRunning = true;
            System.out.println("The " + color + " " + make + " " + model + " has started.");
        } else if (isRunning) {
            System.out.println("The car is already running.");
        } else {
            System.out.println("Cannot start car. No fuel.");
        }
    }
    
    public void stop() {
        if (isRunning) {
            isRunning = false;
            System.out.println("The car has stopped.");
        } else {
            System.out.println("The car is already stopped.");
        }
    }
    
    public void accelerate() {
        if (isRunning && fuelLevel > 0) {
            fuelLevel -= 1.0;
            mileage += 1;
            System.out.println("The car accelerates. Fuel level: " + fuelLevel);
        } else {
            System.out.println("Cannot accelerate. Car is not running or out of fuel.");
        }
    }
    
    // Getters and setters (Encapsulation)
    public String getColor() {
        return color;
    }
    
    public void setColor(String color) {
        this.color = color;
    }
    
   
}

```

### 3. Car Instances (Objects Created from the Class)

```java
// Creating multiple car instances from the same Car class
public class CarDemo {
    public static void main(String[] args) {
        // Create first car instance
        Car myCar = new Car("Red", "Toyota", "Corolla");
        
        // Create second car instance
        Car friendsCar = new Car("Blue", "Honda", "Civic");
        
        // Each car is a separate object with its own state
        myCar.start();
        myCar.accelerate();
        
        friendsCar.start();
        friendsCar.accelerate();
        friendsCar.accelerate();
        
        System.out.println("My car's color: " + myCar.getColor());
        System.out.println("Friend's car's color: " + friendsCar.getColor());
        
        // Change the color of my car (using encapsulation)
        myCar.setColor("Black");
        System.out.println("My car's new color: " + myCar.getColor());
    }
}

```

## 2. Abstraction in OOP

Abstraction means hiding complex implementation details and showing only the necessary features of an object. It's about simplifying reality by modeling classes based on the essential properties needed for the application.

### Abstraction Applied to Car Example

In our Car class example:

- **We abstract the car's internals:** Users of the Car class don't need to know how the engine works internally or how fuel combustion happens.
- **We provide simple interfaces:** Methods like `start()`, `stop()`, and `accelerate()` hide the complex mechanics behind simple commands.

```java
// Abstraction example with Car
public abstract class Vehicle {
    // Abstract method (no implementation)
    public abstract void startEngine();
    
    // Concrete method
    public void stopEngine() {
        System.out.println("Engine stopped");
    }
}

public class Car extends Vehicle {
    // Implementation of the abstract method
    @Override
    public void startEngine() {
        System.out.println("Car engine started with key ignition");
    }
    
    // Car-specific method
    public void accelerate() {
        System.out.println("Car accelerating");
    }
}

```

Here, the `Vehicle` class abstracts the concept of a vehicle with abstract methods that subclasses must implement. Users don't need to know how different vehicles start their engines - they just call `startEngine()`.

Benefits of Abstraction

1. Simplified Interfaces: Clients focus on what an object does, not how it does it.
2. Ease of Maintenance: Internal changes (e.g., switching from a V6 to an electric motor) don’t affect client code.
3. Code Reuse: Multiple concrete classes can implement the same abstract interface (e.g., SportsCar, SUV, ElectricCar).
4. Reduced Complexity: Large systems are easier to reason about when broken into abstract modules.

## 3. Encapsulation in OOP

Encapsulation is the bundling of data (attributes) and the methods (behaviors) that operate on the data into a single unit (class), while restricting direct access to some of the object's components.

### Encapsulation Applied to Car Example

In our Car class:

- **Private attributes:** Fields like `color`, `fuelLevel`, and `isRunning` are declared private, preventing direct access from outside the class.
- **Public methods:** Access to these attributes is controlled through public methods (getters and setters).
- **Data protection:** We can implement validation in setters to ensure data integrity (e.g., fuel level can't be negative).

```java
public class Car {
    // Encapsulated attributes (private)
    private String make;
    private double fuelLevel;
    private int speed;
    
    // Constructor
    public Car(String make) {
        this.make = make;
        this.fuelLevel = 100.0;
        this.speed = 0;
    }
    
    // Getter method
    public double getFuelLevel() {
        return fuelLevel;
    }
    
    // Setter method with validation
    public void setFuelLevel(double level) {
        // Validation ensures data integrity
        if (level >= 0 && level <= 100) {
            this.fuelLevel = level;
        } else {
            System.out.println("Invalid fuel level. Must be between 0 and 100.");
        }
    }
    
    // Behavior that uses encapsulated data
    public void accelerate() {
        if (fuelLevel > 0) {
            speed += 10;
            fuelLevel -= 0.5;
            System.out.println(make + " accelerating. Speed: " + speed + " mph");
        } else {
            System.out.println("Cannot accelerate. No fuel.");
        }
    }
}

```

### Benefits of Encapsulation in the Car Example

- **Data hiding:** The internal state of the car (fuel level, running status) is protected from outside interference.
- **Controlled access:** Changes to the car's state happen only through well-defined methods.
- **Validation:** We can ensure the car operates within proper parameters (e.g.,