# Hedera Account

This section covers topics related to accounts management.

## Features

Hedera maintains accounts in its ledger on the node, very much like Ethereum, but with some key differences in structure and usage.   

* **Explicitly Created**: Unlike Ethereum where accounts are implicitly created by sending Ether to an address, Hedera requires an explicit AccountCreateTransaction to create an account.

* **Account ID**: Each account is assigned a unique Account ID in the format `shard.realm.num` (e.g., 0.0.12345). This ID is the primary way to reference an account on the Hedera network.

* **Properties**: Hedera accounts have several properties stored on the ledger:
    * **Account Balance**: The amount of HBAR (Hedera's native cryptocurrency) held by the account.
    * **Public Key**: The public key associated with the account, used for authorizing transactions.   
    * **Other Properties**: Accounts can also have properties like:
        * `Key rotation`: The ability to update the public key associated with the account.
        * `Expiration time`: A time after which the account becomes inactive.
        * `Staking information`: For participating in network staking (if enabled).
        * `Contract association`: Linking the account to smart contracts.

## Hedera vs Ethereum Accounts:

* **Account ID vs Address**: Ethereum uses addresses derived directly from public keys, while Hedera uses distinct Account IDs.

* **Explicit Creation**: Hedera requires explicit account creation transactions, while Ethereum accounts are created implicitly.

* **Additional Properties**: Hedera accounts have more built-in properties compared to basic Ethereum accounts.

Banking analogy

| Ethereum | Hedera |
| --- | --- |
|  Your bank account number is directly derived from your fingerprint (public key). Anyone with your fingerprint can easily figure out your account number.  |  Your bank account has a unique account number assigned by the bank. You provide a signature card (public key) to authorize transactions. You can later update your signature card (change your public key) without changing your account number. |
