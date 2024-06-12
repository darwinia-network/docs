# Run Development Testnet

While there is an established test network, namely the [Koi network](./koi.md), which serves as an ideal sandbox for your applications, eliminating any concern about initiating and connecting nodes, among other things. The official test network is designed to fulfill application developers' requirements. However, there may be scenarios where you want to perform low-level tasks. In such cases, creating your own development network can significantly enhance your development, testing, or debugging efficiency. This guide will walk you through the process of establishing a single-node development network.

## Compile darwinia node

1. Open a terminal shell on your computer.
2. Clone the darwinia repository by running the following command:
    
    ```bash
    git clone https://github.com/darwinia-network/darwinia.git
    ```
    
3. Change to the root of the repository and compile the node:
    
    ```bash
    cd darwinia
    cargo build --release -p darwinia --features koi-native
    ```
    
4. When the compilation is finished, something like this will be printed:
    
    ```bash
    ......
    Compiling polkadot-node-core-backing v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-gossip-support v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-node-core-dispute-coordinator v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-statement-distribution v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-availability-distribution v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-node-core-prospective-parachains v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-node-core-bitfield-signing v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-node-core-av-store v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-approval-distribution v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-availability-bitfield-distribution v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-node-core-pvf-checker v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-node-core-chain-selection v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-node-core-approval-voting v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-node-core-parachains-inherent v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling polkadot-node-core-chain-api v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling fc-db v2.0.0-dev (https://github.com/darwinia-network/frontier?branch=polkadot-v1.1.0-patch#a562b665)
    Compiling fc-mapping-sync v2.0.0-dev (https://github.com/darwinia-network/frontier?branch=polkadot-v1.1.0-patch#a562b665)
    Compiling cumulus-client-consensus-common v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling cumulus-pallet-aura-ext v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling cumulus-client-network v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling try-runtime-cli v0.10.0-dev (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling sc-storage-monitor v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling cumulus-client-collator v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling fc-rpc v2.0.0-dev (https://github.com/darwinia-network/frontier?branch=polkadot-v1.1.0-patch#a562b665)
    Compiling cumulus-relay-chain-rpc-interface v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling cumulus-relay-chain-minimal-node v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling cumulus-client-consensus-proposer v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling cumulus-client-cli v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling cumulus-client-consensus-aura v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling moonbeam-rpc-debug v0.1.0 (https://github.com/darwinia-network/moonbeam?branch=polkadot-v1.1.0#078eff3e)
    Compiling moonbeam-rpc-trace v0.6.0 (https://github.com/darwinia-network/moonbeam?branch=polkadot-v1.1.0#078eff3e)
    Compiling polkadot-service v1.0.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling cumulus-relay-chain-inprocess-interface v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Compiling cumulus-client-service v0.1.0 (https://github.com/paritytech/polkadot-sdk?branch=release-polkadot-v1.1.0#c8d2251c)
    Finished release [optimized] target(s) in 16m 12s
    ```
    

## Start the development node

After your node compiles, you are ready to start exploring what it does using the darwinia development node.

To start the local darwinia koi testnet node:

1. In the same terminal where you compiled your node, you can now start the node in development mode by running the following command:
    
    ```bash
    ./target/release/darwinia --chain koi-dev --alice --tmp --rpc-external --rpc-cors all
    ```
    
    The darwinia command-line options specify how you want the running node to operate. In this case, the `--dev` option specifies that the node runs in development mode using the predefined `development` chain specification. By default, this option also deletes all active data—such as keys, the blockchain database, and networking information when you stop the node by pressing `Ctrl-c`. Using the `--dev` option ensures that you have a clean working state any time you stop and restart the node.
    
