# Migrate Generate Account


!!! info
    This article only covers the migration of general accounts. For guidance on migrating a multisig account, please consult [this tutorial](./multisig-account.md).


This tutorial will walk you through the steps of migrating your accounts from `Darwinia 1.0` to the current Darwinia using the [Account Migration Dapp](https://migration.darwinia.network/#/?network=Darwinia). It's important to note that this tutorial is also applicable for the Crab chain.

## Get Started With The Dashboard

To get started with the dashboard, navigate to [migration.darwinia.network](https://migration.darwinia.network/#/?network=Darwinia). You’ll be prompted to connect to [polkadot{.js} extension](https://polkadot.js.org/extension/), [Talisman wallet](https://www.talisman.xyz/), [Subwallet](https://subwallet.app/), or [NovaWallet](https://novawallet.io/).

![evm-tutorial-migrate-general-1](../../../images/evm-tutorial-migrate-general-1.png)

Upon accepting the permission, you will be directed to the main dashboard where you will find details about the account data to be migrated. You can click on the top right corner to switch accounts for the corresponding migration operation.

![evm-tutorial-migrate-general-2](../../../images/evm-tutorial-migrate-general-2.png)

## How to Migrate

For the purpose of account migration operations, we will use the following account as an example: `2ryX5gyPDyctCfgqGdUknkfBDftpcpSnTP9gtgJGaqdpLiCB`

1. Verify that you selected the account you want to migrate from.
2. Enter the EVM account you would like to migrate to.
    
    !!! note
        Please ensure that you **have the private key** for this EVM account. And this account is not from any third-party platform.
    
    !!! note
        Please confirm that the EVM account you are using is a new address that has not been previously used on Darwinia 1.0. If the account already exists on Darwinia 1.0, don't worry 🤗 - the migrate button will not be clickable and you will receive a prompt indicating that `the EVM account is not free` and that you need to fill in another account.
    
    ![evm-tutorial-migrate-general-3](../../../images/evm-tutorial-migrate-general-3.png)
    
3. Click `Migrate`.

![evm-tutorial-migrate-general-4](../../../images/evm-tutorial-migrate-general-4.png)
![evm-tutorial-migrate-general-5](../../../images/evm-tutorial-migrate-general-5.png)
![evm-tutorial-migrate-general-6](../../../images/evm-tutorial-migrate-general-6.png)

Polkadot{.js} Extension will pop-up and you will be prompted to sign a transaction.

Once the transaction has been confirmed and you receive the transaction confirmed notification, the dashboard will update to include the migration record.

![evm-tutorial-migrate-general-7](../../../images/evm-tutorial-migrate-general-7.png)

That’s it! Now you’ve successfully migrated the account. Please don’t forget to check your account after the migration is complete. 

## Check Your Account After The Migration

### Transferrable

The current version of [Subscan](https://darwinia.subscan.io/) supports Darwinia data queries except staking.

![evm-tutorial-migrate-general-8](../../../images/evm-tutorial-migrate-general-8.png)
![evm-tutorial-migrate-general-9](../../../images/evm-tutorial-migrate-general-9.png)

Also, you can refer to [here](../../../build/getting-started/networks/darwinia.md#network-info) and add the darwinia RPC to your wallet. Then you can see the transferrable `RING` on MetaMask.

![evm-tutorial-migrate-general-10](../../../images/evm-tutorial-migrate-general-10.png)

How about `KTON`? Please add the `KTON` to MetaMask, then you can see the transferrable `KTON`.

```markdown
Symbol: KTON
Spec: ERC20
Decimals: 18
Smart Contract Address: 0x0000000000000000000000000000000000000402
```
![evm-tutorial-migrate-general-11](../../../images/evm-tutorial-migrate-general-11.png)
![evm-tutorial-migrate-general-12](../../../images/evm-tutorial-migrate-general-12.png)

### Bonded & Unbonding & Unbonded & Deposits

Please navigate to [staking.darwinia.network](https://staking.darwinia.network/#/staking?network=Darwinia). You’ll be prompted to connect to [MetaMask](https://metamask.io/).

MetaMask will pop up and ask you to sign in. Once signed in, you will be prompted to select the account to connect to the Dapp and accept permissions.

Upon accepting permissions and changing the network to `Darwinia`, you will be directed to the main dashboard. There, you will find the details of the stake you had on Darwinia 1.0, including Bonded, Unbonding, Unbonded, and Deposits. You can continue to use these to participate in staking on the Darwinia. Please refer to [this tutorial](../staking.md) for instructions on how to stake and earn staking rewards on the Darwinia.

![evm-tutorial-migrate-general-13](../../../images/evm-tutorial-migrate-general-13.png)