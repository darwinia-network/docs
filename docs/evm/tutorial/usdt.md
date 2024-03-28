# Overview

Tether (USDT) is a stablecoin widely used in the crypto world. It has been [integrated into the Polkadot network](https://polkadot.network/newsroom/press-releases/tether-tokens-usdt-live-on-polkadot/) since 2022, specifically in the AssetHub. This integration enables users to transfer USDT from the Polkadot AssetHub to the Darwinia Asset module, allowing them to utilize USDT within the Darwinia ecosystem. The management of USDT within Darwinia is facilitated by the `pallet-asset` module, which is part of the Substrate ecosystem. This module provides various features for managing tokens, including token transfers, balance tracking, and other related operations.

This guide will walk you through the general workflow of depositing the USDT token from the AssetHub and the reverse operation of withdrawing the USDT token from Darwinia back to the AssetHub. We will use an example from Pangolin and the AssetHub (Rococo), but this guide also applies to other Darwinia chains like Darwinia and Crab.

# Pangolin <> Rococo(AssetHub) USDT

## Deposit `USDT` to the Pangolin

1. To acquire USDT in the AssetHub, The first step is to deposit USDT tokens from your preferred exchange, such as Bitfinex or Binance. This tutorial does not cover the process of depositing USDT from an exchange, but you can refer to [How to Withdraw USDT from Exchanges on Asset Hub](https://support.polkadot.network/support/solutions/articles/65000181634-how-to-withdraw-usdt-from-bitfinex-on-statemine) for assistance with that step.
2. Before proceeding, please ensure that you have successfully deposited some Tether (USDT) on the Rococo AssetHub with the asset ID 7777. If you are working with the Polkadot AssetHub, please note that the asset ID is 1984.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/a2739a4f-1eb7-4ba9-b2d2-18c34ed5b60d/03ed46e0-4531-4945-a5a6-98ecc1810862/Untitled.png)
    
3. To initiate the transfer of USDT, open the [Darwinia USDT App](https://crosschain-stg.vercel.app/) and enter the transfer amount, sender account, and recipient account. It's important to note that the sender account belongs to the Rococo network, which is a Substrate account, while the recipient account belongs to the Pangolin network, which is an Ethereum-compatible account. Once you have confirmed that all the details are correct, click the `Send` button and wait for the transaction to be completed. After the transaction is complete, you can check the [Pangolin Asset in the Polkadot Apps](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fpangolin-rpc.darwinia.network#/assets), as shown in the screenshot below.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/a2739a4f-1eb7-4ba9-b2d2-18c34ed5b60d/f207b7db-21d9-4146-9edb-47149978e888/Untitled.png)
    
    The USDT token in the Pangolin asset module is named **`ahUSDT`**. This is the specific USDT token that you deposit into the system.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/a2739a4f-1eb7-4ba9-b2d2-18c34ed5b60d/a5f4f73e-a356-4a63-80ad-c24870ef43bc/Untitled.png)
    

## Transfer with MetaMask

After depositing USDT on the Pangolin chain, a precompiled contract [USDT](https://www.notion.so/USDT-1c6dd32ae9f54ed48ab4be289c5eb51c?pvs=21) will allow you to manage USDT assets using an Ethereum-compatible wallet such as Metamask, treating it similarly to an ERC20 token. This means there's no need to familiarize yourself with Substrate transaction tools if you're already accustomed to Ethereum ecosystem tools.

## Withdraw `ahUSDT` to AssetHub

The process of withdrawing USDT is the opposite of the deposit process described above and involves using the [Darwinia USDT App](https://crosschain-stg.vercel.app/). We will not expand further on this topic.