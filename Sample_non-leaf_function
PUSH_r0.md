C.3. Sample non-leaf function
PUSH r0 // .. e b a f c d bc
MOV r0,s4 // a
MOV r1,s1 // d
CALL r_mul // ad
POP r1 // bc; .. e b a f c d
CALL r_sub // D:=ad-bc
XCHG r0,s4 // b ; .. e D a f c d
MOV r1,s2 // f
CALL r_mul // bf
POP r1 // d ; .. e D a f c
PUSH r0 // .. e D a f c bf
MOV r0,s5 // e
CALL r_mul // ed
POP r1 // bf; .. e D a f c
CALL r_sub // Dx:=ed-bf
XCHG r0,s4 // e ; .. Dx D a f c
POP r1 // c ; .. Dx D a f
CALL r_mul // ec
XCHG r0,s1 // a ; .. Dx D ec f
POP r1 // f ; .. Dx D ec
CALL r_mul // af
POP r1 // ec; .. Dx D
CALL r_sub // Dy:=af-ec
XCHG r0,s1 // Dx; .. Dy D
MOV r1,s0 // D
CALL r_div // x:=Dx/D
XCHG r0,s1 // Dy; .. x D
POP r1 // D ; .. x
CALL r_div // y:=Dy/D
MOV r1,r0 // y
POP r0 // x ; ..
RET
We have used 41 instructions: 17 one-byte (eight PUSH/POP pairs and one
RET), 13 two-byte (MOV and XCHG; out of them 11 “new” ones, involving the
stack), and 11 three-byte (CALL), for a total of 17 · 1 + 13 · 2 + 11 · 3 = 76
bytes.32
32Code produced for this function by an optimizing compiler for x86-64 architecture
162

