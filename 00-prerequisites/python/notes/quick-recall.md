# Python for AI Engineering — Quick Recall

This file contains 60-second summary cards for each video session in the Python for AI Engineering course. Use these cards for active recall and quick refreshers.

---

## 01. Python Fundamentals

**Video:** [Session 1 - Python Fundamentals](https://www.youtube.com/live/1z5-O7-5AXk?si=B0u9BJ3bPBL824e2) · **Date:** 7 Nov 2022
→ Deep-dive: [01-python-fundamentals.md](01-python-fundamentals.md)

### TL;DR
Covers Python output (`print()`), dynamic typing and binding, rules for identifiers and comments, user input string safety, implicit and explicit type conversions, and literals (numeric, float, complex, string, boolean, and None).

### Key Points
* **Dynamic Typing vs. Binding** — Dynamic typing infers data types at runtime based on assigned values; dynamic binding allows variables to be bound to different data types during execution.
* **print() parameters** — `sep` defines characters between comma-separated values (default space); `end` defines the trailing print behavior (default newline `\n`).
* **input() string default** — Always returns type `str` as a safety mechanism to prevent runtime crashes on non-numeric inputs.
* **Type Conversion** — Operations like `int(x)` do not modify the original variable `x` (which remains unchanged in memory); instead, they return a new object of the converted type.
* **None Literal** — Used to declare variable names in memory before their values are initialized, bypassing NameErrors.
* **Booleans** — Subclass of `int` internally; `True` evaluates to `1` and `False` to `0` in arithmetic operations.
* **Raw Strings** — Prefixed with `r` (e.g., `r"\n"`) to treat escape sequences as literal characters, crucial for regular expressions and path structures.

### Terms Introduced
| Term | Definition (one line) |
|---|---|
| **Dynamic Typing** | A system where variable data types are evaluated at runtime rather than compile time. |
| **Dynamic Binding** | The ability to re-bind a variable name to reference objects of different data types in the same program. |
| **Implicit Type Conversion** | Automatic data type promotion by the interpreter during calculations (e.g., `int + float -> float`). |
| **Explicit Type Conversion** | Manually casting a value to another type using built-in functions like `int()`, `float()`, `str()`. |
| **Raw String Literal** | A string prefixed by `r` that treats all backslashes as literal characters rather than escape sequences. |
| **None Type** | A special data type containing only a single literal value (`None`) representing the absence of value. |

### Self-Test
- Why does Python require explicit conversion (like `int()`) when reading numeric input from `input()`?
- What is the difference between dynamic typing and dynamic binding?
- What will `print("A", "B", sep="|", end="")` followed by `print("C")` output?
- How is the `None` literal used as a declaration placeholder?
