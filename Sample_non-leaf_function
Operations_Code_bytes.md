C.3. Sample non-leaf function
Operations Code bytes Opcode space
Machine r data arith total data arith total data arith total
3-addr. 0 0 11 12 0 27.5 28.5 64/256 4/256 69/256
2-addr. 0 4 11 16 6 22 29 64/256 4/256 69/256
1-addr. 1 13 11 25 16 16.5 32.5 64/256 4/256 69/256
stack (basic) 0 16 11 28 16 11 28 64/256 4/256 69/256
stack (comp.) 0 9 11 21 15 11 27 84/256 4/256 89/256
Table 4: A summary of machine code properties for hypothetical 3-address, 2-address,
1-address and stack machines, generated for a sample leaf function (cf. C.1.1), assuming
that only 8 of the 16 registers must be preserved by functions (m = 8, n = 16). This
time we can use fractions of bytes to encode instructions, so as to match opcode space
used by different machines. All arithmetic instructions have 8-bit opcodes, all data/stack
manipulation instructions have 4-bit opcodes. In other respects this table is similar to
Table 3.
C.3 Sample non-leaf function
This section compares the machine code for different register machines for a
sample non-leaf function. Again, we assume that either m = 0, m = 8, or
m = 16 registers are preserved by called functions, with m = 8 representing
the compromise made by most modern compilers and operating systems.
C.3.1. Sample source code for a non-leaf function. Asamplesourcefile
maybeobtainedbyreplacingthebuilt-inintegertypewithacustomRational
type, represented by a pointer to an object in memory, in our function for
solving systems of two linear equations (cf. C.1.1):
struct Rational;
typedef struct Rational *num;
extern num r_add(num, num);
extern num r_sub(num, num);
extern num r_mul(num, num);
extern num r_div(num, num);
(num, num) r_f(num a, num b, num c, num d, num e, num f) {
num D = r_sub(r_mul(a, d), r_mul(b, c)); // a*d-b*c
num Dx = r_sub(r_mul(e, d), r_mul(b, f)); // e*d-b*f
num Dy = r_sub(r_mul(a, f), r_mul(e, c)); // a*f-e*c
return (r_div(Dx, D), r_div(Dy, D)); // Dx/D, Dy/D
}
160

| Machine | r | Operations
data arith total | Code bytes
data arith total | Opcode space
data arith total |
| 3-addr. | 0 | 0 11 12 | 0 27.5 28.5 | 64/256 4/256 69/256 |
| 2-addr. | 0 | 4 11 16 | 6 22 29 | 64/256 4/256 69/256 |
| 1-addr. | 1 | 13 11 25 | 16 16.5 32.5 | 64/256 4/256 69/256 |
| stack (basic)
stack (comp.) | 0
0 | 16 11 28
9 11 21 | 16 11 28
15 11 27 | 64/256 4/256 69/256
84/256 4/256 89/256 |

