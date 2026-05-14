# COP 1047C — Lecture 1 Recap
**MDC Live | Summer 2026 | May 12, 2026**

Welcome to Introduction to Python Programming! This recap captures the key points from our first session so you can review on your own and make sure nothing slipped past. The full recording is available in **Canvas → Class for Teams → Recordings** (it usually appears within an hour of class ending; you can speed it up, slow it down, and turn on captions).

---

## 1. Course logistics

- **Lectures** are recorded automatically through Class for Teams. If you ever notice I forgot to record, please say so in chat.
- **Attendance** is captured automatically when you join the Teams session. You're allowed up to 4 absences for the term; 3 consecutive missed classes can trigger an automatic withdrawal. If something comes up, email me before class — excused absences don't extend deadlines, but they keep you on the roster.
- **Communication**: please use Canvas messages or my MDC email (jmasseri@mdc.edu). I aim to respond within 48 hours (longer on weekends). When you hit a bug, send a screenshot — it speeds things up significantly.
- **Office hours**: book a time through the link on the Instructor Information page. I'm also planning to host open drop-in office hours on weekday evenings; details to follow.

## 2. Required materials

- **Textbook**: zyBook — *COP 1047C: Introduction to Python Programming* (Miller, Lysecky, Vahid, Wheatland). Included via the MDC Shark Pack program — don't opt out unless you've arranged an alternative, because the zyBook is where your reading and lab work lives.
- **Python 3.8+** installed on your home machine.
- **Visual Studio Code** (free) — we'll use this for the bigger programming assignment after the midterm. Until then, the zyBook's built-in editor is enough.
- **Webcam + headset** — required for exams (Respondus LockDown Browser) and helpful for office hours.

## 3. Grading at a glance

| Component | Weight |
| --- | --- |
| zyBook reading assignments (participation + challenge activities) | 25% |
| zyBook labs + programming assignment | 30% |
| In-class project | 5% |
| Attendance + background survey | 5% |
| Midterm exam | 15% |
| Final exam | 20% |
| Chapter 11 reading (extra credit) | +5% |

Both exams are taken at home using Respondus LockDown Browser with a webcam. You'll have cheat sheets I provide, so don't waste energy memorizing syntax — focus on understanding.

## 4. Using AI in this course

You are **encouraged** to use AI tools (ChatGPT, Claude, Gemini, GitHub Copilot, and MDC's Circle In AI tutor) as study aids — for explanations, debugging hints, alternative wordings, and tutoring. You **must not** submit code that was generated end-to-end by AI, and you must cite AI assistance when you use it.

The reason for the line isn't ceremony. Programming is a skill, like a musical instrument — you build it by writing code, hitting errors, reading the error messages, and reasoning your way out. If you outsource that loop to a model, the class will feel fine while you're in it and the job market won't. Use AI the way you'd use a tutor sitting next to you: ask it to explain, not to do the work.

## 5. Concepts we covered

### The universal program model: input → process → output
Every program follows this pattern, whether it's a five-line script on your laptop or an AWS Lambda function handling millions of requests. Get comfortable seeing it everywhere.

### Pseudocode and "playing computer"
Before writing code, sketch the steps in plain language. When reading code, trace through it line by line with a pencil and a table of variables. This is exactly the skill the midterm and final test — you'll be shown a short program and asked what it outputs.

### Algorithms
A program is an algorithm — a recipe — expressed in a language a computer understands. The word comes from al-Khwarizmi, a 9th-century Persian mathematician.

### Determinism (and randomness)
Given the same inputs, a deterministic program produces the same outputs every time. When we want non-deterministic behavior (games, simulations), we'll import Python's `random` module — but even those numbers are produced by an algorithm.

### Metric prefixes — you need these cold
| Prefix | Multiplier |
| --- | --- |
| kilo (k) | 10^3 |
| mega (M) | 10^6 |
| giga (G) | 10^9 |
| tera (T) | 10^12 |
| milli (m) | 10^-3 |
| micro (µ) | 10^-6 |
| nano (n) | 10^-9 |

These show up constantly: file sizes, RAM, clock speeds, network latency.

## 6. Python in action

We worked at the interactive interpreter (the `>>>` prompt) and walked through these constructs.

**Variables and assignment**
```python
x = 1
y = 2
z = x + y
print(z)   # 3
```

**Built-in functions we used**
- `print(...)` — keyword arguments `sep` (default `' '`) and `end` (default `'\n'`).
- `input(prompt)` — pauses, then returns whatever the user types **as a string**. If you need a number, convert it.
- `type(obj)` — shows the type.
- `help(obj)` — shows the docstring.

**Types**: `int`, `float`, `str`. Python is **dynamically typed** — you don't declare a variable's type, and reassigning a different type is legal (sometimes too legal). Compare with C++, Java, and Swift, which are statically typed.

**Strings** use either single or double quotes. Common escape characters:

| Sequence | Meaning |
| --- | --- |
| `\n` | newline |
| `\t` | tab |
| `\"` | literal double quote |
| `\'` | literal single quote |
| `\\` | literal backslash |

**Type conversion**
```python
wage_str = input("Enter wage: ")
wage = float(wage_str)   # use int() for whole numbers
```

**Comments** start with `#`. Triple-quoted strings at the top of a function become its **docstring** and are what `help()` displays.

**Identifiers (variable names)**: letters, digits, and underscores; cannot start with a digit. Names like `__init__` and `__name__` are reserved for Python's internals — leave them alone. Reserved words (`if`, `def`, `class`, etc.) can't be used as variable names. Built-in names like `print` *can* be overwritten, but if you reassign `print = 0`, you've just broken `print` for the rest of that session.

### Two kinds of errors
- **Syntax errors** — the code doesn't parse. A real IDE flags these as you type.
- **Runtime errors** — the code parses but blows up when it runs (e.g., `x / d` where `d` happens to be `0`).

Rule of thumb: catch errors as early as you can. A bug caught while typing is free; the same bug shipped to a million customers is expensive.

## 7. A bit of history (worth knowing)

- The first recorded **computer bug** was a literal moth pulled from a relay in the Harvard Mark II in 1947 — Grace Hopper taped it into the logbook. The artifact lives at the Smithsonian.
- In 1940, "computer" was a job title for a human who performed calculations. The film *Hidden Figures* (2016) tells the story of three of them at NASA. Worth watching.
- **Python** was created in the late 1980s by Guido van Rossum. It's open source and community-governed. **Python 3 is not backward-compatible with Python 2** — `print` is the most famous change. We're now on Python 3.14.

## 8. This week — action items

1. **Student Background and Expectation Survey** in Canvas — due 5/20.
2. **zyBook Chapter 1 — Reading** (all participation + challenge activities count) — due 5/27.
3. **zyBook Chapter 1 — Labs**: three short labs, starting with "Hello, World!" You have **unlimited submission attempts** — due 5/27.
4. Install **Python 3** and (optionally) **VS Code** on your home machine.
5. If you've never used Respondus LockDown Browser, install it before the practice midterm so you don't hit surprises on exam day.

**Next time**: why floating-point numbers in Python are a "necessary evil" — and what to do about it.

See you next week. Email me anytime.

— John
