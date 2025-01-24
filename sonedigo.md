---
timezone: Asia/Shanghai
---

> 请在上边的 timezone 添加你的当地时区，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区
> 时区请参考以下列表，请移除 # 以后的内容


timezone: Asia/Shanghai


---

# {Harris Lee}

1. 自我介绍

大家好，我是Harris Lee，一位对OP Layer 2的发展感兴趣的教师，希望可以学习并传播ETH&OP 生态
2. 你认为你会完成本次残酷学习吗？

我为什么要认为不会呢？肯定是会的，希望最后能学下来并传播推广

## Notes

<!-- Content_START -->

### 2025.01.01

笔记内容

测试一下PR
### 2025.01.02

### 2025.01.06

笔记内容：
今天学习的内容是Optimism的overview
Firstly, Optimism is a Layer 2 scaling solution for Ethereum. The idea of Optimism rollups is to create a new type of blockchain that allows for faster transactions and lower fees than traditional Ethereum, which is using EIP-4844 blobs.

Secondly, Optimism block production is managed by the sequencer. The sequencer will provide the following services:
1. Providing transaction confirmations and state updates
2. Constructing and executing L2 blocks
3. Submitting user transcations to L1

The sequencer does have a mempool, similar to Ethereum.

Transactions get to the sequencer in two ways: 
1. Transactions submitted directly to the sequencer. But these transactions cannot be made censorship-resistant since only the sequencer knows them
2. Transcations deposit to L1, which are included in the chain in the apporpriate L2 block. It provides OP mainnet with L1 Ethereum-level censorship resistance. For the moment, The Optimism Foundation runs the only block producer on OP mainnet.

Block execution receives blocks using two mechanisms:

1.The execution engine can update itself using peer to peer network with other execution engines.
2.rollup node derives the L2 blocks from L1.

OP also could be thinking as bridging ETH or tokens between layers

OP is designed for users sending arbitrary messages between smart contracts on L2 and the underlying L1

Moving from Ethereum to OP mainnet called "deposit", meanwhile, moving from OP mainnet to Ethereum called "withdrawal"

Fault proofs:

When a state commitment is challenged, the commitment can  be invalidated through a "fault-proof" process. This process wil replace the invalidated state commitment with a new one. A successful challenge does not roll back OP Mainnet itself, only the published commitments about the state of the chain. The order of transactions and the state of Op mainnet is unchanged by a fault-proof challenge.

### 2025.01.07

According to yesterday's learning notes, I will start to learn about Optimism's rollup architecture. Today will start to learn about EVM Equivalence,the sequencers and messager and the rollup node  with https://specs.optimism.io/protocol/messengers.html\

EVM Equivalence:

The EVM Equivalence is the core concept of Optimism. It is a set of rules that allow the execution of Ethereum smart contracts on Optimism. The EVM Equivalence is a set of rules that allow the execution of Ethereum smart contracts on Optimism. The EVM Equivalence is a set of rules that allow the execution of Ethereum smart contracts on Optimism.

With a readable word to describe the functionality of Ethereum for Optimism,  If you think of Ethereum as an almighty, decentralized court, then the core insight of L2 scalability is: “don’t go to court to cash a check — just go if the check bounces.”--To translate this saying in Chinese it could said:不要为了兑现支票而去法院——只有在支票跳票时才去。
具体解释上面这句话可以理解为：

以太坊作为“全能的、去中心化的法院”：这里指的是以太坊作为一个基础区块链平台，它提供了安全、不可篡改的交易记录，并能够执行智能合约。就像法院一样，以太坊确保所有规则都被正确遵循，所有的争议都能得到公正的解决。然而，就像现实中的法院，以太坊处理每一笔交易或争议的成本（Gas费用）较高，而且处理速度相对较慢，因为每个区块都需要网络中的大多数节点进行验证和共识。

“不要为了兑现支票而去法院”：这表示不是每一个操作或交易都需要直接在以太坊主链上进行。许多日常的小额交易或快速交互可以通过更高效的方式完成，而不必占用以太坊主链的资源。这就是二层扩展方案的作用，它们允许用户在不依赖于以太坊主链的情况下进行大量的交易和互动，从而提高了效率并降低了成本。

“只有在支票跳票时才去”：如果在L2系统中出现了问题，比如资金没有按照预期转移，或者发生了欺诈行为，这时用户可以回到以太坊主链（“法院”）来解决争议。以太坊主链的安全性和最终性保证了即使L2出现问题，用户的资产仍然是安全的，并且可以恢复到正确状态。

