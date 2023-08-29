A.3. Tuple, List, and Null primitives
• 62—-ROLLXorROLLREVX,popsintegerifromthestack, thenperforms
BLKSWAP i,1.
• 63 — BLKSWX, pops integers i,j from the stack, then performs BLKSWAP
i,j.
• 64 — REVX, pops integers i,j from the stack, then performs REVERSE
i,j.
• 65 — DROPX, pops integer i from the stack, then performs BLKDROP i.
• 66 — TUCK (ab−bab), equivalent to SWAP; OVER or to XCPU s1,s1.
• 67 — XCHGX, pops integer i from the stack, then performs XCHG s(i).
• 68 — DEPTH, pushes the current depth of the stack.
• 69 — CHKDEPTH, pops integer i from the stack, then checks whether
there are at least i elements, generating a stack underflow exception
otherwise.
• 6A — ONLYTOPX, pops integer i from the stack, then removes all but
the top i elements.
• 6B — ONLYX, pops integer i from the stack, then leaves only the bottom
i elements. Approximately equivalent to DEPTH; SWAP; SUB; DROPX.
• 6C00–6C0F — reserved for stack operations.
• 6Cij — BLKDROP2 i,j, drops i stack elements under the top j elements,
where 1 ≤ i ≤ 15 and 0 ≤ j ≤ 15. Equivalent to REVERSE i + j,0;
BLKDROP i; REVERSE j,0.
A.3 Tuple, List, and Null primitives
Tuples are ordered collections consisting of at most 255 TVM stack values of
arbitrary types (not necessarily the same). Tuple primitives create, modify,
and unpack Tuples; they manipulate values of arbitrary types in the process,
similarly to the stack primitives. We do not recommend using Tuples of more
than 15 elements.
When a Tuple t contains elements x , ..., x (in that order), we write
1 n
t = (x ,...,x ); number n ≥ 0 is the length of Tuple t. It is also denoted
1 n
81

