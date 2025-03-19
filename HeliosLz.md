---
timezone: Asia/Shanghai
---

> 请在上边的 timezone 添加你的当地时区，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区
> 时区请参考以下列表，请移除 # 以后的内容

timezone: Pacific/Honolulu # 夏威夷-阿留申标准时间 (UTC-10)

timezone: America/Anchorage # 阿拉斯加标准时间 (UTC-9)

timezone: America/Los_Angeles # 太平洋标准时间 (UTC-8)

timezone: America/Denver # 山地标准时间 (UTC-7)

timezone: America/Chicago # 中部标准时间 (UTC-6)

timezone: America/New_York # 东部标准时间 (UTC-5)

timezone: America/Halifax # 大西洋标准时间 (UTC-4)

timezone: America/St_Johns # 纽芬兰标准时间 (UTC-3:30)

timezone: America/Sao_Paulo # 巴西利亚时间 (UTC-3)

timezone: Atlantic/Azores # 亚速尔群岛时间 (UTC-1)

timezone: Europe/London # 格林威治标准时间 (UTC+0)

timezone: Europe/Berlin # 中欧标准时间 (UTC+1)

timezone: Europe/Helsinki # 东欧标准时间 (UTC+2)

timezone: Europe/Moscow # 莫斯科标准时间 (UTC+3)

timezone: Asia/Dubai # 海湾标准时间 (UTC+4)

timezone: Asia/Kolkata # 印度标准时间 (UTC+5:30)

timezone: Asia/Dhaka # 孟加拉国标准时间 (UTC+6)

timezone: Asia/Bangkok # 中南半岛时间 (UTC+7)

timezone: Asia/Shanghai # 中国标准时间 (UTC+8)

timezone: Asia/Tokyo # 日本标准时间 (UTC+9)

timezone: Australia/Sydney # 澳大利亚东部标准时间 (UTC+10)

timezone: Pacific/Auckland # 新西兰标准时间 (UTC+12)

---

# HeliosLz

1. 自我介绍：hi，大家好。我叫 Helios，希望可以深入了解 Optimism 方面的知识，加深自己对生态的理解程度。
2. 你认为你会完成本次残酷学习吗？Yes

## Notes

<!-- Content_START -->

### 2025.01.06

笔记内容

### 2025.01.07

**Optimism 简介**

Optimism 是以太坊的 Layer 2 扩容解决方案，基于 Optimistic Rollups 技术。它的目标是提高以太坊的可扩展性，同时保持其高度的安全性和去中心化特性。Optimism 通过在链下处理大量交易，减少网络拥堵，降低交易费用，从而增强 Ethereum 网络的性能。

工作原理

1.	Rollup 技术：
     * Optimism 使用 Rollup 技术，将交易数据批量提交到以太坊主链上进行验证。Rollup 本质上是将多个交易压缩成一个数据包，并将这个数据包发送到以太坊主链上。
     * 在 Optimistic Rollups 中，假设交易是有效的，只有在出现争议时才会进行检查。若没有问题，交易将在链上得到确认；如果有问题，其他用户可以提交挑战，智能合约会检查交易的有效性。

2.	Optimistic vs. ZK-Rollups：
    * Optimistic Rollups 和 ZK-Rollups 都是 Layer 2 解决方案，但它们的工作方式不同。ZK-Rollups 通过使用零知识证明（ZKPs）直接验证交易的正确性，而 Optimistic Rollups 假设交易是有效的，只有在质疑的情况下才需要进行验证，这种方式在性能上通常更高效。

3.	交易处理：
    * 在 Optimism 中，用户可以在 Layer 2 网络上进行低成本、快速的交易，所有交易的最终状态都会通过周期性的批量更新提交到以太坊主链。

4.	安全性：
    * 虽然大部分交易都在 Optimism 上处理，但所有的交易数据最终都提交到以太坊主链上，因此依然继承了以太坊的安全性。

如果有交易存在问题，可以通过“欺诈证明”机制发起挑战，确保数据的有效性。

**总结**

Optimism 是一种通过 Optimistic Rollups 技术扩展以太坊的 Layer 2 解决方案，能够大幅度提升交易吞吐量、降低交易成本，同时保持以太坊的安全性。它的设计使得现有的以太坊生态系统能够快速迁移到更加高效的环境中，满足更大规模的去中心化应用需求。


### 2025.01.08

**为什么会有 Mev 的产生，为什么 op 可以避免 Mev？**

MEV（最大化可提取价值，Maximum Extractable Value）产生的原因

MEV 指的是在区块链网络中，矿工（或验证者）可以通过重新排序、插入或删除交易，从中提取的额外价值。MEV 是一种通过控制区块中交易执行顺序的行为来获得的额外利润。其产生原因主要有以下几点：

1. 交易排序的可操控性：
* 在传统的区块链网络（如以太坊）中，矿工或验证者有权决定区块中交易的执行顺序。如果矿工或验证者能根据交易顺序进行优化（比如优先处理价格差异大的交易），就能从中获利。

2. 交易前的透明度：
* 以太坊和其他区块链的交易池（mempool）是公开的，矿工可以看到待处理的交易，并且可以预见到潜在的套利机会。例如，在去中心化交易所（DEX）上，可能存在由于订单簿顺序导致的价格滑点或闪电贷机会。

3.	套利机会和价格操控：
* MEV 的主要来源之一是 套利。例如，在不同的交易所之间，可能存在价格差异，矿工或验证者可以通过重新安排交易顺序或插入自有交易来利用这些差价，从中赚取差价利润。

4.	闪电贷攻击：
* 闪电贷可以使攻击者在没有任何初始资本的情况下借贷大量资金，然后利用这些资金进行价格操控或操纵市场，最后还款。通过操控交易顺序，攻击者可以从这些市场中提取价值。

**Optimism 如何避免 MEV**

Optimism 作为一个基于 Optimistic Rollups 的 Layer 2 扩容解决方案，它通过一些机制减少了 MEV 的问题。以下是 Optimism 如何减少 MEV 的几种方式：
	
1. 交易可预测性和透明性：
* Optimism 通过在 Layer 2 中处理大量的交易，并在最终提交至以太坊主链时进行批量确认，减少了交易池的操控空间。在 Optimism 中，交易的顺序和执行通常更加可预测，因为它们是批量提交和处理的，这减少了矿工通过操控交易顺序来提取 MEV 的机会。

2. 交易提交顺序和竞争降低：
* 在 Optimism 中，交易的排序和执行通常由 Rollup 的协议控制，而不是由单个矿工或验证者决定。这减少了矿工之间为了操控交易顺序而进行的竞争，也降低了 MEV 的产生空间。

3. 费用的分配机制：
* Optimism 采用了一种更加透明的费用分配模型，其中 gas费 和奖励等机制的调整可以减少对矿工优先排序交易的动力。通过减少矿工基于 MEV 动机的收益，降低了 MEV 的诱因。

4. 透明的验证和争议处理：
* Optimistic Rollups 的核心特性之一是争议解决机制。如果某个交易被质疑有效性，网络会进行验证并采取相应措施，这样的机制减少了通过恶意操作获得 MEV 的机会。

5. 在主链和子链的分离：
* Optimism 将交易和数据处理的负载转移到 Layer 2，并通过最终提交批量处理到以太坊主链上。这种分离的机制减少了 Layer 1 上的矿工可以控制和操纵的交易数据，从而减少了 MEV 产生的空间。

