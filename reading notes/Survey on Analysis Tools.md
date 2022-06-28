# Survey on Analysis Tools
There are many smart contract analysis tools listed in [Analysis Tools.md](./Analysis Tools.md). Not all the identified tools are well suited for the survey. Only the tools that met the following inclusion criteria were included in this survey.

1. Public Available and CLI
2. Compatible Input: The tool takes as input a Solidity contract, rather than only consider EVM bytecode.
3. Only Source: The tool requires only the source code of the contract, rather than test suite or contracts annotated with assertions.
4. Vulnerability Finding: The tool identifies vulnerabilities or bad practices in contracts, rather than only visualize control flow graphs.
4. Classic and original: The tool should be a classic original tool, rather than the fine-tuning based on a framework.

#### Evaluation Matrix

- [Effectiveness] How precise the analysis tools are in detecting known vulnerabilities
- [Production] How many vulnerabilities are present in the Ethereum blockchain
- [Performance / Efficiency] How long do the tools require to analyze the smart contracts?

#### Test Dataset and Tool

- Dataset: contracts with know vulnerabilities: [A Survey on Ethereum Systems Security: Vulnerabilities, Attacks and Defenses](https://arxiv.org/pdf/1908.04507.pdf), [SWC](https://swcregistry.io/)
- Dataset: real contracts on etherscan
- Tool: [SmartBugs](https://github.com/smartbugs/smartbugs)

#### Conclusion

##### Effectiveness

- Current state-of-the-art tools are not able to detect two vulnerabilities from [DASP10](https://dasp.co/): Bad Randomness and Short Addresses.
- Tools underperform to detect vulnerabilities in three categories: Access Control, Denial of service, and Front running.
- Suggest the combination of Mythril and Slither. This combination detects 42 (37%) unique vulnerabilities.
- Oyente has the highest number of false positives when compared to Mythril, Securify, and Smartcheck.
- It is far from being the case that tools yield low false positives and false negatives.

##### Production

- No tool can find all the vulnerabilities. Should extend the scope of vulnerabilities (combine static with dynamic analysis)

| Category            | Maian | Manticore | Mythril | Oyente | Securify | Slither | Smartcheck |
| ------------------- | :---: | :-------: | :-----: | :----: | :------: | :-----: | :--------: |
| Access Control      |  44   |    47     |  1076   |   2    |   614    |  2356   |    2356    |
| Arithmetic          |   0   |    102    |  18515  | 34306  |    0     |    0    |    7430    |
| Bad Randomness      |   0   |     0     |    0    |   0    |    0     |    0    |     0      |
| Denial of Service   |   0   |     0     |    0    |  880   |    0     |  2555   |   11621    |
| Front Running       |   0   |     0     |  2015   |   0    |   7217   |    0    |     0      |
| Reentrancy          |   0   |     2     |  8454   |  308   |   2033   |  8764   |    847     |
| Short Addresses     |   0   |     0     |    0    |   0    |    0     |    0    |     0      |
| Time Manipulation   |   0   |    90     |    0    |  1452  |    0     |  1988   |     68     |
| Unchecked Low Calls |   0   |     4     |   443   |   0    |   592    |  12199  |    2867    |
| Unknown Unknows     |  135  |   1032    |  11126  |   0    |   561    |  9133   |   14113    |
| Total               |  179  |   1203    |  22994  | 34764  |   8781   |  22269  |   24906    |

###### Performance

- Manticore is the only tool that faces timeouts (average 24m28s / contract, cannot be parallelized) during the experiment. Mythril (1m24s), Oyente (30s), Slither (5s)

| Execution time | Maian | Manticore | Mythril | Oyente | Securify | Slither | Smartcheck |
| -------------- | :---: | :-------: | :-----: | :----: | :------: | :-----: | :--------: |
| Average        | 05:16 |   24:28   |  01:24  | 00:03  |  06:37   |  00:05  |   00:10    |

#### Reference

- [A Survey of Tools for Analyzing Ethereum Smart Contracts](https://publik.tuwien.ac.at/files/publik_278277.pdf)
- [Empirical Review of Automated Analysis Tools on 47,587 Ethereum Smart Contracts](https://arxiv.org/pdf/1910.10601.pdf)
- [Towards Safer Smart Contracts: A Survey of Languages and Verification Methods](https://arxiv.org/pdf/1809.09805.pdf)
- [A Survey on Ethereum Systems Security: Vulnerabilities, Attacks and Defenses](https://arxiv.org/pdf/1908.04507.pdf)
- [Defining Smart Contract Defects on Ethereum](https://arxiv.org/pdf/1905.01467.pdf)
- [Empirical Vulnerability Analysis of Automated Smart Contracts Security Testing on Blockchains](https://arxiv.org/pdf/1809.02702.pdf)
- [A Massive Analysis of Ethereum Smart Contracts Empirical Study and Code Metrics](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8733785)
