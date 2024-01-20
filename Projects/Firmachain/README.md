<h1 align="center"> 🔥FirmaChain🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Firmachain)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=http://firma.rpc.m.stavr.tech:1037
SEEDS=35b9e0a0818d2c5e9ef187984872c0ad2dbd447c@firma.peer.stavr.tech:1036
cp $HOME/.firmachain/data/priv_validator_state.json $HOME/.firmachain/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.firmachain/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.firmachain/config/config.toml
firmachaind tendermint unsafe-reset-all --home $HOME/.firmachain --keep-addr-book
mv $HOME/.firmachain/priv_validator_state.json.backup $HOME/.firmachain/data/priv_validator_state.json
curl -o - -L http://firma.wasm.stavr.tech:12/wasm-firma.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.firmachain --strip-components 2
sudo systemctl restart firmachaind && journalctl -u firmachaind -f -o cat
```
# SnapShot (~0.9 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop firmachaind
cp $HOME/.firmachain/data/priv_validator_state.json $HOME/.firmachain/priv_validator_state.json.backup
rm -rf $HOME/.firmachain/data
curl -o - -L http://firma.snapshot.stavr.tech:6/firmachain/firmachain-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.firmachain --strip-components 2
curl -o - -L http://firma.wasm.stavr.tech:12/wasm-firma.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.firmachain --strip-components 2
mv $HOME/.firmachain/priv_validator_state.json.backup $HOME/.firmachain/data/priv_validator_state.json
wget -O $HOME/.firmachain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Firmachain/addrbook.json"
sudo systemctl restart firmachaind && journalctl -u firmachaind -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Firmachain-M        `Indexer "ON"` \
🔥API🔥:          https://firma.api.m.stavr.tech \
🔥RPC🔥:          http://firma.rpc.m.stavr.tech:1037              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://firma.grpc.m.stavr.tech:2030 \
🔥peer🔥:         `35b9e0a0818d2c5e9ef187984872c0ad2dbd447c@firma.peer.stavr.tech:1036` \
🔥Addrbook🔥:  `wget -O $HOME/.firmachain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Firmachain/addrbook.json"` \
🔥WASM🔥:  `curl -o - -L http://firma.wasm.stavr.tech:12/wasm-firma.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.firmachain --strip-components 2` \
🔥Auto_install script🔥:`wget -O firmam https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Firmachain/firmam && chmod +x firmam && ./firmam`

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

[raw Mainnet json](https://rpc-check.firmam.stavr.tech/firmam/rpc-firmam-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>13.229.64.47:26657</td><td>colosseum-1</td><td>seed2 🟢</td><td>10698207</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T16:08:30.749713926UTC</td></tr><tr><td>13.214.198.112:26657</td><td>colosseum-1</td><td>seed3 🟢</td><td>10698209</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T16:08:38.387693326UTC</td></tr><tr><td>15.164.176.96:26657</td><td>colosseum-1</td><td>node 🟢</td><td>10698212</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T16:08:58.848550189UTC</td></tr><tr><td>54.255.246.117:26657</td><td>colosseum-1</td><td>seed1 🟢</td><td>10698213</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T16:09:00.190213786UTC</td></tr><tr><td>142.132.202.86:57657</td><td>colosseum-1</td><td>ramuchi.tech 🟢</td><td>10698207</td><td>6308001</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T16:08:30.983069374UTC</td></tr><tr><td>95.168.173.33:15657</td><td>colosseum-1</td><td>FirmaChain-mainnet-prod 🔴</td><td>10698210</td><td>6776707</td><td>False</td><td>on</td><td>101862</td><td>2024-01-20T16:08:44.870450872UTC</td></tr><tr><td>195.201.110.169:26657</td><td>colosseum-1</td><td>SRG0Z10-RPC 🟢</td><td>10698212</td><td>9585707</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T16:08:55.380075017UTC</td></tr><tr><td>66.45.246.166:1037</td><td>colosseum-1</td><td>STAVR-Service 🟢</td><td>10698204</td><td>10695501</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T16:08:21.227459439UTC</td></tr></table>