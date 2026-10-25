# AP CSA Key Concepts Checklist ☕📋

Master checklist of high-yield core concepts tested on the **AP Computer Science A** exam. Check off each concept as you review!

---

## [ ] 1. Static vs. Non-Static (Class vs. Instance) — *Top Priority*

### 🔑 Core Definition
- **`static` (Class-level)**: Belong to the **Class** as a whole. Exactly ONE shared copy exists in memory, regardless of how many objects are instantiated.
- **Non-Static (Instance-level)**: Belong to an **individual object**. Every object created with `new` gets its own separate copy of non-static variables.

### 📊 Quick Comparison Matrix
| Feature | `static` (Class) | Non-Static (Instance) |
| :--- | :--- | :--- |
| **Belongs to** | The Class itself | A specific object instance |
| **How to call** | `ClassName.method()` | `objectName.method()` |
| **Memory allocation** | 1 copy shared by all instances | Unique copy for every instance created with `new` |
| **Access to `this`** | ❌ Cannot use `this` keyword | ✅ Has access to `this` |
| **Access to instance vars** | ❌ Cannot access without an object | ✅ Can access directly |
| **AP CSA Examples** | `Math.random()`, `Math.sqrt()`, `Integer.MAX_VALUE` | `str.substring()`, `list.add()`, `myCar.drive()` |

### 💡 AP Exam Traps
1. **Calling instance methods from `main`**: `main` is `static`. Calling `display()` inside `main` without `new MyClass().display()` causes: *"non-static method cannot be referenced from a static context"*.
2. **Static Counter Trap**: If a class has `private static int count = 0;` and constructor increments `count++`, `count` tracks the *total* objects created across the entire program.
3. **Static Mutability**: Modifying a static variable from object A affects object B!

```java
public class Student {
    private String name;           // Instance variable (each student has their own)
    private static int totalStudents = 0; // Static variable (shared counter)

    public Student(String name) {
        this.name = name;
        totalStudents++; // Shared counter increments for each new student
    }

    public static int getTotalStudents() { // Static method
        return totalStudents;
        // return this.name; // CE: Cannot use 'this' or instance vars here!
    }
}
```

---

## [ ] 2. Inheritance & Polymorphism

### 🔑 Core Rules
- **`extends`**: A subclass inherits all public and protected methods/fields from its superclass.
- **`super()`**: Calls the superclass constructor. **Must be the very first line** of the subclass constructor.
- **Method Overriding**: Subclass writes a method with the exact same signature (name and parameter types) to replace the superclass behavior.
- **Polymorphism Rule**:
  `SuperType obj = new SubType();`
  1. **Compile-time check**: The compiler checks if the method exists in the **declared reference type** (`SuperType`). If not, it won't compile!
  2. **Runtime execution**: At runtime, Java executes the method in the **actual instantiated object's class** (`SubType`). This is *Dynamic Binding*.

```java
class Animal {
    public void speak() { System.out.println("Sound"); }
}
class Dog extends Animal {
    public void speak() { System.out.println("Bark"); }
    public void fetch() { System.out.println("Ball"); }
}

Animal a = new Dog(); // Polymorphic declaration
a.speak(); // OK: Prints "Bark" (dynamic method dispatch)
// a.fetch(); // CE: Animal class does not have fetch()!
((Dog) a).fetch(); // OK: Downcast permits fetch()
```

---

## [ ] 3. References, Aliasing & `==` vs. `.equals()`

### 🔑 Core Rules
- **Primitives** (`int`, `double`, `boolean`): Variable holds the *literal value*. `==` checks if the two values are identical.
- **Objects** (`String`, `ArrayList`, custom objects): Variable holds a **memory address (reference)** pointing to the object in heap memory.
- **The `==` Trap**: On objects, `==` checks whether two references point to the **same memory location**, NOT whether their contents match!
- **Aliasing**: `Dog d2 = d1;` does NOT duplicate the dog; it creates a second pointer pointing to the exact same dog object!

```java
String s1 = new String("hello");
String s2 = new String("hello");
System.out.println(s1 == s2);      // FALSE (different memory addresses)
System.out.println(s1.equals(s2));  // TRUE (same sequence of characters)
```

---

## [ ] 4. Array vs. `ArrayList<E>` Mastery

