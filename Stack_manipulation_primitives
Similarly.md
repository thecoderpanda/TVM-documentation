1. 2.2. Stack manipulation primitives
Similarly, if the results returned from a function need to be discarded
or moved to other stack registers, a suitable sequence of exchange and pop
operations will do the job. In the typical case of one return value in s0,
this is achieved either by an XCHG s(i) or a POP s(i) (in most cases, a DROP)
operation.9
Rearranging the result value or values before returning from a function is
essentially the same problem as arranging arguments for a function call, and
is achieved similarly.
1. 2.2.3. Compound stack manipulation primitives. In order to improve
the density of the TVM code and simplify development of compilers, com-
pound stack manipulation primitives may be defined, each combining up to
four exchange and push or exchange and pop basic primitives. Such com-
pound stack operations might include, for example:
• XCHG2 s(i),s(j) — Equivalent to XCHG s1,s(i); XCHG s(j).
• PUSH2 s(i),s(j) — Equivalent to PUSH s(i); PUSH s(j +1).
• XCPU s(i),s(j) — Equivalent to XCHG s(i); PUSH s(j).
• PUXC s(i),s(j)—EquivalenttoPUSH s(i); SWAP;XCHG s(j+1). When
j (cid:54)= i and j (cid:54)= 0, it is also equivalent to XCHG s(j); PUSH s(i); SWAP.
• XCHG3 s(i),s(j),s(k) — Equivalent to XCHG s2,s(i); XCHG s1,s(j);
XCHG s(k).
• PUSH3 s(i),s(j),s(k) — Equivalent to PUSH s(i); PUSH s(j+1); PUSH
s(k +2).
Of course, such operations make sense only if they admit a more compact
encoding than the equivalent sequence of basic operations. For example,
if all top-of-stack exchanges, XCHG s1,s(i) exchanges, and push and pop
operations admit one-byte encodings, the only compound stack operations
suggested above that might merit inclusion in the set of stack manipulation
primitives are PUXC, XCHG3, and PUSH3.
9Notice that the most common XCHG s(i) operation is not really required here if we
do not insist on keeping the same temporary value or variable always in the same stack
location, but rather keep track of its subsequent locations. We will move it to some other
location while preparing the arguments to the next primitive or function call.
23