According to the elaboration of the saying, we could easily understand EVM Equivalence as a set of rules that allow the execution of Ethereum smart contracts on Optimism with technique rollup architecture which could provide two outstanding features:
1. uncensorable transactions
2. anybody can transact

The Value of uncensorable transactions for rollup could be explained as follows:

The concept of "uncensorable" in the context of Ethereum Virtual Machine (EVM) Equivalence refers to the characteristic of the Ethereum network that, once a transaction is broadcasted to the network and successfully included in a block, the outcome of the transaction and the state updates are not subject to censorship or reversal. This implies:

Unstoppable Transactions: Any user can initiate transactions as long as they adhere to the protocol rules of Ethereum (e.g., paying sufficient Gas fees), and these transactions cannot be prevented from entering the blockchain due to external intervention.

Immutable History: Once a transaction is included in a block that the consensus mechanism has confirmed, it becomes part of the immutable history of the blockchain. This history is considered permanent and unchangeable unless more than 50% of the network's hash power is controlled to perform what is known as a 51% attack, which is extremely difficult and costly.

Decentralized Nature: Ethereum is a decentralized platform, so no single entity can decide which transactions should be accepted or rejected. All nodes collectively maintain the security and integrity of the network, ensuring that each user's rights are not infringed upon.
Execution of Smart Contracts: Once smart contracts are deployed and executed automatically under specific conditions, their outcomes also cannot be blocked or reversed, unless the contract itself is coded with specific clauses allowing for such actions. This ensures that agreements between parties can reliably execute according to predefined rules.

In summary, "uncensorable" underscores one of the core values provided by Ethereum as a blockchain technology — offering an open, transparent, and trustless environment where information and value exchanges can occur freely without interference. This attribute is crucial for protecting user privacy, safeguarding freedom of speech, and building censorship-resistant applications.

To satisfy the requirements of Ethereum L1 & L2s infrastructure, Optimistic comes with OVM and is targeted to be an EVM equivalence. If L2s want to surf Ethereum’s wave of infrastructural network effects, they must become EVM equivalent.

Optimistic practice EVM equivalence by achieving L2 blocks executed with precise EVM equivalence. Instead of implementing the EVM in Solidity, implement a VM with a much smaller, simpler instruction set, and run the EVM within this VM during fraud proofs. To do this, we must simply compile an existing EVM interpreter, such as Seth’s, to run within the simpler VM.

next day plan: focusing on sequencers, users, messages role in Optimistic protocol stack and step into the next step of Optimistic protocol.




### 2025.01.07

According to yesterday learning notes, I will start to learn about the Optimism's rollup architecture. Today will start to learn about EVM Equivalence,the sequencers and messager and the rollup node  with https://specs.optimism.io/protocol/messengers.html\

EVM Equivalence:

The EVM Equivalence is the core concept of Optimism. It is a set of rules that allow the execution of Ethereum smart contracts on Optimism. The EVM Equivalence is a set of rules that allow the execution of Ethereum smart contracts on Optimism. The EVM Equivalence is a set of rules that allow the execution of Ethereum smart contracts on Optimism.

With a readable word to describe the functionality of Ethereum for Optimism,  If you think of Ethereum as an almighty, decentralized court, then the core insight of L2 scalability is: “don’t go to court to cash a check — just go if the check bounces.”--To translate this saying in Chinese it could said:不要为了兑现支票而去法院——只有在支票跳票时才去。
具体解释上面这句话可以理解为：

以太坊作为“全能的、去中心化的法院”：这里指的是以太坊作为一个基础区块链平台，它提供了安全、不可篡改的交易记录，并能够执行智能合约。就像法院一样，以太坊确保所有规则都被正确遵循，所有的争议都能得到公正的解决。然而，就像现实中的法院，以太坊处理每一笔交易或争议的成本（Gas费用）较高，而且处理速度相对较慢，因为每个区块都需要网络中的大多数节点进行验证和共识。

“不要为了兑现支票而去法院”：这表示不是每一个操作或交易都需要直接在以太坊主链上进行。许多日常的小额交易或快速交互可以通过更高效的方式完成，而不必占用以太坊主链的资源。这就是二层扩展方案的作用，它们允许用户在不依赖于以太坊主链的情况下进行大量的交易和互动，从而提高了效率并降低了成本。

