1. 3.4. Hashmaps with variable-length keys
1. 3.3.11. Taxonomy of dictionary primitives. The dictionary primitives,
described in detail in A.10, can be classified according to the following cat-
egories:
• Which dictionary operation (cf. 3.3.10) do they perform?
• Are they specialized for the case X = ˆY? If so, do they represent val-
ues of type Y by Cells or by Slices? (Generic versions always represent
values of type X as Slices.)
• Are the dictionaries themselves passed and returned as Cells or as
Slices? (Most primitives represent dictionaries as Slices.)
• Is the key length n fixed inside the primitive, or is it passed in the
stack?
• Are the keys represented by Slices, or by signed or unsigned Integers?
In addition, TVM includes special serialization/deserialization primitives,
such as STDICT, LDDICT, and PLDDICT. They can be used to extract a dictio-
nary from a serialization of an encompassing object, or to insert a dictionary
into such a serialization.
1. 3.4 Hashmaps with variable-length keys
TVM provides some support for dictionaries, or hashmaps, with variable-
length keys, in addition to its support for dictionaries with fixed-length keys
(as described in 3.3 above).
1. 3.4.1. Serialization of dictionaries with variable-length keys. The
serialization of a VarHashmap into a tree of cells (or, more generally, into a
Slice) is defined by a TL-B scheme, similar to that described in 3.3.3:
vhm_edge#_ {n:#} {X:Type} {l:#} {m:#} label:(HmLabel ~l n)
{n = (~m) + l} node:(VarHashmapNode m X)
= VarHashmap n X;
vhmn_leaf$00 {n:#} {X:Type} value:X = VarHashmapNode n X;
vhmn_fork$01 {n:#} {X:Type} left:^(VarHashmap n X)
right:^(VarHashmap n X) value:(Maybe X)
= VarHashmapNode (n + 1) X;
vhmn_cont$1 {n:#} {X:Type} branch:bit child:^(VarHashmap n X)
47

