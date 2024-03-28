Before delving into the understanding of this precompile, it's essential to have knowledge about the [Darwinia Native Token](https://www.notion.so/Token-And-Economic-Model-ebfbf88c76794215a4abe75ae13f596b?pvs=21) and the [Commitment Token](https://www.notion.so/Commitment-Token-e17a95fb26664e0d8b39d26370847797?pvs=21), within the Darwinia ecosystem. In the architecture of Darwinia, the native token is designed to be fundamentally compatible with Ethereum. This means that the native token can be seamlessly used in Ethereum-compatible environments without requiring extensive modifications or adaptations. It provides out-of-the-box compatibility, allowing users to interact with the native token using Ethereum tools and infrastructure. However, the commitment token in the Darwinia system operates differently. It is a separate standalone token that functions within the Darwinia ecosystem. The commitment token is implemented by a pallet called the [pallet-asset](https://marketplace.substrate.io/pallets/pallet-assets/), which is part of the Substrate ecosystem. The pallet-asset facilitates the management of the commitment token, including features such as token transfers, balances, and other related operations.

Similar to the staking and deposit precompiles, the commitment token also requires a dedicated precompile to enhance its usability for users of Ethereum tools. This precompile acts as a bridge, simplifying the interaction between Ethereum users and the commitment token. By leveraging this precompile, Ethereum users can seamlessly interact with the commitment token using their familiar Ethereum workflows and tools, such as MetaMask.

# Contract Info

<aside>
💡 The default contract address:  0x0000000000000000000000000000000000000402

</aside>

## Interface

<aside>
💡 The Interface represents the high-level definition of a contract. It defines the functions, events, and modifiers that are part of the contract's public API. Interfaces are used to interact with other contracts or to provide an abstract interface for contract implementations.

</aside>

[](https://github.com/darwinia-network/darwinia/blob/main/precompile/metadata/sol/asset.sol)

## ABI

<aside>
💡 The Application Binary Interface (ABI) is a standardized format used to specify the layout and encoding of data and function calls in Ethereum. It defines how data is packed and unpacked when interacting with smart contracts. The ABI includes information such as function names, types of input and output parameters, and the bytecodes used to call functions.

</aside>