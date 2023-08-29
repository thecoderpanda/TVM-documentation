C.3. Sample non-leaf function
We will ignore all questions related to allocating new objects of type Rational
in memory (e.g., in heap), and to preventing memory leaks. We may assume
that the called subroutines r_sub, r_mul, and so on allocate new objects
simply by advancing some pointer in a pre-allocated buffer, and that unused
objects are later freed by a garbage collector, external to the code being
analysed.
Rational numbers will now be represented by pointers, addresses, or ref-
erences, which will fit into registers of our hypothetical register machines or
into the stack of our stack machines. If we want to use TVM as an instance
of these stack machines, we should use values of type Cell to represent such
references to objects of type Rational in memory.
We assume that subroutines (or functions) are called by a special CALL
instruction, which is encoded by three bytes, including the specification of
the function to be called (e.g., the index in a “global function table”).
C.3.2. Three-address and two-address register machines, m = 0 pre-
served registers. Because our sample function does not use built-in arith-
metic instructions at all, compilers for our hypothetical three-address and
two-address register machines will produce the same machine code. Apart
fromthepreviouslyintroducedPUSH r(i)andPOP r(i)one-byteinstructions,
we assume that our two- and three-address machines support the following
two-byteinstructions: MOV r(i),s(j), MOV s(j),r(i), andXCHG r(i),s(j), for
0 ≤ i,j ≤ 15. Such instructions occupy only 3/256 of the opcode space, so
their addition seems quite natural.
We first assume that m = 0 (i.e., that all subroutines are free to destroy
the values of all registers). In this case, our machine code for r_f does
not have to preserve any registers, but has to save all registers containing
useful values into the stack before calling any subroutines. A size-optimizing
compiler might produce the following code:
PUSH r4 // STACK: e
PUSH r1 // STACK: e b
PUSH r0 // .. e b a
PUSH r6 // .. e b a f
PUSH r2 // .. e b a f c
PUSH r3 // .. e b a f c d
MOV r0,r1 // b
MOV r1,r2 // c
CALL r_mul // bc
161

