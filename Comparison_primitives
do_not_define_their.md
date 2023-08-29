A.6. Comparison primitives
do not define their “boolean circuit” counterparts, which would transfer con-
trol to c0 or c1 depending on the result of the comparison. If needed, such
instructions can be simulated with the aid of RETBOOL.
Quietversionsofintegercomparisonprimitivesarealsoavailable,encoded
with the aid of the QUIET prefix (B7). If any of the integers being compared
are NaNs, the result of a quiet comparison will also be a NaN (“undefined”),
instead of a −1 (“yes”) or 0 (“no”), thus effectively supporting ternary logic.
• B8 — SGN (x – sgn(x)), computes the sign of an integer x: −1 if x < 0,
0 if x = 0, 1 if x > 0.
• B9 — LESS (x y – x < y), returns −1 if x < y, 0 otherwise.
• BA — EQUAL (x y – x = y), returns −1 if x = y, 0 otherwise.
• BB — LEQ (x y – x ≤ y).
• BC — GREATER (x y – x > y).
• BD — NEQ (x y – x (cid:54)= y), equivalent to EQUAL; NOT.
• BE — GEQ (x y – x ≥ y), equivalent to LESS; NOT.
• BF — CMP (x y – sgn(x−y)), computes the sign of x−y: −1 if x < y,
0 if x = y, 1 if x > y. No integer overflow can occur here unless x or y
is a NaN.
• C0yy — EQINT yy (x – x = yy) for −27 ≤ yy < 27.
• C000 — ISZERO, checks whether an integer is zero. Corresponds to
Forth’s 0=.
• C1yy — LESSINT yy (x – x < yy) for −27 ≤ yy < 27.
• C100 — ISNEG, checks whether an integer is negative. Corresponds to
Forth’s 0<.
• C101 — ISNPOS, checks whether an integer is non-positive.
• C2yy — GTINT yy (x – x > yy) for −27 ≤ yy < 27.
• C200 — ISPOS, checks whether an integer is positive. Corresponds to
Forth’s 0>.
93

