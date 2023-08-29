A.11. Application-specific primitives
bits; only the first 512 bits are used. The result is −1 if the signature
is valid, 0 otherwise. Notice that CHKSIGNU is equivalent to ROT; NEWB;
STU 256; ENDB; NEWC; ROTREV; CHKSIGNS, i.e., to CHKSIGNS with the
first argument d set to 256-bit Slice containing h. Therefore, if h is
computed as the hash of some data, these data are hashed twice, the
second hashing occurring inside CHKSIGNS.
• F911 — CHKSIGNS (d s k – ?), checks whether s is a valid Ed25519-
signature of the data portion of Slice d using public key k, similarly to
CHKSIGNU. If the bit length of Slice d is not divisible by eight, throws
a cell underflow exception. The verification of Ed25519 signatures is
the standard one, with sha256 used to reduce d to the 256-bit number
that is actually signed.
• F912–F93F — Reserved for hashing and cryptography primitives.
A.11.7. Miscellaneous primitives.
• F940 — CDATASIZEQ (c n – x y z −1 or 0), recursively computes the
count of distinct cells x, data bits y, and cell references z in the dag
rooted at Cell c, effectively returning the total storage used by this
dag taking into account the identification of equal cells. The values of
x, y, and z are computed by a depth-first traversal of this dag, with a
hash table of visited cell hashes used to prevent visits of already-visited
cells. The total count of visited cells x cannot exceed non-negative
Integer n; otherwise the computation is aborted before visiting the
(n + 1)-st cell and a zero is returned to indicate failure. If c is Null,
returns x = y = z = 0.
• F941 — CDATASIZE (c n – x y z), a non-quiet version of CDATASIZEQ
that throws a cell overflow exception (8) on failure.
• F942 — SDATASIZEQ (s n – x y z −1 or 0), similar to CDATASIZEQ, but
accepting a Slice s instead of a Cell. The returned value of x does not
take into account the cell that contains the slice s itself; however, the
data bits and the cell references of s are accounted for in y and z.
• F943 — SDATASIZE (s n – x y z), a non-quiet version of SDATASIZEQ
that throws a cell overflow exception (8) on failure.
133

