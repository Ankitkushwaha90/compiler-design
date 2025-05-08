# 📘 Parsing Techniques in Compiler Design

## 1. What is Parsing?
Parsing is the process of analyzing a sequence of tokens to determine its grammatical structure according to a given grammar.

**Input**: Stream of tokens from the lexical analyzer.  
**Output**: Parse Tree / Syntax Tree

## 2. Types of Parsers
- **Top-Down Parsers** – Start from the start symbol and try to reach the input string.
- **Bottom-Up Parsers** – Start from the input and try to reach the start symbol.

## 🧭 Basic Parsing Techniques

### A. Shift-Reduce Parsing (Bottom-Up)
Uses a stack to hold grammar symbols.  
Alternates between:
- **Shift**: Push next input symbol onto the stack.
- **Reduce**: Replace stack symbols matching RHS of a production with its LHS.

Handles:
- A handle is a substring matching the RHS of a production and can be reduced.

### B. Operator Precedence Parsing
Handles expressions using precedence relations between operators.

#### Operator Relations:
- **𝑎 < 𝑏**: 𝑎 has lower precedence.
- **𝑎 = 𝑏**: Same precedence, use associativity.
- **𝑎 > 𝑏**: 𝑎 has higher precedence.

#### Limitations:
- Only suitable for operator-based expressions (e.g., arithmetic).
- Cannot handle general grammars or ambiguity.

### C. Top-Down Parsing
Builds parse tree from root to leaves.

#### Types:
- **Recursive Descent Parsing**: Manual implementation using recursive functions. Easy to implement but not efficient for all grammars.
- **Predictive Parsing**: A non-recursive version of recursive descent. Uses lookahead to decide which production to use.

#### FIRST and FOLLOW Sets:
- **FIRST(X)**: Set of terminals that begin strings derived from X.
- **FOLLOW(X)**: Set of terminals that can appear immediately to the right of X.

## 🔧 Automatic Construction of Efficient Parsers

### 1. LR Parsers (Bottom-Up)
**LR = Left-to-right scanning, producing a Rightmost derivation in reverse.**

#### Types:
- **SLR** (Simple LR)
- **LALR** (Look-Ahead LR)
- **Canonical LR**

### 2. Canonical Collection of LR(0) Items
Core step for constructing LR parsing tables.

**LR(0) Item**: A production with a dot (·) showing position in derivation.

Example:

```vbnet
A → α·β  → Dot is before β (we've seen α)
```
## 3. Constructing SLR Parsing Tables
- Use **LR(0)** items.
- Use **FOLLOW** sets to resolve conflicts in reduce actions.
- More straightforward but may not handle all grammars.

## 4. Constructing Canonical LR Parsing Tables
- Uses **LR(1)** items (dot + lookahead symbol).
- More powerful, handles all deterministic context-free grammars.
- Bigger tables and more states.

## 5. Constructing LALR Parsing Tables
- Combines similar **LR(1)** states to reduce size.
- Same power as **Canonical LR** for most practical grammars.
- Efficient and widely used in parser generators like **YACC**.

## 6. Using Ambiguous Grammars
Some grammars (e.g., for expressions) are ambiguous by nature.

#### Approaches:
- Disambiguate using precedence rules.
- Use associativity (left/right) for operators.

## 7. Automatic Parser Generator
**YACC** (Yet Another Compiler Compiler) is a classic tool.

- Takes BNF grammar as input.
- Generates **LALR** parser in C.

## 8. Implementation of LR Parsing Tables
Two main tables:
- **ACTION Table**: Determines shift, reduce, accept, or error.
- **GOTO Table**: Determines state transition after a reduction.

#### Parsing Algorithm (LR):
1. Initialize stack with state 0.
2. Repeat:
   - Use current state and input symbol to look up **ACTION**.
   - **Shift**: Push state & token.
   - **Reduce**: Pop symbols, apply rule, go to **GOTO** table.
   - **Accept**: Input matches grammar.

## ✅ Summary Table

| Technique             | Type       | Uses Lookahead | Handles Ambiguity  | Example Tools           |
|-----------------------|------------|-----------------|---------------------|-------------------------|
| Recursive Descent     | Top-down  | Yes (manual)    | No                  | Manual code             |
| Predictive Parsing    | Top-down  | Yes (LL(1))     | No                  | Manual / Tools          |
| Shift-Reduce          | Bottom-up | No              | Limited             | Manual                  |
| SLR                   | Bottom-up | Yes (FOLLOW)    | Limited             | YACC                    |
| Canonical LR          | Bottom-up | Yes (LR(1))     | Yes                 | yacc -v                 |
| LALR                  | Bottom-up | Yes (merged)    | Mostly              | YACC, Bison             |

---

Let me know if you’d like diagrams (like parsing tables, stack configurations, parse trees, or state machines) for visual understanding.
