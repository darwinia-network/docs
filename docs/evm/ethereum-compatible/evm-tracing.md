The EVM Tracing API allows users to analyze the execution details of the Ethereum Virtual Machine during specific transactions. It is particularly useful for contract executions, as it provides insights into code execution, data modifications, and interactions with other contracts and accounts.

Both Ethereum clients, such as Geth and OpenEthereum, offer comprehensive EVM tracing and debugging APIs. Darwinia is striving for compatibility with Ethereum and has provided a set of useful EVM tracing APIs to facilitate application development. The currently supported Darwinia EVM tracing APIs include:

- [debug_traceBlockByNumber](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#debugtraceblockbynumber)
- [debug_traceBlockByHash](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#debugtraceblockbyhash)
- [debug_traceTransaction](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#debugtracetransaction)
- [trace_filter](https://docs.alchemy.com/reference/trace-filter)

These APIs enable developers to examine and analyze the execution details of the Ethereum Virtual Machine within the Darwinia ecosystem.

## The Underlying Technology

<aside>
💡 The PureStake team has made significant contributions to the Polkadot ecosystem by introducing tracing capabilities comparable to those of Geth and OpenEthereum. Building on this progress, Darwinia Network has adopted a similar approach for EVM tracing within the Darwinia ecosystem. This decision was based on the fact that it currently represents the most effective solution available for Polkadot.

</aside>

It is worth noting that the EVM tracing features in Darwinia are specifically provided by a dedicated type of node. This design decision is made to ensure that the tracing feature is only enabled when needed, avoiding unnecessary overhead for production nodes.

The EVM tracing node in Darwinia has its own distinct binary and requires a separate setup command compared to the production node. For more detailed information on running an EVM tracing node, please refer to the [Run Evm Trace Node](https://www.notion.so/Run-Evm-Trace-Node-aa2c475828534901ae49261e946e859e?pvs=21).

To utilize the EVM tracing features in Darwinia, users should send requests to the dedicated node's RPC endpoint, which can be found in the corresponding [Network Info](https://www.notion.so/Darwinia-Chain-db787b70edd14545a252122d1c7651d1?pvs=21). This ensures that the tracing capabilities are utilized effectively and efficiently within the Darwinia ecosystem.