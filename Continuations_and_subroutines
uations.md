1. 4.1. Continuations and subroutines
uations, representing certain less common states. Examples of extraordinary
continuations include:
• The continuation ec_quit with its parameter set to zero, which rep-
resents the end of the work of TVM. This continuation is the original
value of c0 when TVM begins executing the code of a smart contract.
• The continuation ec_until, which contains references to two other
continuations (ordinary or not) representing the body of the loop being
executed and the code to be executed after the loop.
Execution of an extraordinary continuation by TVM depends on its specific
class, and differs from the operations for ordinary continuations described in
1. 4.1.4.21
1. 4.1.6. Switching to another continuation: JMP and RET. The process of
switching to another continuation c may be performed by such instructions
as JMPX (which takes c from the stack) or RET (which uses c0 as c). This
process is slightly more complex than simply setting the value of cc to c:
before doing this, either all values or the top n values in the current stack
are moved to the stack of the continuation c, and only then is the remainder
of the current stack discarded.
If all values need to be moved (the most common case), and if the con-
tinuation c has an empty stack (also the most common case; notice that
extraordinary continuations are assumed to have an empty stack), then the
new stack of c equals the stack of the current continuation, so we can simply
transfer the current stack in its entirety to c. (If we keep the current stack
as a separate part of the total state of TVM, we have to do nothing at all.)
1. 4.1.7. Determining the number n of arguments passed to the next
continuation c. By default, n equals the depth of the current stack. How-
ever, ifchasanexplicitvalueofnargs(numberofargumentstobeprovided),
then n is computed as n(cid:48), equal to c.nargs minus the current depth of c’s
stack.
Furthermore, there are special forms of JMPX and RET that provide an
explicit value n(cid:48)(cid:48), the number of parameters from the current stack to be
passed to continuation c. If n(cid:48)(cid:48) is provided, it must be less than or equal to
21Technically, TVM may simply invoke a virtual method run() of the continuation
currently in cc.
51

