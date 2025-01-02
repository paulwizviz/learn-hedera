# Ethereum Virtual Machine (EVM) Contracts and Hedera Token Service

This section discuss contract related to topics Smart Contracts and Hedera Token Service (HTS).

## EVM Contract

1. **Compatibility**:
    * Hedera uses the Ethereum Virtual Machine (EVM), making it compatible with Solidity, the primary programming language for Ethereum smart contracts.
    * This means developers can port existing Ethereum smart contracts to Hedera with minimal changes.

2. **Deployment**:
    * Smart contracts can be deployed on Hedera using tools like Hardhat, Truffle, or Hedera-specific SDKs.
    * They are stored and executed on the Hedera network and benefit from the Hashgraph consensus for speed and fairness.

3. **Performance**: While Hedera supports smart contracts, for certain operations (like token creation and transfers), developers are encouraged to use the Hedera Token Service (HTS). HTS provides a more efficient and cost-effective alternative to smart contracts for these specific tasks.

4. **Security**: The asynchronous Byzantine Fault Tolerance (aBFT) ensures a secure execution environment.

### Steps to deploy a Smart Contract in Go

1. Compile Smart Contract

Assuming using `solc`

```sh
solc --bin --optimize -o build SimpleStorage.sol
```

2. Read the complied byte code (`*.bin`) and use the Go SDK and deploy it. Unlike Geth, there is no need to generate ABI. Refer to [https://github.com/paulwizviz/go-hedera-app](https://github.com/paulwizviz/go-hedera-app).


## Hedera Token Service (HTS)

HTS is designed for creating and managing custom tokens on the Hedera network. It is separate from HBAR and can represent:

* Fungible assets (e.g., stablecoins, reward points).
* Non-fungible assets (e.g., NFTs, digital collectibles).
* Utility tokens for dApps or businesses.

The customisable features of Hedera Tokens are:

* **Fungibility**: Create fungible or non-fungible tokens.
* **Roles and Permissions**: Define admin, supply, and treasury roles.
* **Custom Fees**: Add transaction fees payable to specific accounts.
* **Custom Behaviours**: Use Hedera’s APIs for fine-grained token controls like freezing, wiping, or transferring.

### HBAR vs HTS Tokens

| Aspect | HBAR | HTS Tokens |
| --- | --- | --- |
| Purpose | Native cryptocurrency for fees, staking, and transactions.	| Custom tokens for specific use cases (e.g., dApps, NFTs). |
| Creation | Predefined and immutable. | Created programmatically or via tools using HTS. |
| Transaction Fees | Paid in HBAR. | Can define additional custom fees in HTS tokens. |
| Customisation | Not customisable. | Fully customisable (name, supply, fees, etc.). |
| Usage Examples | Paying for network fees, staking, dApp utility. |	Reward programs, NFTs, stablecoins, digital assets. |

### HTS Token managanent

* Create Token:
    * Programmatically:
        * **Initialise the Client**: Connect to the Hedera testnet or mainnet using your account ID and private key.
        * **Define Token Attributes**:
            * Set the token name, symbol, decimals, and initial supply.
            * Specify the treasury account (typically your account) to manage the tokens.
        * **Sign and Execute the Transaction**:
            * The TokenCreateTransaction must be signed with the treasury account’s private key.
            * The transaction is submitted to the Hedera network for processing.
        * **Confirm Creation**: Retrieve the transaction receipt to confirm success and obtain the new token’s ID.
    * Other means:
        * **Hedera Portal**: A web-based interface that allows users to interact with the Hedera network, including creating tokens.
        * **HashPack Wallet**: Some wallets provide token creation features for users without requiring programming.
        * **Third-Party Tools**: Platforms like DragonGlass or Arkhia offer dashboards for managing tokens and accounts on Hedera.

* Transfer tokens
* Mint additional tokens
* Burn tokens
* Assign custom fees and roles
* Freeze or wipe tokens

Refer to [https://github.com/paulwizviz/go-hedera-app](https://github.com/paulwizviz/go-hedera-app) for Go based working examples.

## HTS Tokens vs EVM Contracts

| Aspect | HTS | EVM Contracts |
| --- | --- | -- |
| Purpose | Token creation and management. | Implementing complex, customisable business logic. |
| Custom Logic | Limited to token configuration (e.g., roles, fees). | Fully customisable logic using programming languages like Solidity. |
| Ease of Use | Simple API for creating and managing tokens. | Requires writing and deploying smart contracts. |
| Performance | Highly efficient and faster than smart contracts for token-specific operations. | Slightly slower and more expensive due to execution in the EVM. |
| Use Cases | Native token creation, NFT minting, simple payment systems. | Complex DeFi applications, DAOs, marketplaces, games, etc. |

Hybrid HTS and EVM Contract use case:

* Use HTS for efficient token creation and transfer.
* Use Smart Contracts for advanced logic involving those tokens.

Example use case:

1.	Create a fungible token via HTS.
2.	Deploy a Solidity smart contract that uses the HTS token for specific business logic, such as staking or yield farming.