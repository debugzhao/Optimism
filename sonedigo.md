---
timezone: Pacific/Auckland
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
### 2024.01.02

### 2024.01.06

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

### 2024.01.07

According to yesterday learning notes, I will start to learn about the Optimism's rollup architecture. Today will start to learn about EVM Equivalence,the sequencers and messager and the rollup node  with https://specs.optimism.io/protocol/messengers.html\

EVM Equivalence:

The EVM Equivalence is the core concept of Optimism. It is a set of rules that allow the execution of Ethereum smart contracts on Optimism. The EVM Equivalence is a set of rules that allow the execution of Ethereum smart contracts on Optimism. The EVM Equivalence is a set of rules that allow the execution of Ethereum smart contracts on Optimism.

With a readable word to describe the functionality of Ethereum for Optimism,  If you think of Ethereum as an almighty, decentralized court, then the core insight of L2 scalability is: “don’t go to court to cash a check — just go if the check bounces.”--To translate this saying in Chinese it could said:不要为了兑现支票而去法院——只有在支票跳票时才去。
具体解释上面这句话可以理解为：

以太坊作为“全能的、去中心化的法院”：这里指的是以太坊作为一个基础区块链平台，它提供了安全、不可篡改的交易记录，并能够执行智能合约。就像法院一样，以太坊确保所有规则都被正确遵循，所有的争议都能得到公正的解决。然而，就像现实中的法院，以太坊处理每一笔交易或争议的成本（Gas费用）较高，而且处理速度相对较慢，因为每个区块都需要网络中的大多数节点进行验证和共识。

“不要为了兑现支票而去法院”：这表示不是每一个操作或交易都需要直接在以太坊主链上进行。许多日常的小额交易或快速交互可以通过更高效的方式完成，而不必占用以太坊主链的资源。这就是二层扩展方案的作用，它们允许用户在不依赖于以太坊主链的情况下进行大量的交易和互动，从而提高了效率并降低了成本。

“只有在支票跳票时才去”：如果在L2系统中出现了问题，比如资金没有按照预期转移，或者发生了欺诈行为，这时用户可以回到以太坊主链（“法院”）来解决争议。以太坊主链的安全性和最终性保证了即使L2出现问题，用户的资产仍然是安全的，并且可以恢复到正确状态。

According to the elaboration of the saying, we could easily understand the EVM Equivalence as a set of rules that allow the execution of Ethereum smart contracts on Optimism with technique rollup architecturem which could provide two outstanding features:
1. uncensorable transactions
2. anybody can transcat

The Value of uncensorable transactions for rollup could be explained as following:

The concept of "uncensorable" in the context of Ethereum Virtual Machine (EVM) Equivalence refers to the characteristic of the Ethereum network that, once a transaction is broadcasted to the network and successfully included in a block, the outcome of the transaction and the state updates are not subject to censorship or reversal. This implies:

Unstoppable Transactions: Any user can initiate transactions as long as they adhere to the protocol rules of Ethereum (e.g., paying sufficient Gas fees), and these transactions cannot be prevented from entering the blockchain due to external intervention.

Immutable History: Once a transaction is included in a block that has been confirmed by the consensus mechanism, it becomes part of the immutable history of the blockchain. This history is considered permanent and unchangeable, unless more than 50% of the network's hash power is controlled to perform what is known as a 51% attack, which is extremely difficult and costly.

Decentralized Nature: Because Ethereum is a decentralized platform, no single entity can decide which transactions should be accepted or rejected. All nodes collectively maintain the security and integrity of the network, ensuring that each user's rights are not infringed upon.
Execution of Smart Contracts: Once smart contracts are deployed and execute automatically under specific conditions, their outcomes also cannot be blocked or reversed, unless the contract itself is coded with specific clauses allowing for such actions. This ensures that agreements between parties can reliably execute according to predefined rules.

In summary, "uncensorable" underscores one of the core values provided by Ethereum as a blockchain technology — offering an open, transparent, and trustless environment where information and value exchanges can occur freely without interference. This attribute is crucial for protecting user privacy, safeguarding freedom of speech, and building censorship-resistant applications.

