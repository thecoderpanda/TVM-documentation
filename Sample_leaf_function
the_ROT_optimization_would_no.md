C.1. Sample leaf function
the ROT optimization would not be applicable.
C.1.6. Stack machine with compound stack primitives. A stack ma-
chine with compound stack primitives (cf. 2.2.3) would not significantly
improve code density of the code presented above, at least in terms of bytes
used. The only difference is that, if we were not allowed to use commutativ-
ity of multiplication, the extra XCHG s1 inserted before the third IMUL might
be combined with two previous operations XCHG s3, PUSH s2 into one com-
pound operation PUXC s2,s3; we provide the resulting code below. To make
this less redundant, we show a version of the code that computes subexpres-
sion af before ec as specified in the original source file. We see that this
replaces six operations (starting from line 15) with five other operations, and
disables the ROT optimization:
PUSH s5 // a b c d e f a
PUSH s3 // a b c d e f a d
IMUL // a b c d e f ad
PUSH s5 // a b c d e f ad b
PUSH s5 // a b c d e f ad b c
IMUL // a b c d e f ad bc
SUB // a b c d e f ad-bc
PUXC s2,s3 // a b c ad-bc e f e d
IMUL // a b c ad-bc e f ed
XCHG s5 // a ed c ad-bc e f b
PUSH s1 // a ed c ad-bc e f b f
IMUL // a ed c ad-bc e f bf
XCHG s1,s5 // a f c ad-bc e ed bf
SUB // a f c ad-bc e ed-bf
XCHG s4 // a ed-bf c ad-bc e f
XCHG s1,s5 // e Dx c D a f
IMUL // e Dx c D af
XCHG s2 // e Dx af D c
XCHG s1,s4 // D Dx af e c
IMUL // D Dx af ec
SUB // D Dx Dy
XCHG s1 // D Dy Dx
PUSH s2 // D Dy Dx D
IDIV // D Dy x
XCHG s2 // x Dy D
152

