# Architecture

This section discusses the architecture of Hedera.

## Key Features

1. **Hashgraph Consensus**
    * **Gossip Protocol**: Nodes communicate by sharing transaction information with random neighbouring nodes. This “gossip about gossip” creates a record of communication history.
    * **Virtual Voting**: Nodes reach consensus by analysing the shared information, eliminating the need for extensive communication or energy-intensive mining.

2. **Governance Model**: Hedera is governed by a Council of 39 global organisations, including enterprises like Google, IBM, and Tata Communications. These members rotate and ensure decentralised decision-making.

3. **Node Network**:
    * **Public Nodes**: Ensure open participation in the network.
    * **Council Nodes**: Managed by council members to maintain the network’s security and stability. Over time, the network aims to expand decentralisation by increasing public node participation.

4. **Token Service (HTS)**: Allows users to issue, transfer, and manage native fungible and non-fungible tokens directly on Hedera without smart contracts, making transactions more efficient and cost-effective.

5. **Smart Contracts**: Hedera supports Solidity-based smart contracts, executed in the Ethereum Virtual Machine (EVM) environment.

6. **Consensus Service (HCS)**: Enables the logging of messages or events to the ledger with timestamps and consensus, ideal for tracking and auditing.

7. **Hedera File Service**: Provides decentralised storage for small files or data, linked to the ledger for transparency and security.

8. **Cryptographic Security**: Utilises asynchronous Byzantine Fault Tolerance (aBFT), ensuring high security against malicious actors while maintaining performance.

9. **Hedera Token (HBAR)**: HBAR is used for:
    * Transaction fees.
    * Network services like smart contract execution and file storage.
    * Staking to ensure network security.

## Hedera (Hashgraph) vs Blockchain

| Feature               | Blockchain-Based Solution           | Hedera (Hashgraph)               |
|-----------------------|--------------------------------------|-----------------------------------|
| **Consensus Mechanism** | Proof of Work (PoW), Proof of Stake (PoS) | Hashgraph with Gossip & Virtual Voting |
| **Transaction Structure** | Sequential blocks                  | Directed Acyclic Graph (DAG)     |
| **Finality**           | Probabilistic (requires confirmations) | Instant (asynchronous BFT)       |
| **Throughput**         | Limited (e.g., Ethereum ~30 TPS)    | High (10,000+ TPS)               |
| **Governance**         | Decentralised among miners/stakers  | Council of 39 global organisations |
| **Fairness**           | Potential miner/staker bias         | Timestamp-based ordering         |
| **Energy Efficiency**  | High (PoW systems are energy-intensive) | Low (no mining required)         |
| **Scalability**        | Limited by block size and intervals | Highly scalable via DAG structure |
| **Security**           | Varies by protocol (e.g., 51% attack risk) | Asynchronous BFT (aBFT)          |
| **Cost**               | Variable and often high             | Predictable and low              |

## Hashgraph Consensus

Hedera operates on Hashgraph, achieves consensus through:

1.	**Gossip Protocol**:
    * Nodes randomly share transaction information with neighbouring nodes.
    * Each “gossip” includes both the transaction and metadata about the communication itself (called “gossip about gossip”).
    * This process ensures rapid and efficient propagation of information across the network.

2.	**Virtual Voting**:
    * Using the metadata shared during gossip, each node can independently calculate the consensus without direct voting.
    * Nodes determine the order and validity of transactions by analysing the shared 'gossip history.'

3.	**Asynchronous Byzantine Fault Tolerance (aBFT)**:
    * Guarantees that the system can reach consensus even if some nodes act maliciously.
    * Consensus is reached as soon as nodes have sufficient information, without waiting for blocks to be confirmed.

4.	**Transaction Finality**: Transactions achieve instant finality once consensus is reached. There is no need to wait for multiple confirmations as in many blockchain systems.
