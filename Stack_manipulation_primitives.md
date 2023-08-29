A.2. Stack manipulation primitives
• 55ij — BLKSWAP i+1,j+1, permutes two blocks s(j+i+1)...s(j+1)
and s(j)...s0, for 0 ≤ i,j ≤ 15. Equivalent to REVERSE i+ 1,j + 1;
REVERSE j +1,0; REVERSE i+j +2,0.
• 5513 — ROT2 or 2ROT (a b c d e f – c d e f a b), rotates the three
topmost pairs of stack entries.
• 550i — ROLL i+1, rotates the top i+1 stack entries. Equivalent to
BLKSWAP 1,i+1.
• 55i0 — ROLLREV i+1 or -ROLL i+1, rotates the top i+1 stack entries
in the other direction. Equivalent to BLKSWAP i+1,1.
• 56ii — PUSH s(ii) for 0 ≤ ii ≤ 255.
• 57ii — POP s(ii) for 0 ≤ ii ≤ 255.
• 58—ROT(abc–bca), equivalenttoBLKSWAP 1,2ortoXCHG2 s2,s1.
• 59 — ROTREV or -ROT (a b c – c a b), equivalent to BLKSWAP 2,1 or to
XCHG2 s2,s2.
• 5A — SWAP2 or 2SWAP (a b c d – c d a b), equivalent to BLKSWAP 2,2 or
to XCHG2 s3,s2.
• 5B — DROP2 or 2DROP (a b – ), equivalent to DROP; DROP.
• 5C — DUP2 or 2DUP (a b – a b a b), equivalent to PUSH2 s1,s0.
• 5D — OVER2 or 2OVER (a b c d – a b c d a b), equivalent to PUSH2 s3,s2.
• 5Eij — REVERSE i+2,j, reverses the order of s(j +i+1)...s(j) for
0 ≤ i,j ≤ 15; equivalent to a sequence of (cid:98)i/2(cid:99)+1 XCHGs.
• 5F0i — BLKDROP i, equivalent to DROP performed i times.
• 5Fij — BLKPUSH i,j, equivalent to PUSH s(j) performed i times, 1 ≤
i ≤ 15, 0 ≤ j ≤ 15.
• 60 — PICK or PUSHX, pops integer i from the stack, then performs PUSH
s(i).
• 61—ROLLX,popsintegerifromthestack, thenperformsBLKSWAP 1,i.
80

