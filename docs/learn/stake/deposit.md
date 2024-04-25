# Deposit Module

## Important Parameters

The important parameters to be aware of when understanding the darwinia deposit module are as follows:

- `MinLockingAmount` - *Minimum amount to lock at least.*

## Parameters In The Networks

|  | Darwinia | Crab | Pangolin Testnet |
| --- | --- | --- | --- |
| MinLockingAmount | 1 RING | 1 CRAB | 1 PRING |

## Extrinsic API Documentation

- `lock(amount: Balance, months: u8)`
    - Lock *RING* for some *KTON* profit/interest.
    - Params:
        - `amount` : the quantity to be locked.
        - `months` : the duration for which the amount is to be locked.
- `claim()`
    - Claim the expired-locked *RING*.
- `claim_with_penalty(deposit_id: DepositId)`
    - Claim the unexpired-locked *RING* by paying the *KTON* penalty.
    - Params:
        - `deposit_id`: the specific deposit that you intend to claim.