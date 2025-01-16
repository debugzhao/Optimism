---
timezone: Asia/Shanghai
---

# Oscar

1. A eco-lifelong learner. To surf🏄‍♀️ better in the Web3 world. Enjoy this challenging vibe and become cooler 🆒.
2. 你认为你会完成本次残酷学习吗？ Yes. 

## Notes

<!-- Content_START -->

### 2025.01.06 

学习主题：Optimism 的基本概念 

- Optimism 使用的是OP Rollup，这是一种比较花哨的说法，指的是一个区块链，它利用另一个“父”区块链的安全保障。具体来说，OP Rollup 利用其父链（以太坊）的共识机制（例如工作量证明 PoW 或权益证明 PoS），而不是构建自己的共识机制。

- Optimism 的核心在于一个基本假设：**大多数交易都是诚实的**。该系统基于这样的假设：提交到Rollup的交易是有效的。这种“乐观”的方法与其他 Layer-2 解决方案（如 ZK-Rollups）相比，最大限度地减少了计算开销，因为它不需要为每笔交易生成计算成本高昂的有效性证明。在Rollup的背景下，Optimism 的核心思想是用速度和成本效率来权衡立即验证，依靠激励系统和欺诈证明来确保系统的完整性。这是速度/成本和安全性之间的平衡。一些关键概念：
  * **Rollup：** Rollup 是一种 Layer-2 扩容解决方案，它在链下处理交易，然后将这些交易的汇总记录提交到主链（Layer-1）上。这减少了主链上的拥塞和交易费用。
  * **Optimistic Rollup** 处理交易时不会立即验证。在证明无效之前，它们被假定为有效。这使得交易更快更便宜。
  * **欺诈证明：** 如果有人提交了欺诈交易，任何人都可以通过提交*欺诈证明*来挑战它。该证明证明了交易的无效性，系统会撤销欺诈交易。提交欺诈证明的激励通常是奖励制度。
  * **挑战期：** 在交易批次提交到 Layer-1 区块链后，有一个时间窗口（挑战期）。在此期间，任何人都可以提交欺诈证明来挑战该批次中交易的有效性。如果在此期间没有提交欺诈证明，则该批次被视为最终确定。
  * **Sequencer：** 一个中心实体（或一组实体），称为排序器，负责排序和捆绑 Optimistic Rollup要处理的交易。排序器的作用至关重要，其潜在的恶意行为是系统设计和安全性的关键考虑因素。

- OP Rollups 与 ZK-Rollups 区别：

  - **ZK-Rollups：** 这些使用零知识证明来密码学地证明交易的有效性，而无需透露交易细节。这提供了更高的安全级别，并且不依赖于挑战期。
  - **Optimistic Rollups：** 这些依赖于诚实行为的假设和欺诈证明机制。这通常比 ZK-Rollups 更快更便宜，但如果排序器是恶意的或欺诈交易没有及时挑战，则安全性较低。

### 2025.01.07

学习主题：Layer2 扩容方案 https://docs.optimism.io/stack/rollup/overview

- OP Stack 是为 Optimism 提供支持的一套软件——目前以 OP 主网背后的软件实现的形式出现，最终将以 Optimism 超级链及其治理的形式出现。它由Optimism Collective维护，但是正变得越来越社区化，相关权利和职责正逐步向社区下放。随着超级链概念的出现，对于 Optimism 来说，轻松支持安全创建可在拟议的超级链生态系统中互操作的新链变得越来越重要。 因此，OP Stack 主要专注于创建一个共享的、高质量的、完全开源的系统，用于**创建新的 L2 区块链**。 通过协调共享标准，Optimism Collective可以避免在孤岛中重复构建相同的软件。
- **OP Stack可以被视为软件组件，可以帮助定义 Optimism 生态系统的特定层，也可以充当现有层中的模块。** 尽管 OP Stack 当前的核心是运行 L2 区块链的基础设施，但 OP Stack 理论上可以扩展到底层区块链之上的层，包括区块浏览器、消息传递机制、治理系统等工具。

### 2025.01.08

学习主题：Superchain  https://docs.optimism.io/stack/explainer

- Superchain超级链是Optimism Collective 对 OP 未来发展方向的远景规划。具有超强可扩展性的去中心化计算能力是发展超级链的原始动力。

- 超级链是一个 L2 链网络，称为 OP Chains，共享安全性、通信层和开源技术堆栈(未来也就是OP Stack)。然而，与多链设计不同，这些链是标准化的，旨在用作可互换的资源。这使得开发人员能够构建以整个超级链为目标的应用程序，并抽象出应用程序运行的底层链。

### 2025.01.10

学习主题：Stage 的介绍 https://medium.com/l2beat/introducing-stages-a-framework-to-evaluate-rollups-maturity-d290bb22befe

在不断发展的区块链技术领域，Rollup 已经成为以信任最小化方式扩展以太坊的有前景的解决方案。然而，这些系统的开发通常涉及一个中心化控制阶段，通常被称为“辅助轮”，这允许在受控环境中进行系统更新和错误修复。

