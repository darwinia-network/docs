# Run Archive Node

Owner: bear.wang@itering.io

<aside>
👉🏻 Familiarity with Linux/Mac command line is essential.

</aside>

# **Overview**

A blockchain's growth comes from a *genesis block*, *extrinsics*, and *events*.

An **archive node** keeps all the past blocks and their states. An archive node makes it convenient to query the past state of the chain at any point in time. Finding out what an account's balance at a particular block was or which extrinsics resulted in a specific state change are fast operations when using an archive node. 

## Run Archive Node

When running as a simple sync node (above), only the state of the past 256 blocks will be kept. To keep the full state, use the `--state-pruning` and `--blocks-pruning` flag.

### **Recommended Hardware**

- **RAM:** 8 GB:
- **Storage(SSD)**: 800 GB

### Download Snapshot

It's important to note that there is a faster method to expedite the syncing process**.** You can achieve this by downloading the snapshot blockchain data and moving it to the current node database location and greatly speeding up the node sync process. Click [here](https://www.notion.so/Chain-Database-Snapshot-f0f695e8d4444cf69e1c8dac51d49558?pvs=21) for more detailed instructions.

### Prepare The Binary

As of the time of writing this doc(2023-09-04), the latest version of the Darwinia node is `v6.4.0`. Please ensure that you check for [the latest version](https://github.com/darwinia-network/darwinia/releases) when running your own node.

```bash
wget https://github.com/darwinia-network/darwinia/releases/download/v6.4.0/darwinia-x86_64-linux-gnu.tar.bz2
tar xvf darwinia-x86_64-linux-gnu.tar.bz2
```

### Run An Archive Node

<aside>
💡 Note: Most of the arguments are the same between different networks. However, please note that the `-chain`, `-base-path` and `-chain` after `--` refer to the relay chain in the last line.

</aside>

- For Darwinia Chain
    
    ```bash
    ./darwinia \
        --chain=darwinia \
        --base-path=/data/darwinia-archive-node \
        --state-pruning=archive \
        --blocks-pruning=archive \
        --frontier-backend-type=sql \
        --rpc-external \
        --rpc-cors=all \
        --rpc-max-connections=1000 \
        -- \
        --chain=polkadot
    ```
    
- For Crab Chain
    
    ```bash
    ./darwinia \
        --chain=crab \
        --base-path=/data/crab-archive-node \
        --state-pruning=archive \
        --blocks-pruning=archive \
        --frontier-backend-type=sql \
        --rpc-external \
        --rpc-cors=all \
        --rpc-max-connections=1000 \
        -- \
        --chain=kusama
    ```