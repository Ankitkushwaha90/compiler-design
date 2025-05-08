## 📘 1. Symbol Tables

### 🔹 Purpose
A Symbol Table stores information about the names (identifiers) used in the source program, including:

- Variables
- Functions
- Objects
- Types

### 🔹 Data Structures for Symbol Tables

| **Structure**           | **Features**                                   |
|-------------------------|-----------------------------------------------|
| **Linear List**          | Simple but slow lookup (O(n))                 |
| **Hash Table**           | Fast access (average O(1)), handles collisions |
| **Binary Search Tree (BST)** | Sorted entries, average O(log n) lookup      |
| **Trie**                 | Efficient for prefix-based storage (e.g., names)|
| **Stack-based tables**   | Useful for nested scopes                      |

### 🔹 Scope Management
- **Global Scope**: Declared outside any block.
- **Local Scope**: Declared inside functions/blocks.
- **Block Structured Languages**: Support nested scopes.

**Representing Scope Information**:
- Use a stack of symbol tables:
  - On entering a block, push a new table.
  - On exiting, pop the table.
  - Lookup starts from top of the stack downward.

---

## ⚙️ 2. Run-Time Administration

### 🔹 Memory Allocation at Run Time
There are two main memory regions:
- **Stack**: For function calls, local variables (LIFO structure)
- **Heap**: For dynamic memory allocation

### 🔹 Simple Stack Allocation Scheme
Used for procedural languages where:
- Activation records are pushed on function calls.
- Popped on return.

**Activation Record Includes**:
- Return address
- Parameters
- Local variables
- Temporary storage
- Control link (caller’s base address)
- Access link (for static scoping)

### 🔹 Storage Allocation in Block Structured Languages
Block-structured languages like Pascal or C allow nested function definitions.

| **Type**    | **Use**               | **Example**        |
|-------------|-----------------------|--------------------|
| **Static**  | Fixed size and location| Global vars        |
| **Stack**   | Function calls (LIFO) | Local vars         |
| **Heap**    | Dynamic allocation    | malloc, new        |

---

## 🚨 3. Error Detection & Recovery

### 🔹 Types of Errors by Compiler Phase

| **Phase**  | **Type of Error**      | **Example**                            |
|------------|------------------------|----------------------------------------|
| **Lexical**| Unrecognized characters or tokens | @x = 3; (Invalid symbol '@') |
| **Syntax** | Incorrect structure     | if (x + )                           |
| **Semantic** | Meaning-related errors | x = "abc" + 5                        |

### 🔹 Error Handling Strategies

#### ✅ Panic Mode Recovery
- Skip input symbols until a synchronizing token is found (like `;`, `}`).
- Fast, but may skip useful input.

#### ✅ Phrase-Level Recovery
- Replace or insert a token to continue parsing.
- Example: Insert missing `)` in `if (x + 2)`.

#### ✅ Error Productions
- Augment grammar with common error patterns.
- Helps detect and recover from typical mistakes.

#### ✅ Global Correction
- Tries minimal changes to make input valid.
- Computationally expensive (used rarely in practice).

### 🔹 Lexical Phase Error Handling
- Report and skip illegal characters.
- Use regular expressions to define valid tokens.

### 🔹 Syntactic Phase Error Handling
- Detect grammar rule mismatches.
- Use **FIRST** and **FOLLOW** sets to suggest fixes.

### 🔹 Semantic Phase Error Handling
- **Type mismatches**
- **Undeclared variables**
- **Incompatible function calls**

Handled by:
- Symbol Table lookups
- Type checking rules

---

## ✅ Summary

| **Component**             | **Key Concept**                                         |
|---------------------------|---------------------------------------------------------|
| **Symbol Table**           | Stores info about identifiers and their scopes          |
| **Stack Allocation**       | Activation records for function calls                   |
| **Error Recovery**         | Techniques like panic mode, phrase-level, and error productions |
| **Error Types**            | Lexical, Syntax, Semantic                              |

---

Would you like diagrams (e.g., activation records or symbol table structure) or implementation examples in C/C++ or Python?
