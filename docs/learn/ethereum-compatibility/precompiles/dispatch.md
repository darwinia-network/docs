# Dispatch Precompile

Before diving into understanding this precompile, it's important to explore the [StateStorage precompile](./state-storage.md). The StateStorage precompile is a versatile design that enables reading any storage element as long as the storage key matches. It provides flexibility in accessing and retrieving specific data from the substrate storage. Taking it a step further, we have also introduced the `Dispatch` precompile. This precompile allows you to execute a substrate basic executable call within the EVM environment. It offers a unique capability not found in the Ethereum system. By providing a specific encoded substrate call along with the Ethereum transaction, the dispatch precompile first validates the call. If the validation is successful, the call is internally dispatched within the Darwinia node.

This remarkable experience allows for seamless integration and execution of substrate functionality within the Darwinia ecosystem. It opens up new possibilities for interoperability and cross-chain interactions, enabling developers to leverage the best of both substrate and Ethereum worlds.

## Contract Info

- The default contract address:  0x0000000000000000000000000000000000000401
- The API:
    - Input:
        - `bytes`: The scale encoded substrate dispatch call
    - Output:
        - Returns an empty array on success, otherwise, an error.