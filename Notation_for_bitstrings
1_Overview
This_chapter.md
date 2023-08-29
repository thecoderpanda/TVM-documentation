1. 1.0. Notation for bitstrings
1 Overview
This chapter provides an overview of the main features and design principles
of TVM. More detail on each topic is provided in subsequent chapters.
1. 1.0 Notation for bitstrings
Thefollowingnotationisusedforbitstrings(orbitstrings)—i.e.,finitestrings
consisting of binary digits (bits), 0 and 1—throughout this document.
1. 1.0.1. Hexadecimal notation for bitstrings. When the length of a bit-
string is a multiple of four, we subdivide it into groups of four bits and
represent each group by one of sixteen hexadecimal digits 0–9, A–F in the
usual manner: 0 ↔ 0000, 1 ↔ 0001, ..., F ↔ 1111. The resulting
16 16 16
hexadecimal string is our equivalent representation for the original binary
string.
1. 1.0.2. Bitstrings of lengths not divisible by four. If the length of a
binary string is not divisible by four, we augment it by one 1 and several
(maybe zero) 0s at the end, so that its length becomes divisible by four, and
then transform it into a string of hexadecimal digits as described above. To
indicate that such a transformation has taken place, a special “completion
tag” _ is added to the end of the hexadecimal string. The reverse transforma-
tion (applied if the completion tag is present) consists in first replacing each
hexadecimal digit by four corresponding bits, and then removing all trailing
zeroes (if any) and the last 1 immediately preceding them (if the resulting
bitstring is non-empty at this point).
Notice that there are several admissible hexadecimal representations for
the same bitstring. Among them, the shortest one is “canonical”. It can be
deterministically obtained by the above procedure.
For example, 8A corresponds to binary string 10001010, while 8A_ and
8A0_ both correspond to 100010. An empty bitstring may be represented by
either ‘’, ‘8_’, ‘0_’, ‘_’, or ‘00_’.
1. 1.0.3. Emphasizing that a string is a hexadecimal representation of
a bitstring. Sometimes we need to emphasize that a string of hexadecimal
digits (with or without a _ at the end) is the hexadecimal representation of
a bitstring. In such cases, we either prepend x to the resulting string (e.g.,
x8A), or prepend x{ and append } (e.g., x{2D9_}, which is 00101101100).
5

