# Redbelly Inc Smart Contract Documentation 

## Overview 

- **Name:** Tawhid
- **Symbol:** RBInc
- **Decimals:** 18
- **Total Supply:** 100,000,000 

## Description 

The Tawhid contract represents Redbelly Inc and facilitates the transfer of RBInc tokens between users. RBInc is a simple Redbelly Network token with a fixed supply, and the ownership is initially assigned to the contract deployer. 

## Functions 

1. **Constructor**
    - **Description:** Initializes the contract with the total supply assigned to the owner.
    
2. **Transfer**
    - **Function Signature:** `function transfer(address recipient, uint256 amount) public`
    - **Description:** Transfers RBInc tokens from the sender to the specified recipient.
    - **Requirements:**
        - Sender must have a sufficient balance.
        - The amount to transfer must not exceed the sender's balance.
    - **Example:**
        ```solidity
        function transfer(address recipient, uint256 amount) public {
            require(balances[msg.sender] >= amount, "Insufficient balance.");
            balances[msg.sender] -= amount;
            balances[recipient] += amount;
        }
        ``` 

### State Variables 

- **`name`**: The name of the token (Redbelly Inc).
- **`symbol`**: The symbol of the token (RBInc).
- **`decimals`**: The number of decimals for token value representation (18).
- **`totalSupply`**: The total supply of RBInc tokens. 

- **`balances`**: A mapping of addresses to their RBInc token balances.
- **`owner`**: The address that initially owns the total supply. 

## Getting Started 

### Prerequisites 

- EVM wallet or browser extension (e.g., MetaMask).
- RBInc tokens (RBInc). 

### Interacting with the Contract 

1. **Transferring RBInc Tokens**
    - Use the `transfer` function to send RBInc tokens to another address.
    - **Example:**
        ```javascript
        // Assume you have an instance of the Tawhid contract named 'rbContract'
        rbContract.transfer("0xRecipientAddress", 100);
        ``` 

## Deployment 

1. Deploy the contract to an Redbelly Network (testnet or devnet). 

## Examples 

### JavaScript/TypeScript 

```javascript
// Example using ethers.js
const { ethers } = require('ethers'); 

async function transferRBInc() {
    const provider = new ethers.providers.JsonRpcProvider('YOUR_RPC_ENDPOINT');
    const wallet = new ethers.Wallet('YOUR_PRIVATE_KEY', provider); 

    const contractAddress = 'YOUR_CONTRACT_ADDRESS';
    const contract = new ethers.Contract(contractAddress, ['function transfer(address recipient, uint256 amount) public'], wallet); 

    const recipientAddress = '0xRecipientAddress';
    const amount = 100; 

    const transaction = await contract.transfer(recipientAddress, amount);
    await transaction.wait();
    console.log(`Successfully transferred ${amount} RBInc to ${recipientAddress}`);
} 

transferRBInc();
