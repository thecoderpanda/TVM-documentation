A.11. Application-specific primitives
• F820—F83F — Reserved for configuration primitives.
A.11.5. Global variable primitives. The“globalvariables” maybehelpful
in implementing some high-level smart-contract languages. They are in fact
stored as components of the Tuple at c7: the k-th global variable simply is
the k-th component of this Tuple, for 1 ≤ k ≤ 254. By convention, the 0-th
component is used for the “configuration parameters” of A.11.4, so it is not
available as a global variable.
• F840 — GETGLOBVAR (k – x), returns the k-th global variable for 0 ≤
k < 255. Equivalent to PUSH c7; SWAP; INDEXVARQ (cf. A.3.2).
• F85_k — GETGLOB k ( – x), returns the k-th global variable for 1 ≤
k ≤ 31. Equivalent to PUSH c7; INDEXQ k.
• F860 — SETGLOBVAR (x k – ), assigns x to the k-th global variable for
0 ≤ k < 255. Equivalent to PUSH c7; ROTREV; SETINDEXVARQ; POP c7.
• F87_k — SETGLOB k (x – ), assigns x to the k-th global variable for
1 ≤ k ≤ 31. Equivalent to PUSH c7; SWAP; SETINDEXQ k; POP c7.
A.11.6. Hashing and cryptography primitives.
• F900 — HASHCU (c – x), computes the representation hash (cf. 3.1.5)
of a Cell c and returns it as a 256-bit unsigned integer x. Useful for
signing and checking signatures of arbitrary entities represented by a
tree of cells.
• F901 — HASHSU (s – x), computes the hash of a Slice s and returns it
as a 256-bit unsigned integer x. The result is the same as if an ordinary
cell containing only data and references from s had been created and
its hash computed by HASHCU.
• F902 — SHA256U (s – x), computes sha256 of the data bits of Slice s.
If the bit length of s is not divisible by eight, throws a cell underflow
exception. The hash value is returned as a 256-bit unsigned integer x.
• F910 — CHKSIGNU (h s k – ?), checks the Ed25519-signature s of a
hash h (a 256-bit unsigned integer, usually computed as the hash of
some data) using public key k (also represented by a 256-bit unsigned
integer). The signature s must be a Slice containing at least 512 data
132

