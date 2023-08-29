1. 4.1. Continuations and subroutines
the depth of the current stack, or else a stack underflow exception occurs. If
both n(cid:48) and n(cid:48)(cid:48) are provided, we must have n(cid:48) ≤ n(cid:48)(cid:48), in which case n = n(cid:48) is
used. If n(cid:48)(cid:48) is provided and n(cid:48) is not, then n = n(cid:48)(cid:48) is used.
One could also imagine that the default value of n(cid:48)(cid:48) equals the depth of
the original stack, and that n(cid:48)(cid:48) values are always removed from the top of
the original stack even if only n(cid:48) of them are actually moved to the stack of
the next continuation c. Even though the remainder of the current stack is
discarded afterwards, this description will become useful later.
1. 4.1.8. Restoring control registers from the new continuation c. After
the new stack is computed, the values of control registers present in c.save
are restored accordingly, and the current codepage cp is also set to c.cp.
Only then does TVM set cc equal to the new c and begin its execution.22
1. 4.1.9. Subroutine calls: CALLX or EXECUTE primitives. The execution
of continuations as subroutines is slightly more complicated than switching
to continuations.
Consider the CALLX or EXECUTE primitive, which takes a continuation c
from the (current) stack and executes it as a subroutine.
Apart from doing the stack manipulations described in 4.1.6 and 4.1.7
and setting the new control registers and codepage as described in 4.1.8,
these primitives perform several additional steps:
1. 1. After the top n(cid:48)(cid:48) values are removed from the current stack (cf. 4.1.7),
the (usually empty) remainder is not discarded, but instead is stored
in the (old) current continuation cc.
1. 2. The old value of the special register c0 is saved into the (previously
empty) savelist cc.save.
1. 3. The continuation cc thus modified is not discarded, but instead is set
as the new c0, which performs the role of “next continuation” or “return
continuation” for the subroutine being called.
1. 4. After that, the switching to c continues as before. In particular, some
control registers are restored from c.save, potentially overwriting the
value of c0 set in the previous step. (Therefore, a good optimization
would be to check that c0 is present in c.save from the very beginning,
and skip the three previous steps as useless in this case.)
22Thealreadyusedsavelistcc.saveofthenewccisemptiedbeforetheexecutionstarts.
52

