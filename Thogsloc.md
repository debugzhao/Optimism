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

# Thogsloc

1. 自我介绍
在web3呆过一阵子的社区新人，来和大家一起参与学习
2. 你认为你会完成本次残酷学习吗？
Waaaagh！
## Notes

<!-- Content_START -->

### 2025.01.06

Optimistic Rollup 依赖于“父链”的安全性，核心思想是利用父链的共识机制。

Bedrock 版本中，L2 区块被存储在以太坊区块链上，使用非合约地址来减少 L1 的交易费用。区块以压缩格式写入 L1。

Sequencer 负责：
提供交易确认和状态更新、
构建和执行 L2 区块、
将用户交易提交到 L1。

op-geth 组件通过两种机制接收区块：
通过点对点网络与其他执行引擎同步。
从L1派生L2区块。

OP Rollup 通过以上方法使得交易得到快速处理和保持低成本。

### 2025.01.07

OP Stack 是支持 OP Rollup 的基础架构和协议栈，为 OP Rollup 提供了必要的组件和功能，包含：

桥接（Bridges）
允许不同区块链之间的交互。
信使（Messengers）：用于在链之间传递消息。
存款（Deposits）：用户将资产转移到Optimism链的过程。
取款（Withdrawals）：用户从Optimism链提取资产的过程。
担保的 gas 费市场（Guaranteed Gas Market）：确保交易费用的透明和可预测性。
提案（Proposals）：用户可以提交改进建议。

执行引擎（Execution Engine）
负责处理和执行交易的核心组件。

汇总节点（Rollup Node）
用于聚合和验证交易的节点。
P2P 通信：节点之间的点对点通信。
派生（Derivation）：如何从 L1 链派生出 L2 链的状态。

故障证明（Fault Proof）
确保交易安全性和有效性。
Cannon Fault Proof VM：用于验证交易的虚拟机。

预编译（Precompiles）、预部署（Predeploys）、预安装（Preinstalls）
涉及到在 Optimism 链上预先配置的合约和功能。

超级链配置（Superchain Configuration）
允许用户根据需求调整协议参数。

治理代币（Governance Token）
描述 Optimism 的治理机制，用户如何参与决策。

### 2024.07.12

<!-- Content_END -->
