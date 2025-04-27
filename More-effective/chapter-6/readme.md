

## Part 6: Techniques

### ✅ Item 24: Understand smart pointers and how to use them

- Smart pointers automate memory management but require discipline.

🧠 **Tip**: Prefer `std::unique_ptr` for ownership, `std::shared_ptr` for shared ownership.

---

### ✅ Item 25: Know about proxy classes

- Proxy classes can provide efficient, flexible behavior (e.g., reference counting).

🧠 **Tip**: Proxy objects are useful for optimization but add complexity.

---

### ✅ Item 26: Use reference counting for shared ownership of resources

- Ensures proper memory management with shared ownership.

🧠 **Tip**: Reference counting should be automatic and hidden from users.

---

### ✅ Item 27: Avoid premature optimization

- First make it right, then make it fast.

🧠 **Tip**: Optimize only after identifying bottlenecks with profiling.

---

### ✅ Item 28: Write exception-safe code

- Strong and basic exception guarantees make code robust.

🧠 **Tip**: Prefer resource-managing classes and the RAII idiom.

---

### ✅ Item 29: Understand when and how to use multiple inheritance

- Useful when combining orthogonal behaviors (e.g., interfaces).

🧠 **Tip**: Multiple inheritance is tricky — use it only when truly necessary.

---

### ✅ Item 30: Prefer composition over inheritance

- Composition is more flexible and less fragile than inheritance.

🧠 **Tip**: Model "has-a" relationships with composition.

---

### ✅ Item 31: Understand proxy iterators

- Proxy iterators act like pointers but provide custom behavior.

🧠 **Tip**: Useful when dealing with indirect data structures (e.g., iterators for compressed collections).

---

### ✅ Item 32: Familiarize yourself with allocators

- Allocators control memory allocation in STL containers.

🧠 **Tip**: Custom allocators can optimize memory usage but require deep understanding.

---

### ✅ Item 33: Write small, simple functions

- Easier to read, test, maintain, and optimize.

🧠 **Tip**: Break complex operations into small pieces.

---

### ✅ Item 34: Be aware of temporary objects and lifetime issues

- Be cautious when returning references to locals, binding temporaries, etc.

🧠 **Tip**: Lifetime management is crucial for correct C++ programs.

---

### ✅ Item 35: Understand your compiler’s warnings

- Modern compilers warn about many subtle bugs.

🧠 **Tip**: Treat warnings as errors. Fix all warnings.
