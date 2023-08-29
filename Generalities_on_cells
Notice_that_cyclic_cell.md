1. 3.1. Generalities on cells
Notice that cyclic cell references are not allowed and cannot be created by
means of the TVM (cf. 2.3.5), so this recursion always ends, and the repre-
sentation hash of any cell is well-defined.
1. 3.1.6. The higher hashes of a cell. Recall that a cell c of level l has l
higher hashes Hash (c), 1 ≤ i ≤ l, as well. Exotic cells have their own rules
i
for computing their higher hashes. Higher hashes Hash (c) of an ordinary
i
cell c are computed similarly to its representation hash, but using the higher
hashes Hash (c ) of its children c instead of their representation hashes
i j j
Hash(c ). By convention, we set Hash (c) := Hash(c), and Hash (c) :=
j ∞ i
Hash (c) = Hash(c) for all i > l.12
∞
1. 3.1.7. Types of exotic cells. TVM currently supports the following cell
types:
• Type −1: Ordinary cell — Contains up to 1023 bits of data and up to
four cell references.
• Type 1: Pruned branch cell c — May have any level 1 ≤ l ≤ 3. It
contains exactly 8 + 256l data bits: first an 8-bit integer equal to 1
(representing the cell’s type), then its l higher hashes Hash (c), ...,
1
Hash (c). The level l of a pruned branch cell may be called its de
l
Brujn index, because it determines the outer Merkle proof or Merkle
update during the construction of which the branch has been pruned.
An attempt to load a pruned branch cell usually leads to an exception.
• Type2: Library reference cell—Alwayshaslevel0,andcontains8+256
data bits, including its 8-bit type integer 2 and the representation hash
Hash(c(cid:48)) of the library cell being referred to. When loaded, a library
reference cell may be transparently replaced by the cell it refers to, if
found in the current library context.
• Type 3: Merkle proof cell c — Has exactly one reference c and level
1
0 ≤ l ≤ 3, which must be one less than the level of its only child c :
1
Lvl(c) = max(Lvl(c )−1,0) (3)
1
12From a theoretical perspective, we might say that a cell c has an infinite sequence
of hashes (cid:0)Hash (c)(cid:1) , which eventually stabilizes: Hash (c) → Hash (c). Then the
i i≥1 i ∞
level l is simply the largest index i, such that Hash (c)(cid:54)=Hash (c).
i ∞
30

