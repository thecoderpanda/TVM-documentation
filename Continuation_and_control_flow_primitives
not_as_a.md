A.8. Continuation and control flow primitives
not as a break. One should use either alternative (experimental) loops
or alternative RETALT (along with a SETEXITALT before the loop) to
break out of a loop.
• E5 — REPEATEND (n – ), similar to REPEAT, but it is applied to the
current continuation cc.
• E6 — UNTIL (c – ), executes continuation c, then pops an integer x
from the resulting stack. If x is zero, performs another iteration of
this loop. The actual implementation of this primitive involves an
extraordinary continuation ec_until (cf. 4.1.5) with its arguments
set to the body of the loop (continuation c) and the original current
continuation cc. This extraordinary continuation is then saved into
the savelist of c as c.c0 and the modified c is then executed. The
other loop primitives are implemented similarly with the aid of suitable
extraordinary continuations.
• E7 — UNTILEND ( – ), similar to UNTIL, but executes the current contin-
uation cc in a loop. When the loop exit condition is satisfied, performs
a RET.
• E8 — WHILE (c(cid:48) c – ), executes c(cid:48) and pops an integer x from the
resulting stack. If x is zero, exists the loop and transfers control to
the original cc. If x is non-zero, executes c, and then begins a new
iteration.
• E9 — WHILEEND (c(cid:48) – ), similar to WHILE, but uses the current continu-
ation cc as the loop body.
• EA — AGAIN (c – ), similar to REPEAT, but executes c infinitely many
times. A RET only begins a new iteration of the infinite loop, which can
be exited only by an exception, or a RETALT (or an explicit JMPX).
• EB — AGAINEND ( – ), similar to AGAIN, but performed with respect to
the current continuation cc.
• E314 — REPEATBRK (n c – ), similar to REPEAT, but also sets c1 to
the original cc after saving the old value of c1 into the savelist of the
original cc. In this way RETALT could be used to break out of the loop
body.
109

