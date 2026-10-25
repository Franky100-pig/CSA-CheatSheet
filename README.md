# AP CSA Cheat Sheet & Study Hub ☕📘

Comprehensive reference and printable study guide for **AP Computer Science A** (Java), covering core concepts, compilation errors, syntax rules, and exam strategies.

---

## 📥 Direct Downloads & Resources

| Format | Document | Description | Direct Link |
| :--- | :--- | :--- | :--- |
| 📄 **PDF** | **[AP-CSA-Study-Guide.pdf](./AP-CSA-Study-Guide.pdf)** | Print-ready, beautifully formatted master PDF with checklists & examples | **[⬇️ Download PDF](./AP-CSA-Study-Guide.pdf)** |
| 📝 **Markdown** | **[key-concepts-checklist.md](./key-concepts-checklist.md)** | Key Concepts Checklist (Static vs Non-Static #1, Polymorphism, etc.) | **[View / Raw .MD](./key-concepts-checklist.md)** |
| 📝 **Markdown** | **[common-compile-errors.md](./common-compile-errors.md)** | 11 Common Compile Errors with definitions, causes, & minimal fixes | **[View / Raw .MD](./common-compile-errors.md)** |

---

## 📑 Core Topics Summary

### 1. Key Concepts (Static vs. Non-Static First)
1. **Static vs. Non-Static (Class vs. Instance)**: `static` belongs to the Class (1 shared copy); non-static belongs to individual objects (`new`).
2. **Inheritance & Polymorphism**: Declared reference type determines compile-time methods; instantiated type determines runtime execution (Dynamic Binding).
3. **References & Aliasing**: `==` checks memory location identity. Always use `.equals()` for `String` content equality.
4. **1D Array vs. ArrayList<E>**: Fixed size (`arr.length`) vs. dynamic size (`list.size()`). Always iterate backwards (`i--`) when deleting elements.
5. **2D Arrays**: Row-major order (`grid[row][col]`). `grid.length` is rows; `grid[0].length` is cols.
6. **Recursion**: Must have base case. Code before recursive call runs on the way down; code after runs on the way back up.
7. **Search & Sort**: Binary Search ($O(\log n)$) **requires sorted data**. Selection, Insertion, and Merge Sort mechanics.
8. **Boolean Logic**: De Morgan's laws (`!(A && B) == !A || !B`) and short-circuit evaluation.

---

### 2. Common Compile Errors (CE)
- **`cannot find symbol`**: Out of scope, typo, or missing import (`ArrayList`, `Scanner`).
- **`lossy conversion from double to int`**: Decimal math without explicit cast `(int)`.
- **`variable might not have been initialized`**: Local variables in methods have no default values.
- **`missing return statement`**: Uncovered code paths in non-void methods.
- **`unreachable statement`**: Statements written after a guaranteed `return` or `break`.
- **`non-static method cannot be referenced from static context`**: Calling instance methods from `main` without creating an object.
- **`array required, but ArrayList found`**: Using `[]` on an `ArrayList`.
- **`constructor cannot be applied to given types`**: Calling constructor without matching parameter arguments.
- **`bad operand types for binary operator`**: Using `<` or `>` on `String` objects.
- **`'void' type not allowed here`**: Printing or assigning the result of a `void` method.
- **`class, interface, or enum expected`**: Unbalanced or extra curly braces `}`.

---
Created with GitDev Studio.
