# Deployments

This section describes the deployment networks.

## Testnets

* Visit the [Hedera Portal](https://portal.hedera.com)
* **Sign Up**: Create an account with your email and verify it.
* **Generate a Testnet Account**:
    * After signing in, create a new testnet account.
    * You’ll receive:
        * Account ID (e.g., 0.0.12345).
        * Private Key and Public Key. (**NOTE**: Save the private key it’s required to interact with the testnet.)
* **Access Test HBAR**: The portal will provide a small balance of test HBAR to cover transaction fees.

Key Considerations for Testnet Tokens:

1.	**Persistence**: Testnet tokens will persist indefinitely unless you delete them manually or the Hedera testnet undergoes a periodic reset (testnets are sometimes reset by Hedera to maintain performance and free up resources).
2.	**Periodic Resets**:
    * Hedera may periodically reset the testnet, wiping out all accounts, tokens, and data. This does not occur on the mainnet.
    * Check the Hedera status page or announcements to confirm when resets occur.
3.	**Resource Usage**: Unused tokens do not consume significant network resources on the testnet, but it’s good practice to delete tokens you no longer need to simulate proper lifecycle management.

## Hedera Status Portal

[Status Portal](https://status.hedera.com/)