In order to satisfy the requriement of Ethereum L1 & L2s infrasturucture, Optimistic comes with OVM and targeting to be an EVM equivalence. If L2s want to surf Ethereum’s wave of infrastructural network effects, they must become EVM equivalent.

Optimisistc practice EVM equivalence by achieveing L2 blocks executed with precise EVM equivalence. Instead of implementing the EVM in Solidity, implement a VM with a much smaller, simpler instruction set, and run the EVM within this VM during fraud proofs. To do this, we must simply compile an existing EVM interpreter, such as geth’s, to run within the simpler VM.

next day plan: focusing on sequencers, users, messagers role in Optimistic protocol stack and step into the next step of Optimistic protocol.

### 2024.01.08

今天的学习内容将聚焦于sequencers，users, messagers在Optimistic协议栈中的角色，以及进入Optimistic协议的下一步。

user has two majority activities: submit transcation and query transaction.

user submits transcation to interact with Ethereum through a sequencer
user query transcation from the interfaces operated by verifier

according to the above two activites, we need to about two roles: sequencers and verifiers

sequencers fill the role as block producer. In conclusion, sequencers will have these five activities:
1.Accepts transactions directly from Users.
2.Observes "deposit" transactions generated on Ethereum.
3.Consolidates both transaction streams into ordered L2 blocks.
4.Submits information to L1 that is sufficient to fully reproduce those L2 blocks.
5.Provides real-time access to pending L2 blocks that have not yet been confirmed on L1.

One thing need to be noted that the sequencers are not a trusted actor but responsible for improving the user experience by ordering transactions much more quickly and cheaply than would currently be possible if users were to submit all transactions directly to L1.

Verifier fill the role to download and execute the L2 state transition function independently of the Sequencer.

The depositing and sending transcation will have 5 steps:

1.Submit Deposit: Users initiate the process by submitting a deposit from Ethereum Layer 1 (L1) to the L2 network.
2.Fetch Deposit Events: The Sequencer  fetches deposit events from Ethereum L1 by OptimismPortal. This step ensures that the L2 network is aware of the deposits made on L1.
3.Generate Deposit Block: The Sequencer generates a deposit block based on the fetched deposit events. This block contains information about the deposits and is used to update the state of the L2 network.
4.Send Transactions: Once users have deposited ETH to pay fees, they can start sending transactions on the L2 network. These transactions are processed more efficiently than on L1 due to the nature of L2 solutions.
5.Submit Transaction Batches: The Sequencer submits transaction batches to the Batch Inbox Address on Ethereum L1. This step involves bundling multiple transactions into a single batch, which is then submitted to L1 for finality.
![alt text](image.png)

The withdrawal process is similar to the deposit process, but instead of sending ETH to the L2 network, users withdraw their funds from the L2 network to Ethereum L1. The withdrawal could be simply identified as: **Users withdraw ETH or ERC20 tokens from an OP Stack chain back to Ethereum.**

1.Send Withdrawal Initialization Transaction: Users initiate the withdrawal process by sending a transaction to start the withdrawal on L2.
2.Submit Transaction Batch: The Sequencer submits a batch of transactions, including the withdrawal initialization, to the Batch Inbox Address on Ethereum L1.
3.Submit Output Proposal: Proposers submit an output proposal to the DisputeGameFactory contract on L2.
4.Generate Game: The DisputeGameFactory generates a game based on the output proposal and sends it to the FaultDisputeGame contract.
5.Submit Withdrawal Proof: Users submit a proof of the withdrawal to the OptimismPortal contract on L2.
6.Wait for Finalization: The system waits for the finalization of the withdrawal process.
7.Submit Withdrawal Finalization: Users submit the finalization of the withdrawal to the OptimismPortal contract.
8.Check Game Validity: The OptimismPortal checks the validity of the game generated by the FaultDisputeGame contract.
9.Execute Withdrawal Transaction: Once the game is validated, the OptimismPortal executes the withdrawal transaction to transfer the funds to external contracts on Ethereum L1.

next day(2025.01.09) will learn about some new words/roles: Proposers, Game and OptimismPortal.

<!-- Content_END -->
