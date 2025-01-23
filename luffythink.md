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

回溯式公共产品资助（Retro Funding）基于这样一个理念：相较于预测未来哪些项目有用，评估过去哪些项目有用更容易达成共识。这是一系列实验，Optimism Collective 的公民议会成员将剩余协议收入或 Retro Funding 代币分配的一部分，分配给那些他们认为对 Optimism Collective 和整个超级链产生了积极影响的项目。这是 Optimism “影响=利润”价值观的核心：**对集体产生积极影响应该与个人获得的利润成比例地奖励。**

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

### 2025.01.17

学习主题：RetroPGF 获奖项目https://round6.retrolist.app/ 

Positive impact to the community should be rewarded with profit to the builder.

- Governance Infra & Tooling 46 
- Governance Analytics 22 
- Leadership 20

乐观治理词汇表：[Optimism Governance Glossary - Get Started 🌱 - Optimism Collective](https://gov.optimism.io/t/optimism-governance-glossary/9407)

- **反捕获委员会 (Anticapture Commission)**：反捕获委员会的职责是防止 Token House 被任何单一利益相关方或利益相关群体所控制。该委员会由具有重大影响力的个人代表组成，当发现利益相关群体之间的权力失衡时，它会向 Citizens’ House 发出警告。反捕获委员会使用来自治理基金的 1000 万 OP 进行投票，适用于所有可能受到 Citizens’ House 否决的提案。[了解更多](https://github.com/ethereum-optimism/OPerating-manual/blob/main/Anticapture Commission Charter v2.0.md)

- **公民 (Citizen)**：公民是 Collective 的个人人类利益相关者，包括建设者、用户和社区成员。这些人群与项目价值观保持一致，并关注 Collective 的长期利益。公民拥有对协议升级的否决权，并将逐渐负责更多的治理决策。[了解更多](https://community.optimism.io/citizens-house/citizen-house-overview)

- **Collective 反馈委员会 (Collective Feedback Commission)**：Collective 反馈委员会是一个实验性计划，旨在促进基金会与高背景贡献者之间在治理系统设计上的协作。目标是开发一个“核心治理计划 (Core Governance Program)”，以便 Collective 能够在未来承担元治理职责。委员会由活跃的公民和代表组成，受邀者基于其在相关领域的贡献和专业知识，通过基金会签发的认证证明。[了解更多](https://gov.optimism.io/t/the-collective-feedback-commission-the-next-iteration/9113)

- **代表 (Delegate)**：代表构成了 Token House，他们负责对影响 Collective 的提案（如 OP Stack 升级、委员会成员选举、目标预算等）进行投票。他们由 OP 代币持有者委任，代表持有者做出治理决策。[查看代表](https://vote.optimism.io/delegates)

- **开发者顾问委员会 (Developer Advisory Board)**：开发者顾问委员会由一群开发者组成，负责为技术提案提供反馈和指导。他们确保技术专业知识为治理决策提供依据，特别是在技术去中心化方面。委员会成员由 Token House 代表选举产生。[了解更多](https://github.com/ethereum-optimism/OPerating-manual/blob/main/Developer Advisory Board Charter v1.1.md)

- **拨款委员会 (Grants Council)**：拨款委员会负责提议拨款预算、审核拨款申请并选择拨款接收者。成员对治理基金拨款流程拥有完整的决策权。委员会成员由 Token House 代表选举产生。[了解更多](https://github.com/ethereum-optimism/OPerating-manual/blob/main/Grants Council Charter v0.1.md)

- **OP Stack 接近度排名 (OP Stack Proximity Ranking)**：这一实验性排名基于开发者和代码库与 OP Stack 代码库的接近程度进行评估。通过 GitHub 事件数据和双向信任图，应用 EigenTrust 和 Hubs & Authorities 算法的变体。信任通过用户行为（如星标、分叉）和贡献（如合并的 PR）构建。评分涵盖超过 3 万个代码库和 2000 个组织。OP Stack 接近度排名是与 OpenRank 和 Open Source Observer 合作开发的。[查看 OpenRank 文档](https://docs.openrank.com/integrations/github-developers-and-repo-ranking)

- **安全委员会 (Security Council)**：安全委员会是一个去中心化的个人行动者小组，负责执行 Superchain 的共享升级。主要职能包括实施治理批准的协议升级和角色变更，并在紧急情况下独立行动以维护网络安全。委员会成员由 Token House 代表选举产生，并根据技术能力、声誉、地域多样性以及与 Optimistic Vision 的一致性进行评估。[了解更多](https://github.com/ethereum-optimism/OPerating-manual/blob/main/Security Council Charter v0.1.md)

- **前 100 代表 (Top 100 Delegate)**：前 100 代表是拥有最多投票权的 Token House 前 100 名代表。[查看代表](https://vote.optimism.io/delegates)

- **里程碑与指标委员会 (Milestones and Metrics Council)**：里程碑与指标委员会负责衡量获得拨款的项目是否完成里程碑任务，并向拨款委员会选出的接收者发放拨款。委员会成员由 Token House 代表选举产生。[了解更多](https://github.com/ethereum-optimism/OPerating-manual/blob/main/Milestones and Metrics Council Charter v0.1.md)

### 2025.01.20

学习主题：Superchain 基本介绍 https://docs.optimism.io/stack/explainer

超级链的概念：一个共享桥接、去中心化治理、升级、通信层等等的链网络——所有这些都构建在OP Stack之上。超级链的启动将把OP主网和其他链合并成一个统一的OP链网络（即超级链中的链），标志着向为世界带来可扩展和去中心化计算迈出的重要一步。

Optimism 的超级链旨在通过创建一个共享安全、通信层和开源技术栈的 L2 链网络来解决区块链的可扩展性问题。 虽然超级链的发布将是一个重要的里程碑，但仍需解决一些关键痛点，例如依赖可信证明者、跨链交易速度慢和异步性、L1 的容量限制、缺乏易于使用的开发和钱包工具等。 解决这些问题将使构建复杂 Web2 应用的去中心化替代方案成为可能，最终实现完全可扩展的区块链愿景。

Superchain 致力于通过**标准化和模块化的技术栈**（OP Stack）来实现跨链数据和资产的无缝流转，同时共享以太坊的安全和资源，从而在 L2/L3 多链世界中形成规模化网络效应。

Superchain 内的每条链都需要将排序器（Sequencer）总收入或利润的 15% 支付给 **Optimism Collective**，以在多链之间聚合流动性并引导形成更大网络效应。

### 2025.01.21

学习主题：OP Stack 基本概述 https://docs.optimism.io/stack/getting-started

OP Stack是驱动Optimism的软件集合——目前以OP主网背后的软件形式存在，最终将以Optimism超级链及其治理的形式存在。随着超级链概念的出现，Optimism轻松支持在拟议的超级链生态系统中互操作的新链的安全创建变得越来越重要。因此，OP Stack主要关注于创建一个共享的、高质量的和完全开源的系统，用于创建新的L2区块链。通过协调共享标准，Optimism Collective可以避免重复地在孤岛中重建相同的软件。

OP Stack大大简化了创建L2区块链的过程，但重要的是要注意，这并没有从根本上定义OP Stack是什么。OP Stack是所有驱动Optimism的软件。随着Optimism的发展，OP Stack也将发展。OP Stack可以被认为是软件组件，这些组件要么帮助定义Optimism生态系统的特定层，要么作为现有层中的模块发挥作用。

OP Stack当前的核心是运行L2区块链的基础设施，但理论上OP Stack扩展到底层区块链之上的层，包括区块浏览器、消息传递机制、治理系统等工具。**层通常在堆栈底部（如数据可用性层）定义得更严格，但在堆栈顶部（如治理层）定义得更宽松。**

OP Stack是一个不断发展的概念。随着Optimism的发展，OP Stack也将发展。今天，OP Stack的Bedrock版本简化了部署新的L2 Rollup的过程。随着对堆栈工作的继续，插入和配置不同的模块应该会更容易。随着超级链开始成形，OP Stack可以与其一起发展，以包含允许不同链无缝互操作的消息传递基础设施。最终，OP Stack将成为Optimism所需的东西。

### 2025.01.22

学习主题：体验和分析一下 Superchain 项目 https://www.superchain.eco/projects

[DeFiLlama](https://www.superchain.eco/ecosystem-projects/defillama) 是一个自筹资金的开源平台，提供超过 240 个区块链上 3000 多个DeFi项目的实时、透明数据。它没有正式的治理结构和原生代币，依靠 grants for funding 。其价值主张是通过社区协作，为用户提供准确和全面的 DeFi 分析数据。

DefiLlama 的主要功能包括：

- **实时数据：** DefiLlama 持续更新其数据，提供关于 DeFi 项目的最新信息。
- **多链支持：** 它支持许多不同的区块链，包括以太坊、币安智能链、Polygon 等。
- **全面数据：** 它提供各种 DeFi 项目指标，例如 TVL、交易量、流动性、代币价格等。
- **开源：** DefiLlama 的代码是开源的，这允许社区贡献和审核其数据。
- **易于使用：** 其网站和 API 设计直观易用，方便用户访问和使用数据。需要注意的是，DefiLlama 的数据依赖于各个 DeFi 项目提供的 API，因此数据的准确性和完整性取决于这些 API 的质量。

### 2025.01.23

学习主题：了解 Superchain Eco 超级链指数 https://www.superchain.eco/superchain-index

旨在为以太坊生态系统提供清晰的链状态可视化。该指数根据链的配置和标准性，将链分为三种状态：

1. 绿色链：完全符合标准要求，使用最新治理批准的 OP Stack 版本，由安全委员会管理桥接升级。
2. 黄色链：标准配置，但仍在完成最终升级或安全委员会迁移。
3. 灰色链：使用旧版本或偏离标准配置，但仍为生态系统做出贡献。

关键重点：

- 仅绿色和黄色链构成"Superchain"
- 灰色链可以通过逐步调整达到标准要求
- Season 7 将仅支持标准化和安全委员会的链
- 目标是促进生态系统互操作性和标准化

目前只看到 OP Mainnet 处于 Stage1 阶段，大多数还是 Stage 0 阶段。





<!-- Content_END -->
