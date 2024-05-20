# Staking Precompile

To fully understand the concept of the precompile and its significance in the context of the Darwinia staking solution, it is important to have a grasp of the overall design of the staking solution. [The Darwinia staking](../../collator-staking.md) solution is implemented as a pallet, which is a modular component in the Substrate framework. Pallets are native to Substrate and provide a way to encapsulate and organize blockchain logic. However, they are not inherently compatible with Ethereum tools and infrastructure. One consequence of this design is that accessing the staking API with tools like MetaMask, which are commonly used in Ethereum development, is not possible out of the box. This is because MetaMask expects to interact with Ethereum-compatible contracts and APIs, and the staking solution implemented as a pallet in Darwinia does not natively adhere to those standards.

To bridge this gap and enable interaction with the staking API using Ethereum tools, the staking precompile comes into play. The staking precompile refers to a specific implementation that exposes the staking API in a format that is compatible with Ethereum tools such as MetaMask. By utilizing the staking precompile, developers can seamlessly integrate the Darwinia staking solution with their Ethereum workflows and tools.

## Contract Info

- The default contract address:  0x0000000000000000000000000000000000000601
- [The interface](https://github.com/darwinia-network/darwinia/blob/main/precompile/metadata/sol/staking.sol)
- [ABI](https://github.com/darwinia-network/darwinia/blob/main/precompile/metadata/abi/staking.json)