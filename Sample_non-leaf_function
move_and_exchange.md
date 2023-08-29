C.3. Sample non-leaf function
move and exchange operations, m = 16 preserved registers might result in
slightly shorter code for some non-leaf functions, at the expense of leaf func-
tions (cf. C.2.3 and C.2.4), which would become considerably longer.
C.3.5. One-address register machine, m = 0 preserved registers.
For our one-address register machine, we assume that new register-stack in-
structions work through the accumulator only. Therefore, we have three
new instructions, LD s(j) (equivalent to MOV r0,s(j) of two-address ma-
chines), ST s(j) (equivalent to MOV s(j),r0), and XCHG s(j) (equivalent to
XCHG r0,s(j)). To make the comparison with two-address machines more
interesting, we assume one-byte encodings for these new instructions, even
though this would consume 48/256 = 3/16 of the opcode space.
By adapting the code provided in C.3.2 to the one-address machine, we
obtain the following:
PUSH r4 // STACK: e
PUSH r1 // STACK: e b
PUSH r0 // .. e b a
PUSH r6 // .. e b a f
PUSH r2 // .. e b a f c
PUSH r3 // .. e b a f c d
LD s1 // r0:=c
XCHG r1 // r0:=b, r1:=c
CALL r_mul // bc
PUSH r0 // .. e b a f c d bc
LD s1 // d
XCHG r1 // r1:=d
LD s4 // a
CALL r_mul // ad
POP r1 // bc; .. e b a f c d
CALL r_sub // D:=ad-bc
XCHG s4 // b ; .. e D a f c d
XCHG r1
LD s2 // f
XCHG r1 // r0:=b, r1:=f
CALL r_mul // bf
POP r1 // d ; .. e D a f c
PUSH r0 // .. e D a f c bf
LD s5 // e
165

