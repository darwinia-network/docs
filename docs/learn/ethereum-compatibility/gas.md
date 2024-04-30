# Gas Compatibility

One concern for smart contract developers is the gas mechanism. If there is a large gap in gas between Ethereum and the Darwinia platform, it can result in unexpected errors when migrating Ethereum applications to Darwinia. This can be a frustrating experience for dapp builders aiming to create Ethereum-compatible applications on the Darwinia platform. However, we have found a way to minimize the gas gap by keeping the op code gas the same as the Ethereum official implementation. So far, we haven't encountered any EVM code gas compatibility issues in the long run. That being said, there are still some differences between Darwinia and Ethereum in this aspect. This page will provide a detailed explanation of these differences.

## Gas Calculation

As explained above, Darwinia's EVM highly relies on opcode compatibility with the official Ethereum implementation. However, the unique underlying blockchain framework complicates matters. One key concept in the Polkadot relay chain and parachain architecture is "proof size". For parachains, there's a proof size limit of 5M; if exceeded, the relay chain will reject the inclusion of the parachain block, causing the parachain to hang. Considering this limitation, Darwinia's EVM gas calculation incorporates two components: opcode gas, identical to Ethereum's, and proof size cost. The final gas calculation is the greater of these two values. If discrepancies in gas usage are observed during contract interactions compared to Ethereum, this may be the underlying cause. We are actively seeking additional methods to resolve this problem.

## BlockGasLimit Limitation

In Ethereum, the number of pending transactions that can be included in the next block depends on the amount of gas each transaction consumes. When miners create new blocks, the total gas limit of all transactions in the block must be less than the block's gas limit. Since the London hard fork, each block has a target size of 15 million gas units, but the actual size of a block can vary depending on network demand. The maximum size of a block, known as the block gas limit, is set to **30 million** gas units.

Similarly, the Darwinia platform also has a block gas limit that determines the maximum amount of gas that can be consumed in a block. However, the specific block gas limit in Darwinia may be different from that of Ethereum.

| Network | Darwinia | Crab | Pangolin Testnet |
| --- | --- | --- | --- |
| BlockGasLimit | 20 million gas | 20 million gas | 20 million gas  |

**It is important to note that the BlockGasLimit in the Darwinia Platform is lower than the corresponding value in Ethereum.** This means that when building applications on the Darwinia Platform, developers need to be mindful of the lower gas limit and ensure that their code and transactions stay within this limit. Failure to do so may result in transactions being rejected or not being included in blocks. It is recommended to thoroughly test and optimize gas usage in order to ensure the smooth functioning of applications on the Darwinia Platform.

## GasPrice

In Ethereum, there is a concept of a minimum gas price known as the "gas price floor" or "base fee". This base fee is dynamically adjusted for each block based on network congestion. It serves as the minimum amount of Ether (ETH) that users must pay for each unit of gas consumed in a transaction. If you offer a gas price lower than the base fee, your transaction will still be accepted and included in the memory pool, but it may face challenges in being included in a block. Miners prioritize transactions based on their gas prices, with higher gas price transactions being more attractive to miners as they offer higher potential rewards.

In a similar manner, the Darwinia platform implements a gas price mechanism that is similar to Ethereum. However, it's important to note a subtle difference in how transactions with low gas prices are handled. **If you offer a gas price lower than the minimum acceptable gas price set by the Darwinia platform, your transaction will be rejected immediately with an error message stating "gas price too low"**. Unlike in Ethereum, where such transactions are typically placed in the memory pool for future inclusion in blocks, the Darwinia platform immediately rejects transactions with insufficient gas prices. This immediate rejection helps ensure efficient utilization of network resources and prevents transactions with inadequate gas prices from occupying unnecessary space in the memory pool. Therefore, it is crucial to set an appropriate gas price that meets the minimum requirements of the Darwinia platform to avoid immediate rejection of your transactions.