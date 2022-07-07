# Survey on Analysis Tools
#### Evaluation Subject

There are many smart contract analysis tools listed in [Analysis Tools.md](Analysis Tools.md). Not all the identified tools are well suited for the survey. Only the tools that met the following inclusion criteria were included in this survey.

1. Public Available and CLI
2. Compatible Input: The tool takes as input a Solidity contract, rather than only consider EVM bytecode.
3. Only Source: The tool requires only the source code of the contract, rather than test suite or contracts annotated with assertions.
4. Vulnerability Finding: The tool identifies vulnerabilities or bad practices in contracts, rather than only visualize control flow graphs.
4. Classic and original: The tool should be a classic original tool, rather than the fine-tuning based on a framework.

#### Evaluation Matrix

- [Production] How many vulnerabilities the tools can detect
- [Effectiveness] How precise the analysis tools are in detecting known vulnerabilities
- [Performance / Efficiency] How long do the tools require to analyze the smart contracts?

#### Test Dataset and Tool

- Contract Dataset
  - contracts with know vulnerabilities: [A Survey on Ethereum Systems Security: Vulnerabilities, Attacks and Defenses](https://arxiv.org/pdf/1908.04507.pdf)
  - Real contracts on etherscan

- Vulnerability Dataset: 
  - [DASP10](https://dasp.co/)
  - [SWC](https://swcregistry.io/)
  - [A Survey on Ethereum Systems Security: Vulnerabilities, Attacks and Defenses](https://arxiv.org/pdf/1908.04507.pdf)

- Tool: [SmartBugs](https://github.com/smartbugs/smartbugs)

#### Result

##### Production

- No tool can find all the vulnerabilities. Should extend the scope of vulnerabilities (combine static with dynamic analysis)
- Vulnerability detectors listed by the developer of the tool

| Category                        | Maian | Manticore | Mythril | Oyente | Securify | Slither | Smartcheck |
| ------------------------------- | :---: | :-------: | :-----: | :----: | :------: | :-----: | :--------: |
| Access Control / tx.origin - V8 |       |     √     |    √    |        |          |    √    |     √      |
| Arithmetic - V6                 |       |     √     |    √    |   √    |          |         |     √      |
| Bad Randomness - V26            |       |     √     |    √    |        |          |         |            |
| Denial of Service               |   √   |           |    √    |   √    |    √     |    √    |     √      |
| Front Running / TOD - V24       |       |           |    √    |   √    |    √     |         |            |
| Reentrancy - V1                 |       |     √     |    √    |   √    |    √     |    √    |     √      |
| Short Addresses - V20           |       |           |         |        |          |         |            |
| Time Manipulation - V25         |       |     √     |    √    |   √    |          |    √    |     √      |
| Unchecked Low Calls - V15       |   √   |     √     |    √    |   √    |    √     |    √    |     √      |

- Vulnerabilities actually detected by tools from test dataset, [ref](https://arxiv.org/pdf/1910.10601.pdf)

| Category                        | Maian | Manticore | Mythril | Oyente | Securify | Slither | Smartcheck |
| ------------------------------- | :---: | :-------: | :-----: | :----: | :------: | :-----: | :--------: |
| Access Control / tx.origin - V8 |  44   |    47     |  1076   |   2    |   614    |  2356   |    2356    |
| Arithmetic - V6                 |   0   |    102    |  18515  | 34306  |    0     |    0    |    7430    |
| Bad Randomness - V26            |   0   |     0     |    0    |   0    |    0     |    0    |     0      |
| Denial of Service               |   0   |     0     |    0    |  880   |    0     |  2555   |   11621    |
| Front Running / TOD - V24       |   0   |     0     |  2015   |   0    |   7217   |    0    |     0      |
| Reentrancy - V1                 |   0   |     2     |  8454   |  308   |   2033   |  8764   |    847     |
| Short Addresses - V20           |   0   |     0     |    0    |   0    |    0     |    0    |     0      |
| Time Manipulation - V25         |   0   |    90     |    0    |  1452  |    0     |  1988   |     68     |
| Unchecked Low Calls - V15       |   0   |     4     |   443   |   0    |   592    |  12199  |    2867    |
| Unknown                         |  135  |   1032    |  11126  |   0    |   561    |  9133   |   14113    |
| Total                           |  179  |   1203    |  22994  | 34764  |   8781   |  22269  |   24906    |

##### Effectiveness

- [ref](https://arxiv.org/pdf/2005.11613.pdf)
- False Negative (either incorrectly detected or not detected by the tool)

| Category                        | Manticore | Mythril | Oyente | Securify | Slither | Smartcheck |
| ------------------------------- | :-------: | :-----: | :----: | :------: | :-----: | :--------: |
| Access Control / tx.origin - V8 |    NA     |  33.3%  |   NA   |    NA    |   0%    |   92.7%    |
| Arithmetic - V6                 |   89.7%   |  80.2%  | 67.4%  |    NA    |   NA    |   80.4%    |
| Front Running / TOD - V24       |    NA     |   NA    | 89.7%  |  19.7%   |   NA    |     NA     |
| Reentrancy - V1                 |   93.1%   |  80.8%  | 75.1%  |  17.3%   |   0%    |    100%    |
| Time Manipulation - V25         |    NA     |  58.7%  |  100%  |    NA    |  38.9%  |   65.3%    |
| Unchecked Low Calls - V15       |    NA     |  55.0%  | 76.6%  |  48.9%   |  33.3%  |   96.4%    |

- False Positive (the number of bugs reported by the tool that actually do not exist)

| Category                        | Manticore | Mythril | Oyente | Securify | Slither | Smartcheck |
| ------------------------------- | :-------: | :-----: | :----: | :------: | :-----: | :--------: |
| Access Control / tx.origin - V8 |    NA     |    0    |   NA   |    NA    |    4    |     3      |
| Arithmetic - V6                 |     9     |   17    |  947   |    NA    |   NA    |     3      |
| Front Running / TOD - V24       |    NA     |   NA    |   32   |   121    |   NA    |     NA     |
| Reentrancy - V1                 |     6     |   54    |   0    |    12    |   79    |     0      |
| Time Manipulation - V25         |    NA     |   12    |   0    |    NA    |   12    |     0      |
| Unchecked Low Calls - V15       |    NA     |    0    |   10   |    0     |    0    |     6      |

- False Negative (reproduction with Slither 0.8.3 and Mythril v0.23.3)

| Category                        | Mythril |    Slither     |
| ------------------------------- | :-----: | :------------: |
| Access Control / tx.origin - V8 |         |    0% -> 0%    |
| Arithmetic - V6                 |         |       NA       |
| Front Running / TOD - V24       |         |       NA       |
| Reentrancy - V1                 |         |    0% -> 0%    |
| Time Manipulation - V25         |         | 38.9% ⬇️ 18.1%  |
| Unchecked Low Calls - V15       |         | 33.3% -> 33.3% |

- False Positive (reproduction with Slither 0.8.3 and Mythril v0.23.3)

| Category                        | Mythril | Slither  |
| ------------------------------- | :-----: | :------: |
| Access Control / tx.origin - V8 |         |  4 -> 4  |
| Arithmetic - V6                 |         |    NA    |
| Front Running / TOD - V24       |         |    NA    |
| Reentrancy - V1                 |         | 79 -> 79 |
| Time Manipulation - V25         |         | 12 ⬆️ 68  |
| Unchecked Low Calls - V15       |         |  0 -> 0  |

###### Performance

- Manticore is the only tool that faces timeouts (average 24m28s / contract, cannot be parallelized) during the experiment. Mythril (1m24s), Oyente (30s), Slither (5s)

| Execution time | Maian | Manticore | Mythril | Oyente | Securify | Slither | Smartcheck |
| -------------- | :---: | :-------: | :-----: | :----: | :------: | :-----: | :--------: |
| Average        | 05:16 |   24:28   |  01:24  | 00:03  |  06:37   |  00:05  |   00:10    |

###### Performance Level

- Level of code at which analysis is performed.
- The √ on Bytecode indicates the analysis is mainly based on the bytecode, while the √  on Solidity code indicates the analysis of slither and SmartCheck is mainly based on solidity source code. But then again, all the above 7 tools can take Solidity code as input.

| Level         | Maian | Manticore | Mythril | Oyente | Securify | Slither | Smartcheck |
| ------------- | :---: | :-------: | :-----: | :----: | :------: | :-----: | :--------: |
| Solidity code |       |           |         |        |          |    √    |     √      |
| Bytecode      |   √   |     √     |    √    |   √    |    √     |         |            |

###### Type (Staic / Dynamic)

- Static program analysis means to examine a contract without executing it
- Dynamic program analysis refers to testing and evaluating a contract at run time, such as deploying and executing it on a private blockchain through certain transactions.
- Formal verification
- [ref1](https://arxiv.org/abs/2005.11613), [ref2](https://publik.tuwien.ac.at/files/publik_278277.pdf), [ref3](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/dse.pdf)

| Type             | Maian | Manticore | Mythril | Oyente | Securify | Slither | Smartcheck |
| ---------------- | :---: | :-------: | :-----: | :----: | :------: | :-----: | :--------: |
| Static analysis  |   √   |     √     |    √    |   √    |    √     |    √    |     √      |
| Dynamic analysis |   √   |    √ ?    |   √ ?   |        |          |         |            |

###### Method Involved in Analysis

- Disassembling means to translate EVM bytecode into better readable assembly language, where machine operations and storage addresses are represented symbolically.
- Decompilation is to transform EVM bytecode to a higher abstraction level (intermediate or Solidity code) to ease data flow analysis.

| Method                  | Maian | Manticore | Mythril | Oyente | Securify | Slither | Smartcheck |
| ----------------------- | :---: | :-------: | :-----: | :----: | :------: | :-----: | :--------: |
| Disassembly             |   √   |     √     |    √    |   √    |    √     |         |            |
| Decompilation           |       |           |         |        |    √     |    √    |            |
| CFG                     |   √   |           |    √    |   √    |          |    √    |            |
| AST                     |       |           |         |        |          |    √    |     √      |
| Symbolic execution      |   √   |     √     |    √    |   √    |          |         |            |
| Constraint solving      |   √   |     √     |    √    |   √    |          |         |            |
| Abstract interpretation |       |           |         |        |    √     |    √    |            |
| Horn logic              |       |           |         |        |    √     |         |            |
| Model checking          |       |           |         |        |          |         |            |
| fuzzing                 |       |           |         |        |          |         |            |

#### Insights

- There is a greate difference between the vulnerabilities that tools are designed to detect and those actually detected by tools.
- Even if it is actually detected, it may be false positives or incorrectly reported as another type of vulnerabilities.
- Current state-of-the-art tools are not able to detect two vulnerabilities from [DASP10](https://dasp.co/): Bad Randomness and Short Addresses.
- Tools underperform to detect vulnerabilities in three categories: Access Control, Denial of service, and Front running.
- Suggest the combination of Mythril and Slither. This combination detects 42 (37%) unique vulnerabilities.
- Oyente has the highest number of false positives when compared to Mythril, Securify, and Smartcheck.
- It is far from being the case that tools yield low false positives and false negatives.

#### Reference

- [A Survey of Tools for Analyzing Ethereum Smart Contracts](https://publik.tuwien.ac.at/files/publik_278277.pdf)
- [Empirical Review of Automated Analysis Tools on 47,587 Ethereum Smart Contracts](https://arxiv.org/pdf/1910.10601.pdf)
- [Towards Safer Smart Contracts: A Survey of Languages and Verification Methods](https://arxiv.org/pdf/1809.09805.pdf)
- [A Survey on Ethereum Systems Security: Vulnerabilities, Attacks and Defenses](https://arxiv.org/pdf/1908.04507.pdf)
- [Defining Smart Contract Defects on Ethereum](https://arxiv.org/pdf/1905.01467.pdf)
- [Empirical Vulnerability Analysis of Automated Smart Contracts Security Testing on Blockchains](https://arxiv.org/pdf/1809.02702.pdf)
- [A Massive Analysis of Ethereum Smart Contracts Empirical Study and Code Metrics](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8733785)
- [How Effective are Smart Contract Analysis Tools? Evaluating Smart Contract Static Analysis Tools Using Bug Injection](https://arxiv.org/pdf/2005.11613.pdf)