**总结**

MEV 是因为区块链中矿工或验证者可以操控交易顺序，从中提取额外的价值。它的主要原因是交易排序的可操控性、交易池的透明性和市场中的套利机会。而 Optimism 通过批量处理交易、减少交易顺序的可操控性、采用更加透明的费用机制和争议解决机制，来减少矿工或验证者通过操控交易获取 MEV 的机会。

### 2025.01.09

**可追溯公共物品资助**

Optimism 团队提出了一种名为“可追溯公共物品资助”（Retroactive Public Goods Funding，简称 RetroPGF）的机制，旨在通过事后奖励的方式，为公共物品项目提供资金支持。

核心理念：

传统上，公共物品（如开源软件、非营利项目）缺乏明确的盈利模式，导致资金短缺和发展受限。RetroPGF 的核心原则是：**事后判断价值比事前预测价值更容易达成共识**。 因此，该机制通过在项目完成后，根据其对社区的实际贡献进行奖励，激励更多人参与公共物品的开发。

运作机制：
1. 结果预言机（Results Oracle）： 由去中心化自治组织（DAO）组成，负责评估和奖励已完成的公共物品项目。初期可能由 20-50 名技术专家组成，随着治理机制的完善，成员将逐步增加。
2. 资金来源： 初期，Optimism 团队承诺将其序列器（sequencer）产生的所有利润用于公共物品资助实验。未来，资金可能来自协议费用等渠道。
3. 奖励分配： 结果预言机根据项目的实际贡献，向以下对象分配资金：
* 主要负责项目的个人或组织。
* 代表多个贡献者的智能合约，根据预定比例分配资金。
* 一种项目代币，其供应分配给为项目贡献时间和/或金钱的一个或多个个人和/或组织，但可以进行交易

预期效果：

通过引入类似初创企业的“退出机制”，RetroPGF 希望：
* 激励更多投资者和开发者参与公共物品项目。
* 促进非营利组织的蓬勃发展。
* 实现社区利益最大化，推动技术创新。

Optimism 团队已承诺将其序列器的所有利润用于公共物品资助实验，具体细节仍在制定中。他们期待通过这一机制，为公共物品项目创造类似初创企业的资金循环，促进社区的可持续发展。

https://medium.com/ethereum-optimism/retroactive-public-goods-funding-33c9b7d00f0c

**OP Stack 是 Optimism 的核心基础架构，它是一个用于构建去中心化区块链和扩展解决方案的模块化、开源软件栈（技术栈）。**

简单来说，OP Stack 是一组工具和组件的集合，用于构建和运行区块链（尤其是扩展以太坊的区块链）。它是 Optimism 网络的技术基础，也是 Optimism 为实现其 “Superchain” 愿景开发的关键技术。

**OP Stack 的核心目标**

1. 模块化：每个功能（如共识、执行、数据可用性）都被设计为一个模块，开发者可以根据需要进行定制和替换。
2. 可扩展性：OP Stack 专注于为以太坊提供高效的扩展解决方案，使得更多的交易可以更快、更便宜地执行。
3. 开源与可组合性：OP Stack 是完全开源的，任何人都可以基于它构建自己的区块链，同时确保与以太坊和其他基于 OP Stack 的区块链保持互操作性。
4. Superchain 生态系统：OP Stack 支持构建一个由许多 L2 区块链组成的 “超级链（Superchain）”，这些链在共享安全性和互操作性方面无缝协作。

**OP Stack 的模块**

OP Stack 是模块化的，允许开发者根据自己的需求选择和定制每个组件。主要模块包括：
1. 执行模块（Execution Layer）：
* 负责运行智能合约和处理交易。
* 通常使用以太坊虚拟机（EVM）或其他兼容虚拟机。
2. 共识模块（Consensus Layer）：
* 确保网络节点就区块顺序达成一致。
* 可以选择不同的共识机制（如 PoW、PoS）。
3. 数据可用性模块（Data Availability Layer）：
* 确保所有数据在区块链上都是可验证和可用的。
4. 聚合模块（Rollup Layer）：
* 支持 Rollup 技术，将多个交易打包并提交到以太坊主网，从而降低成本和提高效率。
5. 桥接模块（Bridging Layer）：
* 实现与以太坊主网和其他区块链的无缝交互。

**OP Stack 的优势**

1. 开发灵活性：OP Stack 的模块化设计允许开发者构建高度定制的区块链。
2. 与以太坊的兼容性：OP Stack 天然与以太坊兼容，支持智能合约、DApp 和工具的轻松迁移。
3. 推动 Superchain 愿景：通过基于 OP Stack 的多个区块链的互操作性，实现一个统一、协作的区块链生态系统。

**Superchain 愿景**

“Superchain” 是 Optimism 基于 OP Stack 提出的概念，旨在：
* 构建一个由多个区块链组成的网络，这些区块链共享基础设施、安全性和互操作性。
* Superchain 使得开发者可以在一个共享的生态系统中构建和扩展，而无需担心跨链兼容性问题。

### 2025.01.10

**Superchain Registry**

Superchain Registry（超链注册表）是 Optimism 生态系统中的一个关键组件，用于维护整个 Superchain 网络 中链的完整索引。它为每条链的配置和对既定标准的遵循情况提供透明度。

### 主要功能：

成员索引：
* 该注册表维护了一个完整的链列表，记录了所有属于 Superchain 生态系统的区块链网络及其详细配置和合规情况。

合规级别 (Compliance Levels)：
* 每条链都被分配了一个 superchain_level（超链合规等级），以指示其合规性。
* superchain_level = 1：完全符合 标准 Rollup 宪章 的链，并被指定为标准 Rollup。
* 其他级别可能表示不同程度的合规性或自定义化。

验证检查：
* 超链注册表会执行验证检查，以确保：
* 标准链 完全遵守 标准 Rollup 宪章。
* 非标准链 至少满足基本的技术和治理要求后，才能加入 Superchain 网络。

### 如何加入 Superchain 注册表？

想要加入 Superchain Registry 的链需要按照以下步骤进行：

1. 设置与配置：
* 根据 OP Stack 的指导，建立链的环境和配置。
2. 验证：
* 通过合规性验证检查，确保符合必要的技术与治理标准。
3. 提交申请：
* 向 Superchain Registry 仓库提交 Pull Request，并附上链的详细信息和配置文档。

此流程旨在确保所有参与的链都符合 Superchain 生态系统的安全性和技术一致性。

### 标准 Rollup 宪章 (Standard Rollup Charter)

标准 Rollup 宪章 定义了链需要满足的技术与治理标准，以达到 “标准 Rollup” 状态。这些标准有助于在整个 Superchain 生态中保持一致性、高安全性和可靠性。

### 2025.01.11

**Optimism 超链区块空间宪章**

区块空间宪章 是 Optimism 生态系统中的一项框架，旨在建立管理区块空间的标准、治理政策和预先承诺。其主要目标是确保安全性、正常运行时间，并符合 链法律 (Law of Chains)，以便为所有利益相关方提供一个安全且可扩展的区块链基础设施。

核心要点

1. 标准 Rollup 宪章 (Standard Rollup Charter)
* 标准 Rollup 宪章 规定了链要达到“标准”级别（Superchain 生态系统中最高的安全等级）所需满足的技术和治理要求。
* 遵循该宪章的区块链必须满足以下条件：
* 部署经过治理批准的 OP Stack 版本（Optimism 的开源 Rollup 框架）。
* 通过一系列配置检查，确保链的技术规范符合标准。
* 管理角色（如安全委员会）需符合预定的治理和安全要求。

