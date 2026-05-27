# COP 1047C – Lecture 3 Summary
## Chapter 3: Types
**Date:** May 26, 2026 | **Instructor:** John Masseria

---

## 📋 Administrative Reminders
- **Chapter 2** readings and labs were due tonight. Complete them in zyBooks — grades sync automatically.
- **Chapter 3** readings and labs are due **June 2, 2026**.
- **Midterm Exam:** Take-home, available after **June 16**; due before class on **June 23**. 50 multiple-choice/true-false questions covering Chapters 1–5. Requires lockdown browser + webcam.
- **Tutor available** at West Campus — use this resource if you're falling behind.
- **Circle In** (in Canvas): Use the AI tutor for questions, and complete the **Course Feedback** (exit ticket) after each class.

---

## 🔁 Quick Review: What We Covered Previously
- **Variables** are identifiers that point to objects in memory.
- Identifiers are alphanumeric and case-sensitive; the first character must be a letter or underscore.
- **int** objects hold whole numbers; fractional values are truncated.
- **float** objects hold decimal/floating-point numbers.
- Use `type()` to inspect the type of any variable.

---

## 📘 Chapter 3: Types — Tonight's Content

### 1. Strings
A **string** is a sequence of characters enclosed in single or double quotes.

```python
name = "TRISH"
```

**Key characteristics:**
- **Zero-based indexing:** The first character is at index `0`.
  ```python
  print(name[0])   # → T
  print(name[4])   # → H
  ```
- **Negative indexing:** Count backward from the end.
  ```python
  print(name[-1])  # → H (last character)
  ```
- **Index out of range:** Accessing an index that doesn't exist raises an `IndexError`. Python catches this explicitly — a safety advantage over older languages like C.
- **Strings are immutable:** Once created, a string cannot be modified. You must create a new string to make changes.

**String Concatenation** (the `+` operator is *overloaded* for strings):
```python
first = "New"
last  = "York"
city  = first + " " + last   # → "New York"
```
- You **cannot** concatenate a string directly with an integer — convert first:
  ```python
  room = "Room " + str(5)    # → "Room 5"
  ```

**F-Strings** (formatted string literals):
```python
number = 6
amount = 32
print(f"{number} burritos cost ${amount}")  # → 6 burritos cost $32
```

**F-String Formatting Codes:**

| Format | Meaning | Example |
|--------|---------|---------|
| `:.2f` | Float, 2 decimal places | `f"{3.14159:.2f}"` → `3.14` |
| `:d` | Integer (decimal) | `f"{4:d}"` → `4` |
| `:3d` | Integer, 3 spaces wide | `f"{4:3d}"` → `  4` |
| `:03d` | Integer with leading zeros | `f"{4:03d}"` → `004` |
| `:,d` | Integer with comma separators | `f"{7600:,d}"` → `7,600` |
| `:,.2f` | Float with commas + 2 decimals | `f"{1234567.89:,.2f}"` → `1,234,567.89` |
| `:b` | Binary representation | `f"{13:b}"` → `1101` |
| `:08b` | Binary, 8 digits, leading zeros | `f"{13:08b}"` → `00001101` |
| `:x` | Hexadecimal (lowercase) | `f"{122:x}"` → `7a` |
| `:X` | Hexadecimal (uppercase) | `f"{122:X}"` → `7A` |

---

### 2. Lists
A **list** is a mutable, ordered sequence that can hold items of any type.

```python
students = ["Alice", "Bob", "Carlos", "Diana", "Evan"]
print(students[0])   # → Alice
print(students[-1])  # → Evan
```

**Common list operations:**
```python
students.append("Fatima")      # Add to the end
students.remove("Bob")         # Remove by value
print(len(students))           # Number of items
```

**Lists vs. Strings:**
- Both are indexed sequences.
- Strings are **immutable**; lists are **mutable** (you can change them).
- Use a list when your collection will grow, shrink, or change.

---

### 3. Tuples
A **tuple** is an immutable, ordered sequence defined with parentheses.

```python
white_house = ("1600 Pennsylvania Ave", "Washington", "DC")
print(white_house[0])   # → 1600 Pennsylvania Ave
```

- Tuples **cannot be modified** after creation — useful for fixed/constant data.
- Python can optimize tuples internally because it knows they won't change.
- Printed with `()` vs. lists which print with `[]`.

**Named Tuples** (from the `collections` module):
```python
from collections import namedtuple

Car = namedtuple("Car", ["make", "model", "price", "seats"])
blazer = Car("Chevrolet", "Blazer", 32000, 8)

print(blazer.make)    # → Chevrolet
print(blazer.price)   # → 32000
```
Named tuples let you access fields by name instead of index — cleaner and more readable.

