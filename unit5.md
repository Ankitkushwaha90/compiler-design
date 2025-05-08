## 📘 1. Code Generation

### 🔹 1.1 Design Issues in Code Generation
The goal is to translate intermediate code (like TAC) into target machine code while optimizing for:

| **Design Aspect** | **Description**                               |
|-------------------|-----------------------------------------------|
| **Correctness**   | Code should preserve semantics of source      |
| **Efficiency**    | Generate fast and compact machine code        |
| **Simplicity**    | Easy to implement and debug                   |
| **Speed**         | Faster compilation process                    |
| **Target machine**| Affects instruction format, addressing modes, register use, etc. |

### 🔹 1.2 The Target Language
Could be:
- **Assembly language**
- **Machine language**
- **Bytecode** (e.g., JVM, .NET)
- **Abstract stack-based machine code**

Target code should consider:
- **Instruction selection**
- **Register allocation**
- **Addressing modes**

### 🔹 1.3 Addresses in the Target Code
Variables and temporaries must be mapped to:
- **Registers** (preferred)
- **Memory** (stack/heap)

**Types**:
- **Absolute Address**: Fixed memory location
- **Relative Address**: Based on base pointer or offset (e.g., BP + 8)

### 🔹 1.4 Basic Blocks and Flow Graphs

#### 🔸 Basic Block:
A sequence of statements with no jumps in or out, except at the beginning or end. It starts with a leader instruction.

#### 🔸 Flow Graph (Control Flow Graph - CFG):
- **Nodes**: Basic blocks
- **Edges**: Possible control transfers

Useful for optimization and flow analysis.

### 🔹 1.5 Optimization of Basic Blocks
Key techniques:

| **Optimization**                    | **Description**                                      |
|-------------------------------------|------------------------------------------------------|
| **Common Subexpression Elimination** | Reuse previously computed expressions                |
| **Dead Code Elimination**           | Remove unreachable or unused code                   |
| **Constant Folding**                | Evaluate expressions at compile time                 |
| **Strength Reduction**              | Replace expensive ops with cheaper ones (e.g., x * 2 → x << 1) |

### 🔹 1.6 Code Generator Responsibilities
- **Instruction selection**
- **Register allocation**
- **Instruction scheduling**
- **Handle function calls** (prologue/epilogue)
- **Emit code with appropriate addressing modes**

---

## 🧠 2. Code Optimization

### 🔹 2.1 Machine-Independent Optimizations
Performed on intermediate representation (IR), not tied to specific hardware.

Examples:
- **Constant propagation**
- **Copy propagation**
- **Loop invariant code motion**
- **Dead code elimination**
- **Strength reduction**

### 🔹 2.2 Loop Optimization
Loops are key targets for optimization:

| **Technique**                       | **Description**                                            |
|-------------------------------------|------------------------------------------------------------|
| **Loop Invariant Code Motion**     | Move computations that don’t change across iterations outside the loop |
| **Induction Variable Elimination**  | Simplify loop variables                                    |
| **Strength Reduction**              | Replace multiplication with addition                       |
| **Loop Unrolling**                 | Duplicate loop body to reduce overhead                     |

### 🔹 2.3 DAG Representation of Basic Blocks
**Directed Acyclic Graph (DAG)**:
Represents computations in a basic block.

Helps identify:
- **Common subexpressions**
- **Dead code**
- **Optimal evaluation order**

**Example DAG for**:

```plaintext
a = b + c;
d = b + c;
e = a + 1;
f = d + 1;
```
## 🔹 2.4 Value Numbers & Algebraic Laws

### Value Numbering:
- Assign a unique number to each unique expression.
- Helps detect equivalent expressions, improving efficiency.

### Algebraic Laws (for optimization):
- **Commutativity**: `a + b = b + a`
- **Associativity**: `(a + b) + c = a + (b + c)`
- **Distributivity**: `a * (b + c) = ab + ac`

Used in common subexpression detection.

---

## 🔹 2.5 Global Data-Flow Analysis
Analyzes how data moves through the entire program (not just one block).

### Key Concepts:
- **Live Variable Analysis**: Variable is live if it holds a value that may be used later.
- **Available Expressions**: Expression already computed and not changed.
- **Reaching Definitions**: Which assignments can reach a point.

Used for:
- **Register allocation**
- **Dead code elimination**
- **Code motion**

---

## ✅ Summary Table

| **Component**         | **Key Purpose**                                                   |
|-----------------------|-------------------------------------------------------------------|
| **Basic Block**        | Atomic code unit for local optimizations                         |
| **Flow Graph**         | Shows control flow between basic blocks                          |
| **DAG**                | Identifies redundant computations in a block                     |
| **Loop Optimization**  | Speeds up frequently executed parts of code                      |
| **Global Analysis**    | Enhances optimization by looking across the entire program       |
| **Code Generator**     | Converts IR to efficient target code                             |

---

Would you like sample code generation for a high-level construct like a **for loop** or **if-else** in a specific language (C/C++, Python)?
