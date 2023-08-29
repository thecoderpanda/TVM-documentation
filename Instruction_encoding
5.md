1. 5.2. Instruction encoding
1. 5.2.4. Special case: end-of-code padding. As an exception to the above
rule, some codepages may accept some values of cc.code that are too short
tobevalidinstructionencodingsasadditionalvariantsofNOP,thuseffectively
using the same procedure for them as for an empty cc.code. Such bitstrings
may be used for padding the code near its end.
For example, if binary string 00000000 (i.e., x00, cf. 1.0.3) is used in a
codepage to encode NOP, its proper prefixes cannot encode any instructions.
So this codepage may accept 0, 00, 000, ..., 0000000 as variants of NOP if
this is all that is left in cc.code, instead of generating an invalid opcode
exception.
Such a padding may be useful, for example, if the PUSHCONT primitive
(cf. 4.2.3) creates only continuations with code consisting of an integral
number of bytes, but not all instructions are encoded by an integral number
of bytes.
1. 5.2.5. TVM code is a bitcode, not a bytecode. Recall that TVM is
a bit-oriented machine in the sense that its Cells (and Slices) are naturally
considered as sequences of bits, not just of octets (bytes), cf. 3.2.5. Because
the TVM code is also kept in cells (cf. 3.1.9 and 4.1.4), there is no reason
to use only bitstrings of length divisible by eight as encodings of complete
instructions. In other words, generally speaking, the TVM code is a bitcode,
not a bytecode.
That said, some codepages (such as our experimental codepage zero) may
opt to use a bytecode (i.e., to use only encodings consisting of an integral
number of bytes)—either for simplicity, or for the ease of debugging and of
studying memory (i.e., cell) dumps.27
1. 5.2.6. Opcode space used by a complete instruction. Recall from cod-
ing theory that the lengths of bitstrings l used in a binary prefix code satisfy
i
Kraft–McMillan inequality (cid:80) 2−li ≤ 1. This is applicable in particular to
i
the (complete) instruction encoding used by a TVM codepage. We say that
a particular complete instruction (or, more precisely, the encoding of a com-
plete instruction) utilizes the portion 2−l of the opcode space, if it is encoded
by an l-bit string. One can see that all complete instructions together utilize
at most 1 (i.e., “at most the whole opcode space”).
27If the cell dumps are hexadecimal, encodings consisting of an integral number of
hexadecimal digits (i.e., having length divisible by four bits) might be equally convenient.
71