**When to use which:**
| Structure | Mutable? | Use When… |
|-----------|----------|-----------|
| List | ✅ Yes | Data will grow, shrink, or change |
| Tuple | ❌ No | Data is fixed (like constants) |

---

### 4. Dictionaries
A **dictionary** stores **key-value pairs**, similar to a real-world lookup table.

```python
scores = {}                          # Empty dictionary
scores["Lionel Messi"] = 91
scores["Cristiano Ronaldo"] = 90

print(scores["Lionel Messi"])        # → 91
print(len(scores))                   # → 2
```

- Defined with **curly braces** `{}` containing `key: value` pairs.
- Keys are typically strings; values can be any type.
- Real-world parallel: **Redis** is a production key-value store used to cache web data rather than repeatedly querying a database.

---

### 5. Sets
A **set** is an unordered collection of **unique** values — no duplicates allowed.

```python
# Creating a set from a list (auto-deduplicates)
names = ["Alice", "Bob", "Alice", "Carlos", "Bob"]
unique = set(names)
print(unique)   # → {'Alice', 'Bob', 'Carlos'}
```

> ⚠️ **Important gotcha:** `{}` creates an empty **dictionary**, NOT an empty set.  
> To create an empty set: `my_set = set()`

**Set operations:**
```python
A = {1, 2, 3, "gorgon"}
B = {3, "gorgon", 4, 5}

C = A.union(B)           # All unique items from both sets (returns new set)
D = A.intersection(B)    # Only items in both sets (returns new set)
E = A.difference(B)      # Items in A but not in B
```

**Methods:** `add()`, `remove()`, `pop()` (removes a random item), `clear()`

---

### 6. Type Conversion (Casting)
Python performs **implicit** conversion in some cases, but often you must convert explicitly.

```python
x = int("42")          # String → Integer
y = float("3.14")      # String → Float
z = str(100)           # Integer → String
```

**Gotchas:**
- `int("3.14")` will **fail** — can't convert a decimal string directly to `int`. Convert to float first: `int(float("3.14"))`
- Strings with commas (`"1,000"`) cannot be converted directly — you must strip the comma first.
- The `input()` function **always returns a string** — always cast before doing math!

```python
age = int(input("Enter your age: "))   # Must cast!
```

---

### 7. Binary and Hexadecimal Numbers
- Computers store everything in **binary** (0s and 1s) because circuits have two states: on/off, charged/uncharged.
- **Hexadecimal** (base 16, using 0–9 and A–F) is a compact way to represent binary data — each hex digit = 4 binary bits.

**Binary → Decimal:**  
`1101` = 1×8 + 1×4 + 0×2 + 1×1 = **13**

**Decimal → Binary:**  
Repeatedly divide by 2 and collect remainders (read from bottom to top):  
17 ÷ 2 = 8 R1, 8 ÷ 2 = 4 R0, 4 ÷ 2 = 2 R0, 2 ÷ 2 = 1 R0, 1 ÷ 2 = 0 R1 → **10001**

Use F-strings to do conversions instantly in Python:
```python
n = 13
print(f"{n:b}")    # → 1101   (binary)
print(f"{n:08b}")  # → 00001101 (8-bit binary with leading zeros)
print(f"{n:x}")    # → d     (hexadecimal lowercase)
```

---

## 🛠️ Hands-On Activities (Practice on Your Own)

### Activity 1 – Strings
1. Create a string variable with your full name.
2. Print your first initial using **negative indexing**.
3. Write a program that asks for a first and last name, then prints: `Hello, [Name]! Your name has [N] characters.`
4. Using an F-string, print a receipt with: item name, quantity, price per unit, and total cost (formatted with 2 decimal places).
5. **Challenge:** Ask for a decimal number and print it in binary and hexadecimal.

### Activity 2 – Lists
1. Create a list of 5 student names.
2. Print the first and last name in the list.
3. Add a new student name with `append()`.
4. Remove one student name with `remove()`.

### Activity 3 – List Math
Create a list of exam scores, then compute and print:
- The **average** score
- The **highest** score (`max()`)
- The **lowest** score (`min()`)

### Activity 4 – Named Tuple
Create a named tuple called `SHIP` with the following fields:
- `name`, `capacity`, `home_port`, `year_built`

Create at least two instances and print their details.

---

## 📅 Coming Up
| Date | Topic |
|------|-------|
| June 2 | Chapter 3 readings & labs due |
| June 9 | Chapter 4 – Branching |
| June 16 | Chapter 5 – Loops |
| After June 16 | Midterm available (Chapters 1–5) |
| June 23 | Midterm due (before class) |

---

*Questions? Use the Class Question Board on Canvas, email Prof. Masseria at jmasseri@mdc.edu, or use the Circle In AI tutor.*
