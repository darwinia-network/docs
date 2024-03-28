# Run Relay Chain Testnet

Owner: bear.wang@itering.io

<aside>
💡 Familiarity with Linux/Mac command line is essential.

</aside>

# **Overview**

The Darwinia network is built upon the vision of the Polkadot. More specifically, the Darwinia chain functions as a parachain within the Polkadot Network, while the Crab chain operates as a parachain within the Kusama network. If you are not familiar with the relationship between the relay chain and the parachain, please read [Architecture Of Polkadot](https://wiki.polkadot.network/docs/learn-architecture) first. Sometimes, it becomes necessary to run a relay chain testnet to debug the interaction between the relay chain and parachain. This tutorial provides step-by-step instructions on setting up the environment to run a local relay chain testnet with registered parachains.

# **Start the relay chain node**

Before you can start block production for a parachain, you need to start a relay chain for them to connect to.

1. Open a terminal shell on your computer.
2. Create a work dirctory.
    
    Let's create a directory called `run-relay-chain` to store everything needed for setting up a relay chain network. As of the time of writing this doc(2023-08-15), the latest version of the Polkadot node is `v1.0.0`. Please ensure that you check for **[the latest version](https://github.com/paritytech/polkadot/releases)** when running your own node.
    
    ```bash
    wget https://github.com/paritytech/polkadot/releases/download/v1.0.0/polkadot
    ```
    
3. Export the local relay chain testnet specification.
    
    ```bash
    ./polkadot build-spec --chain rococo-local --disable-default-bootnode --raw > rococo-local.json
    ```
    
    You'll need to specify the path to the file in the commands to start the nodes.
    
4. Start the first validator using the `alice` account by running the following command:
    
    ```bash
    ./polkadot \
        --chain rococo-local.json \
        --alice \
        --validator \
        --base-path /tmp/relay/alice \
        --port 30333 \
        --rpc-port 9944 \
        --rpc-methods=Unsafe \
        --rpc-cors all \
        --rpc-external
    ```
    
    Make sure that the `--chain` command-line specifies the path to the chain specification you exported in the last step. This command also uses the default values for the port (`port`) and RPC port (`rpc-port`). The values are explicitly included here as a reminder to always check these settings. After the node starts, no other nodes on the same local machine can use these ports.
    
5. Review the alice node log messages as the node starts and take note of the Local node identity. You need to specify this identifier to enable other nodes to connect.
    
    ```bash
    2023-08-15 15:18:49 Parity Polkadot    
    2023-08-15 15:18:49 ✌️  version 1.0.0-1ed6e2e50a4    
    2023-08-15 15:18:49 ❤️  by Parity Technologies <admin@parity.io>, 2017-2023    
    2023-08-15 15:18:49 📋 Chain specification: Rococo Local Testnet    
    2023-08-15 15:18:49 🏷  Node name: Alice    
    2023-08-15 15:18:49 👤 Role: AUTHORITY    
    2023-08-15 15:18:49 💾 Database: RocksDb at /tmp/relay/alice/chains/rococo_local_testnet/db/full    
    2023-08-15 15:18:51 🔨 Initializing Genesis block/state (state: 0x56f4…7e84, header-hash: 0xfdd2…5ec3)    
    2023-08-15 15:18:51 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.    
    2023-08-15 15:18:51 👶 Creating empty BABE epoch changes on what appears to be first startup.    
    2023-08-15 15:18:51 🏷  Local node identity is: 12D3KooWMcssN3am9BtmSkeDPtMtzC4AwfPTTdDiFGdqbxhDVY7N
    ```
    
    `12D3KooWMcssN3am9BtmSkeDPtMtzC4AwfPTTdDiFGdqbxhDVY7N` is the identity of the alice relay chain node in this tutorial.
    
6. Open a new terminal and start the second validator using the `bob` account.
    
    The command similar to the command used to start the first node with a few important differences.
    
    ```bash
    ./polkadot \
        --chain rococo-local.json \
        --bob \
        --validator \
        --base-path /tmp/relay/bob \
        --port 30334 \
        --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWMcssN3am9BtmSkeDPtMtzC4AwfPTTdDiFGdqbxhDVY7N \
        --rpc-port 9945 \
        --rpc-methods=Unsafe \
        --rpc-cors all \
        --rpc-external
    ```
    
    Notice that this command uses a different base path ( `/tmp/relay/bob`), validator key (`--bob`), and ports (`30334` and `9945`).  It is important to mention that you also need to specify the `bootnodes` options for the alice relay chain node identity.
    
7. Verify your node is up and running successfully by reviewing the bob node output displayed in the terminal. The terminal should display output similar to this:
    
    ```bash
    2023-08-15 15:21:08 Parity Polkadot    
    2023-08-15 15:21:08 ✌️  version 1.0.0-1ed6e2e50a4    
    2023-08-15 15:21:08 ❤️  by Parity Technologies <admin@parity.io>, 2017-2023    
    2023-08-15 15:21:08 📋 Chain specification: Rococo Local Testnet    
    2023-08-15 15:21:08 🏷  Node name: Bob    
    2023-08-15 15:21:08 👤 Role: AUTHORITY    
    2023-08-15 15:21:08 💾 Database: RocksDb at /tmp/relay/bob/chains/rococo_local_testnet/db/full    
    2023-08-15 15:21:10 🔨 Initializing Genesis block/state (state: 0x56f4…7e84, header-hash: 0xfdd2…5ec3)    
    2023-08-15 15:21:10 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.    
    2023-08-15 15:21:11 👶 Creating empty BABE epoch changes on what appears to be first startup.    
    2023-08-15 15:21:11 🏷  Local node identity is: 12D3KooWPs5ALUGa9jmVnWkfmYKL86F7MeXtby7xXYWN7Faoon8f    
    2023-08-15 15:21:11 💻 Operating system: linux    
    2023-08-15 15:21:11 💻 CPU architecture: x86_64    
    2023-08-15 15:21:11 💻 Target environment: gnu    
    2023-08-15 15:21:11 💻 CPU: AMD Ryzen 7 5700G with Radeon Graphics    
    2023-08-15 15:21:11 💻 CPU cores: 8    
    2023-08-15 15:21:11 💻 Memory: 63576MB    
    2023-08-15 15:21:11 💻 Kernel: 6.2.0-26-generic    
    2023-08-15 15:21:11 💻 Linux distribution: Ubuntu 22.04.2 LTS    
    2023-08-15 15:21:11 💻 Virtual machine: no    
    2023-08-15 15:21:11 📦 Highest known block at #0    
    2023-08-15 15:21:11 Running JSON-RPC server: addr=0.0.0.0:9945, allowed origins=["*"]    
    2023-08-15 15:21:11 🏁 CPU score: 1.34 GiBs    
    2023-08-15 15:21:11 🏁 Memory score: 13.85 GiBs    
    2023-08-15 15:21:11 🏁 Disk score (seq. writes): 1.72 GiBs    
    2023-08-15 15:21:11 🏁 Disk score (rand. writes): 725.38 MiBs
    2023-08-15 15:21:11 Starting with an empty approval vote DB.
    2023-08-15 15:21:11 👶 Starting BABE Authorship worker    
    2023-08-15 15:21:11 🥩 BEEFY gadget waiting for BEEFY pallet to become available...    
    2023-08-15 15:21:11 discovered: 12D3KooWMcssN3am9BtmSkeDPtMtzC4AwfPTTdDiFGdqbxhDVY7N /ip4/192.168.31.52/tcp/30333    
    2023-08-15 15:21:16 💤 Idle (1 peers), best: #0 (0xfdd2…5ec3), finalized #0 (0xfdd2…5ec3), ⬇ 1.4kiB/s ⬆ 1.4kiB/s    
    2023-08-15 15:21:18 🙌 Starting consensus session on top of parent 0xfdd25265d4c8a26c0c7a9ba6127d825f8b63343c8c239a1feea964d6f6ed5ec3    
    2023-08-15 15:21:20 ParentBlockRandomness did not provide entropy    
    2023-08-15 15:21:20 ParentBlockRandomness did not provide entropy    
    2023-08-15 15:21:20 🎁 Prepared block for proposing at 1 (1 ms) [hash: 0x609758e21dab765fa6d6b3bb20c0d0a3c86a15fe5d3909d1e68ba319fa6209a9; parent_hash: 0xfdd2…5ec3; extrinsics (2): [0xeefb…9ae0, 0x3bb3…d7f3]    
    2023-08-15 15:21:20 🔖 Pre-sealed block for proposal at 1. Hash now 0xbb2709d6d328305210f45bc1807547949013feaaa9f15f0ce994d41947c83536, previously 0x609758e21dab765fa6d6b3bb20c0d0a3c86a15fe5d3909d1e68ba319fa6209a9.    
    2023-08-15 15:21:20 👶 New epoch 0 launching at block 0xbb27…3536 (block slot 282014013 >= start slot 282014013).    
    2023-08-15 15:21:20 👶 Next epoch starts at slot 282014023    
    2023-08-15 15:21:20 ✨ Imported #1 (0xbb27…3536)    
    2023-08-15 15:21:21 💤 Idle (1 peers), best: #1 (0xbb27…3536), finalized #0 (0xfdd2…5ec3), ⬇ 0.3kiB/s ⬆ 0.5kiB/s    
    2023-08-15 15:21:24 🙌 Starting consensus session on top of parent 0xbb2709d6d328305210f45bc1807547949013feaaa9f15f0ce994d41947c83536    
    2023-08-15 15:21:24 🎁 Prepared block for proposing at 2 (0 ms) [hash: 0xfa4410daa931cfe05874593793716720358c0ea87539f8806c4b9c552794fc30; parent_hash: 0xbb27…3536; extrinsics (2): [0x9135…0ae2, 0xef7a…1dac]    
    2023-08-15 15:21:24 🔖 Pre-sealed block for proposal at 2. Hash now 0xff99c4d30c95d3c16dbda56be183e087410ddfc8c8d8f30afd8ba79735ad6eae, previously 0xfa4410daa931cfe05874593793716720358c0ea87539f8806c4b9c552794fc30.    
    2023-08-15 15:21:24 ✨ Imported #2 (0xff99…6eae)    
    2023-08-15 15:21:26 💤 Idle (1 peers), best: #2 (0xff99…6eae), finalized #0 (0xfdd2…5ec3), ⬇ 0.4kiB/s ⬆ 0.6kiB/s    
    2023-08-15 15:21:30 ✨ Imported #3 (0x76de…bee4)    
    2023-08-15 15:21:31 💤 Idle (1 peers), best: #3 (0x76de…bee4), finalized #0 (0xfdd2…5ec3), ⬇ 0.4kiB/s ⬆ 0.2kiB/s    
    2023-08-15 15:21:35 🥩 BEEFY pallet available: block 1 beefy genesis 1    
    2023-08-15 15:21:35 🥩 Loading BEEFY voter state from genesis on what appears to be first startup. Starting voting rounds at block 1, genesis validator set ValidatorSet { validators: [Public(020a1091341fe5664bfa1782d5e04779689068c916b04cb365ec3153755684d9a1 (1CoWvCok...)), Public(0390084fdbf27d2b79d26a4f13f0ccd982cb755a661969143c37cbc49ef5b91f27 (1Mcq981h...))], id: 0 }.    
    2023-08-15 15:21:35 🥩 write aux schema version 4    
    2023-08-15 15:21:35 🥩 run BEEFY worker, best grandpa: #1.    
    2023-08-15 15:21:35 🥩 Round #1 concluded, finality_proof: V1(SignedCommitment { commitment: Commitment { payload: Payload([([109, 104], [232, 60, 50, 153, 220, 153, 174, 174, 237, 44, 103, 150, 160, 255, 190, 247, 13, 109, 168, 101, 231, 195, 64, 10, 19, 12, 24, 244, 235, 50, 80, 100])]), block_number: 1, validator_set_id: 0 }, signatures: [Some(Signature(f416d92165642d317f0415fa85c38930e7eacb5c8cde4f2018a6c45e1241036c170e7d3ce2c926b8db526baee33eb3268bb13aac029c5d02b18fe78dcd3a59c800)), Some(Signature(ca8b7adeaa1f362c70f1cda3ade270a1c92a5e3045af479cbde6063061f569600d71499195730c7d6975aeb10cd604b24e514310ff3f0e81cf6abf0e30fa4cd801))] }).    
    2023-08-15 15:21:36 🙌 Starting consensus session on top of parent 0x76de07890819b17436cf870af294c97ed42f3f8e7735439668331fee7f32bee4    
    2023-08-15 15:21:36 🎁 Prepared block for proposing at 4 (0 ms) [hash: 0x5db1031ce3ee02ed6f48feacecc9df55d8db2aed07da1d2d60eb55fb7b153eb1; parent_hash: 0x76de…bee4; extrinsics (2): [0x87ba…1846, 0x01c5…034c]    
    2023-08-15 15:21:36 🔖 Pre-sealed block for proposal at 4. Hash now 0x262ca95317722f692ae8b8f17f73489d3000a89ad9d9eda20f27fa13e2d70983, previously 0x5db1031ce3ee02ed6f48feacecc9df55d8db2aed07da1d2d60eb55fb7b153eb1.    
    2023-08-15 15:21:36 ✨ Imported #4 (0x262c…0983)    
    2023-08-15 15:21:36 💤 Idle (1 peers), best: #4 (0x262c…0983), finalized #1 (0xbb27…3536), ⬇ 0.3kiB/s ⬆ 0.5kiB/s    
    2023-08-15 15:21:41 💤 Idle (1 peers), best: #4 (0x262c…0983), finalized #2 (0xff99…6eae), ⬇ 0.2kiB/s ⬆ 0.2kiB/s    
    2023-08-15 15:21:42 🙌 Starting consensus session on top of parent 0x262ca95317722f692ae8b8f17f73489d3000a89ad9d9eda20f27fa13e2d70983    
    2023-08-15 15:21:42 🎁 Prepared block for proposing at 5 (1 ms) [hash: 0xb5a4cbcdae03fa1afde70bb4a38f66d83457986db20513374509cd40df2c650b; parent_hash: 0x262c…0983; extrinsics (2): [0x9aca…e288, 0xd0b4…1357]    
    2023-08-15 15:21:42 🔖 Pre-sealed block for proposal at 5. Hash now 0x50bdeb60701859999234c0ef477e5bb46cb3530411d5aa5c5ca824805cb1f9b4, previously 0xb5a4cbcdae03fa1afde70bb4a38f66d83457986db20513374509cd40df2c650b.    
    2023-08-15 15:21:42 ✨ Imported #5 (0x50bd…f9b4)    
    2023-08-15 15:21:46 💤 Idle (1 peers), best: #5 (0x50bd…f9b4), finalized #2 (0xff99…6eae), ⬇ 0.4kiB/s ⬆ 0.6kiB/s    
    2023-08-15 15:21:48 🙌 Starting consensus session on top of parent 0x50bdeb60701859999234c0ef477e5bb46cb3530411d5aa5c5ca824805cb1f9b4    
    2023-08-15 15:21:48 🎁 Prepared block for proposing at 6 (1 ms) [hash: 0xf77ac618582490e98aea6cc888a1aef3c909243b2a2b83f7af77c9a56a157b81; parent_hash: 0x50bd…f9b4; extrinsics (2): [0x67ac…bdcb, 0x8082…e872]    
    2023-08-15 15:21:48 🔖 Pre-sealed block for proposal at 6. Hash now 0xdb65648db04783a9f7444d23c5640c440664ab474d13418191cf123b030d0b0b, previously 0xf77ac618582490e98aea6cc888a1aef3c909243b2a2b83f7af77c9a56a157b81.    
    2023-08-15 15:21:48 ✨ Imported #6 (0xdb65…0b0b)    
    2023-08-15 15:21:51 💤 Idle (1 peers), best: #6 (0xdb65…0b0b), finalized #3 (0x76de…bee4), ⬇ 0.2kiB/s ⬆ 0.5kiB/s    
    2023-08-15 15:21:54 🙌 Starting consensus session on top of parent 0xdb65648db04783a9f7444d23c5640c440664ab474d13418191cf123b030d0b0b    
    2023-08-15 15:21:54 🎁 Prepared block for proposing at 7 (1 ms) [hash: 0x68c53155adc645cfe47046fafda6dd06aebbe44a94a4909415f10f0a29aea9cc; parent_hash: 0xdb65…0b0b; extrinsics (2): [0xea6e…c7f4, 0x0cc5…f6ec]    
    2023-08-15 15:21:54 🔖 Pre-sealed block for proposal at 7. Hash now 0xfc99b2d4e8aace9ee1f18e29925f7e0c891b8fbf4dd60a8dec1be0e4eb76e943, previously 0x68c53155adc645cfe47046fafda6dd06aebbe44a94a4909415f10f0a29aea9cc.    
    2023-08-15 15:21:54 ✨ Imported #7 (0xfc99…e943)    
    2023-08-15 15:21:56 💤 Idle (1 peers), best: #7 (0xfc99…e943), finalized #4 (0x262c…0983), ⬇ 0.4kiB/s ⬆ 0.6kiB/s    
    2023-08-15 15:22:00 ✨ Imported #8 (0x7ff6…e18f)    
    2023-08-15 15:22:01 💤 Idle (1 peers), best: #8 (0x7ff6…e18f), finalized #5 (0x50bd…f9b4), ⬇ 0.4kiB/s ⬆ 0.2kiB/s    
    2023-08-15 15:22:06 ✨ Imported #9 (0xf440…367a)    
    2023-08-15 15:22:06 💤 Idle (1 peers), best: #9 (0xf440…367a), finalized #6 (0xdb65…0b0b), ⬇ 0.5kiB/s ⬆ 0.2kiB/s    
    2023-08-15 15:22:11 💤 Idle (1 peers), best: #9 (0xf440…367a), finalized #6 (0xdb65…0b0b), ⬇ 0.2kiB/s ⬆ 0.2kiB/s
    
    ```
    
    ```bash
    2023-08-15 15:22:11 💤 Idle (1 peers), best: #9 (0xf440…367a), finalized #6 (0xdb65…0b0b), ⬇ 0.2kiB/s ⬆ 0.2kiB/s
    ```
    
    This log indicates that the relay chain has started to produce blocks and is working as intended.
    

# Start the parachain node

With the local relay chain running, you are ready to start the parachain collator node and export information about its runtime and genesis state.

1. Open a new terminal shell on your computer.
2. Prepare the darwinia parachain node binary
    
    As of the time of writing this doc(2023-08-15), the latest version of the Darwinia node is `v6.4.0`. Please ensure that you check for **[the latest version](https://github.com/darwinia-network/darwinia/releases)** when running your own node.
    
    ```bash
    wget https://github.com/darwinia-network/darwinia/releases/download/pango-6400/darwinia-x86_64-linux-gnu.tar.bz2
    tar xvf darwinia-x86_64-linux-gnu.tar.bz2
    ```
    
3. Export the local parachain chain testnet specification.
    
    ```bash
    ./darwinia build-spec --chain pangolin-local --disable-default-bootnode > darwinia-spec.json
    ```
    
    You'll need to specify the path to the file in the commands to start the nodes.
    
4. Export the WebAssembly runtime for the parachain.
    
    The relay chain needs the parachain-specific runtime validation logic to validate parachain blocks. You can export the WebAssembly runtime for a parachain collator node by running a command similar to the following:
    
    ```bash
    /darwinia export-genesis-wasm --chain darwinia-spec.json > genesis-wasm
    ```
    
5. Generate a parachain genesis state.
    
    To register a parachain, the relay chain needs to know the genesis state of the parachain. You can export the entire genesis state—hex-encoded—to a file by running a command similar to the following:
    
    ```bash
    ./darwinia export-genesis-state --chain darwinia-spec.json > genesis-state
    ```
    
6. Start the first validator using the `alice` account by running the following command:
    
    ```bash
    ./darwinia \
        --name "Alice" \
        --chain darwinia-spec.json \
        --base-path /tmp/para/alice \
        --rpc-methods=Unsafe \
        --rpc-cors=all \
        --rpc-external \
        --rpc-max-connections=1000 \
        --port 40335 \
        --rpc-port 10044 \
        --alice \
        --force-authoring \
        --collator \
        -- \
        --chain rococo-local.json \
        --port 30335 \
        --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWMcssN3am9BtmSkeDPtMtzC4AwfPTTdDiFGdqbxhDVY7N \
        --rpc-port 9946
    ```
    
    In this command, the arguments passed before the lone `--` argument are for the parachain collator. The arguments after the `--` are for the embedded relay chain node. Notice that this command specifies both the chain specification for the parachain and the chain specification for the relay chain. Ensure that the `bootnodes` option specifies one of the local relay chain nodes.
    
    In the terminal where you started the `alice` node, you should see output similar to the following:
    
    ```bash
    2023-08-15 16:21:45 Darwinia    
    2023-08-15 16:21:45 ✌️  version 6.3.4-8c0457841c7    
    2023-08-15 16:21:45 ❤️  by Darwinia Network <hello@darwinia.network>, 2018-2023    
    2023-08-15 16:21:45 📋 Chain specification: Pangolin2 Local    
    2023-08-15 16:21:45 🏷  Node name: Alice    
    2023-08-15 16:21:45 👤 Role: AUTHORITY    
    2023-08-15 16:21:45 💾 Database: RocksDb at /tmp/para/alice/chains/pangolin2-local/db/full    
    2023-08-15 16:21:45 ⛓  Native runtime: Pangolin2-6400 (DarwiniaOfficialRust-0.tx0.au0)    
    2023-08-15 16:21:47 [pallet::staking] assembling new collators for new session 0 at #0    
    2023-08-15 16:21:47 [pallet::staking] assembling new collators for new session 1 at #0    
    2023-08-15 16:21:47 Parachain id: Id(2105)    
    2023-08-15 16:21:47 Parachain Account: 5Ec4AhNxga1JYLioRBNxfRnovheDELVbZTRSnKMgvSVPvNcN    
    2023-08-15 16:21:47 Parachain genesis state: 0x000000000000000000000000000000000000000000000000000000000000000000ce905c0de2026c714a75f2026a5a4fe7636d654b05ac76a9bc5c5bceed8e91dc03170a2e7597b7b7e3d84c05391d139a62b157e78786d8c082f29dcf4c11131400    
    2023-08-15 16:21:47 Is collating: yes    
    2023-08-15 16:21:47 [Parachain] [pallet::staking] assembling new collators for new session 0 at #0    
    2023-08-15 16:21:47 [Parachain] [pallet::staking] assembling new collators for new session 1 at #0    
    2023-08-15 16:21:48 [Parachain] 🔨 Initializing Genesis block/state (state: 0xce90…91dc, header-hash: 0xe9fc…f482)    
    2023-08-15 16:21:49 [Relaychain] 🔨 Initializing Genesis block/state (state: 0x56f4…7e84, header-hash: 0xfdd2…5ec3)    
    2023-08-15 16:21:49 [Relaychain] 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.    
    2023-08-15 16:21:50 [Relaychain] 👶 Creating empty BABE epoch changes on what appears to be first startup.    
    2023-08-15 16:21:50 [Relaychain] 🏷  Local node identity is: 12D3KooW9vfzADPPTXdrKfrXfiLLirUCFTLK3agW182xDdC22Km9    
    2023-08-15 16:21:50 [Relaychain] 💻 Operating system: linux    
    2023-08-15 16:21:50 [Relaychain] 💻 CPU architecture: x86_64    
    2023-08-15 16:21:50 [Relaychain] 💻 Target environment: gnu    
    2023-08-15 16:21:50 [Relaychain] 💻 CPU: AMD Ryzen 7 5700G with Radeon Graphics    
    2023-08-15 16:21:50 [Relaychain] 💻 CPU cores: 8    
    2023-08-15 16:21:50 [Relaychain] 💻 Memory: 63576MB    
    2023-08-15 16:21:50 [Relaychain] 💻 Kernel: 6.2.0-26-generic    
    2023-08-15 16:21:50 [Relaychain] 💻 Linux distribution: Ubuntu 22.04.2 LTS    
    2023-08-15 16:21:50 [Relaychain] 💻 Virtual machine: no    
    2023-08-15 16:21:50 [Relaychain] 📦 Highest known block at #0    
    2023-08-15 16:21:50 [Relaychain] Running JSON-RPC server: addr=127.0.0.1:9946, allowed origins=["http://localhost:*", "http://127.0.0.1:*", "https://localhost:*", "https://127.0.0.1:*", "https://polkadot.js.org"]    
    2023-08-15 16:21:50 [Relaychain] 🏁 CPU score: 1.33 GiBs    
    2023-08-15 16:21:50 [Relaychain] 〽️ Prometheus exporter started at 127.0.0.1:9616    
    2023-08-15 16:21:50 [Relaychain] 🏁 Memory score: 14.97 GiBs    
    2023-08-15 16:21:50 [Relaychain] 🏁 Disk score (seq. writes): 1.59 GiBs    
    2023-08-15 16:21:50 [Relaychain] 🏁 Disk score (rand. writes): 751.41 MiBs    
    2023-08-15 16:21:50 [Relaychain] Starting with an empty approval vote DB.
    2023-08-15 16:21:50 [Parachain] 🏷  Local node identity is: 12D3KooWMSB38GPZdSJNAYweQ7FisAL94qDLMA9SFMu8XNyNRcGj    
    2023-08-15 16:21:50 [Relaychain] discovered: 12D3KooWPs5ALUGa9jmVnWkfmYKL86F7MeXtby7xXYWN7Faoon8f /ip4/192.168.31.52/tcp/30334    
    2023-08-15 16:21:50 [Relaychain] discovered: 12D3KooWMcssN3am9BtmSkeDPtMtzC4AwfPTTdDiFGdqbxhDVY7N /ip4/192.168.31.52/tcp/30333    
    2023-08-15 16:21:50 [Relaychain] ParentBlockRandomness did not provide entropy    
    2023-08-15 16:21:50 [Parachain] 💻 Operating system: linux    
    2023-08-15 16:21:50 [Parachain] 💻 CPU architecture: x86_64    
    2023-08-15 16:21:50 [Parachain] 💻 Target environment: gnu    
    2023-08-15 16:21:50 [Parachain] 💻 CPU: AMD Ryzen 7 5700G with Radeon Graphics    
    2023-08-15 16:21:50 [Parachain] 💻 CPU cores: 8    
    2023-08-15 16:21:50 [Parachain] 💻 Memory: 63576MB    
    2023-08-15 16:21:50 [Parachain] 💻 Kernel: 6.2.0-26-generic    
    2023-08-15 16:21:50 [Parachain] 💻 Linux distribution: Ubuntu 22.04.2 LTS    
    2023-08-15 16:21:50 [Parachain] 💻 Virtual machine: no    
    2023-08-15 16:21:50 [Parachain] 📦 Highest known block at #0    
    2023-08-15 16:21:50 [Parachain] Running JSON-RPC server: addr=0.0.0.0:10044, allowed origins=["*"]    
    2023-08-15 16:21:50 [Parachain] 🏁 CPU score: 1.33 GiBs    
    2023-08-15 16:21:50 [Parachain] 🏁 Memory score: 14.97 GiBs    
    2023-08-15 16:21:50 [Parachain] 🏁 Disk score (seq. writes): 1.59 GiBs    
    2023-08-15 16:21:50 [Parachain] 🏁 Disk score (rand. writes): 751.41 MiBs    
    2023-08-15 16:21:50 [Parachain] discovered: 12D3KooWPs5ALUGa9jmVnWkfmYKL86F7MeXtby7xXYWN7Faoon8f /ip4/192.168.31.52/tcp/30334    
    2023-08-15 16:21:50 [Parachain] discovered: 12D3KooWMcssN3am9BtmSkeDPtMtzC4AwfPTTdDiFGdqbxhDVY7N /ip4/192.168.31.52/tcp/30333    
    2023-08-15 16:21:54 [Relaychain] ✨ Imported #607 (0x9c46…831a)    
    2023-08-15 16:21:55 [Relaychain] 💤 Idle (2 peers), best: #607 (0x9c46…831a), finalized #604 (0x996f…86cd), ⬇ 120.3kiB/s ⬆ 3.0kiB/s    
    2023-08-15 16:21:55 [Parachain] 💤 Idle (0 peers), best: #0 (0xe9fc…f482), finalized #0 (0xe9fc…f482), ⬇ 1.0kiB/s ⬆ 0.5kiB/s    
    2023-08-15 16:22:00 [Relaychain] ✨ Imported #608 (0xa192…89c2)    
    2023-08-15 16:22:00 [Relaychain] 💤 Idle (2 peers), best: #608 (0xa192…89c2), finalized #605 (0xfec8…0b57), ⬇ 1.6kiB/s ⬆ 0.8kiB/s    
    2023-08-15 16:22:00 [Parachain] 💤 Idle (0 peers), best: #0 (0xe9fc…f482), finalized #0 (0xe9fc…f482), ⬇ 45 B/s ⬆ 45 B/s    
    2023-08-15 16:22:05 [Relaychain] 💤 Idle (2 peers), best: #608 (0xa192…89c2), finalized #606 (0xa1e2…f4c4), ⬇ 1.1kiB/s ⬆ 0.5kiB/s    
    2023-08-15 16:22:05 [Parachain] 💤 Idle (0 peers), best: #0 (0xe9fc…f482), finalized #0 (0xe9fc…f482), ⬇ 0.1kiB/s ⬆ 66 B/s    
    2023-08-15 16:22:06 [Relaychain] ✨ Imported #609 (0x0a7f…85aa)    
    2023-08-15 16:22:06 [Relaychain] ✨ Imported #609 (0xfb83…08ba)    
    2023-08-15 16:22:10 [Relaychain] 💤 Idle (2 peers), best: #609 (0x0a7f…85aa), finalized #606 (0xa1e2…f4c4), ⬇ 1.4kiB/s ⬆ 0.7kiB/s    
    2023-08-15 16:22:10 [Parachain] 💤 Idle (0 peers), best: #0 (0xe9fc…f482), finalized #0 (0xe9fc…f482), ⬇ 0.2kiB/s ⬆ 0.1kiB/s    
    2023-08-15 16:22:12 [Relaychain] ✨ Imported #610 (0x883b…b5c2)    
    2023-08-15 16:22:15 [Relaychain] 💤 Idle (2 peers), best: #610 (0x883b…b5c2), finalized #607 (0x9c46…831a), ⬇ 0.8kiB/s ⬆ 0.5kiB/s    
    2023-08-15 16:22:15 [Parachain] 💤 Idle (0 peers), best: #0 (0xe9fc…f482), finalized #0 (0xe9fc…f482), ⬇ 0.1kiB/s ⬆ 61 B/s    
    2023-08-15 16:22:18 [Relaychain] 👶 New epoch 61 launching at block 0x5f18…813e (block slot 282014623 >= start slot 282014623).    
    2023-08-15 16:22:18 [Relaychain] 👶 Next epoch starts at slot 282014633    
    2023-08-15 16:22:18 [Relaychain] ✨ Imported #611 (0x5f18…813e)    
    2023-08-15 16:22:20 [Relaychain] 💤 Idle (2 peers), best: #611 (0x5f18…813e), finalized #608 (0xa192…89c2), ⬇ 1.6kiB/s ⬆ 0.7kiB/s    
    2023-08-15 16:22:20 [Parachain] 💤 Idle (0 peers), best: #0 (0xe9fc…f482), finalized #0 (0xe9fc…f482), ⬇ 0.1kiB/s ⬆ 0.1kiB/s    
    2023-08-15 16:22:24 [Relaychain] ✨ Imported #612 (0xccbc…4c7d)    
    2023-08-15 16:22:25 [Relaychain] 💤 Idle (2 peers), best: #612 (0xccbc…4c7d), finalized #609 (0x0a7f…85aa), ⬇ 0.9kiB/s ⬆ 0.6kiB/s    
    2023-08-15 16:22:25 [Parachain] 💤 Idle (0 peers), best: #0 (0xe9fc…f482), finalized #0 (0xe9fc…f482), ⬇ 0.2kiB/s ⬆ 0.1kiB/s    
    2023-08-15 16:22:30 [Relaychain] ✨ Imported #613 (0x58a1…81a1)    
    2023-08-15 16:22:30 [Relaychain] 💤 Idle (2 peers), best: #613 (0x58a1…81a1), finalized #610 (0x883b…b5c2), ⬇ 1.0kiB/s ⬆ 0.6kiB/s    
    2023-08-15 16:22:30 [Parachain] 💤 Idle (0 peers), best: #0 (0xe9fc…f482), finalized #0 (0xe9fc…f482), ⬇ 0.1kiB/s ⬆ 66 B/s    
    2023-08-15 16:22:35 [Relaychain] 💤 Idle (2 peers), best: #613 (0x58a1…81a1), finalized #610 (0x883b…b5c2), ⬇ 0.4kiB/s ⬆ 0.3kiB/s    
    2023-08-15 16:22:35 [Parachain] 💤 Idle (0 peers), best: #0 (0xe9fc…f482), finalized #0 (0xe9fc…f482), ⬇ 0.1kiB/s ⬆ 55 B/s    
    2023-08-15 16:22:35 [Relaychain] 👴 Applying authority set change scheduled at block #611    
    2023-08-15 16:22:35 [Relaychain] 👴 Applying GRANDPA set change to new set [(Public(88dc3417d5058ec4b4503e0c12ea1a0a89be200fe98922423d4334014fa6b0ee (5FA9nQDV...)), 1), (Public(d17c2d7823ebf260fd138f2d7e27d114c0145d968b5ff5006125f2414fadae69 (5GoNkf6W...)), 1)]
    ```
    
    ```bash
    2023-08-15 16:23:45 [Relaychain] 💤 Idle (2 peers), best: #625 (0x421f…bad6), finalized #622 (0x84ca…8dcd), ⬇ 0.7kiB/s ⬆ 0.3kiB/s
    ```
    
    This log indicates that the relay chain node embedded in your parachain node has connected to the running relay chain validators.
    
7. Open a new terminal and start the second validator using the `bob` account.
    
    The command similar to the command used to start the alice parachain node with a few important differences.
    
    ```bash
    ./darwinia \
        --name "Bob" \
        --chain darwinia-spec.json \
        --base-path /tmp/para/bob \
        --rpc-methods=Unsafe \
        --rpc-cors=all \
        --rpc-external \
        --rpc-max-connections=1000 \
        --frontier-backend-type sql \
        --port 40336 \
        --rpc-port 10045 \
        --bootnodes /ip4/127.0.0.1/tcp/40335/p2p/12D3KooWMSB38GPZdSJNAYweQ7FisAL94qDLMA9SFMu8XNyNRcGj \
        --bob \
        --force-authoring \
        --collator \
        -- \
        --chain rococo-local.json \
        --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWMcssN3am9BtmSkeDPtMtzC4AwfPTTdDiFGdqbxhDVY7N \
        --port 30336 \
        --rpc-port 9947
    ```
    
    Notice that this command uses a different base path ( `/tmp/para/bob`), collator key (`--bob`), and ports.  It is important to mention that you must specify the correct `bootnodes` options for both the parachain and the relay chain.
    
8. Open a new terminal and start the second validator using the `charlie` account.
    
    The command similar to the command used to start the alice parachain node with a few important differences.
    
    ```bash
    ./darwinia \
        --name "Charlie" \
        --chain darwinia-spec.json \
        --base-path /tmp/para/charlie \
        --rpc-methods=Unsafe \
        --rpc-cors=all \
        --rpc-external \
        --rpc-max-connections=1000 \
        --frontier-backend-type sql \
        --port 40337 \
        --rpc-port 10046 \
        --bootnodes /ip4/127.0.0.1/tcp/40335/p2p/12D3KooWMSB38GPZdSJNAYweQ7FisAL94qDLMA9SFMu8XNyNRcGj \
        --charlie \
        --force-authoring \
        --collator \
        -- \
        --chain rococo-local.json \
        --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWMcssN3am9BtmSkeDPtMtzC4AwfPTTdDiFGdqbxhDVY7N \
        --port 30337 \
        --rpc-port 9948
    ```
    
    Notice that this command uses a different base path ( `/tmp/para/charlie`), collator key (`--charlie`), and ports.  It is important to mention that you must specify the correct bootnodes options for both the parachain and the relay chain.
    

# **Register with the local relay chain**

With the local relay chain and collator node running, you are ready to register the parachain on the local relay chain. In a live public network, registration typically involves a [parachain auction](https://wiki.polkadot.network/docs/en/learn-auction). For this tutorial and local testing, you can use a Sudo transaction and the Polkadot/Substrate Portal. Using a Sudo transaction enables you to bypass the steps required to acquire a parachain or parathread slot.

To register the parachain:

1. Validate your local relay chain validators are running.
2. Open the [Polkadot/Substrate Portal](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/parachains/parathreads) in a browser.
3. Connect to a local relay chain node, and click **Developer** and select **Sudo**.
    
    ![Screenshot from 2023-08-15 16-52-24.png](Run%20Relay%20Chain%20Testnet%2058df644b055648c984de3d33ccc2ba9a/Screenshot_from_2023-08-15_16-52-24.png)
    
4. Select **paraSudoWrapper**, then select **sudoScheduleParaInitialize(id, genesis)** to initialize the reserved paraID at the start of the next relay chain session.
    
    For the transaction parameters:
    
    - `id`: Type your reserved `ParaId`. For this tutorial, the reserved identifier is `2105`.
    - `genesisHead`: Click **file upload** and upload the genesis state you exported for the parachain. For this tutorial, select the `genesis-state` file.
    - `validationCode`: Click **file upload** and upload the WebAssembly runtime you exported for the parachain For this tutorial, select the `genesis-wasm` file.
    - `paraKind`: Select **Yes**.
    
    ![Screenshot from 2023-08-15 17-01-04.png](Run%20Relay%20Chain%20Testnet%2058df644b055648c984de3d33ccc2ba9a/Screenshot_from_2023-08-15_17-01-04.png)
    
5. Click **Submit Sudo**.
6. Review the transaction details, then click **Sign and Submit** to authorize the transaction.
    
    After you submit the transaction, click **Network** and select **Explorer**. Check the list of recent events for successful `sudo.Sudid` *and* `paras.PvfCheckAccepted` and click the event to see details about the transaction.
    
    ![Screenshot from 2023-08-15 17-01-55.png](Run%20Relay%20Chain%20Testnet%2058df644b055648c984de3d33ccc2ba9a/Screenshot_from_2023-08-15_17-01-55.png)
    
7. Click **Network** and select **Parachains** and wait for a new epoch to start.
    
    ![Screenshot from 2023-08-15 17-03-54.png](Run%20Relay%20Chain%20Testnet%2058df644b055648c984de3d33ccc2ba9a/Screenshot_from_2023-08-15_17-03-54.png)
    
    The terminal where the parachain node is running also displays details similar to the following:
    
    ```bash
    023-08-15 17:07:06 [Parachain] Starting collation. relay_parent=0xc1597ee7e74d9b828cd4f5d0ee42e773ca2b0e71219d5c21dffeb25255f1a01e at=0x692ed576627e90c8761c1565ae462b775d846a7541b8ffcc4f23ad0b9da0ad69
    2023-08-15 17:07:06 [Parachain] 🙌 Starting consensus session on top of parent 0x692ed576627e90c8761c1565ae462b775d846a7541b8ffcc4f23ad0b9da0ad69    
    2023-08-15 17:07:06 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.    
    2023-08-15 17:07:06 [Parachain] 🎁 Prepared block for proposing at 20 (0 ms) [hash: 0x8112f315abab76d492752d290adbea64a319257f7eabc11fb4bfe7360730364e; parent_hash: 0x692e…ad69; extrinsics (2): [0xfe56…3f8c, 0xe89f…8e0e]]    
    2023-08-15 17:07:06 [Parachain] 🔖 Pre-sealed block for proposal at 20. Hash now 0x0fe9ae36a7f8ccd29b397782dfe3fe6e31cbd06f6b6bf8db5e95af8caf86fe5e, previously 0x8112f315abab76d492752d290adbea64a319257f7eabc11fb4bfe7360730364e.    
    2023-08-15 17:07:06 [Parachain] ✨ Imported #20 (0x0fe9…fe5e)    
    2023-08-15 17:07:06 [Parachain] PoV size { header: 0.2568359375kb, extrinsics: 3.16796875kb, storage_proof: 9.3154296875kb }
    2023-08-15 17:07:06 [Parachain] Compressed PoV size: 8.869140625kb
    2023-08-15 17:07:06 [Parachain] Produced proof-of-validity candidate. block_hash=0x0fe9ae36a7f8ccd29b397782dfe3fe6e31cbd06f6b6bf8db5e95af8caf86fe5e
    2023-08-15 17:07:10 [Parachain] 💤 Idle (2 peers), best: #19 (0x692e…ad69), finalized #18 (0x9f3f…c19f), ⬇ 0.2kiB/s ⬆ 1.8kiB/s    
    2023-08-15 17:07:10 [Relaychain] 💤 Idle (4 peers), best: #1059 (0xc159…a01e), finalized #1057 (0xff17…58dc), ⬇ 2.6kiB/s ⬆ 3.8kiB/s    
    2023-08-15 17:07:12 [Relaychain] ✨ Imported #1060 (0x63ad…f3f8)    
    2023-08-15 17:07:15 [Parachain] 💤 Idle (2 peers), best: #19 (0x692e…ad69), finalized #18 (0x9f3f…c19f), ⬇ 0.6kiB/s ⬆ 0.3kiB/s    
    2023-08-15 17:07:15 [Relaychain] 💤 Idle (4 peers), best: #1060 (0x63ad…f3f8), finalized #1058 (0x3da3…4eeb), ⬇ 1.8kiB/s ⬆ 1.4kiB/s    
    2023-08-15 17:07:18 [Relaychain] 👶 New epoch 106 launching at block 0xa2c8…630e (block slot 282015073 >= start slot 282015073).    
    2023-08-15 17:07:18 [Relaychain] 👶 Next epoch starts at slot 282015083    
    2023-08-15 17:07:18 [Relaychain] ✨ Imported #1061 (0xa2c8…630e)    
    2023-08-15 17:07:18 [Parachain] Starting collation. relay_parent=0xa2c8678b48702db4ba7d2e686f5b31aaffc12c7ad69f973fb1258f41ae7b630e at=0x0fe9ae36a7f8ccd29b397782dfe3fe6e31cbd06f6b6bf8db5e95af8caf86fe5e
    2023-08-15 17:07:18 [Parachain] ✨ Imported #21 (0x8cf3…7acb)    
    2023-08-15 17:07:18 [Relaychain] Trying to remove unknown reserved node: 12D3KooWPs5ALUGa9jmVnWkfmYKL86F7MeXtby7xXYWN7Faoon8f.    
    2023-08-15 17:07:20 [Parachain] 💤 Idle (2 peers), best: #20 (0x0fe9…fe5e), finalized #18 (0x9f3f…c19f), ⬇ 1.2kiB/s ⬆ 0.3kiB/s    
    2023-08-15 17:07:20 [Relaychain] 💤 Idle (4 peers), best: #1061 (0xa2c8…630e), finalized #1058 (0x3da3…4eeb), ⬇ 2.4kiB/s ⬆ 1.9kiB/s    
    2023-08-15 17:07:24 [Relaychain] ✨ Imported #1062 (0x3de4…4529)    
    2023-08-15 17:07:25 [Parachain] 💤 Idle (2 peers), best: #20 (0x0fe9…fe5e), finalized #19 (0x692e…ad69), ⬇ 0.1kiB/s ⬆ 0.1kiB/s    
    2023-08-15 17:07:25 [Relaychain] 💤 Idle (4 peers), best: #1062 (0x3de4…4529), finalized #1059 (0xc159…a01e), ⬇ 1.6kiB/s ⬆ 0.9kiB/s    
    2023-08-15 17:07:30 [Relaychain] ✨ Imported #1063 (0xd57c…50ce)    
    2023-08-15 17:07:30 [Parachain] Starting collation. relay_parent=0xd57cbb8a510ef0a32b5028920f380342a259026ae2d0b922e5bd24cd4c4850ce at=0x8cf373c6450049ccf62b20f45f5e99e9d0f3af38ab64b87cb7c4273a4b677acb
    2023-08-15 17:07:30 [Parachain] ✨ Imported #22 (0x3150…bea7)    
    2023-08-15 17:07:30 [Parachain] 💤 Idle (2 peers), best: #21 (0x8cf3…7acb), finalized #19 (0x692e…ad69), ⬇ 1.1kiB/s ⬆ 0.1kiB/s    
    2023-08-15 17:07:30 [Relaychain] 💤 Idle (4 peers), best: #1063 (0xd57c…50ce), finalized #1060 (0x63ad…f3f8), ⬇ 2.4kiB/s ⬆ 1.8kiB/s    
    2023-08-15 17:07:34 [Relaychain] 👴 Applying authority set change scheduled at block #1061    
    2023-08-15 17:07:34 [Relaychain] 👴 Applying GRANDPA set change to new set [(Public(88dc3417d5058ec4b4503e0c12ea1a0a89be200fe98922423d4334014fa6b0ee (5FA9nQDV...)), 1), (Public(d17c2d7823ebf260fd138f2d7e27d114c0145d968b5ff5006125f2414fadae69 (5GoNkf6W...)), 1)]
    ```
    
    When you see the message "Starting collation," it means that your collator has begun producing parachain blocks. This indicates that the parachain has been successfully registered in the relay chain.