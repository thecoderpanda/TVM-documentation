1. 1.1. TVM is a stack machine
1. 1.1.1. TVM values. The entities that can be stored in the TVM stack
will be called TVM values, or simply values for brevity. They belong to
one of several predefined value types. Each value belongs to exactly one
value type. The values are always kept on the stack along with tags uniquely
determining their types, and all built-in TVM operations (or primitives) only
accept values of predefined types.
For example, the integer addition primitive ADD accepts only two integer
values, and returns one integer value as a result. One cannot supply ADD with
two strings instead of two integers expecting it to concatenate these strings
or to implicitly transform the strings into their decimal integer values; any
attempt to do so will result in a run-time type-checking exception.
1. 1.1.2. Static typing, dynamic typing, and run-time type checking.
InsomerespectsTVMperformsakindofdynamictypingusingrun-timetype
checking. However, this does not make the TVM code a “dynamically typed
language” like PHP or Javascript, because all primitives accept values and
return results of predefined (value) types, each value belongs to strictly one
type, and values are never implicitly converted from one type to another.
If, on the other hand, one compares the TVM code to the conventional
microprocessor machine code, one sees that the TVM mechanism of value
tagging prevents, for example, using the address of a string as a number—
or, potentially even more disastrously, using a number as the address of
a string—thus eliminating the possibility of all sorts of bugs and security
vulnerabilities related to invalid memory accesses, usually leading to memory
corruption and segmentation faults. This property is highly desirable for
a VM used to execute smart contracts in a blockchain. In this respect,
TVM’s insistence on tagging all values with their appropriate types, instead
of reinterpreting the bit sequence in a register depending on the needs of the
operation it is used in, is just an additional run-time type-safety mechanism.
An alternative would be to somehow analyze the smart-contract code for
type correctness and type safety before allowing its execution in the VM,
or even before allowing it to be uploaded into the blockchain as the code
of a smart contract. Such a static analysis of code for a Turing-complete
machine appears to be a time-consuming and non-trivial problem (likely to
be equivalent to the stopping problem for Turing machines), something we
would rather avoid in a blockchain smart-contract context.
One should bear in mind that one always can implement compilers from
statically typed high-level smart-contract languages into the TVM code (and
7

