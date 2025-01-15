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
    
    As of the time of writing this doc (2024-09-27), the latest version of the Darwinia chains is `v6.7.1`. Please ensure that you check for [the latest version](https://github.com/darwinia-network/darwinia/releases) when running your own node.

    !!! warn 
        Please be aware that there are two types of binaries available on the release page. Select the one that starts with `darwinia-tracing-xxx`.
    
    ```bash
    wget https://github.com/darwinia-network/darwinia/releases/download/v6.7.1/darwinia-tracing-x86_64-linux-gnu.tar.zst
    tar -I zstd -xf darwinia-tracing-x86_64-linux-gnu.tar.zst
    ```
    
3. Download the overridden wasms
    
    Once you have downloaded the tracing binary, you will need to download the overridden wasm files before setting up your EVM tracing node. The overridden wasm files can be found in a repository maintained by the Darwinia core team. To do this, please run the following command:
    
    ```bash
    git clone https://github.com/darwinia-network/darwinia-release.git
    cd darwinia-release

    # Check out the corresponding network branch
    git checkout origin/darwinia
    # Copy the wasm runtime files to the temporary workaround override runtime location 
    cp wasm/evm-tracing/* ../overridden-runtimes/
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
        --chain=polkadot \
        --sync=warp
    ```
    
    Please make sure to update the `--chain`, `--base-path`, and `--wasm-runtime-overrides` parameters according to the network you wish to set up.
    
2. Verify your node is up and running successfully by reviewing the output displayed in the terminal. The terminal should display output similar to this:
    
    ```bash
    Loading genesis from `/home/darwinia/darwinia-nodes/darwinia2.json`
    CLI parameter `--execution` has no effect anymore and will be removed in the future!
    2024-09-27 06:52:53 Darwinia
    2024-09-27 06:52:53 ✌️  version 6.7.1-08ec5e77d17
    2024-09-27 06:52:53 ❤️  by Darwinia Network <hello@darwinia.network>, 2018-2024
    2024-09-27 06:52:53 📋 Chain specification: Darwinia2
    2024-09-27 06:52:53 🏷  Node name: cooing-drug-7964
    2024-09-27 06:52:53 👤 Role: FULL
    2024-09-27 06:52:53 💾 Database: RocksDb at /data/darwinia2/data/chains/darwinia2/db/full
    2024-09-27 06:52:53 Parachain id: Id(2046)
    2024-09-27 06:52:53 Parachain Account: 2qiDxtPxw1BsbLwujRn5Q2352CaDPY8UMZi4iHBfPXo6FgHd
    2024-09-27 06:52:53 Is collating: no
    2024-09-27 06:53:13 [Parachain] Found wasm override. version=Darwinia2-6640 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.6.4-evm-tracing.compact.compressed.wasm
    2024-09-27 06:53:22 [Parachain] Found wasm override. version=Darwinia2-6404 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.4.0-4-evm-tracing.compact.compressed.wasm
    2024-09-27 06:53:31 [Parachain] Found wasm override. version=Darwinia2-6400 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.4.0-evm-tracing.compact.compressed.wasm
    2024-09-27 06:53:40 [Parachain] Found wasm override. version=Darwinia2-6501 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.5.0-1-evm-tracing.compact.compressed.wasm
    2024-09-27 06:53:50 [Parachain] Found wasm override. version=Darwinia2-6600 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.6.0-evm-tracing.compact.compressed.wasm
    2024-09-27 06:53:59 [Parachain] Found wasm override. version=Darwinia2-6650 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.6.5-evm-tracing.compact.compressed.wasm
    2024-09-27 06:54:08 [Parachain] Found wasm override. version=Darwinia2-6620 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.6.2-evm-tracing.compact.compressed.wasm
    2024-09-27 06:54:17 [Parachain] Found wasm override. version=Darwinia2-6510 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.5.1-evm-tracing.compact.compressed.wasm
    2024-09-27 06:54:25 [Parachain] Found wasm override. version=Darwinia2-6340 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.3.4-evm-tracing.compact.compressed.wasm
    2024-09-27 06:54:34 [Parachain] Found wasm override. version=Darwinia2-6500 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.5.0-evm-tracing.compact.compressed.wasm
    2024-09-27 06:54:43 [Parachain] Found wasm override. version=Darwinia2-6670 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.7.0-evm-tracing.compact.compressed.wasm
    2024-09-27 06:54:52 [Parachain] Found wasm override. version=Darwinia2-6401 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.4.0-1-evm-tracing.compact.compressed.wasm
    2024-09-27 06:55:00 [Parachain] Found wasm override. version=Darwinia2-6403 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.4.0-3-evm-tracing.compact.compressed.wasm
    2024-09-27 06:55:09 [Parachain] Found wasm override. version=Darwinia2-6610 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.6.1-evm-tracing.compact.compressed.wasm
    2024-09-27 06:55:17 [Parachain] Found wasm override. version=Darwinia2-6300 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.3.0-evm-tracing.compact.compressed.wasm
    2024-09-27 06:55:26 [Parachain] Found wasm override. version=Darwinia2-6630 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.6.3-evm-tracing.compact.compressed.wasm
    2024-09-27 06:55:34 [Parachain] Found wasm override. version=Darwinia2-6402 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.4.0-2-evm-tracing.compact.compressed.wasm
    2024-09-27 06:55:44 [Parachain] Found wasm override. version=Darwinia2-6511 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.5.1-1-evm-tracing.compact.compressed.wasm
    2024-09-27 06:55:54 [Parachain] Found wasm override. version=Darwinia2-6710 (DarwiniaOfficialRust-0.tx0.au0) file=overridden-runtimes/darwinia/evm-tracing/darwinia-v6.7.1-evm-tracing.compact.compressed.wasm
    2024-09-27 06:58:28 [Relaychain] 🏷  Local node identity is: 12D3KooWDajBn6V4j8Hq5j2yG2H3q16ztZ7wZ9Qg6NoitGr6XYBz
    2024-09-27 06:58:28 [Relaychain] 💻 Operating system: linux
    2024-09-27 06:58:28 [Relaychain] 💻 CPU architecture: x86_64
    2024-09-27 06:58:28 [Relaychain] 💻 Target environment: gnu
    2024-09-27 06:58:28 [Relaychain] 💻 CPU: AMD EPYC 7282 16-Core Processor
    2024-09-27 06:58:28 [Relaychain] 💻 CPU cores: 8
    2024-09-27 06:58:28 [Relaychain] 💻 Memory: 30090MB
    2024-09-27 06:58:28 [Relaychain] 💻 Kernel: 5.15.0-25-generic
    2024-09-27 06:58:28 [Relaychain] 💻 Linux distribution: Ubuntu 20.04.6 LTS
    2024-09-27 06:58:28 [Relaychain] 💻 Virtual machine: yes
    2024-09-27 06:58:28 [Relaychain] 📦 Highest known block at #22715100
    2024-09-27 06:58:28 [Relaychain] 〽️ Prometheus exporter started at 127.0.0.1:9616
    2024-09-27 06:58:28 [Relaychain] Running JSON-RPC server: addr=127.0.0.1:9945, allowed origins=["http://localhost:*", "http://127.0.0.1:*", "https://localhost:*", "https://127.0.0.1:*", "https://polkadot.js.org"]
    2024-09-27 06:58:28 [Relaychain] 🏁 CPU score: 783.33 MiBs
    2024-09-27 06:58:28 [Relaychain] 🏁 Memory score: 6.67 GiBs
    2024-09-27 06:58:28 [Relaychain] 🏁 Disk score (seq. writes): 917.05 MiBs
    2024-09-27 06:58:28 [Relaychain] 🏁 Disk score (rand. writes): 25.05 MiBs
    2024-09-27 06:58:28 [Parachain] 🏷  Local node identity is: 12D3KooWRyXoStSmNnVZjCoQsitLwruKcc6e7mu5dQAnA4CXVMhk
    2024-09-27 06:58:28 [Parachain] 💻 Operating system: linux
    2024-09-27 06:58:28 [Parachain] 💻 CPU architecture: x86_64
    2024-09-27 06:58:28 [Parachain] 💻 Target environment: gnu
    2024-09-27 06:58:28 [Parachain] 💻 CPU: AMD EPYC 7282 16-Core Processor
    2024-09-27 06:58:28 [Parachain] 💻 CPU cores: 8
    2024-09-27 06:58:28 [Parachain] 💻 Memory: 30090MB
    2024-09-27 06:58:28 [Parachain] 💻 Kernel: 5.15.0-25-generic
    2024-09-27 06:58:28 [Parachain] 💻 Linux distribution: Ubuntu 20.04.6 LTS
    2024-09-27 06:58:28 [Parachain] 💻 Virtual machine: yes
    2024-09-27 06:58:28 [Parachain] 📦 Highest known block at #3908530
    2024-09-27 06:58:28 [Parachain] 〽️ Prometheus exporter started at 127.0.0.1:9615
    2024-09-27 06:58:28 [Parachain] Running JSON-RPC server: addr=0.0.0.0:9944, allowed origins=["*"]
    2024-09-27 06:58:28 [Parachain] 🏁 CPU score: 783.33 MiBs
    2024-09-27 06:58:28 [Parachain] 🏁 Memory score: 6.67 GiBs
    2024-09-27 06:58:28 [Parachain] 🏁 Disk score (seq. writes): 917.05 MiBs
    2024-09-27 06:58:28 [Parachain] 🏁 Disk score (rand. writes): 25.05 MiBs
    2024-09-27 06:58:28 [Parachain] ⚠️  The hardware does not meet the minimal requirements Failed checks: Copy(expected: 11.49 GiBs, found: 6.67 GiBs), Seq Write(expected: 950.00 MiBs, found: 917.05 MiBs), Rnd Write(expected: 420.00 MiBs, found: 25.05 MiBs),  for role 'Authority'.
    2024-09-27 06:58:28 [Parachain] discovered: 12D3KooWDajBn6V4j8Hq5j2yG2H3q16ztZ7wZ9Qg6NoitGr6XYBz /ip4/172.20.0.2/tcp/30334/ws
    2024-09-27 06:58:28 [Relaychain] discovered: 12D3KooWRyXoStSmNnVZjCoQsitLwruKcc6e7mu5dQAnA4CXVMhk /ip4/172.20.0.2/tcp/30333/ws
    2024-09-27 06:58:28 [Relaychain] Sending fatal alert BadCertificate
    ```
