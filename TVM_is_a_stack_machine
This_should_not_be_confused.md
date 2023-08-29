1. 1.1. TVM is a stack machine
This should not be confused with hexadecimal numbers, usually prepended
by 0x (e.g., 0x2D9 or 0x2d9, which is the integer 729).
1. 1.0.4. Serializing a bitstring into a sequence of octets. When a bit-
string needs to be represented as a sequence of 8-bit bytes (octets), which
take values in integers 0...255, this is achieved essentially in the same fash-
ion as above: we split the bitstring into groups of eight bits and interpret
each group as the binary representation of an integer 0...255. If the length
of the bitstring is not a multiple of eight, the bitstring is augmented by a
binary 1 and up to seven binary 0s before being split into groups. The fact
that such a completion has been applied is usually reflected by a “completion
tag” bit.
For instance, 00101101100 corresponds to the sequence of two octets
(0x2d,0x90) (hexadecimal), or (45,144) (decimal), along with a completion
tag bit equal to 1 (meaning that the completion has been applied), which
must be stored separately.
In some cases, it is more convenient to assume the completion is enabled
by default rather than store an additional completion tag bit separately.
Under such conventions, 8n-bit strings are represented by n+1 octets, with
the last octet always equal to 0x80 = 128.
1. 1.1 TVM is a stack machine
First of all, TVM is a stack machine. This means that, instead of keeping
values in some “variables” or “general-purpose registers”, they are kept in a
(LIFO) stack, at least from the “low-level” (TVM) perspective.3
Most operations and user-defined functions take their arguments from the
top of the stack, and replace them with their result. For example, the inte-
ger addition primitive (built-in operation) ADD does not take any arguments
describing which registers or immediate values should be added together and
where the result should be stored. Instead, the two top values are taken from
the stack, they are added together, and their sum is pushed into the stack in
their place.
3A high-level smart-contract language might create a visibility of variables for the
ease of programming; however, the high-level source code working with variables will be
translated into TVM machine code keeping all the values of these variables in the TVM
stack.
6

