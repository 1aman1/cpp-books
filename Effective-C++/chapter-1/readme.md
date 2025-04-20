# Chapter 1: Accustoming Yourself to C++

This chapter introduces foundational practices for writing robust and modern C++ code. It helps set the mindset required to be effective with the language.

---

## ✅ Item 1: View C++ as a Federation of Languages

### 🔑 Key Idea:
C++ isn’t a single language — it's a federation of four:

1. **C** – Built-in types, arrays, pointers, manual memory.
2. **Object-Oriented C++** – Classes, inheritance, virtual functions.
3. **Template C++** – Generic programming and compile-time polymorphism.
4. **STL (Standard Template Library)** – Containers, algorithms, iterators, functors.

Each sublanguage has different best practices. Example:
- Use pass-by-value for C-style types.
- Prefer pass-by-const-reference for user-defined types.
- STL iterators behave like pointers → pass-by-value is fine.

### 📌 Takeaway:
> *Understand which sublanguage you're using. Adjust your coding approach accordingly.*

---

## ✅ Item 2: Prefer `const`, `enum`, and `inline` to `#define`

### 🔑 Key Idea:
Avoid `#define` for constants or macros. Prefer:
- `const` for values
- `enum` for scoped integral constants
- `inline` for macro-like functions

### 🧱 Examples:
```cpp
// Instead of this:
#define PI 3.14159

// Use this:
const double Pi = 3.14159;

// For class-scoped constants:
class Game {
    static const int MaxPlayers = 5;
};

// Or use enum hack:
class Game {
    enum { MaxPlayers = 5 };
};

// Inline function instead of macro:
inline int square(int x) { return x * x; }
```

### 📌 Takeaway:
> *Let the compiler manage constants and inlining. Avoid preprocessor complexity and hazards.*

---

## ✅ Item 3: Use `const` Whenever Possible

### 🔑 Key Idea:
`const` improves code safety and clarity. Use it:
- On function parameters and return values
- On member functions
- With pointers

### 🧱 Examples:
```cpp
void display(const std::string& name);
const std::string& getName() const;

const char* const title = "Book";
```

### 📌 Takeaway:
> *Default to `const`. Remove it only when mutation is needed.*

---

## ✅ Item 4: Make Sure That Objects Are Initialized Before They're Used

### 🔑 Key Idea:
Always initialize variables — especially in constructors. Prefer **initializer lists** over assignment.

### 🧱 Examples:
```cpp
// Good
int x = compute();

// In classes
class Point {
    int x, y;
public:
    Point(int a, int b) : x(a), y(b) {} // preferred
};
```

### 📌 Takeaway:
> *Initialize as early as possible. Use constructor initializer lists to avoid redundant or incorrect initialization.*

---

### 🔚 Chapter Summary

| Item | Summary |
|------|---------|
| 1 | Understand C++'s four sublanguages and their rules. |
| 2 | Prefer `const`, `enum`, and `inline` over `#define`. |
| 3 | Use `const` extensively for clarity and safety. |
| 4 | Ensure variables are initialized early, especially in constructors. |

---

✍️ *This summary is adapted from Scott Meyers' Effective C++ (3rd Edition).*