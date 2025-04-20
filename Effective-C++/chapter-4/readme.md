# Chapter 4: Designs and Declarations

This chapter focuses on best practices around designing classes and functions, as well as how to make declarations that lead to robust and maintainable code. The goal is to produce interfaces that are easy to use correctly and hard to use incorrectly.

## ✅ Item 18: Make Interfaces Easy to Use Correctly and Hard to Use Incorrectly

Good interfaces are intuitive and enforce correctness by design. For example, use strong typing, enums instead of bools, and clear function signatures.

```cpp
void setAlarm(Time t, Sound s); // better than using raw ints or bools
```

🧠 **Tip**: Design APIs that make incorrect usage hard or impossible.

---

## ✅ Item 19: Treat Class Design as Type Design

When creating a class, think of it as designing a new data type. Decide on:
- How it's copied or moved
- Whether it supports comparison, streaming, arithmetic, etc.
- Its invariants and representation

🧠 **Tip**: Don't just declare a class — define how it behaves in every scenario.

---

## ✅ Item 20: Prefer Pass-by-Reference-to-const to Pass-by-Value

Pass user-defined types (e.g., strings, vectors) by `const&` to avoid unnecessary copies.

```cpp
void print(const std::string& msg); // efficient
```

For built-in types (int, char, float), pass by value.

🧠 **Tip**: Use `const&` for large objects, and by value for simple types.

---

## ✅ Item 21: Don’t Try to Return a Reference When You Must Return an Object

Returning a reference to a local object or temporary is a bug:

```cpp
const std::string& getName() {
    std::string name = "Bob";
    return name; // ❌ dangling reference
}
```

🧠 **Tip**: Return by value unless you’re returning a reference to something that will outlive the function.

---

## ✅ Item 22: Declare Data Members `private`

Always use encapsulation. Keep data `private` and provide access via methods when necessary. This allows better control and future-proofing.

```cpp
class User {
private:
    std::string name;
public:
    void setName(const std::string& n);
    std::string getName() const;
};
```

🧠 **Tip**: Encapsulation is key to long-term maintainability.

---

## ✅ Item 23: Prefer Non-Member Non-Friend Functions to Member Functions

Non-member functions reduce coupling and can lead to more reusable code.

```cpp
class Rational {
public:
    Rational(int numerator = 0, int denominator = 1);
    int numerator() const;
    int denominator() const;
};

const Rational operator*(const Rational& lhs, const Rational& rhs); // non-member
```

🧠 **Tip**: If a function can be non-member and still access what it needs via public API, keep it out of the class.

---

## ✅ Item 24: Declare Non-Member Functions When Type Conversions Should Apply to All Parameters

Type conversions via constructors or `operator` overloads apply only to the first argument of a member function. Use non-member functions if conversion is needed on both sides.

```cpp
class Rational {
public:
    Rational(int numerator = 0, int denominator = 1);
};

const Rational operator*(const Rational& lhs, const Rational& rhs); // enables conversions on both
```

🧠 **Tip**: Use non-member functions for symmetric operations and conversions.

---

## ✅ Item 25: Consider Support for a `swap` Function

Provide a custom `swap` function for your class to allow efficient swapping. Use member-wise swap for performance and exception safety.

```cpp
class Widget {
public:
    void swap(Widget& other); // member swap
};

namespace std {
    template<>
    void swap(Widget& a, Widget& b) {
        a.swap(b); // use custom swap
    }
}
```

🧠 **Tip**: Providing `swap` enables STL algorithms and improves performance.

---

## 📌 Summary

| Item | Key Point |
|------|-----------|
| 18 | Design interfaces to guide users toward correct usage |
| 19 | Treat classes as full-fledged types with well-defined behavior |
| 20 | Pass large objects by `const&`, small ones by value |
| 21 | Never return references to local or temporary objects |
| 22 | Keep data members `private` to enforce encapsulation |
| 23 | Use non-member non-friend functions when possible |
| 24 | Use non-members to enable conversions on all parameters |
| 25 | Provide and use custom `swap` functions for efficiency |

This chapter lays the groundwork for writing clean, well-encapsulated, reusable components with clearly defined interfaces.
