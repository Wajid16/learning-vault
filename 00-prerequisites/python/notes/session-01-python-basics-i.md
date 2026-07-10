# Session 01: Python Basics I — Output, Data Types, Variables, Comments, Keywords, Identifiers, Input, Type Conversion, Literals

> 🎥 Source: https://www.youtube.com/live/1z5-O7-5AXk?si=r8zwDwRWPpN82LOb · 🗓️ 8 July 2026

## TL;DR
- First session of CampusX's Python for Data Science course — covers the absolute foundations every Python program is built on.
- Topics: printing output, Python's built-in data types, variables, comments, keywords & identifiers, taking user input, type conversion, and literals.
- Understanding **dynamic typing** and **type conversion** here saves a lot of confusion later — they come up in interviews and in real pandas/numpy code when types silently mismatch.
- Everything in this session is a building block. You'll use `print()`, `input()`, `int()`, and `type()` in every session from here on.

---

## Section: Why Python?

### Why Python became so popular

**What is it?** A brief motivational overview of why Python dominates data science — the instructor always opens with this to anchor the "why" before the "how."

**Subtopics:**
- Design philosophy — simple, readable, elegant
- Batteries included — built-in functions and data types that do heavy lifting for you
- General-purpose — works for web, data science, automation, etc.
- Community & libraries — NumPy, Pandas, TensorFlow, Keras, etc.

**Where it's used / interview angle:**
Interviewers sometimes ask: *"Why Python over Java or C++ for data science?"* — the answer is: easy to learn (attracts non-CS people like statisticians), proximity to math (NumPy was already there), and a massive ecosystem.

**Key points from the session:**
- Python was created *before* Java (1989 vs ~1994), but grew slowly until data science exploded.
- The instructor's analogy: Java is like the strict Amitabh Bachchan character; Python is more like the welcoming Shah Rukh Khan — easy-going, forgiving for newcomers.
- *"Don't reinvent the wheel"* — Python's core philosophy. If a library already does it, use it.
- Python is slower than C/C++, but NumPy's array type is implemented in C under the hood, so numerical code is fast anyway.

---

## Section: Output

### `print()` function

**What is it?** A built-in function that displays any value to the screen. The starting point of every Python program.

**Subtopics:**
- Printing single values (strings, numbers, booleans)
- Printing multiple values at once (comma-separated)
- `sep` parameter — controls what goes between multiple values
- `end` parameter — controls what goes after the last value (default is a newline `\n`)

**Where it's used / interview angle:**
`print()` itself isn't an interview topic, but interviewers do test understanding of `sep` and `end` in tricky MCQs. E.g., *"What does `print('a','b', sep='', end='!')` output?"* → `ab!`

**Types / forms, each with an example:**

*Basic print — single value*
```python
print("Hello World")   # Hello World
print(42)              # 42
print(True)            # True
```

*Multiple values with default separator (space)*
```python
print("Hello", "World", 14.5)
# Hello World 14.5
```

*Custom separator with `sep`*
```python
print("Hello", "World", sep="+")
# Hello+World
```

*Custom line ending with `end`*
```python
print("Hello", end=" ")
print("World")
# Hello World     <- both on the same line
```

---

**Practice programs for this section:**

1. Print your name, age, and city on a single line separated by `|`:
```python
print("Wajid", 20, "Karachi", sep=" | ")
```

2. Print a 3-line address without using 3 separate `print()` calls:
```python
print("Line 1\nLine 2\nLine 3")
```

---

## Section: Data Types

### Data types overview

**What is it?** The categories of values Python can work with. Every piece of data in Python belongs to a type, and the type determines what operations are valid on it.

**Subtopics:**
- Numeric: `int`, `float`, `complex`
- Text: `str`
- Logical: `bool`
- Collections: `list`, `tuple`, `set`, `dict`

**Where it's used / interview angle:**
You'll be asked: *"Name all built-in data types in Python."* Also: *"What is the difference between a list and a tuple?"* (covered in a later session). For now, just recognise what each type looks like.

**Types / forms, each with an example:**

*Integer (`int`) — whole numbers, positive or negative, no size limit in Python*
```python
print(9)          # 9
print(-42)        # -42
print(1e308)      # Python handles very large integers natively
```

