---
timezone: Asia/Shanghai
---


# Kylin

1. 自我介绍  
   rust, web3, layer2   
2. 你认为你会完成本次残酷学习吗？  
   Y

## Notes

<!-- Content_START -->

### 2025.01.06
**Optimism Rollup 概述**  
Optimism 是一种基于 “Optimistic Rollup” 的二层扩展解决方案，其核心理念是利用以太坊等“父”区块链的安全性，通过继承其共识机制（如 PoW 或 PoS）而不提供自身的共识机制。  
这种设计确保了 Optimism 可以在提供高效交易和降低成本的同时，依赖以太坊的安全保障和数据完整性。  

在块存储方面，Optimism 通过压缩格式将 L2 区块数据写入以太坊链上（L1）；使用 EIP-4844 blobs 提交交易，降低了存储成本，同时确保了区块数据的不可篡改性。  
在区块生产中，网络主要依赖一个称为“排序器”（sequencer）的单一角色进行管理。  
排序器负责提供交易确认、状态更新，以及构建和执行 L2 区块，同时将用户交易提交到 L1。为了避免 MEV（最大可提取价值）问题，排序器的内存池为私有，每两秒生成一个区块，无论是否为空块。   

Optimism 支持两种交易路由方式：用户可以直接将交易提交到排序器，从而降低费用，但由于排序器的集中性，这类交易不具备抗审查性；  
另一种方式是通过 L1 提交交易（即存款），这些交易最终被纳入相应的 L2 区块中，并继承了以太坊级别的抗审查能力。  
在区块执行方面，Optimism 的执行引擎可以通过点对点网络同步状态，也可以通过从 L1 数据派生 L2 区块实现抗审查的区块同步。  

Optimism 的跨层桥接功能允许用户在 L2 和 L1 之间转移 ETH 或代币（包括 ERC20 代币）。  
当从 L1 到 L2（即存款）时，交易会在与存款相关的 L1 区块对应的 L2 区块中被记录。  
而从 L2 到 L1（即提款）时，整个过程分为初始化提款、提交提款证明以及故障挑战期后完成提款三个阶段，挑战期通常为 7 天，期间可以通过监控系统识别不正确的提款操作。  

Optimistic Rollup 的状态承诺机制会将状态提交到以太坊（L1），但不会直接提供其有效性的证明。这些状态在 7 天的挑战窗口期内会被视为待处理，若无人挑战，则视为最终承诺；若被挑战，则通过“故障证明”流程验证并替换。  
需要注意的是，挑战不会改变 OP 主网的交易顺序和状态，只会影响已发布的状态承诺。  
目前，Optimism 基金会是 OP 主网上唯一的区块生产者，同时其故障证明机制正随着 EVM 等效性更新进行改进，进一步提升系统的稳定性和安全性。    

### 2025.01.07
Layer 2值得关注的原因如下：  
- Layer 2网络将会更快、更便宜，能够让更多用户得以进入以太坊生态；
- 提前参与Layer 2网络的激励，能够获得奖励；
- 在Layer 2 发展的预期下，用户可将资产迁移至二层网络上，将会有很大概率获得空投；

