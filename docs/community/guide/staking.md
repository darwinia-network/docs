# Staking Guide

This tutorial will guide you through the process of staking tokens (RING & KTON & Deposit) on Darwinia using the staking Dapp built by the Darwinia Dev Team. The staking Dapp is compatible with the Crab network. Be sure to select Crab network if you want to stake Crab tokens (CRAB & CKTON & Deposit), this tutorial also works; just switch to the appropriate network.

## Get Started With The Dashboard

To get started with the dashboard, navigate to [staking.darwinia.network](https://staking.darwinia.network/#/?network=Darwinia). You’ll be prompted to connect to [MetaMask](https://metamask.io/).

MetaMask will pop up and ask you to sign in. Once signed in, you will be prompted to select the account to connect to the Dapp and accept permissions.

Upon accepting permissions and changing the network to `Darwinia`, you will be redirected to the main dashboard where you’ll find details about the staking data.

## How to Stake

Token holders can delegate a collator candidate by staking tokens and adding to the collator's stake. In return, the collator will share the rewards received from producing blocks amongst all of their delegators. For more information on reward distribution, check out our documentation on [staking reward distribution](https://medium.com/darwinianetwork/faqs-for-darwinia-2-0-staking-mechanism-adjustments-f330b549f168).


To obtain the `Deposit`, you need to lock your `RING` for a certain period of time.

![evm-tutorial-staking-1](../../images/evm-tutorial-staking-1.png)

To stake your tokens, you need to complete two steps. First, you must delegate a collator, and then you need to stake your tokens with them. After these two steps are done, your stake will be in effect.

## Example

For the purpose of staking operations, we will use the following account as an example:

`0x807b496Bd5fa96dC9E22A43577942b2D90Dd7Ccc`

If you click on the `Select a collator` button, the collator menu will open up and you will be able to see data for each of the collators in the active and waiting pools.

![evm-tutorial-staking-2](../../images/evm-tutorial-staking-2.png)
![evm-tutorial-staking-3](../../images/evm-tutorial-staking-3.png)

You can switch between two tabs in the staking interface: `Active Pool` and `Waiting Pool`. The `Active Pool` tab displays collators who are currently producing blocks and earning rewards, while the `Waiting Pool` tab displays collators who are not yet producing blocks or earning rewards.

To begin staking, select a collator by clicking on them. Then, follow these steps:

1. Double-check that you have selected the correct collator and that the address is accurate.
2. Input the amount of tokens you wish to stake. For example, in this scenario, you will be staking 10`RING`, 0.0005`KTON`, and 1`Deposit`.
3. Click the `Stake` button.

When you click `Stake`, a MetaMask pop-up will appear, and you will be asked to sign a transaction.

![evm-tutorial-staking-4](../../images/evm-tutorial-staking-4.png)

Once the transaction has been confirmed and you receive the transaction confirmed notification, the dashboard will update to include the delegation.

![evm-tutorial-staking-5](../../images/evm-tutorial-staking-5.png)

If you check your MetaMask account, you will see that your balance has decreased by the amount of tokens staked (plus gas fees). Please note that it could take a couple of minutes for MetaMask to reflect any changes to the free balance. And you will be able to see the tokens your staked(bonded) tokens on the dashboard.

![evm-tutorial-staking-6](../../images/evm-tutorial-staking-6.png)

## Make Changes To The Delegation

### How to Bond More Funds

1. Click the `+` icon next to the token you want to modify.
2. Specify the amount you would like to increase your delegation by. In this case, we are increasing our bond by 5`RING`.
3. Click `Bond`.

![evm-tutorial-staking-7](../../images/evm-tutorial-staking-7.png)
![evm-tutorial-staking-8](../../images/evm-tutorial-staking-8.png)

### How to Reduce Funds

1. Click on the `–` icon next to the token you want to modify.
2. Enter the amount you would like to reduce your bond by.  In this case, we are reducing our bond by 0.0001`KTON`.
3. Press `Unbond`.

![evm-tutorial-staking-9](../../images/evm-tutorial-staking-9.png)
![evm-tutorial-staking-10](../../images/evm-tutorial-staking-10.png)

You will be prompted to sign a transaction in MetaMask.

Once the transaction has been confirmed and you receive the Transaction confirmed notification, the dashboard will update, and if you hover over the token, it can show you a message that when will the unbonding tokens can be released. At this time, you have the option to cancel this unbonding request or wait 14 days to release the tokens manually.

![evm-tutorial-staking-11](../../images/evm-tutorial-staking-11.png)

Once the 14 days unbonding period has passed, you can return to this staking dashboard and release the unbonded tokens, after which you will see the unbonded funds in your free balance on MetaMask.

### How to Undelegate

Undelegating usually involves two steps: undelegating of the collator and unbonding the tokens that were previously bonded in the stake.
To undelegate, click the `Undelegate` button. This action will take effect immediately. Then, press the `Unbond all` button to unbond the tokens. This will initiate the 14-day unbonding period. After the period is over, you will need to manually release the tokens before they can be transferred.

![evm-tutorial-staking-12](../../images/evm-tutorial-staking-12.png)
![evm-tutorial-staking-13](../../images/evm-tutorial-staking-13.png)

That’s it! Now you’ve successfully delegated a collator, updated the delegation amount, and then removed the delegation. You have all the tools necessary to get started with staking on `Darwinia`!

## Support

If you experience any difficulties with staking, please use the [links](https://t.me/DarwiniaNetwork) below to get in touch with us.