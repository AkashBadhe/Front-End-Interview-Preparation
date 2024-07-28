Question 1: Explain SOLID principle in derails with example.

# SOLID Principles in JavaScript

The SOLID principles are a set of five design principles that help in creating maintainable and scalable software. These principles are widely used in object-oriented programming and can be applied to JavaScript as well.

## 1. Single Responsibility Principle (SRP)
The SRP states that a class should have only one reason to change. In other words, a class should have only one responsibility. By adhering to this principle, we can ensure that our classes are focused and have a clear purpose.

Example:
```javascript
class UserService {
    // Methods related to user management
}

class EmailService {
    // Methods related to sending emails
}

// Bad Example
public class User {
    public void AddUser() {
        // Code to add user
    }
    
    public void GenerateReport() {
        // Code to generate report
    }
}

// Good Example
public class User {
    public void AddUser() {
        // Code to add user
    }
}

public class ReportGenerator {
    public void GenerateReport() {
        // Code to generate report
    }
}

```

## 2. Open/Closed Principle (OCP)
The OCP states that software entities (classes, modules, functions) should be open for extension but closed for modification. This means that we should be able to add new functionality without modifying existing code.

Example:
```javascript
class Shape {
    // Common shape properties and methods
}

class Circle extends Shape {
    // Circle-specific properties and methods
}

class Rectangle extends Shape {
    // Rectangle-specific properties and methods
}

// Bad Example
public class Rectangle {
    public double Width { get; set; }
    public double Height { get; set; }
}

public class AreaCalculator {
    public double CalculateArea(Rectangle rectangle) {
        return rectangle.Width * rectangle.Height;
    }
}

// Good Example
public abstract class Shape {
    public abstract double CalculateArea();
}

public class Rectangle : Shape {
    public double Width { get; set; }
    public double Height { get; set; }

    public override double CalculateArea() {
        return Width * Height;
    }
}

public class Circle : Shape {
    public double Radius { get; set; }

    public override double CalculateArea() {
        return Math.PI * Radius * Radius;
    }
}
```

## 3. Liskov Substitution Principle (LSP)
The LSP states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. In other words, subclasses should be able to be used interchangeably with their base class.

Example:
```javascript
class Animal {
    makeSound() {
        // Common sound for all animals
    }
}

class Dog extends Animal {
    makeSound() {
        // Sound specific to dogs
    }
}

class Cat extends Animal {
    makeSound() {
        // Sound specific to cats
    }
}

// Bad Example
public class Bird {
    public virtual void Fly() {
        // Fly
    }
}

public class Ostrich : Bird {
    public override void Fly() {
        throw new Exception("Ostriches can't fly!");
    }
}

// Good Example
public abstract class Bird {
    public abstract void Move();
}

public class Sparrow : Bird {
    public override void Move() {
        Fly();
    }

    private void Fly() {
        // Fly
    }
}

public class Ostrich : Bird {
    public override void Move() {
        Run();
    }

    private void Run() {
        // Run
    }
}
```

## 4. Interface Segregation Principle (ISP)
The ISP states that clients should not be forced to depend on interfaces they do not use. It promotes the idea of having smaller, more specific interfaces rather than a single large interface.

Example:
```javascript
class Printer {
    print() {
        // Common print method
    }
}

class Scanner {
    scan() {
        // Common scan method
    }
}

class Photocopier {
    print() {
        // Print method specific to photocopiers
    }

    scan() {
        // Scan method specific to photocopiers
    }
}

// Bad Example
public interface IWorker {
    void Work();
    void Eat();
}

public class Worker : IWorker {
    public void Work() {
        // Work
    }

    public void Eat() {
        // Eat
    }
}

public class Robot : IWorker {
    public void Work() {
        // Work
    }

    public void Eat() {
        throw new Exception("Robots don't eat!");
    }
}

// Good Example
public interface IWorkable {
    void Work();
}

public interface IFeedable {
    void Eat();
}

public class Worker : IWorkable, IFeedable {
    public void Work() {
        // Work
    }

    public void Eat() {
        // Eat
    }
}

public class Robot : IWorkable {
    public void Work() {
        // Work
    }
}
```

