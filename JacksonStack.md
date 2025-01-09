---
timezone: Asia/Shanghai
---


# Kylin

1. 自我介绍  
   rust, web3, layer2   
2. 你认为你会完成本次残酷学习吗？  
   Y

## Notes

<!-- Content_START -->

### 2025.01.06
**Optimism Rollup 概述**  
Optimism 是一种基于 “Optimistic Rollup” 的二层扩展解决方案，其核心理念是利用以太坊等“父”区块链的安全性，通过继承其共识机制（如 PoW 或 PoS）而不提供自身的共识机制。  
这种设计确保了 Optimism 可以在提供高效交易和降低成本的同时，依赖以太坊的安全保障和数据完整性。  

在块存储方面，Optimism 通过压缩格式将 L2 区块数据写入以太坊链上（L1）；使用 EIP-4844 blobs 提交交易，降低了存储成本，同时确保了区块数据的不可篡改性。  
在区块生产中，网络主要依赖一个称为“排序器”（sequencer）的单一角色进行管理。  
排序器负责提供交易确认、状态更新，以及构建和执行 L2 区块，同时将用户交易提交到 L1。为了避免 MEV（最大可提取价值）问题，排序器的内存池为私有，每两秒生成一个区块，无论是否为空块。   

Optimism 支持两种交易路由方式：用户可以直接将交易提交到排序器，从而降低费用，但由于排序器的集中性，这类交易不具备抗审查性；  
另一种方式是通过 L1 提交交易（即存款），这些交易最终被纳入相应的 L2 区块中，并继承了以太坊级别的抗审查能力。  
在区块执行方面，Optimism 的执行引擎可以通过点对点网络同步状态，也可以通过从 L1 数据派生 L2 区块实现抗审查的区块同步。  

Optimism 的跨层桥接功能允许用户在 L2 和 L1 之间转移 ETH 或代币（包括 ERC20 代币）。  
当从 L1 到 L2（即存款）时，交易会在与存款相关的 L1 区块对应的 L2 区块中被记录。  
而从 L2 到 L1（即提款）时，整个过程分为初始化提款、提交提款证明以及故障挑战期后完成提款三个阶段，挑战期通常为 7 天，期间可以通过监控系统识别不正确的提款操作。  

Optimistic Rollup 的状态承诺机制会将状态提交到以太坊（L1），但不会直接提供其有效性的证明。这些状态在 7 天的挑战窗口期内会被视为待处理，若无人挑战，则视为最终承诺；若被挑战，则通过“故障证明”流程验证并替换。  
需要注意的是，挑战不会改变 OP 主网的交易顺序和状态，只会影响已发布的状态承诺。  
目前，Optimism 基金会是 OP 主网上唯一的区块生产者，同时其故障证明机制正随着 EVM 等效性更新进行改进，进一步提升系统的稳定性和安全性。    

### 2025.01.07
Layer 2值得关注的原因如下：  
- Layer 2网络将会更快、更便宜，能够让更多用户得以进入以太坊生态；
- 提前参与Layer 2网络的激励，能够获得奖励；
- 在Layer 2 发展的预期下，用户可将资产迁移至二层网络上，将会有很大概率获得空投；

