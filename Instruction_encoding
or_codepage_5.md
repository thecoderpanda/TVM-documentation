1. 5.2. Instruction encoding
or codepage 5. Clearly, we have now described a status flag, affecting the
execution of some instructions in a certain new manner.
1. 5.1.8. Setting the codepage in the code itself. For convenience, we
reserve some opcode in all codepages—say, FF n—for the instruction SETCP
n, with n from 0 to 255 (cf. A.13). Then by inserting such an instruction
into the very beginning of (the main function of) a program (e.g., a TON
Blockchain smart contract) or a library function, we can ensure that the code
will always be executed in the intended codepage.
1. 5.2 Instruction encoding
This section discusses the general principles of instruction encoding valid for
all codepages and all versions of TVM. Later, 5.3 discusses the choices made
for the experimental “codepage zero”.
1. 5.2.1. Instructions are encoded by a binary prefix code. All com-
plete instructions (i.e., instructions along with all their parameters, such as
the names of stack registers s(i) or other embedded constants) of a TVM
codepage are encoded by a binary prefix code. This means that a (finite)
binary string (i.e., a bitstring) corresponds to each complete instruction, in
such a way that binary strings corresponding to different complete instruc-
tions do not coincide, and no binary string among the chosen subset is a
prefix of another binary string from this subset.
1. 5.2.2. Determining the first instruction from a code stream. As a
consequence of this encoding method, any binary string admits at most one
prefix, which is an encoding of some complete instruction. In particular,
the code cc.code of the current continuation (which is a Slice, and thus a
bitstring along with some cell references) admits at most one such prefix,
which corresponds to the (uniquely determined) instruction that TVM will
execute first. After execution, this prefix is removed from the code of the
current continuation, and the next instruction can be decoded.
1. 5.2.3. Invalid opcode. If no prefix of cc.code encodes a valid instruction
in the current codepage, an invalid opcode exception is generated (cf. 4.5.7).
However, the case of an empty cc.code is treated separately as explained
in 4.1.4 (the exact behavior may depend on the current codepage).
70

