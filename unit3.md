## 📘 Syntax-Directed Translation (SDT)

### 1. What is Syntax-Directed Translation?
It refers to attaching semantic rules or actions to grammar productions to perform translation during parsing.

- Based on **context-free grammar**
- Uses **attributes** and **semantic rules**
- Helps in generating **intermediate code**

### 2. Syntax-Directed Translation Schemes
#### Attributes:
- **Synthesized Attributes**: Computed from child nodes (bottom-up)
- **Inherited Attributes**: Passed down from parent or siblings (top-down)

#### SDT Scheme:
- A **CFG** with actions embedded in productions.
- Actions can be placed at any position (not just at the end of rules).

### 3. Implementation of SD Translators
- Use annotated **parse trees** or **syntax trees**.
- Actions are executed during parsing.
- Can be implemented using:
  - **Top-down parsing** with recursive procedures.
  - **Bottom-up parsing** with syntax-directed definitions (SDDs).

---

## 🧾 Intermediate Code Generation

### 1. Postfix Notation (Reverse Polish)
- Operator follows operands.
  
  Example:
  ```plaintext
  a + b * c → abc*+
  ```

  ## Useful for:
- **Stack-based code generation**
- **Easy evaluation without parentheses**

---

## 2. Parse Trees and Syntax Trees

### Parse Tree:
- Represents all details of derivation.
- Includes all grammar rules.

### Syntax Tree:
- Simplified version of the parse tree.
- Only shows the essential structure of computation.

### Example: For `a + b * c`, the syntax tree:

```plaintext
      +
     / \
    a   *
       / \
      b   c
```

## 3. Three Address Code (TAC)
Intermediate code with at most three operands.

Typically: x = y op z

### Example:

```plaintext
a + b * c → 
t1 = b * c  
t2 = a + t1
```
## 4. Quadruples and Triples
Quadruples:
4 fields: (operator, arg1, arg2, result)

### Example:

```plaintext
(*, b, c, t1)
(+, a, t1, t2)
```
## Triples:
Uses position/index instead of the result variable.

### Example:

```plaintext
(0) (*, b, c)
(1) (+, a, (0))
```
Triples reduce temporary variable usage.

## 🔄 Translation of Programming Constructs
### 1. Assignment Statements
Translate:

```plaintext
x = a + b * c;
```
TAC:

```plaintext
t1 = b * c
t2 = a + t1
x = t2
```
### 2. Boolean Expressions
Use short-circuit evaluation:

```plaintext
if (a < b && c > d)
```
TAC:

```plaintext
if a < b goto L1
goto L2
L1: if c > d goto L3
L2: ...
```
### 3. Flow Control Statements
If-Else:
```plaintext
if (cond) S1 else S2
```
TAC:

```plaintext
if cond goto L1
goto L2
L1: S1
goto L3
L2: S2
L3:
```
While Loop:
```plaintext
while (cond) S
```
TAC:

```plaintext
L1: if cond goto L2
goto L3
L2: S
goto L1
L3:
```
## 4. Postfix Translation
Translate infix to postfix using a stack.

Used in arithmetic expression evaluation. Supports left-to-right evaluation without parentheses.

## 5. Translation with Top-Down Parser
Incorporates semantic actions during parsing.

Uses recursive functions to generate code alongside parsing.

### Example:

```bnf
E → E + T | T
```
SDT:

```bnf
E → E + T { print('+') }
E → T
```
## 🧮 More on Translation
### 1. Array References in Arithmetic Expressions
Example: a[i] = b[i] + c[i]

TAC:

```plaintext
t1 = i * width
t2 = b[t1]
t3 = c[t1]
t4 = t2 + t3
a[t1] = t4
```
### 2. Procedure Calls
```plaintext
call foo(a, b)
```
TAC:

```plaintext
param a
param b
call foo, 2
Return:
```

```plaintext
t1 = call foo, 2
```
### 3. Declarations
Used to assign space or define type:

```plaintext
int x;
```
Intermediate Representation:

```plaintext
declare x, int
```
### 4. Case Statements
```plaintext
switch(x) {
  case 1: S1
  case 2: S2
  default: Sd
}
```
TAC:

```plaintext
t1 = x
if t1 == 1 goto L1
if t1 == 2 goto L2
goto Ld
L1: S1; goto Lend
L2: S2; goto Lend
Ld: Sd
Lend:
```
