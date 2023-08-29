1. 3.1. Generalities on cells
The 8 + 256 data bits of a Merkle proof cell contain its 8-bit type
integer 3, followed by Hash (c ) (assumed to be equal to Hash(c ) if
1 1 1
Lvl(c ) = 0). The higher hashes Hash (c) of c are computed similarly
1 i
to the higher hashes of an ordinary cell, but with Hash (c ) used
i+1 1
instead of Hash (c ). When loaded, a Merkle proof cell is replaced by
i 1
c .
1
• Type 4: Merkle update cell c — Has two children c and c . Its level
1 2
0 ≤ l ≤ 3 is given by
Lvl(c) = max(Lvl(c )−1,Lvl(c )−1,0) (4)
1 2
A Merkle update behaves like a Merkle proof for both c and c , and
1 2
contains 8+256+256 data bits with Hash (c ) and Hash (c ). How-
1 1 1 2
ever, an extra requirement is that all pruned branch cells c(cid:48) that are
descendants of c and are bound by c must also be descendants of c .13
2 1
When a Merkle update cell is loaded, it is replaced by c .
2
1. 3.1.8. All values of algebraic data types are trees of cells. Arbitrary
values of arbitrary algebraic data types (e.g., all types used in functional
programming languages) can be serialized into trees of cells (of level 0), and
such representations are used for representing such values within TVM. The
copy-on-write mechanism (cf. 2.3.2) allows TVM to identify cells containing
the same data and references, and to keep only one copy of such cells. This
actually transforms a tree of cells into a directed acyclic graph (with the
additional property that all its vertices be accessible from a marked vertex
called the “root”). However, this is a storage optimization rather than an
essentialpropertyofTVM.FromtheperspectiveofaTVMcodeprogrammer,
one should think of TVM data structures as trees of cells.
1. 3.1.9. TVM code is a tree of cells. The TVM code itself is also rep-
resented by a tree of cells. Indeed, TVM code is simply a value of some
complex algebraic data type, and as such, it can be serialized into a tree of
cells.
The exact way in which the TVM code (e.g., TVM assembly code) is
transformed into a tree of cells is explained later (cf. 4.1.4 and 5.2), in sec-
tions discussing control flow instructions, continuations, and TVM instruc-
tion encoding.
13Aprunedbranchcellc(cid:48) oflevell isbound byaMerkle(prooforupdate)cellcifthere
are exactly l Merkle cells on the path from c to its descendant c(cid:48), including c.
31

