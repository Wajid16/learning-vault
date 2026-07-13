# Session 04: Python Lists

> 🎥 **Source:** [Session 4 - Lists in Python | CampusX Data Science Mentorship Program](https://www.youtube.com/live/WmbU3WBaoR0?si=ph9tYClhLJ_T8fov) · 📅 14 Nov 2022 · 📚 **Course:** Python for AI Engineering

---

## Table of Contents
1. [TL;DR](#tldr)
2. [What is a Python List?](#what-is-a-python-list)
3. [Arrays vs. Lists](#arrays-vs-lists)
4. [Storage Model: The Referential Array](#storage-model-the-referential-array)
    - [Memory Layout Comparison](#memory-layout-comparison)
    - [Verifying Addresses with id()](#verifying-addresses-with-id)
5. [Creating Lists](#creating-lists)
6. [Accessing Items (Indexing & Slicing)](#accessing-items-indexing--slicing)
    - [Positive & Negative Indexing](#positive--negative-indexing)
    - [Nested Indexing in Multi-Dimensional Lists](#nested-indexing-in-multi-dimensional-lists)
    - [List Slicing](#list-slicing)
7. [Adding Items to a List](#adding-items-to-a-list)
    - [append() vs. extend() vs. insert()](#append-vs-extend-vs-insert)
8. [Editing Items (Mutability)](#editing-items-mutability)
9. [Deleting Items](#deleting-items)
    - [del vs. remove() vs. pop() vs. clear()](#del-vs-remove-vs-pop-vs-clear)
10. [Traversing Lists (Loops)](#traversing-lists-loops)
    - [Item-wise vs. Index-wise Traversals](#item-wise-vs-index-wise-traversals)
11. [Built-in Functions & Methods](#built-in-functions--methods)
12. [List Comprehension](#list-comprehension)
    - [Cartesian Products & Matrix Generation](#cartesian-products--matrix-generation)
13. [The zip() Function](#the-zip-function)
14. [storing Arbitrary Objects in Lists](#storing-arbitrary-objects-in-lists)
15. [Disadvantages & Mutation Risks](#disadvantages--mutation-risks)
    - [The Risk of Reference Assignment](#the-risk-of-reference-assignment)
    - [Creating True Copies with copy()](#creating-true-copies-with-copy)
16. [List Algorithms & Exercises](#list-algorithms--exercises)
17. [Added Context (For AI Engineers)](#added-context-for-ai-engineers)
18. [Quick Recap](#quick-recap)
19. [Practice Check](#practice-check)

---

## TL;DR

This session provides an in-depth exploration of **Python Lists**. We cover their dynamic structure and contrast them with low-level static arrays. We explain the **Referential Array** memory model, which allows lists to store heterogeneous data types by storing references to objects rather than the actual values. We demonstrate indexing, slicing, mutability operations (editing, inserting, extending, and deleting), and the two primary loop traversal techniques. Finally, we explore advanced constructs like **List Comprehensions**, the `zip()` utility, the mechanics of reference-assignment risks, and practical list algorithms.

---

## What is a Python List?

A **List** in Python is an ordered, mutable sequence of elements. It is one of the most flexible and widely used built-in data structures in the language.
*   **Ordered:** The sequence maintains the exact insertion order of elements.
*   **Mutable:** Elements can be added, updated, or removed in-place without generating a new object in memory.
*   **Heterogeneous:** Elements within a single list can be of different data types (integers, strings, floats, lists, functions, classes).

**Code example:**
```python
# A list containing different types of objects
mixed_list = [20, "dataset", 35.7, [1, 2, 3]]
print(mixed_list)
```

---

## Arrays vs. Lists

While lists are conceptually similar to arrays in other programming languages (like C, C++, or Java), they are implemented differently under the hood.

| Feature | Static Arrays (C / C++ / Java) | Python Lists (Dynamic / Referential) |
|---|---|---|
| **Size** | Fixed size. Must specify size at creation (e.g., `int arr[50]`). | Dynamic size. Automatically grows or shrinks on the fly. |
| **Data Homogeneity** | Homogeneous. Can only store elements of the same data type. | Heterogeneous. Can store elements of different data types. |
| **Memory Allocation** | Contiguous. Values are stored back-to-back in memory. | Referential. Stores references (pointers) to objects in a contiguous block. |
| **Performance (Speed)** | Very fast. Direct offset calculation to access elements in memory. | Slower due to pointer dereferencing and dynamic resizing. |
| **Memory Footprint** | Low. Only stores raw values. | High. Stores 64-bit pointers and object wrappers in heap memory. |

---

## Storage Model: The Referential Array

### Memory Layout Comparison

A standard low-level array stores its raw values in contiguous blocks of memory. In contrast, a Python list is implemented as a **referential array**. The list itself only contains a contiguous sequence of memory addresses (pointers). These pointers point to the locations in heap memory where the actual data objects are stored.

```
       STATIC CONTIGUOUS ARRAY (e.g., C/Java)
       Address:   [1000]   [1004]   [1008]   [1012]
       Value:     |  10  |  20  |  30  |  40  |
       
       ----------------------------------------------------
       
       REFERENTIAL PYTHON LIST (Under the hood)
       List Array (Contiguous Pointers):
       Index:        0        1        2        3
       Address:   [2000]   [2008]   [2016]   [2024]
       Pointer:   | 0x5a | | 0x8b | | 0x3f | | 0x9c |
                     |        |        |        |
                     v        v        v        v
       Heap Objects (Scattered):
       Memory Address: [0x5a]      [0x8b]       [0x3f]       [0x9c]
       Object Value:   |  10  |    | "ML" |     | 3.14 |     | [1,2] |
```

Because pointers are of a fixed width (typically 8 bytes on a 64-bit system), the contiguous pointer array is homogeneous, regardless of the data type of the target objects. This referential architecture is what allows Python lists to be heterogeneous.

---

### Verifying Addresses with id()

We can prove this referential design using Python's built-in `id()` function, which returns the memory address of an object.

**Code example:**
```python
l = [10, "ML", 3.14]

print("List Object Memory Address:", id(l))
print("Address stored at index 0:", id(l[0]))
print("Address stored at index 1:", id(l[1]))

# Compare with independent objects
print("Independent integer 10 Address:", id(10))
print("Independent string 'ML' Address:", id("ML"))

# Output comparison shows that l[0] references the same memory address as the object 10
assert id(l[0]) == id(10)
```

---

## Creating Lists

There are several ways to initialize lists in Python:

**Code example:**
```python
# 1. Empty List
empty1 = []
empty2 = list()

# 2. Homogeneous List
ints = [1, 2, 3, 4]

# 3. Heterogeneous List
mixed = [1, "AI", 3.5, True]

# 4. Multi-dimensional (Nested) List
matrix = [[1, 2], [3, 4]]

# 5. Type Casting an Iterable (e.g., String to List of characters)
chars = list("GPT")
print(chars)  # Output: ['G', 'P', 'T']
```

---

## Accessing Items (Indexing & Slicing)

### Positive & Negative Indexing

*   **Positive Indexing:** Accesses elements from left-to-right, starting at `0` for the first element.
*   **Negative Indexing:** Accesses elements from right-to-left, starting at `-1` for the last element.

**Code example:**
```python
l = [10, 20, 30, 40, 50]

print(l[0])    # 10 (First element)
print(l[-1])   # 50 (Last element)
print(l[-3])   # 30

# Out of range index raises IndexError
try:
    print(l[10])
except IndexError as e:
    print("Caught:", e)  # Output: list index out of range
```

---

### Nested Indexing in Multi-Dimensional Lists

To access elements inside a nested list, chain multiple index brackets `[]` together. Each bracket resolves a level of nesting from the outside in.

**Code example:**
```python
# 2D Nested List
list_2d = [1, 2, 3, [4, 5]]
# Retrieve 4 from the nested list
# Index 3 is [4, 5], index 0 of that nested list is 4
print(list_2d[3][0])  # Output: 4

# 3D Nested List
list_3d = [[[1, 2], [3, 4]], [[5, 6], [7, 8]]]
# Retrieve 3
print(list_3d[0][1][0])  # Output: 3
```

---

### List Slicing

Slicing extracts a new list containing a subset of the original list's elements.
Syntax: `l[start:stop:step]` (the `stop` index is exclusive).

**Code example:**
```python
l = [10, 20, 30, 40, 50, 60]

print(l[0:3])    # Output: [10, 20, 30] (Indices 0, 1, 2)
print(l[:3])     # Output: [10, 20, 30] (Defaults to start index 0)
print(l[3:])     # Output: [40, 50, 60] (Defaults to end index)
print(l[::2])    # Output: [10, 30, 50] (Every second element)

# Reversing a list using negative step parameter
print(l[::-1])   # Output: [60, 50, 40, 30, 20, 10]
```

---

## Adding Items to a List

### append() vs. extend() vs. insert()

Python provides three distinct methods to add elements to a list:

1.  **`append(item)`:** Adds a single element to the end of the list.
2.  **`extend(iterable)`:** Appends all elements from an iterable (e.g., list, tuple, string) to the end of the list individually.
3.  **`insert(index, item)`:** Inserts an element at a specified index, shifting all subsequent elements to the right.

```
                  METHODS TO ADD ITEMS
   
   Original List:  [ 10,  20,  30 ]
   
   1. append([40, 50]):
      Adds the argument as a single element at the end.
      Result:      [ 10,  20,  30,  [40, 50] ]
      
   2. extend([40, 50]):
      Iterates over the argument and appends each element.
      Result:      [ 10,  20,  30,  40,  50 ]
      
   3. insert(1, 99):
      Inserts 99 at index 1, shifting subsequent elements.
      Result:      [ 10,  99,  20,  30 ]
```

**Code example:**
```python
# 1. append()
l1 = [1, 2, 3]
l1.append(4)
print("append:", l1)  # Output: [1, 2, 3, 4]

# Passing a list to append() adds it as a single nested element
l1.append([5, 6])
print("append list:", l1) # Output: [1, 2, 3, 4, [5, 6]]

# 2. extend()
l2 = [1, 2, 3]
l2.extend([4, 5])
print("extend:", l2)  # Output: [1, 2, 3, 4, 5]

# String input to extend() will iterate over and add individual characters
l2.extend("AI")
print("extend string:", l2) # Output: [1, 2, 3, 4, 5, 'A', 'I']

# 3. insert()
l3 = [1, 2, 3]
l3.insert(1, 100)
print("insert:", l3)  # Output: [1, 100, 2, 3]
```

---

## Editing Items (Mutability)

Unlike strings, lists are mutable. You can modify list values in-place by target indexing or slicing.

**Code example:**
```python
l = [10, 20, 30, 40, 50]

# Edit a single element
l[-1] = 500
print("Single Edit:", l)  # Output: [10, 20, 30, 40, 500]

# Edit a slice range in-place
l[1:4] = [200, 300, 400]
print("Slice Edit:", l)   # Output: [10, 200, 300, 400, 500]
```

---

## Deleting Items

### del vs. remove() vs. pop() vs. clear()

Python provides four different ways to remove elements from a list:

1.  **`del` Statement:** Deletes an element or a slice range based on its index position. It can also delete the entire list variable.
2.  **`remove(value)`:** Searches for and deletes the *first occurrence* of the specified value. Raises a `ValueError` if the value is not found.
3.  **`pop(index)`:** Removes and returns the element at the specified index. If no index is provided, it defaults to `-1` (removing and returning the last element).
4.  **`clear()`:** Clears the list, removing all elements and leaving an empty list `[]`.

```
                  METHODS TO DELETE ITEMS
   
   Original List:  [ 10,  20,  30,  20,  40 ]
   
   1. del l[0]:
      Deletes element at index 0.
      Result:      [ 20,  30,  20,  40 ]
      
   2. remove(20):
      Deletes first occurrence of value 20.
      Result:      [ 10,  30,  20,  40 ]
      
   3. pop():
      Removes and returns last element (40).
      Result:      [ 10,  20,  30,  20 ]
      
   4. clear():
      Removes all elements.
      Result:      [ ]
```

**Code example:**
```python
l = [10, 20, 30, 40, 50]

# 1. del (Index-based deletion)
del l[0]
print("del index:", l)  # Output: [20, 30, 40, 50]

# del with slice range
del l[1:3]
print("del slice:", l)  # Output: [20, 50]

# 2. remove() (Value-based deletion)
l_val = [10, 20, 30, 20, 40]
l_val.remove(20)        # Removes first 20
print("remove value:", l_val) # Output: [10, 30, 20, 40]

# 3. pop() (Index-based deletion with return value)
l_pop = [10, 20, 30]
popped_val = l_pop.pop(1)
print("popped value:", popped_val) # Output: 20
print("pop list:", l_pop)          # Output: [10, 30]

# 4. clear() (Empty the list)
l_clear = [10, 20, 30]
l_clear.clear()
print("clear:", l_clear)           # Output: []
```

---

## Traversing Lists (Loops)

### Item-wise vs. Index-wise Traversals

There are two primary ways to iterate through a list:

1.  **Item-wise Traversal:** Iterates directly over the elements. This is the most readable and Pythonic approach.
2.  **Index-wise Traversal:** Iterates over the index positions of the list. Use this approach if you need to modify list elements in-place or access the index values during iteration.

**Code example:**
```python
models = ["GPT-4", "Llama-3", "Claude-3"]

# 1. Item-wise traversal
print("Item-wise:")
for model in models:
    print(model, end=" ")
print("\n")

# 2. Index-wise traversal (using range(len(l)))
print("Index-wise:")
for i in range(len(models)):
    print(f"Index {i}: {models[i]}")
```

---

## Built-in Functions & Methods

### Common Functions (Work on other iterables too)
*   `len(l)`: Returns the number of elements in the list.
*   `min(l)`: Returns the minimum element.
*   `max(l)`: Returns the maximum element.
*   `sorted(l)`: Returns a **new** sorted copy of the list, leaving the original list unchanged.

### List-Specific Methods
*   `count(value)`: Returns the number of occurrences of the specified value.
*   `index(value)`: Returns the index of the first occurrence of the specified value. Raises a `ValueError` if not found.
*   `reverse()`: Reverses the list **in-place** (returns `None`).
*   `sort()`: Sorts the list **in-place** (returns `None`).

**Code example:**
```python
l = [30, 10, 50, 20, 40]

# sorted() vs. sort()
new_sorted = sorted(l)
print("sorted() output:", new_sorted) # Output: [10, 20, 30, 40, 50]
print("Original unchanged:", l)       # Output: [30, 10, 50, 20, 40]

l.sort()                              # Sorts in-place
print("sort() in-place output:", l)   # Output: [10, 20, 30, 40, 50]
```

---

## List Comprehension

List comprehension provides a concise way to create lists. It replaces multi-line `for` loops and conditional blocks with a single line of code.

Syntax:
`[expression for item in iterable if condition]`

**Conversion example:**
```python
# Traditional Loop:
squares = []
for i in range(1, 6):
    squares.append(i**2)

# Equivalent List Comprehension:
squares_comp = [i**2 for i in range(1, 6)]
print(squares_comp)  # Output: [1, 4, 9, 16, 25]
```

**Filtering with condition:**
```python
# Extract numbers divisible by 5
divisible_by_5 = [i for i in range(1, 31) if i % 5 == 0]
print(divisible_by_5)  # Output: [5, 10, 15, 20, 25, 30]

# String prefix filtering
langs = ["Python", "JavaScript", "Prolog", "C++"]
p_langs = [lang for lang in langs if lang.startswith("P")]
print(p_langs)  # Output: ['Python', 'Prolog']
```

---

### Cartesian Products & Matrix Generation

List comprehensions can be nested to generate complex structures like Cartesian products or multi-dimensional matrices.

**Cartesian Product:**
```python
l1 = [1, 2, 3]
l2 = [10, 20]

# Computes product of elements
cartesian = [i * j for i in l1 for j in l2]
print(cartesian)  # Output: [10, 20, 20, 40, 30, 60]
```

**2D Matrix Generation:**
```python
# Generates a 3x3 identity matrix
matrix_3d = [[1 if row == col else 0 for col in range(3)] for row in range(3)]
print(matrix_3d)
# Output: [[1, 0, 0], [0, 1, 0], [0, 0, 1]]
```

---

## The zip() Function

The `zip()` function takes multiple iterables and aggregates their elements into tuples based on their position. It stops when the shortest input iterable is exhausted.

**Code example:**
```python
names = ["Alice", "Bob", "Charlie"]
roles = ["Admin", "User"]

# zip pairs elements. It stops at "User", omitting "Charlie"
zipped = list(zip(names, roles))
print(zipped)  # Output: [('Alice', 'Admin'), ('Bob', 'User')]

# Element-wise addition using zip in list comprehension
v1 = [1, 2, 3]
v2 = [10, 20, 30]
sum_vec = [i + j for i, j in zip(v1, v2)]
print(sum_vec)  # Output: [11, 22, 33]
```

---

## Storing Arbitrary Objects in Lists

Because Python lists store references rather than raw values, you can store any Python object inside a list—including built-in functions, custom classes, modules, or generator objects.

**Code example:**
```python
# Storing built-in functions directly inside a list
methods_list = [print, input, len, type]

# Access and call print function from index 0
methods_list[0]("Hello from inside the list!")
```

---

## Disadvantages & Mutation Risks

### The Risk of Reference Assignment

A common mistake in Python is assuming that assigning a list variable to another variable creates a new, independent copy of the list. In reality, it only copies the memory reference. Both variables point to the same list object in memory.

**Code example demonstrating mutation risk:**
```python
a = [1, 2, 3]
b = a  # Copies reference, not the list

a.append(4)
print("a:", a)  # Output: [1, 2, 3, 4]
print("b:", b)  # Output: [1, 2, 3, 4] (Unexpected change in b!)
assert id(a) == id(b)
```

---

### Creating True Copies with copy()

To create an independent copy of a list, use the `.copy()` method (which performs a shallow copy).

**Code example:**
```python
a = [1, 2, 3]
b = a.copy()  # Creates a new list object in memory

a.append(4)
print("a:", a)  # Output: [1, 2, 3, 4]
print("b:", b)  # Output: [1, 2, 3] (b remains unaffected)
assert id(a) != id(b)
```

---

## List Algorithms & Exercises

### Program 1: Find Duplicates in a List

**Problem Statement:** Take a list of elements and extract all duplicate values.

**Code implementation:**
```python
l = [1, 2, 3, 2, 4, 5, 1, 6]
duplicates = []
seen = []

for item in l:
    if item in seen:
        if item not in duplicates:
            duplicates.append(item)
    else:
        seen.append(item)

print("Duplicates:", duplicates)  # Output: [2, 1]
```

---

### Program 2: Merge Two Sorted Lists into a Single Sorted List

**Problem Statement:** Combine two pre-sorted lists into a single sorted list in $O(N + M)$ time complexity, without using the `.sort()` method.

**Code implementation:**
```python
l1 = [1, 3, 5, 7]
l2 = [2, 4, 6, 8, 10]
merged = []

i, j = 0, 0

# Traverse both lists
while i < len(l1) and j < len(l2):
    if l1[i] < l2[j]:
        merged.append(l1[i])
        i += 1
    else:
        merged.append(l2[j])
        j += 1

# Append remaining elements
while i < len(l1):
    merged.append(l1[i])
    i += 1

while j < len(l2):
    merged.append(l2[j])
    j += 1

print("Merged Sorted List:", merged)
# Output: [1, 2, 3, 4, 5, 6, 7, 8, 10]
```

---

## Added Context (For AI Engineers)

### 1. Vector Operations vs. List Comprehension
In machine learning pipelines, you often need to perform element-wise operations on vectors (e.g., adding bias terms, scaling features). While you can perform these operations using list comprehensions, doing so is slow for large datasets. High-performance ML libraries (like NumPy and PyTorch) use contiguous C-style arrays under the hood to perform vectorized operations.
```python
# Element-wise operations: Python List vs. NumPy
import numpy as np

# Python list comprehension (slow referential iteration)
py_list = [1.0, 2.0, 3.0]
scaled_py = [x * 2.0 for x in py_list]

# NumPy vectorization (fast contiguous SIMD execution)
np_arr = np.array([1.0, 2.0, 3.0])
scaled_np = np_arr * 2.0
```

### 2. Dataset Splitting
When preparing data to train machine learning models, slicing operations are used to split dataset lists into training, validation, and test subsets.
```python
# Simulating a dataset of 10 samples
dataset = [f"sample_{i}" for i in range(10)]

# Split dataset: 80% train, 20% validation
train_split = int(len(dataset) * 0.8)
train_data = dataset[:train_split]
val_data = dataset[train_split:]

print("Train Split:", train_data)  # First 8 samples
print("Val Split:", val_data)      # Remaining 2 samples
```

### 3. Shallow vs. Deep Copy in Neural Network Weights
Because lists store references, copy operations on nested lists (like neural network weight arrays) must be handled with care. A shallow copy (using `l.copy()` or `list(l)`) only copies the outer reference array. If the list contains nested list elements, the inner references are shared. Modifying an inner list inside the copy will affect the original. For nested structures, use `copy.deepcopy()`.
```python
import copy

weights = [[0.1, 0.2], [0.3, 0.4]]

# Shallow copy: nested references are still shared
shallow_weights = weights.copy()
shallow_weights[0][0] = 0.99
print("Original weights (affected by shallow modification):", weights) 
# Output: [[0.99, 0.2], [0.3, 0.4]]

# Deep copy: creates independent copies of nested structures
weights = [[0.1, 0.2], [0.3, 0.4]]
deep_weights = copy.deepcopy(weights)
deep_weights[0][0] = 0.99
print("Original weights (unaffected by deep modification):", weights)
# Output: [[0.1, 0.2], [0.3, 0.4]]
```

---

## Quick Recap

| Concept | Key Takeaway |
|---|---|
| Referential Array | Python lists store pointers/references (64-bit addresses) to heap objects, rather than the raw values themselves. |
| Heterogeneity | Enabled by the referential array model, allowing a single list to store elements of different data types. |
| `append()` vs. `extend()` | `append()` adds its argument as a single element; `extend()` iterates over its argument and adds each element individually. |
| Mutability | Elements inside a list can be modified in-place. |
| `pop()` vs. `remove()` | `pop()` removes an element by index and returns it; `remove()` removes an element by value and does not return it. |
| List Comprehension | An optimized, single-line syntax for creating lists from iterables. |
| Shallow Copy | A direct copy (`b = a`) only copies the reference. Use `b = a.copy()` to create an independent shallow copy. |

---

## Practice Check

1.  **Given the nested list `l = [10, 20, [30, 40], [50, [60, 70]]]`, write the index paths to extract:**
    - `40`
    - `60`
    - `70`

2.  **Explain the output of this code snippet:**
    ```python
    x = [1, 2, 3]
    y = x
    x[0] = 99
    print(y)
    ```

3.  **Predict the output of the following list operations:**
    ```python
    l = [1, 2, 3]
    l.extend([4, 5])
    l.append([6, 7])
    print(len(l))
    ```

4.  **Use a list comprehension to extract all words containing the letter "e" from the list `words = ["GPT", "Llama", "BERT", "Claude", "Gemini"]` (case-insensitive).**

---
<!-- Long note complete. Companion: [Quick Recall](quick-recall.md#04-python-lists) -->
