1. 1.2. Categories of TVM instructions
• Continuation — Represents an “execution token” for TVM, which may
be invoked (executed) later. As such, it generalizes function addresses
(i.e., function pointers and references), subroutine return addresses,
instruction pointer addresses, exception handler addresses, closures,
partial applications, anonymous functions, and so on.
This list of value types is incomplete and may be extended in future revisions
of TVM without breaking the old TVM code, due mostly to the fact that
all originally defined primitives accept only values of types known to them
and will fail (generate a type-checking exception) if invoked on values of new
types. Furthermore, existing value types themselves can also be extended in
the future: for example, 257-bit Integer might become 513-bit LongInteger,
with originally defined arithmetic primitives failing if either of the arguments
or the result does not fit into the original subtype Integer. Backward com-
patibility with respect to the introduction of new value types and extension
of existing value types will be discussed in more detail later (cf. 5.1.4).
1. 1.2 Categories of TVM instructions
TVMinstructions, alsocalledprimitives andsometimes(built-in) operations,
arethesmallestoperationsatomicallyperformedbyTVMthatcanbepresent
in the TVM code. They fall into several categories, depending on the types
of values (cf. 1.1.3) they work on. The most important of these categories
are:
• Stack (manipulation) primitives — Rearrange data in the TVM stack,
so that the other primitives and user-defined functions can later be
called with correct arguments. Unlike most other primitives, they are
polymorphic, i.e., work with values of arbitrary types.
• Tuple (manipulation) primitives — Construct, modify, and decompose
Tuples. Similarly to the stack primitives, they are polymorphic.
• Constant or literal primitives — Push into the stack some “constant”
or “literal” values embedded into the TVM code itself, thus providing
arguments to the other primitives. They are somewhat similar to stack
primitives, butarelessgenericbecausetheyworkwithvaluesofspecific
types.
9