“只有在支票跳票时才去”：如果在L2系统中出现了问题，比如资金没有按照预期转移，或者发生了欺诈行为，这时用户可以回到以太坊主链（“法院”）来解决争议。以太坊主链的安全性和最终性保证了即使L2出现问题，用户的资产仍然是安全的，并且可以恢复到正确状态。

According to the elaboration of the saying, we could easily understand the EVM Equivalence as a set of rules that allow the execution of Ethereum smart contracts on Optimism with technique rollup architecturem which could provide two outstanding features:
1. uncensorable transactions
2. anybody can transcat

The Value of uncensorable transactions for rollup could be explained as following:

The concept of "uncensorable" in the context of Ethereum Virtual Machine (EVM) Equivalence refers to the characteristic of the Ethereum network that, once a transaction is broadcasted to the network and successfully included in a block, the outcome of the transaction and the state updates are not subject to censorship or reversal. This implies:

Unstoppable Transactions: Any user can initiate transactions as long as they adhere to the protocol rules of Ethereum (e.g., paying sufficient Gas fees), and these transactions cannot be prevented from entering the blockchain due to external intervention.

Immutable History: Once a transaction is included in a block that has been confirmed by the consensus mechanism, it becomes part of the immutable history of the blockchain. This history is considered permanent and unchangeable, unless more than 50% of the network's hash power is controlled to perform what is known as a 51% attack, which is extremely difficult and costly.

Decentralized Nature: Because Ethereum is a decentralized platform, no single entity can decide which transactions should be accepted or rejected. All nodes collectively maintain the security and integrity of the network, ensuring that each user's rights are not infringed upon.
Execution of Smart Contracts: Once smart contracts are deployed and execute automatically under specific conditions, their outcomes also cannot be blocked or reversed, unless the contract itself is coded with specific clauses allowing for such actions. This ensures that agreements between parties can reliably execute according to predefined rules.

In summary, "uncensorable" underscores one of the core values provided by Ethereum as a blockchain technology — offering an open, transparent, and trustless environment where information and value exchanges can occur freely without interference. This attribute is crucial for protecting user privacy, safeguarding freedom of speech, and building censorship-resistant applications.

In order to satisfy the requriement of Ethereum L1 & L2s infrastructure, Optimistic comes with OVM and targeting to be an EVM equivalence. If L2s want to surf Ethereum’s wave of infrastructural network effects, they must become EVM equivalent.

Optimisistc practice EVM equivalence by achieving L2 blocks executed with precise EVM equivalence. Instead of implementing the EVM in Solidity, implement a VM with a much smaller, simpler instruction set, and run the EVM within this VM during fraud proofs. To do this, we must simply compile an existing EVM interpreter, such as geth’s, to run within the simpler VM.

next day plan: focusing on sequencers, users, messages role in Optimistic protocol stack and step into the next step of Optimistic protocol.

### 2025.01.08

今天的学习内容将聚焦于sequencers，users, messagers在Optimistic协议栈中的角色，以及进入Optimistic协议的下一步。

user has two majority activities: submit transaction and query transaction.

user submits transaction to interact with Ethereum through a sequencer
user query transaction from the interfaces operated by the verifier

according to the above two activites, we need to about two roles: sequencers and verifiers

sequencers fill the role as block producers. In conclusion, sequencers will have these five activities:
1.Accepts transactions directly from Users.
2.Observes "deposit" transactions generated on Ethereum.
3.Consolidates both transaction streams into ordered L2 blocks.
4.Submits information to L1 that is sufficient to reproduce those L2 blocks fully.
5.Provides real-time access to pending L2 blocks that have not yet been confirmed on L1.

One thing needs to be noted that the sequencers are not trusted actors but are responsible for improving the user experience by ordering transactions much more quickly and cheaply than would currently be possible if users were to submit all transactions directly to L1.

Verifier fills the downloading role and executes the L2 state transition function independently of the Sequencer.

The depositing and sending transaction will have 5 steps:

1.Submit Deposit: Users initiate the process by submitting a deposit from Ethereum Layer 1 (L1) to the L2 network.
2.Fetch Deposit Events: The Sequencer  fetches deposit events from Ethereum L1 by OptimismPortal. This step ensures that the L2 network is aware of the deposits made on L1.
3.Generate Deposit Block: The Sequencer generates a deposit block based on the fetched deposit events. This block contains information about the deposits and is used to update the state of the L2 network.
4.Send Transactions: Users can start sending transactions on the L2 network once they have deposited ETH to pay fees. These transactions are processed more efficiently than on L1 due to the nature of L2 solutions.
5.Submit Transaction Batches: The Sequencer submits transaction batches to the Batch Inbox Address on Ethereum L1. This step involves bundling multiple transactions into a single batch, which is then submitted to L1 for finality.
![alt text](image.png)

