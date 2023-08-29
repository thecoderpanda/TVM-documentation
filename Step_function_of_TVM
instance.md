B.2. Step function of TVM
instance, if such an emulator interpreted a DICTISET instruction simply by
invoking this instruction itself, then a bug in the underlying implementation
of TVM would remain unnoticed.
B.2.4. Reference implementation inside a minimal version of TVM.
We see that using TVM itself as a host machine for a reference implementa-
tion of TVM emulator would yield little insight. A better idea is to define
a stripped-down version of TVM, which supports only the bare minimum
of primitives and 64-bit integer arithmetic, and provide a reference imple-
mentation P of the TVM step function f for this stripped-down version of
TVM.
In that case, one must carefully implement and check only a handful
of primitives to obtain a stripped-down version of TVM, and compare the
reference implementation P running on this stripped-down version to the full
custom TVM implementation being verified. In particular, if there are any
doubts about the validity of a specific run of a custom TVM implementation,
they can now be easily resolved with the aid of the reference implementation.
B.2.5. Relevance for the TON Blockchain. TheTONBlockchainadopts
this approach to validate the runs of TVM (e.g., those used for processing
inbound messages by smart contracts) when the validators’ results do not
match one another. In this case, a reference implementation of TVM, stored
inside the masterchain as a configurable parameter (thus defining the current
revision of TVM), is used to obtain the correct result.
B.2.6. Codepage −1. Codepage −1 of TVM is reserved for the stripped-
down version of TVM. Its main purpose is to execute the reference imple-
mentation of the step function of the full TVM. This codepage contains only
special versions of arithmetic primitives working with “tiny integers” (64-bit
signed integers); therefore, TVM’s 257-bit Integer arithmetic must be de-
fined in terms of 64-bit arithmetic. Elliptic curve cryptography primitives
are also implemented directly in codepage −1, without using any third-party
libraries. Finally, a reference implementation of the sha256 hash function is
also provided in codepage −1.
B.2.7. Codepage −2. This bootstrapping process could be iterated even
further, by providing an emulator of the stripped-down version of TVM writ-
ten for an even simpler version of TVM that supports only boolean values
(or integers 0 and 1)—a “codepage −2”. All 64-bit arithmetic used in code-
page −1 would then need to be defined by means of boolean operations, thus
145

