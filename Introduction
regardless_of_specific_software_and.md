Introduction
regardless of specific software and hardware used.1
The design of TVM is guided by these requirements. While this document
describes a preliminary and experimental version of TVM,2 the backward
compatibility mechanisms built into the system allow us to be relatively
unconcerned with the efficiency of the operation encoding used for TVM
code in this preliminary version.
TVMisnotintendedtobeimplementedinhardware(e.g., inaspecialized
microprocessor chip); rather, it should be implemented in software running
on conventional hardware. This consideration lets us incorporate some high-
level concepts and operations in TVM that would require convoluted mi-
crocode in a hardware implementation but pose no significant problems for a
software implementation. Such operations are useful for achieving high code
density and minimizing the byte (or storage cell) profile of smart-contract
code when deployed in the TON Blockchain.
1For example, there are no floating-point arithmetic operations (which could be effi-
cientlyimplementedusinghardware-supporteddoubletypeonmostmodernCPUs)present
inTVM,becausetheresultofperformingsuchoperationsisdependentonthespecificun-
derlying hardware implementation and rounding mode settings. Instead, TVM supports
specialintegerarithmeticoperations,whichcanbeusedtosimulatefixed-pointarithmetic
if needed.
2The production version will likely require some tweaks and modifications prior to
launch, which will become apparent only after using the experimental version in the test
environment for some time.
2

