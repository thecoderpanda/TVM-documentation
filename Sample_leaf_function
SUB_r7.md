C.1. Sample leaf function
SUB r7 // r0 := ad-bc = D
XCHG r1 // r1 := D, r0 := b
IMUL r5 // r0 := bf
XCHG r3 // r0 := d, r3 := bf
IMUL r4 // r0 := de
SUB r3 // r0 := de-bf = Dx
IDIV r1 // r0 := Dx/D = x
XCHG r2 // r0 := c, r2 := x
IMUL r4 // r0 := ce
XCHG r5 // r0 := f, r5 := ce
IMUL r8 // r0 := af
SUB r5 // r0 := af-ce = Dy
IDIV r1 // r0 := Dy/D = y
MOV r1,r0 // r1 := y
MOV r0,r2 // r0 := x
RET
Wehaveused23operations; ifweassumeone-byteencodingforallarithmetic
operations and XCHG, and two-byte encodings for MOV, the total size of the
code will be 29 bytes. Notice, however, that to obtain the compact code
shown above we had to choose a specific order of computation, and made
heavy use of the commutativity of multiplication. (For example, we compute
bc before af, and af − bc immediately after af.) It is not clear whether a
compiler would be able to make all such optimizations by itself.
C.1.5. Stack machine with basic stack primitives. The machine code
for a stack machine equipped with basic stack manipulation primitives de-
scribed in 2.2.1 might look as follows:
PUSH s5 // a b c d e f a
PUSH s3 // a b c d e f a d
IMUL // a b c d e f ad
PUSH s5 // a b c d e f ad b
PUSH s5 // a b c d e f ad b c
IMUL // a b c d e f ad bc
SUB // a b c d e f ad-bc
XCHG s3 // a b c ad-bc e f d
PUSH s2 // a b c ad-bc e f d e
IMUL // a b c ad-bc e f de
150

