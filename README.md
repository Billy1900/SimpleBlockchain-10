# SimpleBlockchain-10 English Version
add network based on simple block chain-9
## Blockchain network
The blockchain network is decentralized, which means that there is no server, and the client does not need to rely on the server to obtain or process data. In the blockchain network, there are nodes, and each node is a full-fledged member of the network. The node is everything: it is both a client and a server. This needs to be kept in mind, because this is very different from traditional web applications.

The blockchain network is a P2P (Peer-to-Peer, end-to-end) network, that is, nodes are directly connected to other nodes. Its topology is flat, because there is no hierarchy in the world of nodes.

## Node role
Although nodes have complete and mature attributes, they can also play different roles in the network. such as:

1. Miners Such nodes run on powerful or dedicated hardware (such as ASIC), and their only goal is to mine new blocks as quickly as possible. Miners are the only role in the blockchain that may use proof of work, because mining actually means solving the PoW problem. In the blockchain of Proof-of-Stake, there is no mining.

2. Full nodes These nodes verify the validity of the blocks mined by miners and confirm transactions. For this, they must have a complete copy of the blockchain. At the same time, all nodes perform routing operations to help other nodes discover each other. For the network, a very important section is to have enough full nodes. Because it is these nodes that perform the decision-making function: they determine the validity of a block or a transaction.

3. SPV SPV stands for Simplified Payment Verification, simple payment verification. These nodes do not store a copy of the entire blockchain, but can still verify transactions (but not all transactions, but a subset of transactions, such as transactions sent to a specified address). An SPV node depends on a full node to obtain data. There may be multiple SPV nodes connected to a full node. SPV makes wallet applications possible: a person does not need to download the entire blockchain, but can still verify his transactions.

## Network Simplification
In order to implement the network in the current blockchain prototype, I had to simplify some things. Because I don't have so many computers to simulate a multi-node network. Of course, we can use virtual machines or Docker to solve this problem. Therefore, we want to run multiple blockchain nodes on a machine, and hope that they have different addresses. In order to achieve this, we will use the port number as the node identifier instead of the IP address. For example, there will be nodes with such addresses: 127.0.0.1:3000, 127.0.0.1:3001, 127.0.0.1:3002, etc. We call it the port node ID and use the environment variable NODE_ID to set them. Therefore, you can open multiple terminal windows and set different NODE_IDs to run different nodes.

This method also requires different blockchain and wallet files. They must now be named depending on the node ID, such as blockchain_3000.db, blockchain_30001.db, wallet_3000.db, wallet_30001.db, etc.


Hard-coding an address in Bitcoin Core has proven to be an error: because the node may be attacked or shut down, this will cause new nodes to be unable to join the network. In Bitcoin Core, DNS seeds are hard-coded. Although these are not nodes, the DNS server knows the addresses of some nodes. When you start a brand new Bitcoin Core, it will connect to a seed node, get the full node list, and then download the blockchain from these nodes.

However, in the current implementation, it is impossible to achieve complete decentralization because of the characteristics of centralization. We will have three nodes:

- A central node. All other nodes will connect to this node, and this node will send data between other nodes.
- A miner node. This node will store new transactions in the memory pool, and when there are enough transactions, it will pack and mine a new block.
- A wallet node. This node will be used to send coins between wallets. But unlike the SPV node, it stores a complete copy of the blockchain.


# SimpleBlockchain-10 Chinese Version
## 区块链网络
区块链网络是去中心化的，这意味着没有服务器，客户端也不需要依赖服务器来获取或处理数据。在区块链网络中，有的是节点，每个节点是网络的一个完全（full-fledged）成员。节点就是一切：它既是一个客户端，也是一个服务器。这一点需要牢记于心，因为这与传统的网页应用非常不同。

区块链网络是一个 P2P（Peer-to-Peer，端到端）的网络，即节点直接连接到其他节点。它的拓扑是扁平的，因为在节点的世界中没有层级之分.

## 节点角色
尽管节点具有完备成熟的属性，但是它们也可以在网络中扮演不同角色。比如：

1. 矿工 这样的节点运行于强大或专用的硬件（比如 ASIC）之上，它们唯一的目标是，尽可能快地挖出新块。矿工是区块链中唯一可能会用到工作量证明的角色，因为挖矿实际上意味着解决 PoW 难题。在权益证明 PoS 的区块链中，没有挖矿。

2. 全节点 这些节点验证矿工挖出来的块的有效性，并对交易进行确认。为此，他们必须拥有区块链的完整拷贝。同时，全节点执行路由操作，帮助其他节点发现彼此。对于网络来说，非常重要的一段就是要有足够多的全节点。因为正是这些节点执行了决策功能：他们决定了一个块或一笔交易的有效性。

3. SPV SPV 表示 Simplified Payment Verification，简单支付验证。这些节点并不存储整个区块链副本，但是仍然能够对交易进行验证（不过不是验证全部交易，而是一个交易子集，比如，发送到某个指定地址的交易）。一个 SPV 节点依赖一个全节点来获取数据，可能有多个 SPV 节点连接到一个全节点。SPV 使得钱包应用成为可能：一个人不需要下载整个区块链，但是仍能够验证他的交易。

## 网络简化
为了在目前的区块链原型中实现网络，我不得不简化一些事情。因为我没有那么多的计算机来模拟一个多节点的网络。当然，我们可以使用虚拟机或是 Docker 来解决这个问题. 所以，我们想要在一台机器上运行多个区块链节点，同时希望它们有不同的地址。为了实现这一点，我们将使用端口号作为节点标识符，而不是使用 IP 地址，比如将会有这样地址的节点：127.0.0.1:3000，127.0.0.1:3001，127.0.0.1:3002 等等。我们叫它端口节点（port node） ID，并使用环境变量 NODE_ID 对它们进行设置。故而，你可以打开多个终端窗口，设置不同的 NODE_ID 运行不同的节点。

这个方法也需要有不同的区块链和钱包文件。它们现在必须依赖于节点 ID 进行命名，比如 blockchain_3000.db, blockchain_30001.db , wallet_3000.db, wallet_30001.db 等等。


在 Bitcoin Core 中硬编码一个地址，已经被证实是一个错误：因为节点可能会被攻击或关机，这会导致新的节点无法加入到网络中。在 Bitcoin Core 中，硬编码了 DNS seeds。虽然这些并不是节点，但是 DNS 服务器知道一些节点的地址。当你启动一个全新的 Bitcoin Core 时，它会连接到一个种子节点，获取全节点列表，随后从这些节点中下载区块链。

不过目前的实现中，无法做到完全的去中心化，因为会出现中心化的特点。我们会有三个节点：

- 一个中心节点。所有其他节点都会连接到这个节点，这个节点会在其他节点之间发送数据。
- 一个矿工节点。这个节点会在内存池中存储新的交易，当有足够的交易时，它就会打包挖出一个新块。
- 一个钱包节点。这个节点会被用作在钱包之间发送币。但是与 SPV 节点不同，它存储了区块链的一个完整副本。

