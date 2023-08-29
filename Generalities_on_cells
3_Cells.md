1. 3.1. Generalities on cells
3 Cells, memory, and persistent storage
ThischapterbrieflydescribesTVMcells, usedtorepresentalldatastructures
inside the TVM memory and its persistent storage, and the basic operations
used to create cells, write (or serialize) data into them, and read (or deseri-
alize) data from them.
1. 3.1 Generalities on cells
This section presents a classification and general descriptions of cell types.
1. 3.1.1. TVM memory and persistent storage consist of cells. Recall
that the TVM memory and persistent storage consist of (TVM) cells. Each
cell contains up to 1023 bits of data and up to four references to other cells.11
Circular references are forbidden and cannot be created by means of TVM
(cf. 2.3.5). In this way, all cells kept in TVM memory and persistent storage
constitute a directed acyclic graph (DAG).
1. 3.1.2. Ordinary and exotic cells. Apart from the data and references,
a cell has a cell type, encoded by an integer −1...255. A cell of type −1
is called ordinary; such cells do not require any special processing. Cells of
other types are called exotic, and may be loaded—automatically replaced by
other cells when an attempt to deserialize them (i.e., to convert them into
a Slice by a CTOS instruction) is made. They may also exhibit a non-trivial
behavior when their hashes are computed.
The most common use for exotic cells is to represent some other cells—for
instance, cells present in an external library, or pruned from the original tree
of cells when a Merkle proof has been created.
The type of an exotic cell is stored as the first eight bits of its data. If an
exotic cell has less than eight data bits, it is invalid.
1. 3.1.3. The level of a cell. Every cell c has another attribute Lvl(c) called
its (de Brujn) level, which currently takes integer values in the range 0...3.
11From the perspective of low-level cell operations, these data bits and cell references
are not intermixed. In other words, an (ordinary) cell essentially is a couple consisting of
a list of up to 1023 bits and of a list of up to four cell references, without prescribing an
order in which the references and the data bits should be deserialized, even though TL-B
schemes appear to suggest such an order.
28

