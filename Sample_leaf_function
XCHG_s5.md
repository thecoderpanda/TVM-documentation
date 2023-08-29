C.1. Sample leaf function
XCHG s5 // a de c ad-bc e f b
PUSH s1 // a de c ad-bc e f b f
IMUL // a de c ad-bc e f bf
XCHG s1,s5 // a f c ad-bc e de bf
SUB // a f c ad-bc e de-bf
XCHG s3 // a f de-bf ad-bc e c
IMUL // a f de-bf ad-bc ec
XCHG s3 // a ec de-bf ad-bc f
XCHG s1,s4 // ad-bc ec de-bf a f
IMUL // D ec Dx af
XCHG s1 // D ec af Dx
XCHG s2 // D Dx af ec
SUB // D Dx Dy
XCHG s1 // D Dy Dx
PUSH s2 // D Dy Dx D
IDIV // D Dy x
XCHG s2 // x Dy D
IDIV // x y
RET
We have used 29 operations; assuming one-byte encodings for all stack oper-
ations involved (including XCHG s1,s(i)), we have used 29 code bytes as well.
Noticethatwithone-byteencoding,the“unsystematic” operationROT(equiv-
alent to XCHG s1; XCHG s2) would reduce the operation and byte count to
1. 28. This shows that such “unsystematic” operations, borrowed from Forth,
may indeed reduce the code size on some occasions.
Notice as well that we have implicitly used the commutativity of multi-
plication in this code, computing de−bf instead of ed−bf as specified in
high-level language source code. If we were not allowed to do so, an extra
XCHG s1 would need to be inserted before the third IMUL, increasing the total
size of the code by one operation and one byte.
The code presented above might have been produced by a rather unso-
phisticated compiler that simply computed all expressions and subexpres-
sions in the order they appear, then rearranged the arguments near the top
of the stack before each operation as outlined in 2.2.2. The only “manual”
optimization done here involves computing ec before af; one can check that
the other order would lead to slightly shorter code of 28 operations and bytes
(or 29, if we are not allowed to use the commutativity of multiplication), but
151

