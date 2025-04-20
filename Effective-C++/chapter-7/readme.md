# Chapter 7: Templates and Generic Programming

This chapter explores the power of templates in C++, as well as how to write efficient, maintainable, and predictable template code. It emphasizes type independence, traits, specialization, and template pitfalls.

---

## ✅ Item 38: Understand How to Choose Among Templates and Inheritance

- Use **templates** for **compile-time polymorphism** (i.e., when types vary).
- Use **inheritance** for **runtime polymorphism** (i.e., when behavior varies).

Example:
```cpp
template<typename T>
class Array { /* generic type-independent container */ };

class Shape {
public:
    virtual void draw() const = 0;
};
```

🧠 **Tip**: Templates are great for performance and flexibility; inheritance is better when behavior needs to vary dynamically.

---

## ✅ Item 39: Use `void` Parameters to Indicate That a Function Template Has No Parameters

When writing a function template that takes no arguments, explicitly write `void` to avoid ambiguity.

```cpp
template<typename T>
T getDefaultValue(void); // preferred
```

🧠 **Tip**: Prevent surprises and clarify intent by using `void` in parameter lists.

---

## ✅ Item 40: Make Functor Classes Adaptable

Adaptable functors define typedefs like `result_type`, `argument_type`, etc., making them compatible with STL function adaptors (`bind1st`, `not1`, etc.).

Example:
```cpp
struct AddValue : public std::unary_function<int, int> {
    int value;
    AddValue(int v) : value(v) {}
    int operator()(int x) const { return x + value; }
};
```

🧠 **Tip**: In legacy STL, adaptability is required. In modern C++, prefer lambdas.

---

## ✅ Item 41: Use Traits Classes for Information About Types

Traits let templates query type-specific information at compile time.

Example:
```cpp
template<typename T>
struct TypeTraits {
    static const bool isPointer = false;
};

template<typename T>
struct TypeTraits<T*> {
    static const bool isPointer = true;
};
```

🧠 **Tip**: Traits allow you to write more general and type-safe code.

---

## ✅ Item 42: Design and Use Inheritance with Templates Carefully

Templates and inheritance don't always mix well — pay attention to which member functions are instantiated and inherited.

Example:
```cpp
template<typename T>
class Base {
protected:
    void log(const T&);
};

template<typename T>
class Derived : public Base<T> {
public:
    void process(const T& val) {
        this->log(val); // use `this->` to avoid name lookup issues
    }
};
```

🧠 **Tip**: Use `this->` to access inherited names from base class templates.

---

## ✅ Item 43: Know How to Access Names in Template Base Classes

In template-derived classes, base class members may not be found without qualification.

```cpp
this->func();
Base<T>::func();
using Base<T>::func;
```

🧠 **Tip**: Avoid confusing name lookup failures by explicitly qualifying base class names.

---

## ✅ Item 44: Factor Parameter-Independent Code Out of Templates

If part of your code doesn’t depend on the template parameter, move it out to a non-template base class. This reduces code bloat and improves compilation speed.

Example:
```cpp
class Logger {
protected:
    void log(const std::string&);
};

template<typename T>
class Processor : private Logger {
public:
    void run(const T& input) {
        log("Processing...");
    }
};
```

🧠 **Tip**: Isolate template-dependent parts — factor out the rest for clarity and efficiency.

---

## 📌 Summary

| Item | Key Point |
|------|-----------|
| 38 | Use templates for type-based variation, inheritance for behavior variation |
| 39 | Use `void` to make zero-arg templates unambiguous |
| 40 | Make functors adaptable by defining STL-compatible typedefs |
| 41 | Use traits classes to specialize behavior based on types |
| 42 | Mix templates and inheritance carefully; use `this->` or `Base<T>::` for access |
| 43 | Be explicit with name lookup in template base classes |
| 44 | Move type-independent logic out of templates to reduce bloat |

Templates are a foundational tool for generic programming in C++. With careful design, you can write elegant, reusable, and highly efficient code.
