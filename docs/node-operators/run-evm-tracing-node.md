# Run Evm Trace Node

As you may be aware, Darwinia chains are EVM compatible, which means that the RPC behavior should be consistent with an Ethereum node. The majority of RPC usage aligns with the official Ethereum RPC, with the exception of the EVM tracing APIs. The key distinction is that the EVM tracing functionality is offered by a dedicated node. This tutorial will demonstrate how to run a dedicated node to enable EVM tracing functionality.

## Run Evm Trace Node

### Recommended Hardware

- **RAM:** 8 GB:
- **Storage(SSD)**: 800 GB

### Prepare Tracing Binary And Overridden Wasms

1. Create a work dirctory
    
    Let's create a directory called `run-evm-tracing-node` to store everything needed for setting up an EVM tracing node, including the downloaded evm tracing binary and the chain database. Additionally, we'll create a subdirectory called `overridden-runtimes` under `run-evm-tracing-node` to store all the overridden runtime files. To accomplish this, please execute the following command:
    
    ```bash
    mkdir run-evm-tracing-node && cd run-evm-tracing-node
    mkdir overridden-runtimes
    ```
    
2. Download the precompiled tracing binary
    
    As of the time of writing this doc (2023-10-16), the latest version of the Pangolin Chain is `v6.4.0`. Please ensure that you check for [the latest version](https://github.com/darwinia-network/darwinia/releases) when running your own node.
    
    ***Please be aware that there are two types of binaries available on the release page. Select the one that starts with `darwinia-tracing-xxx`.***
    
    ```bash
    wget https://github.com/darwinia-network/darwinia/releases/download/pango-6405/darwinia-tracing-x86_64-linux-gnu.tar.zst
    tar xvf darwinia-tracing-x86_64-linux-gnu.tar.zst
    ```
    
3. Download the overridden wasms
    
    Once you have downloaded the tracing binary, you will need to download the overridden wasms before setting up your EVM tracing node. The overridden wasm files can be found in a repository maintained by the Darwinia core team. To do this, please run the following command:
    
    ```bash
    git clone https://github.com/darwinia-network/wasm-runtime-overrides.git
    cd wasm-runtime-overrides/
    git checkout origin/pangolin
    cp -r pangolin/ ../run-evm-tracing-node/overridden-runtimes/
    ```
    
    The `wasm-runtime-overrides` repository has four branches, each corresponding to one of the four Darwinia chains. You will need to switch to the branch that corresponds to your desired network and copy the `wasm` directory to your temporary workaround location. In this tutorial, we will use the `pangolin` branch.
    

### Start The EVM Tracing Node

1. Start the node by running the following command:
    
    ```bash
    ./darwinia \
        --chain=pangolin \
        --base-path=/data/pangolin-trace-node\
        --state-pruning=archive \
        --blocks-pruning=archive \
        --execution=wasm \
        --rpc-external \
        --rpc-cors=all \
        --tracing-api=debug,trace \
        --runtime-cache-size=64 \
        --frontier-backend-type=sql \
        --wasm-runtime-overrides=overridden-runtimes/pangolin/wasms
        -- \
        --chain=rococo \
        --sync=warp
    ```
    
    Please make sure to update the `--chain`, `--base-path`, and `--wasm-runtime-overrides` parameters according to the network you wish to set up. Additionally, ensure that the `--execution=wasm` flag is enabled.
    
2. Verify your node is up and running successfully by reviewing the output displayed in the terminal. The terminal should display output similar to this:
    
    ```bash
    Loading genesis from `/home/bear/coding/rust-space/test-docs/run-evm-tracing-node/pangolin2.json`
    2023-10-16 16:37:41 Darwinia    
    2023-10-16 16:37:41 ✌️  version 6.4.0-7e4d35a1c28    
    2023-10-16 16:37:41 ❤️  by Darwinia Network <hello@darwinia.network>, 2018-2023    
    2023-10-16 16:37:41 📋 Chain specification: Pangolin2    
    2023-10-16 16:37:41 🏷  Node name: profuse-honey-5725    
    2023-10-16 16:37:41 👤 Role: FULL    
    2023-10-16 16:37:41 💾 Database: RocksDb at /data/pangolin-trace-node/chains/pangolin2/db/full    
    2023-10-16 16:37:41 ⛓  Native runtime: Pangolin2-6405 (DarwiniaOfficialRust-0.tx0.au0)    
    2023-10-16 16:37:42 Parachain id: Id(2105)    
    2023-10-16 16:37:42 Parachain Account: 5Ec4AhNxga1JYLioRBNxfRnovheDELVbZTRSnKMgvSVPvNcN    
    2023-10-16 16:37:42 Parachain genesis state: 0x000000000000000000000000000000000000000000000000000000000000000000d353645e3503ca0ebe7319eee9bd70821acfa54d4161386990329b4a4f9813be03170a2e7597b7b7e3d84c05391d139a62b157e78786d8c082f29dcf4c11131400    
    2023-10-16 16:37:42 Is collating: no    
    2023-10-16 16:37:43 [Parachain] Found wasm override. version=Pangolin2-6320 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/pangolin/wasms/pangolin-pango-6320-tracing-runtime.compact.compressed.wasm
    2023-10-16 16:37:44 [Parachain] Found wasm override. version=Pangolin2-6401 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/pangolin/wasms/pangolin-pango-6401-tracing-runtime.compact.compressed.wasm
    2023-10-16 16:37:45 [Parachain] Found wasm override. version=Pangolin2-6300 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/pangolin/wasms/pangolin-pango-6300-tracing-runtime.compact.compressed.wasm
    2023-10-16 16:37:46 [Parachain] Found wasm override. version=Pangolin2-6402 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/pangolin/wasms/pangolin-pango-6402-tracing-runtime.compact.compressed.wasm
    2023-10-16 16:37:46 [Parachain] Found wasm override. version=Pangolin2-6403 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/pangolin/wasms/pangolin-pango-6403-tracing-runtime.compact.compressed.wasm
    2023-10-16 16:37:47 [Parachain] Found wasm override. version=Pangolin2-6405 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/pangolin/wasms/pangolin-pango-6405-tracing-runtime.compact.compressed.wasm
    2023-10-16 16:37:48 [Parachain] Found wasm override. version=Pangolin2-6340 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/pangolin/wasms/pangolin-pango-6340-tracing-runtime.compact.compressed.wasm
    2023-10-16 16:37:49 [Parachain] Found wasm override. version=Pangolin2-6400 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/pangolin/wasms/pangolin-pango-6400-tracing-runtime.compact.compressed.wasm
    2023-10-16 16:37:49 [Parachain] Found wasm override. version=Pangolin2-6310 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/pangolin/wasms/pangolin-pango-6310-tracing-runtime.compact.compressed.wasm
    2023-10-16 16:37:50 [Parachain] Found wasm override. version=Pangolin2-6404 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/pangolin/wasms/pangolin-pango-6404-tracing-runtime.compact.compressed.wasm
    2023-10-16 16:37:51 [Parachain] 🔨 Initializing Genesis block/state (state: 0xd353…13be, header-hash: 0xb067…6b70)    
    2023-10-16 16:37:52 [Parachain] 📑 Connection configuration: SqliteBackendConfig { path: "/data/pangolin-trace-node/chains/pangolin2/sql/frontier.db3", create_if_missing: true, thread_count: 4, cache_size: 209715200 }    
    2023-10-16 16:37:52 [Relaychain] 🔨 Initializing Genesis block/state (state: 0x8ad9…f0da, header-hash: 0x6408…063e)    
    2023-10-16 16:37:52 [Relaychain] 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.    
    2023-10-16 16:37:53 [Relaychain] 👶 Creating empty BABE epoch changes on what appears to be first startup.    
    2023-10-16 16:37:53 [Relaychain] 🏷  Local node identity is: 12D3KooWKD6yACpTYygZGgmaBgLgbfWLL7GEfGXqBbdjgxDyd2PM    
    2023-10-16 16:37:53 [Relaychain] 💻 Operating system: linux    
    2023-10-16 16:37:53 [Relaychain] 💻 CPU architecture: x86_64    
    2023-10-16 16:37:53 [Relaychain] 💻 Target environment: gnu    
    2023-10-16 16:37:53 [Relaychain] 💻 CPU: AMD Ryzen 7 5700G with Radeon Graphics    
    2023-10-16 16:37:53 [Relaychain] 💻 CPU cores: 8    
    2023-10-16 16:37:53 [Relaychain] 💻 Memory: 63578MB    
    2023-10-16 16:37:53 [Relaychain] 💻 Kernel: 6.2.0-33-generic    
    2023-10-16 16:37:53 [Relaychain] 💻 Linux distribution: Ubuntu 22.04.3 LTS    
    2023-10-16 16:37:53 [Relaychain] 💻 Virtual machine: no    
    2023-10-16 16:37:53 [Relaychain] 📦 Highest known block at #0    
    2023-10-16 16:37:53 [Relaychain] Running JSON-RPC server: addr=127.0.0.1:9945, allowed origins=["http://localhost:*", "http://127.0.0.1:*", "https://localhost:*", "https://127.0.0.1:*", "https://polkadot.js.org"]    
    2023-10-16 16:37:53 [Relaychain] 〽️ Prometheus exporter started at 127.0.0.1:9616    
    2023-10-16 16:37:53 [Relaychain] 🏁 CPU score: 1.34 GiBs    
    2023-10-16 16:37:53 [Relaychain] 🏁 Memory score: 15.73 GiBs    
    2023-10-16 16:37:53 [Relaychain] 🏁 Disk score (seq. writes): 1.61 GiBs    
    2023-10-16 16:37:53 [Relaychain] 🏁 Disk score (rand. writes): 742.59 MiBs    
    2023-10-16 16:37:53 [Relaychain] Starting with an empty approval vote DB.
    2023-10-16 16:37:53 [Parachain] 🏷  Local node identity is: 12D3KooWMmLGUqtaHW174JrE7UjeVagpKsCsBXDZfCyoQcvvHLjH    
    2023-10-16 16:37:53 Import genesis    
    2023-10-16 16:37:53 [Parachain] 💻 Operating system: linux    
    2023-10-16 16:37:53 [Parachain] 💻 CPU architecture: x86_64    
    2023-10-16 16:37:53 [Parachain] 💻 Target environment: gnu    
    2023-10-16 16:37:53 [Parachain] 💻 CPU: AMD Ryzen 7 5700G with Radeon Graphics    
    2023-10-16 16:37:53 [Parachain] 💻 CPU cores: 8    
    2023-10-16 16:37:53 [Parachain] 💻 Memory: 63578MB    
    2023-10-16 16:37:53 [Parachain] 💻 Kernel: 6.2.0-33-generic    
    2023-10-16 16:37:53 [Parachain] 💻 Linux distribution: Ubuntu 22.04.3 LTS    
    2023-10-16 16:37:53 [Parachain] 💻 Virtual machine: no    
    2023-10-16 16:37:53 [Parachain] 📦 Highest known block at #0    
    2023-10-16 16:37:53 [Parachain] 〽️ Prometheus exporter started at 127.0.0.1:9615    
    2023-10-16 16:37:53 [Parachain] Running JSON-RPC server: addr=0.0.0.0:9944, allowed origins=["*"]    
    2023-10-16 16:37:53 [Parachain] 🏁 CPU score: 1.34 GiBs    
    2023-10-16 16:37:53 [Parachain] 🏁 Memory score: 15.73 GiBs    
    2023-10-16 16:37:53 [Parachain] 🏁 Disk score (seq. writes): 1.61 GiBs    
    2023-10-16 16:37:53 [Parachain] 🏁 Disk score (rand. writes): 742.59 MiBs    
    2023-10-16 16:37:54 [Parachain] 🔍 Discovered new external address for our node: /ip4/60.176.103.239/tcp/30333/ws/p2p/12D3KooWMmLGUqtaHW174JrE7UjeVagpKsCsBXDZfCyoQcvvHLjH    
    2023-10-16 16:37:54 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.    
    2023-10-16 16:37:54 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.    
    2023-10-16 16:37:54 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.    
    2023-10-16 16:37:54 [Parachain] [pallet::message-gadget] invalid raw message root: [], return.
    ```