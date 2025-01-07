---
timezone: Asia/Shanghai
---

> 请在上边的 timezone 添加你的当地时区，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区
> 时区请参考以下列表，请移除 # 以后的内容


timezone: Asia/Shanghai


---

# {Harris Lee}

1. 自我介绍

大家好，我是Harris Lee，一位对OP Layer 2的发展感兴趣的教师，希望可以学习并传播ETH&OP 生态
2. 你认为你会完成本次残酷学习吗？

我为什么要认为不会呢？肯定是会的，希望最后能学下来并传播推广

## Notes

<!-- Content_START -->

### 2025.01.01

笔记内容

测试一下PR
### 2025.01.02

### 2025.01.06

笔记内容：
今天学习的内容是Optimism的overview
Firstly, Optimism is a Layer 2 scaling solution for Ethereum. The idea of Optimism rollups is to create a new type of blockchain that allows for faster transactions and lower fees than traditional Ethereum, which is using EIP-4844 blobs.

Secondly, Optimism block production is managed by the sequencer. The sequencer will provide the following services:
1. Providing transaction confirmations and state updates
2. Constructing and executing L2 blocks
3. Submitting user transcations to L1

The sequencer does have a mempool, similar to Ethereum.

Transactions get to the sequencer in two ways: 
1. Transactions submitted directly to the sequencer. But these transactions cannot be made censorship-resistant since only the sequencer knows them
2. Transcations deposit to L1, which are included in the chain in the apporpriate L2 block. It provides OP mainnet with L1 Ethereum-level censorship resistance. For the moment, The Optimism Foundation runs the only block producer on OP mainnet.

Block execution receives blocks using two mechanisms:

1.The execution engine can update itself using peer to peer network with other execution engines.
2.rollup node derives the L2 blocks from L1.

OP also could be thinking as bridging ETH or tokens between layers

OP is designed for users sending arbitrary messages between smart contracts on L2 and the underlying L1

Moving from Ethereum to OP mainnet called "deposit", meanwhile, moving from OP mainnet to Ethereum called "withdrawal"

Fault proofs:

When a state commitment is challenged, the commitment can  be invalidated through a "fault-proof" process. This process wil replace the invalidated state commitment with a new one. A successful challenge does not roll back OP Mainnet itself, only the published commitments about the state of the chain. The order of transactions and the state of Op mainnet is unchanged by a fault-proof challenge.

### 2025.01.07

According to yesterday's learning notes, I will start to learn about Optimism's rollup architecture. Today will start to learn about EVM Equivalence,the sequencers and messager and the rollup node  with https://specs.optimism.io/protocol/messengers.html\

EVM Equivalence:

The EVM Equivalence is the core concept of Optimism. It is a set of rules that allow the execution of Ethereum smart contracts on Optimism. The EVM Equivalence is a set of rules that allow the execution of Ethereum smart contracts on Optimism. The EVM Equivalence is a set of rules that allow the execution of Ethereum smart contracts on Optimism.

With a readable word to describe the functionality of Ethereum for Optimism,  If you think of Ethereum as an almighty, decentralized court, then the core insight of L2 scalability is: “don’t go to court to cash a check — just go if the check bounces.”--To translate this saying in Chinese it could said:不要为了兑现支票而去法院——只有在支票跳票时才去。
具体解释上面这句话可以理解为：

以太坊作为“全能的、去中心化的法院”：这里指的是以太坊作为一个基础区块链平台，它提供了安全、不可篡改的交易记录，并能够执行智能合约。就像法院一样，以太坊确保所有规则都被正确遵循，所有的争议都能得到公正的解决。然而，就像现实中的法院，以太坊处理每一笔交易或争议的成本（Gas费用）较高，而且处理速度相对较慢，因为每个区块都需要网络中的大多数节点进行验证和共识。

“不要为了兑现支票而去法院”：这表示不是每一个操作或交易都需要直接在以太坊主链上进行。许多日常的小额交易或快速交互可以通过更高效的方式完成，而不必占用以太坊主链的资源。这就是二层扩展方案的作用，它们允许用户在不依赖于以太坊主链的情况下进行大量的交易和互动，从而提高了效率并降低了成本。

“只有在支票跳票时才去”：如果在L2系统中出现了问题，比如资金没有按照预期转移，或者发生了欺诈行为，这时用户可以回到以太坊主链（“法院”）来解决争议。以太坊主链的安全性和最终性保证了即使L2出现问题，用户的资产仍然是安全的，并且可以恢复到正确状态。

According to the elaboration of the saying, we could easily understand EVM Equivalence as a set of rules that allow the execution of Ethereum smart contracts on Optimism with technique rollup architecture which could provide two outstanding features:
1. uncensorable transactions
2. anybody can transact

The Value of uncensorable transactions for rollup could be explained as follows:

The concept of "uncensorable" in the context of Ethereum Virtual Machine (EVM) Equivalence refers to the characteristic of the Ethereum network that, once a transaction is broadcasted to the network and successfully included in a block, the outcome of the transaction and the state updates are not subject to censorship or reversal. This implies:

Unstoppable Transactions: Any user can initiate transactions as long as they adhere to the protocol rules of Ethereum (e.g., paying sufficient Gas fees), and these transactions cannot be prevented from entering the blockchain due to external intervention.

Immutable History: Once a transaction is included in a block that the consensus mechanism has confirmed, it becomes part of the immutable history of the blockchain. This history is considered permanent and unchangeable unless more than 50% of the network's hash power is controlled to perform what is known as a 51% attack, which is extremely difficult and costly.

Decentralized Nature: Ethereum is a decentralized platform, so no single entity can decide which transactions should be accepted or rejected. All nodes collectively maintain the security and integrity of the network, ensuring that each user's rights are not infringed upon.
Execution of Smart Contracts: Once smart contracts are deployed and executed automatically under specific conditions, their outcomes also cannot be blocked or reversed, unless the contract itself is coded with specific clauses allowing for such actions. This ensures that agreements between parties can reliably execute according to predefined rules.

In summary, "uncensorable" underscores one of the core values provided by Ethereum as a blockchain technology — offering an open, transparent, and trustless environment where information and value exchanges can occur freely without interference. This attribute is crucial for protecting user privacy, safeguarding freedom of speech, and building censorship-resistant applications.

To satisfy the requirements of Ethereum L1 & L2s infrastructure, Optimistic comes with OVM and is targeted to be an EVM equivalence. If L2s want to surf Ethereum’s wave of infrastructural network effects, they must become EVM equivalent.

Optimistic practice EVM equivalence by achieving L2 blocks executed with precise EVM equivalence. Instead of implementing the EVM in Solidity, implement a VM with a much smaller, simpler instruction set, and run the EVM within this VM during fraud proofs. To do this, we must simply compile an existing EVM interpreter, such as Seth’s, to run within the simpler VM.

next day plan: focusing on sequencers, users, messages role in Optimistic protocol stack and step into the next step of Optimistic protocol.




<!-- Content_END -->
