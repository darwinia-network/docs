# Order XClearing

Many use cases involve order clearing, such as order book DEXs, swap DEXs, equivalent swap, NFT markets, and more. These use cases can all be extended to cross-chain scenarios. HelixBridge is one such example. It is a third-party token bridge that allows users to perform cross-chain swaps with liquidity relayers, serving as permissionless order takers and makers, essentially facilitating order based cross-chain equivalent swap. 

For example, [Helix Bridge](https://helixbridge.app/) leverages [Msgport](../overview.md) to do settements after users taking orders of liquidity relayer. Msgport can deliver messages indicating that whether liquidity relayer fullfill user's order successfullly or not, where truth of messages are verified by the underlining message protocols Msgport are integrating.

!!! Quote
    The advantage of using `Msgport` is that it is very easy to switch between different low-level message layers without making big changes to the code. — Helix Bridge

## Helix Bridge

Compared to other traditional token bridges, Helix Bridge offers very low cross-chain fees because it only requires actual cross-chain messages in very rare scenarios. The actual cross-chain messages are implemented on `Msgport`.

Helix Bridge protocol establishes a liquidity provider role called the **LnProvider** (Liquidity Node Provider). When a user transfers tokens between two chains, the LnProvider receives tokens on one chain and transfers an equivalent amount of tokens to the user on the other chain. 

![msgport-token-bridge-1](../../images/msgport-token-bridge-1.png)

## When cross-chain occur?

In fact, Helix Bridge's token cross-chain functionality doesn't require the transmission of actual cross-chain messages. Instead, token cross-chain transfers are handled off-chain by liquidity providers, which is the primary reason for its exceptionally low cross-chain fees. Cross-chain messages are only needed to prove the non-functioning of an liquidity provider when it fails to perform as expected. The protocol will then use this proof to slash the non-functioning liquidity provider. This is because every liquidity provider must first register on the protocol and make a collateral.

> The Slasher monitors liquidity provider and steps in when they fail, using the messaging channel to apply penalties. The Slasher can receive rewards for its actions.

When a user initiates a cross-chain transfer on LN Bridge and the LnProvider fails to transfer tokens to the user on the target chain, that's when cross-chain messaging comes in.

There are two scenarios:

- If the liquidity provider fails to transfer tokens to the user, and **the collateral is on the target chain**.
    
    The user can submit the transfer proof to the target chain through the `Darwinia Msgport`. The target chain combines the proof with evidence that the LnProvider failed to transfer the tokens, and extracts collateral from the LnProvider to compensate the user.
    
- If the liquidity provider fails to transfer tokens to the user, and **the collateral is on the source chain**.
    
    The user can use `Msgport` to send proof of the failed transfer to the source chain. The source chain can then combine this proof with the original transfer proof to verify the LnProvider's failure. Once the source chain has verified the liquidity provider's failure, it can extract collateral from the LnProvider to compensate the user.
    
## Summary

Helix Bridge operates without requiring actual cross-chain messages for token transfers, instead using off-chain handling by liquidity providers. These providers manage token exchanges between chains, with cross-chain messages only needed if an liquidity provider fails to perform. While cross-chain messages are only needed when an liquidity provider fails to perform, the security of cross-chain messaging is vital for the reliability of Helix Bridge. `Msgport` serves as the final guard of the Helix Bridge Protocol.

## Reference

[1] https://docs.helixbridge.app/helixbridge/liquidate_node