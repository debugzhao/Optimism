---
timezone: Asia/Shanghai
---


# Ye

1. 自我介绍
     - 清华-南加大 Communication Data Science 25'硕士在读，链上数据分析2年经验，Dune [@wyeeeh](https://dune.com/wyeeeh)，X [@wyeeeeh](https://x.com/wyeeeh)，Optimism NumbaNERDs 分析师，入选Optimism RetroPGF Round 3 & Round 6 头部贡献者。

2. 你认为你会完成本次残酷学习吗？
   - 有激励就有野心，之前完成过Sixdegree Lab和BuidlerDAO发起的Dune Analytics共学计划，以及DeFiHackLabs发起的Solidity残酷共学计划。

## Notes

<!-- Content_START -->

### 2025.01.06
#### Layer2 扩容方案
在 Bedrock 中，Layer2区块通过非合约地址以压缩格式写入L1区块链 (Ethereum)上，以减少Layer1的 gas 费用。这
种方式确保了 OP Mainnet 继承了 Ethereum 的可用性和完整性保证。
##### Optimistic Rollups
- Optimistic Rollups 使用它们的父链（如 Ethereum）的共识机制（如PoS），而不是自己提供共识机制。
- 在 Optimistic Rollup 中，状态承诺被发布到 L1（在 OP Mainnet 的情况下是 Ethereum）而不提供直接的有效性证明。这些承诺在“挑战窗口”期间被视为待定状态。如果在挑战窗口期间无人挑战状态承诺，则视为最终确定。当状态承诺被挑战时，可以通过“故障证明”过程使其无效。成功的挑战不会回滚 OP Mainnet 本身，只会移除有关链状态的发布承诺。

##### 区块
Optimism 的区块生产主要由单一的“排序器 (sequencer)”管理，负责提供交易确认、状态更新、构建和执行 L2 区块以及将用户交易提交到 L1。为了避免 MEV，Bedrock 中的排序器拥有一个私有的 mempool。OP Mainnet 每两秒产生一个区块，无论区块是否包含交易。

执行引擎（op-geth 组件）通过两种机制接收区块：
- **通过Layer 2 内部的P2P网络同步状态。** 执行引擎（op-geth 组件）通过点对点（P2P）网络与其他在同一 Layer 2 网络上的执行引擎进行通信和数据同步。
- **通过rollup 节点（op-node 组件）实现，从 L1 派生 L2 区块。** 这种方法相比于直接的 P2P 网络同步会慢一些，因为它需要等待 L1 区块的确认，并且处理从 L1 到 L2 的映射逻辑。然而，这种方法能抗审查。由于 L2 区块的生成是基于已经公开且被广泛认可的 L1 数据，这就使得任何试图对 L2 数据进行审查或篡改的行为都会被发现并受到阻止。可以把这种机制比喻为通过官方渠道获取信息，虽然可能不是最快的，但却是最可靠和最不容易被篡改的。




### 2025.01.07
##### Bridge
Optimism 允许用户在 L2（如 OP Mainnet）和底层 L1（如 Ethereum mainnet）之间的智能合约发送任意消息，从而实现 ETH 或代币（包括 ERC20 代币）的转移。标准桥（Standard bridge）使用这一功能，允许用户从 Ethereum 存入代币到 OP Mainnet，并允许从 OP Mainnet 提取代币回 Ethereum。

- **从 Ethereum 到 OP Mainnet**: 称为存款(deposit)，通过使用 L1CrossDomainMessenger 或 L1StandardBridge 完成，成为对应 L1 区块的第一个 L2 区块的一部分。

- **从 OP Mainnet 到 Ethereum**: 称为提款(withdrawl)，分为三个阶段：初始化提款 L2 交易、等待下一个输出根提交到 L1 并提交提款证明、以及在故障挑战期结束后完成提款。


### 2025.01.08
#### Layer2的解决方案交易成本对比

- **为什么要L2？更快、更便宜**
   普通转账eth需要字节数112左右，ZK压缩为12个字节，op系压缩为78.4（不固定，假设压缩了30%的空间），假设swap转账需要字节数约180左右，ZK压缩为14个字节，op系压缩为126个字节。