虽然在早期阶段是必要的，“辅助轮”最终应该被移除，以便 Rollup 能充分继承底层的安全特性。为了指导这一过渡，引入了一个新的框架，其灵感来自 Vitalik 提出的里程碑，该框架根据 Rollup 对这些“辅助轮”的依赖程度将其分为三个不同的阶段：

**阶段 0——完全依赖辅助轮：**在这个阶段，Rollup 有效地由运营商运行。尽管如此，仍然存在一个源代码公开的软件，允许根据 L1 上发布的数据重建状态，用于将状态根与建议的状态根进行比较。

**阶段 1——有限依赖辅助轮：**在这个阶段，Rollup 向由智能合约治理过渡。然而，安全委员会可能仍然存在以解决潜在的错误。这个阶段的特点是实现了完全功能的证明系统、欺诈证明提交的去中心化以及无需运营商协调即可进行用户退出。安全委员会由各种各样的参与者组成，提供安全保障，但其权力也构成潜在风险。

**阶段 2——无辅助轮：**这是最终阶段，Rollup 完全由智能合约管理。此时，欺诈证明系统是无需许可的，并且在发生意外升级的情况下，用户有充足的时间退出。安全委员会的角色严格限于处理可在链上裁决的健全性错误，并且用户受到保护，免受治理攻击。

### 2025.01.11

学习主题：https://learnblockchain.cn/article/3703

目前主要有四种技术方案：Optimistic Rollup、ZK Rollup、Plasma、Validium。每种方案都在安全、可扩展性、开发复杂性和去中心化之间进行权衡。“最佳”方案取决于项目的具体需求和优先级。ZK Rollup通常以其高安全性和快速最终确认而闻名，而Optimistic Rollup则被认为更易于开发。Plasma提供灵活性，但安全性更复杂。Validium为了提高速度牺牲了完全的去中心化。

### 2025.01.13

学习主题：治理理念 https://community.optimism.io/welcome/welcome-overview

Optimism Collective 旨在通过构建一个由标准化链组成的可扩展超级链，并结合创新的“影响即利润”的经济模型和双重议院治理结构（Token House 和 Citizens' House），来创建一个更去中心化、更安全、更可持续的以太坊生态系统。其治理机制仍在不断迭代和完善中，并通过一系列文件来指导其发展。 Retro Funding 是其核心经济机制，奖励对生态系统做出贡献的个人和项目。

治理文件:

