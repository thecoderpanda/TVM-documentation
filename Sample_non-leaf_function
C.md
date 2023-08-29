C.3. Sample non-leaf function
C.3.3. Three-address and two-address register machines, m = 8
preserved registers. Now we have eight registers, r8 to r15, that are
preserved by subroutine calls. We might keep some intermediate values there
instead of pushing them into the stack. However, the penalty for doing so
consists in a PUSH/POP pair for every such register that we choose to use,
because our function is also required to preserve its original value. It seems
that using these registers under such a penalty does not improve the density
of the code, so the optimal code for three- and two-address machines for
m = 8 preserved registers is the same as that provided in C.3.2, with a total
of 42 instructions and 74 code bytes.
C.3.4. Three-address and two-address register machines, m = 16
preserved registers. This time all registers must be preserved by the
subroutines, excluding those used for returning the results. This means that
our code must preserve the original values of r2 to r5, as well as any other
registers it uses for temporary values. A straightforward way of writing the
code of our subroutine would be to push registers r2 up to, say, r8 into the
stack, then perform all the operations required, using r6–r8 for intermediate
values, and finally restore registers from the stack. However, this would not
optimize code size. We choose another approach:
PUSH r0 // STACK: a
PUSH r1 // STACK: a b
MOV r0,r1 // b
MOV r1,r2 // c
CALL r_mul // bc
PUSH r0 // .. a b bc
MOV r0,s2 // a
MOV r1,r3 // d
CALL r_mul // ad
POP r1 // bc; .. a b
CALL r_sub // D:=ad-bc
XCHG r0,s0 // b; .. a D
MOV r1,r5 // f
CALL r_mul // bf
PUSH r0 // .. a D bf
with size-optimization enabled actually occupied 150 bytes, due mostly to the fact that
actual instruction encodings are about twice as long as we had optimistically assumed.
163

