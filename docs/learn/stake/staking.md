# Staking Module

## Important Parameters

The important parameters to be aware of when understanding the darwinia staking module are as follows:

- `MinStakingDuration` - *Minimum time to stake at least.*
- `MaxDeposits` - *Maximum deposit count.*
- `MaxUnstakings` - *Maximum unstaking/unbonding count.*

## **Parameters In The Networks**

|  | Darwinia | Crab | Pangolin Testnet |
| --- | --- | --- | --- |
| MinStakingDuration | 14 days | 14 days | 2 mins |
| MaxDeposits | 100 | 512 | 512 |
| MaxUnstakings | 16 | 16 | 16 |

## Extrinsic API Documentation

- `stake(ring_amount: Balance, kton_amount: Balance, deposits: Vec<DepositId<T>>)`
    - Add stakes to the staking pool. This will transfer the stakes to a pallet/contact account.
    - Params:
        - `ring_amount`: the amount of RING to be staked.
        - `kton_amount`: the amount of KTON to be staked.
        - `deposits`: a vector of specific deposits that you want to add to the staking pool.
- `unstake(ring_amount: Balance, kton_amount: Balance, deposits: Vec<DepositId<T>>)`
    - Withdraw stakes from the staking pool.
    - Params:
        - `ring_amount`: the amount of RING to be withdrawn.
        - `kton_amount`: the amount of KTON to be withdrawn.
        - `deposits`: a vector of specific deposits that you want to withdraw from the staking pool.
- `restake(ring_amount: Balance, kton_amount: Balance, deposits: Vec<DepositId<T>>)`
    - Cancel the `unstake` operation. Re-stake the unstaking assets immediately.
    - Params:
        - `ring_amount`: the amount of RING to be restaked.
        - `kton_amount`: the amount of KTON to be restaked.
        - `deposits`: a vector of specific deposits that you want to restake immediately.
- `claim`:
    - claim the stakes from the pallet/contract account.
- `collect(commission: Perbill)`
    
    !!! note
        Please note that the staking commission design on the Darwinia network differ significantly from the Polkadot. See [DIP-1](https://dips.darwinia.network/DIPs/dip-1.html) for details.
    
    - Declare the desire to collect. Effects will be felt at the beginning of the next session.
    - Params:
        - `commission`: the proportion of the staking reward that you want to collect, represented as a perbill (a fraction of a billion).
- `nominate(target: T::AccountId)`
    - Declare the desire to nominate a collator. Effects will be felt at the beginning of the next session.
    - Params:
        - `target`: the account ID of the collator you wish to nominate.
- `chill`
    - Declare no desire to either collect or nominate. Effects will be felt at the beginning of the next era. If the target is a collator, its nominators need to re-nominate.
- `set_collator_count(count: u32)`
    - Set collator count. This will apply to the incoming session. Require root origin.
    - Params:
        - `count`: the number of collators you want to set for the upcoming session.