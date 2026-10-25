# AP CSA Cheat Sheet ☕📘

Comprehensive reference and study guide for **AP Computer Science A** (Java), covering common compilation errors, syntax pitfalls, OOP guidelines, arrays/ArrayList mechanics, and test-taking tips.

## 📑 Contents
- **[Common Compile Errors & Solutions](./common-compile-errors.md)**: Detailed breakdown of Java compilation errors commonly seen in AP CSA exams and labs with causes and code fixes.
- **Java Basics & Type Rules**: Primitives vs Objects, casting, and scope.
- **Object-Oriented Programming**: `class`, `super()`, inheritance, and polymorphism.
- **Standard Library**: `String`, `Math`, `ArrayList<E>`, and wrapper classes.

## 🚀 Quick Exam Tips
1. In Java, array lengths are a field (`arr.length`), String lengths are a method (`str.length()`), and ArrayList sizes are a method (`list.size()`).
2. Integer division truncates towards zero (`5 / 2 == 2`). Cast to double before division if decimals are needed (`(double) 5 / 2 == 2.5`).
3. Always check loop bounds: `for (int i = 0; i <= arr.length; i++)` throws `ArrayIndexOutOfBoundsException`. Use `i < arr.length`.
4. Remember that `String` objects are immutable—methods like `toLowerCase()` or `substring()` return a **new** String and do not modify the original.

---
Created with GitDev Studio.
