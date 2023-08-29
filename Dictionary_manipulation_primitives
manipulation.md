A.10. Dictionary manipulation primitives
manipulation primitives is provided in 3.3.11. Here we use the concepts and
notation introduced in those sections.
Dictionaries admit two different representations as TVM stack values:
• A Slice s with a serialization of a TL-B value of type HashmapE(n,X).
In other words, s consists either of one bit equal to zero (if the dic-
tionary is empty), or of one bit equal to one and a reference to a Cell
containing the root of the binary tree, i.e., a serialized value of type
Hashmap(n,X).
• A “maybe Cell” c?, i.e., a value that is either a Cell (containing a seri-
alized value of type Hashmap(n,X) as before) or a Null (corresponding
to an empty dictionary). When a “maybe Cell” c? is used to represent
a dictionary, we usually denote it by D in the stack notation.
Most of the dictionary primitives listed below accept and return dictionar-
ies in the second form, which is more convenient for stack manipulation.
However, serialized dictionaries inside larger TL-B objects use the first rep-
resentation.
Opcodes starting with F4 and F5 are reserved for dictionary operations.
A.10.1. Dictionary creation.
• 6D — NEWDICT ( – D), returns a new empty dictionary. It is an alter-
native mnemonics for PUSHNULL, cf. A.3.1.
• 6E — DICTEMPTY (D – ?), checks whether dictionary D is empty, and
returns −1 or 0 accordingly. It is an alternative mnemonics for ISNULL,
cf. A.3.1.
A.10.2. Dictionary serialization and deserialization.
• CE — STDICTS (s b – b(cid:48)), stores a Slice-represented dictionary s into
Builder b. It is actually a synonym for STSLICE.
• F400—STDICTorSTOPTREF(D b–b(cid:48)), storesdictionaryD intoBuilder
b, returing the resulting Builder b(cid:48). In other words, if D is a cell,
performs STONE and STREF; if D is Null, performs NIP and STZERO;
otherwise throws a type checking exception.
• F401 — SKIPDICT or SKIPOPTREF (s – s(cid:48)), equivalent to LDDICT; NIP.
116

