B.1. Serialization of the TVM state
B.1.3. TVM control registers. ControlregistersinTVMcanbeserialized
as follows:
_ cregs:(HashmapE 4 VmStackValue) = VmSaveList;
B.1.4. TVM gas limits. Gas limits in TVM can be serialized as follows:
gas_limits#_ remaining:int64 _:^[
max_limit:int64 cur_limit:int64 credit:int64 ]
= VmGasLimits;
B.1.5. TVM library environment. The TVM library environment can
be serialized as follows:
_ libraries:(HashmapE 256 ^Cell) = VmLibraries;
B.1.6. TVM continuations. Continuations in TVM can be serialized as
follows:
vmc_std$00 nargs:(## 22) stack:(Maybe VmStack) save:VmSaveList
cp:int16 code:VmCellSlice = VmCont;
vmc_envelope$01 nargs:(## 22) stack:(Maybe VmStack)
save:VmSaveList next:^VmCont = VmCont;
vmc_quit$1000 exit_code:int32 = VmCont;
vmc_quit_exc$1001 = VmCont;
vmc_until$1010 body:^VmCont after:^VmCont = VmCont;
vmc_again$1011 body:^VmCont = VmCont;
vmc_while_cond$1100 cond:^VmCont body:^VmCont
after:^VmCont = VmCont;
vmc_while_body$1101 cond:^VmCont body:^VmCont
after:^VmCont = VmCont;
vmc_pushint$1111 value:int32 next:^VmCont = VmCont;
B.1.7. TVM state. The total state of TVM can be serialized as follows:
vms_init$00 cp:int16 step:int32 gas:GasLimits
stack:(Maybe VmStack) save:VmSaveList code:VmCellSlice
lib:VmLibraries = VmState;
vms_exception$01 cp:int16 step:int32 gas:GasLimits
exc_no:int32 exc_arg:VmStackValue
save:VmSaveList lib:VmLibraries = VmState;
143

