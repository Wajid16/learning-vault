# Session 03: Loops Wrap-Up & Python Strings

> 🎥 **Source:** [Session 3 - Python Strings | CampusX Data Science Mentorship Program](https://www.youtube.com/live/6HAu0Y9BjA4?si=G0nzYrn6otXGAGPQ) · 📅 9 Nov 2022 · 📚 **Course:** Python for AI Engineering

---

## Table of Contents
1. [TL;DR](#tldr)
2. [Loops Wrap-Up](#loops-wrap-up)
    - [Correction to Population Decay Loop](#correction-to-population-decay-loop)
    - [Sum of Factorials Series Program](#sum-of-factorials-series-program)
    - [Nested Loops & Coordinates Output](#nested-loops--coordinates-output)
    - [Star Triangle Pattern Printing](#star-triangle-pattern-printing)
    - [Break Statement (Linear Search Analogy & Prime Range Checker)](#break-statement-linear-search-analogy--prime-range-checker)
    - [Continue Statement (E-Commerce Stock Analogy)](#continue-statement-e-commerce-stock-analogy)
    - [Pass Statement (Block Placeholder)](#pass-statement-block-placeholder)
3. [Introduction to Python Strings](#introduction-to-python-strings)
    - [Definition & Unicode vs. ASCII](#definition--unicode-vs-ascii)
4. [Creating Strings](#creating-strings)
    - [Quotes & Multi-Line Text](#quotes--multi-line-text)
5. [Accessing Characters (Indexing)](#accessing-characters-indexing)
    - [Positive & Negative Indexing](#positive--negative-indexing)
6. [Slicing Strings](#slicing-strings)
    - [Substrings & Step Parameters](#substrings--step-parameters)
    - [Reversing a String](#reversing-a-string)
7. [Mutability & Immutability Rules](#mutability--immutability-rules)
8. [String Operations](#string-operations)
    - [Arithmetic Operations](#arithmetic-operations)
    - [Relational (Lexicographical) Operations](#relational-lexicographical-operations)
    - [Logical (Short-Circuit) Operations](#logical-short-circuit-operations)
    - [Loop Iterations & Membership Checks](#loop-iterations--membership-checks)
9. [Common String Functions & Methods](#common-string-functions--methods)
    - [Common Functions (len, max, min, sorted)](#common-functions-len-max-min-sorted)
    - [String-Specific Methods](#string-specific-methods)
10. [String Programming Exercises](#string-programming-exercises)
    - [Program 1: Substring Frequency Count (Without count())](#program-1-substring-frequency-count-without-count)
    - [Program 2: Remove Character from String](#program-2-remove-character-from-string)
    - [Program 3: Check Palindrome (Without Reverse Slicing)](#program-3-check-palindrome-without-reverse-slicing)
    - [Program 4: Count Words (Without split())](#program-4-count-words-without-split)
    - [Program 5: Title Case Conversion (Without title())](#program-5-title-case-conversion-without-title)
    - [Program 6: Integer to String Casting (Without str())](#program-6-integer-to-string-casting-without-str)
11. [Added Context (For AI Engineers)](#added-context-for-ai-engineers)
12. [Quick Recap](#quick-recap)
13. [Practice Check](#practice-check)

---

## TL;DR

This session begins with a resolution of outstanding loop details (fixing the mathematical representation of population decay, evaluating factorial sequences, building nested loop star patterns, and detailing `break`, `continue`, and `pass`). The focus then shifts to Python Strings. We detail how Python represents text internally using Unicode (16-bit) instead of ASCII (8-bit) and explore string indexing, slicing, and Python's strict immutability constraint. We review common string operations and specific methods (like `split()`, `join()`, and `strip()`). Finally, we walk through 6 coding challenges to build logical programming skills.

---

## Loops Wrap-Up

### Correction to Population Decay Loop

In the previous session, the backward calculation of a town's population declining by 10% was modeled as `population = population - 0.10 * population` (or `population *= 0.9`). 
*   **The Mathematical Flaw:** Subtracting 10% directly from 10,000 gives 9,000. However, if the population increases *forward* by 10% next year, it is calculated as $9,000 \times 1.10 = 9,900$, which does not equal our starting 10,000.
*   **The Correct Math:** To calculate backwards, we must solve the growth equation for the previous year ($P_{\text{prev}}$):
    $$P_{\text{curr}} = P_{\text{prev}} + 0.10 \times P_{\text{prev}} = 1.10 \times P_{\text{prev}} \implies P_{\text{prev}} = \frac{P_{\text{curr}}}{1.10}$$

**Corrected Code:**
```python
population = 10000

for year in range(10, 0, -1):
    print(f"Year {year}: {round(population)}")
    # Divide by 1.10 to find previous year's population
    population = population / 1.10
```

---

### Sum of Factorials Series Program

**Problem Statement:** Take integer $n$ and calculate the sum of the series: 
$$\frac{1}{1!} + \frac{2}{2!} + \frac{3}{3!} + \dots + \frac{n}{n!}$$

**Mental Model:**
Track a running sum (`result`) and a running factorial (`fact`). In each step $i$, calculate $i!$ by updating `fact = fact * i` and add $i / fact$ to the sum.

**Code implementation:**
```python
n = int(input("Enter number of terms (n): "))
result = 0.0
fact = 1

for i in range(1, n + 1):
    fact *= i  # Updates to represent i!
    result += i / fact

print("Sum of series:", result)
```

---

### Nested Loops & Coordinates Output

A nested loop is a loop inside another loop's code block. The inner loop executes all of its iterations for every single iteration of the outer loop.

**Coordinate Pairs Program:**
```python
# Prints combinations of coordinate pairs (i, j)
for i in range(1, 5):      # Outer loop (runs 4 times)
    for j in range(1, 5):  # Inner loop (runs 4 times per outer loop)
        print(f"({i}, {j})", end=" ")
    print()  # Line break after inner loop completes
```

**Interview / exam angle:**
*   *Question:* "What is the time complexity of the nested coordinate printing block above?"
*   *Answer:* The outer loop runs $N$ times (where $N=4$) and the inner loop runs $M$ times (where $M=4$). The print statement is executed $N \times M$ times. The overall time complexity is $O(N \times M)$ (or $O(N^2)$ if both loops scale to $N$).

---

### Star Triangle Pattern Printing

**Problem Statement:** Prompt the user for the number of rows and print a right-angled triangle pattern of asterisks.
```
*
* *
* * *
* * * *
```

**Code implementation:**
```python
rows = int(input("Enter number of rows: "))

for i in range(1, rows + 1):
    for j in range(1, i + 1):
        print("*", end=" ")
    print()  # Move to next line
```

---

### Break Statement (Linear Search Analogy & Prime Range Checker)

The `break` statement terminates the active loop immediately. Control jumps to the first statement outside the loop block.

**Analogy (Linear Search):**
If you are searching a database of 10,000,000 customer records for a specific username and find it at index 50, it is inefficient to check the remaining 9,999,950 records. You use `break` to stop the search loop immediately once the record is found.

**Prime Range Checker Program (Using Loop `else`):**
In Python, if a loop finishes naturally without hitting a `break` statement, its optional `else` block executes. If it hits a `break`, the `else` block is skipped.
```python
lower = int(input("Enter lower range: "))
upper = int(input("Enter upper range: "))

print(f"Prime numbers between {lower} and {upper}:")
for num in range(lower, upper + 1):
    if num > 1:
        # Check for divisors
        for divisor in range(2, num):
            if num % divisor == 0:
                break  # Not prime, exit the inner loop
        else:
            # Executes only if inner loop ran fully without hitting 'break'
            print(num, end=" ")
print()
```

---

### Continue Statement (E-Commerce Stock Analogy)

The `continue` statement skips the remaining code inside the active loop iteration and jumps directly to the evaluation of the next iteration cycle.

**Analogy (E-Commerce Stock):**
When iterating through a list of products to render a catalog web page, if a product's stock count is 0 (out of stock), the system can call `continue` to skip rendering that specific card and proceed to the next item.

**Code example:**
```python
# Print numbers 1 to 10, skipping 5
for i in range(1, 11):
    if i == 5:
        continue  # Skip print statement for 5
    print(i, end=" ")
# Output: 1 2 3 4 6 7 8 9 10
print()
```

---

### Pass Statement (Block Placeholder)

The `pass` statement is a null operation. It acts as a syntactic placeholder when a code block is required (e.g., inside an `if` statement, loop, or function definition) but you have not yet written the logic. Leaving a block empty in Python causes an `IndentationError`.

**Code example:**
```python
for i in range(1, 10):
    if i % 2 == 0:
        pass  # TODO: Handle even numbers later
    else:
        print(i, "is odd")
```

---

## Introduction to Python Strings

### Definition & Unicode vs. ASCII

A **String** is a sequence of characters. In Python, strings are treated as sequences of **Unicode** characters rather than simple ASCII characters.

| Feature | ASCII (American Standard Code) | Unicode |
|---|---|---|
| **Bit Width** | 8-bit (historically 7-bit). | 16-bit to 32-bit. |
| **Character Limit** | $2^8 = 256$ characters maximum. | $2^{16} = 65,536$ up to millions of characters. |
| **Language Support** | Standard English, basic symbols, numbers. | Global alphabets (Hindi, Chinese, etc.), Emojis, math symbols. |
| **Python Integration** | Default in older languages (C, C++). | Default string representation in Python 3. |

**Code example:**
```python
# Unicode emojis and Hindi text are supported out of the box in Python strings
emoji_str = "Hello 🤖 नमस्ते"
print(emoji_str)
```

---

## Creating Strings

### Quotes & Multi-Line Text

Strings are created by wrapping text in single quotes (`'`), double quotes (`"`), or triple quotes (`'''` or `"""`).

*   **Single and Double Quotes:** Behave identically. Having both allows nesting quotes without using escape characters.
*   **Triple Quotes:** Used to define multi-line strings or docstrings.

**Code example:**
```python
# Nesting quotes to avoid escape characters
sentence1 = "It's raining outside"  # Outer double quotes, inner single quote works
sentence2 = 'He said, "Python is clean"'  # Outer single quotes, inner double quotes works

# Multi-line string using triple quotes
paragraph = """This is line one.
This is line two of a multi-line string."""
print(paragraph)
```

---

## Accessing Characters (Indexing)

### Positive & Negative Indexing

Python supports two indexing directions to reference characters within a string:
1.  **Positive Indexing (Left-to-Right):** Starts at `0` for the first character and increments up to `length - 1`.
2.  **Negative Indexing (Right-to-Left):** Starts at `-1` for the last character and decrements down to `-length`.

```
 String:  P   y   t   h   o   n
 Pos:     0   1   2   3   4   5
 Neg:    -6  -5  -4  -3  -2  -1
```

**Code example:**
```python
s = "Python"

# Positive Indexing
print(s[0])   # Output: 'P'
print(s[4])   # Output: 'o'

# Negative Indexing
print(s[-1])  # Output: 'n' (Last character)
print(s[-3])  # Output: 'h'

# Indexing Out of Bounds raises IndexError
try:
    print(s[10])
except IndexError as e:
    print("Caught Error:", e)  # Output: string index out of range
```

---

## Slicing Strings

### Substrings & Step Parameters

Slicing extracts a subset (substring) of a string using the syntax: `s[start:stop:step]`
*   `start`: Index to begin extraction (inclusive, defaults to 0).
*   `stop`: Index to end extraction (exclusive, defaults to string length).
*   `step`: Interval step size (defaults to 1). If the step is negative, the extraction runs backwards.

> 💡 **Negative Step Rule:** When using a negative step size (e.g., `-1`), the `start` index must be **greater** than the `stop` index (moving from right to left). Otherwise, it returns an empty string `""`.

**Code example:**
```python
s = "Hello World"

# Basic Slice (exclusive of stop index)
print(s[0:5])   # Output: 'Hello' (indexes 0, 1, 2, 3, 4)

# Skip start (defaults to 0) or stop (defaults to end)
print(s[:5])    # Output: 'Hello'
print(s[6:])    # Output: 'World'

# Using step size
print(s[0:11:2]) # Output: 'HloWrd' (every second character)

# Slicing with negative step size (start > stop)
print(s[10:5:-1])  # Output: 'dlroW' (extracts backwards)
```

---

### Reversing a String

By leaving the `start` and `stop` fields blank and setting the step size to `-1`, you can reverse a string in a single line of code.

**Code example:**
```python
s = "transformer"
reversed_s = s[::-1]
print(reversed_s)  # Output: 'remrofsnart'
```

---

## Mutability & Immutability Rules

In Python, strings are **immutable**. Once a string object is created in memory, its characters cannot be modified or updated in-place. Any operations that appear to modify a string (like `.lower()` or `.replace()`) actually construct and return a **new string object** at a different memory location.

**Code example demonstrating Immutability Errors:**
```python
s = "hello"

# Trying to reassign a single character raises a TypeError
try:
    s[0] = "H"
except TypeError as e:
    # Output: 'str' object does not support item assignment
    print("Error:", e)

# Trying to delete a character or slice also raises a TypeError
try:
    del s[0]
except TypeError as e:
    # Output: 'str' object doesn't support item deletion
    print("Error:", e)

# You can, however, delete the entire variable name reference
del s
```

---

## String Operations

### Arithmetic Operations

*   `+` (Concatenation) — Joins two strings together. Requires both operands to be strings.
*   `*` (Repetition) — Repeats the string a specified number of times. Requires one operand to be a string and the other to be an integer.

**Code example:**
```python
# Concatenation
print("Deep" + "Learning")  # Output: 'DeepLearning'

# Repetition (Useful for visual block layout formatting)
print("-" * 30)  # Output: '------------------------------'
```

---

### Relational (Lexicographical) Operations

Relational operators (`<`, `>`, `<=`, `>=`, `==`, `!=`) compare strings **lexicographically** (based on alphabetical dictionary ordering, using the underlying ASCII/Unicode numeric values).

*   Uppercase letters have lower Unicode values than lowercase letters (e.g., `A` is `65`, `a` is `97`). Therefore, `"Apple" < "apple"` evaluates to `True`.

**Code example:**
```python
print("Apple" == "Apple")  # True
print("Pune" > "Mumbai")   # True ('P' comes after 'M' in alphabet)
print("Apple" < "apple")   # True (ASCII 65 < 97)
```

---

### Logical (Short-Circuit) Operations

An empty string (`""`) evaluates to a boolean value of `False`. Any string containing one or more characters evaluates to `True`.

*   **`and` Operator:** If the first operand evaluates to `False`, it short-circuits and returns it. Otherwise, it returns the second operand.
*   **`or` Operator:** If the first operand evaluates to `True`, it short-circuits and returns it. Otherwise, it returns the second operand.

**Code example:**
```python
# Empty string is False, non-empty is True
print("" and "Hello")   # Output: "" (First term is False, short-circuits)
print("Hello" and "World") # Output: "World" (First term is True, returns second)
print("Hello" or "World")  # Output: "Hello" (First term is True, short-circuits)
print(not "")           # Output: True
```

---

### Loop Iterations & Membership Checks

*   Strings are **iterables**, meaning you can loop through them character-by-character.
*   The membership operators `in` and `not in` search for a substring inside a string (case-sensitive).

**Code example:**
```python
# String traversal
for char in "BERT":
    print(char, end="-")  # Output: B-E-R-T-
print()

# Membership check
print("GPT" in "GPT-4o")      # Output: True
print("gpt" in "GPT-4o")      # Output: False (Case-sensitive)
```

---

## Common String Functions & Methods

### Common Functions (len, max, min, sorted)

These functions work on most iterable collections in Python (like lists, tuples, and sets).

**Code example:**
```python
s = "Hello World"

print(len(s))       # Output: 11 (Characters including space)
print(max(s))       # Output: 'r' (Highest Unicode value character)
print(min("abc"))   # Output: 'a' (Lowest Unicode value character)

# sorted() returns a sorted list of characters, not a string
print(sorted(s))    # Output: [' ', 'D', 'H', 'W', 'd', 'e', 'l', 'l', 'l', 'o', 'o', 'r']
```

---

### String-Specific Methods

Methods are functions called on a string instance using the dot (`.`) syntax. Because strings are immutable, these methods return new strings and do not modify the original string in-place.

| Method | Description | Example |
|---|---|---|
| `capitalize()` | Capitalizes the first character of the string, lowers the rest. | `"hello WORLD".capitalize() -> "Hello world"` |
| `title()` | Capitalizes the first letter of every word. | `"hello world".title() -> "Hello World"` |
| `upper()` | Converts all characters to uppercase. | `"text".upper() -> "TEXT"` |
| `lower()` | Converts all characters to lowercase. | `"TEXT".lower() -> "text"` |
| `swapcase()` | Inverts case of all characters. | `"Py".swapcase() -> "pY"` |
| `count(sub)` | Counts non-overlapping occurrences of substring. | `"hello".count("l") -> 2` |
| `find(sub)` | Returns index of first occurrence of substring, or `-1` if not found. | `"hello".find("e") -> 1` |
| `index(sub)` | Same as `find()`, but raises a `ValueError` if not found. | `"hello".index("z") -> ValueError` |
| `startswith(sub)` | Returns `True` if string starts with substring. | `"GPT-4".startswith("GP") -> True` |
| `endswith(sub)` | Returns `True` if string ends with substring. | `"file.csv".endswith(".csv") -> True` |
| `format()` | Formats placeholders `{}` with provided values. | `"{0} is {1}".format("AI", "cool") -> "AI is cool"` |
| `isalnum()` | Returns `True` if all characters are alphanumeric. | `"user123".isalnum() -> True` |
| `isalpha()` | Returns `True` if all characters are alphabetic. | `"user123".isalpha() -> False` |
| `isdigit()` | Returns `True` if all characters are digits. | `"12345".isdigit() -> True` |
| `isidentifier()` | Returns `True` if string is a valid variable name. | `"class".isidentifier() -> True` |
| `split(delim)` | Splits string into a list of substrings using a delimiter. | `"A,B,C".split(",") -> ['A', 'B', 'C']` |
| `join(iterable)` | Joins an iterable of strings using the string as a separator. | `"-".join(['A', 'B']) -> "A-B"` |
| `replace(old, new)`| Replaces occurrences of `old` substring with `new`. | `"test".replace("t", "p") -> "pesp"` |
| `strip()` | Removes leading and trailing whitespace characters. | `"  test  ".strip() -> "test"` |

**Code examples:**
```python
# Format method with positional routing
sentence = "User {1} has role {0}".format("Admin", "Alice")
print(sentence)  # Output: "User Alice has role Admin"

# Split & Join
data = "Llama-2,GPT-4,Claude-3"
models_list = data.split(",")  # Splits at commas
print(models_list)  # Output: ['Llama-2', 'GPT-4', 'Claude-3']

joined_data = " | ".join(models_list)  # Joins list with separator
print(joined_data)  # Output: "Llama-2 | GPT-4 | Claude-3"
```

---

## String Programming Exercises

### Program 1: Substring Frequency Count (Without count())

**Problem Statement:** Write a program that counts the number of times a search term appears in a given sentence, without using the built-in `.count()` method.

**Code implementation:**
```python
sentence = input("Enter sentence: ")
target = input("Enter search term: ")

count = 0
target_len = len(target)

# Iterate through all slice start positions
for i in range(len(sentence) - target_len + 1):
    # Slice a substring of the target length
    if sentence[i : i + target_len] == target:
        count += 1

print("Occurrence count:", count)
```

---

### Program 2: Remove Character from String

**Problem Statement:** Take a string input and a target character to remove. Return a new string with all occurrences of that character removed, without using the `.replace()` method.

**Concept:**
Because strings are immutable, we cannot delete characters in-place. We must initialize an empty results string, iterate through the input string, and append all characters *except* the target character.

**Code implementation:**
```python
string = input("Enter string: ")
char_to_remove = input("Character to remove: ")
result = ""

for char in string:
    if char != char_to_remove:
        result += char

print("Result:", result)
```

---

### Program 3: Check Palindrome (Without Reverse Slicing)

**Problem Statement:** Determine if an input string is a palindrome (reads the same forwards and backwards) without using the `s[::-1]` slicing shortcut.

**Concept:**
Iterate from the start up to the middle index (`len(s) // 2`). Compare the character at the current index `i` with the corresponding character at the end of the string `-(i + 1)`. If they do not match, the string is not a palindrome.

**Code implementation:**
```python
s = input("Enter string: ").strip().lower()
is_palindrome = True

# Check up to middle character
for i in range(len(s) // 2):
    # Compare start character with corresponding end character
    if s[i] != s[-(i + 1)]:
        is_palindrome = False
        break

if is_palindrome:
    print("The string is a palindrome.")
else:
    print("The string is not a palindrome.")
```

---

### Program 4: Count Words (Without split())

**Problem Statement:** Recreate the basic behavior of `.split(" ")` to extract words from a sentence separated by spaces, without using the built-in `.split()` method.

**Concept:**
Iterate through the string character by character. Accumulate characters in a temporary string (`temp`). When a space is encountered, append `temp` to a results list (if it's not empty) and reset `temp` to an empty string. After the loop completes, append any remaining characters in `temp` to the list.

**Code implementation:**
```python
sentence = input("Enter sentence: ")
words = []
temp = ""

for char in sentence:
    if char == " ":
        if temp:  # Avoid appending empty strings if multiple spaces exist
            words.append(temp)
            temp = ""
    else:
        temp += char

# Append last word
if temp:
    words.append(temp)

print("Words list:", words)
print("Word count:", len(words))
```

---

### Program 5: Title Case Conversion (Without title())

**Problem Statement:** Convert an input sentence to title case (where the first letter of every word is capitalized and the remaining letters are lowercase) without using the built-in `.title()` method.

**Code implementation:**
```python
sentence = input("Enter sentence: ")
words = sentence.split()
title_words = []

for word in words:
    # Capitalize first char, lowercase the rest
    transformed = word[0].upper() + word[1:].lower()
    title_words.append(transformed)

# Join the words back together with a space separator
title_sentence = " ".join(title_words)
print("Title Case Result:", title_sentence)
```

---

### Program 6: Integer to String Casting (Without str())

**Problem Statement:** Write a program that converts an integer value (e.g. `345`) to its string representation (e.g. `"345"`) without using the built-in `str()` function.

**Concept:**
Create a lookup string index `"0123456789"`. Extract digits one by one from the end of the number using `% 10` math. Look up the corresponding character in the index string and prepend it to your result string. Then, update the number using floor division `// 10` to strip off the last digit.

**Code implementation:**
```python
number = int(input("Enter integer: "))
digits_lookup = "0123456789"
result = ""

# Handle edge case where input is exactly 0
if number == 0:
    result = "0"

# Track if number is negative
is_negative = False
if number < 0:
    is_negative = True
    number = abs(number)

while number > 0:
    digit = number % 10
    # Prepend matching character from digits lookup string
    result = digits_lookup[digit] + result
    number = number // 10

if is_negative:
    result = "-" + result

print("String representation:", result)
print("Data type:", type(result))
```

---

## Added Context (For AI Engineers)

### 1. Slicing in Transformer Token Arrays
In modern LLM architectures (like GPT or Llama), text is converted into arrays of tokens. When implementing sliding window attention mechanisms, sequence chunking, or positional context limits, Python's list and string slicing syntax is used to split context windows.
```python
# Simulating a sliding context window of size 4 tokens
tokens = ["User", "wants", "to", "learn", "how", "to", "code", "agents"]
window_size = 4

# Slide context window across the token array
for i in range(len(tokens) - window_size + 1):
    context_slice = tokens[i : i + window_size]
    print("Active context window:", context_slice)
```

### 2. Lexicographical Comparisons in Tokenizers
Lexicographical string comparisons are used to sort vocabulary items when building Byte-Pair Encoding (BPE) tokenizers. Vocabularies must be sorted systematically based on character frequencies and lexicographical order to assign token IDs.

### 3. Mutability and GPU Memory Allocation
Because Python strings are immutable, calling string operations inside high-frequency processing loops (like data loader preprocessing pipelines) allocates new memory every iteration. This can create memory overhead. For high-performance deep learning pipelines, string transformations should be performed outside of model training loops, or text should be converted to numeric arrays (like PyTorch Tensors) as early as possible.

### 4. Split and Join in Structured LLM Outputs
When parsing structured text outputs from LLMs (such as parsing CSV data, log directories, or tool arguments), the `.split()` and `.join()` methods are used to extract key values from formatted string responses.
```python
# Parsing structured tool invocation strings from LLMs
tool_call_response = "TOOL:retriever_tool | QUERY:vector databases | LIMIT:5"

# Parse arguments using split operations
args = {}
parts = tool_call_response.split(" | ")
for part in parts:
    key, val = part.split(":")
    args[key] = val

print("Parsed Tool Arguments:", args)
# Output: {'TOOL': 'retriever_tool', 'QUERY': 'vector databases', 'LIMIT': '5'}
```

---

## Quick Recap

| Concept | Key Takeaway |
|---|---|
| `break` vs `continue` | `break` exits the active loop immediately; `continue` skips the rest of the current iteration and jumps to the next cycle. |
| ASCII vs Unicode | ASCII is an 8-bit mapping (max 256 characters); Unicode is a 16-to-32-bit mapping (allows emojis and multi-language support). |
| Negative Indexing | Accesses characters starting from the end of the string (`s[-1]` is the last character). |
| Reverse Slicing | `s[::-1]` reverses a string. When using a negative step size, `start` index must be greater than `stop` index. |
| Immutability | String objects cannot be modified in-place. Trying to run `s[0] = 'a'` throws a `TypeError`. |
| String Operators | `+` performs concatenation; `*` performs string repetition; relational operators compare lexicographically. |
| `split()` & `join()` | `split()` breaks a string into a list of substrings; `join()` merges an iterable of strings into a single string. |
| `strip()` | Removes leading and trailing whitespace characters. |

---

## Practice Check

1.  **Given the string `s = "AI-Engineering"`, write the slicing expressions to extract:**
    - `"AI"`
    - `"Engineering"`
    - The reversed string `"gnireenignE-IA"`

2.  **Explain the output of the following short-circuit code block:**
    ```python
    x = ""
    y = "Agent"
    z = x or y
    print(z)
    ```

3.  **Evaluate this code block. Will it run or raise an error? Explain why.**
    ```python
    s = "Claude"
    del s[0]
    print(s)
    ```

4.  **Write a Python program that counts the number of uppercase characters in a user-provided string using string traversal and a helper function (e.g. `char.isupper()`).**

---
<!-- Long note complete. Companion: [Quick Recall](quick-recall.md#03-python-strings) -->
