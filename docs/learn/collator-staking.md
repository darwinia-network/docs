# Overview


## What is Collator?

For Ethereum-based chains, the node validator (called miner before the Merge) is not only response for produce new blocks, but also maintaining the security of the chain by communicate with other peers and perform validation to move the consensus process forward.
For the parachains of the Polkadot, the block production and chain security is separated. The parachain's chain consensus security is 
managed by the Polkadot, there is another role called collator, which is responsible for accepting transaction and producing new blocks.
If you want to learn more about the Collator, check out the [Collator in Polkadot Wiki](https://wiki.polkadot.network/docs/learn-collator).

## Collator Staking

The first step to become a collator is to stake RING tokens in the [Collator Staking App](https://collator-staking.darwinia.network/).
The darwinia chains currently have a fixed number of collators N, that means only the top N collators can be chosen to produce blocks for the networks. The more RING token you staked, the more possibility to become a collator. If you currently don't have enough RING tokens,
you can also participate the staking by nominating(delegating) RING tokens to other collators and get some rewards from the block produce reward. Following the [Staking Guide](../community/guide/staking.md) to finish this step.

Once the staking is done, next is running the chain nodes in your prepared machine. See the operation guide in the [Collator Node Guide](../node-operators/run-collator-node.md).

## Staking Design

