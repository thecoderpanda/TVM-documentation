A.8. Continuation and control flow primitives
• ED11—SETCONTVARARGS(x x ...x crn–c(cid:48)),similartoSETCONTARGS,
1 2 r
but with 0 ≤ r ≤ 255 and −1 ≤ n ≤ 255 taken from the stack.
• ED12 — SETNUMVARARGS (c n – c(cid:48)), where −1 ≤ n ≤ 255. If n = −1,
this operation does nothing (c(cid:48) = c). Otherwise its action is similar to
SETNUMARGS n, but with n taken from the stack.
A.8.5. Creating simple continuations and closures.
• ED1E — BLESS (s – c), transforms a Slice s into a simple ordinary
continuation c, with c.code = s and an empty stack and savelist.
• ED1F — BLESSVARARGS (x ...x s r n – c), equivalent to ROT; BLESS;
1 r
ROTREV; SETCONTVARARGS.
• EErn — BLESSARGS r,n (x ...x s – c), where 0 ≤ r ≤ 15, −1 ≤
1 r
n ≤ 14, equivalent to BLESS; SETCONTARGS r,n. The value of n is
represented inside the instruction by the 4-bit integer n mod 16.
• EE0n — BLESSNUMARGS n or BLESSARGS 0,n (s – c), also transforms a
Slice s into a Continuation c, but sets c.nargs to 0 ≤ n ≤ 14.
A.8.6. Operations with continuation savelists and control registers.
• ED4i — PUSH c(i) or PUSHCTR c(i) ( – x), pushes the current value of
control register c(i). If the control register is not supported in the cur-
rent codepage, or if it does not have a value, an exception is triggered.
• ED44 — PUSH c4 or PUSHROOT, pushes the “global data root” cell refer-
ence, thus enabling access to persistent smart-contract data.
• ED5i — POP c(i) or POPCTR c(i) (x – ), pops a value x from the stack
and stores it into control register c(i), if supported in the current code-
page. Notice that if a control register accepts only values of a specific
type, a type-checking exception may occur.
• ED54 — POP c4 or POPROOT, sets the “global data root” cell reference,
thus allowing modification of persistent smart-contract data.
• ED6i — SETCONT c(i) or SETCONTCTR c(i) (x c – c(cid:48)), stores x into the
savelist of continuation c as c(i), and returns the resulting continuation
c(cid:48). Almost all operations with continuations may be expressed in terms
of SETCONTCTR, POPCTR, and PUSHCTR.
111

