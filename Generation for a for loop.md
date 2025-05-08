# Code Generation Example

## 1. Code Generation for a for Loop

### Example:

```c
for (i = 0; i < 10; i++) {
    sum = sum + i;
}
```
### Intermediate Representation (Three Address Code - TAC):
```text
i = 0                        # init
L1: if i >= 10 goto L2       # condition check
sum = sum + i                # body
i = i + 1                    # increment
goto L1                      # repeat loop
L2:                          # end
```
### Basic Blocks:
```vbnet
B1: i = 0
B2: if i >= 10 goto L2
B3: sum = sum + i
    i = i + 1
    goto L1
B4: L2:
```
### Simple Assembly-style Target Code (Pseudocode):
```asm
MOV i, 0           ; initialize i
L1:
CMP i, 10
JGE L2             ; if i >= 10, jump to L2
ADD sum, i         ; sum = sum + i
ADD i, 1           ; i++
JMP L1             ; loop again
L2:
; loop end
```
## 2. Code Generation for an if-else Statement
Example:
```c
if (a > b) {
    max = a;
} else {
    max = b;
}
```
### Intermediate Representation (Three-Address Code - TAC):
```text
if a <= b goto L1
max = a
goto L2
L1: max = b
L2:
```
### Basic Blocks:
```vbnet
B1: if a <= b goto L1
B2: max = a
    goto L2
B3: L1: max = b
B4: L2:
```
### Simple Assembly-style Target Code (Pseudocode):
```asm
CMP a, b
JLE L1            ; if a <= b, jump to L1
MOV max, a
JMP L2
L1:
MOV max, b
L2:
; end
```
### ✅ Summary of Constructs
High-Level Code	Intermediate Code (TAC)	Assembly Pseudocode
for Loop	Labels, condition, body, jump	CMP, JGE, ADD, JMP
if-else Statement	Conditional branch and jumps	CMP, JLE/JGE, MOV, JMP
