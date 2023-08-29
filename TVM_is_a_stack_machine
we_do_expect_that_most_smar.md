1. 1.1. TVM is a stack machine
we do expect that most smart contracts for TON will be written in such lan-
guages), just as one can compile statically typed languages into conventional
machine code (e.g., x86 architecture). If the compiler works correctly, the
resulting machine code will never generate any run-time type-checking ex-
ceptions. All type tags attached to values processed by TVM will always
have expected values and may be safely ignored during the analysis of the
resulting TVM code, apart from the fact that the run-time generation and
verification of these type tags by TVM will slightly slow down the execution
of the TVM code.
1. 1.1.3. Preliminary list of value types. A preliminary list of value types
supported by TVM is as follows:
• Integer — Signed 257-bit integers, representing integer numbers in the
range −2256...2256 −1, as well as a special “not-a-number” value NaN.
• Cell — A TVM cell consists of at most 1023 bits of data, and of at
most four references to other cells. All persistent data (including TVM
code) in the TON Blockchain is represented as a collection of TVM
cells (cf. [1, 2.5.14]).
• Tuple — An ordered collection of up to 255 components, having ar-
bitrary value types, possibly distinct. May be used to represent non-
persistent values of arbitrary algebraic data types.
• Null — A type with exactly one value ⊥, used for representing empty
lists, empty branches of binary trees, absence of return value in some
situations, and so on.
• Slice — A TVM cell slice, or slice for short, is a contiguous “sub-cell”
of an existing cell, containing some of its bits of data and some of its
references. Essentially, a slice is a read-only view for a subcell of a cell.
Slices are used for unpacking data previously stored (or serialized) in a
cell or a tree of cells.
• Builder — A TVM cell builder, or builder for short, is an “incomplete”
cell that supports fast operations of appending bitstrings and cell ref-
erences at its end. Builders are used for packing (or serializing) data
from the top of the stack into new cells (e.g., before transferring them
to persistent storage).
8

