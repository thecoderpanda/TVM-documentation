1. 2.2. Stack manipulation primitives
These compound stack operations essentially augment other primitives
(instructions) in the code with the “true” locations of their operands, some-
what similarly to what happens with two-address or three-address register
machine code. However, instead of encoding these locations inside the op-
code of the arithmetic or another instruction, as is customary for register
machines, we indicate these locations in a preceding compound stack ma-
nipulation operation. As already described in 2.1.7, the advantage of such
an approach is that user-defined functions (or rarely used specific primitives
added in a future version of TVM) can benefit from it as well (cf. C.3 for a
more detailed discussion with examples).
1. 2.2.4. Mnemonics of compound stack operations. The mnemonics
of compound stack operations, some examples of which have been provided
in 2.2.3, are created as follows.
The γ ≥ 2 formal arguments s(i ), ..., s(i ) to such an operation O
1 γ
represent the values in the original stack that will end up in s(γ − 1), ...,
s0 after the execution of this compound operation, at least if all i , 1 ≤
ν
ν ≤ γ, are distinct and at least γ. The mnemonic itself of the operation
O is a sequence of γ two-letter strings PU and XC, with PU meaning that
the corresponding argument is to be PUshed (i.e., a copy is to be created),
and XC meaning that the value is to be eXChanged (i.e., no other copy of
the original value is created). Sequences of several PU or XC strings may be
abbreviated to one PU or XC followed by the number of copies. (For instance,
we write PUXC2PU instead of PUXCXCPU.)
Asanexception,ifamnemonicwouldconsistofonlyPUoronlyXCstrings,
so that the compound operation is equivalent to a sequence of m PUSHes or
eXCHanGes, the notation PUSHm or XCHGm is used instead of PUm or XCm.
1. 2.2.5. Semantics of compound stack operations. Each compound γ-
ary operation O s(i ),...,s(i ) is translated into an equivalent sequence of
1 γ
basic stack operations by induction in γ as follows:
• As a base of induction, if γ = 0, the only nullary compound stack
operation corresponds to an empty sequence of basic stack operations.
• Equivalently, we might begin the induction from γ = 1. Then PU s(i)
corresponds to the sequence consisting of one basic operation PUSH
s(i), and XC s(i) corresponds to the one-element sequence consisting
of XCHG s(i).
24

