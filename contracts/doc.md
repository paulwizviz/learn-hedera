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

2. Initialise Go Project

```go
package main

import (
	"fmt"
	"github.com/hashgraph/hedera-sdk-go/v2"
	"os"
)
```

3. Connect to Hedera

```go
func createHederaClient() *hedera.Client {
	client := hedera.ClientForTestnet()
	client.SetOperator(
		hedera.AccountID{Account: 12345}, // Replace with your Account ID
		hedera.PrivateKeyFromString("302e...") // Replace with your private key
	)
	return client
}
```

4. Deploy the Smart Contract

```go
func deploySmartContract(client *hedera.Client, bytecode []byte) (hedera.ContractID, error) {
	fileTx, err := hedera.NewFileCreateTransaction().
		SetKeys(client.GetOperatorPublicKey()).
		SetContents(bytecode).
		Execute(client)
	if err != nil {
		return hedera.ContractID{}, err
	}

	fileReceipt, err := fileTx.GetReceipt(client)
	if err != nil {
		return hedera.ContractID{}, err
	}

	contractFileID := fileReceipt.FileID

	contractTx, err := hedera.NewContractCreateTransaction().
		SetBytecodeFileID(*contractFileID).
		SetGas(100000).
		Execute(client)
	if err != nil {
		return hedera.ContractID{}, err
	}

	contractReceipt, err := contractTx.GetReceipt(client)
	if err != nil {
		return hedera.ContractID{}, err
	}

	return *contractReceipt.ContractID, nil
}
```

5. Interact with the Contract

```go
func callContractFunction(client *hedera.Client, contractID hedera.ContractID) error {
	callTx, err := hedera.NewContractExecuteTransaction().
		SetContractID(contractID).
		SetGas(100000).
		SetFunction("store", hedera.NewContractFunctionParameters().AddUint64(42)).
		Execute(client)
	if err != nil {
		return err
	}

	_, err = callTx.GetReceipt(client)
	return err
}
```

6. Main function

```go
func main() {
	client := createHederaClient()
	defer client.Close()

	bytecode, err := os.ReadFile("build/SimpleStorage.bin")
	if err != nil {
		fmt.Println("Error reading bytecode:", err)
		return
	}

	contractID, err := deploySmartContract(client, bytecode)
	if err != nil {
		fmt.Println("Error deploying contract:", err)
		return
	}

	fmt.Println("Contract deployed with ID:", contractID)

	err = callContractFunction(client, contractID)
	if err != nil {
		fmt.Println("Error calling contract:", err)
		return
	}

	fmt.Println("Contract function executed successfully!")
}
```