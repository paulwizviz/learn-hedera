# Key Management

This section covers topics related to cryptographic keys.

## `Ed25519` vs `ECDSA (secp256k1)` Keys

* `Ed25519` is generally the recommended key type for native Hedera operations like transfering HBAR.
* `ECDSA (secp256k1)` for operations with EVM contracts.

| Use Case | Key Type | Rationale |
| --- | --- | --- |
| Native Hedera Operations | Ed25519 | Recommended for most native Hedera operations, including:<ul><li>Creating accounts</li><li>Transferring HBAR</li><li>Updating account properties (e.g., key rotation)</li><li>File service operations</li><li>Consensus service operations</li></ul>Ed25519 offers better performance and security characteristics compared to ECDSA on Hedera for these use cases. |
| Interacting with EVM Smart Contracts | ECDSA (secp256k1) | Required for interacting with smart contracts deployed to Hedera's EVM. This is because the EVM expects transactions to be signed using ECDSA keys, maintaining compatibility with the Ethereum ecosystem. This includes:<ul><li>Deploying EVM contracts</li><li>Calling functions on EVM contracts</li><li>Sending transactions to EVM contracts</li></ul> |
| Multi-signature Accounts (General) | Ed25519 | Generally preferred for multi-signature accounts on Hedera for the same performance and security reasons as above. You can use Key Lists or Threshold Keys with Ed25519 keys. |
| Multi-signature Accounts (EVM Compatibility) | ECDSA (secp256k1) | If you need a multi-signature scheme that is also compatible with EVM contracts (e.g., a multi-sig wallet contract), you would need to use ECDSA keys. This is because the EVM's `ecrecover` precompile and other related functions operate on ECDSA signatures. However, it's important to note that implementing robust multi-sig directly in Solidity/EVM can be complex and gas-intensive. Often, it's better to manage multi-sig at the Hedera layer if EVM compatibility is not strictly required. |