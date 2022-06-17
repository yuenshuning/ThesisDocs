# Reading Notes

#### 6.10

###### Formal verification Overview

1. Securify：有论文，https://github.com/eth-sri/securify2，https://arxiv.org/pdf/1806.01143.pdf
2. Oyente：有论文，https://github.com/melonproject/oyente

###### Dynamic Analysis Overview

1. Manticore，有论文，trailofbits的，https://arxiv.org/pdf/1907.03890.pdf。完善。
2. Mythril：开源，无论文，https://github.com/ConsenSys/mythril，https://mythril-classic.readthedocs.io/en/develop/module-list.html。完善。EVM、动态、符号执行+fuzz+SMT Z3求解器、不光能分析本地源码，还能分析链上的合约。
3. MAIAN：开源，有论文，https://github.com/ivicanikolicsg/MAIAN，https://arxiv.org/pdf/1802.06038.pdf。个人，不再维护。只有3个检测项，Z3求解器。

###### Static Analysis Overview

1. Slither：有论文，https://github.com/crytic/slither#publications。完善。扩展性强，有丰富的extension论文：在slither之上加了符号执行；基于slither构建storage dependency graph；22年的文章在slither的基础上结合Symbolic evaluation with Value summary analysis做State inconsistency方面的漏洞检测，SI主要就两个漏洞，重入和Transaction Order Dependence（attacker提高gas limit以影响两笔交易的执行顺序，先提交的tx被后打包执行）
2. SmartCheck：有论文，https://github.com/smartdec/smartcheck、https://orbilu.uni.lu/bitstream/10993/35862/3/smartcheck-paper.pdf。个人，不再维护。把代码语句转成了一棵XML parse tree，用xpath写matching rules

#### 6.17

###### 《MPro: Combining Static and Symbolic Analysis for Scalable Testing of Smart Contract》

1. [论文地址](https://arxiv.org/pdf/1911.00570.pdf)，[源码](https://github.com/QuanZhang-William/M-Pro)
2. 动静态结合，用slither改进了mythril。该论文关注的漏洞是**多个函数**的**外部**的组合调用产生的漏洞。
3. 现有工具mythril的不足：该论文指出mythril的在函数相互调用的调用组合方面，剪枝比较简单，比如某个函数有revert、suicide操作符，或者这个函数整个执行过程没有更改状态变量，那么在函数组合的时候，就不会把这个函数考虑进去，仅此而已。
4. 该论文的改进：给mythril的depth-n组合调用加了一个条件。
   - Q：一个函数执行完，如何选择下一个函数，如何选择branch的引导条件？A：状态变量的RAW (Read After Write) dependency。只有存在至少一个R函数对W函数有RAW依赖，W函数才会被执行，而且W函数执行完后，下一个执行的函数一定是对W函数有RAW依赖的R函数。
   - Q：这个RAW dependency是怎么构建的？A：基于slither。slither输出结果包括了state dependency，每个函数读了哪些、写了哪些状态变量。
5. 总结：该篇论文的贡献在于提高了mythril对于函数组合调用产生的漏洞的检测速度，缓解了组合爆炸。在该论文的evaluation中，最深的depth-n函数组合深度为3层。mythril在depth-2时，平均检测时间就在20分钟了。
6. 基于该论文的future work
   - targeted symbolic execution。该论文没有改动mythril的核心实现，只是在depth-n的函数组合调用之间，使用了state dependency引导了一下 如何选择下一个被执行的函数。也许能使用targeted symbolic execution更改mythril的核心实现，基于state dependency等静态分析得到的信息，不光指导depth-n函数组合，也指导mythril函数内部执行的路径选择。
   - 扩大这些工具的检测粒度。针对mythril，如果分析对象是单个文件里有多个合约，mythril只分析最后一个合约，且没有支持multi-file import、父子合约的继承。
7. 另：根据[A Survey of Languages and Verification Methods](https://arxiv.org/pdf/1809.09805.pdf)，mythril被分进了verification，是model-based verification。Q：mythril属于dynamic analysis？verification？A：mythril是动态符号执行，用fuzz+约束求解器找test case，约束有两方面，一方面是路径约束，一方面是漏洞特征的model。漏洞特征model以及SMT solver使得mythril涉及了verification。