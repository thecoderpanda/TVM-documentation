A.4. Constant, or literal primitives
• 83xx — PUSHPOW2 xx+1, (quietly) pushes 2xx+1 for 0 ≤ xx ≤ 255.
• 83FF — PUSHNAN, pushes a NaN.
• 84xx — PUSHPOW2DEC xx+1, pushes 2xx+1 −1 for 0 ≤ xx ≤ 255.
• 85xx — PUSHNEGPOW2 xx+1, pushes −2xx+1 for 0 ≤ xx ≤ 255.
• 86, 87 — reserved for integer constants.
A.4.2. Constant slices, continuations, cells, and references. Most
of the instructions listed below push literal slices, continuations, cells, and
cell references, stored as immediate arguments to the instruction. Therefore,
if the immediate argument is absent or too short, an “invalid or too short
opcode” exception (code 6) is thrown.
• 88 — PUSHREF, pushes the first reference of cc.code into the stack as
a Cell (and removes this reference from the current continuation).
• 89 — PUSHREFSLICE, similar to PUSHREF, but converts the cell into a
Slice.
• 8A — PUSHREFCONT, similar to PUSHREFSLICE, but makes a simple or-
dinary Continuation out of the cell.
• 8Bxsss—PUSHSLICE sss, pushesthe(prefix)subsliceofcc.codecon-
sisting of its first 8x+4 bits and no references (i.e., essentially a bit-
string), where 0 ≤ x ≤ 15. A completion tag is assumed, meaning that
all trailing zeroes and the last binary one (if present) are removed from
this bitstring. If the original bitstring consists only of zeroes, an empty
slice will be pushed.
• 8B08 — PUSHSLICE x8_, pushes an empty slice (bitstring ‘’).
• 8B04 — PUSHSLICE x4_, pushes bitstring ‘0’.
• 8B0C — PUSHSLICE xC_, pushes bitstring ‘1’.
• 8Crxxssss—PUSHSLICE ssss, pushesthe(prefix)subsliceofcc.code
consisting of its first 1 ≤ r +1 ≤ 4 references and up to first 8xx+1
bits of data, with 0 ≤ xx ≤ 31. A completion tag is also assumed.
87

