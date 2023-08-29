1. 5.3. Instruction encoding in codepage zero
1. 5.3.2. Choice of instructions. We opted to include many “experimental”
and not strictly necessary instructions in codepage zero just to see how they
might be used in real code. For example, we have both the basic (cf. 2.2.1)
and the compound (cf. 2.2.3) stack manipulation primitives, as well as some
“unsystematic” ones such as ROT (mostly borrowed from Forth). If such
primitives are rarely used, their inclusion just wastes some part of the opcode
space and makes the encodings of other instructions slightly less effective,
something we can afford at this stage of TVM’s development.
1. 5.3.3. Using experimental instructions. Some of these experimental
instructions have been assigned quite long opcodes, just to fit more of them
into the opcode space. One should not be afraid to use them just because
they are long; if these instructions turn out to be useful, they will receive
shorter opcodes in future revisions. Codepage zero is not meant to be fine-
tuned in this respect.
1. 5.3.4. Choice of bytecode. We opted to use a bytecode (i.e., to use encod-
ings of complete instructions of lengths divisible by eight). While this may
not produce optimal code density, because such a length restriction makes
it more difficult to match portions of opcode space used for the encoding of
instructions with estimated frequencies of these instructions in TVM code
(cf. 5.2.11 and 5.2.9), such an approach has its advantages: it admits a
simpler instruction decoder and simplifies debugging (cf. 5.2.5).
After all, we do not have enough data on the relative frequencies of dif-
ferent instructions right now, so our code density optimizations are likely to
be very approximate at this stage. The ease of debugging and experimenting
and the simplicity of implementation are more important at this point.
1. 5.3.5. Simple encodings for all instructions. For similar reasons, we
opted to use simple encodings for all instructions (cf. 5.2.11 and 5.2.13),
with separate simple encodings for some very frequently used subcases as
outlined in 5.2.13. That said, we tried to distribute opcode space using the
heuristics described in 5.2.9 and 5.2.10.
1. 5.3.6. Lack of context-dependent encodings. This version of TVM also
does not use context-dependent encodings (cf. 5.1.6). They may be added
at a later stage, if deemed useful.
1. 5.3.7. The list of all instructions. The list of all instructions available in
74

