# Overview

!!! note
    Familiarity with Linux/Javascript is essential.

[Web3.js](https://web3js.org/) is a comprehensive library that enables developers to communicate with Ethereum nodes using various protocols such as HTTP or WebSocket in JavaScript. Darwinia offers an [Ethereum-Compatible API](../../learn/ethereum-compatibility/jsonrpc.md) that supports JSON RPC calls similar to Ethereum. As a result, developers can utilize the Web3.js library to interact with a Darwinia node in the same way they would interact with an Ethereum node. This compatibility simplifies the process of building applications that interact with Darwinia using familiar Ethereum tools and libraries.

## Prerequisites

### Install Solidity Compiler

The solc compiler is a JavaScript library used to retrieve the code and ABI metadata of a Solidity smart contract by compiling it. This allows developers to access the necessary information for interacting with the smart contract programmatically. Run the following command to install:

```bash
npm install -g solc
```

Check the installed result by:

```bash
solc --version
```

The output:

```bash
solc, the solidity compiler commandline interface
Version: 0.8.17+commit.8df45f5f.Linux.g++
```

### Install Web3.js

In this tutorial, we will explore the usage of web3.js by deploying a contract and performing various contract functionalities. The tutorial involves multiple script files, so let's create a new JavaScript project called **`example-with-web3js`** to organize and manage the code effectively. This project will serve as a workaround for implementing the web3.js functionality.

```bash
mkdir example-with-web3js && cd example-with-web3js && npm init --y
```

Install the Web3.js by runing the following command:

```bash
npm install web3@1.10.2
```

## Contract Interaction


!!! note
    The network provider used in this tutorial is the Pangolin Testnet. However, the concepts and techniques covered in this tutorial are applicable to other Darwinia networks as well.

### Prepare Contract

Create a smart contract file by running this command:

```bash
touch storage.sol
```

To showcase the interaction with the smart contract, we have prepared a simple Solidity smart contract. You can find the contract code pasted into the **`storage.sol`** file. This contract will serve as the basis for demonstrating how to interact with it using web3.js.

```solidity linenums="1" title="storage.sol"
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.8.2 <0.9.0;

contract Storage {

    uint256 number;

    /**
     * @dev Store value in variable
     * @param num value to store
     */
    function store(uint256 num) public {
        number = num;
    }

    /**
     * @dev Return value 
     * @return value of 'number'
     */
    function retrieve() public view returns (uint256){
        return number;
    }
}
```

This contract is straightforward and easy to understand. It consists of two functionalities: storing a number and retrieving the updated number. Let's proceed to learn how to interact with this contract using web3.js.

### Generate Contract Metadata

When interacting with a contract using Web3.js, it is essential to have the contract metadata. The toolchain relies on this metadata information to properly interact with the contract. To generate the metadata and store it in a **`metadata.json`** file, you can run the following command:

```bash
solc storage.sol --combined-json abi,bin,hashes --pretty-json > metadata.json
```

The output of `cat metadata.json`:

```json
{
  "contracts": {
    "storage.sol:Storage": {
      "abi": [
        {
          "inputs": [],
          "name": "retrieve",
          "outputs": [
            {
              "internalType": "uint256",
              "name": "",
              "type": "uint256"
            }
          ],
          "stateMutability": "view",
          "type": "function"
        },
        {
          "inputs": [
            {
              "internalType": "uint256",
              "name": "num",
              "type": "uint256"
            }
          ],
          "name": "store",
          "outputs": [],
          "stateMutability": "nonpayable",
          "type": "function"
        }
      ],
      "bin": "608060405234801561001057600080fd5b50610150806100206000396000f3fe608060405234801561001057600080fd5b50600436106100365760003560e01c80632e64cec11461003b5780636057361d14610059575b600080fd5b610043610075565b60405161005091906100a1565b60405180910390f35b610073600480360381019061006e91906100ed565b61007e565b005b60008054905090565b8060008190555050565b6000819050919050565b61009b81610088565b82525050565b60006020820190506100b66000830184610092565b92915050565b600080fd5b6100ca81610088565b81146100d557600080fd5b50565b6000813590506100e7816100c1565b92915050565b600060208284031215610103576101026100bc565b5b6000610111848285016100d8565b9150509291505056fea264697066735822122084d3253ae949e222c0defd4cd0cd1238db9d84a3fee248e7cd91529d9a759ad164736f6c63430008110033",
      "hashes": {
        "retrieve()": "2e64cec1",
        "store(uint256)": "6057361d"
      }
    }
  },
  "version": "0.8.17+commit.8df45f5f.Linux.g++"
}
```

### Deploy Storage Contract

Create a deploy script by running this command:

```bash
node deploy.js
```

And paste the following content into it:

```jsx linenums="1" title="deploy.js"
const  Web3 = require("web3");
const contractMetadata = require("./metadata.json");

// The test account
const accountFrom = {
    address: "0x6Bc9543094D17f52CF6b419FB692797E48d275d0",
    privateKey: "0xd5cef12c5641455ad949c3ce8f9056478eeda53dcbade335b06467e8d6b2accc",
}

const web3 = new Web3('https://pangolin-rpc.darwinia.network');
const abi = contractMetadata.contracts["storage.sol:Storage"].abi;
const bin = contractMetadata.contracts["storage.sol:Storage"].bin;

const deploy = async () => {
    console.log(`Attempting to deploy from account ${accountFrom.address}`);

    // Construct the contract instance
    const contract = new web3.eth.Contract(abi);
    // Create the deploy contract raw transaction
    let rawTransaction = contract.deploy({
        data: bin,
    });

    // Sign the raw transaction with the private key
    const createTransaction = await web3.eth.accounts.signTransaction(
        {
            from: accountFrom.address,
            data: rawTransaction.encodeABI(),
            gas: await rawTransaction.estimateGas(),
            gasPrice: await web3.eth.getGasPrice()
        },
        accountFrom.privateKey
    );

    const createReceipt = await web3.eth.sendSignedTransaction(
        createTransaction.rawTransaction
    );
    console.log(`Contract deployed at address: ${createReceipt.contractAddress}`);
};

deploy();
```

Start the deployment by running the command:

```bash
node deploy.js
```

The output like this:

```bash
Attempting to deploy from account 0x6Bc9543094D17f52CF6b419FB692797E48d275d0
Contract deployed at address: 0x677163264bcb88A6f8F71E2B7D88F51d54325AB1
```

`0x677163264bcb88A6f8F71E2B7D88F51d54325AB1` is the address of the deployed storage contract, as a unique identifier for that contract. It will be used later to store and retrieve the number.

### Store Number

Create a store script by running this command:

```bash
touch store.js
```

Please paste the following content into the `store.js` file, *ensuring that you have updated the **`contractAddress`** in the script with the address of the contract you deployed.*

```jsx linenums="1" title="store.js"
const  Web3 = require("web3");
const contractMetadata = require("./metadata.json");

// The test account
const accountFrom = {
    address: "0x6Bc9543094D17f52CF6b419FB692797E48d275d0",
    privateKey: "0xd5cef12c5641455ad949c3ce8f9056478eeda53dcbade335b06467e8d6b2accc",
}

const web3 = new Web3('https://pangolin-rpc.darwinia.network');
const abi = contractMetadata.contracts["storage.sol:Storage"].abi;

// The contract address deployed in last step
const contractAddress = '0x677163264bcb88A6f8F71E2B7D88F51d54325AB1';
const store = async () => {
    web3.eth.accounts.wallet.add(accountFrom.privateKey);

    // Construct the contract instance
    let storageContract = new web3.eth.Contract(abi, contractAddress);
    storageContract.options.from = accountFrom.address;
    storageContract.options.gas = 4_000_000;
    
    // Call store to update the number to 3
    let receipt = await storageContract.methods.store(3).send();
    console.log(`Tx successful with hash: ${receipt.transactionHash}`);
};

store();
```

Run the script by the command:

```bash
node store.js
```

The output:

```bash
Tx successful with hash: 0x524f2647157635978feff15754400f36d93d2e4bc5f0b0119da0a671b666cd74
```

### Retrieve Number

Create a retrieve script by running this command:

```bash
touch retrieve.js
```

Please paste the following content into the `retrieve.js` file, *ensuring that you have updated the **`contractAddress`** in the script with the address of the contract you deployed.*

```jsx linenums="1" title="retrieve.js"
const  Web3 = require("web3");
const contractMetadata = require("./metadata.json");

const web3 = new Web3('https://pangolin-rpc.darwinia.network');
const abi = contractMetadata.contracts["storage.sol:Storage"].abi;

// The contract address deployed in last step
const contractAddress = '0x677163264bcb88A6f8F71E2B7D88F51d54325AB1';
const retrieve = async () => {
    // Construct the contract instance
    let storageContract = new web3.eth.Contract(abi, contractAddress);
    // Call retrieve
    let number = await storageContract.methods.retrieve().call();
    console.log(`The current number stored is: ${number}`);
};

retrieve();
```

Run the script by the command:

```bash
node retrieve.js
```

The output:

```sh
The current number stored is: 3
```