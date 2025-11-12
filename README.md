# LL(1) and SLR(1) Grammar Analyzer

## Project Overview
This project implements a **syntactic analyzer** capable of determining whether a context-free grammar is **LL(1)**, **SLR(1)**, both, or neither. It includes predictive (top-down) and shift-reduce (bottom-up) parsers with full FIRST/FOLLOW computation and table construction.

The main driver (`main.py`) automatically detects the grammar type and allows interactive parsing of input strings according to the project specification.

---

## Authors & Course Information
- **Authors:** Felipe Martínez, Santiago Ochoa  
- **Course:** Lenguajes Formales y Compiladores (ST0270)  
- **Term:** 2025-2

---

## Repository Structure
```
├── main.py              → Main program (grammar detection & interactive loop)
├── ll1_parser.py        → Predictive LL(1) parser
├── slr1_parser.py       → Bottom-up SLR(1) parser
├── first_follow.py      → FIRST & FOLLOW computation
├── grammar.txt          → Grammar file
└── README.md            → Documentation
```

---

## Requirements
- **Python 3.10+**
- Works on Windows PowerShell or any terminal that supports standard input.

---

## How to Run
```bash
python main.py -g grammar.txt
```
Depending on the grammar, the program automatically identifies its type and behaves as follows:
- **Both LL(1) & SLR(1):** prompts `Select a parser (T: for LL(1), B: for SLR(1), Q: quit):`
- **Only LL(1):** runs the LL(1) parser directly.
- **Only SLR(1):** runs the SLR(1) parser directly.
- **Neither:** prints a message and exits.

---

## Grammar File Format
- **Line 1:** number of productions (integer).
- Each following line: `NonTerminal -> production1 production2 ...`
- Nonterminals must be **one uppercase letter** (A–Z).
- Use **`e`** to represent **epsilon**.
- No blank lines are allowed.

### Example:
```
3
S -> AB
A -> aA d
B -> bBc e
```

## Example Executions

### Case 1 – Only SLR(1)
```
> python main.py -g slr_only_expr.txt
Grammar is SLR(1). Enter strings (empty line to finish):
i+i
yes
(i+i)*i
yes
(i+i)*i)
no
```

### Case 2 – Both LL(1) and SLR(1)
```
> python main.py -g both_ll1_slr1.txt
Select a parser (T: for LL(1), B: for SLR(1), Q: quit):
T
d
yes
adbc
yes
a
no
```

### Case 3 – Neither
```
> python main.py -g neither.txt
Grammar is neither LL(1) nor SLR(1).
```

### Case 4 – LL(1) but not SLR(1)
```
> python main.py -g ll1_not_slr1_c1.txt
Grammar is LL(1). Enter strings (empty line to finish):
ab
yes
ba
yes
a
no
b
no
```

---

## Conclusions
- The program correctly distinguishes LL(1), SLR(1), both, or neither according to theoretical definitions.
- ε-productions and FOLLOW overlaps are the main causes of **LL(1)** vs **SLR(1)** divergence.
- SLR(1) parsers tolerate **left recursion**, while LL(1) parsers cannot.

---