*Float (`float`) — decimal numbers, up to ~1.7 x 10^308*
```python
print(7.65)       # 7.65
print(1.7e308)    # near float limit
```

*Boolean (`bool`) — only `True` or `False`; note capital T/F, no quotes*
```python
print(True)       # True
print(False)      # False
```

*String (`str`) — any text wrapped in quotes*
```python
print("Hello")    # Hello
print('World')    # World   <- single or double quotes both work
```

*Complex (`complex`) — real + imaginary part (j notation)*
```python
print(5 + 7j)     # (5+7j)
```

*List — ordered, mutable collection (like arrays in C)*
```python
print([1, 2, 3])  # [1, 2, 3]
```

*Tuple — ordered, immutable collection*
```python
print((1, 2, 3))  # (1, 2, 3)
```

*Set — unordered, unique-values collection*
```python
print({1, 2, 3, 4})  # {1, 2, 3, 4}
```

*Dictionary (`dict`) — key-value pairs*
```python
print({"Name": "Wajid", "Age": 20})  # {'Name': 'Wajid', 'Age': 20}
```

### `type()` function

**What is it?** A built-in function that returns the data type of any value or variable.

**Where it's used / interview angle:**
You'll use this constantly while debugging. Interviewers sometimes ask: *"How do you check the type of a variable at runtime?"* -> `type(x)`.

**Example:**
```python
print(type(105))      # <class 'int'>
print(type(7.65))     # <class 'float'>
print(type("Hello"))  # <class 'str'>
print(type(True))     # <class 'bool'>
print(type([1, 2]))   # <class 'list'>
```

---

**Practice programs for this section:**

1. Print one value of each data type and its `type()`:
```python
values = [42, 3.14, True, "hi", 2+3j, [1,2], (1,2), {1,2}, {"a":1}]
for v in values:
    print(v, "->", type(v))
```

2. Check what `type(True + 4)` returns and verify:
```python
result = True + 4
print(result, type(result))   # 5, <class 'int'>
```

---

## Section: Variables

### Variables

**What is it?** Named containers for storing values whose content may not be known at the time you write the program — e.g., you don't know which user will log in next.

**Subtopics:**
- Declaration syntax (no type annotation needed)
- Dynamic typing — Python infers the type from the value
- Dynamic binding — a variable can hold different types at different points in the same program
- Multiple assignment / stylish declaration

**Where it's used / interview angle:**
Two high-frequency interview questions: *"What is dynamic typing in Python?"* and *"What is dynamic binding?"* Know both and how they differ from static typing (C/Java).

**Types / forms, each with an example:**

*Basic variable assignment*
```python
name = "Wajid"      # Python figures out it's a str
age = 20            # Python figures out it's an int
print(name, age)    # Wajid 20
```

*Dynamic typing — no need to declare the type*
```python
# In C you'd write: int a = 5;
# In Python:
a = 5               # Python sees 5 -> int
b = 3.14            # Python sees 3.14 -> float
# No type keyword needed
```

*Dynamic binding — same variable, different types in one program*
```python
a = 3
print(a)       # 3   (int)
a = "Hi"
print(a)       # Hi  (str)
# 'a' changed type — totally valid in Python
```

*Multiple assignment (stylish declaration)*
```python
# Assign different values to three variables in one line
a, b, c = 4, 4, 6
print(a, b, c)   # 4 4 6

# Assign the same value to multiple variables
a = b = c = 7
print(a, b, c)   # 7 7 7
```

---

**Practice programs for this section:**

1. Swap two variables without a temporary variable:
```python
x = 10
y = 20
x, y = y, x
print(x, y)   # 20 10
```

2. Ask the user for their name, store it in a variable, and greet them:
```python
name = input("Enter your name: ")
print("Hello,", name)
```

---

## Section: Comments

### Comments

**What is it?** Lines in your code that Python's interpreter completely ignores — used to explain your logic to other developers (and your future self).

**Where it's used / interview angle:**
Not an interview question itself, but the instructor strongly emphasised: *always comment your code*. In team settings, uncommented code is a liability. Also: Python only has single-line comments natively (via `#`).

**Types / forms, each with an example:**

*Single-line comment — above the code*
```python
# Add two numbers
a = 5
b = 6
print(a + b)   # 10
```

*Inline comment — beside the code*
```python
a = 5    # first number
b = 6    # second number
```

