# Governance

Currently, Darwinia employs OpenGov for governance. For more details on how it functions, please consult the Polkadot official [WIKI](https://wiki.polkadot.network/docs/learn-polkadot-opengov-index).

Darwinia plans to transition from OpenGov to Tally in the future.

Check out the [tutorial](../community/guide/governance.md).

## Parameters

|     Origin/Track     |                      Usage                      | Prepare  Period | Decision Period | Confirm Period | Min Enactment Period |
| :------------------: | :---------------------------------------------: | :-------------: | :-------------: | :------------: | :------------------: |
|         Root         |                 Any root call.                  |     3 days      |     28 days     |     4 days     |        1 day         |
|  Whitelisted Caller  |   Authorized to dispatch a whitelisted call.    |     10 mins     |     28 days     |    10 mins     |       30 mins        |
|    General Admin     |      General administrative capabilities.       |     3 days      |     28 days     |     4 days     |        1 day         |
| Referendum Canceller |         Authorized to cancel referenda.         |     1 hour      |     28 days     |    3 hours     |       10 mins        |
|  Referendum Killer   |          Authorized to kill referenda.          |     1 hour      |     28 days     |    3 hours     |       10 mins        |
|    Medium Spender    | Can spend up to **4M** RING from the treasury.  |     4 hours     |     28 days     |     1 day      |        1 day         |
|     Big Spender      | Can spend up to **20M** RING from the treasury. |     4 hours     |     28 days     |     2 days     |        1 day         |
