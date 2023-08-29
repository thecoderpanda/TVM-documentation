1. 1.5. Integer arithmetic
unexpected integer overflows happen to be among the most common source
of bugs.
1. 1.5.4. Reduction modulo 2n. TVM also has a primitive MODPOW2 n, which
reduces the integer at the top of the stack modulo 2n, with the result ranging
from 0 to 2n −1.
1. 1.5.5. Integer is 257-bit, not 256-bit. One can understand now why
TVM’s Integer is (signed) 257-bit, not 256-bit. The reason is that it is the
smallest integer type containing both signed 256-bit integers and unsigned
256-bit integers, which does not require automatic reinterpreting of the same
256-bit string depending on the operation used (cf. 1.5.1).
1. 1.5.6. Division and rounding. The most important division primitives
are DIV, MOD, and DIVMOD. All of them take two numbers from the stack, x
and y (y is taken from the top of the stack, and x is originally under it),
compute the quotient q and remainder r of the division of x by y (i.e., two
integers such that x = yq +r and |r| < |y|), and return either q, r, or both
of them. If y is zero, then all of the expected results are replaced by NaNs,
and (usually) an integer overflow exception is generated.
The implementation of division in TVM somewhat differs from most
other implementations with regards to rounding. By default, these prim-
itives round to −∞, meaning that q = (cid:98)x/y(cid:99), and r has the same sign
as y. (Most conventional implementations of division use “rounding to zero”
instead, meaning that r has the same sign as x.) Apart from this “floor
rounding”, two other rounding modes are available, called “ceiling rounding”
(with q = (cid:100)x/y(cid:101), and r and y having opposite signs) and “nearest round-
ing” (with q = (cid:98)x/y + 1/2(cid:99) and |r| ≤ |y|/2). These rounding modes are
selected by using other division primitives, with letters C and R appended
to their mnemonics. For example, DIVMODR computes both the quotient and
the remainder using rounding to the nearest integer.
1. 1.5.7. Combined multiply-divide, multiply-shift, and shift-divide
operations. To simplify implementation of fixed-point arithmetic, TVM
supports combined multiply-divide, multiply-shift, and shift-divide opera-
tions with double-length (i.e., 514-bit) intermediate product. For example,
MULDIVMODR takes three integer arguments from the stack, a, b, and c, first
computes ab using a 514-bit intermediate result, and then divides ab by c
using rounding to the nearest integer. If c is zero or if the quotient does not
14

