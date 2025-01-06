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

# {partypill}

1. 自我介绍
一个自学了一些python的老白。想努力学习获得更多收益。

2. 你认为你会完成本次残酷学习吗？
我愿意为此努力。

## Notes

<!-- Content_START -->

### 2025.01.06

笔记内容
1、今天第一天打卡，记录那些我不懂的东西并明天得出结论。
“默认假设所有交易都是有效的，只有在有人提出争议时才进行验证”：以太坊的验证机制是什么？怎么通过验证机制保持安全性？这点我不懂需要继续学习。
以太坊虚拟机（EVM）：不懂这个东西是啥，需要进一步回溯学习。
“挑战期”（Challenge Period）：不知道这个概念
复杂智能合约：不懂这个的机制，只知道因为它需要主网交互，导致需要高处理。
L2 和 L1 层：对概念掌握不清晰。
退出时间：这个也不清楚，需要搞明白挑战期。

欺诈证明（Fraud Proof）机制：不懂。
2、今天学到的东西
知道了op设计的初衷是为了降低eth的高gas，因为安全，去中心化和速度是不可能三角。eth保证了安全和去中心化，但速度没法保证。所以一开始设计了子链Plsma，除了少数必要的交易其他都在子链上处理，但这导致了子链的信息无法同步到eth主网，一个是不安全，另一个是挑战期退出慢。
然后op设计了打包交易上传，等于压缩了多次交易只需要一次上链，好处是同步速度快，坏处就是扩容性差。

3、阅读steps去了解必要的信息。

### 2024.07.12

<!-- Content_END -->
