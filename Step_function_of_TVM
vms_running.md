B.2. Step function of TVM
vms_running$10 cp:int16 step:int32 gas:GasLimits stack:VmStack
save:VmSaveList code:VmCellSlice lib:VmLibraries
= VmState;
vms_finished$11 cp:int16 step:int32 gas:GasLimits
exit_code:int32 no_gas:Boolean stack:VmStack
save:VmSaveList lib:VmLibraries = VmState;
When TVM is initialized, its state is described by a vms_init, usually with
step set to zero. The step function of TVM does nothing to a vms_finished
state, and transforms all other states into vms_running, vms_exception, or
vms_finished, with step increased by one.
B.2 Step function of TVM
A formal specification of TVM would be completed by the definition of a step
function f : VmState → VmState. This function deterministically trans-
forms a valid VM state into a valid subsequent VM state, and is allowed to
throw exceptions or return an invalid subsequent state if the original state
was invalid.
B.2.1. A high-level definition of the step function. We might present
a very long formal definition of the TVM step function in a high-level func-
tional programming language. Such a specification, however, would mostly
be useful as a reference for the (human) developers. We have chosen another
approach, better adapted to automated formal verification by computers.
B.2.2. An operational definition of the step function. Notice that the
step function f is a well-defined computable function from trees of cells into
trees of cells. As such, it can be computed by a universal Turing machine.
Then a program P computing f on such a machine would provide a machine-
checkable specification of the step function f. This program P effectively is
an emulator of TVM on this Turing machine.
B.2.3. A reference implementation of the TVM emulator inside
TVM. We see that the step function of TVM may be defined by a reference
implementation of a TVM emulator on another machine. An obvious idea
is to use TVM itself, since it is well-adapted to working with trees of cells.
However, an emulator of TVM inside itself is not very useful if we have
doubts about a particular implementation of TVM and want to check it. For
144

