# AP CSA Cheat Sheet ☕📘

Each topic contains both the **Markdown (`.md`)** source and its exact matching **PDF (`.pdf`)** for easy downloading and printing:

---

## 📑 Documents & Direct Downloads

### 1. Compile Errors (CE) Guide
11 Most frequent Java compilation errors with definitions, causes, broken code, and verified fixes:
- 📄 **PDF**: **[common-compile-errors.pdf](./common-compile-errors.pdf)** (Print-ready)
- 📝 **Markdown**: **[common-compile-errors.md](./common-compile-errors.md)** (Raw / GitHub Markdown)

---

### 2. Key Concepts Checklist (Static vs. Non-Static #01)
Master review checklist for core AP CSA concepts:
- 📄 **PDF**: **[key-concepts-checklist.pdf](./key-concepts-checklist.pdf)** (Print-ready)
- 📝 **Markdown**: **[key-concepts-checklist.md](./key-concepts-checklist.md)** (Raw / GitHub Markdown)

---

### 3. Class Template (Write-a-Class-from-Scratch)
Complete annotated class skeleton, a six-step recipe for "write a class" questions, four variations (subclass, `ArrayList` field, array field, static utility), and the traps that cost points:
- 📄 **PDF**: **[class-template.pdf](./class-template.pdf)** (Print-ready)
- 📝 **Markdown**: **[class-template.md](./class-template.md)** (Raw / GitHub Markdown)

---

### 4. Writing Methods: Rules, Patterns & Traps
Method anatomy, return rules, parameter passing (the highest-value trap), shadowing, overloading vs overriding, six method patterns you actually write, recursion notes, and a trap table:
- 📄 **PDF**: **[method-writing-notes.pdf](./method-writing-notes.pdf)** (Print-ready)
- 📝 **Markdown**: **[method-writing-notes.md](./method-writing-notes.md)** (Raw / GitHub Markdown)

---

### 5. Keywords & Modifiers Reference
Every keyword the exam uses, grouped by job: access modifiers, `static`, `final`, `void`, `this`/`super`, `new`, `null`, `extends`, `return`, control flow, the combinations you type constantly, and a keyword-level trap table:
- 📄 **PDF**: **[keyword-reference.pdf](./keyword-reference.pdf)** (Print-ready)
- 📝 **Markdown**: **[keyword-reference.md](./keyword-reference.md)** (Raw / GitHub Markdown)

---

## 🚀 Quick Exam Tips
1. **Static vs. Non-Static**: `static` belongs to the Class (1 shared copy); non-static belongs to individual object instances created with `new`.
2. **Syntax Differences**:
   - Arrays: `arr.length` (variable, no `()`)
   - Strings: `str.length()` (method, with `()`)
   - ArrayLists: `list.size()` (method, with `()`)
3. **Integer Division**: `5 / 2 == 2`. Cast to double first if decimal is required: `(double) 5 / 2 == 2.5`.
4. **Strings are Immutable**: `str.toLowerCase()` produces a new string; it does NOT alter the original.
5. **ArrayList Removals**: Always iterate backwards (`for (int i = list.size() - 1; i >= 0; i--)`) when removing elements in a loop to avoid index skip bugs.
6. **Constructors Have No Return Type**: `public Student(String n)` — adding `void` breaks it (`invalid method declaration; return type required`).
7. **Parameters Are Copies**: for an object the copy is the *reference*. Mutating the object is visible to the caller; reassigning the parameter is not.
8. **`final` Does Not Freeze Contents**: `final int[] a` locks the reference, not the values — `a[0] = 5;` is still legal.

---
Created with GitDev Studio.
