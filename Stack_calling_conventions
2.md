1. 2.1. Stack calling conventions
1. 2.1.6. Order of function arguments. If a function or primitive requires
m arguments x , ..., x , they are pushed by the caller into the stack in the
1 m
same order, starting from x . Therefore, when the function or primitive is
1
invoked, its first argument x is in s(m − 1), its second argument x is in
1 2
s(m−2), and so on. The last argument x is in s0 (i.e., at the top of the
m
stack). It is the called function or primitive’s responsibility to remove its
arguments from the stack.
In this respect the TVM stack calling conventions—obeyed, at least, by
TMV primitives—match those of Pascal and Forth, and are the opposite of
those of C (in which the arguments are pushed into the stack in the reverse
order, and are removed by the caller after it regains control, not the callee).
Of course, an implementation of a high-level language for TVM might
choose some other calling conventions for its functions, different from the
default ones. This might be useful for certain functions—for instance, if the
total number of arguments depends on the value of the first argument, as
happens for “variadic functions” such as scanf and printf. In such cases,
the first one or several arguments are better passed near the top of the stack,
not somewhere at some unknown location deep in the stack.
1. 2.1.7. Arguments to arithmetic primitives on register machines.
On a stack machine, built-in arithmetic primitives (such as ADD or DIVMOD)
follow the same calling conventions as user-defined functions. In this respect,
user-defined functions (for example, a function computing the square root of
a number) might be considered as “extensions” or “custom upgrades” of the
stack machine. This is one of the clearest advantages of stack machines
(and of stack programming languages such as Forth) compared to register
machines.
In contrast, arithmetic instructions (built-in operations) on register ma-
chines usually get their parameters from general-purpose registers encoded
in the full opcode. A binary operation, such as SUB, thus requires two argu-
ments, r(i) and r(j), with i and j specified by the instruction. A register
r(k) for storing the result also must be specified. Arithmetic operations can
take several possible forms, depending on whether i, j, and k are allowed to
take arbitrary values:
• Three-address form — Allows the programmer to arbitrarily choose
not only the two source registers r(i) and r(j), but also a separate
cumulator register, if present, is also r0; for simplicity, we will resolve this problem by
assuming that the first argument to a function is passed in the accumulator.
18

