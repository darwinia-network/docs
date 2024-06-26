# USDT Precompile

Tether (USDT) is a widely used stablecoin in the crypto world. It has been [integrated into the Polkadot network](https://polkadot.network/newsroom/press-releases/tether-tokens-usdt-live-on-polkadot/) since 2022, specifically in the [AssetHub](https://support.polkadot.network/support/solutions/articles/65000181800-what-is-asset-hub-and-how-do-i-use-it-). This integration allows users to transfer USDT from the Polkadot AssetHub to the Darwinia Asset module, enabling them to utilize USDT within the Darwinia ecosystem. The management of USDT within the Darwinia is facilitated by the `pallet-asset` module, which is part of the Substrate ecosystem. This module provides various features for managing tokens, including token transfers, balance tracking, and other related operations.

In order to improve the compatibility of USDT with Ethereum-based tools and workflows, a dedicated precompile has been developed. This precompile acts as a bridge, simplifying the interaction between Ethereum users and USDT. By leveraging this precompile, Ethereum users can seamlessly interact with USDT using their familiar Ethereum tools, such as MetaMask.

## Add to MetaMask

View details about the [USDT Token on Subscan](https://darwinia.subscan.io/erc20_token/0x0000000000000000000000000000000000000403) and add it to MetaMask by clicking its icon.

![precompiles-usdt](../../images/precompiles-usdt.png)

## Contract Info

- The default contract address:  0x0000000000000000000000000000000000000403
- [The interface](https://github.com/darwinia-network/darwinia/blob/main/precompile/metadata/sol/asset.sol)
- [The ABI](https://github.com/darwinia-network/darwinia/blob/main/precompile/metadata/sol/asset.sol)