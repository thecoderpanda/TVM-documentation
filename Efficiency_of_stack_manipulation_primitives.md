1. 2.3. Efficiency of stack manipulation primitives
• For γ ≥ 1 (or for γ ≥ 2, if we use γ = 1 as induction base), there are
two subcases:
1. 1. Os(i ),...,s(i ), with O = XCO(cid:48), where O(cid:48) is a compound opera-
1 γ
tion of arity γ−1 (i.e., the mnemonic of O(cid:48) consists of γ−1 strings
XC and PU). Let α be the total quantity of PUshes in O, and β be
that of eXChanges, so that α+β = γ. Then the original operation
is translated into XCHG s(β−1),s(i ), followed by the translation
1
of O(cid:48)s(i ),...,s(i ), defined by the induction hypothesis.
2 γ
1. 2. Os(i ),...,s(i ), with O = PUO(cid:48), where O(cid:48) is a compound op-
1 γ
eration of arity γ − 1. Then the original operation is trans-
lated into PUSH s(i ); XCHG s(β), followed by the translation of
1
O(cid:48)s(i +1),...,s(i +1), defined by the induction hypothesis.10
2 γ
1. 2.2.6. Stack manipulation instructions are polymorphic. Notice that
the stack manipulation instructions are almost the only “polymorphic” prim-
itives in TVM—i.e., they work with values of arbitrary types (including the
value types that will appear only in future revisions of TVM). For exam-
ple, SWAP always interchanges the two top values of the stack, even if one of
them is an integer and the other is a cell. Almost all other instructions, es-
pecially the data processing instructions (including arithmetic instructions),
require each of their arguments to be of some fixed type (possibly different
for different arguments).
1. 2.3 Efficiency of stack manipulation primitives
Stack manipulation primitives employed by a stack machine, such as TVM,
have to be implemented very efficiently, because they constitute more than
half of all the instructions used in a typical program. In fact, TVM performs
all these instructions in a (small) constant time, regardless of the values
involved (even if they represent very large integers or very large trees of
cells).
1. 2.3.1. Implementation of stack manipulation primitives: using ref-
erences for operations instead of objects. The efficiency of TVM’s
implementation of stack manipulation primitives results from the fact that a
10An alternative, arguably better, translation of PUO(cid:48)s(i ),...,s(i ) consists of the
1 γ
translation of O(cid:48)s(i ),...,s(i ), followed by PUSH s(i +α−1); XCHG s(γ−1).
2 γ 1
25

