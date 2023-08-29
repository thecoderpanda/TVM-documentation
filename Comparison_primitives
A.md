A.6. Comparison primitives
A.5.4. Quiet arithmetic primitives. We opted to make all arithmetic
operations “non-quiet” (signaling) by default, and create their quiet counter-
parts by means of a prefix. Such an encoding is definitely sub-optimal. It is
not yet clear whether it should be done in this way, or in the opposite way
by making all arithmetic operations quiet by default, or whether quiet and
non-quiet operations should be given opcodes of equal length; this can only
be settled by practice.
• B7xx — QUIET prefix, transforming any arithmetic operation into its
“quiet” variant, indicated by prefixing a Q to its mnemonic. Such op-
erations return NaNs instead of throwing integer overflow exceptions if
the results do not fit in Integers, or if one of their arguments is a NaN.
Notice that this does not extend to shift amounts and other parame-
ters that must be within a small range (e.g., 0–1023). Also notice that
this does not disable type-checking exceptions if a value of a type other
than Integer is supplied.
• B7A0 — QADD (x y – x+y), always works if x and y are Integers, but
returns a NaN if the addition cannot be performed.
• B7A904 — QDIV (x y – (cid:98)x/y(cid:99)), returns a NaN if y = 0, or if y = −1 and
x = −2256, or if either of x or y is a NaN.
• B7B0 — QAND (x y – x&y), bitwise “and” (similar to AND), but returns
a NaN if either x or y is a NaN instead of throwing an integer overflow
exception. However, if one of the arguments is zero, and the other is a
NaN, the result is zero.
• B7B1 — QOR (x y – x∨y), bitwise “or”. If x = −1 or y = −1, the result
is always −1, even if the other argument is a NaN.
• B7B507 — QUFITS 8 (x – x(cid:48)), checks whether x is an unsigned byte
(i.e., whether 0 ≤ x < 28), and replaces x with a NaN if this is not the
case; leaves x intact otherwise (i.e., if x is an unsigned byte).
A.6 Comparison primitives
A.6.1. Integer comparison. All integer comparison primitives return in-
teger −1 (“true”) or 0 (“false”) to indicate the result of the comparison. We
92

