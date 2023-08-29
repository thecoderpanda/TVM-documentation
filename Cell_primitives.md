A.7. Cell primitives
• D5 — LDREFRTOS (s – s(cid:48) s(cid:48)(cid:48)), equivalent to LDREF; SWAP; CTOS.
• D6cc — LDSLICE cc+1 (s – s(cid:48)(cid:48) s(cid:48)), cuts the next cc+1 bits of s into a
separate Slice s(cid:48)(cid:48).
• D700 — LDIX (s l – x s(cid:48)), loads a signed l-bit (0 ≤ l ≤ 257) integer x
from Slice s, and returns the remainder of s as s(cid:48).
• D701 — LDUX (s l – x s(cid:48)), loads an unsigned l-bit integer x from (the
first l bits of) s, with 0 ≤ l ≤ 256.
• D702 — PLDIX (s l – x), preloads a signed l-bit integer from Slice s,
for 0 ≤ l ≤ 257.
• D703 — PLDUX (s l – x), preloads an unsigned l-bit integer from s, for
0 ≤ l ≤ 256.
• D704 — LDIXQ (s l – x s(cid:48) −1 or s 0), quiet version of LDIX: loads a
signed l-bit integer from s similarly to LDIX, but returns a success flag,
equal to −1 on success or to 0 on failure (if s does not have l bits),
instead of throwing a cell underflow exception.
• D705 — LDUXQ (s l – x s(cid:48) −1 or s 0), quiet version of LDUX.
• D706 — PLDIXQ (s l – x −1 or 0), quiet version of PLDIX.
• D707 — PLDUXQ (s l – x −1 or 0), quiet version of PLDUX.
• D708cc — LDI cc+1 (s – x s(cid:48)), a longer encoding for LDI.
• D709cc — LDU cc+1 (s – x s(cid:48)), a longer encoding for LDU.
• D70Acc — PLDI cc+1 (s – x), preloads a signed cc+1-bit integer from
Slice s.
• D70Bcc — PLDU cc+1 (s – x), preloads an unsigned cc+1-bit integer
from s.
• D70Ccc — LDIQ cc+1 (s – x s(cid:48) −1 or s 0), a quiet version of LDI.
• D70Dcc — LDUQ cc+1 (s – x s(cid:48) −1 or s 0), a quiet version of LDU.
• D70Ecc — PLDIQ cc+1 (s – x −1 or 0), a quiet version of PLDI.
100

