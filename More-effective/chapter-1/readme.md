
## Part 1: Basics

### ✅ Item 1: Distinguish between pointers and references

- Pointers can be reassigned; references cannot.
- Pointers can be `nullptr`; references must always refer to a valid object.

🧠 **Tip**: Use references when an object is guaranteed to exist, pointers when it might not.

---

### ✅ Item 2: Prefer `const` and `inline` to `#define`

- Avoid macros when you can use `const`, `inline`, `enum`, or templates.

🧠 **Tip**: Macros don't respect C++'s type system; prefer language features.

---

### ✅ Item 3: Use `new` and `delete` correctly in classes that manage resources

- Follow the Rule of Three (destructor, copy constructor, copy assignment).
- Manage resource ownership explicitly.

🧠 **Tip**: Classes managing resources should handle copying and cleanup properly.

---

### ✅ Item 4: Prevent resource leaks in constructors

- If part of a constructor fails (e.g., throws an exception), already acquired resources must still be released.

🧠 **Tip**: Use RAII (Resource Acquisition Is Initialization) to manage resources safely.

---

### ✅ Item 5: Be alert for implicit type conversions

- Constructors with a single argument and conversion operators can introduce implicit conversions that may surprise you.

🧠 **Tip**: Use `explicit` keyword to avoid unwanted conversions.

---

### ✅ Item 6: Explicitly disallow unwanted compiler-generated functions

- Delete or privatize copy constructors or assignment operators if copying doesn’t make sense.

🧠 **Tip**: Make your intentions clear to the compiler and other developers.