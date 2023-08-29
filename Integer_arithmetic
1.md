1. 1.5. Integer arithmetic
1. 1.4 Total state of TVM (SCCCG)
The total state of TVM consists of the following components:
• Stack (cf. 1.1) — Contains zero or more values (cf. 1.1.1), each be-
longing to one of value types listed in 1.1.3.
• Control registers c0–c15 — Contain some specific values as described
in 1.3.2. (Only seven control registers are used in the current version.)
• Current continuation cc — Contains the current continuation (i.e., the
code that would be normally executed after the current primitive is
completed). This component is similar to the instruction pointer reg-
ister (ip) in other architectures.
• Current codepage cp—Aspecialsigned16-bitintegervaluethatselects
the way the next TVM opcode will be decoded. For example, future
versions of TVM might use different codepages to add new opcodes
while preserving backward compatibility.
• Gas limits gas — Contains four signed 64-bit integers: the current gas
limit g , the maximal gas limit g , the remaining gas g , and the gas
l m r
credit g . Always 0 ≤ g ≤ g , g ≥ 0, and g ≤ g +g ; g is usually
c l m c r l c c
initialized by zero, g is initialized by g + g and gradually decreases
r l c
as the TVM runs. When g becomes negative or if the final value of g
r r
is less than g , an out of gas exception is triggered.
c
Notice that there is no “return stack” containing the return addresses of all
previously called but unfinished functions. Instead, only control register c0
is used. The reason for this will be explained later in 4.1.9.
Also notice that there are no general-purpose registers, because TVM
is a stack machine (cf. 1.1). So the above list, which can be summarized
as “stack, control, continuation, codepage, and gas” (SCCCG), similarly to
the classical SECD machine state (“stack, environment, control, dump”), is
indeed the total state of TVM.5
5Strictlyspeaking,thereisalsothecurrentlibrarycontext,whichconsistsofadictionary
with 256-bit keys and cell values, used to load library reference cells of 3.1.7.
12

