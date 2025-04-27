## Part 5: Implementations

### ✅ Item 19: Treat class design as type design

- Consider copyability, comparability, streamability, etc.

🧠 **Tip**: Be thorough when designing new types.

---

### ✅ Item 20: Avoid data members that are pointers to implementation details

- Prefer value semantics when possible.

🧠 **Tip**: Don't expose raw pointers if you can help it.

---

### ✅ Item 21: Use double-checked locking cautiously

- Improper use is prone to race conditions.

🧠 **Tip**: Prefer C++11 constructs (`std::call_once`) to ensure thread-safe initialization.

---

### ✅ Item 22: Beware of compiler optimizations

- Optimizations can break poorly designed code that relies on undefined behavior.

🧠 **Tip**: Write correct code first; optimize only when needed.

---

### ✅ Item 23: Understand the cost of non-virtual interface classes (NVI)

- Forces calling through a stable public interface.

🧠 **Tip**: Use NVI to decouple public APIs from customizable behavior.

