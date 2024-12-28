# Deployments

This section describes the deployment networks.

## Testnets

1. Create a Hedera Testnet Account
    * Visit the Hedera Portal: https://portal.hedera.com
    * **Sign Up**: Create an account with your email and verify it.
    * **Generate a Testnet Account**:
        * After signing in, create a new testnet account.
        * You’ll receive:
            * Account ID (e.g., 0.0.12345).
            * Private Key and Public Key. (**NOTE**: Save the private key it’s required to interact with the testnet.)
    * **Access Test HBAR**: The portal will provide a small balance of test HBAR to cover transaction fees.

2. Set up the development environment (Go)

Install the Hedera SDK for Go.

```sh
go get github.com/hashgraph/hedera-sdk-go/v2
```

3. Write Go code to connect to the Testnet

```go
package main

import (
	"fmt"
	"log"

	"github.com/hashgraph/hedera-sdk-go/v2"
)

func main() {
	// Replace with your Testnet Account ID and Private Key
	accountID := hedera.AccountID{Account: 12345}
	privateKey, err := hedera.PrivateKeyFromString("302e020100300506032b657004220420...") // Replace with your private key
	if err != nil {
		log.Fatalf("Error parsing private key: %v", err)
	}

	// Create a client for the Hedera Testnet
	client := hedera.ClientForTestnet()
	client.SetOperator(accountID, privateKey)
	defer client.Close()

	fmt.Println("Connected to Hedera Testnet!")
}
```

4. Test the connection

Scenario: Transfer HBAR
```go
func transferHBAR(client *hedera.Client) {
	recipient := hedera.AccountID{Account: 54321} // Replace with recipient account ID

	transferTx, err := hedera.NewTransferTransaction().
		AddHbarTransfer(client.GetOperatorAccountID(), -hedera.HbarFrom(10, "hbar")). // Deduct 10 HBAR
		AddHbarTransfer(recipient, hedera.HbarFrom(10, "hbar")).                     // Add 10 HBAR
		Execute(client)

	if err != nil {
		log.Fatalf("Error executing transfer: %v", err)
	}

	receipt, err := transferTx.GetReceipt(client)
	if err != nil {
		log.Fatalf("Error getting receipt: %v", err)
	}

	fmt.Printf("Transfer successful: %v\n", receipt.Status)
}

func main() {
	// Create and configure the client (as shown earlier)
	client := createHederaClient()
	defer client.Close()

	// Transfer HBAR
	transferHBAR(client)
}
```

5. Explorer the Hedera Testnet Dashboard

After running transactions, you can view their status and details on the [Hedera Testnet Explorer](https://hashscan.io/testnet)