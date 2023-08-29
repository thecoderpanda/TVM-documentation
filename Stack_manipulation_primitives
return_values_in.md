1. 2.2. Stack manipulation primitives
return values in their place, by convention leaving all deeper values intact.
Then the resulting stack, again in its entirety, is returned to the caller.
MostTVMprimitivesbehaveinthisway,andweexpectmostuser-defined
functions to be implemented under such conventions. However, TVM pro-
vides mechanisms to specify how many arguments must be passed to a called
function (cf. 4.1.10). When these mechanisms are employed, the specified
number of values are moved from the caller’s stack into the (usually initially
empty) stack of the called function, while deeper values remain in the caller’s
stack and are inaccessible to the callee. The caller can also specify how many
return values it expects from the called function.
Such argument-checking mechanisms might be useful, for example, for a
library function that calls user-provided functions passed as arguments to it.
1. 2.2 Stack manipulation primitives
A stack machine, such as TVM, employs a lot of stack manipulation primi-
tives to rearrange arguments to other primitives and user-defined functions,
so that they become located near the top of the stack in correct order. This
section discusses which stack manipulation primitives are necessary and suf-
ficient for achieving this goal, and which of them are used by TVM. Some
examples of code using these primitives can be found in Appendix C.
1. 2.2.1. Basic stack manipulation primitives. The most important stack
manipulation primitives used by TVM are the following:
• Top-of-stack exchange operation: XCHG s0,s(i) or XCHG s(i) — Ex-
changes values of s0 and s(i). When i = 1, operation XCHG s1 is
traditionally denoted by SWAP. When i = 0, this is a NOP (an operation
that does nothing, at least if the stack is non-empty).
• Arbitrary exchange operation: XCHG s(i),s(j) — Exchanges values of
s(i) and s(j). Notice that this operation is not strictly necessary, be-
cause it can be simulated by three top-of-stack exchanges: XCHG s(i);
XCHG s(j); XCHG s(i). However, it isuseful to have arbitraryexchanges
as primitives, because they are required quite often.
• Push operation: PUSH s(i) — Pushes a copy of the (old) value of s(i)
into the stack. Traditionally, PUSH s0 is also denoted by DUP (it dupli-
cates the value at the top of the stack), and PUSH s1 by OVER.
21

