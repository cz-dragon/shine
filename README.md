# Shine SSA compiler
Shine is an optimizing compiler with custom target architecture which aims to remain relatively simple wherever possible.
Uses custom intermediate representation (Shine IR) on which the compiler applies optimizations.

### Example architecture
```mermaid
flowchart TD

classDef default stroke-width:2px,stroke:#888888,fill:#CCCCCC
classDef green stroke-width:2px,stroke:#00AA00,fill:#88FF88

A[URCL]:::green
B[C]
C[Rust]

D[Preprocessed C]
E[LLVM IR]

F[Shine IR]:::green

G[URCL Core]:::green
H[RISC-V]

linkStyle default stroke-width:2px,stroke:#404040

A--->|URCL to Shine IR|F
B-->|Expand macros using gcc/clang|D
B-->|Compile to LLVM IR using clang|E
C-->|Compile to LLVM IR using rustc|E
D-->|Relatively simple to support a subset of C|F
E-->|"Very hard<br/>(requires supporting everything LLVM can generate)"|F
F-->|Apply optimizations for known target|G
F-->|Apply optimizations for known target|H

linkStyle 0,6 color:#00AA00
```
