A.12. Debug primitives
• FEnn — DEBUG nn, for 0 ≤ nn < 240, is a two-byte NOP.
• FEFnssss — DEBUGSTR ssss, for 0 ≤ n < 16, is an (n+3)-byte NOP,
with the (n+1)-byte “contents string” ssss skipped as well.
A.12.2. Debug primitives as operations without side-effect. Next
we describe the debug primitives that might (and actually are) implemented
in a version of TVM. Notice that another TVM implementation is free to
use these codes for other debug purposes, or treat them as multibyte NOPs.
Whenever these primitives need some arguments from the stack, they inspect
these arguments, but leave them intact in the stack. If there are insufficient
valuesinthestack, ortheyhaveincorrecttypes, debugprimitivesmayoutput
error messages into the debug log, or behave as NOPs, but they cannot throw
exceptions.
• FE00 — DUMPSTK, dumps the stack (at most the top 255 values) and
shows the total stack depth.
• FE0n — DUMPSTKTOP n, 1 ≤ n < 15, dumps the top n values from the
stack, starting from the deepest of them. If there are d < n values
available, dumps only d values.
• FE10 — HEXDUMP, dumps s0 in hexadecimal form, be it a Slice or an
Integer.
• FE11 — HEXPRINT, similar to HEXDUMP, except the hexadecimal repre-
sentation of s0 is not immediately output, but rather concatenated to
an output text buffer.
• FE12 — BINDUMP, dumps s0 in binary form, similarly to HEXDUMP.
• FE13 — BINPRINT, outputs the binary representation of s0 to a text
buffer.
• FE14 — STRDUMP, dumps the Slice at s0 as an UTF-8 string.
• FE15 — STRPRINT, similar to STRDUMP, but outputs the string into a
text buffer (without carriage return).
• FE1E — DEBUGOFF, disables all debug output until it is re-enabled by
a DEBUGON. More precisely, this primitive increases an internal counter,
which disables all debug operations (except DEBUGOFF and DEBUGON)
when strictly positive.
139