## 5. Dependency Inversion Principle (DIP)
The DIP states that high-level modules should not depend on low-level modules. Both should depend on abstractions. It promotes loose coupling between modules and allows for easier maintenance and testing.

Example:
```javascript
class Database {
    // Database-related methods
}

class UserRepository {
    constructor(database) {
        this.database = database;
    }

    // Methods for user data manipulation using the database
}

// Bad Example
public class LightBulb {
    public void TurnOn() {
        // Turn on the light
    }

    public void TurnOff() {
        // Turn off the light
    }
}

public class Switch {
    private LightBulb _lightBulb;

    public Switch(LightBulb lightBulb) {
        _lightBulb = lightBulb;
    }

    public void Operate() {
        _lightBulb.TurnOn();
    }
}

// Good Example
public interface ISwitchable {
    void TurnOn();
    void TurnOff();
}

public class LightBulb : ISwitchable {
    public void TurnOn() {
        // Turn on the light
    }

    public void TurnOff() {
        // Turn off the light
    }
}

public class Switch {
    private ISwitchable _device;

    public Switch(ISwitchable device) {
        _device = device;
    }

    public void Operate() {
        _device.TurnOn();
    }
}
```

By following these SOLID principles, we can create more modular, maintainable, and extensible JavaScript code. Remember, these principles are not strict rules, but guidelines that can help improve the quality of your software.

Question 2: Can you please explain the DRY principle?
## Don't Repeat Yourself (DRY) Principle

The DRY principle is a software development principle that promotes the idea of avoiding duplication of code. It states that every piece of knowledge or logic should have a single, unambiguous representation within a system.

By adhering to the DRY principle, developers can reduce code duplication, improve code maintainability, and minimize the risk of introducing bugs. Instead of repeating the same code in multiple places, developers should strive to extract common functionality into reusable components, functions, or modules.

DRY principle encourages the use of abstractions, such as functions, classes, or libraries, to encapsulate common logic and promote code reuse. This not only reduces the amount of code that needs to be written but also makes it easier to update and maintain the codebase.

In addition to reducing code duplication, the DRY principle also promotes the concept of "Single Source of Truth" (SSOT). This means that if a piece of information or logic needs to be changed, it only needs to be updated in one place, ensuring consistency throughout the system.

Overall, the DRY principle emphasizes the importance of writing clean, concise, and reusable code, leading to more efficient development and easier maintenance of software systems.

Question 3: Explain Null vs Undefined in JavaScript?
In JavaScript, both null and undefined represent the absence of a value, but they have slightly different meanings and use cases.

undefined is a primitive value that is automatically assigned to a variable that has been declared but has not been assigned a value. It is also the default return value of a function that does not explicitly return anything. For example:

```
let x; // x is undefined because it has not been assigned a value
console.log(x); // Output: undefined

function foo() {
  // No return statement
}

console.log(foo()); // Output: undefined
```

On the other hand, null is a special value that represents the intentional absence of any object value. It is often used to indicate that a variable or property has no value or that an object reference is intentionally empty. For example:
```
let y = null; // y is explicitly assigned the value null
console.log(y); // Output: null

let obj = null; // obj is intentionally empty
console.log(obj); // Output: null
```

Here are a few key differences between null and undefined:

undefined is the default value for uninitialized variables, while null is an explicitly assigned value.
undefined is of type undefined, while null is of type object.
undefined is automatically assigned by JavaScript, while null needs to be explicitly assigned by the programmer.
undefined is often used to check if a variable has been assigned a value, while null is often used to indicate intentional absence of a value.
It's important to handle both null and undefined appropriately in your code to avoid unexpected behavior or errors.
