# Contracts

This section discuss contract related to topics

## Support for EVM

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
