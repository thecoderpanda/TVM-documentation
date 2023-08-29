1. 1.4. Total state of TVM (SCCCG)
• c0 — Contains the next continuation or return continuation (similar
to the subroutine return address in conventional designs). This value
must be a Continuation.
• c1 — Contains the alternative (return) continuation; this value must
be a Continuation. It is used in some (experimental) control flow
primitives, allowing TVM to define and call “subroutines with two exit
points”.
• c2 — Contains the exception handler. This value is a Continuation,
invoked whenever an exception is triggered.
• c3—Containsthecurrent dictionary, essentiallyahashmapcontaining
the code of all functions used in the program. For reasons explained
later in 4.6, this value is also a Continuation, not a Cell as one might
expect.
• c4 — Contains the root of persistent data, or simply the data. This
value is a Cell. When the code of a smart contract is invoked, c4
points to the root cell of its persistent data kept in the blockchain
state. If the smart contract needs to modify this data, it changes c4
before returning.
• c5 — Contains the output actions. It is also a Cell initialized by a
reference to an empty cell, but its final value is considered one of the
smart contract outputs. For instance, the SENDMSG primitive, specific
for the TON Blockchain, simply inserts the message into a list stored
in the output actions.
• c7 — Contains the root of temporary data. It is a Tuple, initialized by
a reference to an empty Tuple before invoking the smart contract and
discarded after its termination.4
More control registers may be defined in the future for specific TON Block-
chain or high-level programming language purposes, if necessary.
4In the TON Blockchain context, c7 is initialized with a singleton Tuple, the only
component of which is a Tuple containing blockchain-specific data. The smart contract is
free to modify c7 to store its temporary data provided the first component of this Tuple
remains intact.
11

