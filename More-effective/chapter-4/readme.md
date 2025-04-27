## Part 4: Efficiency

### ✅ Item 15: Use reference-counted smart pointers where appropriate

- Manual memory management is error-prone; prefer smart pointers.

🧠 **Tip**: Use `std::shared_ptr`, `std::unique_ptr`, or custom reference-counted classes.

---

### ✅ Item 16: Use the Pimpl idiom to reduce compile-time dependencies

- Hide implementation details to speed up builds and improve encapsulation.

🧠 **Tip**: Use pointers to an implementation struct (`pImpl`) to reduce recompilation.

---

### ✅ Item 17: Understand the cost of virtual functions

- Virtual functions add runtime overhead (vtable lookup).

🧠 **Tip**: Don’t use virtuals unless dynamic dispatch is necessary.

---

### ✅ Item 18: Have realistic expectations about the cost of exception handling

- Exceptions are generally cheap unless thrown frequently.

🧠 **Tip**: Don't avoid exceptions for fear of minor runtime overhead.
