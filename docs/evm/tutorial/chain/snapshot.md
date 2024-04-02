# Chain Database Snapshot

Darwinia provides node database snapshots for node maintainers, facilitating a quick start for a node without syncing from the genesis block. The archive node snapshot contains the state of the blockchain at a certain block height, allowing the node to start from that point instead of starting from the genesis block. Node maintainers can download the latest archive node snapshot and start a node instantly, significantly reducing the block syncing time from several days to about 30 minutes.

The existing architecture of Polkadot consists of a relay chain node and a parachain node. The parachain node cannot create blocks until both the relay chain node and the parachain node are synchronized with the latest chain status. To reduce the synchronization time for the parachain node, downloading the snapshot is recommended. However, for the relay chain, the use of a relay chain snapshot is not necessary and discouraged since the introduction of warp sync. Instead, warp sync downloads finality proofs and state in priority, allowing the relay node to provide the necessary data to the parachain node in less than 15 minutes.

## Available Snapshots

- Darwinia2 Parachain: [https://snapshots.darwinia.network](https://snapshots.darwinia.network/)
- Crab2 Parachain: [https://snapshots.crab.network](https://snapshots.crab.network/)

## Usage

!!! note
    The tutorial is originally based on the Darwinia chain, but it is also applicable to the Crab chain. To use the tutorial for the Crab chain, you just need to choose the correct snapshot resource.

### Install [zstd](https://github.com/facebook/zstd)

```bash
apt install zstd
```

### Create Data Directory

If you are running the collator according to this [tutorial](https://www.notion.so/Run-Collator-Node-af6bce360d5b49ddacc56e4587510210?pvs=21), the **`base-path`** command parameter is set to `/data/darwinia-collator`. If you have customized the path for the data, please adjust it accordingly. To create a snapshot data location, run the following command:

```bash
mkdir -p /data/darwinia-collator/chains/darwinia2/
```

### Prepare Parachain

Select the archive block height and download the parachain snapshot, then extract the database to the node `base-path` by running the following command:

```bash
wget -c https://snapshots.darwinia.network/darwinia2-1172183.tar.zst
tar xv --zstd -f darwinia2-1172183.tar.zst -C data/chains/darwinia2
```

### Prepare Relaychain

To sync the relay chain in warp mode, just add this at the end of the node command(in the `--` section):

```bash
-- --sync warp
```

!!! Tip
    `WARN main sync: [Relaychain] Can't use warp sync mode with a partially synced database. Reverting to full sync mode.`
    If you encounter this log message in your console output, it indicates that you cannot interrupt the sync process of the relay chain node until it reaches the latest finalized block. If you attempt to do so, you will need to purge the already synced database and start the sync process again.


### Start Node

Once you have placed these extracted database files in the correct locations, then you can start your node either a full node or an archive node, by following the other tutorials.