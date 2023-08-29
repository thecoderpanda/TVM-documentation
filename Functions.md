1. 4.6. Functions, recursion, and dictionaries
(cf. A.8.7) are equivalent to PUSHINT nn; PUSH c3; EXECUTE, and similarly
JMP nn or JMPDICT nn are equivalent to PUSHINT nn; PUSH c3; JMPX. In
this way a TVM program, which ultimately is a large collection of mutually
recursive functions, may initialize c3 with the correct selector function rep-
resenting the family of all the functions in the program, and then use CALL
nn to invoke any of these functions by its index (sometimes also called the
selector of a function).
1. 4.6.10. Initialization of c3. A TVM program might initialize c3 by means
of a POP c3 instruction. However, because this usually is the very first ac-
tion undertaken by a program (e.g., a smart contract), TVM makes some
provisions for the automatic initialization of c3. Namely, c3 is initialized by
the code (the initial value of cc) of the program itself, and an extra zero
(or, in some cases, some other predefined number s) is pushed into the stack
before the program’s execution. This is approximately equivalent to invok-
ing JMPDICT 0 (or JMPDICT s) at the very beginning of a program—i.e., the
function with index zero is effectively the main() function for the program.
1. 4.6.11. Creating selector functions and switch statements. TVM
makes special provisions for simple and concise implementation of selector
functions(whichusuallyconstitutethetoplevelofaTVMprogram)or, more
generally, arbitrary switch or case statements (which are also useful in TVM
programs). The most important primitives included for this purpose are
IFBITJMP, IFNBITJMP, IFBITJMPREF, and IFNBITJMPREF (cf. A.8.2). They
effectively enable one to combine subroutines, kept either in separate cells or
as subslices of certain cells, into a binary decision tree with decisions made
according to the indicated bits of the integer passed in the top of the stack.
Another instruction, useful for the implementation of sum-product types,
is PLDUZ (cf. A.7.2). This instruction preloads the first several bits of a Slice
into an Integer, which can later be inspected by IFBITJMP and other similar
instructions.
1. 4.6.12. Alternative: using a hashmap to select the correct function.
Yet another alternative is to use a Hashmap (cf. 3.3) to hold the “collection”
or“dictionary” ofthecodeofallfunctionsinaprogram, andusethehashmap
lookupprimitives(cf.A.10)toselectthecodeoftherequiredfunction, which
can then be BLESSed into a continuation (cf. A.8.5) and executed. Special
combined “lookup, bless, and execute” primitives, such as DICTIGETJMP and
DICTIGETEXEC, are also available (cf. A.10.11). This approach may be more
65

