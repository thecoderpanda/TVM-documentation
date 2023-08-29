A.9. Exception generating and handling primitives
• F16_n — JMP n or JMPDICT n ( – n), jumps to the continuation in c3,
pushing integer 0 ≤ n < 214 as its argument. Approximately equivalent
to PUSHINT n; PUSH c3; JMPX.
• F1A_n — PREPARE n or PREPAREDICT n ( – n c), equivalent to PUSHINT
n; PUSH c3, for 0 ≤ n < 214. In this way, CALL n is approximately
equivalent to PREPARE n; EXECUTE, and JMP n is approximately equiv-
alent to PREPARE n; JMPX. One might use, for instance, CALLARGS or
CALLCC instead of EXECUTE here.
A.9 Exception generating and handling primitives
A.9.1. Throwing exceptions.
• F22_nn — THROW nn ( – 0 nn), throws exception 0 ≤ nn ≤ 63 with
parameter zero. In other words, it transfers control to the continuation
in c2, pushing 0 and nn into its stack, and discarding the old stack
altogether.
• F26_nn — THROWIF nn (f – ), throws exception 0 ≤ nn ≤ 63 with
parameter zero only if integer f (cid:54)= 0.
• F2A_nn — THROWIFNOT nn (f – ), throws exception 0 ≤ nn ≤ 63 with
parameter zero only if integer f = 0.
• F2C4_nn — THROW nn for 0 ≤ nn < 211, an encoding of THROW nn for
larger values of nn.
• F2CC_nn — THROWARG nn (x – x nn), throws exception 0 ≤ nn <
211 with parameter x, by copying x and nn into the stack of c2 and
transferring control to c2.
• F2D4_nn — THROWIF nn (f – ) for 0 ≤ nn < 211.
• F2DC_nn — THROWARGIF nn (x f – ), throws exception 0 ≤ nn < 211
with parameter x only if integer f (cid:54)= 0.
• F2E4_nn — THROWIFNOT nn (f – ) for 0 ≤ nn < 211.
• F2EC_nn — THROWARGIFNOT nn (x f – ), throws exception 0 ≤ nn <
211 with parameter x only if integer f = 0.
114

