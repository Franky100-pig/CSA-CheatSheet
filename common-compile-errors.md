# AP CSA Common Compile Errors (CE) Guide

A beginner-friendly cheat sheet for **AP Computer Science A** explaining what each Compile Error means, why it happens, with simple, minimal code examples and instant fixes.

---

## 1. cannot find symbol

### Definition
The compiler encounters a name (variable, method, or class) that it does not recognize in the current scope.

### Why It Happens
- You declared a variable inside an `if` or `for` block and tried to use it outside that block.
- A spelling typo or wrong capitalization (`totalScore` vs `totalscore`).
- Forgot to import a class (like `import java.util.ArrayList;`).

### Simple Example
```java
// ❌ BROKEN
for (int i = 0; i < 5; i++) {
    int secret = 42;
}
System.out.println(secret); // CE: cannot find symbol variable secret
```

### Simple Fix
Declare the variable before the block so it exists in the outer scope:
```java
// ✅ FIXED
int secret = 0;
for (int i = 0; i < 5; i++) {
    secret = 42;
}
System.out.println(secret); // OK: prints 42
```

---

## 2. incompatible types: possible lossy conversion from double to int

### Definition
You are trying to store a decimal number (`double`) into an integer variable (`int`), which would lose the fractional part.

### Why It Happens
- Java strictly forbids silent precision loss. Any calculation involving a decimal literal (like `3.0` or `Math.random()`) produces a `double`.

### Simple Example
```java
// ❌ BROKEN
int count = 5.8;     // CE: lossy conversion from double to int
int half = 10 / 4.0; // CE: 4.0 makes the result 2.5 (double)
```

### Simple Fix
Add an explicit cast `(int)` to deliberately truncate the decimal portion:
```java
// ✅ FIXED
int count = (int) 5.8;       // count becomes 5
int half = (int) (10 / 4.0); // half becomes 2
```

---

## 3. variable <var> might not have been initialized

### Definition
You tried to read or use a local variable before assigning it a value on every possible execution branch.

### Why It Happens
- Local variables inside methods do **not** receive default values (unlike class instance variables). If an `if` condition isn't met, the variable is left with no value.

### Simple Example
```java
// ❌ BROKEN
int grade;
int score = 75;
if (score >= 90) {
    grade = 1;
}
System.out.println(grade); // CE: variable grade might not have been initialized
```

### Simple Fix
Always provide a starting default value when declaring local variables:
```java
// ✅ FIXED
int grade = 0; // Initialized
int score = 75;
if (score >= 90) {
    grade = 1;
}
System.out.println(grade); // OK: prints 0
```

---

## 4. missing return statement

### Definition
A method promises to return a value (such as `int` or `boolean`), but there is a scenario where the method finishes without executing a `return` statement.

### Why It Happens
- Putting a `return` only inside an `if` block without an `else` or fallback at the end of the method.

### Simple Example
```java
// ❌ BROKEN
public boolean isPositive(int n) {
    if (n > 0) {
        return true;
    }
    // CE: missing return statement if n <= 0
}
```

### Simple Fix
Ensure every branch returns a value:
```java
// ✅ FIXED
public boolean isPositive(int n) {
    if (n > 0) {
        return true;
    }
    return false; // Fallback return
}

// Or even cleaner:
public boolean isPositive(int n) {
    return n > 0;
}
```

---

## 5. unreachable code / unreachable statement

### Definition
You wrote code directly after a line that already terminates the method or exits the loop (like `return` or `break`), so it can never be reached.

### Why It Happens
- Placing statements immediately after a `return` line.

### Simple Example
```java
// ❌ BROKEN
public int getMultiplier() {
    return 10;
    System.out.println("Returned"); // CE: unreachable statement
}
```

### Simple Fix
Move the statement before the `return`:
```java
// ✅ FIXED
public int getMultiplier() {
    System.out.println("Returned");
    return 10;
}
```

---

## 6. non-static method cannot be referenced from a static context

### Definition
You tried to call an ordinary instance method directly from `public static void main` without creating an object instance first.

### Why It Happens
- `static` methods belong to the class itself, not to any specific object. Non-static methods require an individual object to act upon.

