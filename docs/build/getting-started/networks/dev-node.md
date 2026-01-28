# Run Development Testnet

Darwinia no longer maintains a public testnet, so spinning up a local development network is the best way to experiment without risking production funds. Creating your own development network significantly enhances your ability to test or debug low-level features. This guide walks you through the process of establishing a single-node development network.

## Compile darwinia node

1. Open a terminal shell on your computer.
2. Clone the darwinia repository by running the following command:
    
    ```bash
    git clone https://github.com/darwinia-network/darwinia.git
    ```
    
3. Change to the root of the repository and compile the node:
    
    ```bash
    cd darwinia
    cargo build --release -p darwinia --features all-runtime
    ```
    
4. When the compilation is finished, something like this will be printed:
    
    ```bash
    ......
    Compiling evm-gasometer v0.41.0 (https://github.com/darwinia-network/evm.git?branch=stable2407#b1e92a28)
    Compiling evm v0.41.2 (https://github.com/darwinia-network/evm.git?branch=stable2407#b1e92a28)
    Compiling fp-evm v3.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling evm-tracing-events v0.1.0 (https://github.com/darwinia-network/moonbeam?branch=stable2407#a816c21a)
    Compiling moonbeam-client-evm-tracing v0.1.0 (https://github.com/darwinia-network/moonbeam?branch=stable2407#a816c21a)
    Compiling pallet-evm v6.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling fp-rpc v3.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling fp-ethereum v1.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling pallet-evm-precompile-bn128 v2.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling pallet-evm-precompile-modexp v2.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling pallet-evm-precompile-blake2 v2.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling pallet-evm-precompile-simple v2.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling pallet-evm-precompile-bls12381 v1.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling fc-storage v1.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling fc-consensus v2.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling moonbeam-rpc-core-debug v0.1.0 (https://github.com/darwinia-network/moonbeam?branch=stable2407#a816c21a)
    Compiling moonbeam-rpc-core-trace v0.6.0 (https://github.com/darwinia-network/moonbeam?branch=stable2407#a816c21a)
    Compiling fc-db v2.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling precompile-utils v0.1.0 (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling darwinia-ethtx-forwarder v6.8.1 (/mnt/myssd/coding/darwinia-space/darwinia/pallet/ethtx-forwarder)
    Compiling pallet-evm-precompile-dispatch v2.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling pallet-ethereum v4.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling darwinia-deposit v6.8.1 (/mnt/myssd/coding/darwinia-space/darwinia/pallet/deposit)
    Compiling darwinia-staking v6.8.1 (/mnt/myssd/coding/darwinia-space/darwinia/pallet/staking)
    Compiling fc-mapping-sync v2.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling darwinia-account-migration v6.8.1 (/mnt/myssd/coding/darwinia-space/darwinia/pallet/account-migration)
    Compiling fc-rpc v2.0.0-dev (https://github.com/polkadot-evm/frontier?branch=stable2407#2e219e17)
    Compiling moonbeam-rpc-debug v0.1.0 (https://github.com/darwinia-network/moonbeam?branch=stable2407#a816c21a)
    Compiling moonbeam-rpc-trace v0.6.0 (https://github.com/darwinia-network/moonbeam?branch=stable2407#a816c21a)
    Compiling darwinia-precompile-assets v6.8.1 (/mnt/myssd/coding/darwinia-space/darwinia/precompile/assets)
    Compiling pallet-evm-precompile-conviction-voting v0.1.0 (https://github.com/darwinia-network/moonbeam?branch=stable2407#a816c21a)
    Compiling darwinia-precompile-state-storage v6.8.1 (/mnt/myssd/coding/darwinia-space/darwinia/precompile/state-storage)
    Compiling darwinia-common-runtime v6.8.1 (/mnt/myssd/coding/darwinia-space/darwinia/runtime/common)
    Finished `release` profile [optimized] target(s) in 2m 40s
    ```
    

## Start the development node

After your node compiles, you are ready to start exploring what it does using the Darwinia development node.

To start the local development node:

1. In the same terminal where you compiled your node, you can now start the node in development mode by running the following command:
    
	```bash
	./target/release/darwinia --dev --alice --tmp --rpc-external --rpc-cors all --unsafe-force-node-key-generation
	```

	The darwinia command-line options specify how you want the running node to operate. In this case, the `--dev` option runs an ephemeral single-node network with predefined accounts. By default, this option also deletes all active data—such as keys, the blockchain database, and networking information—when you stop the node by pressing Ctrl-C. Using the `--tmp` option ensures that you have a clean working state any time you stop and restart the node.
    
