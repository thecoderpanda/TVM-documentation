1. 4.1. Continuations and subroutines
4 Control flow, continuations, and exceptions
This chapter describes continuations, which may represent execution tokens
and exception handlers in TVM. Continuations are deeply involved with the
control flow of a TVM program; in particular, subroutine calls and condi-
tional and iterated execution are implemented in TVM using special primi-
tives that accept one or more continuations as their arguments.
We conclude this chapter with a discussion of the problem of recursion
and of families of mutually recursive functions, exacerbated by the fact that
cyclic references are not allowed in TVM data structures (including TVM
code).
1. 4.1 Continuations and subroutines
Recall (cf.1.1.3) that Continuation values represent “execution tokens” that
can be executed later—for example, by EXECUTE=CALLX (“execute” or “call
indirect”) or JMPX (“jump indirect”) primitives. As such, the continuations
are responsible for the execution of the program, and are heavily used by
control flow primitives, enabling subroutine calls, conditional expressions,
loops, and so on.
1. 4.1.1. Ordinary continuations. The most common kind of continuations
are the ordinary continuations, containing the following data:
• A Slice code (cf. 1.1.3 and 3.2.2), containing (the remainder of) the
TVM code to be executed.
• A (possibly empty) Stack stack, containing the original contents of
the stack for the code to be executed.
• A (possibly empty) list save of pairs (c(i),v ) (also called “savelist”),
i
containing the values of control registers to be restored before the ex-
ecution of the code.
• A16-bitintegervaluecp, selectingtheTVMcodepageusedtointerpret
the TVM code from code.
• An optional non-negative integer nargs, indicating the number of ar-
guments expected by the continuation.
49

