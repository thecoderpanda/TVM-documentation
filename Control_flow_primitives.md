1. 4.2. Control flow primitives: conditional and iterated execution
way as EXECUTE would do it) only if x is non-zero; otherwise both values
are simply discarded from the stack. Similarly, IFNOT accepts x and c, but
executes c only if x = 0. Finally, IFELSE accepts x, c, and c(cid:48), removes these
values from the stack, and executes c if x (cid:54)= 0 or c(cid:48) if x = 0.
1. 4.2.2. Iterated execution and loops. More sophisticated modifications
of EXECUTE include:
• REPEAT — Takes an integer n and a continuation c, and executes c n
times.23
• WHILE — Takes c(cid:48) and c(cid:48)(cid:48), executes c(cid:48), and then takes the top value x
from the stack. If x is non-zero, it executes c(cid:48)(cid:48) and then begins a new
loop by executing c(cid:48) again; if x is zero, it stops.
• UNTIL — Takes c, executes it, and then takes the top integer x from
the stack. If x is zero, a new iteration begins; if x is non-zero, the
previously executed code is resumed.
1. 4.2.3. Constant, or literal, continuations. We see that we can create
arbitrarily complex conditional expressions and loops in the TVM code, pro-
vided we have a means to push constant continuations into the stack. In fact,
TVM includes special versions of “literal” or “constant” primitives that cut
the next n bytes or bits from the remainder of the current code cc.code into
a cell slice, and then push it into the stack not as a Slice (as a PUSHSLICE
does) but as a simple ordinary Continuation (which has only code and cp).
The simplest of these primitives is PUSHCONT, which has an immediate
argument n describing the number of subsequent bytes (in a byte-oriented
version of TVM) or bits to be converted into a simple continuation. Another
primitive is PUSHREFCONT, which removes the first cell reference from the
current continuation cc.code, converts the cell referred to into a cell slice,
and finally converts the cell slice into a simple continuation.
1. 4.2.4. Constant continuations combined with conditional or iter-
ated execution primitives. Because constant continuations are very often
used as arguments to conditional or iterated execution primitives, combined
23TheimplementationofREPEATinvolvesanextraordinarycontinuationthatremembers
the remaining number of iterations, the body of the loop c, and the return continuation
c(cid:48). (The latter term represents the remainder of the body of the function that invoked
REPEAT, which would be normally stored in c0 of the new cc.)
54

