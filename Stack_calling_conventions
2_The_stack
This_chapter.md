1. 2.1. Stack calling conventions
2 The stack
This chapter contains a general discussion and comparison of register and
stack machines, expanded further in Appendix C, and describes the two
main classes of stack manipulation primitives employed by TVM: the basic
and thecompound stack manipulation primitives. Aninformal explanationof
their sufficiency for all stack reordering required for correctly invoking other
primitives and user-defined functions is also provided. Finally, the problem
of efficiently implementing TVM stack manipulation primitives is discussed
in 2.3.
1. 2.1 Stack calling conventions
A stack machine, such as TVM, uses the stack—and especially the values
near the top of the stack—to pass arguments to called functions and primi-
tives (such as built-in arithmetic operations) and receive their results. This
section discusses the TVM stack calling conventions, introduces some no-
tation, and compares TVM stack calling conventions with those of certain
register machines.
1. 2.1.1. Notation for “stack registers”. Recall that a stack machine, as
opposed to a more conventional register machine, lacks general-purpose reg-
isters. However, one can treat the values near the top of the stack as a kind
of “stack registers”.
We denote by s0 or s(0) the value at the top of the stack, by s1 or s(1)
the value immediately under it, and so on. The total number of values in the
stack is called its depth. If the depth of the stack is n, then s(0), s(1), ...,
s(n−1) are well-defined, while s(n) and all subsequent s(i) with i > n are
not. Any attempt to use s(i) with i ≥ n should produce a stack underflow
exception.
A compiler, or a human programmer in “TVM code”, would use these
“stack registers” to hold all declared variables and intermediate values, simi-
larly to the way general-purpose registers are used on a register machine.
1. 2.1.2. Pushing and popping values. When a value x is pushed into a
stackofdepthn, itbecomesthenews0; atthesametime, theolds0becomes
the new s1, the old s1—the new s2, and so on. The depth of the resulting
stack is n+1.
16