2. Verify your node is up and running successfully by reviewing the output displayed in the terminal. The terminal should display output similar to this:
    
    ```bash
    2025-01-14 17:46:13 darwinia    
    2025-01-14 17:46:13 ✌️  version 6.8.1-8476af2e40e    
    2025-01-14 17:46:13 ❤️  by Darwinia Network <hello@darwinia.network>, 2018-2025    
    2025-01-14 17:46:13 📋 Chain specification: Development    
    2025-01-14 17:46:13 🏷  Node name: Alice    
    2025-01-14 17:46:13 👤 Role: AUTHORITY    
    2025-01-14 17:46:13 💾 Database: RocksDb at /tmp/substraterhaReX/chains/dev/db/full    
    2025-01-14 17:46:13 🪪 Parachain id: Id(2046)    
    2025-01-14 17:46:13 🧾 Parachain Account: 5Ec4AhNxga1JYLioRBNxfRnovheDELVbZTRSnKMgvSVPvNcN    
    2025-01-14 17:46:13 ✍️ Is collating: yes    
    2025-01-14 17:46:14 assembling new collators for new session 0 at #0    
    2025-01-14 17:46:14 RING staking contract must be some; qed    
    2025-01-14 17:46:14 assembling new collators for new session 1 at #0    
    2025-01-14 17:46:14 RING staking contract must be some; qed    
    2025-01-14 17:46:14 🔨 Initializing Genesis block/state (state: 0x8af4…8f61, header-hash: 0x2e55…42d9)    
    2025-01-14 17:46:14 🏷  Local node identity is: 12D3KooWLUJfiPveWoHTeEpN8MFypjoABVuuLPGahAjzqM7xn32C    
    2025-01-14 17:46:14 Running libp2p network backend    
    2025-01-14 17:46:14 💻 Operating system: linux    
    2025-01-14 17:46:14 💻 CPU architecture: x86_64    
    2025-01-14 17:46:14 💻 Target environment: gnu    
    2025-01-14 17:46:14 💻 CPU: AMD Ryzen 7 5700G with Radeon Graphics    
    2025-01-14 17:46:14 💻 CPU cores: 8    
    2025-01-14 17:46:14 💻 Memory: 63584MB    
    2025-01-14 17:46:14 💻 Kernel: 6.8.0-49-generic    
    2025-01-14 17:46:14 💻 Linux distribution: Ubuntu 22.04.5 LTS    
    2025-01-14 17:46:14 💻 Virtual machine: no    
    2025-01-14 17:46:14 📦 Highest known block at #0    
    2025-01-14 17:46:14 〽️ Prometheus exporter started at 127.0.0.1:9615    
    2025-01-14 17:46:14 Running JSON-RPC server: addr=0.0.0.0:9944, allowed origins=["*"]    
    2025-01-14 17:46:18 🙌 Starting consensus session on top of parent 0x2e5540a21c82b56c1c562c70bfd98e30a9b1f7646b0e8aff06415c833faf42d9 (#0)    
    2025-01-14 17:46:18 🎁 Prepared block for proposing at 1 (1 ms) [hash: 0xf2a26363dda74c26d61d8473f47bc8ba588a3015de0e5d7c047f99aaedd15b7c; parent_hash: 0x2e55…42d9; extrinsics (2): [0x0bf5…e66e, 0x7af7…7dc6]    
    2025-01-14 17:46:18 🔖 Pre-sealed block for proposal at 1. Hash now 0xfaf6737b21b49929fce65a138b839c79593d835cc679e967a3767d3f59bc0784, previously 0xf2a26363dda74c26d61d8473f47bc8ba588a3015de0e5d7c047f99aaedd15b7c.    
    2025-01-14 17:46:18 🏆 Imported #1 (0x2e55…42d9 → 0xfaf6…0784)    
    2025-01-14 17:46:19 💤 Idle (0 peers), best: #1 (0xfaf6…0784), finalized #1 (0xfaf6…0784), ⬇ 0 ⬆ 0    
    2025-01-14 17:46:24 🙌 Starting consensus session on top of parent 0xfaf6737b21b49929fce65a138b839c79593d835cc679e967a3767d3f59bc0784 (#1)    
    2025-01-14 17:46:24 🎁 Prepared block for proposing at 2 (1 ms) [hash: 0xf4c5189184dd79ba7203bbca689947a66729efb6c1f3ec078c0ef7d089189bbe; parent_hash: 0xfaf6…0784; extrinsics (2): [0x1dab…0d91, 0xa161…c06b]    
    2025-01-14 17:46:24 🔖 Pre-sealed block for proposal at 2. Hash now 0xc9e89c0b5cde3de6ddf7430c9f5951225aa06f906c27375002212b41acfef087, previously 0xf4c5189184dd79ba7203bbca689947a66729efb6c1f3ec078c0ef7d089189bbe.    
    2025-01-14 17:46:24 🏆 Imported #2 (0xfaf6…0784 → 0xc9e8…f087)    
    2025-01-14 17:46:24 💤 Idle (0 peers), best: #2 (0xc9e8…f087), finalized #2 (0xc9e8…f087), ⬇ 0 ⬆ 0    
    2025-01-14 17:46:29 💤 Idle (0 peers), best: #2 (0xc9e8…f087), finalized #2 (0xc9e8…f087), ⬇ 0 ⬆ 0    
    2025-01-14 17:46:30 🙌 Starting consensus session on top of parent 0xc9e89c0b5cde3de6ddf7430c9f5951225aa06f906c27375002212b41acfef087 (#2)    
    2025-01-14 17:46:30 🎁 Prepared block for proposing at 3 (1 ms) [hash: 0x7103a33c5a61eb4ed39eae641e4cca6414c56af6fbe19ce9bae9dcae46f1a1f9; parent_hash: 0xc9e8…f087; extrinsics (2): [0x8a2b…b767, 0xd967…8e1b]    
    2025-01-14 17:46:30 🔖 Pre-sealed block for proposal at 3. Hash now 0xb3048c2267eed86ec3703c0d80857304e124be3b757ab54207ceedbb4ec88edd, previously 0x7103a33c5a61eb4ed39eae641e4cca6414c56af6fbe19ce9bae9dcae46f1a1f9.    
    2025-01-14 17:46:30 🏆 Imported #3 (0xc9e8…f087 → 0xb304…8edd)    
    ....
    ```
    
    If the number after `finalized` is increasing, your blockchain is producing new blocks and reaching consensus about the state they describe.
    
3. Keep the terminal displaying the node's output open to continue. You can use the `curl` command to check the block number and verify that the node is functioning correctly.

    ```bash
    curl -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' -H "Content-Type: application/json" http://localhost:9944 | jq
    ```

    The output:

    ```json
    {
        "jsonrpc": "2.0",
        "result": "0x1a",
        "id": 1
    }
    ```

Once the node is up and producing new blocks, you can connect to node to explore more advanced features, such as token transfer and contract development.
