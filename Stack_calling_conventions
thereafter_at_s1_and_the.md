1. 2.1. Stack calling conventions
thereafter at s1 and the remainder at s0. The net effect of DIVMOD is to
divide the original value of s1 by the original value of s0, and return the
quotient in s1 and the remainder in s0. In this particular case the depth
of the stack and the values of all other “stack registers” remain unchanged,
because DIVMOD takes two arguments and returns two results. In general, the
values of other “stack registers” that lie in the stack below the arguments
passed and the values returned are shifted according to the change of the
depth of the stack.
In principle, some primitives and user-defined functions might return a
variable number of result values. In this respect, the remarks above about
variadic functions (cf. 2.1.6) apply: the total number of result values and
their types should be determined by the values near the top of the stack.
(For example, one might push the return values y , ..., y , and then push
1 k
their total number k as an integer. The caller would then determine the total
number of returned values by inspecting s0.)
In this respect TVM, again, faithfully observes Forth calling conventions.
1. 2.1.10. Stack notation. When a stack of depth n contains values z , ...,
1
z , in that order, with z the deepest element and z the top of the stack,
n 1 n
the contents of the stack are often represented by a list z z ...z , in that
1 2 n
order. When a primitive transforms the original stack state S(cid:48) into a new
state S(cid:48)(cid:48), this is often written as S(cid:48) – S(cid:48)(cid:48); this is the so-called stack notation.
For example, the action of the division primitive DIV can be described by S
x y – S (cid:98)x/y(cid:99), where S is any list of values. This is usually abbreviated as x
y – (cid:98)x/y(cid:99), tacitly assuming that all other values deeper in the stack remain
intact.
Alternatively, one can describe DIV as a primitive that runs on a stack S(cid:48)
of depth n ≥ 2, divides s1 by s0, and returns the floor-rounded quotient as
s0 of the new stack S(cid:48)(cid:48) of depth n−1. The new value of s(i) equals the old
value of s(i + 1) for 1 ≤ i < n − 1. These descriptions are equivalent, but
saying that DIV transforms x y into (cid:98)x/y(cid:99), or ...x y into ...(cid:98)x/y(cid:99), is more
concise.
The stack notation is extensively used throughout Appendix A, where all
currently defined TVM primitives are listed.
1. 2.1.11. Explicitly defining the number of arguments to a function.
Stack machines usually pass the current stack in its entirety to the invoked
primitive or function. That primitive or function accesses only the several
values near the top of the stack that represent its arguments, and pushes the
20

