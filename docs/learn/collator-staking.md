# Overview

This section provides an overview of the collator staking system on Darwinia.

## What is Collator?

For Ethereum-based chains, the node validator (previously referred to as a miner before the Merge) plays a dual role: not only is it responsible for producing new blocks, but it also maintains the security of the chain by communicating with other peers and performing validations to advance the consensus process. 

In contrast, for Polkadot parachains, block production and chain security are separate responsibilities. The security of the parachain's consensus is managed by Polkadot, while a distinct role called a collator is responsible for accepting transactions and producing new blocks.

If you're interested in learning more about collators, you can find additional information in the [Collator section of the Polkadot Wiki](https://wiki.polkadot.network/docs/learn-collator).

## How to Staking?

!!! note
    Following the implementation of DIP-7, the staking system was rewritten as a set of smart contracts, replacing the Substrate pallet. For more information on the reasoning behind this change, please refer to the [DIP-7 specification](https://dips.darwinia.network/DIPs/dip-7.html).

The staking system has two types:

1. Direct RING token staking: This is the most straightforward way to stake, and the reward you receive is based on the amount of tokens you stake.
2. Deposit-based staking: By depositing RING tokens, you can receive a bonus in the form of [KTON](../community/orgs/ktondao.md) tokens. Additionally, the deposited tokens can be considered part of the amount you staked, allowing you to receive more rewards.

Once you have obtained RING tokens, you can choose to either stake them directly or deposit them to receive KTON tokens following the steps outlined in the [Staking Guide](https://ringdao.notion.site/How-to-stake-and-earn-staking-rewards-fffaad1d671e81409a42c8244bf671bd).

## Become a Collator

Currently, the Darwinia chains have a fixed number of collators (N), which means only the top N collators are selected to produce blocks for the network. The more `RING` tokens you stake, the higher your chances of becoming a collator. If you don't have enough `RING` tokens, you can still participate in staking by nominating (delegating) your `RING` tokens to other collators and earning a portion of the block production rewards. Refer to the [Collator Node Guide](../node-operators/run-collator-node.md) for detailed operation instructions.