The withdrawal process is similar to the deposit process, but instead of sending ETH to the L2 network, users withdraw their funds from the L2 network to Ethereum L1. The withdrawal could be simply identified as: **Users withdraw ETH or ERC20 tokens from an OP Stack chain back to Ethereum.**

1.Send Withdrawal Initialization Transaction: Users initiate the withdrawal process by sending a transaction to start the withdrawal on L2.
2.Submit Transaction Batch: The Sequencer submits a batch of transactions, including the withdrawal initialization, to the Batch Inbox Address on Ethereum L1.
3.Submit Output Proposal: Proposers submit an output proposal to the DisputeGameFactory contract on L2.
4.Generate Game: The DisputeGameFactory generates a game based on the output proposal and sends it to the FaultDisputeGame contract.
5.Submit Withdrawal Proof: Users submit proof of the withdrawal to the OptimismPortal contract on L2.
6.Wait for Finalization: The system waits for the finalization of the withdrawal process.
7.Submit Withdrawal Finalization: Users submit the finalization of the withdrawal to the OptimismPortal contract.
8.Check Game Validity: The OptimismPortal checks the validity of the game generated by the FaultDisputeGame contract.
9.Execute Withdrawal Transaction: Once the game is validated, OptimismPortal executes the withdrawal transaction to transfer the funds to external contracts on Ethereum L1.

next day(2025.01.09) will learn about some new words/roles: Proposers, Game and OptimismPortal.

### 2025.01.09

Today's plan to take away the new words/roles: Proposers, Game and OptimismPortal.

为了理解Proposers, 我们需要认识到Proposers在L2网络中角色所在的意义，以及Proposers在L2网络中如何与L1网络进行交互。

Proposers:

After processing one or more blocks the outputs will need to be synchronized with the settlement layer (L1) for trustless execution of L2-to-L1 messaging, such as withdrawals. These output proposals act as the bridge's view into the L2 state. **Actors called "Proposers" submit the output roots to the settlement layer (L1) and can be contested with a fault proof, with a bond at stake if the proof is wrong.**

The proposer's role is to construct and submit output roots, which are commitments to the L2's state. To practice these submission operation, proposers will post through contract L2OutputOracle on L1. The L2OutputOracle contract is responsible for submitting output roots to the L1. 

repo for optimism L2 proposers code: https://github.com/ethereum-optimism/optimism/tree/d48b45954c381f75a13e61312da68d84e9b41418/op-proposer

L2 blocks are produced at a constant rate of L2_BLOCK_TIME (2 seconds). A new L2 output MUST be appended to the chain once per SUBMISSION_INTERVAL which is based on a number of blocks. The exact number is yet to be determined, and will depend on the design of the fault proving game.

OptimismPortal:

The OptimismPortal is a low-level contract responsible for passing messages between L1 and L2. Messages sent directly to the OptimismPortal have no form of replayability. Users are encouraged to use the L1CrossDomainMessenger for a higher-level interface.

Next day(2025.01.10) will step into comparison between OP and other rollup proposals.

### 2025.01.10

Layer 2 rollup的四种技术方案：Optimistic Rollup、ZK Rollup、Plasma、Validium

https://learnblockchain.cn/article/3703

以下是计算gas费用降低的具体事例：
普通转账eth需要字节数112左右，ZK压缩为12个字节，op系压缩为78.4（不固定，假设压缩了30%的空间），假设swap转账需要字节数约180左右，ZK压缩为14个字节，op系压缩为126个字节。

在现有的以太坊链上，gas 上限为 3000 万，交易中每个非0字节的calldata数据需要 16 个 gas，0字节需要4个gas。如果ZK占领了以太坊所有的区块空间（在证明验证上花费 500k gas），忽略0字节的数量。

那么该批次可以有（2950 万 / 16）= 1,843,750 字节的数据。如上所示，每次用户操作的 ETH 转账汇总只需要 12 个字节，这意味着该批次最多可以包含 153,645笔交易。在13 秒的平均出块时间下，这转化为 ~11,818 TPS（相比之下，直接在以太坊本身上传输的 ETH 传输为 1300 万 / 21000 / 13 ~= 101 TPS）。

