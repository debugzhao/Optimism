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

# Louis

1. 自我介绍
My name is louis and I am a blockchain development engineer

2. 你认为你会完成本次残酷学习吗？
I believe that I can complete the study task

## Notes

<!-- Content_START -->

### 2025.01.06

Optimism 是一种“乐观型 Rollup”，即以太坊的 Layer 2 扩展解决方案，通过利用以太坊的安全性来提高交易吞吐量并降低费用。 与传统区块链不同，乐观型 Rollup 默认假设交易是有效的，只有在出现挑战时才执行计算，从而显著提高效率。

**乐观型 Rollup 的关键组成部分：**

- **区块存储：**在 Bedrock 版本中，Optimism 使用非合约地址（0xff00...0010）在以太坊上存储 Layer 2（L2）区块，以最小化 gas 费用。 这些区块作为交易提交，使用 EIP-4844 blobs，一旦包含在具有足够验证的区块中，即可确保数据的可用性和完整性。 这种设计使 Optimism 继承了以太坊的安全保证。

- **区块生产：**一个称为“排序者”的实体负责区块生产。 排序者提供交易确认，构建和执行 L2 区块，并将用户交易提交到 Layer 1（L1）。 在 Bedrock 中，排序者拥有一个私有内存池，以防止矿工可提取价值（MEV）机会。 无论交易量如何，每两秒生成一个区块。

- **区块执行：**交易在 L2 链上执行，结果定期发布到以太坊。 这种方法减少了以太坊的计算负担，同时保持安全性。

- **资产桥接：**用户可以使用桥接将 ETH 和代币在以太坊和 Optimism 之间转移。 从以太坊移动资产到 Optimism 涉及在以太坊的合约中锁定代币，并在 Optimism 上铸造相应的代币。 相反的过程涉及在 Optimism 上销毁代币，并在以太坊上解锁它们。

- **故障证明：**Optimism 采用一种挑战机制，默认假设交易是有效的，除非被证明无效。 如果有人发现无效交易，可以提交故障证明进行挑战。 该系统在无需对每笔交易进行链上计算的情况下确保正确性。

通过利用这些机制，Optimism 在保持以太坊的安全性和去中心化的同时，实现了更高的可扩展性和更低的费用。 

### 2024.01.07

<!-- Content_END -->
