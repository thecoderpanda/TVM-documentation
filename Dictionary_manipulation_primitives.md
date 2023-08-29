A.10. Dictionary manipulation primitives
• F463—DICTDELGETREF(k Dn–D(cid:48) c−1orD0),similartoDICTDELGET,
but with LDREF; ENDS applied to x on success, so that the value re-
turned c is a Cell.
• F464 — DICTIDELGET (i D n – D(cid:48) x −1 or D 0), a variant of primitive
DICTDELGET with signed n-bit integer i as a key.
• F465 — DICTIDELGETREF (i D n – D(cid:48) c −1 or D 0), a variant of
primitive DICTIDELGET returning a Cell instead of a Slice.
• F466 — DICTUDELGET (i D n – D(cid:48) x −1 or D 0), a variant of primitive
DICTDELGET with unsigned n-bit integer i as a key.
• F467 — DICTUDELGETREF (i D n – D(cid:48) c −1 or D 0), a variant of
primitive DICTUDELGET returning a Cell instead of a Slice.
A.10.7. “Maybe reference” dictionary operations. The following op-
erations assume that a dictionary is used to store values c? of type Cell?
(“Maybe Cell”), which can be used in particular to store dictionaries as val-
ues in other dictionaries. The representation is as follows: if c? is a Cell, it
is stored as a value with no data bits and exactly one reference to this Cell.
If c? is Null, then the corresponding key must be absent from the dictionary
altogether.
• F469 — DICTGETOPTREF (k D n – c?), a variant of DICTGETREF that
returns Null instead of the value c? if the key k is absent from dictio-
nary D.
• F46A — DICTIGETOPTREF (i D n – c?), similar to DICTGETOPTREF, but
with the key given by signed n-bit Integer i. If the key i is out of range,
also returns Null.
• F46B — DICTUGETOPTREF (i D n – c?), similar to DICTGETOPTREF, but
with the key given by unsigned n-bit Integer i.
• F46D — DICTSETGETOPTREF (c? k D n – D(cid:48) c˜?), a variant of both
DICTGETOPTREF and DICTSETGETREF that sets the value corresponding
to key k in dictionary D to c? (if c? is Null, then the key is deleted
instead), and returns the old value c˜? (if the key k was absent before,
returns Null instead).
122

