C.1. Sample leaf function
MOV r6,r0 // r6 := r0 = a
MOV r7,r1 // r7 := b
IMUL r6,r3 // r6 := r6*r3 = ad
IMUL r7,r2 // r7 := bc
IMUL r3,r4 // r3 := de
IMUL r1,r5 // r1 := bf
SUB r6,r7 // r6 := ad-bc = D
IMUL r5,r0 // r5 := af
SUB r3,r1 // r3 := de-bf = Dx
IMUL r2,r4 // r2 := ce
MOV r0,r3 // r0 := Dx
SUB r5,r2 // r5 := af-ce = Dy
IDIV r0,r6 // r0 := x = Dx/D
MOV r1,r5 // r1 := Dy
IDIV r1,r6 // r1 := Dy/D
RET
We have used 16 operations; optimistically assuming each of them (with the
exception of RET) can be encoded by two bytes, this code would require 31
bytes.31
C.1.4. One-address register machine. The machine code for a one-
address register machine might look as follows:
MOV r8,r0 // r8 := r0 = a
XCHG r1 // r0 <-> r1; r0 := b, r1 := a
MOV r6,r0 // r6 := b
IMUL r2 // r0 := r0*r2; r0 := bc
MOV r7,r0 // r7 := bc
MOV r0,r8 // r0 := a
IMUL r3 // r0 := ad
31It is interesting to compare this code with that generated by optimizing C compilers
for the x86-64 architecture.
First of all, the integer division operation for x86-64 uses the one-address form, with
the (double-length) dividend to be supplied in accumulator pair r2:r0. The quotient is
also returned in r0. As a consequence, two single-to-double extension operations (CDQ or
CQO) and at least one move operation need to be added.
Secondly, the encoding used for arithmetic and move operations is less optimistic than
in our example above, requiring about three bytes per operation on average. As a result,
we obtain a total of 43 bytes for 32-bit integers, and 68 bytes for 64-bit integers.
149

