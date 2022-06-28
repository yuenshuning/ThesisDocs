# Ethereum-Smart-Contract-Vulnerability
Research around Ethereum smart contract vulnerabilities (Detection/Secure Code Generation)

#### Let's take a look on Tools :}

Artemis: An Improved Smart Contract Verification Tool for Vulnerability Detection, [ref](https://scholars.cityu.edu.hk/en/publications/publication(540f6e82-4908-4408-beef-521a653bcb2f).html)

Defectchecker: Automated Smart Contract Defect Detection by Analyzing EVM Bytecode, [ref](https://ieeexplore.ieee.org/abstract/document/9337195/)

Echidna: effective, usable, and fast fuzzing for smart contracts, [ref](https://dl.acm.org/doi/abs/10.1145/3395363.3404366)

Echidna-Parade: a tool for diverse multicore smart contract fuzzing, [ref](https://dl.acm.org/doi/abs/10.1145/3460319.3469076)

Ethainter: A Smart Contract Security Analyzer for Composite Vulnerabilities, [ref](https://dl.acm.org/doi/abs/10.1145/3385412.3385990) Dedaub公司未开源

EthIR: A Framework for High-Level Analysis of Ethereum Bytecode, [ref](https://link.springer.com/chapter/10.1007/978-3-030-01090-4_30)

👉 Ethploit: From Fuzzing to Efficient Exploit Generation against Smart Contracts
[seemingly code](https://github.com/zqzqz/contract-fuzzer), [paper](https://wcventure.github.io/FuzzingPaper/Paper/SANER20_ETHPLOIT.pdf)
动态，本地ganache部署执行，用slither指导fuzzing，站在attacker的视角，针对合约生成可利用的漏洞用例（transaction/fuction sequence with

👉 HoneyBadger: The Art of The Scam: Demystifying Honeypots in Ethereum Smart Contracts
[code](https://github.com/christoftorres/HoneyBadger), [paper](https://arxiv.org/pdf/1902.06976.pdf)
An Oyente-based tool that employs symbolic execution and a set of heuristics to pinpoint honeypots (appear to look vulnerable but actually not) in smart contracts

MadMax: surviving out-of-gas conditions in Ethereum smart contracts, [ref](https://dl.acm.org/doi/abs/10.1145/3276486)

👉 MAIAN: Finding The Greedy, Prodigal, and Suicidal Contracts at Scale
[code](https://github.com/ivicanikolicsg/MAIAN), [paper](https://arxiv.org/pdf/1802.06038.pdf)
An Oyente-based tool, dynamic analysis，只有3个检测项，Z3求解器。

👉 Manticore: A User-Friendly Symbolic Execution Framework for Binaries and Smart Contracts
[code](https://github.com/trailofbits/manticore)，[paper](https://arxiv.org/pdf/1907.03890.pdf)
Symbolic execution finding execution paths in EVM bytecode that lead to vulnerabilities, developed by TrailOfBits

MuSC: A Tool for Mutation Testing of Ethereum Smart Contract, [ref](https://dl.acm.org/doi/abs/10.1109/ASE.2019.00136)

👉 Mythril: Smashing Ethereum Smart Contracts for Fun and Real Profit
[paper](https://github.com/muellerberndt/smashing-smart-contracts)，[code](https://github.com/ConsenSys/mythril)，[user guide](https://mythril-classic.readthedocs.io/en/develop/module-list.html)
EVM、动态、fuzz、SMT Z3求解器、不光能分析本地源码，还能分析链上的合约，concolic analysis混合执行 + taint analysis + control flow checking剪枝搜索空间

NeuCheck: A more practical Ethereum smart contract security analysis tool, [ref](https://onlinelibrary.wiley.com/doi/abs/10.1002/spe.2745)

👉 Oyente: Making Smart Contracts Smarter
[code](https://github.com/melonproject/oyente), [paper](https://www.comp.nus.edu.sg/~prateeks/papers/Oyente.pdf)
Symbolic execution on EVM bytecode

👉 Osiris: Hunting for Integer Bugs in Ethereum Smart Contracts
[code](https://github.com/christoftorres/Osiris), [paper](https://orbilu.uni.lu/bitstream/10993/36757/1/osiris.pdf)
An Oyente-based tool that extends Oyente to detect integer bugs in smart contracts

Porosity:  A Decompiler For Blockchain-Based Smart Contracts Bytecode, [ref](https://infocon.org/cons/DEF%20CON/DEF%20CON%2025/DEF%20CON%2025%20presentations/DEF%20CON%2025%20-%20Matt-Suiche-Porosity-Decompiling-Ethereum-Smart-Contracts-WP.pdf)

Reentrancy Vulnerability Identification in Ethereum Smart Contracts, [ref](https://arxiv.org/pdf/2105.02881.pdf)

ReGuard: Finding Reentrancy Bugs in Smart Contracts, [ref](https://dl.acm.org/doi/abs/10.1145/3183440.3183495)

👉 Securify: Practical Security Analysis of Smart Contracts
[code](https://github.com/eth-sri/securify2)，[paper](https://arxiv.org/pdf/1806.01143.pdf)
Formal verification

sFuzz: An Efficient Adaptive Fuzzer for Solidity Smart Contracts, [ref](https://dl.acm.org/doi/abs/10.1145/3377811.3380334)

👉 Slither: A Static Analysis Framework For Smart Contracts
[code](https://github.com/crytic/slither), [paper](https://github.com/crytic/slither#publications)
Static analysis, developed by TrailOfBits,

SmartAnvil: Open-Source Tool Suite for Smart Contract Analysis, [ref](https://hal.inria.fr/hal-01940287/file/Duca18a-BookChapter-SmartAnvil.pdf)

👉 SmartCheck: Static Analysis of Ethereum Smart Contracts
[code](https://github.com/smartdec/smartcheck), [paper](https://orbilu.uni.lu/bitstream/10993/35862/3/smartcheck-paper.pdf)
个人，不再维护。把代码语句转成了一棵XML parse tree，用xpath写matching rules

Smartian: Enhancing Smart Contract Fuzzing with Static and Dynamic Data-Flow Analyses, [ref](https://softsec.kaist.ac.kr/~jschoi/data/ase2021.pdf)

SmartInspect: Solidity Smart Contract Inspector, [ref](https://www.computer.org/csdl/proceedings-article/iwbose/2018/08327566/12OmNwpGgGD)

SolAnalyser: A Framework for Analysing and Testing Smart Contracts, [ref](https://www.research.ed.ac.uk/en/publications/solanalyser-a-framework-for-analysing-and-testing-smart-contracts)

TokenHook: Secure ERC-20 smart contract, [ref](https://ui.adsabs.harvard.edu/abs/2021arXiv210702997R/abstract)

Vandal: A Scalable Security Analysis Framework for Smart Contracts, [ref](https://ui.adsabs.harvard.edu/abs/2018arXiv180903981B/abstract)

VeriSolid: Correct-by-Design Smart Contracts for Ethereum, [ref](https://aronlaszka.com/papers/mavridou2019verisolid.pdf)

Zeus: Analyzing Safety of Smart Contracts, [ref](http://pages.cpsc.ucalgary.ca/~joel.reardon/blockchain/readings/ndss2018_09-1_Kalra_paper.pdf)

#### Secure Code Generation for Ethereum :}

Building Executable Secure Design Models for Smart Contracts with Formal Methods, [ref](https://ui.adsabs.harvard.edu/abs/2019arXiv191204051X/abstract)

FSolidM: Tool Demonstration: FSolidM for Designing Secure Ethereum Smart Contracts, [ref](https://www.aronlaszka.com/papers/mavridou2018tool.pdf)

iContractML: A Domain-Specific Language for Modeling and Deploying Smart Contracts onto Multiple Blockchain Platforms, [ref](https://dl.acm.org/doi/abs/10.1145/3419804.3421454)

ICML: Domain Specific Language for Smart Contract Development, [ref](https://ieeexplore.ieee.org/abstract/document/9169399/)

Quartz: A Framework for Engineering Secure Smart Contracts, [ref](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2020/EECS-2020-178.pdf)

Secure smart contract generation based on petri nets, [ref](https://link.springer.com/chapter/10.1007/978-981-15-1137-0_4)

#### Greate sites for learning more (advance topic) :}

Vulnerability blog https://blog.sigmaprime.io/
Smart contract weakness classification https://swcregistry.io/
Nicola Atzei Thesis https://iris.unica.it/retrieve/handle/11584/261568/331756/main.pdf
Watch vulnerable contract onchain https://contract-library.com/
Decentralized Application Security Project https://www.dasp.co/#item-1
Solidity Hacks https://solidity-by-example.org/hacks/
