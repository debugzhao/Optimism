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

# Neal Lee

1. 自我介绍
用挣钱激励自己学习，用学习激励自己赚钱。
2. 你认为你会完成本次残酷学习吗？
可以的。
## Notes

<!-- Content_START -->

### 2025.01.06
核心概念 - Optimistic Rollup 是 Optimism 的关键，借父链（以太坊）安全与共识机制运作。
块存储 - Bedrock里，L2块以特定方式存于以太坊，提交后不可改，用压缩格式写入L1降成本。
块生产 - “排序器”管理块生产，防MEV。块每2秒生成，交易通过直接或L1提交至排序器，L1提交具备抗审查能力，当前由Optimism Foundation运行块生产。
块执行 - 执行引擎（op-geth）通过对等网络同步、rollup节点（op-node）从L1派生两种方式接收块。
跨层转移 - 支持 L1 和 L2 间资产转移，OP Mainnet 用标准桥实现。从以太坊到 OP Mainnet为 “存款”，反向 “取款” 分三步（初始化、提交证明、最终完成）。
故障证明 - 状态承诺在L1有7天挑战期，无挑战即确认，受挑战可经故障证明处理，不回滚OP Mainnet。该流程现因EVM更新而重构。

### 2024.07.12

<!-- Content_END -->
