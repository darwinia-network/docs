Tether (USDT) is a widely used stablecoin in the crypto world. It has been [integrated into the Polkadot network](https://polkadot.network/newsroom/press-releases/tether-tokens-usdt-live-on-polkadot/) since 2022, specifically in the [AssetHub](https://support.polkadot.network/support/solutions/articles/65000181800-what-is-asset-hub-and-how-do-i-use-it-). This integration allows users to transfer USDT from the Polkadot AssetHub to the Darwinia Asset module, enabling them to utilize USDT within the Darwinia ecosystem. The management of USDT within the Darwinia is facilitated by the `pallet-asset` module, which is part of the Substrate ecosystem. This module provides various features for managing tokens, including token transfers, balance tracking, and other related operations.

In order to improve the compatibility of USDT with Ethereum-based tools and workflows, a dedicated precompile has been developed. This precompile acts as a bridge, simplifying the interaction between Ethereum users and USDT. By leveraging this precompile, Ethereum users can seamlessly interact with USDT using their familiar Ethereum tools, such as MetaMask.

<aside>
💡 **Note: As of 2023-11-21, the USDT functionality is only enabled for testing purposes in the Pangolin Testnet. We have plans to enable this in the Darwinia in the future.**

</aside>

# Contract Info

<aside>
💡 The default contract address:  0x0000000000000000000000000000000000000403

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