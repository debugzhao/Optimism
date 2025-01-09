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

# {ChinesePaladin61}

1. 自我介绍

2. 你认为你会完成本次残酷学习吗？
是的

## Notes

<!-- Content_START -->

### 2025.01.06
### Layer2 扩容方案

  Rollup是一种区块链扩展技术，利用L1的安全性，去中心化和共识机制运行，并且解决L1的部分问题，如：费用高，速度慢等缺点，是一种L2层的解决方案，将交易从L1分出链外解决，然后将结果回滚到主链。
  Optimism 的底层技术是 Optimistic Rollups，一个Layer2扩容方案，通过批量处理大量交易，减少主链的计算和费用。特点是：
  乐观机制，假设所有交易都是合法的，一开始并不会验证每一个交易的合法性，通常不会进行交易验证。
  欺诈证明：每一个交易都有7天的挑战期，如果在规定时间内没有人质疑某个交易的合法性，那么交易的结果会被视为最终结果（哪怕是恶意的交易结果，比如偷走别人的资金）如果有人在7天内质疑交易的合法性时会触发欺诈证明，并且进行交易验证，如果发现交易不合法，系统会回滚交易结果，并处罚恶意提供者。

  Optimism 允许用户在L1与L2之间相互转移代币或ETH，称为跨链桥。
  将代币从L1转到L2称为存款，用户在（L1） 发起一笔交易，调用 L1StandardBridge 合约，将代币发送到L2，Optimism 在 L2 的第一个规范区块 中记录该存款交易。
  从L2到L1转账叫取款，会经历三个阶段：
  一：用户在（L2）发起一笔交易，调用 L2StandardBridge 合约，开始提款。
  二：等待输出根提交到L1，Optimism会将 L2 的交易状态提交到 L1，生成一个 输出根。
  用户需要提交一份 提现证明，证明提款交易已在 L2 上执行。
  三：挑战期结束后完成提款，提款交易需要经过一个 挑战期，以确保交易的合法性。挑战期为7天，如果挑战期内没有质疑，提款将在 L1 完成，可以在L1上提取资产。

### 2025.01.07

  先介绍optimism Gas 机制
  optimism 交易中的两个成本来源：L2 执行费和 L1 数据/安全费。
  
### L2执行费
  optimism在L2中的交易收费和在以太坊上交易一样收取gas费，用作计算和储存的需求，每一笔交易都会支付一定的gas费，计算公式：
  L2_execution_fee = transaction_gas_price * L2_gas_used
  transaction_gas_price：L2网络上的gas价格，通常以 Gwei 为单位。
  l2_gas_used：交易在L2上的消耗数量，每个操作，比如转账，存储，调用合约等，都会消耗不同的gas，操作越多gas费越高。

### L1 数据费
### L1 数据费
  Optimism 与以太坊不同，因为 Optimism 上的所有交易也都发布到以太坊。此步骤对于 Optimism 的安全属性至关重要，因为这意味着同步 Optimism 节点所需的所有数据始终在以太坊上公开可用。这就是使 Optimism 成为 L2 的原因。
  Optimism 上的用户必须支付向以太坊提交交易的费用。称之为L1 数据费用 ，这是 Optimism（和其他 L2）与以太坊之间的主要差异。由于以太坊上的 gas 成本非常昂贵，因此 L1 数据费用通常会在 Optimism 上占据交易的总成本。该费用基于四个因素：
  
  以太坊当前的gas价格。
  将交易发布到以太坊的 gas 成本。这交易长度的大小（以字节为单位）成比例。
  以gas计价的固定费用。当前设置为 2100。
  一种动态的间接费用，按固定数字支付的 L1 费用。当前设置为 1.24。

  L1数据费计算公式：
  L1_data_fee = L1_gas_price * (tx_data_gas + fixed_overhead) * dynamic_overhead
  L1_gas_price：以太坊主网的 Gas 价格，通常以 Gwei 为单位。
  tx_data_gas：交易数据所需的 Gas，表示将 L2 上的交易数据提交到 L1 时消耗的 Gas。
  fixed_overhead：固定的开销，包括 L2 网络在提交数据时的固定成本，如签名验证、批次处理等。
  dynamic_overhead：动态开销，表示网络的负载和 L1 上的拥堵情况对 Gas 消耗的影响。

  固定费用（例如：提交批次时的签名验证、Merkle 树计算等），这些成本不会随交易数量变化。
  动态费用则是因为L1的网络情况，有时拥堵，那么提交批次的费用就可能变高。

  因此，L2执行费+L1数据费才是一个交易的总共费用。
  total_fee = l2_execution_fee + l1_data_fee

  提交数据费的好处是，将一些重要信息同步到L1中，比如状态根，提交到L1后，所有人都可以查看交易，帮助用户发现不诚实者，并发起挑战。

