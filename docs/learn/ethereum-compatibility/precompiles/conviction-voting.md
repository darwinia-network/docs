

# Conviction Voting Precompile

The governance structure of Darwinia has been undergoing a transformation, initially modeled after [Polkadot Governance V1](https://wiki.polkadot.network/docs/learn-governance) and now advancing towards [Polkadot's OpenGov](https://wiki.polkadot.network/docs/learn-polkadot-opengov-index) framework. For a detailed comparison between the two governance models, please visit Polkadot OpenGov: [Gov1 vs Polkadot OpenGov](https://wiki.polkadot.network/docs/learn-polkadot-opengov#gov1-vs-polkadot-opengov). The article provides an in-depth analysis of the distinctions and the rationale behind Darwinia's transition to Polkadot OpenGov. Central to the OpenGov model is the concept of conviction voting, which is implemented via the `pallet-conviction-vote` module in Substrate. This module is critical as it encompasses key governance functions such as proposing votes and retracting them. Furthermore, the ConvictionVoting precompile allows Ethereum users to seamlessly engage with the governance processes of the Darwinia network as part of their daily activities.

## Contract Info

- The default contract address:  0x0000000000000000000000000000000000000602
- [The interface](https://github.com/darwinia-network/darwinia/blob/main/precompile/metadata/sol/conviction-voting.sol)
- [The ABI](https://github.com/darwinia-network/darwinia/blob/main/precompile/metadata/abi/conviction-voting.json)