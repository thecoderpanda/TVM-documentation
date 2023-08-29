C.4. Comparison of machine code for sample non-leaf function
Operations Code bytes Opcode space
Machine m data cont. total data cont. total data arith total
0,8 29 12 41 42 34 76
3-addr. 35/256 34/256 72/256
16 27 12 39 44 34 78
0,8 29 12 41 42 34 76
2-addr. 37/256 4/256 44/256
16 27 12 39 44 34 78
0,8 33 12 45 33 34 67
1-addr. 97/256 64/256 164/256
16 28 12 40 39 34 73
stack (basic) − 18 11 29 18 33 51 64/256 4/256 71/256
stack (comp.) − 9 11 20 15 33 48 84/256 4/256 91/256
Table 5: A summary of machine code properties for hypothetical 3-address, 2-address,
1-address, and stack machines, generated for a sample non-leaf function (cf. C.3.1),
assuming m of the 16 registers must be preserved by called subroutines.
C.4 Comparison of machine code for sample non-leaf
function
Table 5 summarizes the properties of machine code corresponding to the
same source file provided in C.3.1. We consider only the “realistically”
encoded three-address machines. Three-address and two-address machines
have the same code density properties, but differ in the utilization of opcode
space. The one-address machine, somewhat surprisingly, managed to pro-
duced shorter code than the two-address and three-address machines, at the
expense of using up more than half of all opcode space. The stack machine
is the obvious winner in this code density contest, without compromizing its
excellent extendability (measured in opcode space used for arithmetic and
other data transformation instructions).
C.4.1. Combining with results for leaf functions. It is instructive
to compare this table with the results in C.2 for a sample leaf function,
summarized in Table 1 (for m = 0 preserved registers) and the very similar
Table 3 (for m = 8 preserved registers), and, if one is still interested in case
m = 16 (which turned out to be worse than m = 8 in almost all situations),
also to Table 2.
We see that the stack machine beats all register machines on non-leaf
functions. As for the leaf functions, only the three-address machine with the
“optimistic” encoding of arithmetic instructions was able to beat the stack
machine, winning by 15%, by compromising its extendability. However, the
same three-address machine produces 25% longer code for non-leaf functions.
170

| Machine | m | Operations
data cont. total | Code bytes
data cont. total | Opcode space
data arith total |
| 3-addr. | 0,8
16 | 29 12 41
27 12 39 | 42 34 76
44 34 78 | 35/256 34/256 72/256 |
| 2-addr. | 0,8
16 | 29 12 41
27 12 39 | 42 34 76
44 34 78 | 37/256 4/256 44/256 |
| 1-addr. | 0,8
16 | 33 12 45
28 12 40 | 33 34 67
39 34 73 | 97/256 64/256 164/256 |
| stack (basic)
stack (comp.) | −
− | 18 11 29
9 11 20 | 18 33 51
15 33 48 | 64/256 4/256 71/256
84/256 4/256 91/256 |