- 《工作宪法》([Working Constitution](https://gov.optimism.io/t/working-constitution-of-the-optimism-collective/55)): 概述 Collective 的治理条款和原则。
- 《运作手册》([Operating Manual](https://github.com/ethereum-optimism/OPerating-manual/blob/main/manual.md)): 描述 Token House 的当前治理流程，会随着 Collective 的发展而演变。

### 2025.01.14

学习主题：投票机制 https://github.com/ethereum-optimism/OPerating-manual/blob/main/manual.md

Optimism Collective 的治理由两院组成：代币持有者议院 (Token House) 和公民议院 (Citizens’ House)。

- 在代币持有者议院中，OP 持有者负责提交、审议和投票各种 Optimism Collective 治理提案。他们可以通过直接投票（在将其 OP 投票权委托给自己地址后）或将其 OP 投票权委托给符合条件的第三方来进行投票。拥有委托 OP 投票权的地址被称为“代表”。

- 在公民议院中，Optimism 公民负责通过名为“追溯性公共产品资助”（Retro Funding）的流程向公共产品建设者分配奖励。参与 Retro Funding 3 并通过 AttestationStation 智能合约中的条目进行标记的徽章持有者现在是公民。公民身份目前是临时的。公民还负责对升级提案的否决进行投票。

所有代币持有者议院和公民议院的代表都应负责任地行使权力，并遵守 [Rules of Engagement](https://gov.optimism.io/t/rules-of-engagement-2-0/5728) and [Optimist Expectations](https://gov.optimism.io/t/optimist-expectations/7241).

代币持有者议院治理的主要工具目前包括：

- **代币持有者议院治理合约 (Token House Governance Contract):** 代币持有者议院治理提案的链上投票合约。所有符合条件的代币持有者议院治理提案都将在此提交投票。
- **Optimism 治理门户网站 (Optimism Governance Portal):** 一个前端界面，使代币持有者议院成员能够委托和投票他们的 OP。
- **公民议院 Snapshot 空间 (The Citizens’ House Snapshot Space):** 一个前端界面，使公民议院成员能够否决代币持有者议院的提案。
- **Optimism 论坛 (The Optimism Forum):** 一个讨论和审议治理提案的平台。
- **Discord:** 用于非正式的治理讨论和反馈。
- **Github:** 拨款（使命请求）通过此公共 github 存储库中的问题进行管理。
- **Charmverse:** 社区主导的 Optimism 拨款委员会的所在地。

随着治理的演变，这些工具或其用途可能会随着时间而改变。例如，将来可能会开发专门用于治理委员会的其他用户界面。同样，虽然投票目前通过治理合约在链上进行，但成功的投票目前由 Optimism 基金会管理和实施，这种情况不应无限期持续下去。

### 2025.01.15

学习主题：投票机制 https://github.com/ethereum-optimism/OPerating-manual/blob/main/manual.md

了解委员会 https://gov.optimism.io/search?q=council

- [Code of Conduct Council](https://gov.optimism.io/t/code-of-conduct-council-season-6-retrospective/9286)
- [Security Council ](https://gov.optimism.io/t/security-council-communication-thread/7726)
- [Grants **Council**](https://gov.optimism.io/t/grants-council-season-3-launch/4833)

**Process TLDR**

- Proposals are reviewed over a three week voting cycle.
- If you’re submitting a grant application, you’ll need to submit your application as outlined on each individual Mission Request in [github.](https://github.com/ethereum-optimism/ecosystem-contributions/issues?q=is%3Aissue)
- For all other proposal types, you may draft a proposal based on [this](https://gov.optimism.io/t/standard-proposal-template-optimism-token-house/5443) template and post it on the Forum with [Draft] in the title for feedback. Delegates and/or Citizens will provide feedback on your proposal in the forum. Use your judgment to incorporate feedback.
- Once your non-grant proposal has been approved by four top 100 delegates or four Citizens add a link to your proposal to the Voting Cycle Roundup thread by the last day of Week 2 and update the title from [Draft] to [Final]. These proposals will move on to Week 3 voting. Proposals initiated by the Foundation do not require approvals.
- Protocol or Governor Upgrades approved by the Token House, must also pass the Citizens’ House Veto Procedure, as outlined in the Veto Procedure section above, before they are considered officially approved.
- The Security Council will enact officially approved Protocol or Governor Upgrades. The Optimism Foundation will facilitate the administration of all other approved proposals, including by distributing any approved OP grants. The Foundation will be in touch to collect additional information from your project in order to execute the proposal or grant, including information to perform KYC.
- If your proposal is passed, the Optimism Foundation will facilitate its administration, including by distributing any approved OP grants. The Foundation will be in touch to collect additional information from your project in order to execute the proposal or grant, including information to perform KYC.
- If your proposal fails, you can make a new proposal in the next cycle specifying how you have incorporated significant changes from your first proposal.

**The Citizens’ House also manages the allocation of Retro Funding:**

- Citizenship is currently temporary, with the Retro Funding 3 Citizens recorded via entries in the AttestationStation.
- Retro Funding rounds occur in intervals and according to a predefined process, which currently includes phases for scoping, application creation, application review, voting, and disbursements. The Foundation will collect information from projects in order to distribute the grant, including information to perform KYC.

### 2025.01.16

学习主题：RetroPGF https://community.optimism.io/citizens-house/how-retro-funding-works

回溯式公共产品资助（Retro Funding）基于这样一个理念：相较于预测未来哪些项目有用，评估过去哪些项目有用更容易达成共识。这是一系列实验，Optimism Collective 的公民议会成员将剩余协议收入或 Retro Funding 代币分配的一部分，分配给那些他们认为对 Optimism Collective 和整个超级链产生了积极影响的项目。这是 Optimism “影响=利润”价值观的核心：对集体产生积极影响应该与个人获得的利润成比例地奖励。

这些奖励为人们构建有益于 Optimism Collective 的公共产品创造了强大的激励。其累积效应是一个更容易构建、学习和连接的生态系统，进而推动应用程序的使用并产生对区块空间的更多需求。通过可持续地资助公共产品，集体可以创建一个丰富的生态系统和更好的经济。

![](https://community.optimism.io/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fhow-retro-funding-works.9368ab75.png&w=3840&q=75)

**对实验的承诺：奖励影响**

回溯式资助是对构建未来乐观主义者想要看到的未来的长期押注。集体将定期进行回溯式资助，每一轮都与上一轮不同。这是一个新兴的过程，需要社区参与才能发展和完善。

- 回溯式资助第一轮于 2021 年底进行，向 58 个项目分配了 100 万美元。
- 回溯式资助第二轮于 2023 年第一季度进行，向 195 个项目分配了 1000 万个 OP 代币。
- 回溯式资助第三轮于 2023 年第四季度进行，向 501 个项目分配了 3000 万个 OP 代币。
- 回溯式资助第四轮将于 2024 年第二/三季度进行，将奖励为 Optimism 的成功做出贡献的链上建设者。
- 可在 [retrofunding.optimism.io](http://retrofunding.optimism.io/) 注册参与未来的轮次。

**实验框架**

回溯式资助具有三个核心组成部分，每个部分都有大量的实验空间：

- **影响范围界定：**集体应该资助什么？如何定义和决定？
- **影响评分：**公民议院如何评估影响？我们使用什么单位、流程或工具？
- **影响结算：**投票如何运作？

在最初几轮回溯式资助中，Optimism 基金会将根据社区的意见决定范围和投票机制。最终，关于资助什么、资助多少以及如何投票的变量将由公民议院决定，并由代币议院进行制衡。您可以在此处阅读有关开放元治理路径的更多信息。随着时间的推移，集体旨在扩大回溯式资助的范围，以支持在 Optimism 生态系统之外生产公共产品。为了实现这一目标，我们必须根据定期的实验来改进回溯式资助中使用的工具和流程。



<!-- Content_END -->
