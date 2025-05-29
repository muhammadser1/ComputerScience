# Java - Object-Oriented Programming (OOP)

## 1. What is OOP?
Object-Oriented Programming (OOP) is a paradigm that organizes code using **objects**, which represent real-world entities. It is based on four core principles:

- **Encapsulation:** Bundling data and methods in a single unit and restricting direct access.
- **Abstraction:** Hiding complex details, exposing only relevant parts.
- **Inheritance:** One class inherits the properties and behaviors of another.
- **Polymorphism:** A method or object behaves differently in different contexts.

---

## 2. What is Encapsulation?
| Modifier          | Access Level                                                  | Example                |
|-------------------|---------------------------------------------------------------|------------------------|
| `public`          | Accessible from anywhere                                       | `public int number;`   |
| `private`         | Accessible only within the same class                         | `private int age;`     |
| `protected`       | Accessible within same package and subclasses                 | `protected String name;`|
| `default`         | Accessible within the same package (no modifier specified)    | `int id;`              |

---

## 3. What is Inheritance?
Inheritance allows a **subclass** to inherit the fields and methods of a **superclass**. Enables reuse, extension, and polymorphism.

---

## 4. Overloading vs Overriding
- **Overloading:** Same method name, different parameter types.
- **Overriding:** Subclass redefines superclass method.

---

## 5. `super` Keyword
Used to refer to the immediate superclass.
- Access superclass methods/variables.
- Call superclass constructors.

---

## 6. `this` Keyword
Refers to the current object.
- Access instance variables.
- Call other methods.
- Constructor chaining.
- Pass current object.

---

## 7. Static Variables and Static Methods

**Static Variables:**
- Shared among all instances.
- Use for constants and shared data.

**Static Methods:**
- Utility/helper functions.
- Factory methods (e.g., `getInstance()`).
- Can access static variables.

---

## 8. The `final` Keyword

| Usage             | Description                                     | Example                      |
|------------------|-------------------------------------------------|------------------------------|
| Final Variable    | Value cannot be changed                         | `final int MAX_AGE = 100;`   |
| Final Method      | Cannot be overridden                            | `final void show() {}`       |
| Final Class       | Cannot be extended                              | `final class Calculator {}`  |

---

## 9. Can a class extend multiple classes?
No. Java does **not support multiple inheritance** for classes to avoid ambiguity (Diamond Problem). Java uses **interfaces** instead.

---

## 10. What is Polymorphism?
Allows objects to behave differently based on context.

- **Compile-Time Polymorphism:** Method overloading.
- **Runtime Polymorphism:** Method overriding.

---

## 11. Abstraction vs Encapsulation

| Feature        | Encapsulation                        | Abstraction                        |
|----------------|---------------------------------------|-------------------------------------|
| Purpose        | Protect data                          | Hide complexity                     |
| How            | private variables + public methods    | abstract classes/interfaces         |
| Example        | `getters/setters`                     | `abstract void sound();`           |

```java
abstract class Animal {
    abstract void sound();
    void breathe() {
        System.out.println("Animal is breathing");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a = new Dog();
        a.sound(); // Dog barks
        a.breathe(); // Animal is breathing
    }
}
```

---

## 12. Abstract Class
- Cannot be instantiated.
- May contain abstract and concrete methods.
- May include static methods.

---

## 13. Can Abstract Classes Have Constructors?
Yes. Called when subclass object is created.

---

## 14. Why Use Abstract Classes?
- To share base behavior.
- To enforce method implementation.
- To allow partial abstraction.

---

## 15. Can We Instantiate Abstract Classes?
No, they are designed to be extended only.

---

## 16. Can an Interface Have a Constructor?
No. Interfaces are blueprints, not classes.

---

## 17. Interfaces
- Java 8+: Default and static methods allowed.
- Java 9+: Private methods allowed.

### Interface vs Abstract Class

| Aspect               | Interface                                 | Abstract Class                          |
|----------------------|-------------------------------------------|------------------------------------------|
| Purpose              | Define rules                              | Base class with common behavior          |
| Inheritance          | Multiple                                  | Single                                   |
| Methods              | Abstract + Default + Static               | Abstract + Concrete                      |
| Constructors         | ❌ No                                      | ✅ Yes                                   |
| Variables            | Public static final only                  | Can have instance variables              |
| State Management     | Not allowed                               | Allowed                                  |
| Use When             | Capabilities (e.g. Runnable)              | Base class reuse                         |

```java
interface Flyable {
    void fly();
    default void showFlyDetails() {
        System.out.println("Flyable Interface Default Method");
    }
    static void flyInfo() {
        System.out.println("Static Flyable Info");
    }
}

interface Runnable {
    void run();
    default void showRunDetails() {
        System.out.println("Runnable Interface Default Method");
    }
    static void runInfo() {
        System.out.println("Static Runnable Info");
    }
}

class Bird implements Flyable, Runnable {
    public void fly() { System.out.println("Bird is flying"); }
    public void run() { System.out.println("Bird is running"); }
    @Override
    public void showFlyDetails() {
        System.out.println("Bird flies with wings");
    }
}

public class Main {
    public static void main(String[] args) {
        Flyable.flyInfo();
        Runnable.runInfo();

        Bird b = new Bird();
        b.fly();                // Bird is flying
        b.run();                // Bird is running
        b.showFlyDetails();     // Overridden Default Method (Flyable)
        b.showRunDetails();     // Default Method (Runnable)

    }
}
```

---

## Why Use OOP?
✅ Modularity – Code is organized into classes.  
✅ Reusability – Inheritance promotes reuse.  
✅ Maintainability – Easy to update/extend code.  
✅ Encapsulation – Secure and bug-resistant design.  
✅ Abstraction – Focus on what, not how.  
✅ Polymorphism – Flexible, reusable code.

---

## Generics
Allows type-safe, reusable methods/classes. <T>

---

## Composition vs Inheritance
- **Inheritance:** "is-a" relationship.
- **Composition:** "has-a" relationship. (Preferred for flexibility)

---

## Serializable
Marks class for converting object into a byte stream (e.g., file/network).

---

## Object Methods: `equals`, `toString`, `clone`, `hashCode`

```java
class Person implements Cloneable {
    String name;

    Person(String name) {
        this.name = name;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // copy
    }
}

public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
        Person p1 = new Person("Ali");
        Person p2 = (Person) p1.clone();

        System.out.println(p1 == p2);                  // false
        System.out.println(p1.name.equals(p2.name));   // true
    }
}
```
