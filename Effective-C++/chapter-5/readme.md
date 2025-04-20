# Chapter 5: Implementations

This chapter dives into best practices for implementing your classes and functions. It emphasizes writing efficient, safe, and maintainable code, especially focusing on details like casting, inline functions, scoping, and exception safety.

---

## ✅ Item 26: Postpone Variable Definitions as Long as Possible

Define variables close to where they're used. This improves readability and performance.

```cpp
for (int i = 0; i < n; ++i) {
    std::string result = process(i); // declare here, not at the top of the function
}
```

🧠 **Tip**: Delay declaration to limit variable scope and optimize performance.

---

## ✅ Item 27: Minimize Casting

Avoid casting whenever possible. If you must cast, prefer `static_cast`, `dynamic_cast`, `const_cast`, or `reinterpret_cast` over C-style casts.

```cpp
// Prefer this
Base* base = static_cast<Base*>(derivedPtr);

// Not this
Base* base = (Base*)derivedPtr;
```

🧠 **Tip**: C-style casts are unsafe and can silently do the wrong thing.

---

## ✅ Item 28: Avoid Returning "Handles" to Object Internals

Don't expose raw pointers or references to internal members (especially data members) from your class.

```cpp
class Widget {
private:
    std::vector<int> data;
public:
    // ❌ Bad: exposes internal state directly
    std::vector<int>& getData();

    // ✅ Better: return a copy or provide access via functions
    int getItem(size_t index) const;
};
```

🧠 **Tip**: Avoid breaking encapsulation by leaking internal representations.

---

## ✅ Item 29: Strive for Exception-Safe Code

Ensure your code offers one of the three levels of exception safety:
1. **No-throw guarantee**
2. **Strong guarantee** (rollback semantics)
3. **Basic guarantee** (no resource leaks or corruption)

Use RAII, smart pointers, and `swap` to manage exceptions effectively.

🧠 **Tip**: Always ask: “What happens if an exception is thrown here?”

---

## ✅ Item 30: Understand the Ins and Outs of Inlining

Inlining can improve performance by eliminating function call overhead, but it can also:
- Increase code size
- Harm compile times
- Obscure binary interfaces in libraries

```cpp
inline int square(int x) { return x * x; }
```

🧠 **Tip**: Use `inline` for small, frequently called functions — but don’t abuse it.

---

## 📌 Summary

| Item | Key Point |
|------|-----------|
| 26 | Define variables close to where they’re used |
| 27 | Avoid casts; use the C++ cast operators when necessary |
| 28 | Don’t expose internal object state via references or pointers |
| 29 | Always write exception-safe code; understand the different safety levels |
| 30 | Use `inline` judiciously — not every small function should be inlined |

By following these practices, you write cleaner, safer, and more efficient implementations — avoiding subtle bugs and performance pitfalls.
