Telegram Open Network Virtual Machine
Nikolai Durov
March 23, 2020
Abstract
The aim of this text is to provide a description of the Telegram
Open Network Virtual Machine (TON VM or TVM), used to execute
smart contracts in the TON Blockchain.
Introduction
The primary purpose of the Telegram Open Network Virtual Machine (TON
VM or TVM) is to execute smart-contract code in the TON Blockchain.
TVM must support all operations required to parse incoming messages and
persistent data, and to create new messages and modify persistent data.
Additionally, TVM must meet the following requirements:
• It must provide for possible future extensions and improvements while
retainingbackwardcompatibilityandinteroperability,becausethecode
of a smart contract, once committed into the blockchain, must continue
working in a predictable manner regardless of any future modifications
to the VM.
• It must strive to attain high “(virtual) machine code” density, so that
the code of a typical smart contract occupies as little persistent block-
chain storage as possible.
• It must be completely deterministic. In other words, each run of the
same code with the same input data must produce the same result,
1

