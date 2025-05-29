# Java - Exception Handling

## 1. What is an Exception? How is it different from an Error?

An **Exception** is an unwanted or unexpected event that occurs during the execution of a program.

| Aspect             | Exception                                                       | Error                                                   |
|--------------------|------------------------------------------------------------------|----------------------------------------------------------|
| Definition         | An abnormal condition that can be caught and handled.           | A serious issue that indicates a problem in the JVM/system. |
| Type               | Part of `java.lang.Exception` class hierarchy.                  | Part of `java.lang.Error` class hierarchy.              |
| Recoverability     | Typically recoverable.                                           | Generally not recoverable.                              |
| Common Causes      | Incorrect input, null values, division by zero.                 | `OutOfMemoryError`, `StackOverflowError`, `VirtualMachineError`. |
| Handling Mechanism | Handled using `try`, `catch`, `finally`.                        | Should not be handled; usually fatal.                   |

### Why Exception Handling is Important

Exception handling improves code quality, prevents crashes, and eases debugging. Java handles exceptions using:
- `try`
- `catch`
- `finally`
- `throw` / `throws`

---

## 2. What are Checked and Unchecked Exceptions?

### Unchecked Exceptions (Runtime Exceptions)
- Any exception that extends `RuntimeException`.
- Considered bugs and must be fixed by the developer.
- Not checked by the compiler.

**Examples:** `NullPointerException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException`

### Checked Exceptions (Compilation Exceptions)
- Any exception that does **not** extend `RuntimeException`.
- Must be declared and handled (checked by the compiler).
- Often user-defined exceptions.

**Examples:** `IOException`, `SQLException`, `ClassNotFoundException`

### Errors
- Serious problems (e.g., hardware or JVM failure).
- Not meant to be caught or handled.

---

## 3. Example

```java
public class Main {
    public static void main(String[] args) {
        try {
            System.out.println("Starting the program...");

            // ArithmeticException (divide by zero)
            int result = 10 / 0;
            System.out.println("Result: " + result);

            // NullPointerException
            String str = null;
            System.out.println(str.length());

            // ArrayIndexOutOfBoundsException
            int[] arr = {1, 2, 3};
            System.out.println(arr[5]);

        } catch (ArithmeticException e) {
            System.out.println("Error: Arithmetic Exception - " + e.getMessage());
        } catch (NullPointerException e) {
            System.out.println("Error: Null Pointer Exception - " + e.getMessage());
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Error: Array Index Out of Bounds - " + e.getMessage());
        } finally {
            System.out.println("Finally block always runs (Cleanup).");
        }

        System.out.println("Program continues after try-catch-finally.");
    }
}
```

**Output:**
```
Starting the program...
Error: Arithmetic Exception - / by zero
Finally block always runs (Cleanup).
Program continues after try-catch-finally.
```

---

## 4. Methods for Exception Information

| Method            | Description |
|-------------------|-------------|
| `getMessage()`    | Displays a user-friendly error message. |
| `getCause()`      | Identifies the root cause of a chained exception. |
| `printStackTrace()` | Debugging: shows full error location and stack trace. |

---

## 5. `throw` vs `throws`

- `throw`: Used to manually create and throw an exception.
- `throws`: Declared in a method signature to indicate it might throw an exception.

---

## 6. Full Example with Custom Exception

```java
// Custom Exception Class
class SpecialValueException extends Exception {
    public SpecialValueException(String message) {
        super(message);
    }
}

public class DivisionAdvancedExample {

    // Method that throws exceptions
    public static double divide(int a, int b) throws ArithmeticException, SpecialValueException {
        if (b == 0) {
            throw new ArithmeticException("Cannot divide by zero.");
        }

        if (b == 10) {
            throw new SpecialValueException("Division by 10 is not allowed.");
        }

        return (double) a / b;
    }

    public static void main(String[] args) {
        try {
            System.out.println("Result 1: " + divide(20, 2));  // 10.0
            System.out.println("Result 2: " + divide(20, 0));  // Error
            System.out.println("Result 3: " + divide(20, 10)); // Error

        } catch (ArithmeticException e) {
            System.out.println("Arithmetic Error: " + e.getMessage());
        } catch (SpecialValueException e) {
            System.out.println("Special Value Error: " + e.getMessage());
        }
    }
}
```

---