### 2025.01.08

### 补充Optimism Bedrock 架构：块存储、区块生产
  1. 块存储
    在 Bedrock 架构中，Optimism 的 L2 区块 通过 非合约地址（0xff00...0010） 写入以太坊主网，以减少 L1 上的 gas 费用。

    EIP-4844是以太坊的一个改进提案，引入了blob这一数据结构，它的特点是：
      blob是指包含大量数据的二进制数据块，这些blob将数据储存到链外，而不是存在以太坊主网上，通过这种方式，可以显著降低数据的储存和大量处理的成本。
      扩展性提升，通过使用blob数据块，EIP-4844 允许 rollups 在处理交易时仅存储必要的计算数据，而无需每次都将所有数据发布到以太坊主链，从而有效减轻了主链的负担，提升了网络的整体吞吐量。

 2. 区块生产
  Optimism 的区块生产由 Sequencer（排序器） 负责。
  Sequencer的作用是：
  
  事务排序：Sequencer 会接收来自用户的交易，并按顺序对它们进行排序，确保 Rollup 内部状态的一致性。通过正确排序事务，Sequencer 可以防止双重支付等冲突问题。
  批处理：排序后的交易会被批量处理。Sequencer 会将多笔交易合并为一个批次，然后将这个批次提交到以太坊主链（Layer 1）。这种批处理方式有助于降低提交多笔交易的成本。
  数据可用性：在 Rollups 中，数据的可用性非常关键，Sequencer 负责确保所有验证 Rollup 状态所需的数据是可用的。这意味着它需要确保交易数据对以太坊主链或其他验证者是可访问的，以便验证这些交易是否正确。
  提高效率：Sequencer 的设计目的是尽量减少交易处理的延迟，这对于提高 Rollup 解决方案的可扩展性和效率至关重要。它确保交易能够接近实时地进行处理，从而降低了主链的拥堵和高费用问题。

  在乐观 Rollups 中，Sequencer 提交批量的交易数据到以太坊主链，并由验证者检查这些交易批次的有效性。如果没有人提出异议，那么这些交易就会被最终确认。

### 2025.01.09

### 学习Stages 框架
  Stages 框架是以太坊社区提出的一个标准化工具，用于评估和衡量 Rollup（二层扩容方案） 的去中心化程度和成熟度。它将 Rollup 的发展分为四个阶段（Stages），帮助开发者和用户了解 Rollup 项目当前的技术状态、风险因素，以及它们距离实现完全去中心化的目标还有多远。这个框架的核心目标是引导 Rollup 项目逐步去除中心化依赖，从中心化控制过渡到完全去中心化的状态，实现更高的安全性、抗审查性和数据可用性保障。

 Stages 框架的核心目标：
  衡量 Rollup 的成熟度：Stages 框架提供一个标准化的评估体系，让用户了解某个 Rollup 项目的去中心化程度和安全性。
  推动 Rollup 去中心化：鼓励 Rollup 项目团队逐步减少对中心化组件的依赖，降低单点故障风险和审查风险。
  提升用户信任和透明度：帮助用户理解 Rollup 的安全保障水平，让用户知道是否可以完全信任该系统，而不需要依赖于中心化的角色。

Stages 框架通过评估 Rollup 的四个核心模块来确定其阶段：
  Sequencer	是否去中心化？是否支持多 Sequencer？
  数据可用性	数据是否去信任化？是否采用链上数据可用性方案？
  桥接机制	L1 和 L2 之间的桥接是否去中心化？是否存在信任风险？
  验证机制	是否实现了抗欺诈证明（Fraud Proof）或有效性证明？

  stages框架提高了项目的透明度，帮助用户了解当前rollup项目的风险和目前状态，通过将 Rollup 的发展过程分为阶段，Stages 框架鼓励项目团队逐步减少中心化控制，向完全去中心化的目标迈进。

<!-- Content_END -->
