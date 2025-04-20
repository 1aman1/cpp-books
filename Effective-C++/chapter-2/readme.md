
# Chapter 2: Constructors, Destructors, and Assignment Operators

This chapter dives deep into the life cycle of C++ objects. It emphasizes understanding what the compiler does implicitly and what you should handle explicitly to ensure correct, safe, and predictable behavior in constructors, destructors, and assignment operators.

## ✅ Item 5: Know What Functions C++ Silently Writes and Calls

C++ can automatically generate the following special member functions:
- Default constructor
- Copy constructor
- Copy assignment operator
- Destructor

🧠 **Tip**: If you don't declare these yourself, the compiler might do it for you — sometimes in ways that aren't ideal.

🔍 Be especially cautious with classes managing resources (e.g., dynamic memory). Compiler-generated copy semantics can lead to **double-deletes**, **shallow copies**, and **resource leaks**.

---

## ✅ Item 6: Explicitly Disallow the Use of Compiler-Generated Functions You Do Not Want

To prevent copying, declare the copy constructor and copy assignment operator as `deleted` (C++11+) or private and undefined (pre-C++11):

```cpp
class NonCopyable {
private:
    NonCopyable(const NonCopyable&);
    NonCopyable& operator=(const NonCopyable&);
};
```

Or in modern C++:
```cpp
class NonCopyable {
public:
    NonCopyable(const NonCopyable&) = delete;
    NonCopyable& operator=(const NonCopyable&) = delete;
};
```

🧠 **Tip**: Make design decisions explicit by deleting or declaring private any functions you don’t want used.

---

## ✅ Item 7: Declare Destructors Virtual in Polymorphic Base Classes

If a class has virtual functions, it must have a **virtual destructor**. Otherwise, deleting a derived object through a base pointer will cause undefined behavior.

```cpp
class Base {
public:
    virtual ~Base() {}; // Required if derived class might be deleted via Base*
};
```

🧠 **Tip**: Always make the destructor virtual in a class designed to be used polymorphically.

---

## ✅ Item 8: Prevent Exceptions from Leaving Destructors

Throwing an exception from a destructor during stack unwinding (when another exception is already propagating) causes `std::terminate()`.

```cpp
~Widget() {
    try {
        closeLog(); // may throw
    } catch (...) {
        // log the error but do not rethrow
    }
}
```

🧠 **Tip**: Destructors should never throw. Catch exceptions internally if needed.

---

## ✅ Item 9: Never Call Virtual Functions During Construction or Destruction

During construction and destruction, virtual dispatch does **not** work as expected — it calls functions for the current class only.

```cpp
class Base {
public:
    Base() { call(); } // dangerous: will not call overridden function
    virtual void call() {}
};

class Derived : public Base {
public:
    void call() override { /* won't be called during Base construction */ }
};
```

🧠 **Tip**: Avoid virtual calls in constructors and destructors — they break polymorphic behavior.

---

## ✅ Item 10: Have Assignment Operators Return a Reference to `*this`

This enables chained assignments like `a = b = c;`.

```cpp
class Widget {
public:
    Widget& operator=(const Widget& rhs) {
        // do assignment
        return *this;
    }
};
```

🧠 **Tip**: Follow established conventions — always return `*this` from `operator=`.

---

## ✅ Item 11: Handle Assignment to Self in `operator=`

Assignment must be safe even if `a = a;`. Check for self-assignment or design code to handle it safely.

```cpp
if (this == &rhs) return *this;
```

Or use the **copy-and-swap idiom**, which naturally handles self-assignment.

🧠 **Tip**: Protect against self-assignment to avoid bugs and crashes.

---

## ✅ Item 12: Copy All Parts of an Object

Don’t forget to copy all data members, including base class parts:

```cpp
Widget& operator=(const Widget& rhs) {
    Base::operator=(rhs); // copy base part
    data = rhs.data;      // copy member
    return *this;
}
```

🧠 **Tip**: Copy every piece — including base classes and all data members.

---

## 📌 Summary

| Item | Key Point |
|------|-----------|
| 5 | Understand which functions the compiler generates and when |
| 6 | Explicitly delete or block unwanted compiler-generated functions |
| 7 | Make destructors virtual in polymorphic base classes |
| 8 | Never let exceptions escape destructors |
| 9 | Avoid virtual calls in constructors/destructors |
| 10 | Return `*this` from assignment operators |
| 11 | Handle self-assignment in `operator=` |
| 12 | Copy all parts of the object, including base class and members |

These rules ensure that objects are safe to construct, copy, assign, and destroy, especially when they manage resources like memory, files, or locks.
