---
timezone: Asia/Shanghai
---


# Ye

1. 自我介绍
     - 清华-南加大 Communication Data Science 25'硕士在读，链上数据分析2年经验，Dune [@wyeeeh](https://dune.com/wyeeeh)，X [@wyeeeeh](https://x.com/wyeeeh)，Optimism NumbaNERDs 分析师，入选Optimism RetroPGF Round 3 & Round 6 头部贡献者。

2. 你认为你会完成本次残酷学习吗？
   - 有激励就有野心，之前完成过Sixdegree Lab和BuidlerDAO发起的Dune Analytics共学计划，以及DeFiHackLabs发起的Solidity残酷共学计划。

## Notes

<!-- Content_START -->

### 2025.01.06
#### Layer2 扩容方案
在 Bedrock 中，Layer2区块通过非合约地址以压缩格式写入L1区块链 (Ethereum)上，以减少Layer1的 gas 费用。这
种方式确保了 OP Mainnet 继承了 Ethereum 的可用性和完整性保证。
##### Optimistic Rollups
- Optimistic Rollups 使用它们的父链（如 Ethereum）的共识机制（如PoS），而不是自己提供共识机制。
- 在 Optimistic Rollup 中，状态承诺被发布到 L1（在 OP Mainnet 的情况下是 Ethereum）而不提供直接的有效性证明。这些承诺在“挑战窗口”期间被视为待定状态。如果在挑战窗口期间无人挑战状态承诺，则视为最终确定。当状态承诺被挑战时，可以通过“故障证明”过程使其无效。成功的挑战不会回滚 OP Mainnet 本身，只会移除有关链状态的发布承诺。

##### 区块
Optimism 的区块生产主要由单一的“排序器 (sequencer)”管理，负责提供交易确认、状态更新、构建和执行 L2 区块以及将用户交易提交到 L1。为了避免 MEV，Bedrock 中的排序器拥有一个私有的 mempool。OP Mainnet 每两秒产生一个区块，无论区块是否包含交易。

执行引擎（op-geth 组件）通过两种机制接收区块：
- **通过Layer 2 内部的P2P网络同步状态。** 执行引擎（op-geth 组件）通过点对点（P2P）网络与其他在同一 Layer 2 网络上的执行引擎进行通信和数据同步。
- **通过rollup 节点（op-node 组件）实现，从 L1 派生 L2 区块。** 这种方法相比于直接的 P2P 网络同步会慢一些，因为它需要等待 L1 区块的确认，并且处理从 L1 到 L2 的映射逻辑。然而，这种方法能抗审查。由于 L2 区块的生成是基于已经公开且被广泛认可的 L1 数据，这就使得任何试图对 L2 数据进行审查或篡改的行为都会被发现并受到阻止。可以把这种机制比喻为通过官方渠道获取信息，虽然可能不是最快的，但却是最可靠和最不容易被篡改的。




### 2025.01.07
##### Bridge
Optimism 允许用户在 L2（如 OP Mainnet）和底层 L1（如 Ethereum mainnet）之间的智能合约发送任意消息，从而实现 ETH 或代币（包括 ERC20 代币）的转移。标准桥（Standard bridge）使用这一功能，允许用户从 Ethereum 存入代币到 OP Mainnet，并允许从 OP Mainnet 提取代币回 Ethereum。

- **从 Ethereum 到 OP Mainnet**: 称为存款(deposit)，通过使用 L1CrossDomainMessenger 或 L1StandardBridge 完成，成为对应 L1 区块的第一个 L2 区块的一部分。

- **从 OP Mainnet 到 Ethereum**: 称为提款(withdrawl)，分为三个阶段：初始化提款 L2 交易、等待下一个输出根提交到 L1 并提交提款证明、以及在故障挑战期结束后完成提款。


### 2025.01.08
#### Layer2的解决方案交易成本对比

- **为什么要L2？更快、更便宜**
   普通转账eth需要字节数112左右，ZK压缩为12个字节，op系压缩为78.4（不固定，假设压缩了30%的空间），假设swap转账需要字节数约180左右，ZK压缩为14个字节，op系压缩为126个字节。
- 目前主要有四种技术方案：**Optimistic Rollup、ZK Rollup、Plasma、Validium。**

##### Optimistic Rollup
**交易成本**
- L2 执行费：每笔 L2 交易都会支付一定的执行费用，等于交易使用的 gas 数量乘以交易附带的 gas 价格。
   - `l2_execution_fee = transaction_gas_price * l2_gas_used`
- L1 数据/安全费：Optimism 上的用户必须支付向以太坊提交交易的费用，称之为L1 数据费用
   - `L1_data_fee = L1_gas_price * (tx_data_gas + fixed_overhead) * dynamic_overhead`

##### ZK Rollup
**交易成本**
在zkSync 中，每笔交易的成本有两个组成部分：
- 链下部分（存储 + 证明者成本）：状态存储和 SNARK（零知识证明）生成的成本。这部分依赖于硬件资源的使用，因此是不变的。
- 链上部分（gas 成本）：对于每个zkSync 区块，验证者必须支付以太坊 gas 来验证 SNARK，另外每笔交易额外支付约 0.4k gas 来发布状态。

**影响地板价的因素**
Rollup的交易地板价依赖于 ETH 主网 calldata 的费用。

**无气体转账**
用户可以直接用被转账的代币中支付交易费用（如DAI）而无需使用原生Token支付

### 2025.01.09
#### Layer2扩容方案对比
##### Plasma

##### Rollup
**ZK Rollup**
zk-Rollups 是一种基于零知识证明的二层扩容方案。首先由 Rollup Operator 组件将多个链下交易聚合成一个批次，之后使用零知识证明（例如 zk-SNARKs 或 zk-STARKs）生成一个简洁的证明文件，这个证明可以验证整个批次的交易的有效性，而不需要逐一检查每笔交易；然后将证明及与该批次相关的数据提交到主链，主链通过验证证明的正确性，确保交易是有效的；主链验证通过后，链上合约会根据证明中的数据更新链上的状态。这意味着，尽管交易是在链下进行的，但链上状态仍然得到了更新，确保了数据的一致性。

**OP Rollup**
Optimistic Rollups 是一种基于乐观性验证的二层扩容方案，即默认提交的区块是正确的，除非有人提出质疑。它同样需要 Rollup Operator 将许多链下交易聚合成一个批次，之后计算批次交易产生的新状态（如余额、合约状态等）并生成一份链下状态更新；然后将链下状态更新、相关数据提交到主链，这个状态默认是正确的，不需要额外验证；但是在状态更新提交后，会有一个固定的挑战期，在此期间，任何人都可以通过提供欺诈证明来质疑提交的状态更新的有效性，与被质疑状态的相关的整个交易将通过 EVM 运行检验，如果证明状态更新是错误的，提交者会被惩罚（扣除押金），同时链上状态会回滚到正确的状态；如果在挑战期内没有人质疑状态更新，或者质疑被证明是错误的，那么链上状态会根据提交的状态更新进行更新。


##### 参考文章
- [L2 扩容技术详解：Optimistic Rollups 与 zk-Rollups](https://web3caff.com/zh/archives/55667)
- [Optimistic Rollup vs. ZK Rollup 对比](https://learnblockchain.cn/article/738)
- [一文详解以太坊扩容方案：OP vs ZK Rollup](https://foresightnews.pro/article/detail/7248)

<!-- Content_END -->
