1. 4.3. Operations with continuations
versions of these primitives (e.g., IFCONT or UNTILREFCONT) may be defined
in a future revision of TVM, which combine a PUSHCONT or PUSHREFCONT
with another primitive. If one inspects the resulting code, IFCONT looks very
much like the more customary “conditional-branch-forward” instruction.
1. 4.3 Operations with continuations
1. 4.3.1.Continuationsareopaque. Noticethatallcontinuationsareopaque,
at least in the current version of TVM, meaning that there is no way to
modify a continuation or inspect its internal data. Almost the only use of a
continuation is to supply it to a control flow primitive.
While there are some arguments in favor of including support for non-
opaque continuations in TVM (along with opaque continuations, which are
required for virtualization), the current revision offers no such support.
1. 4.3.2. Allowed operations with continuations. However, some opera-
tions with opaque continuations are still possible, mostly because they are
equivalent to operations of the kind “create a new continuation, which will
do something special, and then invoke the original continuation”. Allowed
operations with continuations include:
• Push one or several values into the stack of a continuation c (thus
creating a partial application of a function, or a closure).
• Set the saved value of a control register c(i) inside the savelist c.save
of a continuation c. If there is already a value for the control register
in question, this operation silently does nothing.
1. 4.3.3. Example: operations with control registers. TVM has some
primitives to set and inspect the values of control registers. The most impor-
tant of them are PUSH c(i) (pushes the current value of c(i) into the stack)
and POP c(i) (sets the value of c(i) from the stack, if the supplied value is
of the correct type). However, there is also a modified version of the latter
instruction, called POPSAVE c(i), which saves the old value of c(i) (for i > 0)
intothecontinuationatc0asdescribedin4.3.2beforesettingthenewvalue.
1. 4.3.4. Example: setting the number of arguments to a function in
its code. The primitive LEAVEARGS n demonstrates another application of
continuations in an operation: it leaves only the top n values of the cur-
rent stack, and moves the remainder to the stack of the continuation in c0.
55

