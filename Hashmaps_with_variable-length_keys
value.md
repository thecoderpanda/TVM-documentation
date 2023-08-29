1. 3.4. Hashmaps with variable-length keys
value:X = VarHashmapNode (n + 1) X;
nothing$0 {X:Type} = Maybe X;
just$1 {X:Type} value:X = Maybe X;
vhme_empty$0 {n:#} {X:Type} = VarHashmapE n X;
vhme_root$1 {n:#} {X:Type} root:^(VarHashmap n X)
= VarHashmapE n X;
1. 3.4.2. Serialization of prefix codes. One special case of a dictionary with
variable-length keys is that of a prefix code, where the keys cannot be prefixes
of each other. Values in such dictionaries may occur only in the leaves of a
Patricia tree.
The serialization of a prefix code is defined by the following TL-B scheme:
phm_edge#_ {n:#} {X:Type} {l:#} {m:#} label:(HmLabel ~l n)
{n = (~m) + l} node:(PfxHashmapNode m X)
= PfxHashmap n X;
phmn_leaf$0 {n:#} {X:Type} value:X = PfxHashmapNode n X;
phmn_fork$1 {n:#} {X:Type} left:^(PfxHashmap n X)
right:^(PfxHashmap n X) = PfxHashmapNode (n + 1) X;
phme_empty$0 {n:#} {X:Type} = PfxHashmapE n X;
phme_root$1 {n:#} {X:Type} root:^(PfxHashmap n X)
= PfxHashmapE n X;
48

