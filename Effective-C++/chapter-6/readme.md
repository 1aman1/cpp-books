# Chapter 6: Inheritance and Object-Oriented Design

This chapter focuses on how to properly use inheritance, virtual functions, and polymorphism in C++. It emphasizes designing base classes carefully, avoiding common pitfalls in inheritance, and understanding dynamic behavior in class hierarchies.

---

## ✅ Item 31: Make Sure Public Inheritance Models “Is-A”

Only use public inheritance when the derived class truly **“is a”** kind of the base class. This ensures substitutability.

```cpp
class Bird {
public:
    virtual void fly();
};

class Sparrow : public Bird {}; // ✅ Sparrow is-a Bird

class Engine {};
class Car : public Engine {};   // ❌ Car is-not an Engine
```

🧠 **Tip**: Use public inheritance only when you intend polymorphic substitution (Liskov Principle).

---

## ✅ Item 32: Avoid Inheriting from Classes That Were Not Designed to Be Base Classes

If a class lacks a virtual destructor or virtual functions, it’s not meant to be used as a base class.

```cpp
class Timer {
    // No virtual destructor → unsafe to derive from
};
```

🧠 **Tip**: Don’t inherit from a class unless it's explicitly designed for inheritance.

---

## ✅ Item 33: Avoid Hiding Inherited Names

Name hiding can occur when a derived class declares a function or member that shares a name with something in the base class — even if the signatures differ.

```cpp
class Base {
public:
    int size() const;
};

class Derived : public Base {
public:
    void size(int); // hides Base::size()
};
```

To bring base versions back into scope:
```cpp
using Base::size;
```

🧠 **Tip**: Be aware of name hiding and restore hidden base members explicitly.

---

## ✅ Item 34: Differentiate Between Inheritance of Interface and Inheritance of Implementation

- **Interface inheritance**: Base class declares functions only.
- **Implementation inheritance**: Base provides reusable functionality.

Use pure virtual functions (`= 0`) for interface inheritance.

```cpp
class Shape {
public:
    virtual void draw() const = 0; // pure virtual → interface
};
```

🧠 **Tip**: Be intentional — inherit interfaces when you want polymorphism, implementations when you want code reuse.

---

## ✅ Item 35: Consider Alternatives to Virtual Functions

Alternatives include:
- **Function pointers**
- **`std::function`**
- **Templates / CRTP**
- **Strategy pattern**

Example: Using function pointers
```cpp
class Button {
public:
    std::function<void()> onClick;
};
```

🧠 **Tip**: Virtual functions incur runtime overhead; alternatives may be simpler or more efficient in some cases.

---

## ✅ Item 36: Never Redefine an Inherited Non-Virtual Function

Redefining a non-virtual function in a derived class doesn't override it — it **hides** it.

```cpp
class Base {
public:
    void log();
};

class Derived : public Base {
public:
    void log(); // hides Base::log(); not virtual, not polymorphic
};
```

🧠 **Tip**: Redefining non-virtuals leads to confusion. Either make it virtual or don’t override it.

---

## ✅ Item 37: Never Redefine a Function’s Inherited Default Parameter Value

Default arguments are statically bound — they do not behave polymorphically.

```cpp
class Base {
public:
    virtual void draw(int color = 0); // default = 0
};

class Derived : public Base {
public:
    void draw(int color = 1); // default = 1, but base pointer still uses 0
};
```

🧠 **Tip**: If you override a virtual function, keep default arguments in sync or avoid them altogether.

---

## 📌 Summary

| Item | Key Point |
|------|-----------|
| 31 | Use public inheritance only when there's a true "is-a" relationship |
| 32 | Inherit only from classes explicitly designed to be base classes |
| 33 | Avoid accidentally hiding base class names in derived classes |
| 34 | Distinguish clearly between interface and implementation inheritance |
| 35 | Consider function pointers, `std::function`, or templates as alternatives to virtuals |
| 36 | Never override a non-virtual function — it leads to name hiding |
| 37 | Don’t redefine default parameters of inherited virtual functions |

Correct use of inheritance can enable powerful object-oriented designs — but misuse can lead to fragile, confusing, or broken code. Be precise and intentional in your inheritance strategies.
