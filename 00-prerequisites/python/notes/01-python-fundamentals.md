# Session 01: Python Fundamentals

> 🎥 **Source:** [Session 1 - Python Fundamentals | CampusX Data Science Mentorship Program](https://www.youtube.com/live/1z5-O7-5AXk?si=B0u9BJ3bPBL824e2) · 📅 7 Nov 2022 · 📚 **Course:** Python for AI Engineering

---

## Table of Contents
1. [TL;DR](#tldr)
2. [Why Python?](#why-python)
    - [Python's Popularity & History](#pythons-popularity--history)
    - [Why Python Rules AI & Data Science](#why-python-rules-ai--data-science)
3. [Output: The print() Function](#output-the-print-function)
    - [Syntactical Details & Parameters](#syntactical-details--parameters)
4. [Data Types: The Building Blocks](#data-types-the-building-blocks)
    - [Built-in Data Types](#built-in-data-types)
    - [The type() Function](#the-type-function)
5. [Variables & Memory State](#variables--memory-state)
    - [Variable Declarations](#variable-declarations)
    - [Dynamic Typing vs. Static Typing](#dynamic-typing-vs-static-typing)
    - [Dynamic Binding vs. Static Binding](#dynamic-binding-vs-static-binding)
    - [Stylish Declarations](#stylish-declarations)
6. [Code Readability & Comments](#code-readability--comments)
    - [Comment Syntax and PEP8](#comment-syntax-and-pep8)
7. [Keywords & Identifiers](#keywords--identifiers)
    - [Keywords](#keywords)
    - [Identifiers & Naming Rules](#identifiers--naming-rules)
8. [User Input: Dynamic Applications](#user-input-dynamic-applications)
    - [The input() Function](#the-input-function)
    - [Why input() Defaults to Strings](#why-input-defaults-to-strings)
9. [Type Conversion: Explicit & Implicit](#type-conversion-explicit--implicit)
    - [Implicit Type Conversion](#implicit-type-conversion)
    - [Explicit Type Conversion (Casting)](#explicit-type-conversion-casting)
    - [Non-Destructive Nature of Conversion](#non-destructive-nature-of-conversion)
10. [Literals: Raw Constants](#literals-raw-constants)
    - [Numeric Literals](#numeric-literals)
    - [Float & Complex Literals](#float--complex-literals)
    - [String Literals](#string-literals)
    - [Boolean & None Literals](#boolean--none-literals)
11. [Added Context (For AI Engineers)](#added-context-for-ai-engineers)
12. [Quick Recap](#quick-recap)
13. [Practice Check](#practice-check)

---

## TL;DR

This session establishes the foundational building blocks of Python programming. By examining how Python manages output (`print()`), stores data (variables, dynamic typing/binding, and literals), takes inputs (`input()`), and handles data-type mutations (implicit/explicit type conversion), we build the bedrock necessary for writing clean scripts. For an AI Engineer, these mechanisms govern how neural network inputs are parsed, how configuration files are structured, and how dynamic tensor dimensions are handled at runtime.

---

## Why Python?

### Python's Popularity & History

**What is it?**
Python is a high-level, general-purpose, interpreted programming language created by Guido van Rossum in 1989. While Python was created *before* Java (~1995), it grew slowly for the first two decades, eventually overtaking Java as the language of choice for scientific computing and AI during the mid-2010s data explosion.

**Why does it exist / what problem does it solve?**
Traditional languages (like Java and C++) are verbose, syntactically rigid, and require high development overhead. Python was designed with a core philosophy of simplicity, readability, and speed of development. 

**How does it work? (mental model / analogy)**
*   **The Shah Rukh Khan vs. Amitabh Bachchan Analogy:** 
    *   **Java** is like the strict Amitabh Bachchan character in *Mohabbatein*: rigid, disciplinary, and demanding adherence to protocol (types, imports, classes) before letting you run even one line of code.
    *   **Python** is like Shah Rukh Khan: welcoming, easy-going, and forgiving. It invites beginners to write code easily and figure out mistakes as they go.
*   **Do Not Reinvent the Wheel:** Python's design philosophy encourages using existing blocks. If the wheel (libraries) is already built, your job as an engineer is to use it to build a car (applications), not rebuild the wheel from scratch.

---

### Why Python Rules AI & Data Science

| Aspect | Description | Why it matters to AI |
|---|---|---|
| **Easy to Learn** | Low syntactical friction enables mathematicians, physicists, and statisticians to code without deep CS backgrounds. | Domain experts can transition directly into training models without wrestling with pointers or memory leaks. |
| **Proximity to Math** | Python syntax mirrors mathematical notation closely. | Code representing complex equations, loss functions, and matrices is intuitive and compact. |
| **C-Engine Bindings** | Under the hood, critical computation libraries (like NumPy, SciPy) are written in C/C++. | Python provides a clean interface while maintaining execution speeds matching compiled C systems (via vectorized operations). |
| **Ecosystem & Community** | A massive repository of libraries (Pandas, PyTorch, Hugging Face, NumPy, Scikit-learn). | AI developers rarely build algorithms from scratch; they orchestrate high-level pre-built pipelines. |

**Interview / exam angle:**
*   *Question:* "If Python is an interpreted language and inherently slower than C++, why is it the dominant language for high-performance AI and Machine Learning?"
*   *Answer:* While Python itself is slow due to dynamic interpretation, its core numerical libraries (like NumPy and PyTorch) wrap high-performance C and C++ backends. Operations on data structures (like `numpy.ndarray` or `torch.Tensor`) run compiled compiled C/C++ routines or CUDA kernels on GPUs, minimizing Python interpreter overhead.

---

## Output: The print() Function

### Syntactical Details & Parameters

**What is it?**
A built-in function that displays values or the evaluation of expressions onto the console (standard output).

**Subtopics:**
*   **Multi-value printing:** Passing multiple variables separated by commas. By default, Python separates them with a space.
*   **`sep` parameter:** Defines the separator character between multiple values (defaults to a space `" "`).
*   **`end` parameter:** Defines the trailing character printed at the very end of the print statement (defaults to a newline `\n`).

**Code example:**
```python
# Basic single value print
print("Initializing LLM Agent...")

# Multiple values (prints with default space separator)
model_name = "Llama-3"
parameters = "8B"
print("Model:", model_name, "Params:", parameters)
# Output: Model: Llama-3 Params: 8B

# Custom separator (sep)
print("00", "prerequisites", "python", sep="/")
# Output: 00/prerequisites/python

# Custom ending (end) to print on the same line
print("Fetching weights...", end=" ")
print("Success!")
# Output: Fetching weights... Success!
```

**Interview / exam angle:**
*   *Question:* "What will be the output of `print("A", "B", sep="-", end="*")` followed by `print("C")`?"
*   *Answer:* `A-B*C` (The asterisk prevents the first print from outputting a newline, so the subsequent output `C` immediately follows it on the same line).

---

## Data Types: The Building Blocks

### Built-in Data Types

**What is it?**
Data types determine the category of a value, defining how much memory it occupies and what operations can be performed on it.

| Category | Type | Code Syntax | Notes |
|---|---|---|---|
| **Numeric** | Integer (`int`) | `x = 42` | Whole numbers; Python dynamically expands memory to fit arbitrarily large integers. |
| | Floating-point (`float`) | `y = 3.14` | Decimal numbers; represented as double-precision floats under the hood. |
| | Complex (`complex`) | `z = 3 + 5j` | Real and imaginary parts (`j` is used for imaginary unit instead of standard math `i`). |
| **Text** | String (`str`) | `s = "HuggingFace"` | Immutable sequence of characters wrapped in single, double, or triple quotes. |
| **Logical** | Boolean (`bool`) | `is_valid = True` | Can only be `True` or `False`. Case-sensitive. |
| **Sequence** | List | `lst = [1, 2, 3]` | Ordered, mutable collection. Equivalent to arrays but can hold heterogeneous types. |
| | Tuple | `tpl = (1, 2, 3)` | Ordered, **immutable** sequence. |
| **Set** | Set | `st = {1, 2, 3}` | Unordered collection of unique items. |
| **Map** | Dictionary (`dict`) | `d = {"model": "GPT-4"}` | Unordered collection of key-value pairs. |

---

### The type() Function

**What is it?**
A built-in function that queries and returns the runtime class/data type of any value or variable.

**Code example:**
```python
# Inspecting types of values
print(type(100))        # <class 'int'>
print(type(99.9))       # <class 'float'>
print(type(True))       # <class 'bool'>
print(type("Prompt"))   # <class 'str'>
print(type(5 + 2j))     # <class 'complex'>
print(type([1, 2, 3]))  # <class 'list'>
```

**Interview / exam angle:**
*   *Question:* "What does `type(True + 4)` output and why?"
*   *Answer:* `<class 'int'>`. Booleans in Python are a subclass of integers (`True` is represented internally as `1` and `False` as `0`). When added to an integer, it is implicitly promoted to an integer calculation (`1 + 4 = 5`).

---

## Variables & Memory State

### Variable Declarations

**What is it?**
Variables are named containers used to store reference pointers to memory objects. In Python, variables are initialized by assigning a value using the `=` operator. Unlike compiled languages, variables in Python do not need to be declared before assignment.

---

### Dynamic Typing vs. Static Typing

*   **Static Typing (e.g., Java, C++):** Variables must be declared with a strict data type. The compiler enforces that only values matching this type are assigned to the variable.
    ```java
    int a = 5; // compiler reserves memory specifically for an integer
    ```
*   **Dynamic Typing (Python):** Variable types are determined automatically at runtime based on the value assigned to them. You do not declare variable types.
    ```python
    a = 5  # Python automatically binds 'a' to an integer object
    ```

---

### Dynamic Binding vs. Static Binding

*   **Static Binding:** Once a variable is declared with a specific type, its type cannot change during execution.
*   **Dynamic Binding (Python):** A variable's association with a data type is not fixed. The same variable can refer to a different type of object at any point in the program.
    ```python
    x = 100       # x points to an integer object
    print(type(x)) # <class 'int'>
    
    x = "Llama"   # x now points to a string object. Valid in Python.
    print(type(x)) # <class 'str'>
    ```

**Interview / exam angle:**
*   *Question:* "What is the difference between Dynamic Typing and Dynamic Binding in Python?"
*   *Answer:* **Dynamic typing** means the interpreter evaluates a variable's data type at runtime based on the object it references (no compile-time declarations). **Dynamic binding** means a variable name can be re-bound to reference objects of completely different types during the program's lifecycle.

---

### Stylish Declarations

Python allows compact, comma-separated assignment syntaxes to keep initialization clean.

**Code example:**
```python
# Multiple variable initialization in a single line
a, b, c = 1, 2.5, "Agent"
print(a, b, c)  # 1 2.5 Agent

# Assigning the same value to multiple variables simultaneously
x = y = z = 100
print(x, y, z)  # 100 100 100
```

---

## Code Readability & Comments

### Comment Syntax and PEP8

**What is it?**
Comments are notes written inside the source code for human explanation. The Python interpreter ignores comments during execution.

**Subtopics:**
*   **Single-line comments:** Defined using the `#` symbol.
*   **Multi-line comments:** Python has no native multi-line comment symbol (like `/* ... */` in Java). Instead, multi-line comments are constructed using `#` on every line.
*   **The Batsman Analogy:** The instructor warns against being a "brilliant coder who writes zero comments." That is like a batsman who hits sixes but runs out his partner—they damage the team's longevity. Code should always be self-documenting or accompanied by comments.

```python
# Correct way (PEP8 compliant)
# We are initializing the temperature hyperparameter 
# to control output randomness.
temperature = 0.7

# Incorrect/Bad Practice (Using triple-quoted strings as comments)
"""
This looks like a comment but is actually a multiline string literal
stored in memory. Avoid using this in production.
"""
```

**Interview / exam angle:**
*   *Question:* "Does Python have a native multi-line comment block? Why are triple quotes discouraged for commenting code?"
*   *Answer:* Python does not have a native multi-line comment symbol. Using triple-quoted strings (`"""..."""`) as comments is discouraged because they are string literals, not true comments. If they are not assigned to a variable, they are evaluated in memory and discarded, causing unnecessary runtime overhead. PEP8 advises using `#` on each line for multi-line comments.

---

## Keywords & Identifiers

### Keywords

**What is it?**
Keywords are reserved, predefined words in Python that have special meaning to the interpreter. They cannot be used as variable names, function names, or other identifiers.

*   Python 3 contains **35 keywords** (e.g., `if`, `else`, `while`, `True`, `False`, `None`, `import`, etc.).
*   Keywords can be inspected programmatically using the `keyword` library.

**Code example:**
```python
import keyword
print("Total keywords:", len(keyword.kwlist))
print(keyword.kwlist)
```

---

### Identifiers & Naming Rules

**What is it?**
An identifier is a user-defined name given to program elements like variables, functions, classes, or modules.

**Rules for Valid Identifiers:**
1.  **Cannot start with a digit:** `1_model` is invalid; `model_1` is valid.
2.  **Allowed characters:** Only alphanumeric characters and underscores (`a-z`, `A-Z`, `0-9`, `_`). No special characters like `@`, `$`, `-`, `%`, etc.
3.  **Case-sensitivity:** `temp` and `Temp` are distinct identifiers.
4.  **No keywords:** You cannot name an identifier a keyword (e.g., `if = 5` is invalid).

**Code example:**
```python
# Valid identifiers
user_prompt = "Hello"
_model_weight = 0.85
token2 = 42

# Invalid identifiers (uncommenting will raise SyntaxError)
# 3_layer = [64, 32]       # Rule 1 Violation (starts with a digit)
# model-name = "BERT"      # Rule 2 Violation (contains a hyphen)
# class = "AI-101"         # Rule 4 Violation (uses reserved keyword)
```

---

## User Input: Dynamic Applications

### The input() Function

**What is it?**
A built-in function that pauses program execution, waits for user keyboard input, and resumes execution once the user hits Enter. 

---

### Why input() Defaults to Strings

Regardless of what the user types (numbers, symbols, boolean), the `input()` function **always returns a value of type `str`**.
*   **The Safety Reason:** String is the "universal data type." Any typed data can be safely converted to and stored as a string without crashing the program (e.g., `"42"`, `"99.9"`, `"True"`). Converting input directly into numbers at the interpreter level would crash the program if a user entered alphabetical text.

**Code example:**
```python
# Beginner mistake: string concatenation instead of math addition
num1 = input("Enter first number: ")   # User inputs: 5
num2 = input("Enter second number: ")  # User inputs: 6
result = num1 + num2
print(result)                          # Output: 56 (string concatenation)

# Correct approach: convert type explicitly
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))
print(num1 + num2)                     # Output: 11 (integer math)
```

---

## Type Conversion: Explicit & Implicit

### Implicit Type Conversion

**What is it?**
Python automatically converts one data type to another at runtime when the operation is mathematically logical and does not risk losing data.

**Code example:**
```python
num_int = 5
num_float = 4.5
result = num_int + num_float  # int + float is promoted to float
print(result, type(result))   # Output: 9.5 <class 'float'>
```

---

### Explicit Type Conversion (Casting)

**What is it?**
Explicitly converting a value from one data type to another using built-in casting functions like `int()`, `float()`, `str()`, `bool()`, `list()`, etc.

**Code example:**
```python
# Valid Explicit Conversions
print(int("42"))       # String to Integer -> 42
print(float(10))       # Integer to Float -> 10.0
print(str(15.7))       # Float to String -> '15.7'

# Invalid Explicit Conversions (Raises ValueError/TypeError)
# int("hello")         # Cannot convert alphabetic strings to integers
# int(3 + 5j)          # Cannot convert complex number to int (causes information loss)
```

---

### Non-Destructive Nature of Conversion

Casting functions **never modify the original variable**. Instead, they create a new object in memory.

**Code example:**
```python
x = "123"
y = int(x)      # Creates a new integer object and binds it to y
print(type(x))  # Output: <class 'str'> (x is untouched)
print(type(y))  # Output: <class 'int'>
```

**Interview / exam angle:**
*   *Question:* "If you run `x = "45"` followed by `int(x)`, what is the data type of `x` after execution?"
*   *Answer:* The data type of `x` remains `<class 'str'>`. The expression `int(x)` returns a new integer value but does not mutate the variable `x` itself. To update `x`, you must explicitly rebind it: `x = int(x)`.

---

## Literals: Raw Constants

### Numeric Literals

**What is it?**
Literals are the raw values assigned directly to variables. In `a = 10`, `10` is the literal.

*   **Decimal System:** Default number system.
*   **Binary System:** Prefix using `0b` or `0B`.
*   **Octal System:** Prefix using `0o` or `0O`.
*   **Hexadecimal System:** Prefix using `0x` or `0X`.

**Code example:**
```python
a = 100       # Decimal
b = 0b1010    # Binary (10 in decimal)
c = 0o310     # Octal (200 in decimal)
d = 0x12C     # Hexadecimal (300 in decimal)

print(a, b, c, d)  # Output: 100 10 200 300
```

---

### Float & Complex Literals

*   **Float Literals:** Can be defined directly (`10.5`) or using scientific exponential notation `e` or `E` for very large or small values.
*   **Complex Literals:** Composed of real and imaginary parts. Imaginary unit is specified using `j`.

**Code example:**
```python
f1 = 10.5
f2 = 1.5e2    # 1.5 * 10^2 = 150.0
f3 = 1.5e-3   # 1.5 * 10^-3 = 0.0015
print(f1, f2, f3)

z = 2 + 5j
print(z.real) # Output: 2.0
print(z.imag) # Output: 5.0
```

---

### String Literals

Python supports multiple string definitions depending on formatting requirements.

| Form | Syntax | Best Use Case |
|---|---|---|
| **Single quotes** | `'Text'` | Short strings |
| **Double quotes** | `"Text"` | Short strings, or containing single quotes: `"user's prompt"` |
| **Triple quotes** | `"""Text"""` or `'''Text'''` | Multi-line strings, prompt templates, docstrings. |
| **Raw strings** | `r"raw \n string"` | Regular expressions, folder paths (ignores escape sequences like `\n`). |
| **Unicode strings** | `u"\U0001F600"` | Embedding emojis or localized characters. |

**Code example:**
```python
# Triple quotes for multiline formatting
prompt_template = """System: You are an AI assistant.
User: Summarize this text.
Assistant:"""

# Raw string vs Standard string
standard_path = "C:\new_folder\table.txt"  # \n evaluates to newline, \t to tab
raw_path = r"C:\new_folder\table.txt"      # Treated as literal characters

print(standard_path)
# Output:
# C:
# ew_folder       able.txt

print(raw_path)
# Output: C:\new_folder\table.txt
```

---

### Boolean & None Literals

*   **Boolean Literals:** `True` and `False` represent binary truth states. They behave as `1` and `0` mathematically.
*   **None Literal:** Represents "nothing" or the absence of value. It is Python's version of `null`.

**None Literal Use Case:**
Because Python has no variable declaration syntax (like `int x;`), trying to mention a variable before assigning it a value throws a `NameError`. Setting `x = None` declares the variable name as a placeholder in memory until it is assigned a value later.

**Code example:**
```python
# Boolean math
print(True + 4)   # Output: 5
print(False + 10) # Output: 10

# None declaration placeholder
output_text = None
# ... downstream pipeline runs ...
output_text = "Generated summary."
```

---

## Added Context (For AI Engineers)

### 1. Dynamic Typing & Weight Configurations
In AI systems, weights or hyperparameters are often read from configuration files (like JSON or YAML) as dynamic dictionary objects. Because Python is dynamically typed, nested settings can be initialized without boilerplate parser definitions.
```python
# Config dictionaries rely heavily on dynamic typing to parse fields dynamically
model_config = {
    "temperature": 0.7,      # float
    "max_tokens": 512,       # int
    "stop_sequences": None   # NoneType placeholder
}
```

### 2. isinstance() vs. type() in Type Verification
While `type(x) == int` checks if `x` is exactly an integer, it is best practice in engineering to use `isinstance()`. In Python, Booleans are subclasses of integers. Using `type()` handles inheritance strictly, whereas `isinstance()` handles subclass checks.
```python
# In runtime validation:
print(type(True) == int)          # Output: False
print(isinstance(True, int))      # Output: True
```

### 3. Raw Strings in Tokenization & Regex
Regular expressions are core to tokenizing textual data before passing it to LLMs. Raw string literals (`r"..."`) prevent backslashes from being treated as escape sequences by Python, passing them clean to the regex compiler.
```python
import re
# Matches digit sequences in prompt text
pattern = r"\d+"
text = "The user has 25 tokens remaining."
print(re.findall(pattern, text))  # Output: ['25']
```

---

## Quick Recap

| Concept | Key Takeaway |
|---|---|
| `print(sep, end)` | `sep` separates multi-values (default `" "`), `end` appends at conclusion (default `\n`). |
| Data Types | `int`, `float`, `complex`, `str`, `bool`, `list`, `tuple`, `set`, `dict`. |
| Dynamic Typing | Python determines variable types dynamically at runtime based on assigned values. |
| Dynamic Binding | The same variable can point to completely different types during program execution. |
| Comments | Use `#` for single/multi-line. Discourage triple quotes `"""` for regular code comments. |
| Identifiers | Must not start with digit; can only contain letters, numbers, and `_`; cannot be keywords. |
| `input()` | Always returns `str` values to prevent program crashes. |
| Type Conversion | Implicit happens automatically if safe; Explicit requires functions (`int()`, `str()`). |
| Literals | Constant values. None represents empty/placeholder; Booleans resolve to `1` and `0` in math. |

---

## Practice Check

1.  **What will the following code output, and why?**
    ```python
    x = "10"
    y = "20"
    print(x + y, type(x + y))
    ```

2.  **Evaluate this script. What is printed, and why does this error-free behavior occur?**
    ```python
    val = True
    val = val + 5.5
    print(val, type(val))
    ```

3.  **Explain the difference between the outputs of the following two print calls:**
    ```python
    print("AI\nEngineering")
    print(r"AI\nEngineering")
    ```

4.  **Why does writing `x` on a line by itself raise a `NameError` in Python, but writing `x = None` does not? Explain this behavior in the context of variable declarations.**

---
<!-- Long note complete. Companion: [Quick Recall](quick-recall.md#01-python-fundamentals) -->
