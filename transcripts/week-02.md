# COP 1047C — Lecture 2 Recap
**MDC Live | Summer 2026 | May 19, 2026**

Tonight covered Chapter 2 (Variables and Expressions), delivered a closer look at floating-point arithmetic, and wrapped up with a guided Python and VS Code installation. The recording is in **Canvas → Class for Teams → Recordings** as usual.

---

## 1. Extra resources worth bookmarking

Tyler asked a great opening question — here are three resources mentioned in class.

**OpenStax: Introduction to Python Programming (free)**
Rice University's free, open-source Python textbook. Search for *OpenStax Python* or go to openstax.org. It covers the same chapter sequence as zyBook, in a more traditional textbook format — useful for a second read on any topic you want re-explained differently. [Here's the link to the OpenStax textbook.](https://openstax.org/details/books/introduction-python-programming)

**MDC Circle In (AI tutor)**
Access through Canvas. It's designed to help you think through problems rather than hand you answers — more like a tutor guiding you than a search engine. Good for when you're stuck and want a hint on your approach before you look at a full solution.

**CodeWars (codewars.com)**
A community site of short programming challenges ranked by difficulty. Once we're a few weeks in, working through beginner-level Python challenges there is one of the best ways to build fluency. Programming is a skill; it takes repetition.

---

## 2. Quick course reminders

- Chapter 1 assignments (reading + labs) were due tonight. If you haven't submitted, do so — the gradebook will show a zero tomorrow, but zyBook remains open through the end of the semester.
- Python 3.14 and Visual Studio Code installation links were posted in the chat. See Section 7 below if you still need to set these up.
- Attendance is being tracked through Class for Teams automatically.

---

## 3. Brief recap: interpreted vs. compiled

Python is an **interpreted** language. When you run a Python file, the Python interpreter reads each statement and executes it directly. Files you write end in `.py`; Python sometimes generates a compiled bytecode cache (`.pyc`) to speed up repeated runs, but you'll rarely interact with those directly.

Languages like C++, Java, and Swift are **compiled**: a compiler translates the entire source file into machine instructions ahead of time, which is why those programs tend to run faster. As an illustration: the simple assignment `c = a + b` compiles down to several machine-level operations — load value from one memory address into a register, load another value into a second register, add them, store the result at a third address. Python's interpreter handles all of that for you under the hood.

---

## 4. Variables and identifiers

A **variable** is a named container for a value. In Python you create one simply by assigning to it:

```python
wage = 20
hours = 40
salary = wage * hours * 52
```

The name part is called an **identifier**. Rules:
- Letters, digits, and underscores only — no spaces, no dollar signs.
- Cannot start with a digit (`1a` is invalid; `a1` is fine).
- Python is **case-sensitive**: `salary`, `Salary`, and `SALARY` are three different variables.

The case-sensitivity rule is a common source of silent bugs. If you accidentally write `Wage` when you meant `wage`, Python creates a brand-new variable instead of updating the one you intended. Unlike Java or C++, Python won't warn you — it just silently does something different. Keep your naming consistent, and if a value isn't updating the way you expect during debugging, check for case mismatches.

---

## 5. Types — integers, floats, and strings

Even though Python doesn't require you to declare a type, every value has one.

```python
a = 10        # int   — whole number
b = 3.14      # float — fractional / decimal
c = "hello"   # str   — text
```

Use `type(x)` to inspect what Python thinks a variable is. Because Python is dynamically typed, a variable's type can change when you reassign it — which can be a source of surprises.

**Integers** hold whole numbers (positive, negative, zero). No fractional part.

**Floats** hold decimal values. Use them for any calculation that might produce a fraction. One important caveat — see the next section.

**Strings** hold text. You'll use them constantly; we'll cover string operations in depth in Chapter 7.

---

## 6. Floating-point arithmetic — the essential warning

This is worth paying close attention to because it trips up working developers, not just students.

Open your Python interpreter and try this:

```python
>>> 0.1 + 0.2
0.30000000000000004
```

That is not a Python bug. It is a fundamental property of how computers represent decimal fractions in binary. Some decimal fractions (like 1/3) cannot be expressed exactly in any finite number of bits, just as 1/3 cannot be written as a finite decimal. The result is a tiny rounding error that accumulates.

**Two practical consequences:**

**Never test float equality with `==`:**
```python
>>> 0.1 + 0.2 == 0.3
False      # This will bite you
```

Instead, test whether two floats are *close enough*:
```python
>>> abs((0.1 + 0.2) - 0.3) < 1e-9
True

# More pragmatically, if you need to test if two float variables (a, b)
# are equal you would use:

abs( a - b ) < 1e-9

```

**Format floats before displaying them to users**, especially for money:
```python
check = 123.33
print(f"Total with 20% tip: ${check * 1.20:.2f}")
# Output: Total with 20% tip: $147.99
```

The `f"..."` syntax is called an **f-string**. The `:.2f` inside the curly braces means "format as a float with exactly 2 decimal places." This doesn't change the internal value — it only affects what's printed. Do all your calculations with full precision; only round at the moment of display.

---

## 7. The assignment operator vs. the equality operator

This confuses every beginner at least once:

| Symbol | Meaning | Example |
| --- | --- | --- |
| `=` | Assignment — store a value | `x = 5` |
| `==` | Equality test — is this true? | `x == 5` → `True` |

```python
x = 5       # stores 5 in x
x == 5      # asks "is x equal to 5?" — returns True
x == 6      # returns False
```

We'll use `==` extensively once we get to branching (Chapter 4).

---

## 8. Python's object model (a mental model that pays off later)

In Python, **everything is an object** — integers, floats, strings, functions, all of it. When you write `x = 4`, Python creates a float object holding the value 4 and makes the label `x` point to it. If you then write `y = x`, both `x` and `y` point to the exact same object in memory.

You can verify this with the built-in `id()` function, which returns a unique identifier for each object:

```python
x = 1.0
y = x
id(x) == id(y)   # True — same object
```

Integers and strings in Python are **immutable** — when you "change" an integer variable, you're actually creating a new object and re-pointing the label, not modifying the old one. This distinction matters when we get to lists and dictionaries later in the semester.

---

## 9. Scientific notation

Python uses the letter `E` for scientific notation:

```python
avogadro = 6.02e23      # 6.02 × 10²³
tiny = 1.5e-10          # 1.5 × 10⁻¹⁰
```

This is the same format you'll see on the midterm and final when questions involve very large or very small values. If you type `import sys; sys.float_info` in the interpreter you'll see Python's float limits.

---

## 10. Strings — characters, Unicode, and escape sequences

Every character is stored internally as a number following the **Unicode** standard. You can inspect this with two built-in functions:

```python
ord('A')    # → 65
ord('a')    # → 97
chr(65)     # → 'A'
```

Notice that uppercase letters have lower numbers than lowercase. This matters for sorting — Python's default sort puts `'Z'` before `'a'` because 90 < 97. Keep this in mind when you write comparison programs.

**Escape sequences** (review from Week 1):

| Sequence | Meaning |
| --- | --- |
| `\n` | newline |
| `\t` | tab |
| `\\` | literal backslash |
| `\"` | literal double-quote inside a `"..."` string |
| `\'` | literal single-quote inside a `'...'` string |

Each escape sequence counts as **one character**, not two. So `len("a\\b")` is 3, not 4.

If you want a string where backslashes are treated literally (common for Windows file paths), prefix with `r`:

```python
path = r"C:\Users\student\Documents"   # raw string — no escaping
```

The `len()` function returns the number of characters in a string:

```python
len("hello")    # → 5
```

---

## 11. Random numbers

```python
import random
random.random()         # float between 0.0 and 1.0
random.randint(1, 6)    # integer from 1 to 6 inclusive (a die roll)
random.seed(42)         # fix the seed for reproducible results
```

Computers cannot generate truly random numbers — they use a mathematical algorithm that produces sequences that *look* random. The `seed` sets where in that sequence you start. With a fixed seed you get the same sequence every run, which is useful for testing and debugging.

---

## 12. Python style guidelines (PEP 8)

These are conventions, not syntax rules — Python won't stop you from ignoring them. But following them makes your code readable to other programmers and to your future self.

- **Variable names**: `snake_case` — lowercase words joined by underscores (`monthly_salary`, `total_hours`)
- **Constants**: `ALL_CAPS` — tells readers this value shouldn't change (`MAX_WEIGHT`, `PI`)
- **Class names**: `CamelCase` — capitalize each word, no underscores (we'll use this in Chapter 10)
- **Spaces around operators**: `x = a + b`, not `x=a+b`
- **Indentation**: 4 spaces per level (not tabs)
- **One statement per line** — Python allows semicolons to put two on one line, but don't
- **Line length**: aim for under 100 characters; break long statements across lines if needed
- **Strings**: double quotes for string literals; single quotes for dictionary keys (more on this in Chapter 9)

Good style is a professional habit. Start building it now.

---

## 13. Installing Python and VS Code

For students who still need to install these:

**Python 3:** Go to python.org, download the installer for your OS, and run it. Accept the defaults. On a Mac, open Terminal and type `python3` to confirm it's working. On Windows, open Command Prompt and type `python --version`.

**Visual Studio Code:** Go to code.visualstudio.com and download the installer. After installing, add the Python extension (search for "Python" in the Extensions panel). VS Code will use the Python interpreter you installed above.

You don't need these for zyBook labs — zyBook has a built-in editor. You will need them for the larger programming assignment later in the semester.

---

## 14. This week — action items

1. Complete **zyBook Chapter 2 — Reading** (participation + challenge activities) — due 6/17.
2. Complete **zyBook Chapter 2 — Labs** — due 6/17.
3. Catch up on any **Chapter 1** items if you haven't submitted them yet.
4. Install Python 3 and VS Code if you haven't already (Section 13 above).

**Next time:** Chapter 3 — Types in depth, including type conversion, casting, and more on strings.
