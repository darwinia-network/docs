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
    
    As of the time of writing this doc (2024-06-13), the latest version of the Koi Chain is `v6.6.3`. Please ensure that you check for [the latest version](https://github.com/darwinia-network/darwinia/releases) when running your own node.

    !!! warn 
        Please be aware that there are two types of binaries available on the release page. Select the one that starts with `darwinia-tracing-xxx`.
    
    ```bash
    wget https://github.com/darwinia-network/darwinia/releases/download/v6.6.3/darwinia-tracing-x86_64-linux-gnu.tar.zst
    tar xvf darwinia-tracing-x86_64-linux-gnu.tar.zst
    ```
    
3. Download the overridden wasms
    
    Once you have downloaded the tracing binary, you will need to download the overridden wasm files before setting up your EVM tracing node. The overridden wasm files can be found in a repository maintained by the Darwinia core team. To do this, please run the following command:
    
    ```bash
    git clone https://github.com/darwinia-network/darwinia-release.git
    cd darwinia-release

    # Check out the corresponding network branch
    git checkout origin/darwinia
    # Copy the wasm runtime files to the temporary workaround override runtime location 
    cp wasm/evm-tracing/* ../run-evm-tracing-node/overridden-runtimes/
    ```
    
    The `wasm-runtime-overrides` repository has five branches, each corresponding to one of the four Darwinia chains. You will need to switch to the branch that corresponds to your desired network and copy the `wasm` directory to your temporary workaround location. In this tutorial, we will use the `darwinia` branch.
    

### Start The EVM Tracing Node

1. Start the node by running the following command:
    
    ```bash
    ./darwinia \
        --chain=darwinia \
        --base-path=/data/darwinia-trace-node\
        --state-pruning=archive \
        --blocks-pruning=archive \
        --rpc-external \
        --rpc-cors=all \
        --tracing-api=debug,trace \
        --runtime-cache-size=64 \
        --frontier-backend-type=sql \
        --wasm-runtime-overrides=overridden-runtimes \
        -- \
        --chain polkadot \
        --sync=warp
    ```
    
    Please make sure to update the `--chain`, `--base-path`, and `--wasm-runtime-overrides` parameters according to the network you wish to set up.
    
2. Verify your node is up and running successfully by reviewing the output displayed in the terminal. The terminal should display output similar to this:
    
    ```bash
    2024-06-13 14:22:45 Darwinia    
    2024-06-13 14:22:45 ✌️  version 6.6.3-1eb277e94b0    
    2024-06-13 14:22:45 ❤️  by Darwinia Network <hello@darwinia.network>, 2018-2024    
    2024-06-13 14:22:45 📋 Chain specification: Darwinia2    
    2024-06-13 14:22:45 🏷  Node name: grumpy-kittens-1092    
    2024-06-13 14:22:45 👤 Role: FULL    
    2024-06-13 14:22:45 💾 Database: RocksDb at /data/darwinia-trace-node/chains/darwinia2/db/full    
    2024-06-13 14:22:47 Parachain id: Id(2046)    
    2024-06-13 14:22:47 Parachain Account: 2qiDxtPxw1BsbLwujRn5Q2352CaDPY8UMZi4iHBfPXo6FgHd    
    2024-06-13 14:22:47 Is collating: no    
    2024-06-13 14:22:48 [Parachain] Found wasm override. version=Darwinia2-6610 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.6.1-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:49 [Parachain] Found wasm override. version=Darwinia2-6400 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.4.0-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:49 [Parachain] Found wasm override. version=Darwinia2-6511 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.5.1-1-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:50 [Parachain] Found wasm override. version=Darwinia2-6401 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.4.0-1-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:51 [Parachain] Found wasm override. version=Darwinia2-6402 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.4.0-2-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:52 [Parachain] Found wasm override. version=Darwinia2-6403 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.4.0-3-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:53 [Parachain] Found wasm override. version=Darwinia2-6300 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.3.0-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:54 [Parachain] Found wasm override. version=Darwinia2-6620 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.6.2-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:55 [Parachain] Found wasm override. version=Darwinia2-6501 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.5.0-1-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:55 [Parachain] Found wasm override. version=Darwinia2-6404 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.4.0-4-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:56 [Parachain] Found wasm override. version=Darwinia2-6600 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.6.0-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:57 [Parachain] Found wasm override. version=Darwinia2-6500 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.5.0-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:58 [Parachain] Found wasm override. version=Darwinia2-6510 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.5.1-evm-tracing.compact.compressed.wasm
    2024-06-13 14:22:59 [Parachain] Found wasm override. version=Darwinia2-6340 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.3.4-evm-tracing.compact.compressed.wasm
    2024-06-13 14:23:00 [Parachain] Found wasm override. version=Darwinia2-6630 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia-v6.6.3-evm-tracing.compact.compressed.wasm
    2024-06-13 14:23:01 [Parachain] 🔨 Initializing Genesis block/state (state: 0xde42…7b71, header-hash: 0xf0b8…570e)    
    2024-06-13 14:23:02 [Parachain] 📑 Connection configuration: SqliteBackendConfig { path: "/data/darwinia-trace-node/chains/darwinia2/sql/frontier.db3", create_if_missing: true, thread_count: 4, cache_size: 209715200 }    
    2024-06-13 14:23:02 [Relaychain] 🔨 Initializing Genesis block/state (state: 0x29d0…4e17, header-hash: 0x91b1…90c3)    
    2024-06-13 14:23:02 [Relaychain] 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.    
    2024-06-13 14:23:02 [Relaychain] 👶 Creating empty BABE epoch changes on what appears to be first startup.    
    2024-06-13 14:23:02 [Relaychain] 🏷  Local node identity is: 12D3KooWA9n7SitbhPdV8qFYrNEApMeBS5mGQhV972krg9vc7G6Y    
    2024-06-13 14:23:03 [Relaychain] 💻 Operating system: linux    
    2024-06-13 14:23:03 [Relaychain] 💻 CPU architecture: x86_64    
    2024-06-13 14:23:03 [Relaychain] 💻 Target environment: gnu    
    2024-06-13 14:23:03 [Relaychain] 💻 CPU: AMD Ryzen 7 5700G with Radeon Graphics    
    2024-06-13 14:23:03 [Relaychain] 💻 CPU cores: 8    
    2024-06-13 14:23:03 [Relaychain] 💻 Memory: 63578MB    
    2024-06-13 14:23:03 [Relaychain] 💻 Kernel: 6.5.0-35-generic    
    2024-06-13 14:23:03 [Relaychain] 💻 Linux distribution: Ubuntu 22.04.4 LTS    
    2024-06-13 14:23:03 [Relaychain] 💻 Virtual machine: no    
    2024-06-13 14:23:03 [Relaychain] 📦 Highest known block at #0    
    2024-06-13 14:23:03 [Relaychain] 〽️ Prometheus exporter started at 127.0.0.1:9616    
    2024-06-13 14:23:03 [Relaychain] Running JSON-RPC server: addr=127.0.0.1:9945, allowed origins=["http://localhost:*", "http://127.0.0.1:*", "https://localhost:*", "https://127.0.0.1:*", "https://polkadot.js.org"]    
    2024-06-13 14:23:03 [Relaychain] 🏁 CPU score: 1.23 GiBs    
    2024-06-13 14:23:03 [Relaychain] 🏁 Memory score: 14.63 GiBs    
    2024-06-13 14:23:03 [Relaychain] 🏁 Disk score (seq. writes): 1.47 GiBs    
    2024-06-13 14:23:03 [Relaychain] 🏁 Disk score (rand. writes): 552.04 MiBs    
    2024-06-13 14:23:03 [Relaychain] Starting with an empty approval vote DB.
    2024-06-13 14:23:03 [Parachain] 🏷  Local node identity is: 12D3KooWA6UpwpZ9YSkR3k9VkqPtvf9z7dERfEooB4P81vDPAvWu    
    2024-06-13 14:23:03 Import genesis    
    2024-06-13 14:23:03 [Parachain] 💻 Operating system: linux    
    2024-06-13 14:23:03 [Parachain] 💻 CPU architecture: x86_64    
    2024-06-13 14:23:03 [Parachain] 💻 Target environment: gnu    
    2024-06-13 14:23:03 [Parachain] 💻 CPU: AMD Ryzen 7 5700G with Radeon Graphics    
    2024-06-13 14:23:03 [Parachain] 💻 CPU cores: 8    
    2024-06-13 14:23:03 [Parachain] 💻 Memory: 63578MB    
    2024-06-13 14:23:03 [Parachain] 💻 Kernel: 6.5.0-35-generic    
    2024-06-13 14:23:03 [Parachain] 💻 Linux distribution: Ubuntu 22.04.4 LTS    
    2024-06-13 14:23:03 [Parachain] 💻 Virtual machine: no    
    2024-06-13 14:23:03 [Parachain] 📦 Highest known block at #0    
    2024-06-13 14:23:03 [Parachain] 〽️ Prometheus exporter started at 127.0.0.1:9615    
    2024-06-13 14:23:03 [Parachain] Running JSON-RPC server: addr=0.0.0.0:9944, allowed origins=["*"]    
    2024-06-13 14:23:03 [Parachain] 🏁 CPU score: 1.23 GiBs    
    2024-06-13 14:23:03 [Parachain] 🏁 Memory score: 14.63 GiBs    
    2024-06-13 14:23:03 [Parachain] 🏁 Disk score (seq. writes): 1.47 GiBs    
    2024-06-13 14:23:03 [Parachain] 🏁 Disk score (rand. writes): 552.04 MiBs    
    2024-06-13 14:23:03 [Relaychain] discovered: 12D3KooWA6UpwpZ9YSkR3k9VkqPtvf9z7dERfEooB4P81vDPAvWu /ip4/192.168.31.52/tcp/30333/ws    
    2024-06-13 14:23:03 [Parachain] discovered: 12D3KooWA9n7SitbhPdV8qFYrNEApMeBS5mGQhV972krg9vc7G6Y /ip4/192.168.31.52/tcp/30334/ws    
    2024-06-13 14:23:03 [Relaychain] discovered: 12D3KooWA6UpwpZ9YSkR3k9VkqPtvf9z7dERfEooB4P81vDPAvWu /ip4/172.18.0.1/tcp/30333/ws    
    2024-06-13 14:23:03 [Parachain] discovered: 12D3KooWA9n7SitbhPdV8qFYrNEApMeBS5mGQhV972krg9vc7G6Y /ip4/172.17.0.1/tcp/30334/ws    
    2024-06-13 14:23:03 [Parachain] discovered: 12D3KooWA9n7SitbhPdV8qFYrNEApMeBS5mGQhV972krg9vc7G6Y /ip4/172.18.0.1/tcp/30334/ws    
    2024-06-13 14:23:03 [Relaychain] discovered: 12D3KooWA6UpwpZ9YSkR3k9VkqPtvf9z7dERfEooB4P81vDPAvWu /ip4/172.17.0.1/tcp/30333/ws    
    2024-06-13 14:23:03 [Relaychain] Sending fatal alert BadCertificate    
    2024-06-13 14:23:04 [Relaychain] 🔍 Discovered new external address for our node: /ip4/183.159.52.240/tcp/30334/ws/p2p/12D3KooWA9n7SitbhPdV8qFYrNEApMeBS5mGQhV972krg9vc7G6Y    
    2024-06-13 14:23:05 [Relaychain] Sending fatal alert BadCertificate    
    2024-06-13 14:23:08 [Relaychain] ⏩ Warping, Waiting for 3 peers to be connected, 0.00 Mib (0 peers), best: #0 (0x91b1…90c3), finalized #0 (0x91b1…90c3), ⬇ 19.9kiB/s ⬆ 12.6kiB/s    
    2024-06-13 14:23:08 [Parachain] 💤 Idle (0 peers), best: #0 (0xf0b8…570e), finalized #0 (0xf0b8…570e), ⬇ 0 ⬆ 0    
    2024-06-13 14:23:08 [Relaychain] Sending fatal alert BadCertificate    
    2024-06-13 14:23:13 [Relaychain] ⏩ Warping, Downloading finality proofs, 0.00 Mib (3 peers), best: #0 (0x91b1…90c3), finalized #0 (0x91b1…90c3), ⬇ 77.7kiB/s ⬆ 37.2kiB/s    
    2024-06-13 14:23:13 encountered unexpected or invalid data: [Metadata] No logs found for hash 0xf0b8924b12e8108550d28870bc03f7b45a947e1b2b9abf81bfb0b89ecb60570e    
    2024-06-13 14:23:13 no rows returned by a query that expected to return at least one row    
    2024-06-13 14:23:13 [Parachain] 💤 Idle (0 peers), best: #0 (0xf0b8…570e), finalized #0 (0xf0b8…570e), ⬇ 0 ⬆ 0    
    2024-06-13 14:23:18 [Relaychain] ⏩ Warping, Downloading finality proofs, 7.98 Mib (4 peers), best: #0 (0x91b1…90c3), finalized #0 (0x91b1…90c3), ⬇ 1.6MiB/s ⬆ 18.2kiB/s    
    2024-06-13 14:23:18 [Parachain] 💤 Idle (0 peers), best: #0 (0xf0b8…570e), finalized #0 (0xf0b8…570e), ⬇ 0 ⬆ 0    
    2024-06-13 14:23:18 [Relaychain] Sending fatal alert BadCertificate    
    ```