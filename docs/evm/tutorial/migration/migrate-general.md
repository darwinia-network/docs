# Migrate Generate Account

Owner: bear.wang@itering.io

<aside>
🙋‍♂️ This article only covers the migration of general accounts. For guidance on migrating a multisig account, please consult [this tutorial](https://www.notion.so/Migrate-Multisig-Account-2309e46d50d6419ba4c18f58bea890d9?pvs=21).

</aside>

This tutorial will walk you through the steps of migrating your accounts from `Darwinia 1.0` to the current Darwinia using the [Account Migration Dapp](https://migration.darwinia.network/#/?network=Darwinia). It's important to note that this tutorial is also applicable for the Crab chain.

# Get started with the dashboard

To get started with the dashboard, navigate to [migration.darwinia.network](https://migration.darwinia.network/#/?network=Darwinia). You’ll be prompted to connect to [polkadot{.js} extension](https://polkadot.js.org/extension/), [Talisman wallet](https://www.talisman.xyz/), [Subwallet](https://subwallet.app/), or [NovaWallet](https://novawallet.io/).

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled.png)

Upon accepting the permission, you will be directed to the main dashboard where you will find details about the account data to be migrated. You can click on the top right corner to switch accounts for the corresponding migration operation.

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%201.png)

# How to migrate

For the purpose of account migration operations, we will use the following account as an example: `2ryX5gyPDyctCfgqGdUknkfBDftpcpSnTP9gtgJGaqdpLiCB`

1. Verify that you selected the account you want to migrate from.
2. Enter the EVM account you would like to migrate to.
    
    <aside>
    🙋‍♂️ a. Please ensure that you **have the private key** for this EVM account. And this account is not from any third-party platform.
    
    b. Please confirm that the EVM account you are using is a new address that has not been previously used on Darwinia 1.0. If the account already exists on Darwinia 1.0, don't worry 🤗 - the migrate button will not be clickable and you will receive a prompt indicating that `the EVM account is not free` and that you need to fill in another account.
    
    ![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%202.png)
    
    </aside>
    
3. Click `Migrate`.

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%203.png)

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%204.png)

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%205.png)

Polkadot{.js} Extension will pop-up and you will be prompted to sign a transaction.

Once the transaction has been confirmed and you receive the transaction confirmed notification, the dashboard will update to include the migration record.

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%206.png)

That’s it! Now you’ve successfully migrated the account. Please don’t forget to check your account after the migration is complete. 

# Check your account after the migration

## Transferrable

<aside>
💡 The current version of [Subscan](https://darwinia.subscan.io/) supports Darwinia data queries except staking.

</aside>

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%207.png)

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%208.png)

Also, you can click [here](https://www.notion.so/Darwinia-Chain-db787b70edd14545a252122d1c7651d1?pvs=21) and select `Add To MetaMask`, and darwinia RPC will be added automatically. Then you can see the transferrable `RING` on MetaMask.

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%209.png)

How about `KTON`? Please add the `KTON` to MetaMask, then you can see the transferrable `KTON`.

```markdown
Symbol: KTON
Spec: ERC20
Decimals: 18
Smart Contract Address: 0x0000000000000000000000000000000000000402
```

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%2010.png)

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%2011.png)

## Bonded & Unbonding & Unbonded & Deposits

Please navigate to [staking.darwinia.network](https://staking.darwinia.network/#/staking?network=Darwinia). You’ll be prompted to connect to [MetaMask](https://metamask.io/).

MetaMask will pop up and ask you to sign in. Once signed in, you will be prompted to select the account to connect to the Dapp and accept permissions.

Upon accepting permissions and changing the network to `Darwinia`, you will be directed to the main dashboard. There, you will find the details of the stake you had on Darwinia 1.0, including Bonded, Unbonding, Unbonded, and Deposits. You can continue to use these to participate in staking on the Darwinia. Please refer to [this tutorial](https://www.notion.so/Staking-Guide-d7387bfc4d3f4604860651f268ed00ba?pvs=21) for instructions on how to stake and earn staking rewards on the Darwinia.

![Untitled](Migrate%20Generate%20Account%2066167771afba4768b6878907eb4e86bd/Untitled%2012.png)