<h1 align="center"> 🔥BITCANNA MAINNET🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Bitcanna)
=

# StateSync
```python
RPC="http://bitcanna.rpc.m.stavr.tech:21327"
peers="644ac886e7f2fe082b3556dc694076e71a4e959a@bitcanna.peers.stavr.tech:21326"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.bcna/config/config.toml
LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.bcna/config/config.toml
sudo systemctl stop bcnad && bcnad tendermint unsafe-reset-all --keep-addr-book
sudo systemctl restart bcnad && sudo journalctl -u bcnad -f -o cat
```
# SnapShot (~0.3 GB) updated every 5 hours
```python
cd $HOME
snap install lz4
sudo systemctl stop bcnad
cp $HOME/.bcna/data/priv_validator_state.json $HOME/.bcna/priv_validator_state.json.backup
rm -rf $HOME/.bcna/data
curl -o - -L http://bitcanna.snapshot.stavr.tech:1004/bca/bca-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.bcna --strip-components 2
mv $HOME/.bcna/priv_validator_state.json.backup $HOME/.bcna/data/priv_validator_state.json
wget -O $HOME/.bcna/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/addrbook.json"
sudo systemctl restart bcnad && journalctl -u bcnad -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:    https://explorer.stavr.tech/Bitcanna/staking          `Indexer "ON"` \
🔥EXPLORER Devnet🔥:     https://explorer.stavr.tech/Bitcanna-DEV/staking     `Indexer "ON"` \
🔥API Mainnet🔥:         https://bitcanna.api.m.stavr.tech \
🔥API Devnet🔥:          https://bitcanna.api.dev.stavr.tech \
🔥RPC Mainnet🔥:         http://bitcanna.rpc.m.stavr.tech:21327         `Snapshot-interval = 300` \
🔥gRPC Mainnet🔥:        http://bitcanna.grpc.m.stavr.tech:9081 \
🔥gRPC Devnet🔥:         http://bitcanna.grpc.dev.stavr.tech:2901 \
🔥peer Mainnet🔥:        `644ac886e7f2fe082b3556dc694076e71a4e959a@bitcanna.peers.stavr.tech:21326` \
🔥peer Devnet🔥:         `b0c7e5c69aaf00626baaf7c59370029b587a91a4@bitcannadev.peers.stavr.tech:30006` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.bcna/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/addrbook.json"``` \
🔥Addrbook Devnet🔥:    ```wget -O $HOME/.bcna/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/Bitcanna_DEV/addrbook.json"``` \
🔥Auto_install script Mainnet🔥:```wget -O bitcanna https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/bitcanna && chmod +x bitcanna && ./bitcanna``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Bitcanna/Decentralization)🔥


<details>
<summary>RPC Scanning</summary>

<h2 align="center"> We scan nodes in real time every 4 hours. And we provide the final result of RPC endpoints.
We cannot influence the operation of these nodes in any way. </h2>


```python
If Voting Power is higher than 0 --> then the Node is a validator of the network and may be subject to attack and be a potential threat to the chain.
```
```python
We marked such validators with a red symbol
```

</details>

[raw Mainnet json](https://rpc-check.bcam.stavr.tech/bcam/rpc-bcam-result.json) \
[raw Testnet json](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Bitcanna/Rpc-Check-Testnet)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>95.216.242.82:36657</td><td>bitcanna-1</td><td>Moniker 🟢</td><td>11960633</td><td>5776907</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T06:53:31.449416197UTC</td></tr><tr><td>65.108.142.81:26683</td><td>bitcanna-1</td><td>Stakely.io 🟢</td><td>11960636</td><td>6152001</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T06:53:48.858734683UTC</td></tr><tr><td>93.115.25.15:26657</td><td>bitcanna-1</td><td>Stakely.io 🟢</td><td>11960635</td><td>6520001</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T06:53:42.314398615UTC</td></tr><tr><td>144.76.97.251:27657</td><td>bitcanna-1</td><td>AlxVoy 🟢</td><td>11960640</td><td>8805201</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T06:54:09.643535481UTC</td></tr><tr><td>65.109.155.238:33657</td><td>bitcanna-1</td><td>MultVR 🔴</td><td>11960637</td><td>9933415</td><td>False</td><td>on</td><td>350755</td><td>2024-01-03T06:53:53.719913190UTC</td></tr><tr><td>65.108.76.33:26777</td><td>bitcanna-1</td><td>StakePool-bitcanna 🟢</td><td>11960633</td><td>10823915</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T06:53:31.105640986UTC</td></tr><tr><td>65.109.93.152:26357</td><td>bitcanna-1</td><td>AlxVoy 🔴</td><td>11960641</td><td>10824001</td><td>False</td><td>on</td><td>1391603</td><td>2024-01-03T06:54:18.437801299UTC</td></tr><tr><td>161.97.150.65:26657</td><td>bitcanna-1</td><td>New_peer 🟢</td><td>11960636</td><td>11334001</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T06:53:49.183074114UTC</td></tr><tr><td>185.144.99.40:46657</td><td>bitcanna-1</td><td>cryptech 🟢</td><td>11960633</td><td>11528001</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T06:53:28.754308781UTC</td></tr><tr><td>193.34.144.156:26657</td><td>bitcanna-1</td><td>Paranorm 🟢</td><td>11960638</td><td>11645501</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T06:53:58.395555927UTC</td></tr><tr><td>65.108.131.190:21957</td><td>bitcanna-1</td><td>bitcanna 🔴</td><td>11960638</td><td>11860638</td><td>False</td><td>on</td><td>408777</td><td>2024-01-03T06:53:58.139456491UTC</td></tr><tr><td>144.91.65.13:26667</td><td>bitcanna-1</td><td>AviaDoc_by_AviaOne 🟢</td><td>11960639</td><td>11955501</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T06:54:04.937006060UTC</td></tr><tr><td>135.181.210.171:21327</td><td>bitcanna-1</td><td>STAVR-Service 🟢</td><td>11960640</td><td>11959001</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T06:54:09.388794222UTC</td></tr></table>
