1. 4.1. Continuations and subroutines
1. 4.1.2. Simple ordinary continuations. In most cases, the ordinary con-
tinuationsarethesimplestones, havingempty stackandsave. Theyconsist
essentially of a reference code to (the remainder of) the code to be executed,
and of the codepage cp to be used while decoding the instructions from this
code.
1. 4.1.3. Current continuation cc. The “current continuation” cc is an im-
portant part of the total state of TVM, representing the code being executed
right now (cf. 1.1). In particular, what we call “the current stack” (or simply
“the stack”) when discussing all other primitives is in fact the stack of the
current continuation. All other components of the total state of TVM may
be also thought of as parts of the current continuation cc; however, they
may be extracted from the current continuation and kept separately as part
of the total state for performance reasons. This is why we describe the stack,
the control registers, and the codepage as separate parts of the TVM state
in 1.4.
1. 4.1.4. Normal work of TVM, or the main loop. TVM usually performs
the following operations:
If the current continuation cc is an ordinary one, it decodes the first
instruction from the Slice code, similarly to the way other cells are deseri-
alized by TVM LD* primitives (cf. 3.2 and 3.2.11): it decodes the opcode
first, and then the parameters of the instruction (e.g., 4-bit fields indicating
“stack registers” involved for stack manipulation primitives, or constant val-
ues for “push constant” or “literal” primitives). The remainder of the Slice
is then put into the code of the new cc, and the decoded operation is exe-
cuted on the current stack. This entire process is repeated until there are no
operations left in cc.code.
If the code is empty (i.e., contains no bits of data and no references), or if
a (rarely needed) explicit subroutine return (RET) instruction is encountered,
the current continuation is discarded, and the “return continuation” from
control register c0 is loaded into cc instead (this process is discussed in
more detail starting in 4.1.6).20 Then the execution continues by parsing
operations from the new current continuation.
1. 4.1.5. Extraordinary continuations. In addition to the ordinary continu-
ationsconsideredsofar(cf.4.1.1), TVMincludessomeextraordinary contin-
20If there are no bits of data left in code, but there is still exactly one reference, an
implicit JMP to the cell at that reference is performed instead of an implicit RET.
50

