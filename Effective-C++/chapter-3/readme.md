
# Chapter 3: Resource Management

This chapter focuses on techniques for managing dynamically allocated resources safely and efficiently. C++ supports fine-grained control of memory, and with that power comes the responsibility to manage resources correctly, especially when using pointers, file handles, sockets, etc.

## ✅ Item 13: Use Objects to Manage Resources

Use the RAII (Resource Acquisition Is Initialization) idiom: encapsulate resource management in an object whose constructor acquires the resource and whose destructor releases it.

Example using smart pointer:
```cpp
std::shared_ptr<Investment> pInv(createInvestment());
```

🧠 **Tip**: Let objects handle the acquire and release to avoid leaks and ensure exception safety.

---

## ✅ Item 14: Think Carefully About Copying Behavior in Resource-Managing Classes

Decide whether a class should be copyable. If copying doesn't make sense (e.g., ownership semantics), then disable copy constructor and assignment operator.

For unique ownership (like `std::unique_ptr`), copying is disabled and moving is used instead.

🧠 **Tip**: Define or delete copy/move operations intentionally when your class manages a resource.

---

## ✅ Item 15: Provide Access to Raw Resources in Resource-Managing Classes

Sometimes, you need access to the raw pointer or file descriptor. Provide it safely through a member function like `get()`:

```cpp
std::shared_ptr<Widget> sp;
Widget* p = sp.get(); // non-owning pointer
```

🧠 **Tip**: Allow access to raw resources, but clarify ownership semantics.

---

## ✅ Item 16: Use the Same Form in Corresponding Uses of `new` and `delete`

Always match `new` with `delete` and `new[]` with `delete[]`.

```cpp
int* arr = new int[10];
delete[] arr; // not delete!
```

🧠 **Tip**: Mixing `new`/`delete` forms causes undefined behavior. Be precise.

---

## ✅ Item 17: Store `new`ed Objects in Smart Pointers in Standalone Statements

Don't pass raw pointers into smart pointers in the same statement that allocates them:

```cpp
std::shared_ptr<Widget> sp(new Widget()); // ✅ OK
```

Avoid this:
```cpp
process(std::shared_ptr<Widget>(new Widget())); // ❌ risky if process throws
```

🧠 **Tip**: To avoid leaks during construction, separate `new` from smart pointer wrapping.

---

## 📌 Summary

| Item | Key Point |
|------|-----------|
| 13 | Use RAII: let objects manage the lifetime of resources |
| 14 | Explicitly manage copying semantics in resource-owning classes |
| 15 | Provide safe access to raw resources when needed |
| 16 | Match `new` with `delete`, and `new[]` with `delete[]` |
| 17 | Wrap `new`ed resources in smart pointers using separate statements |

Resource leaks and dangling pointers are major sources of bugs in C++. RAII and smart pointers are the keys to safe and efficient resource management.
