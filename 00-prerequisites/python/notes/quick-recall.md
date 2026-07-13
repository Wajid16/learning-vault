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

---

## 02. Operators, Conditionals, and Loops

**Video:** [Session 2 - Operators + If-Else + Loops](https://www.youtube.com/live/JCkIrdrZEE8?si=sZUEuKbKZr-4-igW) · **Date:** 8 Nov 2022
→ Deep-dive: [02-operators-if-else-loops.md](02-operators-if-else-loops.md)

### TL;DR
Covers six types of operators, the sum of digits extraction problem, branch logic with `if-elif-else` conditionals, code reusability using modules, `while` and `for` loops, Python's `while-else` construct, and iterative traversal.

### Key Points
* **Division differences** — `/` evaluates float division (always returning float); `//` evaluates floor division (returning truncated integer).
* **Compound Assignment** — Python lacks `++` or `--` increment/decrement structures; use `x += 1` instead.
* **Membership search** — `in` and `not in` verify if an item exists inside a collection. Hashed structures (sets/dicts) resolve in $O(1)$ time complexity.
* **Conditionals & Nesting** — Code blocks are delineated by colons `:` and indentation (PEP8 advises 4 spaces). Nesting lets us stack conditionals for multi-stage branches.
* **Modules & Reusability** — Brings pre-built namespaces and functions via `import` statements (e.g., `math`, `random`, `datetime`).
* **while-else loop** — The `else` block executes only when the loop terminates naturally (condition becomes `False`). If terminated by a `break`, the `else` block is bypassed.
* **for loop & range()** — Traverses sequences or generated bounds. The `range(start, stop, step)` limits start as inclusive and stop as exclusive.

### Terms Introduced
| Term | Definition (one line) |
|---|---|
| **Floor Division (`//`)** | Division that rounds down to the nearest whole integer. |
| **XOR Operation (`^`)** | Bitwise evaluation that returns `1` only if the input bits are different. |
| **Membership Operators** | Symbols (`in` / `not in`) testing containment of a value within an iterable. |
| **Module** | A Python file containing functions and classes meant to be imported and reused. |
| **while-else loop** | A loop structure whose `else` block executes only upon standard, non-broken completion. |
| **range() function** | A built-in generator function returning a sequence of numbers within specified bounds. |

### Self-Test
- What is the output of `5 // 2` versus `5 / 2`?
- Under what conditions does the `else` block of a `while-else` loop execute?
- How do membership operators achieve $O(1)$ search time on sets and dictionaries?
- Write a `for` loop that prints numbers from 10 down to 1 using `range()`.

---

## 03. Python Strings

**Video:** [Session 3 - Python Strings](https://www.youtube.com/live/6HAu0Y9BjA4?si=G0nzYrn6otXGAGPQ) · **Date:** 9 Nov 2022
→ Deep-dive: [03-python-strings.md](03-python-strings.md)

### TL;DR
Covers loop wrap-up, Unicode character encoding, positive/negative indexing, string slicing rules, mutability limits, lexicographical and logical string evaluations, key methods (`split()`, `join()`, `strip()`), and algorithmic string solutions.

### Key Points
* **Unicode Default** — Python represents characters using 16-bit to 32-bit Unicode mapping, enabling emojis and multi-language handling, unlike standard 8-bit ASCII.
* **Negative Slicing** — Ex: `s[::-1]` reverses a string. For negative step sizes, the `start` parameter must be numerically greater than `stop`.
* **Mutability constraint** — Strings are immutable. Actions trying to execute in-place edits (e.g. `s[0] = 'H'` or `del s[0]`) raise a `TypeError`.
* **Logical behavior** — Non-empty strings act as `True`, empty strings (`""`) as `False`. Evaluation short-circuits (`and` returns first false/last term, `or` returns first true term).
* **Lexicographical comparison** — Relational checks analyze values alphabetical-order wise based on Unicode codes (meaning uppercase chars `<` lowercase chars).
* **Split & Join operations** — `split("delim")` slices strings into lists of substrings; `join(list)` constructs strings from lists of text components.

### Terms Introduced
| Term | Definition (one line) |
|---|---|
| **Unicode** | A comprehensive character encoding system mapping text characters from global languages and symbols. |
| **IndexError** | Error raised when a program tries to access an index position outside of active string boundaries. |
| **Immutability** | Memory structure constraint preventing in-place updates of data objects after creation. |
| **Lexicographical order** | Dictionary-based character order evaluated using Unicode character numerical values. |
| **Short-Circuit Evaluation** | Logical evaluation path stopping as soon as the final boolean result is determined. |
| **Whitespace stripping** | Removing leading and trailing whitespace characters (e.g., spaces, tabs, newlines) via `.strip()`. |

### Self-Test
- What error is raised by `s[0] = 'H'` and why does it happen?
- What will `"hello" and "world"` evaluate to and why?
- Write a slice expression that extracts every second character from index 1 to 7.
- Implement word counting for a string without calling the built-in `.split()` method.


