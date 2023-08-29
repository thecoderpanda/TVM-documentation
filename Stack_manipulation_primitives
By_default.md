A.2. Stack manipulation primitives
By default, the gas price of an instruction equals P := P +C +L+B +C .
b r w w
A.2 Stack manipulation primitives
This section includes both the basic (cf. 2.2.1) and the compound (cf. 2.2.3)
stack manipulation primitives, as well as some “unsystematic” ones. Some
compound stack manipulation primitives, such as XCPU or XCHG2, turn out
to have the same length as an equivalent sequence of simpler operations. We
have included these primitives regardless, so that they can easily be allocated
shorter opcodes in a future revision of TVM—or removed for good.
Some stack manipulation instructions have two mnemonics: one Forth-
style (e.g., -ROT), the other conforming to the usual rules for identifiers (e.g.,
ROTREV). Whenever a stack manipulation primitive (e.g., PICK) accepts an
integer parameter n from the stack, it must be within the range 0...255;
otherwise a range check exception happens before any further checks.
A.2.1. Basic stack manipulation primitives.
• 00 — NOP, does nothing.
• 01 — XCHG s1, also known as SWAP.
• 0i — XCHG s(i) or XCHG s0,s(i), interchanges the top of the stack with
s(i), 1 ≤ i ≤ 15.
• 10ij — XCHG s(i),s(j), 1 ≤ i < j ≤ 15, interchanges s(i) with s(j).
• 11ii — XCHG s0,s(ii), with 0 ≤ ii ≤ 255.
• 1i — XCHG s1,s(i), 2 ≤ i ≤ 15.
• 2i — PUSH s(i), 0 ≤ i ≤ 15, pushes a copy of the old s(i) into the
stack.
• 20 — PUSH s0, also known as DUP.
• 21 — PUSH s1, also known as OVER.
• 3i — POP s(i), 0 ≤ i ≤ 15, pops the old top-of-stack value into the old
s(i).
• 30 — POP s0, also known as DROP, discards the top-of-stack value.
78

