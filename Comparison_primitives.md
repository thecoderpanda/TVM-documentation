A.6. Comparison primitives
• C2FF — ISNNEG, checks whether an integer is non-negative.
• C3yy — NEQINT yy (x – x (cid:54)= yy) for −27 ≤ yy < 27.
• C4 — ISNAN (x – x = NaN), checks whether x is a NaN.
• C5 — CHKNAN (x – x), throws an arithmetic overflow exception if x is a
NaN.
• C6 — reserved for integer comparison.
A.6.2. Other comparison.
Most of these “other comparison” primitives actually compare the data
portions of Slices as bitstrings.
• C700 — SEMPTY (s – s = ∅), checks whether a Slice s is empty (i.e.,
contains no bits of data and no cell references).
• C701 — SDEMPTY (s – s ≈ ∅), checks whether Slice s has no bits of
data.
• C702 — SREMPTY (s – r(s) = 0), checks whether Slice s has no refer-
ences.
• C703 — SDFIRST (s – s = 1), checks whether the first bit of Slice s is
0
a one.
• C704 — SDLEXCMP (s s(cid:48) – c), compares the data of s lexicographically
with the data of s(cid:48), returning −1, 0, or 1 depending on the result.
• C705 — SDEQ (s s(cid:48) – s ≈ s(cid:48)), checks whether the data parts of s and s(cid:48)
coincide, equivalent to SDLEXCMP; ISZERO.
• C708 — SDPFX (s s(cid:48) – ?), checks whether s is a prefix of s(cid:48).
• C709—SDPFXREV(ss(cid:48) –?), checkswhethers(cid:48) isaprefixofs, equivalent
to SWAP; SDPFX.
• C70A — SDPPFX (s s(cid:48) – ?), checks whether s is a proper prefix of s(cid:48) (i.e.,
a prefix distinct from s(cid:48)).
• C70B — SDPPFXREV (s s(cid:48) – ?), checks whether s(cid:48) is a proper prefix of s.
94

