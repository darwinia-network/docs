<aside>
💡 Understanding the storage layout in the Substrate framework is crucial for effectively utilizing this precompile.

</aside>

As you may be aware, the underlying technology of Darwinia is built on the Substrate framework. Within this framework, certain features are implemented as runtime pallets. Unlike Ethereum, where the chain state data is typically stored in the EVM account storage, in Substrate, these pallets store the chain state data within their own pallet storage.

For the frequently used storage interaction pallets, we provide dedicated precompiles to facilitate seamless interaction with these pallets, such as staking, deposit pallets. These precompiles enable users to access and manipulate the data stored within the pallet storage efficiently, without the need for complex custom integrations. However, there are cases where the pallet storage needs to be accessed on the EVM side, although this is not a common scenario. To address these cases, we have designed the `state_storage` precompile. This precompile allows users to access and retrieve data from the allowed pallet storage using the substrate storage key.

# Contract Info

<aside>
💡 The default contract address:  0x0000000000000000000000000000000000000400

</aside>

## Interface

<aside>
💡 The Interface represents the high-level definition of a contract. It defines the functions, events, and modifiers that are part of the contract's public API. Interfaces are used to interact with other contracts or to provide an abstract interface for contract implementations.

</aside>

[](https://github.com/darwinia-network/darwinia/blob/main/precompile/metadata/sol/state-storage.sol)

## ABI

<aside>
💡 The Application Binary Interface (ABI) is a standardized format used to specify the layout and encoding of data and function calls in Ethereum. It defines how data is packed and unpacked when interacting with smart contracts. The ABI includes information such as function names, types of input and output parameters, and the bytecodes used to call functions.

</aside>