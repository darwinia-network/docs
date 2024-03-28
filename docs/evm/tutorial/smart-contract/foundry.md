<aside>
💡 Familiarity with Linux/Rust is essential.

</aside>

# **Overview**

[Foundry](https://github.com/foundry-rs/foundry) is a Rust-based Ethereum development environment that provides various tools for managing dependencies, compiling projects, running tests, deploying contracts, and interacting with blockchains from the command line. It can also directly interact with the Darwinia Ethereum API, allowing developers to deploy smart contracts into Darwinia.

The four main tools in Foundry are:

1. [Forge](https://github.com/foundry-rs/foundry/blob/master/crates/forge): This tool is used for compiling, testing, and deploying contracts.
2. [Cast](https://github.com/foundry-rs/foundry/blob/master/crates/cast): Cast is a command line interface that enables developers to interact with contracts.
3. [Anvil](https://github.com/foundry-rs/foundry/blob/master/crates/anvil): Anvil is a local TestNet node that can be used for development purposes. It has the ability to fork preexisting networks.
4. [Chisel](https://github.com/foundry-rs/foundry/blob/master/crates/chisel): Chisel is a Solidity REPL (Read-Eval-Print Loop) that allows for quick testing of Solidity snippets.

This guide will provide instructions on how to use Foundry's Forge and Cast tools to interact with Ethereum smart contracts on the Darwinia Pangolin TestNet.

# **Prerequisites**

### Install Foundry

See the [installation guide](https://book.getfoundry.sh/getting-started/installation) in the book, run the following command in Linux:

```bash
curl -L https://foundry.paradigm.xyz | bash
```

### **Setting up a project**

In this tutorial, we will explore the usage of foundry by deploying a contract and performing various contract functionalities. The tutorial involves multiple script files, so let's create a new project called `example-with-foundry` to organize and manage the code effectively. This project will serve as a workaround for implementing the foundry functionality.

```bash
forge init example-with-foundry
```

With the default project created, you should see three folders.

- `lib` - all of the project's dependencies in the form of git submodules
- `src` - where to put your smart contracts (with functionality)
- `test` - where to put the forge tests for your project, which are written in Solidity

In addition to these three folders, a git project will also be created along with a prewritten `.gitignore` file with relevant file types and folders ignored.

# Contract Interaction

<aside>
💡 The network provider used in this tutorial is the Pangolin Testnet. However, the concepts and techniques covered in this tutorial are applicable to other Darwinia networks as well.

</aside>

## Prepare And Compile Contract

Create a smart contract file under the `src` by running this command:

```bash
touch storage.sol
```

To showcase the interaction with the smart contract, we have prepared a simple Solidity smart contract. You can find the contract code pasted into the **`storage.sol`** file. This contract will serve as the basis for demonstrating how to interact with it using foundry.

```solidity
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

This contract is straightforward and easy to understand. It consists of two functionalities: storing a number and retrieving the updated number. Let's proceed to learn how to interact with this contract using foundry.

To compile your contracts in your foundry project, use the built-in `compile` task:

```jsx
forge build
```

The output looks like this and the compiled artifacts will be saved in the `out/` directory by default.

```jsx
[⠊] Compiling...
[⠘] Installing solc version 0.8.21
[⠃] Successfully installed solc 0.8.21
[⠑] Compiling 23 files with 0.8.21
[⠒] Solc 0.8.21 finished in 2.77s
Compiler run successful!
```

## Deploy Storage Contract

Start the deployment by running the command:

```bash
forge create --rpc-url https://pangolin-rpc.darwinia.network --private-key 0xd5cef12c5641455ad949c3ce8f9056478eeda53dcbade335b06467e8d6b2accc src/storage.sol:Storage
```

The output like this:

```bash
[⠢] Compiling...
No files changed, compilation skipped
Deployer: 0x6Bc9543094D17f52CF6b419FB692797E48d275d0
Deployed to: 0x0De784894D8FfE792EA7cF108E96f6e4451D066E
Transaction hash: 0x8a9089e9aaf1569807cf3bae0f525370a490444fb6c55702aee46aaad70e7e32
```

`0x0De784894D8FfE792EA7cF108E96f6e4451D066E` is the address of the deployed storage contract, as a unique identifier for that contract. It will be used later to store and retrieve the number.

## **Store Number**

Run the command:

```bash
cast send --private-key 0xd5cef12c5641455ad949c3ce8f9056478eeda53dcbade335b06467e8d6b2accc --rpc-url https://pangolin-rpc.darwinia.network 0x0De784894D8FfE792EA7cF108E96f6e4451D066E "store(uint256)" 3
```

The output:

```bash
blockHash               0x76301b13b73500b15ccfff4a8336140a571467351899577b101d28c5f0eaa679
blockNumber             1463191
contractAddress         
cumulativeGasUsed       43516
effectiveGasPrice       167997624034
gasUsed                 43516
logs                    []
logsBloom               0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
root                    
status                  1
transactionHash         0x280c2af73fa5914a9c41defdde2127aff58e7dded48bea0de5676974fcb83d97
transactionIndex        0
type                    2
```

## **Retrieve Number**

Run the command:

```bash
cast call 0x0De784894D8FfE792EA7cF108E96f6e4451D066E "retrieve()" --rpc-url https://pangolin-rpc.darwinia.network
```

The output: