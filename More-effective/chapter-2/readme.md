
## Part 2: Operators

### ✅ Item 7: Declare `operator=` consistently with copy constructors

- Follow the Rule of Three.

🧠 **Tip**: Ensure assignment and copying behave consistently.

---

### ✅ Item 8: Understand why base classes need virtual destructors

- Deleting a derived object through a base pointer without a virtual destructor causes undefined behavior.

🧠 **Tip**: If a class is polymorphic, always give it a virtual destructor.

---

### ✅ Item 9: Avoid slicing

- Assigning a derived class object to a base class object slices off the derived parts.

🧠 **Tip**: Pass polymorphic types by pointer or reference, not by value.

---

### ✅ Item 10: Don't overload `&&`, `||`, or `,`

- These operators have short-circuit behavior or sequencing guarantees that are very hard to replicate safely.

🧠 **Tip**: Stick to overloading safer operators like `+`, `-`, `==`, etc.