> **Note from instructor:** Python has no true multi-line comment syntax. Use `#` on every line. Triple-quoted strings `"""..."""` can *look* like multi-line comments but are actually string literals — companies don't use this pattern in production.

---

## Section: Keywords & Identifiers

### Keywords

**What is it?** Reserved words that Python's interpreter uses internally to understand your code. You cannot use them as variable names or any other identifier.

**Where it's used / interview angle:**
Interviewers sometimes test: *"What happens if you name a variable `if` or `print`?"* -> SyntaxError / unexpected behavior. Also: *"What is the role of keywords in a compiled/interpreted language?"*

**Key facts:**
- Python 3 has **35 keywords** (the instructor said ~32; the exact count varies by minor version — don't memorise the number, just know they exist).
- Examples: `if`, `else`, `for`, `while`, `True`, `False`, `None`, `and`, `or`, `not`, `in`, `is`, `def`, `class`, `return`, `import`, `from`, `as`, `pass`, `break`, `continue`, `lambda`, `with`, `yield`, `del`, `raise`, `try`, `except`, `finally`, `global`, `nonlocal`, `assert`

*Checking all keywords programmatically:*
```python
import keyword
print(keyword.kwlist)   # prints the full list
```

### Identifiers

**What is it?** Any name you create in your program — variable names, function names, class names. Basically, anything you name yourself.

**Where it's used / interview angle:**
If a student's code throws a weird `SyntaxError` on a variable name, it's usually an identifier rule violation. Good to know the rules cold.

**Rules for valid identifiers:**
1. **Cannot start with a digit** — `1name` is invalid, `name1` is valid
2. **Only letters, digits, and underscore `_`** — no hyphens, spaces, or other special chars
3. **Cannot be a keyword** — `if = 5` is invalid

**Example:**
```python
# Valid identifiers
first_name = "Wajid"
_count = 0
value2 = 42

# Invalid — would cause SyntaxError
# 1name = "Wajid"      # starts with digit
# first-name = "X"     # hyphen not allowed
# if = 5               # keyword
```

---

**Practice programs for this section:**

1. Use `keyword.iskeyword()` to check if a user-entered word is a keyword:
```python
import keyword
word = input("Enter a word: ")
print(keyword.iskeyword(word))
```

2. Try naming a variable with a keyword and observe the error (then fix it):
```python
# for = 10    <- SyntaxError; rename to: loop_for = 10
loop_for = 10
print(loop_for)
```

---

## Section: User Input

### `input()` function

**What is it?** A built-in function that pauses execution and waits for the user to type something, then returns what they typed as a **string**.

**Subtopics:**
- Basic usage (no prompt)
- With a prompt message (best practice)
- Why `input()` always returns `str` — and what to do about it

**Where it's used / interview angle:**
A classic gotcha: *"A user enters `5` and `6` and you add them — what does your program print?"* If you didn't convert types, it prints `56` instead of `11`. This is the most common beginner bug and a valid interview question about types.

**Why `input()` always stores as string:**
> String is the "universal" data format — you can store any other type's representation in a string (e.g., `"42"`, `"3.14"`, `"True"`), but you can't go the other way safely for all cases. So Python's team decided: always default to string to avoid crashes.

**Types / forms, each with an example:**

*Basic input — no prompt (bad UX)*
```python
x = input()
print(x)
```

*Input with prompt (best practice)*
```python
email = input("Enter your email: ")
print("You entered:", email)
```

*Input + type conversion (the usual pattern)*
```python
# WRONG: "56" + "67" = "5667" (string concatenation!)
a = input("First number: ")
b = input("Second number: ")
print(a + b)      # "5667"

# CORRECT: convert first
a = int(input("First number: "))
b = int(input("Second number: "))
print(a + b)      # 123
```

---

**Practice programs for this section:**

1. Take two numbers from the user and print their sum, difference, and product:
```python
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))
print("Sum:", a + b)
print("Difference:", a - b)
print("Product:", a * b)
```

2. Ask for a name and age, print a personalised sentence:
```python
name = input("Name: ")
age = int(input("Age: "))
print("Hello " + name + ", you are", age, "years old.")
```

---

## Section: Type Conversion

### Type Conversion

**What is it?** Converting a value from one data type to another. Python does this automatically in some cases (implicit), or you do it manually (explicit).

**Subtopics:**
- Implicit type conversion — Python handles it silently
- Explicit type conversion — you call a conversion function
- Key rule: conversion creates a **new object**, the original is unchanged

**Where it's used / interview angle:**
Common MCQ trap: *"After `int(x)`, what is the type of `x`?"* -> **still the original type**. `int(x)` creates a new value; `x` itself is unchanged unless you do `x = int(x)`. Also: *"What is the difference between type casting and type conversion?"* (see Added Context below).

**Types / forms, each with an example:**

*Implicit — Python converts automatically when it is mathematically sensible*
```python
result = 5 + 5.6    # int + float -> Python promotes to float
print(result)       # 10.6
print(type(result)) # <class 'float'>
```

*Implicit fails — Python won't guess across incompatible types*
```python
# print(4 + "3")   # TypeError: can't add int and str
```

*Explicit — you call the conversion function*
```python
# str -> int
x = "3"
y = int(x)
print(y, type(y))    # 3 <class 'int'>

# int -> float
print(float(4))      # 4.0

# int -> str
print(str(5))        # '5'

# str -> int (only works if the string is a valid integer)
print(int("42"))     # 42

# This crashes — non-numeric string:
# int("hello")       # ValueError
```

*Conversion is non-destructive — original unchanged*
```python
s = "56"
result = int(s)     # creates a new int object
print(type(s))      # still <class 'str'>
print(type(result)) # <class 'int'>
```

*Complex -> int is NOT allowed (information loss)*
```python
# int(4 + 5j)   # TypeError — can't drop the imaginary part
```

---

**Practice programs for this section:**

1. Show that type conversion does not modify the original variable:
```python
original = "100"
converted = int(original)
print(type(original))    # str
print(type(converted))   # int
```

2. Take a float from the user, show its truncated int and its string form:
```python
n = float(input("Enter a decimal number: "))
print("As int (truncated):", int(n))
print("As string:", str(n))
```

---

## Section: Literals

### Literals

**What is it?** The raw, fixed values you write directly into your code — the actual data stored in a variable. In `a = 5`, `5` is the literal.

**Subtopics:**
- Numeric literals: integer (decimal, binary, octal, hexadecimal), float, complex
- String literals: single-quote, double-quote, triple-quote, raw, unicode
- Boolean literals: `True`, `False`
- `None` literal

**Where it's used / interview angle:**
The number-system variants (binary `0b`, octal `0o`, hex `0x`) come up in embedded/hardware contexts and occasionally in interview MCQs. The `None` literal is critical — it's used everywhere in Python to represent "no value yet."

**Types / forms, each with an example:**

*Integer literals — four number systems*
```python
a = 0b1010   # Binary  -> 10
b = 105      # Decimal -> 105
c = 0o130    # Octal   -> 200 (1x64 + 3x8 + 0)
d = 0x12C    # Hex     -> 300

print(a, b, c, d)   # 10  105  200  300
```

*Float literals — decimal and scientific notation*
```python
f1 = 10.5        # normal decimal
f2 = 1.5e2       # scientific: 1.5 x 10^2 = 150.0
f3 = 1.5e-3      # scientific: 1.5 x 10^-3 = 0.0015

print(f1, f2, f3)   # 10.5  150.0  0.0015
```

*Complex literals*
```python
x = 3.14j        # purely imaginary
y = 2 + 5j       # real + imaginary

print(y.real)    # 2.0
print(y.imag)    # 5.0
```

*String literals — five forms*
```python
s1 = 'Hello'              # single quotes
s2 = "Hello"              # double quotes (both are equivalent)
s3 = """This is a
multiline string"""        # triple quotes
s4 = "C"                  # single character (still a str in Python)
s5 = u"\U0001F600"        # unicode literal (emoji)
s6 = r"raw \n string"     # raw string — backslash is literal

print(s5)   # displays the emoji
print(s6)   # raw \n string  (\n is NOT a newline here)
```

*Boolean literals — map to 1 and 0 internally*
```python
a = True
b = False

print(a + 4)    # 5  (True == 1)
print(b + 3)    # 3  (False == 0)
```

*`None` literal — represents "no value"*
```python
x = None
print(x)           # None
print(type(x))     # <class 'NoneType'>

# Common use: declare a variable before you know its value
result = None
# ... program logic runs ...
# result = some_calculated_value
```

---

**Practice programs for this section:**

1. Show binary, octal, and hex representations of the number 255:
```python
n = 255
print(bin(n))    # 0b11111111
print(oct(n))    # 0o377
print(hex(n))    # 0xff
```

2. Use `None` as a placeholder, then fill it in:
```python
score = None
score = int(input("Enter your score: "))
if score >= 50:
    print("Pass")
else:
    print("Fail")
```

---

## Added context (not in the video/your notes)

**f-strings (formatted string literals):**
The instructor used `"Hello " + name` style. Python 3.6+ has f-strings: `f"Hello {name}"` — cleaner and faster. You'll see this in every modern codebase. Example: `print(f"Sum of {a} and {b} is {a+b}")`. Commonly asked in interviews: *"What are f-strings and how do they differ from `.format()`?"* You'll need these in the next session when we write more complex output.

**`isinstance()` vs `type()`:**
`type(x) == int` checks the exact type. `isinstance(x, int)` also returns `True` for subclasses. In real code and interviews, `isinstance()` is preferred. Example: `isinstance(True, int)` -> `True` (because `bool` is a subclass of `int`). Commonly asked in interviews.

**Type casting vs type conversion — the strict difference:**
The instructor briefly mentioned this. Strict definition: *Type casting* = converting and storing the result back (changing the binding permanently, e.g. `x = int(x)`). *Type conversion* = creating a new value without necessarily storing it back. In Python, both terms are often used interchangeably, but the key interview point is: Python's conversion always creates a **new object**, it never modifies the original in-place.

**`None` vs `0` vs `False` vs `""` — all "falsy" but not equal:**
```python
print(None == 0)      # False
print(None == False)  # False
print(bool(None))     # False  <- None is falsy
```
This comes up in if-statements and is a classic interview trap.

**Identifier naming conventions (PEP8):**
- Variables and functions: `snake_case` (e.g., `first_name`)
- Constants: `UPPER_CASE` (e.g., `MAX_SIZE`)
- Classes: `PascalCase` (e.g., `MyClass`)
You'll need this for the "Production-Ready Python Mindset" later in the roadmap.

**Static software vs dynamic software (mentioned in input() section):**
The instructor explained this as: static software = user can't interact (e.g., a clock, a calendar — info only); dynamic software = user interacts (e.g., YouTube, Zomato, Ola). This is why `input()` matters — it's what makes programs dynamic.

---

## Quick recap (cheat-sheet)

| Concept | What to remember |
|---|---|
| `print(a, b, sep=X, end=Y)` | `sep` between items, `end` after last (default `\n`) |
| Data types | `int`, `float`, `complex`, `str`, `bool`, `list`, `tuple`, `set`, `dict` |
| `type(x)` | Returns the type of `x` at runtime |
| Variable | Named container; write `name = value`, no type keyword needed |
| Dynamic typing | Python infers the type from the value automatically |
| Dynamic binding | Same variable can hold different types at different points in a program |
| Comment | `#` ignores rest of line; Python has no built-in multi-line comment |
| Keyword | ~35 reserved words; can't use as identifiers (`if`, `for`, `True`, etc.) |
| Identifier | Any name you create; can't start with digit; only `_` as special char; can't be a keyword |
| `input()` | Always returns `str`; wrap with `int()` / `float()` to convert |
| Implicit type conversion | Python does it automatically when safe (e.g., `int + float -> float`) |
| Explicit type conversion | You call `int()`, `float()`, `str()`, etc.; creates a **new** object |
| Literals | Raw values in code: `42`, `3.14`, `"hi"`, `True`, `None`, `0b1010`, `1.5e2` |
| `None` | Represents "no value"; type is `NoneType`; used as a placeholder |
| Boolean arithmetic | `True == 1`, `False == 0`; can use in math expressions |

---

## Practice check

1. What will this print, and why?
```python
a = "10"
b = "20"
print(a + b)
```

2. After running the code below, what is the type of `x`? What is the type of `int(x)`?
```python
x = "42"
result = int(x)
```

3. Write a program that takes a user's age as input and prints whether they are a minor (under 18) or an adult — handle the fact that `input()` returns a string.