由上可知ZK Rollup 转账eth的可扩展性提高了100 + 倍，而zk最大优势不在于转账eth，相比转账erc20的合约代币，与uniswap交易来算，主网消耗的gaslimit的更多，ZK Rollup 压缩的性价比也越高，ZK Rollup相比主网的uniswap交易拓展可提高400+倍。

计算其他如OP的rollup机制，也可以参考上述的计算方法

以上rollup的机制主要聚焦于两个以太坊社区的提案：EIP-4488、EIP-4844

其中EIP-4488针对的是L1的calldata费用过高的问题,于2021年末提出，它实现了压缩calldata的功能，压缩后calldata的gas费用降低，从而提高交易效率。
具体包括：
1.降低Calldata Gas费用：EIP-4488提议将每字节calldata的gas费用从16 gas显著降低到3 gas。
2.引入最大Calldata限制：为了防止滥用和网络拥堵，该提案还建议对每个区块内可包含的calldata总量设置上限，即约1MB（具体数值可能会根据实际情况调整），这样可以避免因为过低的费用导致的数据膨胀问题。

EIP-4844 是一个更为复杂的提案，旨在为以太坊带来一种新的交易类型，这种交易可以携带额外的数据块(blob)，用于支持Rollup技术而无需立即进行全面的分片升级，于2023年提出
具体内容包括：
1.携带Blob的交易：EIP-4844引入了一种新的交易格式，允许交易附带所谓的“blobs”。Blobs是大型、临时存储的数据块，专门设计用于满足Rollup的数据可用性需求。
2.独立Gas价格和限制：与calldata不同，blob有自己的gas价格和限制，并且其定价模型更注重长期维护成本而非短期使用成本。
3.数据生命周期管理：Blobs只会在共识层节点中保留一段时间（例如几周），之后会被删除，这与传统的永久存储机制形成对比，减少了长期存储的压力。
4.通往完全Danksharding的桥梁：虽然EIP-4844本身不是完整的分片实现，但它为未来的完全分片（Danksharding）铺平了道路，提供了一个逐步过渡的方法。

next day 2025.01.11 will learn about stages from https://medium.com/l2beat/introducing-stages-a-framework-to-evaluate-rollups-maturity-d290bb22befe

### 2025.01.11

According to the Vitalik’s proposed milestones, Ethereum rollup could be divided into 3 stages which having different assistance from centralized control, as known as, training wheels of rollup:
1.stage 0:Full Training Wheels: At this stage, the rollup is effectively run by the operators. All data and operation relay on the L1.

2.stage 1:Limited Training Wheels: At this stage, the rollup is run by smart contracts. However, a Security Council might remain in place to address potential bugs. The Security Council, comprised of a diverse set of participants, provides a safety net, but its power also poses a potential risk.

3.stage 2:No Training Wheels: This is the final stage where the rollup becomes fully managed by smart contracts. At this point, the fraud proof system is permissionless, and users are given ample time to exit in the event of unwanted upgrades. The Security Council’s role is strictly confined to addressing soundness errors that can be adjudicated on-chain, and users are protected from governance attacks.

The stages idea comes from Vitalik's blog and many discussion in the community to define the rollup boundaries, such as the minimum exit window, the Security Council thresholds, and fraud proof allowlist size.

Each stage's requirement could be describe into several questions:
For stage 0: we need to think about these 4 questions:
- Does the project call itself a rollup?
- Are L2 state roots posted on L1?
- Does the project provide Data Availability (DA) on L1
- Is software capable of reconstructing the rollup’s state source available?

For stage 1: we need to think about these 5 questions:
- Does the project use a proper proof system?
- Are there at least 5 external actors that can submit a fraud proof?
- Can the users exit without the operator’s coordination?
- Do users have at least 7 days to exit in case of unwanted upgrades (Security Council and governance excluded)?
- Is the Security Council properly set up?

For stage 2:
- Is the fraud proof system permissionless?
- Do users have at least 30 days to exit in case of unwanted upgrades?
- Is the Security Council restricted to act only due to errors detected on chain?

next day 2025.01.12 will learn about rollup's and Optimism's protocal

### 2025.01.12

Today‘s work will learn through  https://specs.optimism.io/protocol/overview.html

对于Layer 2的总体架构来说，需要根据Layer 1的情况去诠释它的意义
在Execution-level实现等效以太坊虚拟机，要求有：
1.不需要特殊的编译器运行
2.无意外的gas费用
3.交易跟踪不需要额外的配置
4.所有以太坊的工具和特性均可使用
在此基础上，所有的节点要兼容以太坊layer 1，并且L2的实现要尽可能地减小和vanila Geth node的差异，并且充分利用L1的特性

