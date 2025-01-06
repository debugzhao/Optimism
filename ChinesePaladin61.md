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

### 2024.07.12

<!-- Content_END -->
