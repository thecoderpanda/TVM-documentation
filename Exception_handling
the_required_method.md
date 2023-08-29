1. 4.5. Exception handling
the required method, and executes it. If o needs to modify its state, it simply
computes a new continuation o(cid:48) of the same sort (perhaps with the same code
as o, but with a different initial stack). The new continuation o(cid:48) is returned
to the caller along with whatever other return values need to be returned.
1. 4.4.2. Serializable objects. Another way of representing Smalltalk-style
objects as continuations, or even as trees of cells, consists in using the
JMPREFDATA primitive (a variant of JMPXDATA, cf. 4.1.11), which takes the
first cell reference from the code of the current continuation, transforms the
cell referred to into a simple ordinary continuation, and transfers control to
it, first pushing the remainder of the current continuation as a Slice into the
stack. In this way, an object might be represented by a cell o˜ that contains
JMPREFDATA at the beginning of its data, and the actual code of the object
in the first reference (one might say that the first reference of cell o˜ is the
class of object o˜). Remaining data and references of this cell will be used for
storing the fields of the object.
Such objects have the advantage of being trees of cells, and not just
continuations, meaning that they can be stored into the persistent storage of
a TON smart contract.
1. 4.4.3. Unique continuations and capabilities. It might make sense (in
a future revision of TVM) to mark some continuations as unique, meaning
that they cannot be copied, even in a delayed manner, by increasing their
reference counter to a value greater than one. If an opaque continuation is
unique, it essentially becomes a capability, which can either be used by its
owner exactly once or be transferred to somebody else.
For example, imagine a continuation that represents the output stream to
a printer (this is an example of a continuation used as an object, cf. 4.4.1).
When invoked with one integer argument n, this continuation outputs the
character with code n to the printer, and returns a new continuation of
the same kind reflecting the new state of the stream. Obviously, copying
such a continuation and using the two copies in parallel would lead to some
unintended side effects; marking it as unique would prohibit such adverse
usage.
1. 4.5 Exception handling
TVM’s exception handling is quite simple and consists in a transfer of control
to the continuation kept in control register c2.
58

