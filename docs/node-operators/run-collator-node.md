# Run Collator Node

Darwinia Collators play a crucial role in the Darwinia Network as they are responsible for block production and ensuring block liveness. These Collators collect transactions from users on the parachain and generate state transition proofs for Relay Chain validators. In essence, they provide blocks to validators on the relay chain for finalization.

To learn more about Collators and their functions, you can click [here](https://wiki.polkadot.network/docs/learn-collator). This resource will provide you with detailed information on the topic.

## Recommended Hardware

- **RAM:**  8 GB:
- **Storage(SSD)**: 800 GB

## Download Snapshot

It's important to note that there is a faster method to expedite the syncing process. You can achieve this by downloading the snapshot blockchain data and moving it to the current node database location and greatly speeding up the node sync process. Click [here](./snapshot.md) for more detailed instructions.

## Start The Collator Node

1. Open a terminal shell on your computer
2. Create a work dirctory
    
    Let's create a directory called `run-collator-node` to store everything needed for setting up an collator node, including the downloaded node binary and the chain database.
    
    ```bash
    mkdir run-collator-node && cd run-collator-node
    ```
    
3. Download and decompress the binary.
    
    As of the time of writing this doc(2024-09-27), the latest version of the Darwinia node is `v6.7.1`. Please ensure that you check for [the latest version](https://github.com/darwinia-network/darwinia/releases) when running your own node. 
    
    ```bash
    wget https://github.com/darwinia-network/darwinia/releases/download/v6.7.1/darwinia-x86_64-linux-gnu.tar.bz2
    tar xvf darwinia-x86_64-linux-gnu.tar.bz2
    ```
    
4. Start the node by running the following command:
    
    ```bash
    ./darwinia --chain=darwinia --base-path=/data/darwinia-collator --frontier-backend-type=sql --collator
    ```
    
5. Verify your node is up and running successfully by reviewing the output displayed in the terminal. The terminal should display output similar to this:
    
    ```bash
    Loading genesis from `/home/darwinia/darwinia-nodes/darwinia2.json`
    2024-09-27 06:48:10 Darwinia
    2024-09-27 06:48:10 ✌️  version 6.7.1-08ec5e77d17
    2024-09-27 06:48:10 ❤️  by Darwinia Network <hello@darwinia.network>, 2018-2024
    2024-09-27 06:48:10 📋 Chain specification: Darwinia2
    2024-09-27 06:48:10 🏷  Node name: jazzy-bird-4606
    2024-09-27 06:48:10 👤 Role: AUTHORITY
    2024-09-27 06:48:10 💾 Database: RocksDb at /home/darwinia/data/chains/darwinia2/db/full
    2024-09-27 06:48:10 Parachain id: Id(2046)
    2024-09-27 06:48:10 Parachain Account: 2qiDxtPxw1BsbLwujRn5Q2352CaDPY8UMZi4iHBfPXo6FgHd
    2024-09-27 06:48:10 Is collating: yes
    2024-09-27 06:48:12 [Parachain] 🔨 Initializing Genesis block/state (state: 0xde42…7b71, header-hash: 0xf0b8…570e)
    2024-09-27 06:48:13 [Parachain] 📑 Connection configuration: SqliteBackendConfig { path: "/home/darwinia/data/chains/darwinia2/sql/frontier.db3", create_if_missing: true, thread_count: 4, cache_size: 209715200 }
    2024-09-27 06:48:16 [Relaychain] 🔨 Initializing Genesis block/state (state: 0x29d0…4e17, header-hash: 0x91b1…90c3)
    2024-09-27 06:48:16 [Relaychain] 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.
    2024-09-27 06:48:16 [Relaychain] 👶 Creating empty BABE epoch changes on what appears to be first startup.
    2024-09-27 06:48:16 [Relaychain] 🏷  Local node identity is: 12D3KooWGijgF3rWBaG9VvsaKMWBrFKyhwU5ysgxhAdTxassM82Z
    2024-09-27 06:48:16 [Relaychain] 💻 Operating system: linux
    2024-09-27 06:48:16 [Relaychain] 💻 CPU architecture: x86_64
    2024-09-27 06:48:16 [Relaychain] 💻 Target environment: gnu
    2024-09-27 06:48:16 [Relaychain] 💻 CPU: Intel(R) Core(TM) i9-9900K CPU @ 3.60GHz
    2024-09-27 06:48:16 [Relaychain] 💻 CPU cores: 8
    2024-09-27 06:48:16 [Relaychain] 💻 Memory: 64268MB
    2024-09-27 06:48:16 [Relaychain] 💻 Kernel: 4.19.0-23-amd64
    2024-09-27 06:48:16 [Relaychain] 💻 Linux distribution: Ubuntu 20.04.6 LTS
    2024-09-27 06:48:16 [Relaychain] 💻 Virtual machine: no
    2024-09-27 06:48:16 [Relaychain] 📦 Highest known block at #0
    2024-09-27 06:48:16 [Relaychain] 〽️ Prometheus exporter started at 127.0.0.1:9616
    2024-09-27 06:48:16 [Relaychain] Running JSON-RPC server: addr=127.0.0.1:9945, allowed origins=["http://localhost:*", "http://127.0.0.1:*", "https://localhost:*", "https://127.0.0.1:*", "https://polkadot.js.org"]
    2024-09-27 06:48:16 [Relaychain] 🏁 CPU score: 1.46 GiBs
    2024-09-27 06:48:16 [Relaychain] 🏁 Memory score: 5.16 GiBs
    2024-09-27 06:48:16 [Relaychain] 🏁 Disk score (seq. writes): 334.31 MiBs
    2024-09-27 06:48:16 [Relaychain] 🏁 Disk score (rand. writes): 123.23 MiBs
    2024-09-27 06:48:16 [Parachain] 🏷  Local node identity is: 12D3KooWSNvVDTkZvkEjFosA8d79VysvQ4BW653zD3dy5aVbqmzm
    2024-09-27 06:48:16 Import genesis
    2024-09-27 06:48:16 [Parachain] 💻 Operating system: linux
    2024-09-27 06:48:16 [Parachain] 💻 CPU architecture: x86_64
    2024-09-27 06:48:16 [Parachain] 💻 Target environment: gnu
    2024-09-27 06:48:16 [Parachain] 💻 CPU: Intel(R) Core(TM) i9-9900K CPU @ 3.60GHz
    2024-09-27 06:48:16 [Parachain] 💻 CPU cores: 8
    2024-09-27 06:48:16 [Parachain] 💻 Memory: 64268MB
    2024-09-27 06:48:16 [Parachain] 💻 Kernel: 4.19.0-23-amd64
    2024-09-27 06:48:16 [Parachain] 💻 Linux distribution: Ubuntu 20.04.6 LTS
    2024-09-27 06:48:16 [Parachain] 💻 Virtual machine: no
    2024-09-27 06:48:16 [Parachain] 📦 Highest known block at #0
    2024-09-27 06:48:16 [Parachain] 〽️ Prometheus exporter started at 127.0.0.1:9615
    2024-09-27 06:48:16 [Parachain] Running JSON-RPC server: addr=127.0.0.1:9944, allowed origins=["http://localhost:*", "http://127.0.0.1:*", "https://localhost:*", "https://127.0.0.1:*", "https://polkadot.js.org"]
    2024-09-27 06:48:16 [Parachain] 🏁 CPU score: 1.46 GiBs
    2024-09-27 06:48:16 [Parachain] 🏁 Memory score: 5.16 GiBs
    2024-09-27 06:48:16 [Parachain] 🏁 Disk score (seq. writes): 334.31 MiBs
    2024-09-27 06:48:16 [Parachain] 🏁 Disk score (rand. writes): 123.23 MiBs
    2024-09-27 06:48:16 [Parachain] ⚠️  The hardware does not meet the minimal requirements Failed checks: Copy(expected: 11.49 GiBs, found: 5.16 GiBs), Seq Write(expected: 950.00 MiBs, found: 334.31 MiBs), Rnd Write(expected: 420.00 MiBs, found: 123.23 MiBs),  for role 'Authority'.
    2024-09-27 06:48:16 [Relaychain] discovered: 12D3KooWSNvVDTkZvkEjFosA8d79VysvQ4BW653zD3dy5aVbqmzm /ip4/172.17.0.2/tcp/30333
    2024-09-27 06:48:16 [Parachain] discovered: 12D3KooWGijgF3rWBaG9VvsaKMWBrFKyhwU5ysgxhAdTxassM82Z /ip4/172.17.0.2/tcp/30334/ws
    2024-09-27 06:48:17 [Relaychain] Sending fatal alert BadCertificate
    2024-09-27 06:48:17 [Relaychain] 💔 The bootnode you want to connect to at `/dns/dot14.rotko.net/tcp/33214/p2p/12D3KooWPyEvPEXghnMC67Gff6PuZiSvfx3fmziKiPZcGStZ5xff` provided a different peer ID `12D3KooWPc7jNXa7zbsRzF5rdq3QEqhwJLdnXcgG3PR74z99PAka` than the one you expect `12D3KooWPyEvPEXghnMC67Gff6PuZiSvfx3fmziKiPZcGStZ5xff`.
    2024-09-27 06:48:17 [Relaychain] Sending fatal alert BadCertificate
    2024-09-27 06:48:18 [Parachain] 🔍 Discovered new external address for our node: /ip4/220.246.94.186/tcp/30333/p2p/12D3KooWSNvVDTkZvkEjFosA8d79VysvQ4BW653zD3dy5aVbqmzm
    2024-09-27 06:48:18 [Relaychain] Sending fatal alert BadCertificate
    2024-09-27 06:48:18 [Relaychain] 🔍 Discovered new external address for our node: /ip4/220.246.94.186/tcp/30334/ws/p2p/12D3KooWGijgF3rWBaG9VvsaKMWBrFKyhwU5ysgxhAdTxassM82Z
    2024-09-27 06:48:19 [Relaychain] Sending fatal alert BadCertificate
    2024-09-27 06:48:19 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.
    2024-09-27 06:48:19 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.
    2024-09-27 06:48:19 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.
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
    2024-09-04 02:43:30 [Relaychain] ✨ Imported #16547932 (0x3391…ab15)
    2024-09-04 02:43:31 [Parachain] ✨ Imported #636560 (0x2ea0…29d0)
    2024-09-04 02:43:35 [Relaychain] 💤 Idle (109 peers), best: #16547932 (0x3391…ab15), finalized #16547930 (0x7b6b…4c5d), ⬇ 326.8kiB/s ⬆ 203.2kiB/s
    2024-09-04 02:43:35 [Parachain] 💤 Idle (31 peers), best: #636559 (0x235e…ab71), finalized #636558 (0x03fc…a0f5), ⬇ 30.9kiB/s ⬆ 14.5kiB/s
    2024-09-04 02:43:36 [Relaychain] ✨ Imported #16547933 (0x7569…7c4d)
    2024-09-04 02:43:40 [Relaychain] 💤 Idle (109 peers), best: #16547933 (0x7569…7c4d), finalized #16547930 (0x7b6b…4c5d), ⬇ 305.1kiB/s ⬆ 272.8kiB/s
    2024-09-04 02:43:40 [Parachain] 💤 Idle (31 peers), best: #636559 (0x235e…ab71), finalized #636558 (0x03fc…a0f5), ⬇ 1.1kiB/s ⬆ 1.4kiB/s
    2024-09-04 02:43:42 [Relaychain] ✨ Imported #16547934 (0xa4aa…c72b)
    2024-09-04 02:43:43 [Parachain] ✨ Imported #636561 (0x97de…c0ba)
    2024-09-04 02:43:45 [Relaychain] 💤 Idle (109 peers), best: #16547934 (0xa4aa…c72b), finalized #16547931 (0x17bc…5121), ⬇ 364.1kiB/s ⬆ 296.6kiB/s
    2024-09-04 02:43:45 [Parachain] 💤 Idle (31 peers), best: #636560 (0x2ea0…29d0), finalized #636558 (0x03fc…a0f5), ⬇ 35.5kiB/s ⬆ 8.1kiB/s
    2024-09-04 02:43:48 [Relaychain] ✨ Imported #16547935 (0x9f0f…517e)
    2024-09-04 02:43:48 [Relaychain] ✨ Imported #16547935 (0x7892…a897)
    2024-09-04 02:43:50 [Relaychain] 💤 Idle (109 peers), best: #16547935 (0x9f0f…517e), finalized #16547932 (0x3391…ab15), ⬇ 466.0kiB/s ⬆ 301.9kiB/s
    2024-09-04 02:43:50 [Parachain] 💤 Idle (31 peers), best: #636560 (0x2ea0…29d0), finalized #636559 (0x235e…ab71), ⬇ 1.0kiB/s ⬆ 3.1kiB/s
    ```
    

## Join The Collators Set

Once your node has finished syncing, ensure that it is still running, then follow the [Join Collators Set Guide](https://ringdao.notion.site/How-to-become-a-collator-fffaad1d671e81c6b5f0ee4e97c29889) to complete the process of becoming a collator.

## To Be A Real Collator

1. Accumulate `RING` by staking or depositing
    
    At this point, your node is operational and the node session key has been successfully registered and associated with your account. As a candidate collator, you are currently in the waiting pool. However, in order to progress and participate in block production, as well as receive rewards, you must collect sufficient `RING`. To achieve this, you can either stake native `RING`  or deposit `KTON`. By doing so, you will accumulate the necessary `RING ` to be included in the real collator list. It is important to note that only the top 20 RING-owning collators will be selected to form the collator set for the next session.
    
2. Wait until the next session
    
    Once you have accumulated enough `RING` and have been selected as a real collator, your node will begin producing blocks once the next session starts. You will be able to observe messages similar to the following in the node log:
    
    ```bash
    2024-09-04 02:29:36 [Parachain] Starting collation. relay_parent=0x6e01f34762d42f007122a3e1ce6c4831dfd83ac5b6785d094ec526c573f332a6 at=0x0daa9a024b7c31241cdaffeebcc60ae778c24a005f42a6989092e7f63860161a
    2024-09-04 02:29:36 [Parachain] ✨ Imported #636493 (0x0cf1…1d91)
    2024-09-04 02:29:38 [Parachain] 💤 Idle (11 peers), best: #636492 (0x0daa…161a), finalized #636490 (0x4b44…310c), ⬇ 7.4kiB/s ⬆ 4.7kiB/s
    2024-09-04 02:29:38 [Relaychain] 💤 Idle (147 peers), best: #16547793 (0x6e01…32a6), finalized #16547790 (0x63fa…f203), ⬇ 335.0kiB/s ⬆ 404.6kiB/s
    2024-09-04 02:29:42 [Relaychain] ✨ Imported #16547794 (0xa7e0…5f03)
    2024-09-04 02:29:43 [Parachain] 💤 Idle (11 peers), best: #636492 (0x0daa…161a), finalized #636491 (0x78a0…5135), ⬇ 0.2kiB/s ⬆ 0.2kiB/s
    2024-09-04 02:29:43 [Relaychain] 💤 Idle (147 peers), best: #16547794 (0xa7e0…5f03), finalized #16547791 (0x865f…5f93), ⬇ 335.0kiB/s ⬆ 380.2kiB/s
    2024-09-04 02:29:48 [Parachain] 💤 Idle (11 peers), best: #636492 (0x0daa…161a), finalized #636491 (0x78a0…5135), ⬇ 74 B/s ⬆ 74 B/s
    2024-09-04 02:29:48 [Relaychain] 💤 Idle (149 peers), best: #16547794 (0xa7e0…5f03), finalized #16547792 (0x4fe7…12a4), ⬇ 364.7kiB/s ⬆ 417.2kiB/s
    2024-09-04 02:29:48 [Relaychain] ✨ Imported #16547795 (0x59e7…1c0c)
    2024-09-04 02:29:48 [Parachain] Starting collation. relay_parent=0x59e78ce166cfd86edbd65e827d4091bf571a7eff09dcb8ba054ad3f5eb8d1c0c at=0x0cf1b42f16e6411f624b15c48a9fd3666643cbba12ff9b4ea36aa4d18ceb1d91
    2024-09-04 02:29:48 [Relaychain] ✨ Imported #16547795 (0x62f3…ec4b)
    2024-09-04 02:29:48 [Parachain] Starting collation. relay_parent=0x62f3987004eafc258b4a62252c3f187e7cdd8dc896b760692a456721f743ec4b at=0x0cf1b42f16e6411f624b15c48a9fd3666643cbba12ff9b4ea36aa4d18ceb1d91
    2024-09-04 02:29:51 [Parachain] ✨ Imported #636494 (0x7318…81cc)
    2024-09-04 02:29:51 [Parachain] ✨ Imported #636494 (0xe2ac…8564)
    2024-09-04 02:29:53 [Parachain] 💤 Idle (11 peers), best: #636493 (0x0cf1…1d91), finalized #636491 (0x78a0…5135), ⬇ 24.0kiB/s ⬆ 3.9kiB/s
    2024-09-04 02:29:53 [Relaychain] 💤 Idle (149 peers), best: #16547795 (0x59e7…1c0c), finalized #16547792 (0x4fe7…12a4), ⬇ 372.0kiB/s ⬆ 422.2kiB/s
    2024-09-04 02:29:54 [Relaychain] ✨ Imported #16547796 (0x3385…41df)
    2024-09-04 02:29:58 [Parachain] 💤 Idle (11 peers), best: #636493 (0x0cf1…1d91), finalized #636492 (0x0daa…161a), ⬇ 0.1kiB/s ⬆ 0.3kiB/s
    2024-09-04 02:29:58 [Relaychain] 💤 Idle (148 peers), best: #16547796 (0x3385…41df), finalized #16547793 (0x6e01…32a6), ⬇ 193.2kiB/s ⬆ 345.7kiB/s
    2024-09-04 02:30:00 [Relaychain] ✨ Imported #16547797 (0x8476…715f)
    2024-09-04 02:30:00 [Parachain] Starting collation. relay_parent=0x84766f7ebf5ec140fd3add8052447f0c74f688a1fb0b71083498ff1853b4715f at=0xe2acefecc7a059cd833b8b3347fb076768f6587e37d58337ded0e9d376068564
    2024-09-04 02:30:03 [Parachain] 💤 Idle (11 peers), best: #636494 (0xe2ac…8564), finalized #636492 (0x0daa…161a), ⬇ 0.2kiB/s ⬆ 0.2kiB/s
    2024-09-04 02:30:03 [Relaychain] 💤 Idle (147 peers), best: #16547797 (0x8476…715f), finalized #16547794 (0xa7e0…5f03), ⬇ 257.7kiB/s ⬆ 464.5kiB/s
    ```
    

Congratulations! You have successfully become a collator on the Darwinia network. As a collator, you play a crucial role in ensuring the overall liveness of the network. It is important that you actively monitor and stay updated with the latest developments concerning the Darwinia node. Please note that if you are not actively fulfilling your duties, there is a risk of your staking assets being slashed.
