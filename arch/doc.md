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