- 目前主要有四种技术方案：**Optimistic Rollup、ZK Rollup、Plasma、Validium。**

##### Optimistic Rollup
**交易成本**
- L2 执行费：每笔 L2 交易都会支付一定的执行费用，等于交易使用的 gas 数量乘以交易附带的 gas 价格。
   - `l2_execution_fee = transaction_gas_price * l2_gas_used`
- L1 数据/安全费：Optimism 上的用户必须支付向以太坊提交交易的费用，称之为L1 数据费用
   - `L1_data_fee = L1_gas_price * (tx_data_gas + fixed_overhead) * dynamic_overhead`

##### ZK Rollup
**交易成本**
在zkSync 中，每笔交易的成本有两个组成部分：
- 链下部分（存储 + 证明者成本）：状态存储和 SNARK（零知识证明）生成的成本。这部分依赖于硬件资源的使用，因此是不变的。
- 链上部分（gas 成本）：对于每个zkSync 区块，验证者必须支付以太坊 gas 来验证 SNARK，另外每笔交易额外支付约 0.4k gas 来发布状态。

**影响地板价的因素**
Rollup的交易地板价依赖于 ETH 主网 calldata 的费用。

**无气体转账**
用户可以直接用被转账的代币中支付交易费用（如DAI）而无需使用原生Token支付

### 2025.01.09
#### Layer2扩容方案对比

##### Rollup
**ZK Rollup**
zk-Rollups 是一种基于零知识证明的二层扩容方案。首先由 Rollup Operator 组件将多个链下交易聚合成一个批次，之后使用零知识证明（例如 zk-SNARKs 或 zk-STARKs）生成一个简洁的证明文件，这个证明可以验证整个批次的交易的有效性，而不需要逐一检查每笔交易；然后将证明及与该批次相关的数据提交到主链，主链通过验证证明的正确性，确保交易是有效的；主链验证通过后，链上合约会根据证明中的数据更新链上的状态。这意味着，尽管交易是在链下进行的，但链上状态仍然得到了更新，确保了数据的一致性。
- 零知识证明（Zero-Knowledge Proof，简称 ZKP）是一种密码学概念，它允许一个证明者向验证者证明某个陈述为真，而无需透露任何关于该陈述的其他信息。简而言之，零知识证明可以让一个人证明他拥有某种信息，而不需要透露这个信息本身。


**OP Rollup**
Optimistic Rollups 是一种基于乐观性验证的二层扩容方案，即默认提交的区块是正确的，除非有人提出质疑。它同样需要 Rollup Operator 将许多链下交易聚合成一个批次，之后计算批次交易产生的新状态（如余额、合约状态等）并生成一份链下状态更新；然后将链下状态更新、相关数据提交到主链，这个状态默认是正确的，不需要额外验证；但是在状态更新提交后，会有一个固定的挑战期，在此期间，任何人都可以通过提供欺诈证明来质疑提交的状态更新的有效性，与被质疑状态的相关的整个交易将通过 EVM 运行检验，如果证明状态更新是错误的，提交者会被惩罚（扣除押金），同时链上状态会回滚到正确的状态；如果在挑战期内没有人质疑状态更新，或者质疑被证明是错误的，那么链上状态会根据提交的状态更新进行更新。

###### ZK 与 OP 比较
||Optimistic Rollups（OP）|zk-Rollups（ZK）|
|----|----|----|
|交易验证方式|通过欺诈证明（fraud proofs）验证交易，默认交易有效，需链下用户和节点持续监测|通过零知识证明（如zk-SNARKs或zk-STARKs）验证交易，生成简洁证明确保交易有效性|
|安全性|因默认交易有效存在一定安全风险，需链下积极监测|基于零知识证明验证方式，安全性较高|
|吞吐量与性能|链下交易处理速度通常较快，但链上验证可能需更长时间（等待欺诈证明挑战周期）|生成零知识证明需计算资源，但链上验证速度较快|
|通用性|完全兼容EVM，适合通用智能合约执行和复杂计算，众多DAPP可直接迁移|在通用智能合约和复杂计算方面应用目前受一定限制|
|成本|通常链下交易成本较低|生成零知识证明需计算资源，可能链下交易成本较高|
|整体优势|更适合处理复杂智能合约场景，以太坊兼容性好|在安全性和隐私保护方面有优势| 

