A.13. Codepage primitives
• FE1F — DEBUGON, enables debug output (in a debug version of TVM).
• FE2n — DUMP s(n), 0 ≤ n < 15, dumps s(n).
• FE3n — PRINT s(n), 0 ≤ n < 15, concatenates the text representation
of s(n) (without any leading or trailing spaces or carriage returns) to a
text buffer which will be output before the output of any other debug
operation.
• FEC0–FEEF — Use these opcodes for custom/experimental debug oper-
ations.
• FEFnssss — DUMPTOSFMT ssss, dumps s0 formatted according to the
(n + 1)-byte string ssss. This string might contain (a prefix of) the
name of a TL-B type supported by the debugger. If the string begins
with a zero byte, simply outputs it (without the first byte) into the
debug log. If the string begins with a byte equal to one, concatenates
ittoabuffer, whichwillbeoutputbeforetheoutputofanyotherdebug
operation (effectively outputs a string without a carriage return).
• FEFn00ssss — LOGSTR ssss, string ssss is n bytes long.
• FEF000 — LOGFLUSH, flushes all pending debug output from the buffer
into the debug log.
• FEFn01ssss — PRINTSTR ssss, string ssss is n bytes long.
A.13 Codepage primitives
The following primitives, which begin with byte FF, typically are used at the
very beginning of a smart contract’s code or a library subroutine to select
another TVM codepage. Notice that we expect all codepages to contain
these primitives with the same codes, otherwise switching back to another
codepage might be impossible (cf. 5.1.8).
• FFnn — SETCP nn, selects TVM codepage 0 ≤ nn < 240. If the
codepage is not supported, throws an invalid opcode exception.
• FF00 — SETCP0, selects TVM (test) codepage zero as described in this
document.
140

