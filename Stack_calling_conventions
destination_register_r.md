1. 2.1. Stack calling conventions
destination register r(k). This form is common for most RISC proces-
sors, and for the XMM and AVX SIMD instruction sets in the x86-64
architecture.
• Two-address form — Uses one of the two operand registers (usually
r(i)) to store the result of an operation, so that k = i is never indicated
explicitly. Only i and j are encoded inside the instruction. This is the
most common form of arithmetic operations on register machines, and
is quite popular on microprocessors (including the x86 family).
• One-address form — Always takes one of the arguments from the ac-
cumulator r0, and stores the result in r0 as well; then i = k = 0, and
only j needs to be specified by the instruction. This form is used by
some simpler microprocessors (such as Intel 8080).
Note that this flexibility is available only for built-in operations, but not
for user-defined functions. In this respect, register machines are not as easily
“upgradable” as stack machines.7
1. 2.1.8. Return values of functions. In stack machines such as TVM,
when a function or primitive needs to return a result value, it simply pushes
it into the stack (from which all arguments to the function have already been
removed). Therefore, the caller will be able to access the result value through
the top-of-stack “register” s0.
This is in complete accordance with Forth calling conventions, but dif-
fers slightly from Pascal and C calling conventions, where the accumulator
register r0 is normally used for the return value.
1. 2.1.9. Returning several values. Some functions might want to return
several values y , ..., y , with k not necessarily equal to one. In these cases,
1 k
the k return values are pushed into the stack in their natural order, starting
from y .
1
For example, the “divide with remainder” primitive DIVMOD needs to re-
turn two values, the quotient q and the remainder r. Therefore, DIVMOD
pushes q and r into the stack, in that order, so that the quotient is available
7For instance, if one writes a function for extracting square roots, this function will
always accept its argument and return its result in the same registers, in contrast with
a hypothetical built-in square root instruction, which could allow the programmer to
arbitrarily choose the source and destination registers. Therefore, a user-defined function
is tremendously less flexible than a built-in instruction on a register machine.
19

