1. 1.3. Control registers
• Arithmetic primitives — Perform the usual integer arithmetic opera-
tions on values of type Integer.
• Cell (manipulation) primitives — Create new cells and store data in
them (cell creation primitives) or read data from previously created
cells (cell parsing primitives). Because all memory and persistent stor-
ageofTVMconsistsofcells, thesecellmanipulationprimitivesactually
correspond to “memory access instructions” of other architectures. Cell
creation primitives usually work with values of type Builder, while cell
parsing primitives work with Slices.
• Continuation and control flow primitives — Create and modify Con-
tinuations, as well as execute existing Continuations in different ways,
including conditional and repeated execution.
• Custom or application-specific primitives — Efficiently perform spe-
cific high-level actions required by the application (in our case, the
TON Blockchain), such as computing hash functions, performing ellip-
tic curve cryptography, sending new blockchain messages, creating new
smart contracts, and so on. These primitives correspond to standard
library functions rather than microprocessor instructions.
1. 1.3 Control registers
While TVM is a stack machine, some rarely changed values needed in almost
allfunctionsarebetterpassedincertainspecialregisters,andnotnearthetop
of the stack. Otherwise, a prohibitive number of stack reordering operations
would be required to manage all these values.
To this end, the TVM model includes, apart from the stack, up to 16
special control registers, denoted by c0 to c15, or c(0) to c(15). The original
version of TVM makes use of only some of these registers; the rest may be
supported later.
1. 1.3.1. Values kept in control registers. The values kept in control regis-
ters are of the same types as those kept on the stack. However, some control
registers accept only values of specific types, and any attempt to load a value
of a different type will lead to an exception.
1. 1.3.2. List of control registers. The original version of TVM defines and
uses the following control registers:
10

