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
5. 小结：该篇论文的贡献在于提高了mythril对于函数组合调用产生的漏洞的检测速度，缓解了组合爆炸。在该论文的evaluation中，最深的depth-n函数组合深度为3层。mythril在depth-2时，平均检测时间就在20分钟了。
6. 基于该论文的future work
   - targeted symbolic execution。该论文没有改动mythril的核心实现，只是在depth-n的函数组合调用之间，使用了state dependency引导了一下 如何选择下一个被执行的函数。也许能使用targeted symbolic execution更改mythril的核心实现，基于state dependency等静态分析得到的信息，不光指导depth-n函数组合，也指导mythril函数内部执行的路径选择。
   - 扩大这些工具的检测粒度。针对mythril，如果分析对象是单个文件里有多个合约，mythril只分析最后一个合约，且没有支持multi-file import、父子合约的继承。
7. 另：根据[A Survey of Languages and Verification Methods](https://arxiv.org/pdf/1809.09805.pdf)，mythril被分进了verification，是model-based verification。Q：mythril属于dynamic analysis？verification？A：mythril是动态符号执行，用fuzz+约束求解器找test case，约束有两方面，一方面是路径约束，一方面是漏洞特征的model。漏洞特征model以及SMT solver使得mythril涉及了verification。

#### 6.24

###### 《Verification of Ethereum Smart Contracts: A Model Checking Approach》

1. [论文地址](http://www.ijmlc.org/vol10/977-AM0059.pdf)
2. 该论文的方法
   1. 预先定义了一些表示状态的结构，记录智能合约执行状态，例如[0xAA(100, 1), 0xBB(130, 2)]，表示0xAA地址有100 ether和1 token，0xBB有130 ether和2 token
   2. 遍历AST，获得状态（1）
   3. 生成CFG，基于CFG的符号执行+数据流和控制流分析，获得状态（2）
   4. 如果状态（1）和状态（2）完全一致（完全一致/相互不冲突），则认为智能合约可信
3. 小结：猜测该论文的符号执行体现在它预先定义的表示合约状态的数据结构[0xAA(100, 1), 0xBB(130, 2)]。参考价值不大

###### 《ETHPLOIT: From Fuzzing to Efficient Exploit Generation against Smart Contracts》

1. [论文地址](https://wcventure.github.io/FuzzingPaper/Paper/SANER20_ETHPLOIT.pdf)，[疑似源码](https://github.com/zqzqz/contract-fuzzer)
2. 动态，本地ganache部署执行，用slither指导fuzzing，站在attacker的视角，针对合约生成可利用的漏洞用例（transaction/fuction sequence with transaction/fuction payload/calldata/args），无误报，平均2秒生成一个漏洞用例
3. 现有符号执行方法的不足
   - Unsolvable Constraints。solver难以求解涉及加密函数/哈希值（keccak256）的路径条件
   - Blockchain Effects。把区块号、timestamp等区块属性视作普通的全局变量，不合适，例如block.timestamp应该是最近的时间戳，而非夸张的未来的时间戳
4. 该论文的改进：用fuzz而非符号执行，生成input candidates而非求解执行路径
   - static taint analysis，指导test case (transaction sequences)的生成，排除无价值的input candidates，最小化搜索空间（基于slither）
   - dynamic seed strategy，解决unsolvable constraints问题。seed作为函数入参，是input candidate。根据前序transaction的执行过程，将前序被执行函数的入参、状态变量等runtime values作为反馈，动态扩展seed，以便从执行历史中找到满足加密函数的函数入参
   - instrumented EVM，解决Blockchain Effects的问题。手动配置区块属性（每一笔交易的timestamp），确保手动配置的区块属性是合理的。（该论文用的EVM是ganache，确实有可能手动配置区块属性）
5. 该论文的方法
   1. 前提：该论文认为被成功利用的漏洞，按照attack的结果可以分成三大类：Balance Increment、Self-destruction、Code Injection，这三类attack过程都触发了外部函数调用： currency transfer、self-destruction、execution of external code，则该论文构造的test case (transaction sequences)应满足两个条件（**<u>此处存疑？</u>**）：
      - 有一笔critical transaction的执行路径，至少触发了上述三种外部函数调用的一种（external calls are the only way to trigger exploits）
      - 在critical transaction之前，有一系列transaction修改了合约的state
   2. Static Analysis (基于slither, data dependency and control dependency)
      - taint sources: state variables, function arguments, blockchain properties
      - taint sinks: state variables (not destructed when function returns) and external calls (i.e., send, transfer, call, callcode, delegatecall, selfdestruct)
   3. Test Case Generation (based on static analysis and feedback): generate transaction/fuction sequence with payload/calldata/args
      - Build Taint Relation Graph
      - Function Selection 。类似《MPro: Combining Static and Symbolic Analysis for Scalable Testing of Smart Contract》多个函数组合调用，选出k个function tx。不同的是，该论文的k可以=1
      - argument generation。with probability `p` to be generated randomly; with probability `1−p` to be generated from seed set
      - blockchain property generation。msg.sender、msg.value、block.timestamp
   4. Test Case Execution
      -  instrumented EVM configures accounts
      -  instrumented EVM configures block properties
   5. Trace Analysis
      - analyze each execution trace. If the <u>exploit detector</u> identifies an exploit, ETHPLOIT reports the current test case as a valid exploit. Exploit detector detail:
        - Balance Increment:  if the balance of attackers’ accounts increases
        - Self-destruction: if the opcode SELFDESTRUCT is in the execution trace
        - Code Injection: if the destination of opcodes CALLCODE and DELEGATECALL is attackers' address
      - analyze coverage as part of the feedback
   6. Feedback Handling
      - Coverage
      - Dynamic seed (filter the seeds with type-matching and taint contraint)
   7. Repeat Step 3 - Step 6
6. smart contract的变量包括4类，该论文的fuzz覆盖到了这4类变量
   - 参数入参 - fuzzing argument generation
   - local variable 
   - state variable - transaction sequence / function selection
   - block effect /block property - instrumented EVM / blockchain property generation
6. 该工具可检测的4种漏洞（<u>**待查？**</u>）
   - TimestampDependency
   - BlockNumberDependency
   - UnhandledException
   - Reentrancy
8. 小结：fuzz，生成了能触发漏洞的用例，可以指示利用漏洞攻击的结果是什么（3类），但无法指示漏洞的具体类型。