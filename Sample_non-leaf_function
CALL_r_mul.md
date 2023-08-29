C.3. Sample non-leaf function
CALL r_mul // ed
POP r1 // bf; .. e D a f c
CALL r_sub // Dx:=ed-bf
XCHG s4 // e ; .. Dx D a f c
POP r1 // c ; .. Dx D a f
CALL r_mul // ec
XCHG s1 // a ; .. Dx D ec f
POP r1 // f ; .. Dx D ec
CALL r_mul // af
POP r1 // ec; .. Dx D
CALL r_sub // Dy:=af-ec
XCHG s1 // Dx; .. Dy D
POP r1 // D ; .. Dy
PUSH r1 // .. Dy D
CALL r_div // x:=Dx/D
XCHG s1 // Dy; .. x D
POP r1 // D ; .. x
CALL r_div // y:=Dy/D
XCHG r1 // r1:=y
POP r0 // r0:=x ; ..
RET
We have used 45 instructions: 34 one-byte and 11 three-byte, for a total of 67
bytes. Compared to the 76 bytes used by two- and three-address machines
in C.3.2, we see that, again, the one-address register machine code may be
denser than that of two-register machines, at the expense of utilizing more
opcode space (just as shown in C.2). However, this time the extra 3/16 of
the opcode space was used for data manipulation instructions, which do not
depend on specific arithmetic operations or user functions invoked.
C.3.6. One-address register machine, m = 8 preserved registers.
As explained in C.3.3, the preservation of r8–r15 between subroutine calls
does not improve the size of our previously written code, so the one-address
machine will use for m = 8 the same code provided in C.3.5.
C.3.7. One-address register machine, m = 16 preserved registers.
We simply adapt the code provided in C.3.4 to the one-address register
machine:
PUSH r0 // STACK: a
166

