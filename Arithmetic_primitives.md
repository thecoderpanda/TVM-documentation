A.5. Arithmetic primitives
• B2 — XOR (x y – x⊕y), bitwise “xor” of two integers.
• B3 — NOT (x – x⊕−1 = −1−x), bitwise “not” of an integer.
• B4cc — FITS cc + 1 (x – x), checks whether x is a cc + 1-bit signed
integer for 0 ≤ cc ≤ 255 (i.e., whether −2cc ≤ x < 2cc). If not, either
triggers an integer overflow exception, or replaces x with a NaN (quiet
version).
• B400 — FITS 1 or CHKBOOL (x – x), checks whether x is a “boolean
value” (i.e., either 0 or -1).
• B5cc — UFITS cc+1 (x – x), checks whether x is a cc+1-bit unsigned
integer for 0 ≤ cc ≤ 255 (i.e., whether 0 ≤ x < 2cc+1).
• B500 — UFITS 1 or CHKBIT, checks whether x is a binary digit (i.e.,
zero or one).
• B600 — FITSX (x c – x), checks whether x is a c-bit signed integer for
0 ≤ c ≤ 1023.
• B601 — UFITSX (x c – x), checks whether x is a c-bit unsigned integer
for 0 ≤ c ≤ 1023.
• B602 — BITSIZE (x – c), computes smallest c ≥ 0 such that x fits into
a c-bit signed integer (−2c−1 ≤ c < 2c−1).
• B603 — UBITSIZE (x – c), computes smallest c ≥ 0 such that x fits
into a c-bit unsigned integer (0 ≤ x < 2c), or throws a range check
exception.
• B608 — MIN (x y – x or y), computes the minimum of two integers x
and y.
• B609 — MAX (x y – x or y), computes the maximum of two integers x
and y.
• B60A—MINMAXorINTSORT2(xy –xy ory x),sortstwointegers. Quiet
version of this operation returns two NaNs if any of the arguments are
NaNs.
• B60B — ABS (x – |x|), computes the absolute value of an integer x.
91

