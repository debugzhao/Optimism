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

# {verygud-0}

1. 一个喜欢学习的人，2017年入圈的老韭菜，希望更多的了解Optimism
2. 我一定会坚持到底

## Notes

<!-- Content_START -->

### 2025.01.06

今天学习、了解了Optimistic Rollup，总的来说他替eth解决了高手续费和低tps的问题，事实证明也确实有很好的效果，虽然中心化方面牺牲了很多，但系统需要人来打造，去中心化也需要中心化来过渡，这可能是目前不可能三角相对平衡的方法，而且op已经成为L2第一大生态，甚至刚刚才知道base也是基于op stack构建，可以说已经垄断了整个L2的链上活动。

再说到具体技术，日常只是通过使用、交互各种DAPP，进行简单的链上行为，却不知道op背后的每一笔交易都有着块存储、区块生产、块执行等技术的支持。
我觉得op的运作理念很好—— “影响=利润，对集体产生积极影响的个人应获得相应的利润回报”，op也确实是这样做的，这种长期、可持续的激励措施，使得生态百花齐放，也让用户更好的接触到真正有价值的应用

### 2025.01.07
今天学到了一个关于op的新机制——故障证明，这个机制的作用在于维护系统的公平公正，可以适当的解决去中心化（信任）的问题，他的运作原理简单但很有趣
其中有几个关键特点：
1.无需许可的提议
   也就是说任何人都可以通过合约向eth提交“状态提议”
    状态提议主要是用于用户在op链上的操作
2.无需许可的挑战
    这个是我觉得最有意思的地方，因为任何人都可以发起挑战，质疑状态提议，再通过“故障证明游戏”进行纠错
3.模块化设计和多层安全性
    模块化设计使得op可以实现多个证明系统，以确保单独证明系统的中心化，进而规避潜在的风险和错误
     在安全层面，建立了链下监控系统来监控所有提议的根，并确保他们与正确的状态一致，“间隙窗口”又给了守护者足够的时间进行监控，以拒绝无效根。
      还有delayweth作为独立的合约持有资金，以保证在哪怕错误的情况下，重新定向到正确的收款人
### 2024.07.12

<!-- Content_END -->
