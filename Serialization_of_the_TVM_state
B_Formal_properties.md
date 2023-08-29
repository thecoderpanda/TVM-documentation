B.1. Serialization of the TVM state
B Formal properties and specifications of TVM
This appendix discusses certain formal properties of TVM that are necessary
for executing smart contracts in the TON Blockchain and validating such
executions afterwards.
B.1 Serialization of the TVM state
Recall that a virtual machine used for executing smart contracts in a block-
chainmustbedeterministic, otherwisethevalidationofeachexecutionwould
require the inclusion of all intermediate steps of the execution into a block,
or at least of the choices made when indeterministic operations have been
performed.
Furthermore, the state of such a virtual machine must be (uniquely) se-
rializable, so that even if the state itself is not usually included in a block,
its hash is still well-defined and can be included into a block for verification
purposes.
B.1.1. TVM stack values. TVM stack values can be serialized as follows:
vm_stk_tinyint#01 value:int64 = VmStackValue;
vm_stk_int#0201_ value:int257 = VmStackValue;
vm_stk_nan#02FF = VmStackValue;
vm_stk_cell#03 cell:^Cell = VmStackValue;
_ cell:^Cell st_bits:(## 10) end_bits:(## 10)
{ st_bits <= end_bits }
st_ref:(#<= 4) end_ref:(#<= 4)
{ st_ref <= end_ref } = VmCellSlice;
vm_stk_slice#04 _:VmCellSlice = VmStackValue;
vm_stk_builder#05 cell:^Cell = VmStackValue;
vm_stk_cont#06 cont:VmCont = VmStackValue;
Of these, vm_stk_tinyint is never used by TVM in codepage zero; it is used
only in restricted modes.
B.1.2. TVM stack. The TVM stack can be serialized as follows:
vm_stack#_ depth:(## 24) stack:(VmStackList depth) = VmStack;
vm_stk_cons#_ {n:#} head:VmStackValue tail:^(VmStackList n)
= VmStackList (n + 1);
vm_stk_nil#_ = VmStackList 0;
142