首先，这个L2区块链将与一个基本的Geth节点交互，并尽可能地利用现有的第一层（L1）标准。这意味着该L2链将在某些方面遵循以太坊协议规范，以便更好地与其他以太坊节点通信。

其次，执行引擎/rollup节点将使用ETH2引擎API来构建主链上的L2链。ETH2引擎是以太坊2.0的核心组件之一，用于处理网络中的所有交易和状态更新。通过使用ETH2引擎API，L2链可以更好地集成到以太坊网络中，并获得更好的性能和安全性。

最后，执行引擎还将利用Geth节点现有的内存池和同步实现，包括快照同步。内存池是保存待确认交易的地方，而同步则是指将新的区块添加到本地区块链中。通过利用这些现有功能，L2链可以更快地处理交易并保持与主链的一致性。

Geth是一个用Go语言编写的以太坊客户端，可以用来连接或创建私有的以太坊网络，而关于L2链的部署，Geth提供的是基础支持，具体实施依赖于额外的协议和工具。

next day 2025.01.13 will learn about Core L1 Smart Contracts

### 2025.01.13

today bring up some new word for Core L1 Smart Contracts

batchers, SuperchainConfig, Batch Inbox Address, L1CrossDomainMessenger, DisputeGameFactory, FaultDisputeGame

note that batchers and guradian are two different roles, batchers are the ones who submit batches to the L1, while guardians are the ones who verify the batches and submit the results to the L1.

Batchers 是负责将多个交易打包成一个批次（batch），然后将这些批次提交到Layer 1（以太坊主链）的角色。这个过程有助于减少直接在主链上执行的交易数量，从而节省费用并提高效率。
Guardians 被描述为负责验证这些批次的有效性，并将验证结果提交回Layer 1的角色。这种机制确保了提交到主链上的批次是有效的，防止欺诈行为。

通过图片和流程，展示了deposit和withdrawal的流程，关键节点还是在OptimismPortal作为user和L1的交互点

next day 2025.01.14 will step into the Optimism Collective https://community.optimism.io/welcome/welcome-overview

### 2025.01.14
Optimism targeting to be a superchain which including public support resource, benefit for all but not the owner. And it is focusing on long term eco-system

OP 生态不仅有token house和citizen house分别决议不同的内容，这一治理具有多个成功案例可以参考，但是侧重点要放在去中心化上

### 2025.01.15

OP的投票机制
OP的管理工具主要有token house governance contract，用于提案的提交与投票

OP Governance Portal作为投票的前端界面

以及相关的snapshot space，discord， github分属不同的社群

对于提案的提交与投票都有详细的流程和时间处理周期，像是一个去中心化的社团组织，遵循各类民主程序，主要围绕着如何审批，修改，投票通过相关的proposal解决问题

### 2025.01.16

今日学习的是OP的创业启动资金如何获取

社区资金有哪些retrofund支持，有哪些项目得到了支持

### 2025.01.18

今日学习的是OP相关的一些项目，主要了解了governance tools系列做了哪些项目，哪些web3的治理投票工具以及metrics

### 2025.01.19

今日学习主要关注的是OP Council 的组成内容
通过观察https://gov.optimism.io/search?q=council，我们可以发现包括了以下常见的council记录
1. code of conduct council
2. security council
3. grants council

通过记录可以看到security council会讨论遇到的一些诸如盗号丢失，transaction问题的解决方案偏技术的具体事务处理的讨论

对于code of conduct council 会谈论一些投票流程的细项，以及社群的一些政治守则，偏向于思想上的统一

对于grants council，根据里面的内容会审议一些项目竞标，以及像season 6 superchain grants programs推出第六季超级链补助金计划的审查过程。为了确保拨款有效地促进超级链的增长和成功，我们已经建立了一个严格评估程序。该程序将涉及一系列针对每个申请的有针对性的问题。这表示所有申请者都必须回答这些问题，并且只有在他们能够提供令人信服的答案时才能获得资助。通过这种方式，我们可以确保资助分配给最有前途的项目，从而为超级链的成功做出最大的贡献。更具体到技术方案升级讨论以及具体的项目计划讨论，最为务实

### 2025.01.20

Today I will step into the L2 core contract at https://specs.optimism.io/protocol/overview.html
在区块链中，智能合约是非常重要的组成部分。这些合约被设计成自动执行特定的任务，并且通常是由代码编写的。在这个话题中，我们将讨论“L2系统合约”、“代理合约”以及“L2桥接合约”。

