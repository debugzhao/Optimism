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

# {183Aaros}

1.  About me: Hey, I'm 183Aaros, a member of OPCN and one of the tutors of the OP co-learning this time. I'm delighted to learn the fundamentals of OP together with everyone here. Here's my personal web if you're interested in know more about me :) -> 183aaros.notion.site
2. About Notes: trying to use md grammar after 2-3 days 
3. Yes

## Notes

<!-- Content_START -->

### 2025.01.06

Optimism Co-learning Notes, day1: 

#### OP and OP Rollup

Dedication:
scaling Ethereum's tech
expanding its ability
coordinape ppl world-wide to build decentralised economies+governance systems

Principle:
impact=profit

OP Collective:
Builds open-source software

OP Stack:
decentralised software stack
backbone of blockchains i.e. OP Mainnet& base

OP Rollups:
Leverage the consensus mechanism of L1

#### Block

Block storage:
using non-contract address(for min gas) on ETH
write in compressed format
transaction anti-censorship via EIP-4844 blobs
inherits ETH availability& integrity

Biobiography:
https://specs.optimism.io/

### 2024.01.07

Key takeaway:

#### OP Mainnet Transaction fee
Transaction fee [Execution Gas Fee(Base fee, Priority fee), L1 Data Fee]

##### L1 Data Fee，Ecotone:
(1)tx_compressed_size = [(count_zero_bytes(tx_data)*4 + count_non_zero_bytes(tx_data)*16)] / 16

(2)
weighted_gas_price = 16*base_fee_scalar*base_fee + blob_base_fee_scalar*blob_base_fee

L1 Data Fee, Ecotone = (1) * (2)

##### L1 Data Fee，Fjord
L1 Data Fee，Fjord(FastLZ-compressed size, base fee/ blob base fee):

(1) estimatedSizeScaled = max(minTransactionSize * 1e6, intercept + fastlzCoef*fastlzSize)

(2)l1FeeScaled = baseFeeScalar*l1BaseFee*16 + blobFeeScalar*l1BlobBaseFee

where both scalars are scaled by 1e6,

thus,

L1cost = (1)*(2)/1e12

##### Biobiography:
https://docs.optimism.io/stack/transactions/fees

<!-- Content_END -->