### 📊 Essential Differences
| Operation | 1D Array (`int[]`) | `ArrayList<String>` |
| :--- | :--- | :--- |
| **Size Capacity** | Fixed at creation (`new int[5]`) | Dynamic (grows/shrinks automatically) |
| **Holds Primitives?** | Yes (`int`, `double`) | No (auto-boxed to `Integer`, `Double`) |
| **Length/Count** | `arr.length` (field, NO `()`) | `list.size()` (method, WITH `()`) |
| **Read Index** | `arr[i]` | `list.get(i)` |
| **Modify Index** | `arr[i] = val;` | `list.set(i, val);` |
| **Add Element** | N/A | `list.add(val)` or `list.add(index, val)` |
| **Remove Element** | N/A | `list.remove(index)` (shifts remaining left!) |

### 💡 Concurrent Modification / Index Shift Trap
When removing items from an `ArrayList` in a loop, elements shift to the left:
```java
// ❌ WRONG: Skips consecutive matching elements!
for (int i = 0; i < list.size(); i++) {
    if (list.get(i).equals("delete")) {
        list.remove(i); // shifts elements, next element skipped!
    }
}

// ✅ CORRECT: Traverse backwards from end to index 0!
for (int i = list.size() - 1; i >= 0; i--) {
    if (list.get(i).equals("delete")) {
        list.remove(i); // Safe, elements shift into already-checked indices
    }
}
```

---

## [ ] 5. 2D Arrays & Matrix Traversal

### 🔑 Core Rules
- 2D arrays in Java are **arrays of arrays** organized in **Row-Major Order** (`grid[row][col]`).
- **Number of Rows**: `grid.length`
- **Number of Columns**: `grid[0].length`
- **Outer loop** = rows (`r`), **Inner loop** = columns (`c`).

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};
// matrix.length == 2 (rows)
// matrix[0].length == 3 (cols)

// Standard Row-Major Traversal:
for (int r = 0; r < matrix.length; r++) {
    for (int c = 0; c < matrix[r].length; c++) {
        System.out.print(matrix[r][c] + " ");
    }
}
```

---

## [ ] 6. Recursion & Base Case Tracing

### 🔑 Core Rules
1. **Base Case**: The stopping condition that does NOT make a recursive call. If missing or unreachable, causes `StackOverflowError`.
2. **Recursive Call**: The step that calls the method with smaller/simpler input, moving closer to the base case.
3. **Execution Order**: Code *before* the recursive call executes on the way DOWN the stack. Code *after* the recursive call executes on the way BACK UP.

```java
public static int mystery(int n) {
    if (n <= 1) return 1; // Base case
    return n + mystery(n - 1); // Recursive call: mystery(4) = 4 + 3 + 2 + 1 = 10
}
```

---

## [ ] 7. Search & Sort Algorithms (Big-O & Mechanics)

| Algorithm | Best / Worst Case | Key Mechanic on AP Exam |
| :--- | :--- | :--- |
| **Sequential (Linear) Search** | O(1) / O(n) | Works on unsorted or sorted data; inspects element by element. |
| **Binary Search** | O(1) / O(log n) | **REQUIRES SORTED DATA!** Compares target with middle element, cuts search space in half each iteration. |
| **Selection Sort** | O(n^2) | Repeatedly finds minimum from unsorted portion and swaps into front. Smallest number of swaps (n-1). |
| **Insertion Sort** | O(n) best / O(n^2) | Inserts each item into its correct sorted position in already-sorted portion. Fast if mostly sorted. |
| **Merge Sort** | O(n log n) always | Divide-and-conquer; recursive split into halves, then merges sorted sublists. Requires auxiliary memory. |

---

## [ ] 8. Boolean Logic & De Morgan's Laws

### 🔑 Core Rules
1. **De Morgan's Laws**:
   - `!(A && B)` is logically equivalent to `(!A || !B)`
   - `!(A || B)` is logically equivalent to `(!A && !B)`
2. **Relational Negations**:
   - Opposite of `<` is `>=` (do NOT forget the equal sign!)
   - Opposite of `>` is `<=`
   - Opposite of `==` is `!=`
3. **Short-Circuit Evaluation**:
   - In `A && B`, if `A` is `false`, `B` is NEVER evaluated. (Prevents NullPointer: `if (str != null && str.length() > 0)`).
   - In `A || B`, if `A` is `true`, `B` is NEVER evaluated.
