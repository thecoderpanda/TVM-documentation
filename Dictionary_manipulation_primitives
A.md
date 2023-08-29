A.10. Dictionary manipulation primitives
A.10.4. Set/Replace/Add dictionary operations. The mnemonics of
the following dictionary primitives are constructed in a systematic fashion
according to the regular expression DICT[,I,U](SET,REPLACE,ADD)[GET][REF]
depending on the type of the key used (a Slice or a signed or unsigned
Integer), the dictionary operation to be performed, and the way the values
are accepted and returned (as Cells or as Slices). Therefore, we provide a
detailed description only for some primitives, assuming that this information
is sufficient for the reader to understand the precise action of the remaining
primitives.
• F412 — DICTSET (x k D n – D(cid:48)), sets the value associated with n-bit
key k (represented by a Slice as in DICTGET) in dictionary D (also rep-
resented by a Slice) to value x (again a Slice), and returns the resulting
dictionary as D(cid:48).
• F413 — DICTSETREF (c k D n – D(cid:48)), similar to DICTSET, but with the
value set to a reference to Cell c.
• F414 — DICTISET (x i D n – D(cid:48)), similar to DICTSET, but with the
key represented by a (big-endian) signed n-bit integer i. If i does not
fit into n bits, a range check exception is generated.
• F415 — DICTISETREF (c i D n – D(cid:48)), similar to DICTSETREF, but with
the key a signed n-bit integer as in DICTISET.
• F416 — DICTUSET (x i D n – D(cid:48)), similar to DICTISET, but with i an
unsigned n-bit integer.
• F417 — DICTUSETREF (c i D n – D(cid:48)), similar to DICTISETREF, but with
i unsigned.
• F41A — DICTSETGET (x k D n – D(cid:48) y −1 or D(cid:48) 0), combines DICTSET
with DICTGET: it sets the value corresponding to key k to x, but also
returns the old value y associated with the key in question, if present.
• F41B — DICTSETGETREF (c k D n – D(cid:48) c(cid:48) −1 or D(cid:48) 0), combines
DICTSETREF with DICTGETREF similarly to DICTSETGET.
• F41C—DICTISETGET(xiDn–D(cid:48) y −1orD(cid:48) 0),similartoDICTSETGET,
but with the key represented by a big-endian signed n-bit Integer i.
118

