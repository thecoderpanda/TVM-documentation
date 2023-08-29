C.1. Sample leaf function
return (Dx / D, Dy / D);
}
We assume (cf. 2.1) that the register machines we consider accept the six
parameters a...f in registers r0...r5, and return the two values x and y in
r0 and r1. We also assume that the register machines have 16 registers, and
that the stack machine can directly access s0 to s15 by its stack manipu-
lation primitives; the stack machine will accept the parameters in s5 to s0,
and return the two values in s0 and s1, somewhat similarly to the register
machine. Finally, we assume at first that the register machine is allowed
to destroy values in all registers (which is slightly unfair towards the stack
machine); this assumption will be revisited later.
C.1.2. Three-address register machine. Themachinecode(orratherthe
corresponding assembly code) for a three-address register machine (cf. 2.1.7)
might look as follows:
IMUL r6,r0,r3 // r6 := r0 * r3 = ad
IMUL r7,r1,r2 // r7 := bc
SUB r6,r6,r7 // r6 := ad-bc = D
IMUL r3,r4,r3 // r3 := ed
IMUL r1,r1,r5 // r1 := bf
SUB r3,r3,r1 // r3 := ed-bf = Dx
IMUL r1,r0,r5 // r1 := af
IMUL r7,r4,r2 // r7 := ec
SUB r1,r1,r7 // r1 := af-ec = Dy
IDIV r0,r3,r6 // x := Dx/D
IDIV r1,r1,r6 // y := Dy/D
RET
We have used 12 operations and at least 23 bytes (each operation uses3×4 =
12 bits to indicate the three registers involved, and at least 4 bits to indicate
the operation performed; thus we need two or three bytes to encode each
operation). A more realistic estimate would be 34 (three bytes for each
arithmetic operation) or 31 bytes (two bytes for addition and subtraction,
three bytes for multiplication and division).
C.1.3. Two-address register machine. The machine code for a two-
address register machine might look as follows:
148

