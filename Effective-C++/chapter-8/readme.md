# Chapter 8: Customizing `new` and `delete`

This chapter covers how and when to customize memory allocation in C++. It explains how to override `new` and `delete` operators, and the rules and responsibilities associated with doing so safely and consistently.

---

## ✅ Item 45: Use `operator new` and `operator delete` for Fine-Grained Control of Memory Allocation

Overloading `operator new`/`delete` allows you to customize memory behavior for performance, debugging, or tracking.

```cpp
void* Widget::operator new(std::size_t size) {
    std::cout << "Allocating Widget\n";
    return ::operator new(size);
}

void Widget::operator delete(void* ptr) {
    std::cout << "Deallocating Widget\n";
    ::operator delete(ptr);
}
```

🧠 **Tip**: Only overload these when you need control — like memory pooling or logging.

---

## ✅ Item 46: Define `operator new` and `operator delete` in Pairs

If you overload `operator new`, you **must** also overload `operator delete`, or memory leaks and undefined behavior can result.

Same goes for:
- `operator new[]` ⇔ `operator delete[]`
- Placement new ⇔ corresponding placement delete

```cpp
class Widget {
public:
    void* operator new(std::size_t size);
    void operator delete(void* ptr);
};
```

🧠 **Tip**: Always define `delete` alongside `new` to match every allocation path with a safe deallocation.

---

## ✅ Item 47: Use a `custom new-handler` When `operator new` Fails

When memory allocation fails, you can install a custom handler to clean up or report before throwing `std::bad_alloc`.

```cpp
void outOfMem() {
    std::cerr << "Out of memory!" << std::endl;
    std::abort();
}

std::set_new_handler(outOfMem);
```

🧠 **Tip**: Set a new-handler to gracefully manage allocation failures.

---

## ✅ Item 48: Write `placement delete` If You Write `placement new`

When you write a custom `placement new`, you must write a matching `placement delete` in case constructor throws after memory is allocated.

```cpp
class Widget {
public:
    void* operator new(std::size_t, void* ptr) noexcept { return ptr; }
    void operator delete(void*, void*) noexcept { /* do nothing */ }
};
```

🧠 **Tip**: If constructor throws, `delete` must still run — define placement delete.

---

## ✅ Item 49: Understand the Behavior of the `new` and `delete` Operators in Relation to Inheritance

When you delete an object via a base class pointer, if the base class doesn't have a **virtual destructor**, the derived part won’t be destroyed — leading to memory leaks or undefined behavior.

```cpp
class Base {
public:
    virtual ~Base(); // crucial for safe polymorphic deletion
};
```

🧠 **Tip**: Always make destructors virtual in base classes meant for polymorphism.

---

## 📌 Summary

| Item | Key Point |
|------|-----------|
| 45 | Overload `new` and `delete` only for valid, performance-critical reasons |
| 46 | Always define `operator delete` alongside any custom `operator new` |
| 47 | Use `set_new_handler` to handle allocation failures gracefully |
| 48 | If you define placement new, also define placement delete |
| 49 | Always declare destructors `virtual` in base classes intended for inheritance |

Customizing `new` and `delete` provides powerful control over memory — but also introduces risk. Follow strict conventions to ensure correctness and maintainability.
