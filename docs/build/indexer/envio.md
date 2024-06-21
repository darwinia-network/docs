# Envio

Envio is a modern, multi-chain EVM blockchain indexing framework speed-optimized for querying real-time and historical data on Darwinia. 

**Envio HyperIndex**

Envio [HyperIndex](https://docs.envio.dev/docs/overview) is a feature-rich indexing solution that provides Darwinia projects with a seamless and efficient way to index and aggregate real-time or historical blockchain data. The indexed data is easily accessible through custom GraphQL queries, giving developers the flexibility and power to retrieve specific information for their blockchain application.

Envio offers native support for Darwinia's EVM networks and has been designed to support high-throughput blockchain applications that rely on real-time data for their business requirements.

Designed to optimize the developer experience, Envio offers automatic code generation, flexible language support, quickstart templates, and a reliable cost-effective [hosted service](https://docs.envio.dev/docs/hosted-service). Indexers on Envio can be written in JavaScript, TypeScript, or ReScript.

**Envio HyperSync**

Envio [HyperSync](https://docs.envio.dev/docs/hypersync) is supported on Darwinia Chain and Crab Chain.  

HyperSync is a real-time data query layer for Darwinia Network, providing APIs that bypass traditional JSON-RPC for up to 1000x faster syncing of historical data. HyperSync is used by default in Envio's indexing framework (HyperIndex), with RPC being optional for data retrieval. 

Using HyperSync, Darwinia Network projects do not need to worry about RPC URLs, rate-limiting, or managing their infrastructure - and can easily sync large datasets in a few minutes, something that would usually take hours or days using traditional indexing solutions. 

HyperSync is also available as a standalone API for data analytic use cases. Data analysts can interact with the HyperSync API using JavaScript, Python, or Rust clients and extract data in JSON, Arrow, or Parquet formats. For more information, visit the HyperSync documentation [here](https://docs.envio.dev/docs/overview-hypersync).

## Getting Started

Developers can choose to start from a template (e.g. Blank, ERC-20, etc.), or use the Contract Import feature when running the `envio init` command. Make sure you have installed the Envio CLI following the [installation guide](https://docs.envio.dev/docs/getting-started). 

The [Contract Import](https://docs.envio.dev/docs/contract-import) feature is a quickstart that allows Darwinia developers to quickly autogenerate the key boilerplate for an entire indexer project off single or multiple smart contracts, and easily start up a basic indexer and a custom GraphQL API for their blockchain application within a few minutes.

## Contract Import Tutorial

This walkthrough explains how to initialize an indexer using a single or multiple contracts that are already deployed on a blockchain. This process allows a user to quickly and easily start up a basic indexer and a queryable GraphQL API for their blockchain application within a few minutes.

### Initialize your indexer

`cd` into the folder of your choice and run

```bash
envio init
```

Name your indexer

```bash
? Name your indexer:
```

Choose the directory where you would like to setup your project (default is the current directory)

```bash
? Set the directory:  (.) .
```

Select `Contract Import` as the initialization option.

```bash
? Choose an initialization option
  Template
> ContractImport
[↑↓ to move, enter to select, type to filter]
```

```bash
? Would you like to import from a block explorer or a local abi?
  Block Explorer
> Local ABI
[↑↓ to move, enter to select, type to filter]
```

Block Explorer option only requires user to input the contracts address and chain of the contract. If the contract is verified and deployed on one of the supported chains, this is the quickest setup as it will retrieve all needed contract information from a block explorer. 

Please note: Block explorer option currently only supports networks with etherscan. If the network doesn't have etherscan, you can proceed using the Local ABI option. 

Choosing `Local ABI` option will allow you to point to a JSON file containing the smart contract ABI. The `Contract Import` process will then populate the required files from the ABI.

#### Specify the directory of JSON file containing ABI

```bash
? What is the path to your json abi file?
```

#### Choose which events to include in the `config.yaml` file

```bash
? Which events would you like to index?
> [x] ClaimRewards(address indexed from, address indexed reward, uint256 amount)
  [x] Deposit(address indexed from, uint256 indexed tokenId, uint256 amount)
  [x] NotifyReward(address indexed from, address indexed reward, uint256 indexed epoch, uint256 amount)
  [x] Withdraw(address indexed from, uint256 indexed tokenId, uint256 amount)
[↑↓ to move, space to select one, → to all, ← to none, type to filter]
```
#### Specify which chain the contract is deployed on
```bash
? Choose network:
> <Enter Network Id>
  ethereum-mainnet
  goerli
  optimism
  base
  bsc
  crab
  darwinia
v polygon
[↑↓ to move, enter to select, type to filter]
```
#### Enter in the name for the contract
```bash
? What is the name of this contract?
```
#### Enter in the address of the contract
```bash
? What is the address of the contract?
[Use the proxy address if your abi is a proxy implementation]
```
Note if you are using a proxy contract with an implementation, the address should be for the proxy.
#### Select the continuation option
```bash
? Would you like to add another contract?
> I'm finished
  Add a new address for same contract on same network
  Add a new network for same contract
  Add a new contract (with a different ABI)
[Current contract: BribeVotingReward, on network: darwinia]
```
The `Contract Import` process will prompt the user whether they would like to finish the import process or continue adding more addresses for same contract on same network, addresses for same contract on different network or a different contract.

For more information on contract import feature, visit the documentation [here](https://docs.envio.dev/docs/contract-import).

## Envio Indexer Examples
Click [here](https://docs.envio.dev/docs/example-uniswap-v3) for Envio Indexer Examples.

## Getting Help
Indexing can be a rollercoaster, especially for more complex use cases. Envio engineers are available for support and to help you with your data availability needs.
* [Discord](https://discord.gg/mZHNWgNCAc)
* Email: [hello@envio.dev](mailto:hello@envio.dev)