首先，“L2 system contract”是指那些作为链上衍生过程的一部分而更新或变异的合约。用户通常不会直接修改这些合约，除非是在FeeVault合约的情况下，任何用户都可以触发将收集到的费用提取到预设的提款地址。

其次，“proxy contract”是指位于其背后的智能合约。这些合约被突出显示为蓝色。

大多数OP Stack智能合约都位于由ProxyAdmin合约管理的代理合约之后。ProxyAdmin合约由某个所有者地址控制，该地址可以是任何EOA或智能合约。下面将提供一个图示来解释典型代理合约的行为。

通常情况下，智能合约需要访问外部资源（如链外数据、存储等），但是以太坊虚拟机并不支持直接与外部系统交互。因此，为了实现这种跨链功能，OP Stack引入了代理合约机制。

代理合约充当智能合约与外部资源之间的桥梁。它允许智能合约通过代理合约调用外部服务，并将结果返回给智能合约。代理合约还可以提供其他功能，例如限制对特定外部资源的访问权限或为多个智能合约共享同一外部资源提供方便的方式。

在OP Stack中，代理合约由ProxyAdmin合约管理。ProxyAdmin合约负责创建和销毁代理合约实例，并授予特定的所有者地址对其的控制权。这意味着只有被授权的所有者才能使用代理合约访问外部资源。

最后，“L2 Bridge Contracts”的用户交互已经被省略在这个图表中，但它们基本上遵循与核心L1智能合约架构图中描述的相同的用户交互方式。

总之，在区块链中，智能合约是非常重要的一部分，它们可以自动执行任务并帮助确保网络的安全性和稳定性。对于不同的合约类型，我们需要有不同的理解和处理方法，以保证区块链系统的正常运行。

### 2025.01.21

今天学习的是区块链传播，涉及的图片是
<img width="649" alt="image" src="https://github.com/user-attachments/assets/64f3e467-af62-41ad-8b5f-61329804d2a5" />
交易/区块传播是指在区块链网络中将交易或区块从一个节点传输到另一个节点的过程。在Optimism网络中，执行引擎（EE）使用Geth作为底层引擎，并利用其内置的点对点网络和事务池来传播交易。同样地，提交的区块也可以通过该网络进行传播并支持快照同步。

然而，未提交的区块则使用Rollup Node的单独点对点网络进行传播。这个过程是可选的，提供给验证者及其JSON-RPC客户端以降低延迟。

下图展示了Sequencer和Verifiers如何协同工作：

总之，交易/区块传播是在区块链网络中确保数据一致性和完整性的重要机制。在Optimism网络中，它通过使用Geth的点对点网络和事务池以及Rollup Node的单独点对点网络实现。这使得网络能够高效地处理交易和区块，并为验证者提供低延迟的服务。

### 2025.01.22
今天学习的内容是superchain

超级链是一个尚未完全实现的概念性项目，其具体实现依赖于整个乐观主义集体的贡献和变化。该文档旨在描述当前对于超级链的预测和规划，以帮助人们了解该项目的方向和发展。

区块链当前的问题在于scale规模不够大，在scale的问题上，一方面是需要基于multichain去构建Horizontal scalability，但是multichain本身存在缺陷

传统多链架构存在两个基本问题：

每个链引入新的安全模型，随着新链被引入生态系统，系统性风险呈复合式增长。
新链启动成本高，因为它们需要新的验证器集合和区块生产者。

这些问题源于缺乏一个单一共享区块链（“L1”链），该区块链作为所有“L2”链（多链系统中的所有链）的共享来源。通过使用共享的源头，可以实现以下两点：a）强制执行所有链的标准安全模型；b）取消部署链时需要一组新的验证器的要求，因为每个L2链都使用L1共识。因此L2链就是需要发展的superchain的基础
对于OP来说，要构建OP的superchain，需要满足以下需求：

1.共享L1区块链提供了所有OP链之间事务的总排序。这意味着所有的交易都按照特定的顺序被处理，并且可以保证交易的安全性和一致性。
2.共享桥梁使得所有的OP链都能够具有标准化的安全特性。这个桥梁允许所有的OP链相互连接，从而形成一个更大的网络。
3.廉价的OP链部署使得可以在不支付高昂费用的情况下在OP链上部署和交易。这使得更多的用户能够使用OP链，而不会因为高额的费用而受到限制。
4.OP链的配置选项使得OP链可以根据自己的需求来配置数据可用性提供程序、序列器地址等。这样可以让每个OP链都可以定制化地满足自己的需求。
5.安全交易和跨链消息使得用户可以安全地在不同的OP链之间迁移状态。这意味着用户可以在不同的OP链之间转移资产或执行其他操作，而不必担心安全问题。
6.一旦Optimism满足了这些属性，它就可以被认为是超级链。这意味着它可以作为一个更加完整的区块链生态系统，支持更多的应用和服务。

