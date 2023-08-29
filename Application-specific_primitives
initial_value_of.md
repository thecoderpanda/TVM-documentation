A.11. Application-specific primitives
initial value of the random seed before a smart contract is executed in TON
Blockchain is a hash of the smart contract address and the global block
random seed. If there are several runs of the same smart contract inside
a block, then all of these runs will have the same random seed. This can
be fixed, for example, by running LTIME; ADDRAND before using the pseudo-
random number generator for the first time.
• F810 — RANDU256 ( – x), generates a new pseudo-random unsigned
256-bit Integer x. The algorithm is as follows: if r is the old value
of the random seed, considered as a 32-byte array (by constructing
the big-endian representation of an unsigned 256-bit integer), then its
sha512(r) is computed; the first 32 bytes of this hash are stored as
the new value r(cid:48) of the random seed, and the remaining 32 bytes are
returned as the next random value x.
• F811 — RAND (y – z), generates a new pseudo-random integer z in the
range 0...y − 1 (or y... − 1, if y < 0). More precisely, an unsigned
random value x is generated as in RAND256U; then z := (cid:98)xy/2256(cid:99) is
computed. Equivalent to RANDU256; MULRSHIFT 256.
• F814 — SETRAND (x – ), sets the random seed to unsigned 256-bit
Integer x.
• F815 — ADDRAND (x – ), mixes unsigned 256-bit Integer x into the ran-
dom seed r by setting the random seed to sha256 of the concatenation
of two 32-byte strings: the first with the big-endian representation of
the old seed r, and the second with the big-endian representation of x.
• F810–F81F — Reserved for pseudo-random number generator primi-
tives.
A.11.4. Configuration primitives. The following primitives read con-
figuration data provided in the Tuple stored in the first component of the
Tuple atc7. WheneverTVMisinvokedforexecutingTONBlockchainsmart
contracts, this Tuple is initialized by a SmartContractInfo structure; config-
uration primitives assume that it has remained intact.
• F82i — GETPARAM i ( – x), returns the i-th parameter from the Tuple
provided at c7 for 0 ≤ i < 16. Equivalent to PUSH c7; FIRST; INDEX
i. If one of these internal operations fails, throws an appropriate type
checking or range checking exception.
130

