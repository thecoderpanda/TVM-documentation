C.3. Sample non-leaf function
MOV r0,r4 // e
MOV r1,r3 // d
CALL r_mul // ed
POP r1 // bf; .. a D
CALL r_sub // Dx:=ed-bf
XCHG r0,s1 // a ; .. Dx D
MOV r1,r5 // f
CALL r_mul // af
PUSH r0 // .. Dx D af
MOV r0,r4 // e
MOV r1,r2 // c
CALL r_mul // ec
MOV r1,r0 // ec
POP r0 // af; .. Dx D
CALL r_sub // Dy:=af-ec
XCHG r0,s1 // Dx; .. Dy D
MOV r1,s0 // D
CALL r_div // x:=Dx/D
XCHG r0,s1 // Dy; .. x D
POP r1 // D ; .. x
CALL r_div // y:=Dy/D
MOV r1,r0 // y
POP r0 // x
RET
We haveused 39 instructions: 11 one-byte, 17two-byte (among them 5 “new”
instructions), and 11 three-byte, for a total of 11 · 1 + 17 · 2 + 11 · 3 = 78
bytes. Somewhat paradoxically, the code size in bytes is slightly longer than
in the previous case (cf. C.3.2), contrary to what one might have expected.
This is partially due to the fact that we have assumed two-byte encodings for
“new” MOV and XCHG instructions involving the stack, similarly to the “old”
instructions. Most existing architectures (such as x86-64) use longer encod-
ings (maybe even twice as long) for their counterparts of our “new” move and
exchange instructions compared to the “usual” register-register ones. Taking
this into account, we see that we would have obtained here 83 bytes (versus
87 for the code in C.3.2) assuming three-byte encodings of new operations,
and 88 bytes (versus 98) assuming four-byte encodings. This shows that,
for two-address architectures without optimized encodings for register-stack
164