### Simple Example
```java
// ❌ BROKEN
public class Player {
    public void jump() {
        System.out.println("Jumping!");
    }

    public static void main(String[] args) {
        jump(); // CE: non-static method jump() called from static main
    }
}
```

### Simple Fix
Instantiate the class first:
```java
// ✅ FIXED
public static void main(String[] args) {
    Player p = new Player();
    p.jump(); // OK: called on instance p
}
```

---

## 7. array required, but ArrayList found / Method vs Field Confusion

### Definition
You used array square brackets `[ ]` on an `ArrayList`, or tried to use `arr.length()` or `arr.get()` on a basic array.

### Why It Happens
- Standard arrays and `ArrayList` have completely different syntax:
  - **Array**: `arr[0]` and `arr.length` (field, NO parentheses!)
  - **ArrayList**: `list.get(0)` and `list.size()` (method, WITH parentheses!)

### Simple Example
```java
// ❌ BROKEN
ArrayList<String> list = new ArrayList<>();
list.add("Java");
System.out.println(list[0]);     // CE: array required, but ArrayList found
System.out.println(list.length); // CE: cannot find symbol variable length
```

### Simple Fix
Use the `ArrayList` methods:
```java
// ✅ FIXED
System.out.println(list.get(0)); // OK: prints Java
System.out.println(list.size());  // OK: prints 1
```

---

## 8. constructor in class cannot be applied to given types

### Definition
You called `new ClassName(...)` or `super(...)` with arguments that do not match any constructor declared in that class.

### Why It Happens
- Once you define a constructor that takes arguments, Java automatically removes the default zero-argument constructor `ClassName()`.

### Simple Example
```java
// ❌ BROKEN
class Student {
    public Student(String name) { ... } // Only constructor requires a String
}

Student s = new Student(); // CE: constructor Student cannot be applied to ()
```

### Simple Fix
Pass the required parameter:
```java
// ✅ FIXED
Student s = new Student("Franky"); // OK
```

---

## 9. bad operand types for binary operator (<, >, ==)

### Definition
You applied a mathematical or relational operator to objects that do not support it, such as using `<` on `String` objects.

### Why It Happens
- In Java, `<` and `>` only compare primitive numbers (`int`, `double`).
- Strings must be compared using `.equals()` (for equality) or `.compareTo()` (for alphabetical order).

### Simple Example
```java
// ❌ BROKEN
String s1 = "apple";
String s2 = "banana";
if (s1 < s2) { ... } // CE: bad operand types for binary operator '<'
```

### Simple Fix
Use `.compareTo()`:
```java
// ✅ FIXED
if (s1.compareTo(s2) < 0) {
    System.out.println(s1 + " comes before " + s2);
}
```

---

## 10. 'void' type not allowed here

### Definition
You tried to print, assign, or use the result of a method that has a `void` return type (meaning it returns nothing).

### Why It Happens
- Methods like `System.out.println(...)` or `list.clear()` do not return any data. You cannot print them or store them in a variable.

### Simple Example
```java
// ❌ BROKEN
ArrayList<String> list = new ArrayList<>();
System.out.println(list.clear()); // CE: 'void' type not allowed here
int x = System.out.println("hi");  // CE: 'void' type not allowed here
```

### Simple Fix
Call the void method as an independent statement:
```java
// ✅ FIXED
list.clear();                    // Separate statement
System.out.println("Cleared!"); // OK
```

---

## 11. class, interface, or enum expected

### Definition
An unexpected closing curly brace `}` closed your class prematurely, leaving subsequent methods floating outside the class boundaries.

### Why It Happens
- An extra or misplaced closing brace `}`.

### Simple Example
```java
// ❌ BROKEN
public class Demo {
    public static void main(String[] args) {
        System.out.println("Hi");
    }
} // Extra closing brace cuts off the class!

    public void doWork() {} // CE: class, interface, or enum expected
```

### Simple Fix
Keep all methods enclosed inside the class body:
```java
// ✅ FIXED
public class Demo {
    public static void main(String[] args) {
        System.out.println("Hi");
    }

    public void doWork() {} // Properly inside Demo
}
```
