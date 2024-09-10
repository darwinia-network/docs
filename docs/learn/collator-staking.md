# Overview


## What is Collator?

For Ethereum-based chains, the node validator (previously referred to as a miner before the Merge) plays a dual role: not only is it responsible for producing new blocks, but it also maintains the security of the chain by communicating with other peers and performing validations to advance the consensus process. 

In contrast, for Polkadot parachains, block production and chain security are separate responsibilities. The security of the parachain's consensus is managed by Polkadot, while a distinct role called a collator is responsible for accepting transactions and producing new blocks.

If you're interested in learning more about collators, you can find additional information in the [Collator section of the Polkadot Wiki](https://wiki.polkadot.network/docs/learn-collator).

## Become a Collator

To become a collator, the first step is to stake RING tokens using the [Collator Staking App](https://collator-staking.darwinia.network/). Currently, the Darwinia chains have a fixed number of collators (N), which means only the top N collators are selected to produce blocks for the network. The more RING tokens you stake, the higher your chances of becoming a collator. If you don't have enough RING tokens, you can still participate in staking by nominating (delegating) your RING tokens to other collators and earning a portion of the block production rewards. Follow the [Staking Guide](../community/guide/staking.md) to complete this step.

Once you've finished staking, the next step is to set up and run the chain nodes on your machine. Refer to the [Collator Node Guide](../node-operators/run-collator-node.md) for detailed operation instructions.

## Collator Staking Design

!!! note
    Following the implementation of DIP-7, the staking system was rewritten as a set of smart contracts, replacing the Substrate pallet. For more information on the reasoning behind this change, please refer to the [DIP-7 specification](https://dips.darwinia.network/DIPs/dip-7.html).

The staking system has two types:

1. Direct RING token staking: This is the most straightforward way to stake, and the reward you receive is based on the amount of tokens you stake.
2. Deposit-based staking: By depositing RING tokens, you can receive a bonus in the form of [KTON](../community/orgs/ktondao.md) tokens. Additionally, the deposited tokens can be considered part of the amount you staked, allowing you to receive more rewards.