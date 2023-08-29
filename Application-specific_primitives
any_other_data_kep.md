A.11. Application-specific primitives
any other data kept in the cell c7, provided the first reference remains in-
tact (otherwise some application-specific primitives would be likely to throw
exceptions when invoked).
Most of the primitives listed below use 16-bit opcodes.
A.11.2. Gas-related primitives. Of the following primitives, only the first
two are “pure” in the sense that they do not use c5 or c7.
• F800 — ACCEPT, sets current gas limit g to its maximal allowed value
l
g , and resets the gas credit g to zero (cf. 1.4), decreasing the value
m c
of g by g in the process. In other words, the current smart contract
r c
agrees to buy some gas to finish the current transaction. This action
is required to process external messages, which bring no value (hence
no gas) with themselves.
• F801 — SETGASLIMIT (g – ), sets current gas limit g to the minimum
l
of g and g , and resets the gas credit g to zero. If the gas consumed
m c
so far (including the present instruction) exceeds the resulting value of
g , an (unhandled) out of gas exception is thrown before setting new
l
gas limits. Notice that SETGASLIMIT with an argument g ≥ 263 −1 is
equivalent to ACCEPT.
• F802 — BUYGAS (x – ), computes the amount of gas that can be
bought for x nanograms, and sets g accordingly in the same way as
l
SETGASLIMIT.
• F804 — GRAMTOGAS (x – g), computes the amount of gas that can be
bought for x nanograms. If x is negative, returns 0. If g exceeds 263−1,
it is replaced with this value.
• F805 — GASTOGRAM (g – x), computes the price of g gas in nanograms.
• F806–F80E — Reserved for gas-related primitives.
• F80F — COMMIT ( – ), commits the current state of registers c4 (“persis-
tentdata”)andc5(“actions”)sothatthecurrentexecutionisconsidered
“successful” with the saved values even if an exception is thrown later.
A.11.3. Pseudo-random number generator primitives. The pseudo-
random number generator uses the random seed (parameter #6, cf. A.11.4),
an unsigned 256-bit Integer, and (sometimes) other data kept in c7. The
129

