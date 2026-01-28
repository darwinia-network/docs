# Overview


[Precompiles Contracts](https://www.evm.codes/precompiled?fork=shanghai) in Ethereum are built-in contracts that offer specific functionalities. They are implemented within the Ethereum Virtual Machine (EVM) and can be executed by sending a transaction to their unique addresses. Typically, precompiles are utilized for computationally expensive operations like cryptographic functions (e.g., SHA-256, elliptic curve operations) and modular exponentiation. These precompiles are optimized and often more efficient than implementing the same functionalities in Solidity or other smart contract languages.

Darwinia strives to achieve compatibility with Ethereum, which includes being RPC compatible. Additionally, compatibility with Ethereum precompiles is also important. All Darwinia networks have integrated the standard Ethereum precompiles, making it easier for existing Ethereum applications to transition to the Darwinia network without any modifications. In addition to the standard precompiles, Darwinia has also installed other precompiles such as `StateStorage`, `Dispatch`. considering the unique architecture of Darwinia chains. This chapter will guide you through the design and usage of precompile contracts in Darwinia.

## Precompiles In Darwinia

Darwinia exposes the following precompiles to help developers build Ethereum-compatible applications without extra boilerplate.

### Darwinia Network

| Precompile Address | Name |
| --- | --- |
| `0x0000000000000000000000000000000000000001 ~ 0x0000000000000000000000000000000000000009` | [Ethereum](../precompiles/ethereum.md) |
| `0x0000000000000000000000000000000000000400` | [StateStorage](../precompiles/state-storage.md) |
| `0x0000000000000000000000000000000000000401` | [Dispatch](../precompiles/dispatch.md) |
| `0x0000000000000000000000000000000000000402` | [Commitment Token](../precompiles/commitment-token.md) |
| `0x0000000000000000000000000000000000000403` | [USDT](../precompiles/usdt.md) |
| `0x0000000000000000000000000000000000000404` | [PINK](../precompiles/pink.md) |
