# Overview
Collator staking involves participants locking up their RING tokens to support the network’s operations and security through a nomination mechanism. In this system, users can participate either as nominators or collators to help the chain's liveness, earning rewards in return. To get started with the DApp, visit[Collator Staking](https://collator-staking.darwinia.network/) is used to 


## Development

If you want to learn how to interact with these Collator Staking Precompile contracts, pleast vist the [precompile detail page](./ethereum-compatibility/precompiles/staking.md), be aware that this contract may be deprecated in future versions.

The parameters to be aware of when understanding the darwinia staking module are as follows:

- `MinStakingDuration` - *Minimum time to stake at least.*
- `MaxDeposits` - *Maximum deposit count.*
- `MaxUnstakings` - *Maximum unstaking/unbonding count.*

### **Parameters In The Networks**

|  | Darwinia | Crab | Pangolin Testnet |
| --- | --- | --- | --- |
| MinStakingDuration | 14 days | 14 days | 2 mins |
| MaxDeposits | 100 | 512 | 512 |
| MaxUnstakings | 16 | 16 | 16 |