##### 参考文章
- [L2 扩容技术详解：Optimistic Rollups 与 zk-Rollups](https://web3caff.com/zh/archives/55667)
- [Optimistic Rollup vs. ZK Rollup 对比](https://learnblockchain.cn/article/738)
- [一文详解以太坊扩容方案：OP vs ZK Rollup](https://foresightnews.pro/article/detail/7248)

### 2025.01.10
#### 扩容方案
[L2 扩容技术详解：Optimistic Rollups 与 zk-Rollups](https://web3caff.com/zh/archives/55667)


##### 链上扩容
链上扩容（Layer 1），通过优化底层区块链协议本身来提高吞吐量。

- **分片**是将区块链网络分割成多个相互独立的子链，每个子链可以并行处理交易。这样，整个网络的吞吐量会随着子链数量的增加而线性增长，分片也是以太坊 2.0 路线图中关键的一步，分片之后 TPS 和 Gas 才能得到真正的优化。
- **共识算法的创新**很少见了，像之前提出的 POS、DPOS、DAG 等都是相对于 POW 的创新，相比于 POW，它们可以减少网络资源消耗，提高交易处理速度，同样，以太坊也选择了这条路。
- **对底层区块链协议进行优化**，例如调整区块大小、区块产生时间等，可以在一定程度上提高网络的吞吐量，比如比特币的隔离见证（SegWit）升级。

##### 链下扩容
链下扩容（Layer 2），通过在底层区块链之上构建新的协议层来实现扩容。

- **状态通道**：状态通道（State Channels）允许用户在链下进行交易，仅在通道开启和关闭时与主链进行交互，这极大地减少了链上交易数量，从而提高了吞吐量，像 Raiden Network 和 Lightning Network 就是分别针对以太坊和比特币的状态通道扩容产品。
- **Plasma**：Plasma 是一种子链（sidechain）方案，允许用户将资产从主链迁移到子链，并在子链上进行交易，子链周期性地将其状态更新提交给主链，以确保安全性，比如 OMG Network。
- **Rollups**：Rollups 是将多笔交易打包成单个证明（zk-SNARKs 或 Optimistic Rollup 的欺诈证明），并提交到主链。这样，主链仅需验证证明而无需处理每笔交易，从而提高了吞吐量。典例是 zkSync（基于 zkRollup）和 Optimism（基于 Optimistic Rollup），Arbitrum 同样也是基于 OP 的 产品。
Arbitrum 是一种基于 Optimistic Rollups 的二层扩容解决方案，它结合了 Optimistic Rollups 的优势，并对仲裁过程进行了创新和优化，在处理质疑和仲裁时采用了二分查找（Binary Search）技术，降低了仲裁过程的复杂性和成本。二分查找仲裁可以缩小错误范围，这个过程在链下执行，而链上只需要验证最后的争议部分，从而减少了链上的交易处理成本，但是这个过程也延长了处理时间，所以在发生仲裁的情况下 Arbitrum 比 Optimistic 更便宜，但也更慢。

### 2025.01.11
#### Stages：Rollup成熟度的三阶段评级框架
根据 rollup 对这些训练轮的依赖将 rollup 分为三个不同的阶段
##### Stage 0 — Full Training Wheels 第 0 阶段 — 全辅助
At this stage, the rollup is effectively run by the operators. Still, there is an source-available software that allows for the reconstruction of the state from the data posted on L1, used to compare state roots with the proposed ones.
在此阶段，rollup 由 Operator 有效地运行。尽管如此，仍然有一个源代码可用的软件，允许从 L1 上发布的数据中重建状态，用于将状态根与建议的根进行比较。
##### Stage 1 — Limited Training Wheels 第 1 阶段 — 有限的辅助轮
In this stage, the rollup transitions to being governed by smart contracts. However, a Security Council might remain in place to address potential bugs. This stage is characterized by the implementation of a fully functional proof system, decentralization of fraud proof submission, and provision for user exits without operator coordination. The Security Council, comprised of a diverse set of participants, provides a safety net, but its power also poses a potential risk.
在此阶段，rollup 过渡到由智能合约管理。但是，安全理事会可能会继续存在以解决潜在的错误。此阶段的特点是实施功能齐全的证明系统、分散欺诈证明提交以及在没有操作员协调的情况下提供用户出口。安理会由不同的参与者组成，提供了一个安全网，但其权力也带来了潜在风险。
##### Stage 2 — No Training Wheels 第 2 阶段 — 没有辅助轮
This is the final stage where the rollup becomes fully managed by smart contracts. At this point, the fraud proof system is permissionless, and users are given ample time to exit in the event of unwanted upgrades. The Security Council’s role is strictly confined to addressing soundness errors that can be adjudicated on-chain, and users are protected from governance attacks.
这是 rollup 完全由智能合约管理的最后阶段。此时，防作弊系统无需许可，用户有充足的时间退出，以防发生不必要的升级。安全理事会的作用严格限于解决可以在链上裁决的健全性错误，并保护用户免受治理攻击。

##### 框架
|项目|Stage 0 要求|Stage 1 要求|Stage 2 要求|
|----|----|----|----|
|自我标识|需自我标识为rollup| - | - |
|L2 状态根发布|在L1上发布L2状态根| - | - |
|数据可用性（DA）|在L1上提供数据可用性，要保证重建 L2 状态的数据在 L1 上可用| - | - |
|重建状态源软件|提供能从L1数据重建L2状态的rollup node软件| - | - |
|证明系统| - |使用适当的证明系统，如欺诈证明或zk rollups的证明系统，至少5个外部行为者可提交欺诈证明（可白名单）|欺诈证明系统应完全去中心化，无需许可，任何人可提交欺诈证明|
|用户退出机制| - |用户可在无操作员协调下退出，至少有7天时间退出（不包括安全理事会和治理相关升级）|用户至少有30天时间退出（包括DAO发起的升级，有链上错误检测系统时对检测到的错误除外）|
|安全理事会设置| - |由至少8个参与者组成的多重签名设置，50%共识阈值，至少一半参与者为外部人员，身份公开披露|安理会权力应高度受限，仅在链上检测到可裁决的健全性错误时能干预| 

### 2025.01.12
#### Optimism治理机制
今天先列一下框架，明天查一下资料对比：
- Token House V.S. Citizen House
- Mission Grants V.S. RetroPGF

**Token House**
- 基于token持有量分配vote权重
- OP 持有者可以直接投票，也可以将其 OP 投票权委托给其他人代表 (delegates)投票
- 负责Mission Grants

**Citizen House**
- 基于声誉的，由链上投票选出
- 负责RetroPGF

### 2025.01.13
**治理平台**
- governance forum
- charmverse
- agora
- snapshot

### 2025.01.14
今天有点忙，登录了Governance Forum看了一下最新的讨论。明天补上笔记。

### 2025.01.15
#### OP Token House
参考文档：https://community.optimism.io/token-house/token-house-overview
- Token House 与 Citizens' House 一起管理 Optimism Collective，并负责 Superchain 协议的治理。
- 成员组成：OP Holders
- 负责对治理基金的分配进行投票，对所有protocol和governor upgrade proposals进行投票，并提出对 OP 代币inflation rate的更改，以及[操作手册](https://github.com/ethereum-optimism/OPerating-manual/blob/main/manual.md)中概述的各种其他提案类型。
- OP 代币的投票权委托给明确自愿在 Token House 治理中活跃的社区成员。这些人被称为"delegates"
- Token House 治理按季节性时间表运行。Season大约每 6 个月一次。每一个Voting Cycle是3周。目前是Season 7。

### 2025.01.16
#### OP Citizen House
参考文档：https://community.optimism.io/citizens-house/citizen-house-overview
- 和Token House的投票权重 1 OP = 1 Vote不同，Citizen House的投票是1 Person = 1 Vote。
- 负责RetroPGF资金的分配，有权否决Token House提出的协议升级proposal
   - 未来可能与 Token House 合作管理**超额收入**的分配
- 成员组成：每一轮RetroPGF有不同的badge holder，通过“Web of Trust”机制选择

### 2025.01.17
#### OP Grants
参考文档：https://community.optimism.io/grant/grant-overview
- Season 7只有一个 [Season 7 Intent](https://gov.optimism.io/t/season-7-intent/9292)
##### Foundation Missions
- Github申请: https://github.com/orgs/ethereum-optimism/projects/31/views/1
##### RetroPGF Missions
- https://atlas.optimism.io/rounds
- 由Citizen House负责，每一轮有对应的scope和eligibility，需要项目报名或提名，再由Citizen House进行投票决定资格和分配
##### Governance Fund Missions
- https://app.charmverse.io/op-grants/
- Grants Council负责，需要项目自行提名，再由Grants Council成员根据每一轮的eligibility对项目进行投票决定资格和分配，符合条件的项目将最后经过Token House投票获得分配

### 2025.01.18
#### OP Grant Council
- https://app.charmverse.io/op-grants/optimism-grants-council-8323028890716944
- 由1个lead和15个reviewers组成的4个sub-committees (review teams)
   - Superchain Sub-Committee
   - Optimism Mission Review Sub-Committee
   - Milestones and Metrics Sub-Committee
   - Audits and Special Missions Sub-Committee
- Season 5有2个Lead
   - Communications Lead
   - Milestone and Metrics Lead

### 2025.01.19
#### Concentration of Power
- https://gov.optimism.io/t/measuring-the-concentration-of-power-in-the-collective/8956
- Concentration of Power Index (CPI)


|Governance Body|Percentage (%)|
|----|----|
|Token House (Th)|32.33%|
|Citizens’ House (Ch)|34.59%|
|Grants Council Builders & Growth Experiments Sub-committee (Gc)|10.15%|
|Grants Council Milestone & Metrics Sub-committee (Gc(M&M))|2.82%|
|Security Council (Sc)|13.17%|
|Code of Conduct Council (CoC)|4.32%|
|Developer Advisory Board (DAB)|3.01%|

- CPI趋势
   - Token House 的初始 CPI 为 329.25。加入RetroPGF Round 2的Citizen House和Season 3的Council数据后， Token House 的CPI 大幅下降至 140.13，并在S4保持稳定。加上S5的数据，Token House的CPI进一步下降至91.81
   ![CPI](https://europe1.discourse-cdn.com/bc41dd/original/2X/0/04efb59df754583ef0fb0755628777db08ce694d.png)

- Appendix: https://www.papermark.io/view/cm1j49mya0001rjn3cmsboya9
- 不同DAO的权力集中度
![DAO-CPI](https://europe1.discourse-cdn.com/bc41dd/original/2X/f/f4e9cb873216ed9c80270550e752326c5141b35f.png)
- 根据Nakamoto Coefficient（控制超过 51% 投票权所需的最低成员数量）
   - Optimism: 21
   - Compound: 13
   - Aave: 8
   - Uniswap: 17
- 一个很好玩的影响力集中度计算器 Influence Calculator：https://optimism-cop-analyzer.vercel.app/

### 2025.01.20
#### Optimism Superchain
- 参考文档
   - https://docs.optimism.io/superchain/superchain-explainer

**Superchain是什么？**
Superchain的愿景是一个去中心化区块链平台，由众多 L2 链集合在一起，这些链共用一套安全机制和 OP Stack 技术，也被称为 OP 链。这些OP链之间实现了标准化，就像积木一样能互相替换使用。这样一来，开发者做应用的时候，不用操心下面具体是哪条链，直接把 Superchain 当成一个整体来开发就可以。它的目标是解决区块链扩容难题，让网络又能**横向扩展**又**去中心化**，目前相关项目正在推进。
- 共享的机制：跨链桥、DAO、协议升级、通信层(Communication Layer)

**传统的多链架构难题**
- 每条链都引入了新的安全模型，随着新链被引入生态系统，系统性风险会加剧。
- 新链的启动成本很高，因为它们需要新的validator和builder。

**超级链的必要属性**
- 共享的 L1 区块链，用来为所有 OP 链提供交易总排序；
- 所有 OP 链共享的跨链桥，实现标准化安全属性；
- 便宜的 OP 链部署，可以在 OP 链上部署和交易而无需支付 L1 交易的高额费用
- OP 链的配置，可以自行决定data availability的提供者和sequencer地址
- 安全的交易和跨链消息。

### 2025.01.21
#### Superchain Project: LayerZero
LayerZero属于跨链通信协议，是一种开源、不可变的消息传递协议，旨在促进全链、可互操作应用程序的创建。开发人员可以通过全链消息轻松发送任意数据、外部函数调用和代币，同时保留对其应用程序的完全自主权和控制权。

**技术原理**
- https://docs.layerzero.network/v2/home/protocol/protocol-overview
- https://layerzero.network/how-it-works

*Step 1. Send (On-chain, Source Chain)*
1. Sender Contract: 用户调用发送者 OApp 合约内的“lzSend”方法，指定消息、Destination LayerZero Endpoint、目标 OApp 地址和其他协议处理选项。
2. Source Endpoint根据发送方OApp 的消息数据生成数据包，为每个数据包分配一个唯一的、连续递增的编号（即nonce随机数）。
3. MessageLib Registry: Layerzero Endpoint使用 OApp 指定的 MessageLib 对数据包进行编码，以将消息发送到选定的Security Stack和Executor，通过 PacketSent 事件完成发送事务。

*Step 2. Verify (Off-chain)*

配置的 DVN 独立验证消息：目标 MessageLib 强制只有 OApp 配置的 DVN 才能提交验证。

*Step 3. Commit (On-chain, Destination Chain)*
1. Message Library: 一旦 OApp 安全堆栈中的所有 DVN 都验证了该消息，目标 MessageLib 就会将该消息标记为可验证的 (Verifiable)。
2. Executor (Off-chain): Executor 将此数据包的验证提交给Endpoint，将数据包暂存以在Destination Endpoint中执行。

*Step 4. Receive (On-chain, Destination Chain)*
1. Destination Endpoint: 确保Executor传送的数据包与 DVN 验证的消息相匹配。
2. Executor (Off-chain): 对提交的消息调用“lzReceive”函数，以使用接收器 OApp 的逻辑处理数据包。
3. Receiver Contract: 消息由目标链上的接收方 OApp 合约接收。

**Tokenomics**
- ZRO 充当其生态系统内的治理代币。 ZRO持有者可以参与协议治理，对影响平台发展和政策的提案进行投票。
- \$ZRO: [0x6985884C4392D348587B19cb9eAAf157F13271cd](https://etherscan.io/token/0x6985884C4392D348587B19cb9eAAf157F13271cd)

**融资信息**

LayerZero Labs 在多轮融资中总共筹集了 \$263 million。
2023年4月，该公司在B轮融资中获得了\$120 million，估值\$3 billion。

**参考文章**
- 官网：https://layerzero.network/
- 文档：https://docs.layerzero.network/v2

- 生态系统：https://layerzero.network/ecosystem/dapps
- 数据看板：https://layerzeroscan.com/
- 支持网络：https://docs.layerzero.network/v2/developers/evm/technical-reference/deployed-contracts


### 2025.01.22
#### Superchain Project: DefiLlama
- 参考链接：https://www.superchain.eco/ecosystem-projects/defillama

*PS. 这里的官网链接有问题，指向的是[https://chainanalysis.com](https://chainanalysis.com)，应该是[https://defillama.com/](https://defillama.com/)*

DefiLlama是一个DeFi产品的数据看板，主要提供各个链生态和DeFi协议的TVL价值。
举例：可以在[Compare Chains](https://defillama.com/compare?chains=Optimism&chains=Base)比较不同链的TVL，Fee，Revenue等metrics

### 2025.01.23
#### Superchain Ecosystem: Base
参考文章
- [行业研究：一文详细解读 Coinbase Layer2 网络 Base 与 OP Stack](https://web3caff.com/zh/archives/54027)

1. 为什么BCoinbase选择了OP Stack做Layer2？
- 未来将会有许多 Layer2 网络，那么 Layer2 之间的战争也不可避免。如果 Layer2 网络之间还是像公链那般用跨链桥链接起来，这就和当前的糟糕情况一样：不同的网络之间依然割裂，跨链桥的风险与成本摩擦依然存在。

- OP Stack的模块化：Optimism 的团队正在将他们原先的开发工作拆解成多个层面的模块（Data Availability Layer，Derivation Layer，Execution Layer 和 Settlement Layer）并开发了 OP Stack。
   - OP Stack 是一套完整可行的构建模块化 Layer2 的方案，通过模块化解耦区块链各功能，并以 API 来组合各模块。只要某个功能模块 API 符合 OP Stack 的标准，那么就可以作为一个模块加入到 OP Chain 的搭建中。这使得其他开发者能快速地构建一个 Layer2 网络。而通过 OP Stack 构建的 OP Chain 不仅可以复用已有的 Optimism 的开发成果，还可以继续改造或者创新为 OP Stack 提供不同层面的不同模块，丰富 OP Stack 的生态。
   - Bedrock 的 Consensus Layer（由 Data Availability Layer 和 Derivation Layer 组成）采用的是 Rollup，执行层为 EVM，而结算层为 Governance。

2. Base对OP Stack的影响
- 帮助 Coinbase 为下一阶段去中心化应用的大规模采用做好准备。Base 将承载未来 Coinbase（2022 年 Q3 Coinbase 有近 1.1 亿用户数和超过 800 万的月交易用户）、Layer2 以及 Layer1 的流量。
- 未来 Base 的部分手续费也会流入 OP Collective，继续推动 OP Stack 的发展。
- 进一步确定以太坊和 Layer2 的地位。Coinbase 明确表示没有发币计划，使用以太坊作为网络汽油费。此外 Coinbase 加入了 OP Stack 的开发，并宣布继续投资和建设 Layer2 基础设施和相关工具。

### 2025.01.24
#### OP Superchain 补充阅读
- [构建以太坊的未来：超级链和原生互操作性](https://mirror.xyz/optimismcn.eth/CvGXTALKqVxVZ4UK_dJ0DUFUQe00rUwVYZ-3_IF2rbE)
- [OP 超级链的崛起](https://mirror.xyz/optimismcn.eth/8G03SGSXi_G_eJgqqCMJGHKwOkIaffXHyt7MbV9mS1Y)
- [详解 “超级链” 概念：Base 只是 Optimism 的小“野心”](https://www.chaincatcher.com/article/2088168)
- [解密超级链 —— 如何与 Optimism 集体共享收益](https://mirror.xyz/optimismcn.eth/VpIfmzutbHG3pD-H4uyDiBLIexKSgjV0kTNj79FjcVg)

Optimism Collective 2025 路线图的重点：建立一组进入互操作性第一阶段的链，每月可进行 2.5 亿美元的跨链资产转移。（互操作性也是[Season 7的唯一重点intent](https://mirror.xyz/optimismcn.eth/E1V-QmzXxB5kthlmhoA3u13Unh60mqXwf7Lc50q8_NM)）

- **消息传递协议**：实现安全的跨链消息传递，让数据和交易在超级链内自由流动。
- **ERC 7802**：简化跨链代币转移的标准代币桥接接口，如 SuperchainERC20。超级链内部跨链交易速度更快、更便宜。
- **互操作性故障证明**：一个将链的安全性结合在一起的安全层，无需引入全新的假设或可信方。
- **收入共享**：超级链中的每个 OP 链都采用标准化的收入分享模式，确保所有链公平公正地贡献，没有例外或特殊待遇。根据标准 Rollup 章程，每条链都将部分收入通过网络范围内遵守的费用分成返还给 Optimism 集体。费用分成计算为链收入的 2.5% 或链上利润的 15% 中的较大者，其中链上利润定义为手续费收入减去 L1 gas 费用。
- **OP Stack模块共享**：只要 OP 链自愿选择进入相同的共享sequencer，所有的 OP 链都可以享受原子式的跨链组合。如果 OP 链可能不想运行自己的sequencer，那么他们可以支付一定的费用来使用他们信任的 Optimism 的共享sequencer。这为 Optimism 开辟了另一种盈利模式，而不仅仅是目前 Optimism 链上的 dapp。

### 2025.01.25
#### OP Stack补充阅读
- [OP Stack 小课堂#0 | 初识 OP Stack](https://mirror.xyz/optimismcn.eth/MJTO9E2GJu4CAMn-7whLdGhQDpaj--9eJD3Hb9JDxHk)
- [一文探讨OP Stack：Optimism对模块化扩展的愿景](https://www.odaily.news/post/5185355)

OP Stack 就是一个用来创建新的 L2 区块链的开源系统，大家可以共享使用。就像是一些软件组件，可以用来定义 Optimism 生态系统的不同部分，也可以作为现有部分的模块。通过统一的标准，开发可以避免重复开发相同的软件。虽然 OP Stack 现在主要是用来运行 L2 区块链的基础设施，但理论上它也可以扩展到其他层，比如区块浏览器、消息传递系统、治理工具等。

##### OP Stack的逻辑层级
OP Stack 有多个逻辑层级，各有其作用。
- **Data Availability Layer 数据可用性层**：主要用来规定基于 OP Stack 的链的原始输入数据该放在哪里。OP Stack 链要获取输入数据，得依靠一个或多个数据可用性模块。
   - 举个例子，就好像一个大型图书馆的书架规划，数据可用性层决定了每一本书（原始输入数据）应该放在哪个书架、哪个格子里。，如果图书馆的某个书架坏了，导致上面的书（数据）再也找不到了，那么读者（链）就没办法正常阅读（同步）这些书的内容了，也就是可能无法同步链。

- **Sequencing Layer 排序层**：负责收集用户交易并发布到数据可用性层模块。排序器模块有单定序器（默认，特定参与者当排序器，治理机制决定人选）和多定序器（从一组预定义参与者选排序器，各链自定选择机制）

- **派生层**：定义如何处理原始数据，形成处理后的输入，再发给执行层。
   - Rollup 模块：它的工作就是专门从以太坊区块数据、Sequencer 交易批次、存款交易事件等里面去收集和整理数据，把这些数据变成执行层能接收的引擎 API 输入。
   - Indexer 模块（提案阶段）：当有交易发送到数据可用性层模块上的特定智能合约，并且这个合约发生了一些事情，比如发出了事件或者修改了存储，Indexer 模块就会开始工作，从这些变化中提取和处理数据，生成引擎 API 输入。

- **执行层**：定义系统内状态结构和改变状态的函数，按照一定的规则和收到派生层的指令，去管理和改变状态。

- **结算层**：建立状态视图且只读，方便其他链验证。结算层能在其他链上展示和证明目标区块链（OP链）的状态，当一个交易在数据可用性层发布并且确定下来了，那在 OP Stack 链上这个交易也就此确定。但是结算层还得去验证这个交易的结果。如果交易结果没问题，结算层才会接受这个交易。
   - 结算机制有基于证明的故障证明（用乐观协议，提案一定时间无异议则正确，特定方证明不同状态可使其无效）、防错乐观解决方案（类似上述，但用无需许可的故障证明过程取代多重签名挑战者）、有效性证明和解（用数学证明观点正确性，无证明不接受提案）。

- **治理层**：指管理系统配置、升级和设计决策的工具和流程，包含目标 OP Stack 链和第三方链上影响其他层的各种机制。比如多重签名合约（预定义参与者签名达阈值执行操作，常用于管理升级）和治理代币（用于分散决策，持有者对项目决策投票）。DAO治理投票就会涉及该层。

##### OP Stack的模块化
- 模块是能插入 OP Stack 创建 L2、L3 或 L4 的数据位，具有 “标准化” 和 “开源” 的特点，“标准化” 是大家对模块标准有共识且都能实现，“开源” 是能免费供人迭代和使用。
- OP Stack 的设计让代码分叉更容易，开发人员能轻松抽象区块链各部分，在一个链的不同执行、共识、结算和数据可用性层中切换模块，就像切换 API 一样。
- 举个例子，比如如果想把 Optimistic rollup 可换成 ZK rollup，那么把欺诈证明模块换成结算层的有效性证明模块就行；数据可用性层也能把以太坊换成 Celestia。


<!-- Content_END -->
