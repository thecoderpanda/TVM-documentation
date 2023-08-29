1. 5.3. Instruction encoding in codepage zero
bitstring called the opcode of the instruction, followed by, say, 4-bit fields
containing the indices i of stack registers s(i) specified in the instruction, fol-
lowed by all other constant (literal, immediate) parameters included in the
complete instruction. While simple encodings may not be exactly optimal,
they admit short descriptions, and their decoding and encoding can be easily
implemented.
Ifa(generic)instructionusesasimpleencodingwithanl-bitopcode, then
the instruction will utilize 2−l portion of the opcode space. This observation
might be useful for considerations described in 5.2.9 and 5.2.10.
1. 5.2.12. Optimizing code density further: Huffman codes. One might
construct optimally dense binary code for the set of all complete instructions,
provided their probabilities or frequences in real code are known. This is the
well-known Huffman code (for the given probability distribution). However,
such code would be highly unsystematic and hard to decode.
1. 5.2.13. Practical instruction encodings. In practice, instruction encod-
ings used in TVM and other virtual machines offer a compromise between
code density and ease of encoding and decoding. Such a compromise may
be achieved by selecting simple encodings (cf. 5.2.11) for all instructions
(maybe with separate simple encodings for some often used variants, such
as XCHG s0,s(i) among all XCHG s(i),s(j)), and allocating opcode space for
such simple encodings using the heuristics outlined in 5.2.9 and 5.2.10; this
is the approach currently used in TVM.
1. 5.3 Instruction encoding in codepage zero
This section provides details about the experimental instruction encoding
for codepage zero, as described elsewhere in this document (cf. Appendix A)
and used in the preliminary test version of TVM.
1. 5.3.1. Upgradability. First of all, even if this preliminary version some-
how gets into the production version of the TON Blockchain, the codepage
mechanism (cf. 5.1) enables us to introduce better versions later without
compromising backward compatibility.29 So in the meantime, we are free to
experiment.
29Notice that any modifications after launch cannot be done unilaterally; rather they
would require the support of at least two-thirds of validators.
73

