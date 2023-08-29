1. 3.2. Data manipulation instructions and cells
• Quiet versions of serialization instructions do not throw exceptions;
instead, they push -1 on top of the resulting Builder upon success, or
return the original Builder with 0 on top of it to indicate failure.
Integer serialization instructions have mnemonics like STU 20 (“store an
unsigned 20-bit integer value”) or STIXQ (“quietly store an integer value of
variable length provided in the stack”). The full list of these instructions—
including their mnemonics, descriptions, and opcodes—is provided in A.7.1.
1. 3.2.8. Integers in cells are big-endian by default. Notice that the
default order of bits in Integers serialized into Cells is big-endian, not little-
endian.14 In this respect TVM is a big-endian machine. However, this affects
only the serialization of integers inside cells. The internal representation of
the Integer value type is implementation-dependent and irrelevant for the
operation of TVM. Besides, there are some special primitives such as STULE
for(de)serializinglittle-endianintegers, whichmustbestoredintoanintegral
number of bytes (otherwise “little-endianness” does not make sense, unless
oneisalsowillingtoreverttheorderofbitsinsideoctets). Suchprimitivesare
useful for interfacing with the little-endian world—for instance, for parsing
custom-format messages arriving to a TON Blockchain smart contract from
the outside world.
1. 3.2.9. Other serialization primitives. Other cell creation primitives seri-
alizebitstrings(i.e., cellsliceswithoutreferences), eithertakenfromthestack
or supplied as literal arguments; cell slices (which are concatenated to the
cell builder in an obvious way); other Builders (which are also concatenated);
and cell references (STREF).
1. 3.2.10. Other cell creation primitives. In addition to the cell serial-
ization primitives for certain built-in value types described above, there are
simple primitives that create a new empty Builder and push it into the stack
(NEWC), or transform a Builder into a Cell (ENDC), thus finishing the cell
creation process. An ENDC can be combined with a STREF into a single in-
struction ENDCST, which finishes the creation of a cell and immediately stores
a reference to it in an “outer” Builder. There are also primitives that obtain
the quantity of data bits or references already stored in a Builder, and check
how many data bits or references can be stored.
14Negative numbers are represented using two’s complement. For instance, integer −17
is serialized by instruction STI 8 into bitstring xEF.
35

