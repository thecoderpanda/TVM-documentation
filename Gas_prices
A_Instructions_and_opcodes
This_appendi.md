A.1. Gas prices
A Instructions and opcodes
This appendix lists all instructions available in the (experimental) codepage
zero of TVM, as explained in 5.3.
We list the instructions in lexicographical opcode order. However, the
opcode space is distributed in such way as to make all instructions in each
category (e.g., arithmetic primitives) have neighboring opcodes. So we first
list a number of stack manipulation primitives, then constant primitives,
arithmetic primitives, comparison primitives, cell primitives, continuation
primitives, dictionary primitives, and finally application-specific primitives.
We use hexadecimal notation (cf. 1.0) for bitstrings. Stack registers s(i)
usually have 0 ≤ i ≤ 15, and i is encoded in a 4-bit field (or, on a few rare
occasions, in an 8-bit field). Other immediate parameters are usually 4-bit,
8-bit, or variable length.
The stack notation described in 2.1.10 is extensively used throughout
this appendix.
A.1 Gas prices
The gas price for most primitives equals the basic gas price, computed as
P := 10 + b + 5r, where b is the instruction length in bits and r is the
b
number of cell references included in the instruction. When the gas price
of an instruction differs from this basic price, it is indicated in parentheses
after its mnemonics, either as (x), meaning that the total gas price equals
x, or as (+x), meaning P +x. Apart from integer constants, the following
b
expressions may appear:
• C — The total price of “reading” cells (i.e., transforming cell refer-
r
ences into cell slices). Currently equal to 100 or 25 gas units per cell
depending on whether it is the first time a cell with this hash is being
“read” during the current run of the VM or not.
• L — The total price of loading cells. Depends on the loading action
required.
• B — The total price of creating new Builders. Currently equal to 0
w
gas units per builder.
• C — The total price of creating new Cells from Builders. Currently
w
equal to 500 gas units per cell.
77