2. 超链注册表 (Superchain Registry)
* 超链注册表 是一个用于索引 Optimism 生态系统中各链的数据库。
* 该注册表用于验证区块链是否符合 标准 Rollup 宪章 中批准的治理和技术标准。
* 满足标准的链会被标记为 superchain_level = 1，表明该链已达到“标准 Rollup”状态。

区块空间宪章 通过 标准 Rollup 宪章 和 超链注册表 形成了一个统一的治理与技术框架。它确保了 Optimism 生态系统中的区块链能够以安全、透明且符合既定标准的方式运行，从而促进整个网络的信任与可扩展性。

### 2025.01.12

### 2025.01.13

**Optimism Fault Proofs**

Optimism 的 故障证明（Fault Proofs） 是其乐观式汇总（Optimistic Rollup）系统的关键组成部分，旨在确保 Layer 2（L2）链的状态提交到 Layer 1（L1）以太坊时的准确性和安全性。

**为什么需要故障证明？**
* 无需信任：Optimistic Rollup 假设所有提交的状态提议都是正确的，但提供了一个挑战期以防止恶意行为。
* 保护网络安全：即使有恶意提议者存在，网络也可以依赖诚实的验证者发起挑战，保障最终状态的正确性。
* 惩罚机制：恶意提议者如果提交错误提议，可能会被罚没资金，防止恶意攻击。

**故障证明的功能**

在 Optimism 的架构中，用户可以通过提交提现证明（withdrawal proof）从 OP Stack 链（如 OP 主网）提取 ETH 和代币。 这些证明显示了提现操作已包含在 OP Stack 链中。 故障证明允许用户无需许可地提交和质疑关于 OP Stack 链状态的提议，这些提议用于验证提现操作。 ￼

**故障证明的工作机制**
1. 无许可的提议：任何人都可以提交关于 OP Stack 链状态的提议，这些提议通过 DisputeGameFactory 合约提交到以太坊。 这些提议主要用于用户证明他们在 OP Stack 链上进行了提现操作。 ￼
2. 无许可的挑战：由于任何人都可以提交提议，确保无效的提议能够被挑战至关重要。 在 OP Stack 链中，存在约一周的挑战期，用户可以在此期间对他们认为不正确的提议提出质疑。 任何用户都可以运行 OP Stack 链的节点，并使用 op-challenger 工具参与争议过程。 ￼
3. 模块化设计和多层安全性：OP Stack 的故障证明系统采用模块化设计，为实现多重证明系统奠定基础。这使得 OP Stack 能够在初始的 Cannon 证明系统之外，支持多种证明机制，从而提高系统对潜在攻击和漏洞的抵抗力。 ￼

**安全保障措施**
* 监控系统：一个离线监控系统被设置用于监控所有提议的根，并确保它们与正确的状态一致。 ￼
* 延迟窗口：在根通过游戏最终确定后，增加了一个称为“气隙窗口”的额外延迟，在此期间，守护者角色可以拒绝该根。 ￼
* 延迟支付：一个名为 DelayedWETH 的合约被设置用于持有保证金，并仅在延迟期后允许支付，以便在游戏错误解决的情况下，将保证金重新定向给正确的接收者。

