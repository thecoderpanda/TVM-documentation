A.11. Application-specific primitives
returns the new subdictionary of the same type HashmapE(n,X) as a
Slice D(cid:48).
• F4B2 — SUBDICTIGET (x l D n – D(cid:48)), variant of SUBDICTGET with
the prefix represented by a signed big-endian l-bit Integer x, where
necessarily l ≤ 257.
• F4B3 — SUBDICTUGET (x l D n – D(cid:48)), variant of SUBDICTGET with the
prefix represented by an unsigned big-endian l-bit Integer x, where
necessarily l ≤ 256.
• F4B5 — SUBDICTRPGET (k l D n – D(cid:48)), similar to SUBDICTGET, but
removes the common prefix k from all keys of the new dictionary D(cid:48),
which becomes of type HashmapE(n−l,X).
• F4B6 — SUBDICTIRPGET (x l D n – D(cid:48)), variant of SUBDICTRPGET with
the prefix represented by a signed big-endian l-bit Integer x, where
necessarily l ≤ 257.
• F4B7 — SUBDICTURPGET (x l D n – D(cid:48)), variant of SUBDICTRPGET with
the prefix represented by an unsigned big-endian l-bit Integer x, where
necessarily l ≤ 256.
• F4BC–F4BF — used by DICT...Z primitives in A.10.11.
A.11 Application-specific primitives
OpcoderangeF8...FBisreservedfortheapplication-specificprimitives. When
TVM is used to execute TON Blockchain smart contracts, these application-
specific primitives are in fact TON Blockchain-specific.
A.11.1. External actions and access to blockchain configuration
data. Someoftheprimitiveslistedbelowpretendtoproducesomeexternally
visible actions, such as sending a message to another smart contract. In fact,
the execution of a smart contract in TVM never has any effect apart from
a modification of the TVM state. All external actions are collected into a
linked list stored in special register c5 (“output actions”). Additionally, some
primitives use the data kept in the first component of the Tuple stored in
c7 (“root of temporary data”, cf. 1.3.2). Smart contracts are free to modify
128

