# Overview

[Hardhat](https://hardhat.org/) is a powerful Ethereum development environment designed to assist developers in managing and automating the repetitive tasks associated with building smart contracts and decentralized applications (DApps). Notably, Hardhat has the capability to directly interact with Darwinia's Ethereum API, enabling developers to deploy their smart contracts onto the Darwinia network. This compatibility allows developers to leverage Hardhat's features and tools when working with Darwinia, streamlining the development process and facilitating the creation of robust and reliable applications.

## Setting up a project

In this tutorial, we will explore the usage of hardhat by deploying a contract and performing various contract functionalities. The tutorial involves multiple script files, so let's create a new JavaScript project called `example-with-hardhat` to organize and manage the code effectively. This project will serve as a workaround for implementing the hardhat functionality.

```bash
mkdir example-with-hardhat && cd example-with-hardhat && npm init --y
```

Install the hardhat by runing the following command:

```bash
npm install --save-dev hardhat
```

If you run `npx hardhat` now, you will be shown some options to facilitate project creation:

```bash
$ npx hardhat
888    888                      888 888               888
888    888                      888 888               888
888    888                      888 888               888
8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
888    888 .d888888 888    888  888 888  888 .d888888 888
888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888

Welcome to Hardhat v2.17.3

? What do you want to do? …
▸ Create a JavaScript project
  Create a TypeScript project
  Create an empty hardhat.config.js
  Quit
```

Select `Create a JavaScript project`, a simple project creation wizard will ask you some questions. After that, the wizard will create some directories and files and install the necessary dependencies. The most important of these dependencies is the [Hardhat Toolbox](https://hardhat.org/hardhat-runner/plugins/nomicfoundation-hardhat-toolbox), a plugin that bundles all the things you need to start working with Hardhat.

The initialized project has the following structure:

```bash
contracts/
scripts/
test/
hardhat.config.js
```

These are the default paths for a Hardhat project.

- `contracts/` is where the source files for your contracts should be.
- `test/` is where your tests should go.
- `scripts/` is where simple automation scripts go.

## Contract Interaction

!!! note
    The network provider used in this tutorial is the [Crab testnet](../getting-started/networks/crab.md). However, the concepts and techniques covered in this tutorial are applicable to other Darwinia networks as well.


### Prepare And Compile Contract

Create a smart contract file under the `contracts` by running this command:

```bash
touch storage.sol
```

To showcase the interaction with the smart contract, we have prepared a simple Solidity smart contract. You can find the contract code pasted into the **`storage.sol`** file. This contract will serve as the basis for demonstrating how to interact with it using hardhat.

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

This contract is straightforward and easy to understand. It consists of two functionalities: storing a number and retrieving the updated number. Let's proceed to learn how to interact with this contract using hardhat.

To compile your contracts in your Hardhat project, use the built-in `compile` task:

```jsx
npx hardhat compile
```

The output looks like this and the compiled artifacts will be saved in the `artifacts/` directory by default.

```jsx
Compiled 1 Solidity file successfully
```

### Update Hardhat Config

Before working with the contracts, there are a few basic configurations that need to be set up. Replace the default **`hardhat.config`** file with the following content. This configuration includes the Crab network RPC information and adds a test account:

```jsx linenums="1" title="hardhat.config"
require("@nomicfoundation/hardhat-toolbox");

/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: "0.8.19",
  defaultNetwork: "crab",
  networks: {
    crab: {
      url: "https://crab-rpc.darwinia.network",
      accounts: ["0xd5cef12c5641455ad949c3ce8f9056478eeda53dcbade335b06467e8d6b2accc"]
    }
  }
};
```

By updating the **`hardhat.config`** file with this content, you will have the necessary configurations in place to interact with the Crab network and use the test account for testing purposes.

### Deploy Storage Contract

And paste the following content into it the `deploy.js` under scripts:

```jsx linenums="1" title="deploy.js"
const hre = require("hardhat");

async function main() {
  const storage = await hre.ethers.deployContract("Storage");
  await storage.waitForDeployment();
  console.log(`Contract deployed at address: ${storage.target}`);
}

// We recommend this pattern to be able to use async/await everywhere
// and properly handle errors.
main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

Start the deployment by running the command:

```jsx
npx hardhat run --network crab scripts/deploy.js
```

The output like this:

```jsx
Contract deployed at address: 0x46c66F6c65C7550a1CF94754979a1A52dB6C26c9
```

`0x46c66F6c65C7550a1CF94754979a1A52dB6C26c9` is the address of the deployed storage contract, as a unique identifier for that contract. It will be used later to store and retrieve the number.

### Using Hardhat Console

Hardhat comes built-in with an interactive JavaScript console. You can use it by running `npx hardhat console`:

```bash
$ npx hardhat console
Welcome to Node.js v12.10.0.
Type ".help" for more information.
>
```

Using the console tool, interacting with the deployed contract becomes incredibly convenient. Let's instantiate a storage contract and bind its address to it. By doing so, we will be able to easily interact with the contract and perform various operations on it.

```bash
# In the harhat console
const Storage = await ethers.getContractFactory('Storage');
const storage = await Storage.attach('0x46c66F6c65C7550a1CF94754979a1A52dB6C26c9');
```

### Store Number

```bash
# In the harhat console
await storage.store(3);
```

The output:

```jsx
ContractTransactionResponse {
  provider: HardhatEthersProvider {
    _hardhatProvider: LazyInitializationProviderAdapter {
      _providerFactory: [AsyncFunction (anonymous)],
      _emitter: [EventEmitter],
      _initializingPromise: [Promise],
      provider: [BackwardsCompatibilityProviderAdapter]
    },
    _networkName: 'crab',
    _blockListeners: [],
    _transactionHashListeners: Map(0) {},
    _eventListeners: []
  },
  blockNumber: null,
  blockHash: null,
  index: undefined,
  hash: '0xbc28842eaa299ac5f4ebbd781a34dd0ae957009f8f9764942ca574fae7c76d47',
  type: 2,
  to: '0x46c66F6c65C7550a1CF94754979a1A52dB6C26c9',
  from: '0x6Bc9543094D17f52CF6b419FB692797E48d275d0',
  nonce: 11,
  gasLimit: 45100n,
  gasPrice: 182721978177n,
  maxPriorityFeePerGas: 0n,
  maxFeePerGas: 182721978177n,
  data: '0x6057361d0000000000000000000000000000000000000000000000000000000000000003',
  value: 0n,
  chainId: 43n,
  signature: Signature { r: "0x191e493eed26c34426522a9e29d913dd0c5a94ae62b44e398b8e0eb72d597b90", s: "0x474e5f1b1f363047b9a7c8c99bdd9f9429946a12acb876c8741ac5ce04a77438", yParity: 0, networkV: null },
  accessList: []
}
```

### Retrieve Number

```bash
# In the harhat console
await storage.retrieve();
```

The output:

```bash
3n
```