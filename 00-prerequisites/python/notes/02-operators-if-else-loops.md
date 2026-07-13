# Session 02: Operators, Conditionals, Modules, and Loops

> 🎥 **Source:** [Session 2 - Operators + If-Else + Loops | CampusX Data Science Mentorship Program](https://www.youtube.com/live/JCkIrdrZEE8?si=sZUEuKbKZr-4-igW) · 📅 8 Nov 2022 · 📚 **Course:** Python for AI Engineering

---

## Table of Contents
1. [TL;DR](#tldr)
2. [Operators](#operators)
    - [Arithmetic Operators](#arithmetic-operators)
    - [Relational Operators](#relational-operators)
    - [Logical Operators](#logical-operators)
    - [Bitwise Operators](#bitwise-operators)
    - [Assignment Operators](#assignment-operators)
    - [Membership Operators](#membership-operators)
3. [Example Problem: Sum of Digits of a 3-Digit Number](#example-problem-sum-of-digits-of-a-3-digit-number)
4. [Conditionals (If-Else) & Branching](#conditionals-if-else--branching)
    - [Syntax & Indentation](#syntax--indentation)
    - [Simple Login Validation](#simple-login-validation)
    - [Nested If-Else & elif Retries](#nested-if-else--elif-retries)
    - [Minimum of Three Numbers](#minimum-of-three-numbers)
    - [Menu-Driven Calculator](#menu-driven-calculator)
    - [ATM Text Menu (Triple-Quoted Formatting)](#atm-text-menu-triple-quoted-formatting)
5. [Modules in Python](#modules-in-python)
    - [The Import Mechanism](#the-import-mechanism)
    - [Standard Modules (math, keyword, random, datetime)](#standard-modules-math-keyword-random-datetime)
    - [Listing Available Modules](#listing-available-modules)
6. [Loops & Iterations](#loops--iterations)
    - [Introduction & Flipkart Analogy](#introduction--flipkart-analogy)
    - [while Loop & pythontutor.com Visualizer](#while-loop--pythontutorcom-visualizer)
    - [while-else Construct](#while-else-construct)
    - [Guessing Game (Jackpot)](#guessing-game-jackpot)
    - [for Loop & range() Function](#for-loop--range-function)
    - [Traversing Iterables](#traversing-iterables)
    - [Population Decay Reverse Loop Program](#population-decay-reverse-loop-program)
7. [Added Context (For AI Engineers)](#added-context-for-ai-engineers)
8. [Quick Recap](#quick-recap)
9. [Practice Check](#practice-check)

---

## TL;DR

This session covers control flow structures and library modularity in Python. We examine six classes of operators (with a deep look at division behaviors and optimized membership operators), build nested conditional statement architectures, explore code modularization via imports (`math`, `random`, `datetime`), and analyze loop constructs (`while`, `for`, and Python's unique `while-else`). For AI Engineers, these are the mechanisms used for tensor indexing, pipeline branching, model checkpointing, evaluation loops, and custom API retry policies.

---

## Operators

**What is it?**
Operators are symbols that direct the Python interpreter to perform specific mathematical, logical, relational, or bitwise manipulations on data values (operands).

---

### Arithmetic Operators

Used to perform standard mathematical calculations.

| Operator | Name | Syntax | Behavior |
|---|---|---|---|
| `+` | Addition | `a + b` | Adds values. |
| `-` | Subtraction | `a - b` | Subtracts right from left. |
| `*` | Multiplication | `a * b` | Multiplies values. |
| `/` | Division | `a / b` | Always returns a float (e.g., `4 / 2 -> 2.0`). |
| `//` | Floor Division | `a // b` | Divides and truncates the decimal part, returning the floor integer (e.g., `5 // 2 -> 2`). |
| `%` | Modulus | `a % b` | Returns the remainder of division (e.g., `5 % 2 -> 1`). |
| `**` | Exponentiation | `a ** b` | Raises the base to the power of the exponent (e.g., `5 ** 2 -> 25`). |

**Code example:**
```python
# Comparison of Division Operators
print(5 / 2)   # Output: 2.5 (Float Division)
print(5 // 2)  # Output: 2   (Floor Division / Integer Division)
print(5 % 2)   # Output: 1   (Modulus / Remainder)
print(5 ** 3)  # Output: 125 (Exponentiation: 5^3)
```

**Interview / exam angle:**
*   *Question:* "What is the difference between `/` and `//` in Python?"
*   *Answer:* The `/` operator performs float division and always returns a floating-point number, even if the division is clean (e.g., `4 / 2 -> 2.0`). The `//` operator performs floor division, which divides the numbers and rounds the result down to the nearest whole integer (e.g., `-5 // 2 -> -3`).

---

### Relational Operators

Used to compare two values, returning a Boolean value (`True` or `False`).

*   `>` (Greater than), `<` (Less than)
*   `>=` (Greater than or equal to), `<=` (Less than or equal to)
*   `==` (Equal to), `!=` (Not equal to)

**Code example:**
```python
print(10 > 5)   # True
print(10 == 5)  # False
print(10 != 5)  # True
```

---

### Logical Operators

Used to combine conditional statements.

*   `and` — Returns `True` if both statements are true (short-circuits if the first is `False`).
*   `or` — Returns `True` if at least one statement is true (short-circuits if the first is `True`).
*   `not` — Reverses the boolean result (negation).

**Code example:**
```python
print(True and False)  # Output: False
print(True or False)   # Output: True
print(not True)        # Output: False
```

---

### Bitwise Operators

Operate directly on the binary representations of integers.

*   `&` (Bitwise AND) — Sets each bit to `1` if both bits are `1`.
*   `|` (Bitwise OR) — Sets each bit to `1` if at least one bit is `1`.
*   `^` (Bitwise XOR) — Sets each bit to `1` if the bits are different (e.g., `1 ^ 0 -> 1`; `1 ^ 1 -> 0`).
*   `~` (Bitwise NOT) — Inverts all the bits (unary operator, maps to `-(x + 1)` internally due to two's complement).
*   `<<` (Left Shift) — Shifts bits left, filling in zeros from the right. Equivalent to multiplying by $2^{\text{shift}}$.
*   `>>` (Right Shift) — Shifts bits right. Equivalent to integer division by $2^{\text{shift}}$.

**Code example:**
```python
# Bitwise XOR validation (2 ^ 3)
# 2 in binary: 010
# 3 in binary: 011
# XOR result:  001 (1 in decimal)
print(2 ^ 3)  # Output: 1

# Bitwise Shift
print(4 << 1)  # Output: 8  (4 * 2^1)
print(4 >> 1)  # Output: 2  (4 / 2^1)
```

**Interview / exam angle:**
*   *Question:* "What is the utility of bitwise operators in Data Science and AI Engineering?"
*   *Answer:* In high-level AI applications, bitwise operators are rarely used directly in business logic. However, they are highly useful in low-level image processing (computer vision masks), hardware interfacing (robotics control), and high-efficiency feature hashing or compression arrays where memory flags are packed into bit masks.

---

### Assignment Operators

Used to assign values to variables, often combined with an arithmetic or bitwise operation (compound assignment).

*   `=` (Basic assignment)
*   `+=`, `-=`, `*=`, `/=`, `//=`, `%=`, `**=` (Compound math assignments)

**Code example:**
```python
x = 10
x += 5  # Equivalent to: x = x + 5
print(x)  # Output: 15
```

> ⚠️ **[OUTDATED]** Python does not support increment/decrement operators like `x++` or `--x`.
> **Use instead:** `x += 1` or `x -= 1`. Python chose to exclude `++` and `--` to eliminate syntax ambiguity and prevent confusion between pre-increment and post-increment behaviors seen in C/C++.

---

### Membership Operators

Used to test whether a value or variable is found inside a sequence (string, list, tuple, set, or dictionary).

*   `in` — Returns `True` if the value exists in the sequence.
*   `not in` — Returns `True` if the value does not exist in the sequence.

**Code example:**
```python
# String Membership (Case-Sensitive)
print("d" in "Delhi")      # Output: False ("Delhi" has uppercase 'D')
print("D" in "Delhi")      # Output: True

# List Membership
items = [10, 20, 30, 40]
print(50 not in items)     # Output: True
```

**Interview / exam angle:**
*   *Question:* "Why are membership operators (`in` / `not in`) preferred over writing manual search loops?"
*   *Answer:* Membership operators are highly optimized in the Python C-source backend. When used on hashed structures like `set` or `dict`, they check membership in $O(1)$ time complexity. Running a manual loop to search for a value runs in $O(N)$ time complexity and adds Python interpreter overhead.

---

## Example Problem: Sum of Digits of a 3-Digit Number

**Problem Statement:** Take a 3-digit integer input from the user (e.g., `345`) and print the sum of its individual digits (`3 + 4 + 5 = 12`). Solve this using only mathematical operators (without loops or string manipulation).

**Mental Model:** 
To extract digits from the back of a number:
1.  Use `% 10` to get the remainder (which is the last digit).
2.  Use `// 10` to strip off the last digit, shrinking the number.

**Code implementation:**
```python
number = int(input("Enter a 3-digit number: "))  # Example: 345

# Extract last digit: 345 % 10 = 5
a = number % 10

# Shrink number: 345 // 10 = 34
number = number // 10

# Extract second digit: 34 % 10 = 4
b = number % 10

# Shrink number: 34 // 10 = 3
number = number // 10

# Extract first digit: 3 % 10 = 3
c = number % 10

digit_sum = a + b + c
print("Sum of digits:", digit_sum)  # Output: 12
```

---

## Conditionals (If-Else) & Branching

### Syntax & Indentation

**What is it?**
Conditionals create a fork in execution paths (branching) based on whether an expression evaluates to `True` or `False`. 

**Indentation Rule:**
Unlike C/Java which use curly braces `{}` to group code blocks, Python uses indentation (spaces or tabs). A colon `:` indicates the start of a block, and all subsequent lines within that block must be indented by the same level (conventionally 4 spaces).

---

### Simple Login Validation

**Code example:**
```python
# Setup mock credentials database
correct_email = "nitish.campusx@gmail.com"
correct_password = "1234"

email = input("Enter email: ")
password = input("Enter password: ")

# Check credentials using logical and
if email == correct_email and password == correct_password:
    print("Welcome!")
else:
    print("Not correct credentials.")
```

---

### Nested If-Else & elif Retries

**What is it?**
If there are more than two execution branches, `elif` is used. Placing an `if-else` block inside another `if-else` block is called **nesting**.

**Example Scenario:**
1.  If both email and password are correct, welcome the user.
2.  If the email is correct but the password is wrong, tell the user their password was wrong and give them a second chance to enter it.
3.  If everything is wrong, print a failure message.

**Code example:**
```python
correct_email = "nitish.campusx@gmail.com"
correct_password = "1234"

email = input("Enter email: ")
password = input("Enter password: ")

if email == correct_email and password == correct_password:
    print("Welcome!")
elif email == correct_email and password != correct_password:
    print("Incorrect password.")
    # Re-prompt (Nesting)
    new_password = input("Enter password again: ")
    if new_password == correct_password:
        print("Welcome on second attempt!")
    else:
        print("Second attempt failed. Locked out.")
else:
    print("Incorrect credentials.")
```

---

### Minimum of Three Numbers

A program that takes three numbers and finds the smallest among them using comparison operations.

**Code example:**
```python
a = int(input("First number: "))
b = int(input("Second number: "))
c = int(input("Third number: "))

if a < b and a < c:
    print("Smallest is:", a)
elif b < c:
    print("Smallest is:", b)
else:
    print("Smallest is:", c)
```

---

### Menu-Driven Calculator

Demonstrates using `elif` blocks to structure user selection options.

**Code example:**
```python
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))
op = input("Enter operation (+, -, *, /): ")

if op == "+":
    print("Result:", num1 + num2)
elif op == "-":
    print("Result:", num1 - num2)
elif op == "*":
    print("Result:", num1 * num2)
elif op == "/":
    if num2 != 0:
        print("Result:", num1 / num2)
    else:
        print("Error: Division by zero.")
else:
    print("Invalid operator selected.")
```

---

### ATM Text Menu (Triple-Quoted Formatting)

Triple quotes (`"""..."""`) allow formatting long text blocks across multiple lines. This is useful for writing menus.

**Code example:**
```python
menu = """
Hi! How can I help you?
1. Pin Change
2. Balance Check
3. Cash Withdrawal
4. Exit
"""
user_input = int(input(menu))

if user_input == 1:
    print("Initiating PIN change...")
elif user_input == 2:
    print("Fetching balance...")
elif user_input == 3:
    print("Processing withdrawal...")
elif user_input == 4:
    print("Exiting. Thank you!")
else:
    print("Invalid option selected.")
```

---

## Modules in Python

### The Import Mechanism

**What is it?**
A module is a file containing Python code (functions, variables, classes) that you can bring into your own script. This enables **code reusability** ("Don't reinvent the wheel").

*   To use a module, import it using the `import` keyword.
*   Access functions inside the module using the dot (`.`) syntax: `module_name.function_name()`.

---

### Standard Modules (math, keyword, random, datetime)

**Code example:**
```python
# 1. Math Module
import math
print(math.factorial(5))  # Output: 120 (5!)
print(math.floor(6.8))    # Output: 6   (Rounds down to nearest int)

# 2. Keyword Module
import keyword
print("if is a keyword:", keyword.iskeyword("if"))  # Output: True

# 3. Random Module
import random
# Generates a random integer in the range [1, 100] (inclusive)
random_number = random.randint(1, 100)
print("Random index:", random_number)

# 4. Datetime Module
import datetime
# Fetches the server's current timestamp
print(datetime.datetime.now())
```

---

### Listing Available Modules

To see all installed modules in your current Python environment, use the `help()` command.

**Code example:**
```python
# Warning: This outputs a large index of all installed packages
help('modules')
```

---

## Loops & Iterations

### Introduction & Flipkart Analogy

**What is it?**
Loops repeat a block of code multiple times.

**Why does it exist?**
Imagine you are building a smartphone listing page for Flipkart that displays 478 Samsung phones. Writing individual HTML cards for each phone is inefficient. Instead, you design a single container template and put it inside a loop. The loop runs for every phone in the database, automatically updating the name, price, and image.

---

### while Loop & pythontutor.com Visualizer

Runs as long as a specified condition remains `True`.

**Multiplication Table Program:**
```python
number = int(input("Enter number for multiplication table: "))

i = 1
while i < 11:
    print(number, "*", i, "=", number * i)
    i += 1  # Increment loop counter
```

**Understanding execution step-by-step:**
To debug loops, you can copy-paste your code into [pythontutor.com](https://pythontutor.com/). It allows you to visual step line-by-line through your program, inspecting the state of variables at each iteration.

---

### while-else Construct

**What is it?**
A control structure unique to Python. The `else` block appended to a loop executes **only when the loop terminates naturally** (i.e., the loop condition becomes `False`). If the loop is terminated by a `break` statement, the `else` block is skipped.

**Code example:**
```python
x = 1
while x < 3:
    print(x)
    x += 1
else:
    print("Loop completed successfully without interruption.")
# Output:
# 1
# 2
# Loop completed successfully without interruption.
```

---

### Guessing Game (Jackpot)

A guessing game program that generates a random number and challenges the user to find it, giving feedback along the way.

**Code example:**
```python
import random

# Generate jackpot number between 1 and 100
jackpot = random.randint(1, 100)

guess = int(input("Guess the number (1-100): "))
attempts = 1

while guess != jackpot:
    if guess < jackpot:
        print("Incorrect. Guess higher!")
    else:
        print("Incorrect. Guess lower!")
    
    # Prompt user again
    guess = int(input("Guess again: "))
    attempts += 1
else:
    print("Congratulations! You guessed it right.")
    print("Total attempts:", attempts)
```

---

### for Loop & range() Function

The `for` loop in Python iterates over a sequence (like a list, tuple, string) or a range of numbers.

**The `range()` parameters:**
`range(start, stop, step)`
*   `start`: The starting value of the sequence (inclusive, defaults to 0).
*   `stop`: The ending value of the sequence (exclusive).
*   `step`: The increment value between each number (defaults to 1).

**Code example:**
```python
# Prints 1 to 10 (stop parameter is 11, which is excluded)
for i in range(1, 11):
    print(i, end=" ")
# Output: 1 2 3 4 5 6 7 8 9 10
print()

# Odd numbers only (step size of 2)
for i in range(1, 11, 2):
    print(i, end=" ")
# Output: 1 3 5 7 9
print()
```

---

### Traversing Iterables

Python's `for` loop can iterate directly over elements of string and list structures.

**Code example:**
```python
# Loop through a string
for char in "BERT":
    print(char)
# Output:
# B
# E
# R
# T

# Loop through a list
models = ["Llama", "GPT-4", "Claude"]
for model in models:
    print(model)
```

---

### Population Decay Reverse Loop Program

**Problem Statement:** A town has a current population of 10,000. The population has been growing at a rate of 10% each year. Write a program to display the town's population at each of the *past* 10 years (working backwards from 10,000, decreasing by 10% at each step).

**Mental Model:** 
We can count backwards in a loop using a negative step size in `range()`.
`range(start, stop, step)` -> `range(10, 0, -1)` counts from 10 down to 1.

**Code implementation:**
```python
population = 10000

# Loop backwards from year 10 down to year 1
for year in range(10, 0, -1):
    print("Year:", year, "Population:", round(population))
    # Decrease population by 10% for the previous year
    population = population / 1.10
```

---

## Added Context (For AI Engineers)

### 1. Logical Operators in Guardrails
In agentic AI systems, logical operators are used to write rule-based validation guardrails. For example, before executing an expensive database search, you can verify user authorization and token limits.
```python
# Simple guardrail validation
def execute_agent(user_authorized, token_balance):
    if user_authorized and token_balance > 100:
        return "Querying database..."
    else:
        return "Access denied: insufficient tokens or unauthorized."
```

### 2. Membership in RAG Token Matching
When parsing raw chunks of text in a custom RAG (Retrieval-Augmented Generation) pipeline, membership operators (`in` / `not in`) are used to check for blocked phrases or search for exact keyword matches.
```python
blocked_phrases = ["toxic prompt", "system exploit"]
user_query = "How do I perform a system exploit?"

# Loop checks if any blocked phrase is found in the user prompt
for phrase in blocked_phrases:
    if phrase in user_query:
        print("Prompt rejected by safety guardrails.")
        break
```

### 3. while-else in API Retry Logics
A practical application of Python's `while-else` construct is implementing API retry logic. If your code tries to call the OpenAI API a set number of times and breaks on success, the `else` block will execute **only if all retries fail** (i.e., the loop completes naturally without success).
```python
import random

retries = 3
attempt = 1
success = False

while attempt <= retries:
    print(f"Calling LLM API (Attempt {attempt})...")
    # Simulate API success chance
    if random.random() > 0.8:
        print("API Call Successful!")
        success = True
        break
    attempt += 1
else:
    # Executes only if the loop completed all iterations without breaking
    print("Alert: All API retries failed. Initiating fallback server.")
```

### 4. for loops in Training & Learning Rate Decay
The reverse population loop model ($P_{new} = P_{old} / 1.10$) mirrors the calculation of **Exponential Learning Rate Decay** in neural network optimization. At each epoch step, the learning rate is scaled down to allow the gradient descent algorithm to converge smoothly.
```python
learning_rate = 0.01
decay_rate = 0.95

# Training loop
for epoch in range(1, 6):
    print(f"Epoch {epoch} | Learning Rate: {learning_rate:.6f}")
    # Exponential decay
    learning_rate *= decay_rate
```

---

## Quick Recap

| Concept | Key Takeaway |
|---|---|
| `/` vs `//` | `/` performs float division (returns float); `//` performs floor division (returns truncated int). |
| Bitwise XOR (`^`) | Evaluates bits: returns `1` if the bits are different, `0` if they are the same. |
| Assignment | Python has no `++` or `--` operators. Use `x += 1` instead. |
| Membership | `in` and `not in` test if a value is contained in a sequence. Runs in $O(1)$ time for sets/dicts. |
| Conditionals | Code blocks are defined using colons `:` and indentation (conventionally 4 spaces). |
| Modules | Bring in pre-built code via `import`. Standard modules include `math`, `random`, `datetime`. |
| `while-else` | The `else` block runs only if the loop terminates naturally without hitting a `break` statement. |
| `range()` | Generates a sequence of integers: `range(start, stop, step)`. Stop limit is exclusive. |

---

## Practice Check

1.  **Given `x = 7` and `y = 2`, explain the differences in output between `x / y`, `x // y`, and `x % y`.**

2.  **Evaluate the following code. What does it print and why?**
    ```python
    x = 10
    while x > 5:
        x -= 2
        if x == 6:
            break
    else:
        print("Loop ended naturally.")
    ```

3.  **Write a program that prompts the user for their age. If they enter an age under 13, print "Child". If they are between 13 and 19 (inclusive), print "Teenager". Otherwise, print "Adult". Use `if-elif-else` control flow.**

4.  **Use a `for` loop and the `range()` function to print all multiples of 5 between 50 and 10 (inclusive, counting downwards).**

---
<!-- Long note complete. Companion: [Quick Recall](quick-recall.md#02-operators-conditionals-and-loops) -->