![image](https://github.com/user-attachments/assets/fab66990-ac41-470d-92e5-1fd8207787c2)

这张图解释了 Optimistic Rollup（乐观汇总）中**故障证明（Fault Proofs）**的工作原理，重点是如何防止欺诈性交易通过链上验证。

**图中要素**
* Dishonest Proposer（不诚实的提议者）：尝试提交一个不正确的状态提议（output proposal），即错误的链上状态更新。
* Honest Validator 1 和 Honest Validator 2（诚实的验证者 1 和 2）：两个诚实的验证者，他们监测链上状态并检查是否存在恶意提议。
* Output Proposal（状态提议）：Layer 2 向以太坊主链提交的区块状态提议。
* 7 Day Challenge Period（7天挑战期）：当一个新的状态提议被提交到以太坊主链时，会有一个为期 7 天 的挑战期。任何人都可以在此期间对状态的有效性提出质疑。
* Challenge（挑战）：如果发现错误，诚实的验证者可以对恶意的状态提交发起挑战。

**流程解析**
1. 不诚实的提议者提交状态提议：不诚实的提议者向以太坊主链提交了一个错误的状态提议（output proposal）。
2. 7天挑战期：该提议进入 7 天的挑战期，允许网络中的其他验证者检查其正确性。
3. 诚实验证者检测错误：诚实验证者1 和 诚实验证者2 发现了不诚实的提议者提交的状态有误，决定提交挑战（challenge）。
4. 挑战发起：两位诚实的验证者向以太坊链上发起挑战，并提供证明，表明该状态提议是无效的或有错误的。
5. 结果：
* 如果挑战成功：
* 不诚实的提议者的提议将被驳回。
* 不诚实的提议者可能会失去抵押的资金（罚金）。
* 如果挑战失败或没有挑战者：
* 状态提议被视为有效，并最终确认在以太坊主链上。

Cannon 是 Optimism 的默认故障证明虚拟机（Fault Proof Virtual Machine，FPVM），用于在争议游戏（Dispute Game）中验证 OP Stack 区块链的状态。 ￼

Cannon 由两个主要组件组成：
1. 链上部分（MIPS.sol）：这是在以太坊虚拟机（EVM）中实现的 MIPS 指令模拟器，负责在链上验证单个 MIPS 指令的执行。 ￼
2. 链下部分（mipsevm）：这是用 Go 语言实现的 MIPS 模拟器，用于生成每个 MIPS 指令的证明，以供链上验证。 ￼

在争议过程中，Cannon 的链下部分（mipsevm）会模拟执行 MIPS 指令，并生成相应的证明。

这些证明随后由链上的 MIPS.sol 合约验证，以确保 Layer 2 状态转换的正确性。

这种设计使得 Optimism 的故障证明系统具有模块化特性，允许在争议中使用不同的 FPVM。

然而，目前 Cannon 是唯一实现的 FPVM，因此在所有争议中都会使用它。 ￼

通过这种链上和链下相结合的机制，Cannon 提供了一个高效且安全的方式来验证 Layer 2 的状态转换，确保 Optimism 网络的完整性和可信度。

**在 Optimism 中的 MIPS 指令模拟器**

在 Optimism 的故障证明系统 Cannon 中，MIPS 指令模拟器的作用是：
1. 状态验证：
* 用于模拟并验证 OP Stack Layer 2 区块链的状态转换。
* 如果有争议，MIPS 模拟器会重放整个区块状态计算过程，以证明状态转换的正确性。
2. 链下执行：
* mipsevm（MIPS 模拟器的链下版本）会在链下运行 MIPS 指令，生成每个指令的计算结果。
3. 链上验证：
* MIPS.sol 是一个智能合约，负责在以太坊 EVM 上逐条验证这些 MIPS 指令执行的正确性，以防止欺诈行为。

**为什么使用 MIPS 模拟器？**
* 简单且高效：MIPS 是一个相对简单的指令集，适合用作 Rollup 方案中的状态计算。
* 可验证性：使用 MIPS 指令集进行计算，能够生成可验证的计算证明（如 Cannon 在 Optimism 的实现）。
* 模块化和通用性：MIPS 是通用计算机架构，能够用于多种计算验证方案。

### 2025.01.14

**迈向跨链未来：跨区块链移动数据**

https://blog.oplabs.co/setting-out-for-a-cross-chain-future-moving-data-across-blockchains/?utm_source=chatgpt.com

Wonderland 团队 是 Optimism 生态系统中的核心开发团队之一，他们正在为实现 跨链互操作性 和 优化用户体验 开展以下重要工作：

**流动性碎片化**
* 当前的跨链生态中，资产分散在多个无法原生通信的网络中，这导致流动性碎片化。
* 这种问题引发了高昂的费用、较长的等待时间，以及复杂的用户体验。
* 目标是打造无缝的跨链体验，使在多个链之间的操作像在单一链中操作一样简单。

**跨链互操作性标准**

Wonderland 团队正在开发工具和标准，以促进链间数据互操作性。

贡献包括：
* xERC20：定义跨链桥接代币的标准，支持自主桥接代币。
* SuperchainERC20：为 Superchain 生态系统设计的跨链代币接口。
* ERC-7802 提案：提出统一的跨链桥接接口，用于跨链代币的铸造和销毁。

**USDC 桥接标准** 

当前，USDC 流动性因多个链上的不同版本而分裂，成为一个显著问题。Wonderland 提出了 opUSDC 解决方案：
* 旨在优化 USDC 在 OP Chains 上的部署。
* 最小化资产的分歧。
* 提供从桥接 USDC 到原生 USDC 的平滑升级路径。

**Wonderland 当前主要工作**

1. ETH 共享锁箱（Shared Vault for ETH）
* 问题：当前每条链都保留独立的流动性池，导致现有的 ETH 流动性与可供提款的 ETH 之间出现不匹配。

解决方案：
* Wonderland 正在开发一个名为 ETH 共享锁箱 的单例合约。
* 该合约将统一存储整个 Superchain 的 ETH 流动性。
* 通过 Superchain 的共享证明架构 进行保护，确保安全性和统一性。

目标：消除流动性限制，使用户能够从任何链无缝提款。

2. Interop Mock System（跨链模拟系统）
* 问题：在全面部署跨链通信功能之前，确保跨链交互的安全性和稳定性。

解决方案：
* 推出 Interop Mock System，用于模拟和测试跨链通信。
* 开发者可以使用测试网络（如 OP Sepolia 和 Unichain Testnet），并通过自定义合约和后端服务模拟排序器和预部署合约的角色。

目标：提供一个安全的测试环境，让开发者可以预先验证跨链通信的功能和效果。

3. 推进互操作性的开发

互操作性的重要性：

Wonderland 认为，互操作性是以太坊生态系统实现真正繁荣的关键。它的愿景是整合分散的资产，创建一个统一的跨生态系统流动性池。

解决方案：
* 标准化链间资产移动和交互方式。
* 使智能合约和 dApp 之间的交互变得顺畅，为一个区块链构建即意味着为所有区块链构建。

目标：消除资产和生态碎片化，打造一个互联互通的生态系统。

### 2025.01.15

**Introducing Stages — A Framework to Evaluate Rollups Maturity**

Stages 框架的三个阶段

阶段 0：完全训练轮（Full Training Wheels）

定义：在此阶段，Rollup 的运行主要由中心化实体控制。

特征：
* 系统的核心操作由中心化运营者负责管理。
* 尽管 Rollup 可能具有开源软件，用户可以从 Layer 1 发布的数据中重建状态，但核心逻辑依然依赖于中心化控制。
* 安全性和系统稳定性严重依赖于运营者的行为。

阶段 1：限制性训练轮（Limited Training Wheels）

定义：Rollup 开始通过智能合约管理，但仍依赖于一个安全委员会（Security Council）来应对潜在漏洞。

特征：
* 实现了完整的证明系统（如欺诈证明或有效性证明）。
* 用户可以无需运营者协调，直接退出系统。
* 欺诈证明或有效性证明系统开始实现去中心化。
* 安全委员会为系统提供额外保护，但其权力可能带来一定的集中化风险。

阶段 2：无训练轮（No Training Wheels）

定义：Rollup 完全由智能合约管理，达到完全去中心化的状态。

特征：
* 系统中的所有操作都通过去中心化的欺诈证明或有效性证明机制实现。
* 用户在发生系统升级时有足够的时间退出，确保资产安全。
* 安全委员会仅限于处理少量的极端情况（如可在链上裁定的严重错误），用户免受治理攻击的威胁。
* 这一阶段的 Rollup 达到了真正的去中心化，完全由协议和代码管理。


### 2025.01.16

**Optimism Collective 的双院治理结构**

### 治理机构

1. Token House:
* 由持有 OP 代币的用户组成，负责基于代币持有量进行投票的治理结构。
* 关注资金分配和协议调整，具有更强的经济导向性。

2. Citizens’ House:
* 由被选定为公民的成员组成，强调身份认证而非代币持有。
* 关注公共物品资助和社区权益保护，具有社会导向性。

3. Both Houses (两个院共同参与):
* 某些职责需要两个院协作完成。

### 职责分工
	
1. Resource Allocation（资源分配）
	
**Token House：**
* Treasury: Gov Fund：负责管理治理资金库。
* Foundation Budget Approvals：批准 Optimism 基金会的预算。
* Protocol Revenue Allocation：决定协议收入的分配。
* Inflation Adjustments：调整代币的通胀政策。

**Citizens’ House：**
* Treasury: RetroPGF Fund：管理 RetroPGF（Retroactive Public Goods Funding）的资金池。
* RetroPGF Funding：对公共物品的资助进行决策。

**Both Houses：**
* Director Removal：共同决定是否罢免治理结构中的董事。
* Treasury: Unallocated Fund：共同管理未分配资金。

2. Capture Resistance（抗捕获性）

**Token House：**
* Rights Protections：保护代币持有者的权利。
* Protocol Upgrades：对协议升级的提案进行投票。
* Sequencer Selection：选择 Sequencer（排序器）的管理者。

**Citizens’ House：**
* Citizenship Eligibility：决定谁有资格成为公民。

**Both Houses：**
* Code of Conduct Enforcement：共同执行行为准则，确保治理过程的公平性。



### 2025.01.17

2024 年，Optimism Collective 在多个方面取得了显著进展，推动了以太坊的扩展性和去中心化。

**Superchain 的显著增长**

2024 年，Superchain 生态系统超出了预期的增长：
* 新增链条：30 多条 OP 链加入生态系统，包括 Kraken（Ink）、Sony（Soneium）、Uniswap（Unichain）和 World（World Chain）等主要参与者，以及 Base、Metal、Mode 和 Zora 等早期先驱。
* 交易量：2024 年 12 月，日交易量从 2023 年 12 月的 65 万笔激增至 1110 万笔，增长了 1600%。
* 应用程序：Superchain 上的应用程序数量从 2023 年 12 月的 319 个增长到 2024 年 12 月的 464 个，其中 145 个是在 2024 年推出的。

**OP Stack 的进展**

作为 Superchain 生态系统的核心，OP Stack 在 2024 年取得了以下进展：
* 故障证明与 Stage 1 去中心化：推出了无许可的故障证明系统，为 OP Stack 链实现 Stage 1 去中心化奠定了基础。
* 互操作性：Superchain 和以太坊全网的互操作性成为 2024 年的核心焦点。

核心贡献者的更多成果

OP Stack 的核心贡献者在 2024 年推出了多个重要功能，惠及 Superchain 和以太坊：
* EIP-4844：经过两年的研发，EIP-4844 为所有 L2 带来了显著的成本降低，Gas 费用下降了超过 10 倍。
* Span 批次：Sunnyside Labs 推出了 Span 批次，将运行 OP 链的开销降低了 90%，提高了可负担性和效率。
* RIP-7212：RIP-7212 在 Superchain 上上线，实现了原生密码验证，降低了成本，使开发者能够构建更流畅的智能钱包体验。
* 事件响应能力：Superchain 的事件响应能力得到了升级，利用整个 Superchain 的集体安全情报。
* 开发者控制台：推出了开发者控制台，作为开发者在 Superchain 上构建的综合平台。
* Superchain 注册表和 BloXroute：推出了 Superchain 注册表和 BloXroute，进一步增强了生态系统的功能和互操作性。

2024 年，Optimism Collective 在扩展性、去中心化和生态系统增长方面取得了显著进展，推动了以太坊和用户拥有的互联网的发展。



### 2025.01.18

### 2025.01.19

明确定义安全委员会的要求对于将其与简单多签区分开来非常重要，这也将区分阶段 0 和阶段 1 Rollup。目前的要求是：
* 至少有 8 位参与者。
* 至少 50% 的成员来自核心组织外部。
* 至少需要 50% 的门槛。
* 至少需要 2 位外部成员达成共识。
* 成员需公开宣布。
-----------------
**最低配置的安全委员会：**
8 名成员、50% 的门槛、6 名外部成员，以及 2 名来自组织的成员。

安全委员会可以执行两项操作：
1. 接受证明系统的决定，不推翻它。
2. 推翻证明系统的决定，推动即时升级。

根据当前安全委员会的设置，推翻证明系统或拒绝推翻都需要至少 50% 的成员支持，至少包括 2 名外部成员和 2 名内部成员。

关键在于，安全委员会的门槛可以调整，使得遵循证明系统的决策更容易，而推翻它的决策更困难。

假设一个 87.5% 门槛的多签 (7/8)：至少需要 7 名成员来推翻证明系统，但仅需要 2 名成员即可阻止这种推翻的确认。

通过增加“虚拟地址”（例如许多零地址），可以将这个 7/8 的多签转变为一个 51% 门槛的多签。这些虚拟地址从不参与升级投票，相当于始终同意智能合约证明系统的决策。虚拟地址的数量与原始门槛的高度成正比。例如，一个具有 8/12 (66.6%) 门槛的多签仅需添加 3 个虚拟地址即可达到 8/15，而一个 11/12 的多签则需添加 8 个地址达到 11/20。

虚拟地址总是“遵循”智能合约系统，可以将它们视为证明系统在整个多签中持有的“投票权”。

在原始 7/8 多签设置中，可以将多签视为一个 7/13 (51%) 的多签，其中证明系统默认拥有 5 票，始终倾向于不推翻自身。这样，我们可以得出以下结论：

* 接受证明系统的决定（防止推翻）：需要 7 票，默认由证明系统提供 5 票，还需 2 名其他成员。
* 拒绝证明系统的决定（推动推翻）：需要 7 名成员。

通过这种“虚拟”多签，我们可以计算出证明系统在原始 7/8 多签中的决策权百分比：证明系统在 7/13 多签中占有 5 票，占比约 38.5%。

如果对数学更感兴趣，可以参考本文末尾的附录。回到原始 50% 门槛的多签，很容易看出，证明系统完全没有投票权：它的存在并没有使得拒绝推翻比推动更容易，因此它的投票权为零。


### 2025.01.20

**虚拟地址是什么？ 为什么要引入虚拟地址？虚拟地址能投票吗？如何实现的**
1. 什么是虚拟地址？

虚拟地址 是在多签治理系统中引入的一种抽象机制，用于代表系统内特定默认行为的“自动投票权”。它不是由真实的用户或实体控制的地址，而是一种逻辑上的设计，旨在增强系统的默认行为权重，例如支持智能合约证明系统的默认决定。

虚拟地址的特点：
* 逻辑存在：虚拟地址只存在于系统逻辑中，不对应真实的账户或私钥。
* 自动投票：它的投票行为是预定义的，例如默认支持证明系统的决定。
* 不可独立控制：虚拟地址不受多签成员的直接控制，不能改变其行为。

2. 为什么要引入虚拟地址？

引入虚拟地址的原因在于 平衡治理权重 和 增强系统安全性：

(1) 增强证明系统的影响力
* 在多签中，虚拟地址代表 智能合约证明系统 的默认投票权，使得默认行为更难被推翻。
* 通过虚拟地址，系统在未达到足够多真实成员反对的情况下，可以自动接受证明系统的结果。

(2) 防止恶意篡改
* 如果没有虚拟地址，少数成员可能更容易联合推翻证明系统的决定，增加安全风险。
* 引入虚拟地址后，推翻默认决定需要更多成员一致同意，提高了篡改的难度。

(3) 简化默认决策流程
* 虚拟地址通过默认投票简化了系统治理流程，使得在大多数情况下不需要所有成员参与投票即可达成决定。
* 例如，证明系统的默认行为本身是可信的，虚拟地址可以直接支持它，无需额外表决。

3. 虚拟地址能投票吗？

是的，虚拟地址可以投票，但它的行为是预定义的，无法像真实成员一样灵活调整。
自动投票行为：
* 虚拟地址始终支持特定的默认行为，例如接受证明系统的决定。
* 如果提案是“推翻证明系统的决定”，虚拟地址不会参与支持。
不可变更性：
* 虚拟地址的投票权是通过智能合约内置的逻辑定义的，不能被外部操作或更改。

4. 虚拟地址如何实现？

虚拟地址的实现依赖于 智能合约逻辑，并与多签系统紧密结合。以下是具体实现方式：

(1) 智能合约内置逻辑
* 在多签合约中，虚拟地址被预定义为支持某些特定决策。
例如：
* 如果提案是“接受证明系统的默认决定”，虚拟地址会自动投票支持。
* 如果提案是“推翻证明系统的默认决定”，虚拟地址不会投票。

(2) 将虚拟地址计入投票机制
* 虚拟地址被视为多签系统中的签署者（签名者）。
* 当多签合约检测到提案触发时，会自动将虚拟地址的预定义投票结果计入总票数。

(3) 动态调整虚拟地址数量
* 根据系统需求，可以通过合约逻辑动态调整虚拟地址的数量。
调整方式：
* 增加虚拟地址数量：提升证明系统的权重，使其更难被推翻。
* 减少虚拟地址数量：降低证明系统的权重，增加真实成员的决策影响力。

(4) 示例代码结构

在 Solidity 合约中，可以实现虚拟地址逻辑如下：

~~~
contract VirtualAddressMultisig {

    uint256 public threshold;
    uint256 public totalSigners;
    uint256 public virtualVotes;
    
    constructor(uint256 _threshold, uint256 _totalSigners, uint256 _virtualVotes) {
        threshold = _threshold;
        totalSigners = _totalSigners;
        virtualVotes = _virtualVotes;
    }

    function calculateVotes(uint256 realVotes) public view returns (bool) {
        uint256 totalVotes = realVotes + virtualVotes; // 加上虚拟地址的票数
        return totalVotes >= threshold;
    }
}
~~~

(5) 实现虚拟地址动态调整

通过动态增加虚拟地址，可以调整门槛。例如：
* 多签成员总数为 8，门槛为 7/8。
* 添加 5 个虚拟地址后，总投票数变为 13，门槛调整为 7/13。

5. 举例说明

假设：
* 多签规模：8 名真实成员。
* 门槛：7/8（87.5%）。
* 虚拟地址：5。
* 等效规模：8（真实成员）+ 5（虚拟地址）= 13。

决策场景：
1. 接受证明系统的默认决定：
* 虚拟地址提供 5 票支持。
* 只需要另外 2 名真实成员的支持即可达成 7 票（7/13，51%），决策通过。
2. 推翻证明系统的默认决定：
* 至少需要 7 名真实成员一致同意，才能达成 7 票（7/13），推翻默认决定。

总结
1.虚拟地址的定义：虚拟地址是多签系统中的逻辑实体，代表系统内的默认行为。

2. 引入目的：
* 增强证明系统的权重，防止恶意篡改。
* 简化治理流程，提高系统安全性。

3. 投票行为：虚拟地址能够投票，但行为是预定义的，始终支持证明系统的默认决定。
	
4. 实现方式：通过智能合约逻辑将虚拟地址集成到多签中，动态调整其数量以影响决策权重。


### 2025.01.21

Cannon 是 Optimism 的默认故障证明虚拟机（Fault Proof Virtual Machine，FPVM），用于在 OP Stack 区块链的争议游戏（Dispute Game）中处理故障证明。

### Cannon 由两个主要组件组成

1. 链上组件：MIPS.sol
* 这是一个智能合约，实现了 32 位、大端序的 MIPS III 指令集架构（ISA）。
* 它在以太坊虚拟机（EVM）中验证单个 MIPS 指令的执行。
* 该合约是无状态的，需要外部提供执行所需的状态信息。
2. 链下组件：mipsevm
* 这是用 Go 语言编写的实现，生成可在链上验证的 MIPS 指令执行证明。
* 它与 MIPS.sol 合约协同工作，确保在争议过程中正确执行指令。

在争议游戏中，当参与者对某个 L2 区块状态转换存在分歧时，Cannon 被用于执行 MIPS 指令，以验证争议状态的正确性。

需要注意的是，Cannon 只是可用于解决争议的 FPVM 实例之一，OP Stack 的模块化设计允许集成其他证明机制。


![image](https://github.com/user-attachments/assets/1513bd3f-3294-479c-a6d1-ae793b9b0cd4)

Offchain（链下部分）：
* 包含链下运行的逻辑和组件，主要负责生成、验证以及提交 MIPS 指令的执行证明。
* 包括 op-challenger、Cannon、op-program 和 op-preimage。

Onchain（链上部分）：
* 包含部署在以太坊区块链上的智能合约，主要负责验证链下提交的证明是否正确。
* 包括 DisputeGameFactory、FaultDisputeGame、MIPS.sol 和 PreimageOracle。

### 组件详细解析

链下组件（Offchain）
1. op-challenger：
* 负责触发争议游戏（Dispute Game），挑战不合法的状态更新。
* 与链上合约交互，提交或验证争议的中间状态。
2. Cannon：
* 是核心的链下故障证明虚拟机（FPVM），模拟 MIPS 指令的执行并生成证明。
* 提交执行过程和结果给链上合约进行验证。
3. op-program：
* 定义要验证的具体程序逻辑，包含 Layer 2 状态转换的详细实现。
* Cannon 使用它来模拟和执行 MIPS 指令。
4. op-preimage：
* 负责存储和提供 Cannon 需要的前映像（Preimage），即状态或数据的细节。
* 为 Cannon 提供验证数据。

链上组件（Onchain）
1. DisputeGameFactory：
* 负责创建新的争议游戏实例（FaultDisputeGame）。
* 是争议游戏的入口点。
2. FaultDisputeGame：
* 核心争议游戏逻辑所在，协调挑战者与被挑战者的交互。
* 管理链下提交的状态和证明，并调用 MIPS.sol 验证结果。
3. MIPS.sol：
* 智能合约实现，用于验证链下 Cannon 提交的 MIPS 指令执行证明。
* 解析和执行单条 MIPS 指令，确保其合法性。
4. PreimageOracle：
* 提供链上数据验证服务，用于验证提交的数据与原始状态的一致性。
* 与 MIPS.sol 配合工作，确保证明的完整性。

### 工作流程
1. 争议的触发：
* 当某个状态更新被质疑时，op-challenger 向 DisputeGameFactory 提交挑战，启动争议游戏。
2. 链下生成证明：
* Cannon 使用 op-program 和 op-preimage，模拟 MIPS 指令的执行，生成执行证明。
3. 链上验证：
* FaultDisputeGame 接受 Cannon 提交的证明，并调用 MIPS.sol 验证每条指令的正确性。
* PreimageOracle 提供链上数据，确保提交的证明与原始状态一致。
4. 争议解决：
* 如果验证通过，证明被接受，状态更新被确认。
* 如果验证失败，状态更新被拒绝，争议游戏结束。

### 2025.01.22

![image](https://github.com/user-attachments/assets/39ce8241-5cdb-4b6c-90c2-265cc93d7b90)

这张图展示了 Cannon 组件的整体架构（Cannon Component Overview），这是 Optimism 的故障证明虚拟机（Fault Proof Virtual Machine, FPVM）的核心设计部分，用于模拟和验证 MIPS 指令的执行。以下是图中各个模块的详细解释：

1. 核心模块

1.1 Cannon Runner

文件：run.go 和 instrumented.go
作用：
* Cannon 的运行引擎，负责协调整个执行流程。
* 调用其他模块来执行指令、管理状态和生成证明。
交互：
* 调用 Witness Proof Generation 来生成证明。
* 调用 Memory and State Management 处理内存和状态管理。

1.2 Witness Proof Generation

文件：witness.go
作用：
* 生成用于链上验证的执行证明（Witness Proof）。
* 将链下执行的操作记录为可以验证的链上数据。
交互：
* 接收来自 Cannon Runner 的调用，生成证明。

1.3 Memory and State Management

文件：memory.go、page.go、state.go
作用：
* 管理 MIPS 虚拟机的内存和状态，包括内存分页和状态快照。
* 确保指令执行时的数据一致性。
交互：
* 与 MIPSEVM 协作，提供内存和状态支持。

1.4 MIPSEVM

文件：mips.go
作用：
* MIPS 虚拟机核心，负责执行单个 MIPS 指令。
* 验证 MIPS 指令的合法性，并模拟指令的执行过程。
交互：
* 调用 PreimageOracle Server 获取预映像数据。
* 与 Memory and State Management 协作，处理指令所需的内存和状态。

1.5 ELF Loader

文件：load_elf.go、patch.go 和 metadata.go
作用：
* 负责加载和解析 ELF 格式的可执行文件（程序）。
* 将 MIPS 程序加载到虚拟机中，为模拟执行做好准备。
交互：
* 提供程序数据供 MIPSEVM 执行。

1.6 PreimageOracle Server
作用：
* 提供 MIPS 执行所需的外部数据或状态的前映像（Preimage）。
* 是链下和链上之间的数据桥梁。
交互：
* 被 MIPSEVM 调用，用于验证和获取外部状态。

2. 组件间的工作流程

程序加载：ELF Loader 从 ELF 文件加载 MIPS 程序，并将其提供给 MIPSEVM。

指令执行：
* MIPSEVM 模拟执行 MIPS 指令，调用 Memory and State Management 管理虚拟机的状态。
* 在需要外部数据时，调用 PreimageOracle Server 获取验证所需的前映像。

状态管理：Memory and State Management 负责保存和更新内存页和状态快照，支持指令的执行。

生成证明：Witness Proof Generation 在指令执行后生成证明数据，并将其返回给 Cannon Runner。

执行协调：Cannon Runner 作为核心协调者，负责调用各模块并管理整体流程。
----
链下执行 的 MIPS 程序通过模块化的设计完成指令执行、状态管理和证明生成。

关键功能：
* Cannon Runner 协调整体流程。
* MIPSEVM 模拟 MIPS 指令执行。
* PreimageOracle Server 提供外部数据支持。
* Witness Proof Generation 生成可供链上验证的证明。

通过这些模块的协作，Cannon 能够有效支持 Optimism 的争议解决和状态验证过程。

### 2025.01.23

### 2025.01.24

<img width="846" alt="image" src="https://github.com/user-attachments/assets/275651dd-e2c5-44c0-a87a-570933ce5e17" />

各个组件说明

**OP-Challenger（挑战者）：**
* 功能：挑战者的角色是监控并对无效的输出根（Invalid Output Root Proposals）提出挑战。
* 监控（Monitors）：挑战者不断监控提议的区块状态更新（例如，输出根），确保其正确性。
* 挑战（Challenges）：如果发现提议的输出根无效，挑战者可以提出挑战，阻止该提议被接受。
* 防御有效输出根提案（Defends Valid Output Root Proposals）：如果输出根是有效的，挑战者不会对其提出挑战。

与 OP-Proposer 的交互：
* 协助（Assists）：挑战者协助 OP-Proposer（提议者）解决争议和验证提案。

**OP-Proposer（提议者）：**
* 功能：提议者负责提出有效的输出根提案，并解决与挑战者的争议。
* 解决索赔（Resolves Claims）：当有争议或挑战时，提议者需要解决这些问题，确保提案的有效性。

与 OP-Challenger 的交互：
* 参与争议游戏（Dispute Games）：当挑战者提出挑战时，提议者参与争议解决的过程。
* 支付索赔（Claims Paid）：如果提案被判定无效，提议者需要支付与挑战者相关的赔偿。

**争议游戏（Dispute Games）：**
* 功能：当有争议时，挑战者和提议者通过争议游戏解决分歧，验证提案是否有效。

**保证金（Bonds for Challenger and Proposer）：**
* 功能：为了激励诚实参与并避免滥用，挑战者和提议者都需要为争议游戏支付保证金。
* 作用：如果挑战者的挑战被证明是有效的，他们可以从提议者那里获得赔偿；如果提议者胜诉，则挑战者的保证金将被没收。

### 流程概述

提议的提交：OP-Proposer 提交一个输出根提案（Valid Output Root Proposal）。

监控和挑战：OP-Challenger 监控这些提案，若发现无效的输出根提案（Invalid Output Root Proposal），就会提出挑战。

争议解决：当挑战发生时，OP-Proposer 和 OP-Challenger 进入争议游戏，争议得到解决。

保证金支付：根据争议的结果，OP-Proposer 或 OP-Challenger 可能需要支付保证金。

 总结

* OP-Challenger 和 OP-Proposer 通过争议游戏和保证金制度共同参与协议的安全性验证。
* OP-Challenger 主要负责监控提案并在发现无效提案时提出挑战，而 OP-Proposer 则解决这些挑战并支付相关赔偿。
### 2025.01.25

![image](https://github.com/user-attachments/assets/7f35e0c3-d724-4af4-ae6a-b008426f6ce5)

1. Fault Dispute Game（故障争议游戏）

* 作用：这是争议解决的核心，主要用于处理 Layer 2 状态更新的争议。参与者通过此游戏验证某个状态更新是否存在错误。

交互：
* 挑战者网络（Challenger Network） 监听和参与游戏，检查是否有任何故障。

2. Challenger Network（挑战者网络）

* 作用：挑战者网络负责监听和接收正在进行的争议游戏的状态更新，随时准备对新的错误状态提出挑战。

工作流程：
* 新索赔被发现（New claim detected in a game）：当游戏中发现新的错误或不合法的状态更新时，挑战者会接收到该信息。
* 挑战者随后会判断是否存在有效的反击步骤。

3. Game Solver（游戏解算器）

* 作用：这是一个负责审查并判断错误主张（claim）是否有效的角色。解算器根据争议的深度来确定下一步的操作。

工作流程：
* 有效的操作被发现（Valid move found）：
* 如果发现了一个有效的错误操作，解算器根据争议的深度进行攻击、防御或其他步骤。
* 这可能会触发争议的进一步处理，如调整状态或对抗错误。

没有有效的操作（No valid move）：
* 如果没有发现有效的错误或没有有效的操作步骤，解算器则不会采取任何行动，游戏继续。

总结
* Fault Dispute Game 是争议解决的关键组件，依靠 Challenger Network 来监听和检测潜在的错误状态。
* 当发现错误时， Game Solver 会根据错误的性质决定是否采取行动，如进行反击、挑战或忽略该错误。

这种机制确保了 Optimism 网络中的状态更新能够经过有效的验证和纠正，增强了其去中心化治理和透明性。

### 2025.01.26

**Optimism Interoperability**

互操作性 是一组协议和服务，允许 OP Stack 区块链相互读取对方的状态。

它提供以下好处：
* 1 块延迟的资产转移：解决了资本碎片化问题，提高了资本效率。
* 改善用户和开发者体验：简化了跨链交互，提升了整体体验。
* 安全的资产转移：如 ETH 和 ERC-20 代币，可以在不同的 Layer 2 之间安全地转移。
* 水平扩展性：满足需要的应用程序的扩展需求。

**互操作性架构**

在互操作性之前，OP Stack 节点由两部分软件组成：
* 共识客户端（例如 op-node）
* 执行客户端：负责处理用户交易和构建区块（例如 op-geth）

互操作性通过一个名为 OP Supervisor 的新服务来实现。
每个节点操作员除了运行 Rollup 节点和执行客户端外，还需要运行此服务。

**消息传递流程**

跨链消息需要两笔交易：
1. 初始化消息：在源链上创建，作为日志事件。
2. 执行消息：在目标链上创建，可能导致目标链上合约函数的执行。

目标链上的交易调用名为 CrossL2Inbox 的合约，执行或验证消息。
此调用需要唯一标识初始化消息，包括源链的链 ID、区块号、日志事件在该区块中的索引等信息。

**安全性**

跨链消息的安全性取决于块的安全级别：
* 本地安全：块已写入 Layer 1。
* 跨链安全：块及其所有依赖的块都已写入 Layer 1。

如果序列化器选择接受不安全的消息，它必须信任生成入站消息的序列化器，以及从传递依赖集中生成的任何引用的不安全消息。

**互操作性集群**

互操作性协议通过依赖集工作，依赖集在每个链上配置。
依赖集定义了可以与特定链发送和接收消息的链集。

例如，链 B 的依赖集可能包括链 A 和链 C。
要将资产从链 E 移动到链 B，需要先从链 E 移动到链 A，然后从链 A 移动到链 C，因为 B 和 E 之间没有直接的依赖关系。

**超级链互操作性集群**

超级链建立在互操作性协议之上，实现了一个具有完整依赖关系的单一网状网络。
在此模型中，超级链互操作性集群中的每个区块链都与其他每个区块链直接连接，创建一个完全连接的网状网络。
这种模型提供了最高级别的互操作性，因为任何区块链都可以直接与任何其他区块链进行交易。

超级链互操作性集群中的每个区块链共享相同的安全模型，以减轻最弱环节的风险。
如《标准 Rollup 宪章》所述，这些链共享相同的 Layer 1 ProxyAdmin 所有者。
对超级链互操作性集群的任何更改必须遵循标准的协议升级投票程序——这是超级链修改的既定治理流程。

<img width="860" alt="image" src="https://github.com/user-attachments/assets/09ca8e87-8c5f-4ace-ac4d-493f1d39cd87" />

各个组件说明
1. OP Stack chain #1, OP Stack chain #2, OP Stack chain #3
* 这些代表了不同的 OP Stack 链，它们在不同的区块链上运行并管理不同的交易和状态。每条链都负责自己的数据存储和计算。
* 每条链都通过 log events（日志事件）与 OP-Supervisor 进行通信，确保信息的一致性。
2. L1 Consensus Layer
* 这是一个连接 OP Stack 链和 Layer 1（例如，以太坊）的组件。它负责提供最终的共识层并同步 OP Stack 上的状态到 Layer 1。
* block status（区块状态）指示 Layer 1 上区块的最终状态，帮助 OP Stack 链同步区块数据。
3. OP-Supervisor
* 这是一个中央协调组件，负责管理所有 OP Stack 链之间的操作。它与每条链交互，接收来自不同链的日志事件并根据这些事件进行决策。
* 它的主要作用是管理链的交互和确保多个链之间的一致性，特别是在跨链消息传递和状态更新方面。
4. Execution Engine
* 这个组件位于 OP Stack chain #1 中，负责执行从 OP-Supervisor 传递的命令。
* Execution Engine 执行区块链上的操作，如计算和状态更新，确保在多个链之间同步这些操作。
5. OP Node
* 这是每个 OP Stack 链的核心节点，处理并验证事务的真实性。
* 这些节点通过 OP-Supervisor 进行交互，并通过执行引擎来处理实际的区块和事务。

工作流程

1. 跨链消息传递：
* 每条 OP Stack 链通过 log events 向 OP-Supervisor 提交日志事件。这些事件通常包含有关区块更新、交易和其他状态变更的信息。
2. OP-Supervisor 协调：
* OP-Supervisor 收到来自不同链的日志事件后，它根据这些事件进行协调和处理。它确保每条链都按照适当的顺序和规则执行跨链操作。
3. 执行操作：
* Execution Engine 执行从 OP-Supervisor 提交的操作。执行引擎确保这些操作正确地应用于区块链的状态更新。
4. Layer 1 同步：
* OP Stack 链通过 L1 Consensus Layer 与 Layer 1（如以太坊）同步，以确保区块数据的最终一致性。

<img width="815" alt="image" src="https://github.com/user-attachments/assets/a9a50855-3007-4e58-ad54-a4ae6f89c44b" />

这张图展示了 跨链消息传递 的过程，具体是如何在 Optimism 的 OP Stack 系统中实现跨链通信的。以下是图中各个组件和流程的详细解释：

1. 流程说明

(1) 应用层（Application）
* 事务提交：
* 应用程序发起一笔交易（Transaction），该交易将在源链（Source Chain）上进行处理。

(2) 源链（Source Chain）
* 生成日志事件（Log Event）：
* 源链在交易执行时生成 日志事件，这时该事件被标记为 “Initializing Message”（初始化消息），表示消息的开始，准备向目标链传递。
* 这条消息会通过 OP-Supervisor 发送。

(3) OP-Supervisor
* OP-Supervisor 协调跨链消息的发送和接收：
* 它接收到来自源链的日志事件，并将其处理后发送到目标链，确保消息的正确性和完整性。
* 它负责处理消息的传递，并监控目标链是否成功接收并处理该消息。

(4) 目标链（Destination Chain）
* 执行消息（Execution Message）：
* 在目标链上，OP-Supervisor 向目标链的执行引擎发送请求，调用 CrossL2Inbox 来执行或验证传递过来的消息。
* 目标链检查是否收到来自源链的初始化消息。
* 如果接收到该消息，目标链将继续执行消息，生成 Executing Message（执行消息）。

(5) CrossL2Inbox
* CrossL2Inbox 是目标链上的合约，负责执行和验证跨链消息：
* 它检查是否成功接收到来自源链的消息，并确保消息的有效性。
* 如果成功执行消息，它会发出 Executing Message，并确认消息已被成功处理。

(6) 执行引擎（Execution Engine）
* 执行最终操作：
* 执行引擎根据目标链收到的消息更新目标链的状态，完成跨链操作。

2. 关键步骤
* 源链生成日志事件，发送初始化消息。
* OP-Supervisor 将消息转发到目标链。
* 目标链上的 CrossL2Inbox 验证和执行消息。
* 如果目标链成功接收并执行该消息，Executing Message 被发出。

<img width="771" alt="image" src="https://github.com/user-attachments/assets/4fa2d8d3-9f9a-4d97-8431-2a51d05009dc" />

这张图展示了 跨链消息传递的时序，说明了不同区块链之间如何在多个区块之间进行消息传递和执行。图中的主要概念是 初始化消息（Initiating Messages） 和 执行消息（Executing Messages） 之间的交互。

各个组件与流程解释

1. Chain A 和 Chain B（链 A 和 链 B）
* Chain A 和 Chain B 是两个不同的链（可以视为 Optimism 上的不同 Rollup 链）。这两条链上的区块包含了 初始化消息（Initiating Messages），这些消息用于在不同链之间传递数据。
* 每个链中都包含不同的区块，例如：
* Chain A 上有 Block n，Block n+100 和 Block n+105。
* Chain B 上有 Block m 和 Block m+3。

2. Chain C（链 C）
* Chain C 是接收跨链消息并执行的目标链。
* 在 Chain C 上，所有接收到的初始化消息会被处理，并且在目标链上执行时生成 执行消息（Executing Messages）。
* Block with executing messages 表示该链中的区块已经成功执行了来自其他链的消息。

3. 过程与时间顺序
* 初始化消息的传播：
* Chain A 上的区块（如 Block n、Block n+100、Block n+105）和 Chain B 上的区块（如 Block m 和 Block m+3）会依次生成和发送 初始化消息。
* 这些初始化消息通过 OP-Supervisor 被转发到 Chain C。
* 执行消息的生成：
* Chain C 接收到这些初始化消息后，会执行与这些消息相关的操作。
* Chain C 上的 Block with executing messages 就是一个标记，表示该区块包含已经执行并处理的跨链消息。

4. 消息同步与时延
* 不同链的区块会存在时间上的差异。例如，链 A 和链 B 中的区块在不同时间生成和提交消息。Chain C 必须等待接收到这些初始化消息，并在相应的区块中执行这些消息，最终生成执行结果。

总结

这张图清楚地展示了在多个链之间如何通过 初始化消息 和 执行消息 来进行跨链通信。每个链生成消息并通过 OP-Supervisor 进行协调，最终在 Chain C 上执行这些消息。图中的时序和跨链消息传递展示了如何确保不同链之间的数据一致性和操作同步。








<!-- Content_END -->
