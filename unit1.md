# Compiler Design - Comprehensive Notes

## 1. Introduction to Compiler
A compiler is a program that translates source code written in a high-level programming language into machine code.

## 2. Phases and Passes of a Compiler

### Phases of a Compiler:
- **Lexical Analysis** – Breaks code into tokens.
- **Syntax Analysis** – Builds parse tree from tokens using grammar.
- **Semantic Analysis** – Checks for semantic errors.
- **Intermediate Code Generation** – Converts parse tree into intermediate representation.
- **Code Optimization** – Improves intermediate code for efficiency.
- **Code Generation** – Generates machine code.
- **Code Linking & Loading** – Final executable is produced.

### Passes:
- **One-pass Compiler**: Goes through the source code once.
- **Two-pass Compiler**: First builds symbol table, then generates code.

## 3. Bootstrapping
Bootstrapping is the process of writing a compiler in the source programming language it intends to compile. E.g., writing a C compiler in C.

### Steps:
1. Write a simple version in another language.
2. Use it to compile an improved version of itself.
3. Repeat until the compiler is self-hosted.

## 4. Finite State Machines (FSMs) and Regular Expressions

### FSM:
A mathematical model with states and transitions.  
Used in lexical analyzers.

### Regular Expressions:
Patterns to describe tokens.  
E.g., `[a-zA-Z_][a-zA-Z0-9_]* → identifier`

### Applications:
- Token recognition in Lexical Analysis.
- Used by tools like **LEX** to generate lexical analyzers.

## 5. Optimization of DFA-Based Pattern Matchers
**DFA = Deterministic Finite Automaton**.

Optimized by:
- Minimizing the number of states.
- Transition table compression.
- Using direct code instead of table-driven code.

## 6. Lexical Analyzer Implementation

### Tasks:
- Remove whitespace and comments.
- Recognize tokens using DFA.
- Return tokens to the parser.

### Lexical Analyzer Generator: **LEX**
- Converts regular expressions to DFA.
- Generates C code for the lexical analyzer.
- Works with **YACC** for complete compiler front-end.

## 7. Formal Grammars & Syntax Analysis

### Formal Grammar:
Set of rules to generate valid sentences in a language.

### BNF (Backus-Naur Form):
Notation to describe CFGs.

```bnf
<expr> ::= <term> | <expr> + <term>
<term> ::= <factor> | <term> * <factor>
<factor> ::= ( <expr> ) | id
```
## Ambiguity in Grammars
A grammar is **ambiguous** if a sentence has more than one parse tree, causing problems in syntax analysis.

## 8. YACC (Yet Another Compiler Compiler)
A parser generator.  
Works with **LEX**.  
Accepts CFG in BNF form.  
Generates a parser in **C**.

## 9. Context-Free Grammars (CFGs)

### Components:
- **Non-terminals**
- **Terminals**
- **Start symbol**
- **Production rules**

### Example:

```nginx
S → aSb | ε
```
### Derivations:
- **Leftmost Derivation**: Replace the leftmost non-terminal first.
- **Rightmost Derivation**: Replace the rightmost non-terminal first.

### Parse Trees:
- A tree representation of derivations.
- Useful for understanding syntax structure.

### Capabilities of CFGs:
- Can express nesting (e.g., balanced parentheses).
- Can describe programming language syntax.
- Cannot express context-sensitive constraints (like variable declaration before use).
