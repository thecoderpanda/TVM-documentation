1. 3.3. Hashmaps, or dictionaries
• GetSubdict(D,l,k ) — Given D : HashmapE(n,X) and some l-bit
0
string k : l·bit for 0 ≤ l ≤ n, returns subdictionary D(cid:48) = D/k of D,
0 0
consisting of keys beginning with k . The result D(cid:48) may be of either
0
type HashmapE(n,X) or type HashmapE(n−l,X).
• ReplaceSubdict(D,l,k ,D(cid:48)) — Given D : HashmapE(n,X), 0 ≤
0
l ≤ n, k : l · bit, and D(cid:48) : HashmapE(n − l,X), replaces with D(cid:48)
0
the subdictionary D/k of D consisting of keys beginning with k , and
0 0
returns the resulting dictionary D(cid:48)(cid:48) : HashmapE(n,X). Some variants
ofReplaceSubdictmayalsoreturntheoldvalueofthesubdictionary
D/k in question.
0
• DeleteSubdict(D,l,k )—EquivalenttoReplaceSubdictwithD(cid:48)
0
being an empty dictionary.
• Split(D) — Given D : HashmapE(n,X), returns D := D/0 and
0
D := D/1 : HashmapE(n − 1,X), the two subdictionaries of D con-
1
sisting of all keys beginning with 0 and 1, respectively.
• Merge(D ,D ) — Given D and D : HashmapE(n−1,X), computes
0 1 0 1
D : HashmapE(n,X), such that D/0 = D and D/1 = D .
0 1
• Foreach(D,f) — Executes a function f with two arguments k and
x, with (k,x) running over all key-value pairs of a dictionary D in
lexicographical order.18
• ForeachRev(D,f) — Similar to Foreach, but processes all key-
value pairs in reverse order.
• TreeReduce(D,o,f,g) — Given D : HashmapE(n,X), a value o : X,
and two functions f : X → Y and g : Y × Y → Y, performs a “tree
reduction” of D by first applying f to all the leaves, and then using g
to compute the value corresponding to a fork starting from the values
assigned to its children.19
18In fact, f may receive m extra arguments and return m modified values, which are
passed to the next invocation of f. This may be used to implement “map” and “reduce”
operations with dictionaries.
19Versions of this operation may be introduced where f and g receive an additional
bitstring argument, equal to the key (for leaves) or to the common prefix of all keys (for
forks) in the corresponding subtree.
46