2. Verify your node is up and running successfully by reviewing the output displayed in the terminal. The terminal should display output similar to this:
    
    ```bash
    2024-06-12 11:39:11 Darwinia    
    2024-06-12 11:39:11 ✌️  version 6.6.3-2dadcd456ab    
    2024-06-12 11:39:11 ❤️  by Darwinia Network <hello@darwinia.network>, 2018-2024    
    2024-06-12 11:39:11 📋 Chain specification: Darwinia Koi D    
    2024-06-12 11:39:11 🏷  Node name: Alice    
    2024-06-12 11:39:11 👤 Role: AUTHORITY    
    2024-06-12 11:39:11 💾 Database: RocksDb at /tmp/substrategTTTOz/chains/darwinia-koi-d/db/full    
    2024-06-12 11:39:12 Parachain id: Id(2105)    
    2024-06-12 11:39:12 Parachain Account: 5Ec4AhNxga1JYLioRBNxfRnovheDELVbZTRSnKMgvSVPvNcN    
    2024-06-12 11:39:12 Is collating: yes    
    2024-06-12 11:39:12 [pallet::staking] assembling new collators for new session 0 at #0    
    2024-06-12 11:39:12 [pallet::staking] assembling new collators for new session 1 at #0    
    2024-06-12 11:39:13 🔨 Initializing Genesis block/state (state: 0xed27…e560, header-hash: 0x1411…ebf9)    
    2024-06-12 11:39:14 🏷  Local node identity is: 12D3KooWJMkgwqQuq71NepWoZBsjk3EpZAxHeDdyhUF99zu86rVH    
    2024-06-12 11:39:14 💻 Operating system: linux    
    2024-06-12 11:39:14 💻 CPU architecture: x86_64    
    2024-06-12 11:39:14 💻 Target environment: gnu    
    2024-06-12 11:39:14 💻 CPU: AMD Ryzen 7 5700G with Radeon Graphics    
    2024-06-12 11:39:14 💻 CPU cores: 8    
    2024-06-12 11:39:14 💻 Memory: 63578MB    
    2024-06-12 11:39:14 💻 Kernel: 6.5.0-35-generic    
    2024-06-12 11:39:14 💻 Linux distribution: Ubuntu 22.04.4 LTS    
    2024-06-12 11:39:14 💻 Virtual machine: no    
    2024-06-12 11:39:14 📦 Highest known block at #0    
    2024-06-12 11:39:14 〽️ Prometheus exporter started at 127.0.0.1:9615    
    2024-06-12 11:39:14 Running JSON-RPC server: addr=0.0.0.0:9944, allowed origins=["*"]    
    2024-06-12 11:39:19 💤 Idle (0 peers), best: #0 (0x1411…ebf9), finalized #0 (0x1411…ebf9), ⬇ 0 ⬆ 0    
    2024-06-12 11:39:24 🙌 Starting consensus session on top of parent 0x14110d2746620059805fd18a6047003fcedf6c3f85642c968f7b398536abebf9    
    2024-06-12 11:39:24 🎁 Prepared block for proposing at 1 (0 ms) [hash: 0x7d3ce7da0e2850bc1cbba208f4c408ff5ed4732e3bb363409af5ba73df202cff; parent_hash: 0x1411…ebf9; extrinsics (2): [0xeb54…e7f6, 0x2934…47d2]    
    2024-06-12 11:39:24 🔖 Pre-sealed block for proposal at 1. Hash now 0x8d4eca909342cac95a7d4e4fc40eae0de9a3b781706838aa67a91ee5eb17c4e4, previously 0x7d3ce7da0e2850bc1cbba208f4c408ff5ed4732e3bb363409af5ba73df202cff.    
    2024-06-12 11:39:24 ✨ Imported #1 (0x8d4e…c4e4)    
    2024-06-12 11:39:24 💤 Idle (0 peers), best: #1 (0x8d4e…c4e4), finalized #1 (0x8d4e…c4e4), ⬇ 0 ⬆ 0    
    2024-06-12 11:39:29 💤 Idle (0 peers), best: #1 (0x8d4e…c4e4), finalized #1 (0x8d4e…c4e4), ⬇ 0 ⬆ 0    
    2024-06-12 11:39:34 💤 Idle (0 peers), best: #1 (0x8d4e…c4e4), finalized #1 (0x8d4e…c4e4), ⬇ 0 ⬆ 0    
    2024-06-12 11:39:36 🙌 Starting consensus session on top of parent 0x8d4eca909342cac95a7d4e4fc40eae0de9a3b781706838aa67a91ee5eb17c4e4    
    2024-06-12 11:39:36 🎁 Prepared block for proposing at 2 (0 ms) [hash: 0x65b1fd87b1ba6aa247a232f9f240eba0b44f27b8b61689e60ab6fd7bdbfae65b; parent_hash: 0x8d4e…c4e4; extrinsics (2): [0x2611…0617, 0xe585…ad8d]    
    2024-06-12 11:39:36 🔖 Pre-sealed block for proposal at 2. Hash now 0xa87b9c78352ce2e0f4ba2f2e10043b10b7cc49070ee6274199793b0c465263ae, previously 0x65b1fd87b1ba6aa247a232f9f240eba0b44f27b8b61689e60ab6fd7bdbfae65b.    
    2024-06-12 11:39:36 ✨ Imported #2 (0xa87b…63ae)    
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