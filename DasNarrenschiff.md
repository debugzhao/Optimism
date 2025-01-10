---
timezone: Asia/Shanghai
---
# loxia

https://x.com/Loxia_in_Tj

## Notes

<!-- Content_START -->

### 2025.01.06

Superchain 速览

愿景：通过标准化和模块化的技术栈，实现跨链数据和资产的无缝流转，同时共享以太坊的安全性和资源。

Superchain 内的每条链都需要将排序器总收入或利润的 15% 支付给 Optimism Collective，旨在聚合 L2/L3s 的流动性，引导形成网络效应。

- ERC-7802 对 SuperChain 交易的影响。
    - **提升跨链交易效率：**ERC-7802 通过标准化的跨链接口（如 `crosschainMint` 和 `crosschainBurn`），简化了资产在 Superchain 生态系统中的转移流程。用户不再需要依赖复杂的跨链桥或多重签名验证，而是可以直接通过统一的接口完成资产转移。这种标准化设计显著提升了跨链交易的效率，减少了操作步骤和等待时间。
        - **区块延迟**：Superchain 的原生互操作性使得资产转移的延迟降至 1 个区块，极大提高了资本效率。
        - **无需资产包装**：ERC-7802 避免了传统跨链桥中常见的资产包装（Wrapped Token）问题，用户可以直接使用原生代币进行跨链操作。
    - **增强资本效率：**ERC-7802 通过“销毁-铸造”机制（Burn-Mint）实现了跨链资产的无缝转移，避免了传统跨链桥中流动性池的资产锁定问题。这使得资产可以在 Superchain 生态中自由流动，最大化利用效率。
        - **聚合流动性**：Superchain ERC20（基于 ERC-7802 的实现）允许资产在不同链之间共享流动性，减少了流动性碎片化问题。例如，1M usd 的资产可以在 Superchain 的所有链上使用，而不需要在每条链上分别锁定资金。
        - **降低链间+运营成本**：通过优化链间通信和资源利用，ERC-7802 减少了跨链交易的成本，吸引了更多用户和开发者参与 Superchain 生态。
    
    并且 ERC-7802 的模块化设计将跨链逻辑从代币合约中分离出来，开发者只需关注代币的基本功能，而无需处理复杂的跨链实现细节。标准化的跨链接口也减少了中间环节，降低了跨链桥被攻击的风险。
    
- Base 在生态、治理和协作层面更深地绑定 SuperChain 的整体框架意味着什么？
    - Base 通过收入共享协议向 Optimism 支付 2.5% 的排序器收入或 15% 的利润，同时获得 1.18 亿 OP 代币（分六年支付），用于生态激励和治理参与，OP 和 Base 在战略利益上将长期绑定。
    - Base 将参与 Optimism 提出的“Law of Chains”治理框架，与 Superchain 实现更硬性的绑定。
        - Base 将作为实践“Law of Chains”治理框架的良好示范，以吸引更多链和开发者加入。
    - Base 的治理权限将逐步转移至由全球独立社区成员组成的安全理事会，推动 Superchain 的去中心化进程，Base 将在安全理事会中拥有部分治理权限，但其投票权限不超过总权限的 9%
    - OP 无疑是目前 L2 生态中最去中心化和最具生态多样性的，Base 依托 Coinbase 和相关经验可以为 OP 拓展更多现实世界的可能性，而 Base 也需要 OP 的去中心化治理/运营模式，及经验。

### 2025.01.09

## Retro Funding 的演变

Retro Funding 的历史：

在早期的 Retro Funding 中，追溯的只包含公共物品，例如  RetroPGF 3 的目标：

> *“Optimism 的追溯性公共物品资助（Retroactive Public Goods Funding, RetroPGF）的目标是通过追溯性分配奖励，实现“**影响力=利润**”的原则——即对集体的积极影响应转化为个人的利润。这一原则作为北极星，激励创建一个更具生产力和可持续性的经济体系。*
> 

> ***影响力**：表示贡献者为 Optimism 集体创造的价值。*
> 

> ***利润**：表示贡献者从 Optimism 集体中提取的价值。*
> 

> ***差距**：表示贡献者的影响力与利润之间的差异。*
> 
> 
> *（例如：影响力 - 利润 = 差距）*
> 

> *RetroPGF 填补了贡献者的影响力与利润之间的差距，从而实现“**影响力=利润**”的状态。”*
> 

