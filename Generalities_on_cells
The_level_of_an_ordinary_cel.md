1. 3.1. Generalities on cells
The level of an ordinary cell is always equal to the maximum of the levels of
all its children c :
i
Lvl(c) = max Lvl(c ) , (1)
i
1≤i≤r
for an ordinary cell c containing r references to cells c , ..., c . If r = 0,
1 r
Lvl(c) = 0. Exotic cells may have different rules for setting their level.
A cell’s level affects the number of higher hashes it has. More precisely,
a level l cell has l higher hashes Hash (c), ..., Hash (c) in addition to its
1 l
representation hash Hash(c) = Hash (c). Cells of non-zero level appear
∞
inside Merkle proofs and Merkle updates, after some branches of the tree of
cells representing a value of an abstract data type are pruned.
1. 3.1.4. Standard cell representation. When a cell needs to be transferred
by a network protocol or stored in a disk file, it must be serialized. The
standard representation CellRepr(c) = CellRepr (c) of a cell c as an
∞
octet (byte) sequence is constructed as follows:
1. 1. Two descriptor bytes d and d are serialized first. Byte d equals
1 2 1
r+8s+32l, where 0 ≤ r ≤ 4 is the quantity of cell references contained
in the cell, 0 ≤ l ≤ 3 is the level of the cell, and 0 ≤ s ≤ 1 is 1 for
exotic cells and 0 for ordinary cells. Byte d equals (cid:98)b/8(cid:99)+(cid:100)b/8(cid:101), where
2
0 ≤ b ≤ 1023 is the quantity of data bits in c.
1. 2. Thenthedatabitsareserializedas(cid:100)b/8(cid:101)8-bitoctets(bytes). Ifbisnot
a multiple of eight, a binary 1 and up to six binary 0s are appended to
the data bits. After that, the data is split into (cid:100)b/8(cid:101) eight-bit groups,
andeachgroupisinterpretedasanunsignedbig-endianinteger0...255
and stored into an octet.
1. 3. Finally, each of the r cell references is represented by 32 bytes contain-
ingthe256-bitrepresentation hash Hash(c ), explainedbelowin3.1.5,
i
of the cell c referred to.
i
In this way, 2+(cid:100)b/8(cid:101)+32r bytes of CellRepr(c) are obtained.
1. 3.1.5. The representation hash of a cell. The 256-bit representation
hash or simply hash Hash(c) of a cell c is recursively defined as the sha256
of the standard representation of the cell c:
Hash(c) := sha256(cid:0)CellRepr(c)(cid:1) (2)
29

