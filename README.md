# AP CSA Cheat Sheet & Study Hub ☕📘

Comprehensive reference and study guide for **AP Computer Science A** (Java), covering core concepts, compilation errors, syntax rules, and exam strategies.

## 📑 Repository Structure
- **[Key Concepts Checklist (Static vs Non-Static First)](./key-concepts-checklist.md)**: Master checklist covering Static vs Non-Static, Polymorphism, References, ArrayList mechanics, 2D Arrays, Recursion, and Algorithms.
- **[Common Compile Errors (CE) Guide](./common-compile-errors.md)**: 11 most frequent Java compilation errors with clear definitions, causes, simple broken examples, and verified fixes.

## 🚀 Quick Exam Tips
1. **Static vs Instance**: `static` methods belong to the class, not an object. They cannot use `this` or access instance variables without creating an object instance.
2. **Syntax Trio**:
   - Arrays: `arr.length` (field, NO parentheses)
   - Strings: `str.length()` (method, WITH parentheses)
   - ArrayLists: `list.size()` (method, WITH parentheses)
3. **Integer Division**: `5 / 2 == 2`. Cast to double first if decimal is required: `(double) 5 / 2 == 2.5`.
4. **Strings are Immutable**: `str.toLowerCase()` produces a new string; it does NOT alter the original.
5. **ArrayList Removals**: Always iterate backwards (`for (int i = list.size() - 1; i >= 0; i--)`) when removing elements in a loop to avoid index skip bugs.

---
Created with GitDev Studio.
