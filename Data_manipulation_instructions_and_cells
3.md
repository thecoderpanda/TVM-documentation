1. 3.2. Data manipulation instructions and cells
1. 3.2.3. Builder and Slice values exist only as stack values. Notice that
Builder andSlice objectsappearonlyasvaluesinaTVMstack. Theycannot
be stored in “memory” (i.e., trees of cells) or “persistent storage” (which is
also a bag of cells). In this sense, there are far more Cell objects than Builder
orSlice objectsinaTVMenvironment, but, somewhatparadoxically, aTVM
program sees Builder and Slice objects in its stack more often than Cells. In
fact, a TVM program does not have much use for Cell values, because they
are immutable and opaque; all cell manipulation primitives require that a
Cell value be transformed into either a Builder or a Slice first, before it can
be modified or inspected.
1. 3.2.4. TVM has no separate Bitstring value type. Notice that TVM
offers no separate bitstring value type. Instead, bitstrings are represented by
Slices that happen to have no references at all, but can still contain up to
1023 data bits.
1. 3.2.5. Cells and cell primitives are bit-oriented, not byte-oriented.
An important point is that TVM regards data kept in cells as sequences
(strings, streams) of (up to 1023) bits, not of bytes. In other words, TVM
is a bit-oriented machine, not a byte-oriented machine. If necessary, an ap-
plication is free to use, say, 21-bit integer fields inside records serialized into
TVM cells, thus using fewer persistent storage bytes to represent the same
data.
1. 3.2.6. Taxonomy of cell creation (serialization) primitives. Cell cre-
ation primitives usually accept a Builder argument and an argument rep-
resenting the value to be serialized. Additional arguments controlling some
aspects of the serialization process (e.g., how many bits should be used for
serialization) can be also provided, either in the stack or as an immediate
value inside the instruction. The result of a cell creation primitive is usually
another Builder, representing the concatenation of the original builder and
the serialization of the value provided.
Therefore, one can suggest a classification of cell serialization primitives
according to the answers to the following questions:
• Which is the type of values being serialized?
• How many bits are used for serialization? If this is a variable number,
does it come from the stack, or from the instruction itself?
33

