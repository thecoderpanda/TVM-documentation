C.2. Comparison of machine code for sample leaf function
SUB // D Dx Dy
XCPU s1,s2 // D Dy Dx D
IDIV // D Dy x
XCHG s2 // x Dy D
IDIV // x y
RET
It is interesting to note that this version of stack machine code contains only
9 stack manipulation primitives for 11 arithmetic operations. It is not clear,
however, whether an optimizing compiler would be able to reorganize the
code in such a manner by itself.
C.2 Comparison of machine code for sample leaf func-
tion
Table1summarizesthepropertiesofmachinecodecorrespondingtothesame
source file described in C.1.1, generated for a hypothetical three-address
register machine (cf. C.1.2), with both “optimistic” and “realistic” instruc-
tion encodings; a two-address machine (cf. C.1.3); a one-address machine
(cf. C.1.4); and a stack machine, similar to TVM, using either only the
basic stack manipulation primitives (cf. C.1.5) or both the basic and the
composite stack primitives (cf. C.1.7).
The meaning of the columns in Table 1 is as follows:
• “Operations” — The quantity of instructions used, split into “data”
(i.e., registermoveandexchangeinstructionsforregistermachines, and
stack manipulation instructions for stack machines) and “arithmetic”
(instructions for adding, subtracting, multiplying and dividing integer
numbers). The “total” is one more than the sum of these two, because
there is also a one-byte RET instruction at the end of machine code.
• “Code bytes” — The total amount of code bytes used.
• “Opcode space” — The portion of “opcode space” (i.e., of possible
choices for the first byte of the encoding of an instruction) used by
data and arithmetic instructions in the assumed instruction encoding.
For example, the “optimistic” encoding for the three-address machine
assumes two-byte encodings for all arithmetic instructions op r(i),
r(j), r(k). Each arithmetic instruction would then consume portion
154

