C.3. Sample non-leaf function
PUSH r1 // STACK: a b
MOV r0,r1 // b
MOV r1,r2 // c
CALL r_mul // bc
PUSH r0 // .. a b bc
LD s2 // a
MOV r1,r3 // d
CALL r_mul // ad
POP r1 // bc; .. a b
CALL r_sub // D:=ad-bc
XCHG s0 // b; .. a D
MOV r1,r5 // f
CALL r_mul // bf
PUSH r0 // .. a D bf
MOV r0,r4 // e
MOV r1,r3 // d
CALL r_mul // ed
POP r1 // bf; .. a D
CALL r_sub // Dx:=ed-bf
XCHG s1 // a ; .. Dx D
MOV r1,r5 // f
CALL r_mul // af
PUSH r0 // .. Dx D af
MOV r0,r4 // e
MOV r1,r2 // c
CALL r_mul // ec
MOV r1,r0 // ec
POP r0 // af; .. Dx D
CALL r_sub // Dy:=af-ec
XCHG s1 // Dx; .. Dy D
POP r1 // D ; .. Dy
PUSH r1 // .. Dy D
CALL r_div // x:=Dx/D
XCHG s1 // Dy; .. x D
POP r1 // D ; .. x
CALL r_div // y:=Dy/D
MOV r1,r0 // y
POP r0 // x
167

