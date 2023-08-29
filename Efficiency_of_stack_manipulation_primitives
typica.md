1. 2.3. Efficiency of stack manipulation primitives
typical TVM implementation keeps in the stack not the value objects them-
selves, but only the references (pointers) to such objects. Therefore, a SWAP
instruction only needs to interchange the references at s0 and s1, not the
actual objects they refer to.
1. 2.3.2. Efficient implementation of DUP and PUSH instructions using
copy-on-write. Furthermore, a DUP (or, more generally, PUSH s(i)) instruc-
tion, which appears to make a copy of a potentially large object, also works
in small constant time, because it uses a copy-on-write technique of delayed
copying: it copies only the reference instead of the object itself, but increases
the “reference counter” inside the object, thus sharing the object between the
two references. If an attempt to modify an object with a reference counter
greaterthanoneisdetected, aseparatecopyoftheobjectinquestionismade
first (incurring a certain “non-uniqueness penalty” or “copying penalty” for
the data manipulation instruction that triggered the creation of a new copy).
1. 2.3.3. Garbage collecting and reference counting. When the refer-
ence counter of a TVM object becomes zero (for example, because the last
reference to such an object has been consumed by a DROP operation or an
arithmetic instruction), it is immediately freed. Because cyclic references
are impossible in TVM data structures, this method of reference counting
provides a fast and convenient way of freeing unused objects, replacing slow
and unpredictable garbage collectors.
1. 2.3.4. Transparency of the implementation: Stack values are “val-
ues”, not “references”. Regardless of the implementation details just dis-
cussed, all stack values are really “values”, not “references”, from the perspec-
tive of the TVM programmer, similarly to the values of all types in functional
programming languages. Any attempt to modify an existing object referred
to from any other objects or stack locations will result in a transparent re-
placementofthisobjectbyitsperfectcopybeforethemodificationisactually
performed.
In other words, the programmer should always act as if the objects them-
selves were directly manipulated by stack, arithmetic, and other data trans-
formationprimitives,andtreatthepreviousdiscussiononlyasanexplanation
of the high efficiency of the stack manipulation primitives.
1. 2.3.5. Absence of circular references. One might attempt to create a
circular reference between two cells, A and B, as follows: first create A and
26