明天的学习内容是针对OP落实layer2所做到的一些举措，从而接近superchain

### 2025.01.23

chain factory 对于superchian至关重要
构建chain factory关键在于如何利用bedrock bridge，因为bedrock bridge构建了L1链和L2链的关系，奠定了L2的基础

superchain的价值在于剥离了L2链上的数据使其本地化计算，但是又利用contract保证了计算在L1链上的合法性，实现了permissionless

作为一种新的证明系统，即无权限证明系统。该系统可以通过引入Bedrock中介绍的模块化证明设计来实现，其中证明可以采用故障证明或有效性证明（例如零知识证明）。然而，在有效性证明被生产化之前，作者假设取款将使用故障证明系统。

在设想中的故障证明系统中，任何人都可以提交取款申请，并且这些取款申请可以在任何时候提交。当申请附带债券时，提交取款申请可以是无需许可的，因为如果证明无效，这些债券可以用作抵押品。如果挑战者成功地挑战了该申请，则将支付给挑战者作为参与保护系统的奖励，从而防止甚至在这种无需许可的系统内发生垃圾邮件攻击。此外，由于故障证明游戏可以高效地证明自创世以来整个链的历史，因此不需要定期提交它们。

在 Bedrock 中，引入了可配置的 Sequencer 设计，允许 OP Chain 的部署者在部署时设置 Sequencer 地址。这种设计被称为模块化序列化，它使得不同的实体可以负责不同 OP Chain 的序列化，并保留了 Superchain 桥的安全模型，这是向去中心化的序列器迈进的重要一步。

模块化序列化的能力是在 OP Chain 部署期间配置 Sequencer 地址。这个值可以由 OP Chain 的部署者配置。

Superchain 桥是治理所有 OP Chain 的 L1 桥合约。这个桥可以被 Optimism 集体升级。

在 Superchain 桥的安全模型中，链的安全性和活跃性得到了保证。安全性由证明系统保证，而活跃性则由直接提交交易到 L1 来保证。安全性和活跃性的结合意味着如果某个 OP Chain 序列器出现问题，用户总是可以通过将事务提交到 L1 来迁移到一个新的具有正常运行序列器的 OP Chain 上。

模块化序列化还使开发者能够无许可地实验不同的序列化模型。他们可以设想实施各种序列化协议，如轮询序列化、序列器共识协议、PGA 排序或先进先出排序等。随着时间的推移，我们可以期待竞争序列化协议之间的竞争将产生用户友好的序列化标准。

### 2025.01.24

今天学习的内容是OP stack， OP Stack 是一个软件集合，用于驱动 Optimism。目前的形式是在 OP 主网背后运行的软件，并最终将演变成 Optimism 超级链及其治理形式。

随着超级链概念的出现，对于 Optimism 来说，支持在提出的超级链生态系统内安全创建新的互操作性链变得越来越重要。因此，OP Stack 主要专注于创建共享、高质量且完全开源的新 L2 区块链系统。通过协调共享标准，Optimism 集体可以避免在孤立环境中反复重建相同的软件。

虽然当今的 OP Stack 显著简化了创建 L2 区块链的过程，但需要注意的是，这并不从根本上定义什么是 OP Stack。OP Stack 是所有驱动 Optimism 的软件。随着 Optimism 的发展，OP Stack 也将不断发展。

Optimism Bedrock是OP堆栈的当前版本。Bedrock发布提供了启动生产质量乐观卷积区块链的工具。目前，OP堆栈的不同层的API仍然紧密耦合于该堆栈的Rollup配置。

当今的OP堆栈是为了支持Optimism超级链而构建的，这是一个提议的L2网络，共享安全、通信层和共同开发堆栈（即OP堆栈本身）。Bedrock版的OP堆栈使启动与超级链兼容的L2变得容易。如果您想启动Superchain准备就绪的L2，请查看基于Bedrock版OP堆栈运行链的指南https://docs.optimism.io/builders/chain-operators/hacks/overview

明天的内容将围绕指南深入了解OP stack有哪些既有的具体内容，哪些既带发展

<!-- Content_END -->
