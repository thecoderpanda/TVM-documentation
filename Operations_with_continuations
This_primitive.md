1. 4.3. Operations with continuations
This primitive enables a called function to “return” unneeded arguments to
its caller’s stack, which is useful in some situations (e.g., those related to
exception handling).
1. 4.3.5. Boolean circuits. A continuation c may be thought of as a piece
of code with two optional exit points kept in the savelist of c: the principal
exit point given by c.c0 := c.save(c0), and the auxiliary exit point given
by c.c1 := c.save(c1). If executed, a continuation performs whatever action
it was created for, and then (usually) transfers control to the principal exit
point, or, on some occasions, to the auxiliary exit point. We sometimes say
that a continuation c with both exit points c.c0 and c.c1 defined is a two-exit
continuation, or a boolean circuit, especially if the choice of the exit point
depends on some internally-checked condition.
1. 4.3.6. Composition of continuations. One can compose two continu-
ations c and c(cid:48) simply by setting c.c0 or c.c1 to c(cid:48). This creates a new
continuation denoted by c◦ c(cid:48) or c◦ c(cid:48), which differs from c in its savelist.
0 1
(Recall that if the savelist of c already has an entry corresponding to the con-
trol register in question, such an operation silently does nothing as explained
in 4.3.2).
By composing continuations, one can build chains or other graphs, pos-
sibly with loops, representing the control flow. In fact, the resulting graph
resembles a flow chart, with the boolean circuits corresponding to the “con-
dition nodes” (containing code that will transfer control either to c0 or to c1
depending on some condition), and the one-exit continuations corresponding
to the “action nodes”.
1. 4.3.7. Basic continuation composition primitives. Two basic primi-
tivesforcomposingcontinuationsareCOMPOS(alsoknownasSETCONT c0and
BOOLAND) and COMPOSALT (also known as SETCONT c1 and BOOLOR), which
take c and c(cid:48) from the stack, set c.c0 or c.c1 to c(cid:48), and return the result-
ing continuation c(cid:48)(cid:48) = c ◦ c(cid:48) or c ◦ c(cid:48). All other continuation composition
0 1
operations can be expressed in terms of these two primitives.
1. 4.3.8.Advancedcontinuationcompositionprimitives. However,TVM
can compose continuations not only taken from stack, but also taken from
c0 or c1, or from the current continuation cc; likewise, the result may be
pushed into the stack, stored into either c0 or c1, or used as the new current
continuation (i.e., the control may be transferred to it). Furthermore, TVM
56

