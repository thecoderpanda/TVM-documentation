1. 2.1. Stack calling conventions
Similarly, when a value x is popped from a stack of depth n ≥ 1, it is the
old value of s0 (i.e., the old value at the top of the stack). After this, it is
removed from the stack, and the old s1 becomes the new s0 (the new value
at the top of the stack), the old s2 becomes the new s1, and so on. The
depth of the resulting stack is n−1.
If originally n = 0, then the stack is empty, and a value cannot be popped
from it. If a primitive attempts to pop a value from an empty stack, a stack
underflow exception occurs.
1. 2.1.3. Notation for hypothetical general-purpose registers. In order
tocomparestackmachineswithsufficientlygeneralregistermachines, wewill
denote the general-purpose registers of a register machine by r0, r1, and so
on, or by r(0), r(1), ..., r(n−1), where n is the total number of registers.
When we need a specific value of n, we will use n = 16, corresponding to the
very popular x86-64 architecture.
1. 2.1.4. The top-of-stack register s0 vs. the accumulator register r0.
Some register machine architectures require one of the arguments for most
arithmetic and logical operations to reside in a special register called the
accumulator. In our comparison, we will assume that the accumulator is
the general-purpose register r0; otherwise we could simply renumber the
registers. In this respect, the accumulator is somewhat similar to the top-of-
stack “register” s0 of a stack machine, because virtually all operations of a
stack machine both use s0 as one of their arguments and return their result
as s0.
1. 2.1.5. Register calling conventions. When compiled for a register ma-
chine, high-levellanguagefunctionsusuallyreceivetheirargumentsincertain
registers in a predefined order. If there are too many arguments, these func-
tions take the remainder from the stack (yes, a register machine usually has
a stack, too!). Some register calling conventions pass no arguments in regis-
ters at all, however, and only use the stack (for example, the original calling
conventions used in implementations of Pascal and C, although modern im-
plementations of C use some registers as well).
For simplicity, we will assume that up to m ≤ n function arguments are
passed in registers, and that these registers are r0, r1, ..., r(m−1), in that
order (if some other registers are used, we can simply renumber them).6
6Our inclusion of r0 here creates a minor conflict with our assumption that the ac-
17