目前主要有四种技术方案：Optimistic Rollup、ZK Rollup、Plasma、Validium。
![image](https://github.com/user-attachments/assets/18adfd05-cdea-4677-98be-396fc337bf33)  

四大方案各自费用（以上计算前提是以当前Eth价格为2500u，区块gaslimit为30000000，gas费用为30Gwei，平均13秒的出块时间计算， 极限TPS指对应运行环境占领了所有以太坊区块空间(在证明验证上花费 500000 gas)，普通TPS指对应运行环境占领了所有以太坊1/3的区块空间。）  

**ZK Rollup的交易费用**  
在zkSync 中，每笔交易的成本有两个组成部分：  
链下部分（存储 + 证明者成本） ：状态存储和 SNARK（零知识证明）生成的成本。  
链上部分（gas 成本） ：对于每个zkSync 区块，验证者必须支付以太坊 gas 来验证 SNARK，另外每笔交易额外支付约 0.4k gas 来发布状态 。  
（链上部分是一个变量，取决于以太坊网络中当前的 gas 价格。但是，这部分比普通 ETH/ERC20 转账的成本要便宜几个数量级。）  
（1）交易费用地板价  
ZK rollup的交易地板价依赖于eth主网 gas的费用。
链上 gas fee = 每 wei 的价格 * 交易大小 * gas 的费用 * 代币的风险系数    
链下部分 ： SNARK（零知识证明）生成的成本。这部分依赖于硬件资源的使用，因此是不变的。
（2）影响地板价的因素
Rollup的交易地板价依赖于 ETH 主网 calldata 的费用。  

ETH 的 gas 的相关处于草案阶段的 EIP 主要为 EIP4488，该方案将 calldata 非0字节数据由16gas 降低至 3 gas，对 layer2 TPS的影响较大，利好 layer2 的 Rollup，可以大大降低Rollup主网的交易成本，非0字节的数据可以降低为当前的 1/5 的成本不到，0 字节的也可以微微降低（ab，op，zk 等预计都可以下降至目前 1/5 的手续费）。  
（3）费用支付方式   
zkSync 中的转账天然支持“无气体交易”：用户在被转账的代币中支付交易费用。因此，例如，如果您想交易 DAI 稳定币，您无需拥有 ETH 或任何其他代币。只需支付一小部分 DAI 的费用。     
**zkPorter的交易费用**  
目前 github 无 zkPorter 相关代码，由于 zkPorter 不需要链上数据可用性，预计成本将大大降低。    
主要为链下成本，交易可以控制在 1 到 3 美分的恒定费用。  
### 2025.01.08
在zkSync 2.0中，L2 状态将分为 2 个方面：具有链上数据可用性的 ZK Rollup 和具有链下数据可用性的 zkPorter。   
![image](https://github.com/user-attachments/assets/421cfd66-493b-499f-8d33-dc8552ff4e03)
这两部分将是可组合和可互操作的：ZK Rollup 端的合约和账户将能够与 zkPorter 端的账户无缝交互。从用户的角度来看，唯一明显的区别是 zkPorter 账户的费用减少了 100 倍。  
zkPorter 账户的数据可用性将由 zkSync 代币持有者（称为监护人）保护。他们将通过签署区块来跟踪 zkPorter 端的状态，以确认 zkPorter 帐户的数据可用性。  
监护人使用 zkSync 代币参与权益证明 (PoS)，因此任何数据可用性故障都将导致他们被削减。这为数据可用性提供了加密经济保证。 需要注意的是，zkSync 中的 PoS 比侧链等其他系统中的 PoS 安全得多。这是因为 zkSync 监护人本质上是无法窃取资金。他们只能冻结 zkPorter 状态（冻结他们自己的权益）。 每个用户都可以自由选择自己的安全阈值。任何想要所有链上可用数据的用户都可以完全留在Rollup,使用ZK Rollup账号。  
**Arbitrum Gas 机制**  
Arbgas 费用将根据用户与 Arbitrum 的交互方式而有所不同，但下表可用作一般参考：  
![image](https://github.com/user-attachments/assets/a87ad017-135c-458d-b48c-eb26a4fa2621)   

**optimism Gas 机制**  
optimism 交易中的两个成本来源：L2 执行费和 L1 数据/安全费。   
（1）L2 执行费  
就像在以太坊上一样，Optimism 上的交易必须为他们使用的计算量和存储量支付gas 。每笔 L2 交易都会支付一定的 执行费用，等于交易使用的 gas 数量乘以交易附带的 gas 价格。这也是以太坊的收费方式。    
这是（简单的）公式： l2_execution_fee = transaction_gas_price * l2_gas_used  
使用的 L2 气体量取决于您尝试发送的特定交易，交易在 Optimism 上使用的 gas 量通常与在 Ethereum 上的大致相同。  
（2）L1 数据费  
Optimism 与以太坊不同，因为 Optimism 上的所有交易也都发布到以太坊。此步骤对于 Optimism 的安全属性至关重要，因为这意味着同步 Optimism 节点所需的所有数据始终在以太坊上公开可用。这就是使 Optimism 成为 L2 的原因。  
 
Optimism 上的用户必须支付向以太坊提交交易的费用。称之为L1 数据费用 ，这是 Optimism（和其他 L2）与以太坊之间的主要差异。由于以太坊上的 gas 成本非常昂贵，因此 L1 数据费用通常会在 Optimism 上占据交易的总成本。该费用基于四个因素：  
以太坊当前的gas价格。  
将交易发布到以太坊的 gas 成本。这交易长度的大小（以字节为单位）成比例。    
以gas计价的固定费用。  
一种动态的间接费用，按固定数字支付的 L1 费用。  
公式： L1_data_fee = L1_gas_price * (tx_data_gas + fixed_overhead) * dynamic_overhead  

### 2025.01.09
trainning wheels: a phase of central control during the development of rollup systems, which should be eventually removed to fully inherit the security properties of the base layer.    
**Vitalik's proposed milestones**   
link:https://ethereum-magicians.org/t/proposed-milestones-for-rollups-taking-off-training-wheels/11571  
#### Stage 0: full training wheels
Requirements:
- The project should call itself a rollup.
- All rollup transactions should go on-chain.
- There should exist a “rollup full node”: an independently runnable software package that can read the L1 chain, extract and the rollup chain, and compute the current state of the rollup chain. If it disagrees with a rollup state root posted into the contract, it should give an alarm.
- There should be machinery that allows users to either post rollup transactions or at least ensure a withdrawal of their assets with no cooperation from the operator. That is, the operator cannot freeze or steal users’ assets by censoring users; their only possible tool for doing so must be to post a false state root.
- It’s okay if the on-chain mechanism for posting new state roots is simply a multisig, with no active fraud proof or validity proof whatsoever.
#### Stage 1: limited training wheels
Requirements:
- There must be a running fraud proof or validity proof scheme, which has the practical authority to accept or reject which state roots get accepted by the rollup contract.
- There can exist a multisig-based override mechanism (“security council”) that can override the fraud proof or validity proof system’s outputs and post state roots, to be used in case the proof system code is bugged. However:
      - The multisig must be 6 of 8 or stricter (that is, >= 8 participants AND >= 75% threshold)
      - At least a quorum-blocking group (that is, enough participants to prevent the multisig from acting) must be outside the organization that is running the rollup.
- There can exist an upgrade mechanism, but if it has a lower threshold than the multisig, upgrades must have a mandatory activation delay of at least 7 days or the maximum length of the fraud proof game, whichever is longer. The goal of this rule is to ensure that the upgrade mechanism cannot be used to intervene in real-time disputes.
#### Stage 2: no training wheels
Requirements:  
- In the event that code does not have bugs, there must not be any group of actors that can, even unanimously, post a state root other than the output of the code  
This somewhat awkward phrasing (“IF the code does not have bugs, THEN no one can override it”) is meant to permit use of security councils in ways that are clearly limited to adjudicating undeniable bugs, such as the following:
- The rollup uses two or more independent implementations of its state transition function (eg. two distinct fraud provers, two distinct validity provers, or one of each), and the security council can adjudicate only if they disagree - which would only happen if there is a bug
- If someone submits a transaction or series of transactions that contains two valid proofs for two distinct state roots after processing the same data (ie. “the prover disagrees with itself”), control temporarily turns over to the security council
- If no valid proof is submitted for >= 7 days (ie. “the prover is stuck”), control temporarily turns over to the security council
- Upgrades are allowed, but must have a delay of >= 30 days


**L2Beat's work**
directions explored: a simple three-stages rating, a letter rating with plus and minus signs to express finer details, a star system, and a numeric score system.  


<!-- Content_END -->
