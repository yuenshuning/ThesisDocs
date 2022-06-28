# Survey on Analysis Tools
There are many smart contract analysis tools listed in [Analysis Tools.md](./Analysis Tools.md). Not all the identified tools are well suited for the survey. Only the tools that met the following inclusion criteria were included in this survey.

1. Public Available and CLI
2. Compatible Input: The tool takes as input a Solidity contract, rather than only consider EVM bytecode.
3. Only Source: The tool requires only the source code of the contract, rather than test suite or contracts annotated with assertions.
4. Vulnerability Finding: The tool identifies vulnerabilities or bad practices in contracts, rather than only visualize control flow graphs.

#### Evaluation Matrix

- [Effectiveness] How precise the analysis tools are in detecting known vulnerabilities
- [Production] How many vulnerabilities are present in the Ethereum blockchain
- [Performance / Efficiency] How long do the tools require to analyze the smart contracts?

#### Test Dataset

- Contracts with know vulnerabilities: [A Survey on Ethereum Systems Security: Vulnerabilities, Attacks and Defenses](https://arxiv.org/pdf/1908.04507.pdf)
- Real contracts on etherscan

#### Conclusion

Current state-of-the-art is not able to detect two vulnerabilities from [DASP10](https://dasp.co/): Bad Randomness and Short Addresses. 

#### Reference

- [A Survey of Tools for Analyzing Ethereum Smart Contracts](https://publik.tuwien.ac.at/files/publik_278277.pdf)
- [Empirical Review of Automated Analysis Tools on 47,587 Ethereum Smart Contracts](https://arxiv.org/pdf/1910.10601.pdf)
- [Towards Safer Smart Contracts: A Survey of Languages and Verification Methods](https://arxiv.org/pdf/1809.09805.pdf)
- [A Survey on Ethereum Systems Security: Vulnerabilities, Attacks and Defenses](https://arxiv.org/pdf/1908.04507.pdf)
