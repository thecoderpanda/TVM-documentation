1. 2.3. Efficiency of stack manipulation primitives
write some data into it; then create B and write some data into it, along
with a reference to previously constructed cell A; finally, add a reference to
B into A. While it may seem that after this sequence of operations we obtain
a cell A, which refers to B, which in turn refers to A, this is not the case.
In fact, we obtain a new cell A(cid:48), which contains a copy of the data originally
stored into cell A along with a reference to cell B, which contains a reference
to (the original) cell A.
In this way the transparent copy-on-write mechanism and the “everything
is a value” paradigm enable us to create new cells using only previously
constructed cells, thus forbidding the appearance of circular references. This
property also applies to all other data structures: for instance, the absence
of circular references enables TVM to use reference counting to immediately
free unused memory instead of relying on garbage collectors. Similarly, this
property is crucial for storing data in the TON Blockchain.
27