目前主要有四种技术方案：Optimistic Rollup、ZK Rollup、Plasma、Validium。
![image](https://github.com/user-attachments/assets/18adfd05-cdea-4677-98be-396fc337bf33)  

四大方案各自费用（以上计算前提是以当前Eth价格为2500u，区块gaslimit为30000000，gas费用为30Gwei，平均13秒的出块时间计算， 极限TPS指对应运行环境占领了所有以太坊区块空间(在证明验证上花费 500000 gas)，普通TPS指对应运行环境占领了所有以太坊1/3的区块空间。）  

**ZK Rollup的交易费用**  
在zkSync 中，每笔交易的成本有两个组成部分：  
链下部分（存储 + 证明者成本） ：状态存储和 SNARK（零知识证明）生成的成本。  
链上部分（gas 成本） ：对于每个zkSync 区块，验证者必须支付以太坊 gas 来验证 SNARK，另外每笔交易额外支付约 0.4k gas 来发布状态 。  
（链上部分是一个变量，取决于以太坊网络中当前的 gas 价格。但是，这部分比普通 ETH/ERC20 转账的成本要便宜几个数量级。）  
（1）交易费用地板价  
ZK rollup的交易地板价依赖于eth主网 gas的费用。
链上 gas fee = 每 wei 的价格 * 交易大小 * gas 的费用 * 代币的风险系数    
链下部分 ： SNARK（零知识证明）生成的成本。这部分依赖于硬件资源的使用，因此是不变的。
（2）影响地板价的因素
Rollup的交易地板价依赖于 ETH 主网 calldata 的费用。  

ETH 的 gas 的相关处于草案阶段的 EIP 主要为 EIP4488，该方案将 calldata 非0字节数据由16gas 降低至 3 gas，对 layer2 TPS的影响较大，利好 layer2 的 Rollup，可以大大降低Rollup主网的交易成本，非0字节的数据可以降低为当前的 1/5 的成本不到，0 字节的也可以微微降低（ab，op，zk 等预计都可以下降至目前 1/5 的手续费）。  
（3）费用支付方式   
zkSync 中的转账天然支持“无气体交易”：用户在被转账的代币中支付交易费用。因此，例如，如果您想交易 DAI 稳定币，您无需拥有 ETH 或任何其他代币。只需支付一小部分 DAI 的费用。     
**zkPorter的交易费用**  
目前 github 无 zkPorter 相关代码，由于 zkPorter 不需要链上数据可用性，预计成本将大大降低。    
主要为链下成本，交易可以控制在 1 到 3 美分的恒定费用。  
### 2025.01.08
在zkSync 2.0中，L2 状态将分为 2 个方面：具有链上数据可用性的 ZK Rollup 和具有链下数据可用性的 zkPorter。   
![image](https://github.com/user-attachments/assets/421cfd66-493b-499f-8d33-dc8552ff4e03)
这两部分将是可组合和可互操作的：ZK Rollup 端的合约和账户将能够与 zkPorter 端的账户无缝交互。从用户的角度来看，唯一明显的区别是 zkPorter 账户的费用减少了 100 倍。  
zkPorter 账户的数据可用性将由 zkSync 代币持有者（称为监护人）保护。他们将通过签署区块来跟踪 zkPorter 端的状态，以确认 zkPorter 帐户的数据可用性。  
监护人使用 zkSync 代币参与权益证明 (PoS)，因此任何数据可用性故障都将导致他们被削减。这为数据可用性提供了加密经济保证。 需要注意的是，zkSync 中的 PoS 比侧链等其他系统中的 PoS 安全得多。这是因为 zkSync 监护人本质上是无法窃取资金。他们只能冻结 zkPorter 状态（冻结他们自己的权益）。 每个用户都可以自由选择自己的安全阈值。任何想要所有链上可用数据的用户都可以完全留在Rollup,使用ZK Rollup账号。  
**Arbitrum Gas 机制**  
Arbgas 费用将根据用户与 Arbitrum 的交互方式而有所不同，但下表可用作一般参考：  
![image](https://github.com/user-attachments/assets/a87ad017-135c-458d-b48c-eb26a4fa2621)   

**optimism Gas 机制**  
optimism 交易中的两个成本来源：L2 执行费和 L1 数据/安全费。   
（1）L2 执行费  
就像在以太坊上一样，Optimism 上的交易必须为他们使用的计算量和存储量支付gas 。每笔 L2 交易都会支付一定的 执行费用，等于交易使用的 gas 数量乘以交易附带的 gas 价格。这也是以太坊的收费方式。    
这是（简单的）公式： l2_execution_fee = transaction_gas_price * l2_gas_used  
使用的 L2 气体量取决于您尝试发送的特定交易，交易在 Optimism 上使用的 gas 量通常与在 Ethereum 上的大致相同。  
（2）L1 数据费  
Optimism 与以太坊不同，因为 Optimism 上的所有交易也都发布到以太坊。此步骤对于 Optimism 的安全属性至关重要，因为这意味着同步 Optimism 节点所需的所有数据始终在以太坊上公开可用。这就是使 Optimism 成为 L2 的原因。  
 
Optimism 上的用户必须支付向以太坊提交交易的费用。称之为L1 数据费用 ，这是 Optimism（和其他 L2）与以太坊之间的主要差异。由于以太坊上的 gas 成本非常昂贵，因此 L1 数据费用通常会在 Optimism 上占据交易的总成本。该费用基于四个因素：  
以太坊当前的gas价格。  
将交易发布到以太坊的 gas 成本。这交易长度的大小（以字节为单位）成比例。    
以gas计价的固定费用。  
一种动态的间接费用，按固定数字支付的 L1 费用。  
公式： L1_data_fee = L1_gas_price * (tx_data_gas + fixed_overhead) * dynamic_overhead  

### 2025.01.09
trainning wheels: a phase of central control during the development of rollup systems, which should be eventually removed to fully inherit the security properties of the base layer.    
**Vitalik's proposed milestones**   
link:https://ethereum-magicians.org/t/proposed-milestones-for-rollups-taking-off-training-wheels/11571  
#### Stage 0: full training wheels
Requirements:
- The project should call itself a rollup.
- All rollup transactions should go on-chain.
- There should exist a “rollup full node”: an independently runnable software package that can read the L1 chain, extract and the rollup chain, and compute the current state of the rollup chain. If it disagrees with a rollup state root posted into the contract, it should give an alarm.
- There should be machinery that allows users to either post rollup transactions or at least ensure a withdrawal of their assets with no cooperation from the operator. That is, the operator cannot freeze or steal users’ assets by censoring users; their only possible tool for doing so must be to post a false state root.
- It’s okay if the on-chain mechanism for posting new state roots is simply a multisig, with no active fraud proof or validity proof whatsoever.
#### Stage 1: limited training wheels
Requirements:
- There must be a running fraud proof or validity proof scheme, which has the practical authority to accept or reject which state roots get accepted by the rollup contract.
- There can exist a multisig-based override mechanism (“security council”) that can override the fraud proof or validity proof system’s outputs and post state roots, to be used in case the proof system code is bugged. However:
      - The multisig must be 6 of 8 or stricter (that is, >= 8 participants AND >= 75% threshold)
      - At least a quorum-blocking group (that is, enough participants to prevent the multisig from acting) must be outside the organization that is running the rollup.
- There can exist an upgrade mechanism, but if it has a lower threshold than the multisig, upgrades must have a mandatory activation delay of at least 7 days or the maximum length of the fraud proof game, whichever is longer. The goal of this rule is to ensure that the upgrade mechanism cannot be used to intervene in real-time disputes.
#### Stage 2: no training wheels
Requirements:  
- In the event that code does not have bugs, there must not be any group of actors that can, even unanimously, post a state root other than the output of the code  
This somewhat awkward phrasing (“IF the code does not have bugs, THEN no one can override it”) is meant to permit use of security councils in ways that are clearly limited to adjudicating undeniable bugs, such as the following:
- The rollup uses two or more independent implementations of its state transition function (eg. two distinct fraud provers, two distinct validity provers, or one of each), and the security council can adjudicate only if they disagree - which would only happen if there is a bug
- If someone submits a transaction or series of transactions that contains two valid proofs for two distinct state roots after processing the same data (ie. “the prover disagrees with itself”), control temporarily turns over to the security council
- If no valid proof is submitted for >= 7 days (ie. “the prover is stuck”), control temporarily turns over to the security council
- Upgrades are allowed, but must have a delay of >= 30 days


**L2Beat's work**  
directions explored: a simple three-stages rating, a letter rating with plus and minus signs to express finer details, a star system, and a numeric score system.  
### 2025.01.10
framework  
#### Stage 0 requirements
- Does the project call itself a rollup?
- Are L2 state roots posted on L1?
- Does the project provide Data Availability (DA) on L1
- Is software capable of reconstructing the rollup’s state source available?

#### Stage 1 requirements
- Does the project use a proper proof system?
- Are there at least 5 external actors that can submit a fraud proof?
   - A fraud proof system requires at least one honest actor to verify the correctness of proposed state roots and potentially dispute them. For Stage 2 the proof system must be open to all participants, but for Stage 1 we allow an allowlist. The fraud proof system must allow a minimum of 5 external actors to perform this task.
- Can the users exit without the operator’s coordination?
   - The system should be designed so that user withdrawals cannot be blocked by the rollup operators. The rollup must implement mechanisms that allow users to exit independently, ensuring they can always access and control their assets.
- Do users have at least 7 days to exit in case of unwanted upgrades (Security Council and governance excluded)?
- Is the Security Council properly set up?

#### Stage 2 requirements
- Is the fraud proof system permissionless?
    - In this stage, the fraud proof system should be fully decentralized and open to everyone. This means that anyone, not just a set of allowlisted actors, should be able to submit fraud proofs. This is a key requirement to ensure that the system is not controlled by a limited set of entities and instead is subject to the collective scrutiny of the entire community.

- Do users have at least 30 days to exit in case of unwanted upgrades?
Users should be provided with at least 30 days to exit the system in case of unwanted upgrades, including upgrades initiated by a DAO. This ample time frame allows users to react to significant changes in the system that they may not agree with and withdraw their assets if needed. One exception that we make is given the existence of a on chain bug detection system (e.g. two valid contradicting zk proofs) instant upgrades are allowed for detected bugs.

- Is the Security Council restricted to act only due to errors detected on chain?
In the final stage of rollup development, the power of the Security Council should be highly limited. It should only be able to intervene in the case of adjudicable soundness errors, which are serious flaws in the system that could cause significant harm if not addressed. By restricting the council’s actions to these types of errors, the system becomes more decentralized and the trust placed in the Security Council is reduced. This moves the rollup further towards the ideal of trust minimization, where the code itself is the ultimate authority. An example of this feature is present in the Polygon zkEVM contracts, where the rollup goes in “Emergency Mode” if two different valid proofs can be submitted using the same batches.

### 2025.01.11
link: https://www.cnblogs.com/linguanh/p/16535408.html 
 Op 的程序组件
- 合约，这些会被部署在 L1 公链上面，由 L2 组件或用户来调用，包含不限于有：
   - L2 侧链，基于 geth 源码改造的链，运行在 Op 生态里；
   - L1StandardBridge.sol 垮链桥合约，用来处理充值 Token 到 Op 地址或从 Op 地址提现到 L1 地址 所用；
   - CanonicalTransactionChain.sol 规范处理 L2 --> L1 的交易，下面简称 CTC；
   - L1CrossDomainMessenger.sol 跨链信使合约，里面主要编写进行了各种要触发跨链事件的函数。
- DataTransportLayer，定时扫描 L1 区块，从中获取到 TransactionEnqueued 事件，并存储到 LevelDB 数据库；
- Sequencer：
   - 接受用户发来 L2 的交易；
   - 定期从数据库中获取 DataTransportLayer 存储的 TransactionEnqueued 事件数据，并把交易在 L2 链中执行，使之正常被打包到 L2 区块中；
- Batch-Submitter，定期从 L2 区块中将交易数据以打包的形式组装到交易：
   - 打包批量交易 txBatch 提交到 L1 的 CTC 合约；
   - 打包批量状态 stateBatch 提交到 L1 的StateCommitmentChain.sol
   - 之后这些交易进入等待挑战窗口，挑战方式就是欺诈证明；
- Relayer，定时从 L2 区块中过滤交易中的 SentMessage 事件数据：
   - 判断当前交易是否过了挑战时间；
   - 为此交易生成证明，调用 L1 上的 L1CrossDomainMessenger.relayMessage 函数，使之完成合约检查然后在内部调用目标合约，最终在 L1 完成 L2 交易的最终目的；
它们的组合通讯流程图如下：
![image](https://github.com/user-attachments/assets/fc9aa600-6072-44c6-8b67-e4fd8ca9dc9e)

注:目前所有的 Op 组建，都由官方运行着，欺诈证明还在完善。用户必须要相信官方不会做恶。
如何使用 Op
使用 Op 网络分两种情况：
- 直接使用原生 Token 进行交易，即以太坊，那么：
需要先在 L1 访问 L1StandardBridge.sol 进行充值到 Op；  
充值结束后，到账了，可以进行 Op 网络内的交易活动；  
提现到 L1 的地址；  
流程到这里闭环  
- 其他协议，比如 ERC-20： 
先去 Op 网络部署对应的合约；  
在 L1 的 L1StandardBridge.sol 充值 Token 到 L2 地址；  
到账后，便可自由交易。提现动作和 ETH 的一样。

### 2025.01.12
link https://www.cnblogs.com/linguanh/p/16621521.html  
OP 本质是个大型的 DApp，我们要使用它，就要先从以太坊的主网充值 Token 进去。  
用户在 OP 里面进行了系列的交易动作后，需要把 Token 转回到主网，才能与其他的 DApp 的交互或主网转账。因此对应地，OP 提供了提现 Token 到主网的功能。  
提现的原子性  
虽然在 OP 中的交易都直接发生在 OP 的网络中，比如转账的地址是 OP 网络中的以太坊地址。  
但是所有的交易都会被同步到以太坊主网中，与 OP 的合约发生实际的主网交互。这就意味着，地址所在 OP 中 Token 余额的变化也会导致主网上的余额变化。  
提现的调用链
用户是提现发起的对象，提现遵循下面的步骤：
- 用户向 OP 的 Sequencer 发起提现交易；
- 这笔交易是一次合约调用交易，指向 L2StanderBridger.sol 中的 withdraw 函数；
- withdraw 函数中会构造最后在主网合约中发起真正提现的函数数据；
- 交易被 OP 网络正常打包；
- 交易被Batch-Submitter 提交到主网 CTC 合约，走正常的挑战机制；
- 挑战期过后，Relayer 为此交易生成证明，调用 L1 上的 L1CrossDomainMessenger.relayMessage 函数，使之完成合约检查然后在内部调用目标合约，最终在 L1 完成 L2 交易的最终目的，用户的 Token 在 L1 地址上得到了提现；
- 提现闭环。

### 2025.01.13
**Optimism Collective 概述**  
Optimism Collective 是由企业、社区和公民组成的合作组织，致力于奖励公共物品并为以太坊构建可持续未来。其目标是通过建立 Superchain 实现标准化和可扩展的去中心化体系。  
**Superchain 产品愿景**  
1. **链的标准化**：支持大规模去中心化与可组合性。  
2. **初始规模**：从 15-50 条链扩展到 1000+ 条链，实现“一链化体验”。  
3. **治理保障**：通过治理保护 Superchain 的安全性。  
4. **可持续增长**：治理驱动创新与发展的良性循环。  

**影响 = 利润**  
Optimism Collective 提倡一种新经济模式：**Impact = Profit**。它的使命是创造一个惠及所有人但不属于任何人的互联网。通过奖励对 Collective 和 Superchain 产生积极影响的行为，实现以太坊生态系统的可持续发展（称为 Ether’s Phoenix）。  

**治理架构**  
Collective 的治理采用双议院制，由 **Token House** 和 **Citizens' House** 构成，实验性地构建民主治理体系。  

#### **Token House**  
- 基于 OP Token 的治理系统。  
- 成员职责包括提交、讨论和投票治理提案。  
- 支持直接投票或委托投票权。  
- 提案类型依据 **Operating Manual** 中的规则。  

#### **Citizens' House**  
- 基于声誉的“一人一票”治理实验。  
- 核心职能是**追溯性公共物品资助（Retro Funding）**，奖励对 Collective 和 Superchain 有积极影响的行为。  
- Retro Funding 的理念是“回顾过去的有用性比预测未来更容易达成一致”。  

**双议院协作**  
Token House 和 Citizens' House 共同努力，通过分工与协作推进 Collective 的愿景。  

**治理文件**  
1. **工作宪法（Working Constitution）**：自 2022 年 4 月生效，阐明 Collective 的核心原则与治理规定。  
2. **操作手册（Operating Manual）**：描述 Token House 的治理流程，并随着 Collective 发展不断更新。  
3. **去中心化里程碑模型**：指导 Collective 的去中心化进程与阶段性目标。  
4. **决策模型图**：展示治理决策的全貌及其相互关系，为实现自治提供框架参考。  

### 2025.01.14
在 Token House 中，OP 持有者负责提交、审议和投票各类 Optimism Collective 治理提案。他们可以通过直接投票给他们的 OP（在将他们的 OP 投票权委托给他们自己的地址之后），或者通过将他们的 OP 投票权委托给符合条件的第三方来实现。具有委托 OP 投票权的地址称为“代表”(“delegates”)。   
在Citizens’ House, Optimism Citizens 负责通过一个名为“追溯性公共物品资助”（Retro Funding）的流程向公共物品建设者分配奖励。参与 Retro Funding 3 的徽章持有者（通过 AttestationStation 智能合约中的条目划分）现在是公民。目前，公民身份是暂时的。公民还负责投票否决升级提案。   
所有 Token 和 Citizens' House 代表都应根据the Rules of Engagement和 Optimist Expectations负责任地行使其权力。  
Proposal Process  提案流程  
两院通过治理提案做出决策。通过投票程序接受或拒绝提案。任何人都可以向治理提交提案。该提案必须是下面列出的有效提案类型之一，并且必须遵循此处描述的投票流程。  
Valid Proposal Types 有效提案类型
所有 v0.3 治理提案必须属于以下类别之一：  
Governance Fund  
Protocol or Governor Upgrade  
Inflation Adjustment  
Director Removal  
Treasury Appropriations  
Code of Conduct Violations  
Representative Removal 
Representative Structure Dissolution  
Rights Protections  
Elections  
Ratification 
Reflection Period (Metagovernance)  

Mission Grants  使命补助金  
Applications to Token House Mission Requests将由拨款委员会审查和选择。基金会任务请求的申请将由基金会审查和选择。所有应用程序都应遵循(github)[https://github.com/ethereum-optimism/ecosystem-contributions/issues?q=is%3Aissue]中每个任务请求中概述的提交流程。  

### 2025.01.16
追溯性公共物品资助（Retro Funding）的理念是，就过去有用的内容比对未来可能有用的内容达成一致更容易。  
这是一系列实验，Citizens’ House成员将剩余协议收入或部分复古融资代币分配给他们认为对 Optimism Collective 和整个超级链产生积极影响的项目。  
这是乐观主义价值观 impact=profit “影响=利润”的核心：对集体的积极影响应该与个人的利润成比例地得到回报。  
![image](https://github.com/user-attachments/assets/250ac1f9-ab5e-4415-9f3c-b5023ff98190)

Retro Funding also provides possible exit liquidity for public goods projects, which opens up a market for early investment in those projects. This means builders can:  
- Be rewarded for their positive contributions without generating direct revenue  
- Raise capital to bootstrap based on the early potential and promise of their project  

Retro Funding has three core components, each with substantial surface area for experimentation.

- Impact scoping: what should the Collective fund? How is it defined and decided on?
- Impact scoring: how does the Citizens’ House evaluate impact? What units, process, or tools do we use?
- Impact settlement: how does voting work?

For the first several rounds of Retro Funding, the Optimism Foundation will decide on scope and voting mechanics with input from the community. Eventually the set of variables around what to fund, how much to fund, and how to vote will be up to the Citizens’ House, with checks and balances from the Token House.  

### 2025.01.17
继 Bedrock 之后，OP Stack 的下一个重大可扩展性改进是引入超级链的概念：共享桥接、去中心化治理、升级、通信层等的链网络，所有这些都构建在 OP Stack 上。
The scalability vision  可扩展性愿景  
- 可扩展的去中心化计算的价值是巨大的……如今的区块链技术不足以满足去中心化网络的需求  
| We very, very much need such a system, but the way I understand your proposal, it does not seem to scale to the required size.  

- 可扩展的去中心化计算的价值是巨大的……
   - 如果链上交易与与中心化后端交互一样便宜
      -  使编写高度可扩展的 Web 应用程序成为可能，而无需接触传统的后端软件堆栈。
      -  在这个大多数应用程序都上链的世界中，更多数据变得可以加密验证。
- …and the decentralized web can still be realized 去中心化网络仍然可以实现

 基本的Superchain概念  
 - Horizontal scalability requires multiple chains… 水平可扩展性需要多个链……
 - …but traditional multi-chain architectures are insufficient …但传统的多链架构还不够
    - 多链”架构的传统方法存在两个基本问题：
       - 每条链都引入了新的安全模型，随着新链被引入生态系统，系统性风险会加剧。
       - 新链的启动成本很高，因为它们需要新的验证器集和区块生产者。
   - 这些问题来自于缺乏单一共享区块链（“L1”链）作为多链系统中所有链（“L2”链）的共享事实来源。
   - 通过使用共享的事实来源，可以：
      -  a) 在所有链上实施标准安全模型；
      -  b) 删除链部署需要一组新验证器的要求，因为每个 L2 链都使用 L1 共识。
- Not multi-chain, not mono-chain… Superchain 不是多链，不是单链……超级链

### 2025.01.18
Superchain概述  
Superchain是一个 L2 链网络，共享安全性、通信层和开源技术堆栈。然而，与多链设计不同，这些链是标准化的，旨在用作可互换的资源。这使得开发人员能够构建以整个超级链为目标的应用程序，并抽象出应用程序运行的底层链。  
![image](https://github.com/user-attachments/assets/af8dca97-d596-45cb-bbb9-b30b25506d53)
Superchain 的属性  
为了让 Optimism 升级为Superchain，它必须具备以下属性：    


|Property 属性  |	Purpose  目的  |
|---|---|
|Shared L1 blockchain  共享L1区块链	| Provides a total ordering of transactions across all OP Chains.提供所有 OP 链上交易的总排序。  |
|Shared bridge for all OP Chains 所有 OP 链的共享桥	| Enables OP Chains to have standardized security properties.使OP链具有标准化的安全属性。  |
|Cheap OP Chain deployment 廉价的OP链部署 | Enables deploying and transacting on OP Chains without the high fees of transacting on L1.允许在 OP 链上部署和交易，而无需支付 L1 交易的高额费用。 | 
|Configuration options for OP Chains OP 链的配置选项 | Enables OP Chains to configure their data availability provider, sequencer address, etc. 使 OP Chain 能够配置其数据可用性提供者、定序器地址等。|
|Secure transactions and cross-chain messages 安全交易和跨链消息| Enables users to safely migrate state between OP Chains.使用户能够在 OP 链之间安全地迁移状态。|

### 2025.01.19  
升级Optimism，成为Superchain
- 将Bedrock bridge升级为链工厂
   Bedrock引入了SystemConfig合约，开始直接用L1智能合约定义一些L2链。这可以扩展为将定义 L2 的所有信息放在 L1 上。包括生成唯一的链ID、区块gas limit等关键配置值等。
  一旦链数据完全在链上，就可以创建一个工厂，为每个链部署配置和所有其他所需的合约。这可以通过使用 CREATE2 使合约地址具有确定性来进一步扩展，这意味着给定链配置，可以确定与该链关联的所有桥地址。这也使得链能够进行交互，而无需部署桥接合约，使（反事实）链部署几乎免费，并允许链继承标准安全属性。
- 使用链工厂导出OP Chain数据
Bedrock引入了L1链衍生的L2链，所有链数据都可以基于L1区块进行同步。随着 L1 链工厂扩展此功能以将所有配置放在链上，Optimism节点应该可以在给定单个 L1 地址和到 L1 的连接的情况下确定性地同步任何OP 链。  
- 无需许可的证明系统即可提款
  在 Bedrock 中，用户提交提款需要一个许可角色（“提议者”角色）。此外，提案者必须按照设定的时间间隔向 L1 提交提案。随着超级链中链数量的增加，这会引入线性开销，甚至由于 L1 资源有限而引入链数量上限。
  为了解决这些问题，可以引入两个功能：
  - 提款声明（又名无许可提案）——允许任何人提交提款（又名提案），而不仅仅是指定的提案者。这将从系统中删除许可角色，使用户能够提交自己的提款消息。
  - 无提交间隔的按需提案——仅当用户需要撤回时才提出撤回声明。这消除了部署新 OP 链时产生的开销。

- 每个 OP 链可配置的定序器
 Bedrock 引入了在 SystemConfig 合约中设置定序器地址的功能。当引入具有自己的 SystemConfig 合约的多个链时，可以启用 OP Chain 部署者配置定序器地址。
  这种可配置的定序器设计称为模块化定序。这使得 OP 链能够由不同的实体进行排序，同时保留标准的安全模型——这是实现排序器去中心化的关键一步。

### 2025.01.20
扩展Superchain增强功能以​​实现愿景
在实现完全可扩展的区块链愿景之前，仍然存在必须解决的重大痛点。预期的痛点包括：  
1. 提款声明依赖于一组值得信赖的链证明者。
2. 跨链交易速度很慢，因为它们需要等待挑战期。
3. 跨链交易是异步的，破坏了执行原子跨链交易（如闪贷）的能力。
4. 将交易发布到超级链是不可扩展的，因为交易数据必须提交到容量有限的 L1。
5. 没有易于使用的框架来构建利用许多 OP 链的可扩展应用程序。
6. 没有易于使用的钱包来管理许多 OP 链上的代币和应用程序。
以下是对未来潜在增强功能的概述，这些增强功能结合起来可以解决这些痛点。

Multi-proof security  多重防护安全  
1. 提款声明依赖于一组值得信赖的链证明者。  
建议的解决方案：可以通过引入无需许可的证明（例如 Cannon）来取代可信的链证明者集，其中争议解决完全在链上进行。然而，完全链上证明的挑战是，如果它们被破坏，则没有后备机制。为了确保它们永远不会失败，可以引入多重证明系统，通过冗余提供安全性。  
Low latency L2 to L2 message passing 低延迟 L2 到 L2 消息传递
2. 跨链交易速度很慢，因为它们需要等待挑战期。
建议的解决方案 有效性证明不存在这个问题。有效性证明没有挑战期，因此可以从一个 OP 链即时提款到下一个链。如果用户需要频繁地在链之间迁移，即使在正常的应用程序执行期间，这一点非常重要。然而，有效性证明通常使用零知识证明（ZKP）来实现，这种方法成本昂贵且容易出现错误。真正实现 ZKP 的量产化，使其成为主要的跨链通信协议，可能需要数年时间。
在 ZKP 投入生产的同时，使用 OP Stack 的模块化证明系统可以实现低延迟的 L2 到 L2 消息传递。通过模块化证明，可以对同一条链使用两个证明系统。这使得使用一个证明系统提供低延迟桥接（牺牲安全性）同时使用另一个证明系统提供高安全性、高延迟桥接成为可能。  
混合多个证明系统使开发人员能够为低值状态提供低延迟桥接，为高值状态提供高延迟桥接。甚至可以通过使用高安全性高延迟桥来证明状态的有效性，将立即桥接的低安全状态转变为高安全状态。该构建块使开发人员能够进行有趣的安全权衡，例如使用高阈值证明证明和高安全性、高延迟的故障证明回退。  
Synchronous cross-chain transactions 同步跨链交易
3. 跨链交易是异步的，破坏了执行原子跨链交易（如闪贷）的能力。
建议的解决方案：通过在两个 OP 链上使用共享排序协议，可以引入同步跨链消息传递并实现原子跨链交互。通过低延迟 L2 到 L2 消息传递以及共享排序的结合，可以执行复杂的交易，例如跨链闪电贷。甚至可以更进一步，创建一个 EVM 抽象，其中各个智能合约（甚至各个存储槽）存在于不同的链上。

### 2025.01.21
Alt-Data availability layer — Alt-DA Protocol Alt-Data 可用性层 — Alt-DA 协议  
4. 将交易发布到超级链是不可扩展的，因为交易数据必须提交到容量有限的 L1。
Alt-DA 链 交易数据在 L1 上提交但不直接提供给 L1 的链，具有数据可用性质询回退。  
用的 Alt-DA 协议能够扩展到 L1 上的可能性之外，因为只有对交易数据感兴趣的用户才会下载 Alt-DA 数据，而在 L1 上，每个以太坊节点都会下载 L1 上的所有交易数据。这意味着 Alt-DA 数据非常便宜。然而，Alt-DA 的安全模型比 L1 差——Alt-DA 链数据可能会暂时不可用，这意味着用户必须退出链。请注意，这种安全模型仍然保证了 Alt-DA 链的安全性，只是不能保证活跃性。  
Alt-DA 协议概述：
- 数据可用性 （DA） 提供商从用户那里接收交易数据。
- 然后，DA 提供商对交易数据进行哈希处理，并将哈希值提交给 Alt-DA 合约。
- 提交哈希值后，DA 提供商会向用户发送证明，证明他们的交易数据包含在哈希值中。DA 提供商可以通过扣留证明（即不将其发送给用户）来行为不端。
- 如果 DA 提供商未向用户发送证明，则用户可以提交 DA 质询。这会强制 DA Provider 将交易数据发布到链上。如果 DA 提供商未在链上提交证明，则哈希值将被删除。这确保了用户始终可以（在质询期之后）同步 Alt-DA 链。
- 如果 L1 拥塞严重，DA 质询期可能会延长。
- 用户还可以提交 L1 交易以从 Alt-DA 链中提款，以切换他们的 DA 提供者。
- Alt-DA 链的结算使用与 Rollup 链几乎相同的故障证明系统，唯一的区别是额外的数据是使用 Alt-DA 合约中最终确定的哈希值从链中得出的。
由于哈希能够将任意大小的数据减少为恒定大小的承诺，并且能够并行化交易数据哈希，因此可以使用 Alt-DA DA 实现数据承诺的近乎完美的水平可扩展性。这意味着可以将大规模可扩展的应用程序（如游戏或社交媒体）放在 Alt-DA 链上。
Multi-chain app frameworks 多链应用程序框架
5. 没有易于使用的框架来构建利用许多 OP 链的可扩展应用程序。
6. 没有易于使用的钱包来管理许多 OP 链上的代币和应用程序。
这不是核心协议的更改，而是可以构建在核心 Superchain 协议之上的工具。这里的建议旨在就如何构建工具来改善部署到超级链的体验提供粗略的直觉。
- Content-addressable 智能合约  这使得合约在所有链上都具有相同的地址。通过这种方式，开发人员可以编写智能合约，这些智能合约被反事实地部署到同一地址的所有 OP 链上。如果 OP 链上的用户想使用他们链上尚不可用的智能合约，他们可以独立部署代码。
- 跨链合约状态管理标准  为智能合约状态如何从一条链迁移到另一条链创建标准，使开发人员能够在多个链上对其应用程序进行分片。此外，此逻辑可用于钱包中以显示用户状态，就好像它们都在同一条链上一样。例如，如果用户的代币被拆分到许多链上，钱包可以使用跨链状态管理逻辑来知道它应该将用户余额显示为他们在所有链上的所有代币余额的总和。
- Superchain RPC 端点   创建一个 RPC 端点，用户可以在其中发送他们的 Superchain 交易，无论他们打算用于哪个 OP 链，使用户能够避免不断切换他们的网络。

### 2025.01.22
OP Stack 是支持 Optimism 的一组软件——目前以 OP 主网背后的软件形式，最终以 Optimism 超级链及其治理的形式出现。  
OP Stack 可以被认为是软件组件，它们要么帮助定义 Optimism 生态系统的特定层，要么在现有层中充当模块的角色。 尽管 OP Stack 目前的核心是运行 L2 区块链的基础设施，但 OP Stack 理论上扩展到底层区块链之上的各层，包括区块浏览器、消息传递机制、治理系统等工具。  
Optimism Bedrock 是 OP Stack 的当前迭代。Bedrock 版本提供了启动生产质量 Optimistic Rollup 区块链的工具。此时，OP Stack 不同层的 API 仍然与堆栈的 Rollup 配置紧密耦合。  

### 2025.01.23
#### Layers  
**Data availability  数据可用性**  
数据可用性层定义了基于 OP Stack 的链的原始输入的发布位置。OP Stack 链可以使用单个 Data Availability 模块来获取其输入数据。由于 OP 堆栈链源自数据可用性层，因此所使用的数据可用性模块对系统的安全模型有重大影响。例如，如果无法再从 Data Availability Layer 检索到某条数据，则可能无法同步链。  
Ethereum DA
以太坊 DA 是目前 OP 堆栈中使用最广泛的数据可用性模块。使用 Ethereum DA 模块时，源数据可以从 Ethereum 区块链上可访问的任何信息中派生。这包括 Ethereum calldata、events 和 4844 数据 blob。  
**Sequencing**  
排序层确定如何收集 OP 堆栈链上的用户交易并将其发布到正在使用的数据可用性层模块。在 OP Stack 的默认 Rollup 配置中，Sequencing 通常由单个专用的 Sequencer 处理。Derivation Layer 中定义的规则通常会限制 Sequencer 将事务保留超过特定时间的能力。未来，Sequencing 将是模块化的，以便链可以轻松选择和更改控制其当前 Sequencer 的机制。  
Single sequencer  单定序器  
OP Stack 的默认 Sequencer 模块是 Single Sequencer 模块，其中专用角色能够充当 Sequencer。Single Sequencer 模块允许管理机制来确定在任何给定时间谁可以充当 Sequencer。  
Multiple sequencer 多定序器  
对 Single Sequencer 模块的一个简单修改是 Multiple Sequencer 模块，其中 Sequencer 在任何给定时间都是从一组预定义的可能角色中选择的。基于单个 OP Stack 的链将能够确定定义可能的 Sequencer 集的确切机制以及从集合中选择 Sequencer 的机制。  
**Derivation**  
派生层定义了如何处理数据可用性层中的原始数据，以形成通过标准 Ethereum Engine API 发送到执行层的已处理输入。Derivation Layer 还可以使用 Execution Layer 定义的当前系统状态来通知原始 input 数据的解析。可以修改 Derivation Layer 以从许多不同的数据源派生 Engine API 输入。派生层通常与数据可用性层密切相关，因为它必须了解如何解析任何原始输入数据。  
Rollup   
Rollup 模块从 Ethereum 区块数据、Sequencer 交易批次、Deposited 交易事件等中派生引擎 API 输入。  
Indexer   
索引器模块是一个派生层模块，当交易发送到数据可用性层模块（如 Ethereum DA）上的特定智能合约、发出事件或修改存储时，它将派生引擎 API 输入。  
**Execution  执行**  
执行层定义了 OP Stack 系统中的状态结构，并定义了改变此状态的状态转换函数。当通过 Engine API 从派生层接收输入时，将触发状态转换。执行层抽象为 EVM 修改或完全不同的底层 VM 打开了大门。  
EVM  
EVM 是一个执行层模块，使用与 Ethereum 虚拟机相同的状态表示和状态转换功能。OP 堆栈的以太坊 Rollup 配置中的 EVM 模块是 EVM 的略微修改版本，它增加了对在以太坊上发起的 L2 交易的支持，并为每笔交易增加了额外的 L1 数据费用，以考虑将交易发布到以太坊的成本。  

### 2025.01.24
**Settlement layer**  
 结算层是外部区块链上的一种机制，用于在这些外部第三方链（包括其他 OP Stack 链）上建立 OP Stack 链（目标）的状态视图。对于每个目标链，在一个或多个外部链上可能有一个或多个 Settlement 机制。结算层机制是只读的，允许第三方链根据目标 OP Stack 链的状态做出决策，这可能会影响他们自己的状态。  
 “结算层”一词起源于结算层机制通常用于处理从区块链中提取 ETH 和代币的事实。这种提款系统首先涉及向某个第三方链证明目标区块链的状态，然后根据该状态处理提款。结算层的核心是让第三方链确信目标链的状态。  
 一旦交易在相应的数据可用性层发布并完成，该交易也会在 OP Stack 链上完成。如果不破坏底层数据可用性层，则无法再对其进行修改或删除。它可能还不被 Settlement Layer 接受，因为 Settlement Layer 需要能够验证交易结果，但交易本身已经是不可变的。  
Attestation-based fault proof  
基于证明的 Fault Proof 机制使用 Optimistic 协议来建立 OP Stack 链的视图。在乐观的结算机制中，提议者实体可以提出他们认为是 OP Stack 链当前有效状态的内容。如果这些提案在一段时间内（“质疑期”）没有失效，则机制会假定这些提案是正确的。特别是在鉴证证明机制中，如果预定义方的某些阈值提供的有效状态证明与提案中的状态不同，则提案可能会无效。这将信任假设至少一个阈值数量的预定义参与者的诚实度。
Fault Proof Optimistic Settlement  
Fault Proof Optimistic Settlement 机制与目前使用的基于鉴证的 Fault Proof 机制基本相同，但它用无需许可的故障证明流程取代了多签挑战者。正确构建的 fault proof 应该能够在分配的质询期内使任何不正确的提案无效。这将对 fault proof 结构的正确性进行信任假设。目前，故障证明机制的开发工作正在顺利进行中。  
Validity Proof Settlement  
有效性证明结算机制使用数学证明来证明所提议的观点的正确性。当一个提议的国家附有有效的证明时，它会立即无条件地被接受;否则，它将被拒绝。此机制依赖于加密假设，而不是对某些参与者或进程的信任。虽然它消除了质询期的需要，但它需要大量的前期计算来生成证明。  
**Governance**  

###2025.01.25
治理层是指用于管理系统配置、升级和设计决策的通用工具和流程集。这是一个相对抽象的层，可以在目标 OP Stack 链和影响 OP Stack 的许多其他层的第三方链上包含广泛的机制。  
MultiSig contracts  多签合约  
多重签名合约是智能合约，当它们从一组预定义的参与者收到签名阈值时执行操作。这些通常用于管理基于 OP 堆栈的系统组件的升级。目前，这是用于管理 OP 主网上桥接合约升级的机制。多签合约系统的安全性取决于许多不同的因素，包括参与者的数量、阈值和每个参与者的安全程序。  
Governance tokens  治理代币  
治理代币被广泛用于去中心化决策。尽管治理代币的确切功能因具体情况而异，但最常见的机制允许代币持有者对项目必须做出的某些决策子集进行投票。投票可以直接进行，也可以通过委托进行。  
<!-- Content_END -->
