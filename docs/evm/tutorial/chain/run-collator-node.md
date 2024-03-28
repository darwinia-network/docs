# Run Collator Node

Owner: Darwinia

<aside>
👉🏻 Familiarity with Linux/Mac command line is essential.

</aside>

# Overview

Darwinia Collators play a crucial role in the Darwinia Network as they are responsible for block production and ensuring block liveness. These Collators collect transactions from users on the parachain and generate state transition proofs for Relay Chain validators. In essence, they provide blocks to validators on the relay chain for finalization.

To learn more about Collators and their functions, you can click [here](https://wiki.polkadot.network/docs/learn-collator). This resource will provide you with detailed information on the topic.

<aside>
👉🏻 The steps outlined below are based on Darwinia, and the steps for Crab are similar.

</aside>

# Run Collator Node

### Recommended Hardware

- **RAM:**  8 GB:
- **Storage(SSD)**: 800 GB

### Download Snapshot

It's important to note that there is a faster method to expedite the syncing process**.** You can achieve this by downloading the snapshot blockchain data and moving it to the current node database location and greatly speeding up the node sync process. Click [here](https://www.notion.so/Chain-Database-Snapshot-f0f695e8d4444cf69e1c8dac51d49558?pvs=21) for more detailed instructions.

### Start The Collator Node

1. Open a terminal shell on your computer
2. Create a work dirctory
    
    Let's create a directory called `run-collator-node` to store everything needed for setting up an collator node, including the downloaded node binary and the chain database.
    
    ```bash
    mkdir run-collator-node && cd run-collator-node
    ```
    
3. Download and decompress the binary.
    
    As of the time of writing this doc(2023-09-04), the latest version of the Darwinia node is `v6.4.0`. Please ensure that you check for [the latest version](https://github.com/darwinia-network/darwinia/releases) when running your own node. 
    
    ```bash
    wget [https://github.com/darwinia-network/darwinia/releases/download/v6.4.0/darwinia-x86_64-linux-gnu.tar.bz2](https://github.com/darwinia-network/darwinia/releases/download/v6.3.4/darwinia-x86_64-linux-gnu.tar.bz2)
    tar xvf darwinia-x86_64-linux-gnu.tar.bz2
    ```
    
4. Start the node by running the following command:
    
    ```bash
    ./darwinia --chain darwinia --base-path /data/darwinia-collator --frontier-backend-type sql --collator
    ```
    
5. Verify your node is up and running successfully by reviewing the output displayed in the terminal. The terminal should display output similar to this:
    
    ```bash
    Loading genesis from `/home/bear/coding/rust-space/test-docs/run-collator-node/darwinia2.json`
    2023-10-16 16:14:20 Darwinia    
    2023-10-16 16:14:20 ✌️  version 6.4.0-2f0941d6f2a    
    2023-10-16 16:14:20 ❤️  by Darwinia Network <hello@darwinia.network>, 2018-2023    
    2023-10-16 16:14:20 📋 Chain specification: Darwinia2    
    2023-10-16 16:14:20 🏷  Node name: adventurous-throne-2027    
    2023-10-16 16:14:20 👤 Role: AUTHORITY    
    2023-10-16 16:14:20 💾 Database: RocksDb at /data/darwinia-collator/chains/darwinia2/db/full    
    2023-10-16 16:14:20 ⛓  Native runtime: Darwinia2-6400 (DarwiniaOfficialRust-0.tx0.au0)    
    2023-10-16 16:14:21 Parachain id: Id(2046)    
    2023-10-16 16:14:21 Parachain Account: 2qiDxtPxw1BsbLwujRn5Q2352CaDPY8UMZi4iHBfPXo6FgHd    
    2023-10-16 16:14:21 Parachain genesis state: 0x000000000000000000000000000000000000000000000000000000000000000000de42f41f451c1be24559be5f93ed0a74f2b6a65d0c965fec4647e165d1947b7103170a2e7597b7b7e3d84c05391d139a62b157e78786d8c082f29dcf4c11131400    
    2023-10-16 16:14:21 Is collating: yes    
    2023-10-16 16:14:23 [Parachain] 📑 Connection configuration: SqliteBackendConfig { path: "/data/darwinia-collator/chains/darwinia2/sql/frontier.db3", create_if_missing: true, thread_count: 4, cache_size: 209715200 }    
    2023-10-16 16:14:25 [Relaychain] 🏷  Local node identity is: 12D3KooWJXgiE8JJSv6fCiEmkEjGAewNYh2HPCSJZuKMZrJUwWrR    
    2023-10-16 16:14:25 [Relaychain] 💻 Operating system: linux    
    2023-10-16 16:14:25 [Relaychain] 💻 CPU architecture: x86_64    
    2023-10-16 16:14:25 [Relaychain] 💻 Target environment: gnu    
    2023-10-16 16:14:25 [Relaychain] 💻 CPU: AMD Ryzen 7 5700G with Radeon Graphics    
    2023-10-16 16:14:25 [Relaychain] 💻 CPU cores: 8    
    2023-10-16 16:14:25 [Relaychain] 💻 Memory: 63578MB    
    2023-10-16 16:14:25 [Relaychain] 💻 Kernel: 6.2.0-33-generic    
    2023-10-16 16:14:25 [Relaychain] 💻 Linux distribution: Ubuntu 22.04.3 LTS    
    2023-10-16 16:14:25 [Relaychain] 💻 Virtual machine: no    
    2023-10-16 16:14:25 [Relaychain] 📦 Highest known block at #61195    
    2023-10-16 16:14:25 [Relaychain] 〽️ Prometheus exporter started at 127.0.0.1:9616    
    2023-10-16 16:14:25 [Relaychain] Running JSON-RPC server: addr=127.0.0.1:9945, allowed origins=["http://localhost:*", "http://127.0.0.1:*", "https://localhost:*", "https://127.0.0.1:*", "https://polkadot.js.org"]    
    2023-10-16 16:14:25 [Relaychain] 🏁 CPU score: 1.34 GiBs    
    2023-10-16 16:14:25 [Relaychain] 🏁 Memory score: 14.33 GiBs    
    2023-10-16 16:14:25 [Relaychain] 🏁 Disk score (seq. writes): 1.42 GiBs    
    2023-10-16 16:14:25 [Relaychain] 🏁 Disk score (rand. writes): 746.65 MiBs    
    2023-10-16 16:14:25 [Relaychain] Starting with an empty approval vote DB.
    2023-10-16 16:14:25 [Parachain] 🏷  Local node identity is: 12D3KooWLoBFJ5oRNmXU8SfSiSuA8vuFAwaS5PyMfdWCGvtXGYnJ    
    2023-10-16 16:14:25 [Parachain] 💻 Operating system: linux    
    2023-10-16 16:14:25 [Parachain] 💻 CPU architecture: x86_64    
    2023-10-16 16:14:25 [Parachain] 💻 Target environment: gnu    
    2023-10-16 16:14:25 [Parachain] 💻 CPU: AMD Ryzen 7 5700G with Radeon Graphics    
    2023-10-16 16:14:25 [Parachain] 💻 CPU cores: 8    
    2023-10-16 16:14:25 [Parachain] 💻 Memory: 63578MB    
    2023-10-16 16:14:25 [Parachain] 💻 Kernel: 6.2.0-33-generic    
    2023-10-16 16:14:25 [Parachain] 💻 Linux distribution: Ubuntu 22.04.3 LTS    
    2023-10-16 16:14:25 [Parachain] 💻 Virtual machine: no    
    2023-10-16 16:14:25 [Parachain] 📦 Highest known block at #18290    
    2023-10-16 16:14:25 [Parachain] Running JSON-RPC server: addr=127.0.0.1:9944, allowed origins=["http://localhost:*", "http://127.0.0.1:*", "https://localhost:*", "https://127.0.0.1:*", "https://polkadot.js.org"]    
    2023-10-16 16:14:25 [Parachain] 🏁 CPU score: 1.34 GiBs    
    2023-10-16 16:14:25 [Parachain] 🏁 Memory score: 14.33 GiBs    
    2023-10-16 16:14:25 [Parachain] 🏁 Disk score (seq. writes): 1.42 GiBs    
    2023-10-16 16:14:25 [Parachain] 🏁 Disk score (rand. writes): 746.65 MiBs    
    2023-10-16 16:14:25 [Parachain] 〽️ Prometheus exporter started at 127.0.0.1:9615    
    2023-10-16 16:14:25 [Parachain] 🔍 Discovered new external address for our node: /ip4/60.176.103.239/tcp/30333/p2p/12D3KooWLoBFJ5oRNmXU8SfSiSuA8vuFAwaS5PyMfdWCGvtXGYnJ    
    2023-10-16 16:14:26 [Relaychain] 🔍 Discovered new external address for our node: /ip4/60.176.103.239/tcp/30334/ws/p2p/12D3KooWJXgiE8JJSv6fCiEmkEjGAewNYh2HPCSJZuKMZrJUwWrR    
    2023-10-16 16:14:26 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.    
    2023-10-16 16:14:26 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.    
    2023-10-16 16:14:26 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.    
    2023-10-16 16:14:26 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.    
    2023-10-16 16:14:26 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.    
    2023-10-16 16:14:26 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.
    ```
    
    A collator operates a relay chain node alongside a parachain node. The status messages `[Relaychain] ⚙️ Syncing` and `[Parachain] ⚙️ Syncing` indicate that the node is currently in the process of syncing. You can refer to these logs to monitor the syncing progress. Given that the relay chain and parachain have been active for several years, the syncing process may take anywhere from one to three days to complete.
    
6. Generate [session key](https://www.notion.so/Glossary-8967fc4aa6a046a69b525dff7bf70a50?pvs=21)
    
    To generate your node session key, leave the node running in one terminal and open another terminal. Then, execute the following command:
    
    ```bash
    curl -X POST \
         -H 'Content-Type: application/json' \
         -d '{"id":1, "jsonrpc":"2.0", "method":"author_rotateKeys", "params":[]}' \
         http://127.0.0.1:9944
    ```
    
    the output display like this:
    
    ```bash
    {"jsonrpc":"2.0","result":"0x846fa7e10413740d94281a496f9422447182cb6562ea8df8227dded1766b9163","id":1}
    ```
    
    `0x846fa7e10413740d94281a496f9422447182cb6562ea8df8227dded1766b9163` is the generated session key. **Please remember to securely store this key as it is necessary for registering as a collator in the staking app.**
    
7. Wait for the node sync process to complete
    
    Once the syncing process of the node is complete, you are just a step away from becoming a fully operational network collator. Keep an eye on your node's running terminal, and when you come across a message resembling the following, it signifies the completion of the syncing process.
    
    ```bash
    2023-07-25 02:43:30 [Relaychain] ✨ Imported #16547932 (0x3391…ab15)
    2023-07-25 02:43:31 [Parachain] ✨ Imported #636560 (0x2ea0…29d0)
    2023-07-25 02:43:35 [Relaychain] 💤 Idle (109 peers), best: #16547932 (0x3391…ab15), finalized #16547930 (0x7b6b…4c5d), ⬇ 326.8kiB/s ⬆ 203.2kiB/s
    2023-07-25 02:43:35 [Parachain] 💤 Idle (31 peers), best: #636559 (0x235e…ab71), finalized #636558 (0x03fc…a0f5), ⬇ 30.9kiB/s ⬆ 14.5kiB/s
    2023-07-25 02:43:36 [Relaychain] ✨ Imported #16547933 (0x7569…7c4d)
    2023-07-25 02:43:40 [Relaychain] 💤 Idle (109 peers), best: #16547933 (0x7569…7c4d), finalized #16547930 (0x7b6b…4c5d), ⬇ 305.1kiB/s ⬆ 272.8kiB/s
    2023-07-25 02:43:40 [Parachain] 💤 Idle (31 peers), best: #636559 (0x235e…ab71), finalized #636558 (0x03fc…a0f5), ⬇ 1.1kiB/s ⬆ 1.4kiB/s
    2023-07-25 02:43:42 [Relaychain] ✨ Imported #16547934 (0xa4aa…c72b)
    2023-07-25 02:43:43 [Parachain] ✨ Imported #636561 (0x97de…c0ba)
    2023-07-25 02:43:45 [Relaychain] 💤 Idle (109 peers), best: #16547934 (0xa4aa…c72b), finalized #16547931 (0x17bc…5121), ⬇ 364.1kiB/s ⬆ 296.6kiB/s
    2023-07-25 02:43:45 [Parachain] 💤 Idle (31 peers), best: #636560 (0x2ea0…29d0), finalized #636558 (0x03fc…a0f5), ⬇ 35.5kiB/s ⬆ 8.1kiB/s
    2023-07-25 02:43:48 [Relaychain] ✨ Imported #16547935 (0x9f0f…517e)
    2023-07-25 02:43:48 [Relaychain] ✨ Imported #16547935 (0x7892…a897)
    2023-07-25 02:43:50 [Relaychain] 💤 Idle (109 peers), best: #16547935 (0x9f0f…517e), finalized #16547932 (0x3391…ab15), ⬇ 466.0kiB/s ⬆ 301.9kiB/s
    2023-07-25 02:43:50 [Parachain] 💤 Idle (31 peers), best: #636560 (0x2ea0…29d0), finalized #636559 (0x235e…ab71), ⬇ 1.0kiB/s ⬆ 3.1kiB/s
    ```
    

### Set Session Key And Commission Rate

1. Once your node has finished syncing, ensure that it is still running.
2. Open the [staking app](https://staking.darwinia.network/#/?network=darwinia) in your browser and connect it to your wallet account. You have the option to choose between MetaMask or WalletConnect, as both wallets are now supported.
    
    ![Untitled](Run%20Collator%20Node%20af6bce360d5b49ddacc56e4587510210/Untitled.png)
    
3. Click on the `Join Collator` button and follow these steps:
    1. Enter the session key that was generated earlier and click on `Set Session Key` to prompt the wallet for submitting an Ethereum transaction.
    2. Enter the desired commission amount and click on `Set Commission` to prompt the wallet for submitting an Ethereum transaction.

![Untitled](Run%20Collator%20Node%20af6bce360d5b49ddacc56e4587510210/Untitled%201.png)

![Untitled](Run%20Collator%20Node%20af6bce360d5b49ddacc56e4587510210/Untitled%202.png)

1. To verify that your account is in the collator waiting pool, click on the `Select a collator` button.
    
    ![Untitled](Run%20Collator%20Node%20af6bce360d5b49ddacc56e4587510210/Untitled%203.png)
    
    ![Untitled](Run%20Collator%20Node%20af6bce360d5b49ddacc56e4587510210/Untitled%204.png)
    

## To be a real collator

1. Accumulate power by staking or depositing
    
    At this point, your node is operational and the node session key has been successfully registered and associated with your account. As a candidate collator, you are currently in the waiting pool. However, in order to progress and participate in block production, as well as receive rewards, you must collect sufficient power. To achieve this, you can either stake native `RING`  or deposit `KTON`. By doing so, you will accumulate the necessary power to be included in the real collator list. It is important to note that only the top 20 power-owning collators will be selected to form the collator set for the next session.
    
2. Wait until the next session
    
    Once you have accumulated enough power and have been selected as a real collator, your node will begin producing blocks once the next session starts. You will be able to observe messages similar to the following in the node log:
    
    ```bash
    2023-07-25 02:29:36 [Parachain] Starting collation. relay_parent=0x6e01f34762d42f007122a3e1ce6c4831dfd83ac5b6785d094ec526c573f332a6 at=0x0daa9a024b7c31241cdaffeebcc60ae778c24a005f42a6989092e7f63860161a
    2023-07-25 02:29:36 [Parachain] ✨ Imported #636493 (0x0cf1…1d91)
    2023-07-25 02:29:38 [Parachain] 💤 Idle (11 peers), best: #636492 (0x0daa…161a), finalized #636490 (0x4b44…310c), ⬇ 7.4kiB/s ⬆ 4.7kiB/s
    2023-07-25 02:29:38 [Relaychain] 💤 Idle (147 peers), best: #16547793 (0x6e01…32a6), finalized #16547790 (0x63fa…f203), ⬇ 335.0kiB/s ⬆ 404.6kiB/s
    2023-07-25 02:29:42 [Relaychain] ✨ Imported #16547794 (0xa7e0…5f03)
    2023-07-25 02:29:43 [Parachain] 💤 Idle (11 peers), best: #636492 (0x0daa…161a), finalized #636491 (0x78a0…5135), ⬇ 0.2kiB/s ⬆ 0.2kiB/s
    2023-07-25 02:29:43 [Relaychain] 💤 Idle (147 peers), best: #16547794 (0xa7e0…5f03), finalized #16547791 (0x865f…5f93), ⬇ 335.0kiB/s ⬆ 380.2kiB/s
    2023-07-25 02:29:48 [Parachain] 💤 Idle (11 peers), best: #636492 (0x0daa…161a), finalized #636491 (0x78a0…5135), ⬇ 74 B/s ⬆ 74 B/s
    2023-07-25 02:29:48 [Relaychain] 💤 Idle (149 peers), best: #16547794 (0xa7e0…5f03), finalized #16547792 (0x4fe7…12a4), ⬇ 364.7kiB/s ⬆ 417.2kiB/s
    2023-07-25 02:29:48 [Relaychain] ✨ Imported #16547795 (0x59e7…1c0c)
    2023-07-25 02:29:48 [Parachain] Starting collation. relay_parent=0x59e78ce166cfd86edbd65e827d4091bf571a7eff09dcb8ba054ad3f5eb8d1c0c at=0x0cf1b42f16e6411f624b15c48a9fd3666643cbba12ff9b4ea36aa4d18ceb1d91
    2023-07-25 02:29:48 [Relaychain] ✨ Imported #16547795 (0x62f3…ec4b)
    2023-07-25 02:29:48 [Parachain] Starting collation. relay_parent=0x62f3987004eafc258b4a62252c3f187e7cdd8dc896b760692a456721f743ec4b at=0x0cf1b42f16e6411f624b15c48a9fd3666643cbba12ff9b4ea36aa4d18ceb1d91
    2023-07-25 02:29:51 [Parachain] ✨ Imported #636494 (0x7318…81cc)
    2023-07-25 02:29:51 [Parachain] ✨ Imported #636494 (0xe2ac…8564)
    2023-07-25 02:29:53 [Parachain] 💤 Idle (11 peers), best: #636493 (0x0cf1…1d91), finalized #636491 (0x78a0…5135), ⬇ 24.0kiB/s ⬆ 3.9kiB/s
    2023-07-25 02:29:53 [Relaychain] 💤 Idle (149 peers), best: #16547795 (0x59e7…1c0c), finalized #16547792 (0x4fe7…12a4), ⬇ 372.0kiB/s ⬆ 422.2kiB/s
    2023-07-25 02:29:54 [Relaychain] ✨ Imported #16547796 (0x3385…41df)
    2023-07-25 02:29:58 [Parachain] 💤 Idle (11 peers), best: #636493 (0x0cf1…1d91), finalized #636492 (0x0daa…161a), ⬇ 0.1kiB/s ⬆ 0.3kiB/s
    2023-07-25 02:29:58 [Relaychain] 💤 Idle (148 peers), best: #16547796 (0x3385…41df), finalized #16547793 (0x6e01…32a6), ⬇ 193.2kiB/s ⬆ 345.7kiB/s
    2023-07-25 02:30:00 [Relaychain] ✨ Imported #16547797 (0x8476…715f)
    2023-07-25 02:30:00 [Parachain] Starting collation. relay_parent=0x84766f7ebf5ec140fd3add8052447f0c74f688a1fb0b71083498ff1853b4715f at=0xe2acefecc7a059cd833b8b3347fb076768f6587e37d58337ded0e9d376068564
    2023-07-25 02:30:03 [Parachain] 💤 Idle (11 peers), best: #636494 (0xe2ac…8564), finalized #636492 (0x0daa…161a), ⬇ 0.2kiB/s ⬆ 0.2kiB/s
    2023-07-25 02:30:03 [Relaychain] 💤 Idle (147 peers), best: #16547797 (0x8476…715f), finalized #16547794 (0xa7e0…5f03), ⬇ 257.7kiB/s ⬆ 464.5kiB/s
    ```
    

Congratulations! You have successfully become a collator on the Darwinia network. As a collator, you play a crucial role in ensuring the overall liveness of the network. It is important that you actively monitor and stay updated with the latest developments concerning the Darwinia node. Please note that if you are not actively fulfilling your duties, there is a risk of your staking assets being slashed.