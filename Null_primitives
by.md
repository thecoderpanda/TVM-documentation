A.3. Tuple, List, and Null primitives
by |t|. Tuples of length two are called pairs, and Tuples of length three are
triples.
Lisp-style lists are represented with the aid of pairs, i.e., tuples consisting
of exactly two elements. An empty list is represented by a Null value, and
a non-empty list is represented by pair (h,t), where h is the first element of
the list, and t is its tail.
A.3.1. Null primitives. The following primitives work with (the only)
value ⊥ of type Null, useful for representing empty lists, empty branches
of binary trees, and absence of values in Maybe X types. An empty Tuple
created by NIL could have been used for the same purpose; however, Null is
more efficient and costs less gas.
• 6D — NULL or PUSHNULL ( – ⊥), pushes the only value of type Null.
• 6E — ISNULL (x – ?), checks whether x is a Null, and returns −1 or 0
accordingly.
A.3.2. Tuple primitives.
• 6F0n — TUPLE n (x ...x – t), creates a new Tuple t = (x ,...,x )
1 n 1 n
containing n values x , ..., x , where 0 ≤ n ≤ 15.
1 n
• 6F00 — NIL ( – t), pushes the only Tuple t = () of length zero.
• 6F01 — SINGLE (x – t), creates a singleton t := (x), i.e., a Tuple of
length one.
• 6F02 — PAIR or CONS (x y – t), creates pair t := (x,y).
• 6F03 — TRIPLE (x y z – t), creates triple t := (x,y,z).
• 6F1k — INDEX k (t – x), returns the k-th element of a Tuple t, where
0 ≤ k ≤ 15. In other words, returns x if t = (x ,...,x ). If k ≥ n,
k+1 1 n
throws a range check exception.
• 6F10 — FIRST or CAR (t – x), returns the first element of a Tuple.
• 6F11 — SECOND or CDR (t – y), returns the second element of a Tuple.
• 6F12 — THIRD (t – z), returns the third element of a Tuple.
82

