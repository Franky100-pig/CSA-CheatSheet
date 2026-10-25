# Common Java Compile Errors in AP Computer Science A

This guide covers the most frequent compiler errors encountered by AP CSA students, explaining what causes each error, showing realistic broken code examples, and providing the corrected solution.

---

## 1. cannot find symbol

### Cause
The Java compiler does not recognize an identifier (variable name, method, or class). Common reasons:
- Variable was declared in an inner scope (such as inside an `if` block or `for` loop) and referenced outside.
- Typo in variable or method name (Java is strictly case-sensitive: `totalSum` vs `totalsum`).
- Forgetting to import standard classes (e.g. `import java.util.ArrayList;` or `import java.util.Scanner;`).
- Calling a method that is not declared on the target class.

### Broken Example
```java
public class ScopeTest {
    public static void main(String[] args) {
        if (args.length > 0) {
            int maxScore = 100;
        }
        // ERROR: cannot find symbol variable maxScore
        System.out.println("Max: " + maxScore);
    }
}
```

### Fix
Declare the variable in the outer scope:
```java
public class ScopeTest {
    public static void main(String[] args) {
        int maxScore = 0;
        if (args.length > 0) {
            maxScore = 100;
        }
        System.out.println("Max: " + maxScore); // OK
    }
}
```

---

## 2. incompatible types: possible lossy conversion

### Cause
Assigning a value with wider range or precision (e.g. `double` or `float`) to a narrower type (e.g. `int`) without an explicit cast.

### Broken Example
```java
int avg = (90 + 85 + 88) / 3.0; // 3.0 makes the expression double!
int rounded = 4.99;             // ERROR: possible lossy conversion from double to int
```

### Fix
Use an explicit narrowing cast `(int)`:
```java
int avg = (int) ((90 + 85 + 88) / 3.0);
int rounded = (int) 4.99; // Truncates to 4
```

---

## 3. variable <var> might not have been initialized

### Cause
Local variables in methods have **no default value**. If there is any path through conditional statements where the variable could be unassigned before being used, the compiler rejects the program.

### Broken Example
```java
public int calculateGrade(int score) {
    int grade;
    if (score >= 90) {
        grade = 4;
    } else if (score >= 80) {
        grade = 3;
    }
    // If score < 80, grade is never initialized!
    return grade; // ERROR: variable grade might not have been initialized
}
```

### Fix
Assign a default initial value:
```java
public int calculateGrade(int score) {
    int grade = 0; // Initialized
    if (score >= 90) {
        grade = 4;
    } else if (score >= 80) {
        grade = 3;
    }
    return grade;
}
```

---

## 4. missing return statement

### Cause
In a method with a non-`void` return type, the compiler verifies that all possible control paths end with a `return` statement.

### Broken Example
```java
public boolean isEven(int n) {
    if (n % 2 == 0) {
        return true;
    }
    // ERROR: missing return statement for odd numbers
}
```

### Fix
Provide a fallback return or simplify:
```java
public boolean isEven(int n) {
    return n % 2 == 0;
}
```

---

## 5. unreachable code / unreachable statement

### Cause
Statements placed after a guaranteed `return`, `throw`, or infinite loop without a `break`.

### Broken Example
```java
public int getMultiplier() {
    return 2;
    System.out.println("Returned"); // ERROR: unreachable statement
}
```

### Fix
Remove or relocate the unreachable statement before the return.

---

## 6. non-static method cannot be referenced from a static context

### Cause
Calling an instance method or accessing an instance variable directly from `public static void main` or any other `static` method without an object instance.

### Broken Example
```java
public class StudentRecord {
    private String name = "Franky";

    public void printName() {
        System.out.println(name);
    }

    public static void main(String[] args) {
        printName(); // ERROR: non-static method printName() cannot be referenced from static context
    }
}
```

### Fix
Instantiate the class first:
```java
public static void main(String[] args) {
    StudentRecord s = new StudentRecord();
    s.printName(); // OK: called on instance
}
```

---

## 7. array required, but ArrayList found / Method vs Field Confusion

### Cause
Confusing 1D/2D array bracket syntax (`[]`) with `ArrayList` methods (`.get()`, `.set()`, `.size()`).

### Cheat Sheet Comparison
| Operation | Standard Array | `ArrayList<E>` |
| :--- | :--- | :--- |
| Size/Count | `arr.length` (field, NO parentheses) | `list.size()` (method, WITH parentheses) |
| Read element | `arr[i]` | `list.get(i)` |
| Write element | `arr[i] = val;` | `list.set(i, val);` |
| Add new item | Not supported (fixed capacity) | `list.add(val);` |

### Broken Example
```java
ArrayList<String> roster = new ArrayList<>();
roster.add("Franky");
System.out.println(roster[0]);     // ERROR: array required, but ArrayList found
System.out.println(roster.length); // ERROR: cannot find symbol variable length
```

### Fix
```java
System.out.println(roster.get(0)); // OK
System.out.println(roster.size()); // OK
```

---

## 8. constructor <SuperClass> in class <SuperClass> cannot be applied to given types

### Cause
In inheritance, subclass constructors implicitly call `super()` with no arguments as their first action. If the superclass defines a constructor with parameters and NO default no-arg constructor, Java reports a constructor mismatch.

### Broken Example
```java
class Animal {
    private String species;
    public Animal(String species) { // Only constructor requires String
        this.species = species;
    }
}

class Dog extends Animal {
    public Dog() {
        // Implicit super(); fails here!
    }
}
```

### Fix
Explicitly invoke `super(...)` with the required parameters as the **very first line** of the constructor:
```java
class Dog extends Animal {
    public Dog() {
        super("Canine"); // Explicit call to superclass constructor
    }
}
```

---

## 9. bad operand types for binary operator

### Cause
Applying comparison operators (`<`, `>`, `<=`, `>=`) to `String` objects or other references, or comparing string contents with `==` instead of `.equals()`.

### Broken Example
```java
String s1 = "cat";
String s2 = "dog";
if (s1 < s2) { ... } // ERROR: bad operand types for binary operator '<'
```

### Fix
Use `.compareTo()` or `.equals()`:
```java
if (s1.compareTo(s2) < 0) {
    System.out.println(s1 + " comes before " + s2);
}
```

---

## 10. class, interface, or enum expected

### Cause
Almost always caused by mismatched curly braces (`{` and `}`), such as closing a class prematurely before methods are defined.

### Fix
Check brace indentation and ensure every opening brace has a matching closing brace at the appropriate scope level.
