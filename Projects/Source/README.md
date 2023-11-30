<h1 align="center"> 🔥Source Mainnet🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Source)
=

# StateSync Mainnet 
```python
SNAP_RPC=https://source.rpc.m.stavr.tech:443
peers="9751bfbbb3303db1898ef5c601d8522938623262@source.peers.stavr.tech:20056"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.source/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.source/config/config.toml
sourced tendermint unsafe-reset-all
sudo systemctl restart sourced && journalctl -u sourced -f -o cat
```

# SnapShot Mainnet (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop sourced
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1false|" ~/.source/config/config.toml
cp $HOME/.source/data/priv_validator_state.json $HOME/.source/priv_validator_state.json.backup
rm -rf $HOME/.source/data
curl -o - -L https://source-m.snapshot.stavr.tech/source/source-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.source --strip-components 2
wget -O $HOME/.source/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Source/addrbook.json"
mv $HOME/.source/priv_validator_state.json.backup $HOME/.source/data/priv_validator_state.json
sudo systemctl restart sourced && journalctl -u sourced -f -o cat
```

<h1 align="center"> 🔥Source Testnet🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Source/Testnet)
=

# SnapShot Testnet (~0.3 GB) updated every 6 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop sourced
cp $HOME/.source/data/priv_validator_state.json $HOME/.source/priv_validator_state.json.backup
rm -rf $HOME/.source/data
curl -o - -L http://source.snapshot.stavr.tech:4001/source/source-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.source --strip-components 2
curl -o - -L http://source.wasm.stavr.tech:1050/wasm-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.source/data --strip-components 3
mv $HOME/.source/priv_validator_state.json.backup $HOME/.source/data/priv_validator_state.json
wget -O $HOME/.source/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Source/addrbook.json"
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1false|" ~/.source/config/config.toml
sudo systemctl restart sourced && journalctl -u sourced -f -o cat
```
<h1 align="center"> Useful Tools</h1>

🔥EXPLORER-M🔥:    https://explorer.stavr.tech/Source-Mainnet/staking    `Indexer "ON"` \
🔥EXPLORER-T🔥:    https://explorer.stavr.tech/Source/staking            `Indexer "ON"` \
🔥API-M🔥:         https://source.api.m.stavr.tech \
🔥API-T🔥:         https://source.api.t.stavr.tech \
🔥RPC-M🔥:         https://source.rpc.m.stavr.tech:443              `Snapshot-interval = 100` \
🔥gRPC-M🔥:        http://source.grpc.m.stavr.tech:9590 \
🔥peer-M🔥:        `9751bfbbb3303db1898ef5c601d8522938623262@source.peers.stavr.tech:20056` \
🔥Addrbook-M🔥: `wget -O $HOME/.source/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Source/addrbook.json"` \
🔥Addrbook-T🔥: `wget -O $HOME/.source/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Source/addrbook.json"` \
🔥Auto_install script-M🔥: `wget -O sourcem https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Source/sourcem && chmod +x sourcem && ./sourcem` \
🔥Auto_install script-T🔥: `wget -O sources https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Source/Testnet/sources && chmod +x sources && ./sources`


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

[raw json Mainnet](https://rpc-check.sourcem.stavr.tech/sourcem/rpc-sourcem-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>182.42.93.241:26657</td><td>source-1</td><td>1024dao 🔴</td><td>774677</td><td>1</td><td>False</td><td>603</td><td>2023-11-30T11:03:39.163159538UTC</td></tr><tr><td>182.42.88.202:26657</td><td>source-1</td><td>antennaa 🔴</td><td>774677</td><td>1</td><td>False</td><td>187</td><td>2023-11-30T11:03:40.607843555UTC</td></tr><tr><td>182.42.82.11:26657</td><td>source-1</td><td>topman 🔴</td><td>774677</td><td>1</td><td>False</td><td>117</td><td>2023-11-30T11:03:42.090195427UTC</td></tr><tr><td>218.78.113.63:26657</td><td>source-1</td><td>tapeclaw 🔴</td><td>774679</td><td>1</td><td>False</td><td>155</td><td>2023-11-30T11:03:48.465915076UTC</td></tr><tr><td>168.119.36.251:12657</td><td>source-1</td><td>Indonode-Service 🟢</td><td>774681</td><td>1</td><td>False</td><td>0</td><td>2023-11-30T11:03:59.109229186UTC</td></tr><tr><td>101.91.119.133:26657</td><td>source-1</td><td>XPool 🔴</td><td>774681</td><td>1</td><td>False</td><td>139871</td><td>2023-11-30T11:04:01.142716886UTC</td></tr><tr><td>65.21.57.72:26657</td><td>source-1</td><td>WellNode 🔴</td><td>774681</td><td>628618</td><td>False</td><td>102890</td><td>2023-11-30T11:03:59.865527315UTC</td></tr><tr><td>185.248.24.51:15557</td><td>source-1</td><td>Moonbridge 🟢</td><td>774677</td><td>742763</td><td>False</td><td>0</td><td>2023-11-30T11:03:35.835401395UTC</td></tr><tr><td>135.181.210.171:20057</td><td>source-1</td><td>STAVR-Service 🟢</td><td>774681</td><td>774001</td><td>False</td><td>0</td><td>2023-11-30T11:03:59.482127667UTC</td></tr></table>