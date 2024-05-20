To enable a software application to interact with the blockchain, JSON RPC is the preferred method. Darwinia provides an [Ethereum-compatible JSON RPC endpoint](../../build/getting-started/networks/darwinia.md#network-info), allowing developers to seamlessly interact with the Darwinia node just as they would with [Ethereum API](https://ethereum.github.io/execution-apis/api-documentation). While these APIs strive for high compatibility with Ethereum, it's important to acknowledge that there may be variations, particularly in relation to the consensus mechanism. The details of these differences will be explained in the accompanying guide.

!!! note
    ✅ means the method is fully compatible with the Ethereum, and ❌ means it is not.

## Supported API Methods

### [eth_protocolVersion](https://docs.alchemy.com/reference/eth-protocolversion) ❌

- Returns the current Ethereum protocol version.
- **Compatible Issue: returns `1` by default.**

### [eth_submitHashrate](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_submithashrate)  ❌

- Used for submitting mining hashrate.
- **Compatible Issue: returns `"0x0"` by default**

### [eth_submitWork](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_submitwork) ❌

- Used for submitting a proof-of-work solution.
- **Compatible Issue: returns `false` by default.**

### [eth_getWork](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getwork) ❌

- Returns the hash of the current block, the seedHash, and the boundary condition to be met ("target").
- **Compatible Issue: returns `null` by default**

### [eth_mining](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_mining) ❌

- Returns `true` if client is actively mining new blocks.
- **Compatible Issue: returns `false` by default**

### [eth_hashrate](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_hashrate) ❌

- Returns the number of hashes per second that the node is mining with.
- **Compatible Issue: returns `false` by default.**

### [eth_getUncleByBlockHashAndIndex](https://docs.alchemy.com/reference/eth-getunclebyblockhashandindex) ❌

- Returns information about a uncle of a block by hash and uncle index position.
- **Compatible Issue: returns `null` by default**

### [eth_getUncleByBlockNumberAndIndex](https://docs.alchemy.com/reference/eth-getunclebyblocknumberandindex) ❌

- Returns information about a uncle of a block by number and uncle index position.
- **Compatible Issue: returns `null` by default**

### [eth_getUncleCountByBlockHash](https://docs.alchemy.com/reference/eth-getunclecountbyblockhash) ❌

- Returns the number of uncles in a block from a block matching the given block hash.
- **Compatible Issue: returns `null` by default**

### [eth_getUncleCountByBlockNumber](https://docs.alchemy.com/reference/eth-getunclecountbyblocknumber) ❌

- Returns the number of uncles in a block from a block matching the given block number.
- **Compatible Issue: returns `null` by default**

### [eth_accounts](https://docs.alchemy.com/reference/eth-accounts) ✅

- Returns a list of addresses owned by client.

### [eth_blockNumber](https://docs.alchemy.com/reference/eth-blocknumber) ✅

- Returns the number of most recent block.

### [eth_call](https://docs.alchemy.com/reference/eth-call) ✅

- Executes a new message call immediately without creating a transaction on the block chain.

### [eth_chainId](https://docs.alchemy.com/reference/eth-chainid) ✅

- Returns the chain ID used for signing replay-protected transactions.

### [eth_coinbase](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_coinbase) ✅

- Returns the latest block author.

### [eth_estimateGas](https://docs.alchemy.com/reference/eth-estimategas) ✅

- Generates and returns an estimate of how much gas is necessary to allow the transaction to complete. The transaction will not be added to the blockchain. Note that the estimate may be significantly more than the amount of gas actually used by the transaction, for a variety of reasons including EVM mechanics and node performance.

### [eth_feeHistory](https://docs.alchemy.com/reference/eth-feehistory) ✅

- Returns a collection of historical gas information from which you can decide what to submit as your `maxFeePerGas` and/or `maxPriorityFeePerGas`. This method was introduced with [EIP 1559](https://blog.alchemy.com/blog/eip-1559).

### [eth_gasPrice](https://docs.alchemy.com/reference/eth-gasprice) ✅

- Returns the current price per gas in wei.

### [eth_maxPriorityFeePerGas](https://docs.alchemy.com/reference/eth-maxpriorityfeepergas) ✅

- Generally you will use the value returned from this method to set the `maxFeePerGas` in a subsequent transaction that you are submitting. This method was introduced with [EIP 1559](https://blog.alchemy.com/blog/eip-1559).

### [eth_sendRawTransaction](https://docs.alchemy.com/reference/eth-sendrawtransaction) ✅

- Creates new message call transaction or a contract creation for signed transactions.

### [eth_sendTransaction](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_sendtransaction) ✅

- Creates new message call transaction or a contract creation, if the data field contains code.

### [eth_getBalance](https://docs.alchemy.com/reference/eth-getbalance) ✅

- Returns the balance of the account of given address.

### [eth_getBlockByHash](https://docs.alchemy.com/reference/eth-getblockbyhash) ✅

- Returns information about a block by hash.

### [eth_getBlockByNumber](https://docs.alchemy.com/reference/eth-getblockbynumber) ✅

- Returns information about a block by block number.

### [eth_getBlockTransactionCountByHash](https://docs.alchemy.com/reference/eth-getblocktransactioncountbyhash) ✅

- Returns the number of transactions in a block from a block matching the given block hash.

### [eth_getBlockTransactionCountByNumber](https://docs.alchemy.com/reference/eth-getblocktransactioncountbynumber) ✅

- Returns the number of transactions in a block matching the given block number.

### [eth_getCode](https://docs.alchemy.com/reference/eth-getcode) ✅

- Returns code at a given address.

### [eth_getStorageAt](https://docs.alchemy.com/reference/eth-getstorageat) ✅

- Returns the value from a storage position at a given address.

### [eth_getTransactionByBlockHashAndIndex](https://docs.alchemy.com/reference/eth-gettransactionbyblockhashandindex) ✅

- Returns information about a transaction by block hash and transaction index position.

### [eth_getTransactionByBlockNumberAndIndex](https://docs.alchemy.com/reference/eth-gettransactionbyblocknumberandindex) ✅

- Returns information about a transaction by block number and transaction index position.

### [eth_getTransactionByHash](https://docs.alchemy.com/reference/eth-gettransactionbyhash) ✅

- Returns the information about a transaction requested by transaction hash.

### [eth_getTransactionCount](https://docs.alchemy.com/reference/eth-gettransactioncount) ✅

- Returns the number of transactions *sent* from an address.

### [eth_getTransactionReceipt](https://docs.alchemy.com/reference/eth-gettransactionreceipt) ✅

- Returns the receipt of a transaction by transaction hash.

### [eth_newFilter](https://docs.alchemy.com/reference/eth-newfilter) ✅

- Creates a filter object, based on filter options, to notify when the state changes (logs). To check if the state has changed, call [eth_getFilterChanges](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getfilterchanges).

### [eth_newBlockFilter](https://docs.alchemy.com/reference/eth-newblockfilter) ✅

- Creates a filter in the node, to notify when a new block arrives. To check if the state has changed, call [eth_getFilterChanges](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getfilterchanges).

### [eth_newPendingTransactionFilter](https://docs.alchemy.com/reference/eth-newpendingtransactionfilter) ✅

- Creates a filter in the node, to notify when new pending transactions arrive. To check if the state has changed, call [eth_getFilterChanges](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getfilterchanges).

### [eth_getLogs](https://docs.alchemy.com/reference/eth-getlogs) ✅

- Returns an array of all logs matching a given filter object.

### [eth_getFilterLogs](https://docs.alchemy.com/reference/eth-getfilterlogs) ✅

- Returns an array of all logs matching a given filter object.

### [eth_getFilterChanges](https://docs.alchemy.com/reference/eth-getfilterchanges) ✅

- Polling method for a filter, which returns an array of logs which occurred since last poll.

### [eth_uninstallFilter](https://docs.alchemy.com/reference/eth-uninstallfilter) ✅

- Uninstalls a filter with given id. Should always be called when watch is no longer needed. Additionally Filters timeout when they aren't requested with [eth_getFilterChanges](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getfilterchanges) for a period of time.

### [eth_subscribe](https://docs.alchemy.com/reference/eth-subscribe) ✅

- Creates a new subscription for desired events. Sends data as soon as it occurs.

### [eth_unsubscribe](https://docs.alchemy.com/reference/eth-unsubscribe) ✅

- cancels the subscription given by its ID

### [eth_syncing](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_syncing) ✅

- Returns an object with data about the sync status or `false`.

### [web3_clientVersion](https://docs.alchemy.com/reference/web3-clientversion) ✅

- Returns the current client version.

### [web3_sha3](https://docs.alchemy.com/reference/web3-sha3) ✅

- Returns Keccak-256 (*not* the standardized SHA3-256) of the given data.

### [txpool_content](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-txpool#txpool-content) ✅

- List the exact details of all the transactions currently pending for inclusion in the next block(s), as well as the ones that are being scheduled for future execution only.

### [txpool_inspect](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-txpool#txpool-inspect) ✅

- List a textual summary of all the transactions currently pending for inclusion in the next block(s), as well as the ones that are being scheduled for future execution only.

### [txpool_status](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-txpool#txpool-status) ✅

- For the number of transactions currently pending for inclusion in the next block(s), as well as the ones that are being scheduled for future execution only.

### [debug_traceBlockByNumber](https://docs.alchemy.com/reference/debug-traceblockbynumber) ✅

- Replays the block that matching the given block number.
- **Note: Only accessible on the [EVM-tracing node](https://www.notion.so/EVM-Tracing-fda4666e09d84c18aa6404e6de9ced3a?pvs=21).**

### [debug_traceBlockByHash](https://docs.alchemy.com/reference/debug-traceblockbyhash) ✅

- Replays the block that matching the given block hash.
- **Note: Only accessible on the [EVM-tracing node](https://www.notion.so/EVM-Tracing-fda4666e09d84c18aa6404e6de9ced3a?pvs=21).**

### [debug_traceTransaction](https://docs.alchemy.com/reference/debug-tracetransaction) ✅

- Attempts to run the transaction in the exact same manner as it was executed on the network. It will replay any transaction that may have been executed prior to this one before it and will then attempt to execute the transaction that corresponds to the given hash.
- **Note: Only accessible on the [EVM-tracing node.](https://www.notion.so/EVM-Tracing-fda4666e09d84c18aa6404e6de9ced3a?pvs=21)**

### [trace_filter](https://docs.alchemy.com/reference/trace-filter) ✅

- Returns traces matching given filter.
- **Note: Only accessible on the [EVM-tracing node](https://www.notion.so/EVM-Tracing-fda4666e09d84c18aa6404e6de9ced3a?pvs=21).**