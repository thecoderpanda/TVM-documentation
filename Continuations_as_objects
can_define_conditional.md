1. 4.4. Continuations as objects
can define conditional composition primitives, performing some of the above
actions only if an integer value taken from the stack is non-zero.
For instance, EXECUTE can be described as cc ← c◦ cc, with continuation
0
c taken from the original stack. Similarly, JMPX is cc ← c, and RET (also
knownasRETTRUEinabooleancircuitcontext)iscc ← c0. Otherinteresting
primitives include THENRET (c(cid:48) ← c◦ c0) and ATEXIT (c0 ← c◦ c0).
0 0
Finally, some “experimental” primitives also involve c1 and ◦ . For ex-
1
ample:
• RETALT or RETFALSE does cc ← c1.
• Conditional versions of RET and RETALT may also be useful: RETBOOL
takes an integer x from the stack, and performs RETTRUE if x (cid:54)= 0,
RETFALSE otherwise.
• INVERT does c0 ↔ c1; if the two continuations in c0 and c1 represent
the two branches we should select depending on some boolean expres-
sion, INVERT negates this expression on the outer level.
• INVERTCONT does c.c0 ↔ c.c1 to a continuation c taken from the stack.
• Variants of ATEXIT include ATEXITALT (c1 ← c◦ c1) and SETEXITALT
1
(c1 ← (c◦ c0)◦ c1).
0 1
(cid:0)
• BOOLEVAL takes a continuation c from the stack and does cc ← (c◦
0
(cid:1)
(PUSH−1))◦ (PUSH0) ◦ cc. If c represents a boolean circuit, the net
1 0
effect is to evaluate it and push either −1 or 0 into the stack before
continuing.
1. 4.4 Continuations as objects
1. 4.4.1. Representing objects using continuations. Object-oriented pro-
gramming in Smalltalk (or Objective C) style may be implemented with the
aid of continuations. For this, an object is represented by a special continu-
ation o. If it has any data fields, they can be kept in the stack of o, making
o a partial application (i.e., a continuation with a non-empty stack).
When somebody wants to invoke a method m of o with arguments x , x ,
1 2
..., x , shepushestheargumentsintothestack, thenpushesamagicnumber
n
corresponding to the method m, and then executes o passing n+1 arguments
(cf. 4.1.10). Then o uses the top-of-stack integer m to select the branch with
57

