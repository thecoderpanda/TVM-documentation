Introduction
Contents
1 Overview 5
1. 1.0 Notation for bitstrings . . . . . . . . . . . . . . . . . . . . . . 5
1. 1.1 TVM is a stack machine . . . . . . . . . . . . . . . . . . . . . 6
1. 1.2 Categories of TVM instructions . . . . . . . . . . . . . . . . . 9
1. 1.3 Control registers . . . . . . . . . . . . . . . . . . . . . . . . . 10
1. 1.4 Total state of TVM (SCCCG) . . . . . . . . . . . . . . . . . . 12
1. 1.5 Integer arithmetic . . . . . . . . . . . . . . . . . . . . . . . . . 13
2 The stack 16
1. 2.1 Stack calling conventions . . . . . . . . . . . . . . . . . . . . . 16
1. 2.2 Stack manipulation primitives . . . . . . . . . . . . . . . . . . 21
1. 2.3 Efficiency of stack manipulation primitives . . . . . . . . . . . 25
3 Cells, memory, and persistent storage 28
1. 3.1 Generalities on cells . . . . . . . . . . . . . . . . . . . . . . . . 28
1. 3.2 Data manipulation instructions and cells . . . . . . . . . . . . 32
1. 3.3 Hashmaps, or dictionaries . . . . . . . . . . . . . . . . . . . . 37
1. 3.4 Hashmaps with variable-length keys . . . . . . . . . . . . . . . 47
4 Control flow, continuations, and exceptions 49
1. 4.1 Continuations and subroutines . . . . . . . . . . . . . . . . . . 49
1. 4.2 Control flow primitives: conditional and iterated execution . . 53
1. 4.3 Operations with continuations . . . . . . . . . . . . . . . . . . 55
1. 4.4 Continuations as objects . . . . . . . . . . . . . . . . . . . . . 57
1. 4.5 Exception handling . . . . . . . . . . . . . . . . . . . . . . . . 58
1. 4.6 Functions, recursion, and dictionaries . . . . . . . . . . . . . . 61
5 Codepages and instruction encoding 67
1. 5.1 Codepages and interoperability of different TVM versions . . . 67
1. 5.2 Instruction encoding . . . . . . . . . . . . . . . . . . . . . . . 70
1. 5.3 Instruction encoding in codepage zero . . . . . . . . . . . . . . 73
A Instructions and opcodes 77
A.1 Gas prices . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 77
A.2 Stack manipulation primitives . . . . . . . . . . . . . . . . . . 78
A.3 Tuple, List, and Null primitives . . . . . . . . . . . . . . . . . 81
A.4 Constant, or literal primitives . . . . . . . . . . . . . . . . . . 86
3

