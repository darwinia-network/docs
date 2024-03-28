# Glossary

## Block

A collection of data, such as transactions, that together indicate a state transition of the blockchain.

## Block Explorer

An application that allows a user to explore the different blocks on a blockchain.

## Collator

A node that maintains a parachain by collecting parachain transactions and producing state transition proofs for the validators.

## Commission

Collators and nominators get paid from block production on the network, where collators can set a variable commission rate, which is initially subtracted from the total rewards that collator is entitled to (for that period), where the commission determines the rate of distribution for the remaining rewards set out for the nominators that are backing that collator.

## Dapps

A generic term for a decentralized application, that is, one that runs as part of a distributed network as opposed to being run on a specific system or set of systems.

## Epoch

An epoch is a time duration in the BABE protocol that is broken into smaller time slots. Each slot has at least one slot leader who has the right to propose a block. In Kusama, it is the same duration as a [session](https://www.notion.so/Glossary-8967fc4aa6a046a69b525dff7bf70a50?pvs=21).

## Era

A (whole) number of sessions, which is the period that the validator set (and each validator's active nominator set) is recalculated and where rewards are paid out.

## Parachain

A blockchain that meets several characteristics that allow it to work within the confines of the Polkadot Host. Also known as "parallelized chain.”

## Power

Users participate in staking, and the rights and interests obtained by bonding RING or KTON are called power.

## Power Share

Power share is the percentage of Power held in total Power. The greater the power share, the greater the influence of the decision made on the entire chain.

## Preimage

The on-chain proposals do not require the entire image of extrinsics and data (for instance the WASM code, in case of upgrades) to be submitted, but would rather just need that image's hash. That preimage can be submitted and stored on-chain against the hash later, upon the proposal's
dispatch.

## Relay Chain

The chain that coordinates consensus and communication between parachains (and external chains, via bridges).

## Session

A session is a period of time that has a constant set of validators. Validators can only join or exit the validator set at a session change. It is measured in block numbers. 

## Session key

A session key is actually several keys kept together that provide the various signing functions required by network authorities/validators in pursuit of their duties.

## Substrate

A modular framework for building blockchains. Darwinia network is built with Substrate.