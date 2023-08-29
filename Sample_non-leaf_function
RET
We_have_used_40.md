C.3. Sample non-leaf function
RET
We have used 40 instructions: 18 one-byte, 11 two-byte, and 11 three-byte,
for a total of 18·1+11·2+11·3 = 73 bytes.
C.3.8. Stack machine with basic stack primitives. We reuse the code
provided in C.1.5, simply replacing arithmetic primitives (VM instructions)
with subroutine calls. The only substantive modification is the insertion
of the previously optional XCHG s1 before the third multiplication, because
even an optimizing compiler cannot now know whether CALL r_mul is a
commutative operation. We have also used the “tail recursion optimization”
by replacing the final CALL r_div followed by RET with JMP r_div.
PUSH s5 // a b c d e f a
PUSH s3 // a b c d e f a d
CALL r_mul // a b c d e f ad
PUSH s5 // a b c d e f ad b
PUSH s5 // a b c d e f ad b c
CALL r_mul // a b c d e f ad bc
CALL r_sub // a b c d e f ad-bc
XCHG s3 // a b c ad-bc e f d
PUSH s2 // a b c ad-bc e f d e
XCHG s1 // a b c ad-bc e f e d
CALL r_mul // a b c ad-bc e f ed
XCHG s5 // a ed c ad-bc e f b
PUSH s1 // a ed c ad-bc e f b f
CALL r_mul // a ed c ad-bc e f bf
XCHG s1,s5 // a f c ad-bc e ed bf
CALL r_sub // a f c ad-bc e ed-bf
XCHG s3 // a f ed-bf ad-bc e c
CALL r_mul // a f ed-bf ad-bc ec
XCHG s3 // a ec ed-bf ad-bc f
XCHG s1,s4 // ad-bc ec ed-bf a f
CALL r_mul // D ec Dx af
XCHG s1 // D ec af Dx
XCHG s2 // D Dx af ec
CALL r_sub // D Dx Dy
XCHG s1 // D Dy Dx
PUSH s2 // D Dy Dx D
168

