# Token/Asset Bridge

Darwinia cross-chain solution can provide cross-chain messaging services for token bridges and help them realize the transfer of tokens of different standards (such as ERC-20, ERC-721, etc.) between blockchains. For example, [Helix Bridge](https://helixbridge.app/)’s [LN Bridge](https://docs.helixbridge.app/helixbridge/liquidate_node) leverages [Darwinia Msgport](../overview.md) to deliver proofs when LnProvider failed to pay out assets to users.

!!! Quote
    The advantage of using `Darwinia Msgport` is that it is very easy to switch between different low-level message layers without making big changes to the code. — Helix Bridge

## Helix LN Bridge

LN Bridge is a novel token bridge from Helix Bridge. Compared to other traditional token bridges, LN Bridge offers very low cross-chain fees because it only requires actual cross-chain messages in very rare scenarios. The actual cross-chain messages are implemented on `Darwinia Msgport`.

This LN Bridge protocol establishes a liquidity provider role called the **LnProvider** (Liquidity Node Provider). When a user transfers tokens between two chains, the LnProvider receives tokens on one chain and transfers an equivalent amount of tokens to the user on the other chain. 

![msgport-token-bridge-1](../../images/msgport-token-bridge-1.png)

## When cross-chain occur?

In fact, LN Bridge's token cross-chain functionality doesn't require the transmission of actual cross-chain messages. Instead, token cross-chain transfers are handled off-chain by LN Providers, which is the primary reason for its exceptionally low cross-chain fees. Cross-chain messages are only needed to prove the non-functioning of an LN Provider when it fails to perform as expected. The protocol will then use this proof to slash the non-functioning LN Provider. This is because every LN Provider must first register on the protocol and make a collateral.

> The Slasher monitors LnProviders and steps in when they fail, using the messaging channel to apply penalties. The Slasher can receive rewards for its actions.

When a user initiates a cross-chain transfer on LN Bridge and the LnProvider fails to transfer tokens to the user on the target chain, that's when cross-chain messaging comes in.

There are two scenarios:

- If the LnProvider fails to transfer tokens to the user, and **the collateral is on the target chain**.
    
    The user can submit the transfer proof to the target chain through the `Darwinia Msgport`. The target chain combines the proof with evidence that the LnProvider failed to transfer the tokens, and extracts collateral from the LnProvider to compensate the user.
    
- If the LnProvider fails to transfer tokens to the user, and **the collateral is on the source chain**.
    
    The user can use `Darwinia Msgport` to send proof of the failed transfer to the source chain. The source chain can then combine this proof with the original transfer proof to verify the LnProvider's failure. Once the source chain has verified the LnProvider's failure, it can extract collateral from the LnProvider to compensate the user.
    
## Summary

The LN Bridge operates without requiring actual cross-chain messages for token transfers, instead using off-chain handling by Liquidity Node Providers (LnProviders). These providers manage token exchanges between chains, with cross-chain messages only needed if an LnProvider fails to perform. While cross-chain messages are only needed when an LnProvider fails to perform, the security of cross-chain messaging is vital for the reliability of Helix LN Bridge. `Darwinia Msgport` serves as the final guard of the LN Bridge Protocol.