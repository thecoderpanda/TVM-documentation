1. 5.1. Codepages and interoperability of different TVM versions
5 Codepages and instruction encoding
This chapter describes the codepage mechanism, which allows TVM to be
flexible and extendable while preserving backward compatibility with respect
to previously generated code.
We also discuss some general considerations about instruction encodings
(applicable to arbitrary machine code, not just TVM), as well as the implica-
tions of these considerations for TVM and the choices made while designing
TVM’s (experimental) codepage zero. The instruction encodings themselves
are presented later in Appendix A.
1. 5.1 Codepages and interoperability of different TVM
versions
The codepages are an essential mechanism of backward compatibility and
of future extensions to TVM. They enable transparent execution of code
written for different revisions of TVM, with transparent interaction between
instances of such code. The mechanism of the codepages, however, is general
andpowerfulenoughtoenablesomeotheroriginallyunintendedapplications.
1. 5.1.1. Codepages in continuations. Everyordinarycontinuationcontains
a 16-bit codepage field cp (cf. 4.1.1), which determines the codepage that
will be used to execute its code. If a continuation is created by a PUSHCONT
(cf. 4.2.3) or similar primitive, it usually inherits the current codepage (i.e.,
the codepage of cc).25
1. 5.1.2. Current codepage. The current codepage cp (cf. 1.4) is the code-
page of the current continuation cc. It determines the way the next in-
struction will be decoded from cc.code, the remainder of the current con-
tinuation’s code. Once the instruction has been decoded and executed, it
determines the next value of the current codepage. In most cases, the cur-
rent codepage is left unchanged.
On the other hand, all primitives that switch the current continuation
load the new value of cp from the new current continuation. In this way, all
code in continuations is always interpreted exactly as it was intended to be.
25Thisisnotexactlytrue. Amoreprecisestatementisthatusuallythecodepageofthe
newly-created continuation is a known function of the current codepage.
67