Retroactive Public Goods Funding 1 ~ 3（回溯性公共物品激励） 资助了很多优秀的公共物品，如 RPGF 2 中的 ZachXBT，ZashXBT 是加密货币领域的“无面侦探”，通过链上分析技术揭露骗局、追踪被盗资金，为行业透明度和安全性做出了巨大贡献，这些贡献没有直接激励网络增长，但却对整个集体产生了非常积极的影响力，使整个网络更稳健。所以 OP 的 Citizen House 中的徽章持有者会投票给 ZachXBT，ZachXBT 在 RPGF 2 中获得了近 19 万 OP

而在 Retro Funding 4 中，社区考虑到之前三轮 RPGF 缺乏对 OP 网络实际使用者的支持（在 RPGF 3 中只分配了 5% 的奖励给到网络实际使用量中前 20% 的使用者），尤其缺乏对 Superchain 上开发者增长的支持，并且 OP 社区的徽章持有者对 Retro Funding 的可持续性提出了担忧，在 Retro Funding 的 1~3 轮次，Retro Funding 依赖 850M OP 的回溯性公共物品资助（RPGF）来发放奖励。

在 Retro Funding 的第 4 轮次及之后，Retro Funding 将逐渐转向依赖协议盈余收入作为奖励来源，而之前的协议盈余收入不足以维持回溯性公共物品资助，所以 Retro Funding 在鼓励公共物品创新之外，还肩负起了直接激励网络增长的任务，**于是 Retro Funding 在第 4 轮次时首次提出对链上贡献者的资助（Onchain Builder）**，以激励开发者增长和网络活动的增加。

在 Retro Funding 4 中，Retro Funding 开始首次资助如 DeFi 类的与链上直接贡献（影响力）有关的项目，与前几轮不同，在 RF4 及之后的轮次 RF 开始着重于激励影响力本身的增长，即使受资助的项目本身不缺乏资金。

Retro Funding 5 主要激励了对 OP Stack 的生态工具类项目（Utility），如集成和负载测试基础设施、运行 Optimism 节点的脚本、RaaS 提供商、OP Stack 教程与文档。Retro Funding 6 则专注于治理类别的激励，主要奖励那些在 **治理基础设施、治理分析** 和 **治理领导力** 有突出贡献的项目**。**

Retro Funding S7‘s 3 main points:

1. Retro Funding: S7 Missions
    - 聚焦于以数据驱动的影响力衡量，并采用以人为中心的方法。这些任务（Missions）的选择旨在让集体能够准确衡量一部分重要贡献。
    - 整个集体围绕共同任务框架的对齐将确保所有代币分配计划的协调运作。
    - 评估算法定义了任务产出和结果的衡量方式。它可以包括人类定性评估和数据驱动的定量测量。奖励通过在某个或多个测量日期运行评估算法来分配。追溯资助任务中使用的评估算法将根据选定公民的反馈在整个追溯资助计划中不断演进。
    - （像是 Deep Funding 的尝试）
2. Retro Funding: Onchain Builders (8M OP Max)
    - 链上建设者奖励那些通过跨链互操作性推动资产转移的项目，这些项目通过在符合条件的OP链上扩展超级链来实现。
    - 评估算法的衡量标准：
        - SuperChain 采用率的增长
        - 高质量的链上价值（例如，TVL）
        - 跨链互操作性的支持与采用
            - 二月开始进行评估，奖励每月发放。
3. Retro Funding: Dev Tooling (8M OP Max)
    - 奖励那些支持建设者在 SuperChain 上开发链上应用的工具链软件，如编译器、库和调试器。
    - 评估算法的衡量标准：
        - 链上建设者的采用率。
        - 工具在链上应用开发中的重要性。
        - 支持建设者在 SuperChain 跨链互操作性采用的组件。
            - 二月开始进行评估，奖励每月发放。
         

### 2025.01.10

Pending research link list:

https://docs.contributionism.io/contributionism/characteristics/cooperative-and-competitive-environments

https://mirror.xyz/optimismcn.eth/uJcBF6kl9UwUFOjCt6SnmkZBz_CUsK-W8debwVUnv6g

Accelerated Decentralization Proposal For Optimism (GFX labs)
https://gov.optimism.io/t/accelerated-decentralization-proposal-for-optimism/8875

Insightful philosophical perspectives on governance (polynya)
https://polynya.mirror.xyz/

Delegate nodes to learn:

https://optimism.curiahub.xyz/delegate/delegate.l2beat.eth

https://optimism.curiahub.xyz/delegate/joxes.eth

https://optimism.curiahub.xyz/delegate/opmichael.eth

https://vote.optimism.io/delegates/0x5d36a202687fd6bd0f670545334bf0b4827cc1e

https://david.truong.vc/

seed gov



### 2025.01.11

<!-- Content_END -->
