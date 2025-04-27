
## Part 3: Conversions

### ✅ Item 11: Handle assignment in base classes

- Assignment operators must handle derived classes carefully.

🧠 **Tip**: Let derived classes handle their own members after the base class assignment.

---

### ✅ Item 12: Understand the costs of conversions

- Costly implicit conversions can lead to performance degradation.

🧠 **Tip**: Prefer explicit conversions where non-trivial work is involved.

---

### ✅ Item 13: Make conversion operators explicit

- Avoid surprising implicit conversions.

🧠 **Tip**: Prefer `explicit operator Type()` in modern C++.

---

### ✅ Item 14: Be wary of user-defined conversion functions

- Overusing conversion operators can lead to confusing code.

🧠 **Tip**: Limit conversion functions to only what’s necessary.
