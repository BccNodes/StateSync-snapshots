<h1 align="center"> 🔥AndromedaProtocol Mainnet🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/AndromedaProtocol)
=

# StateSync Andromedad Mainnet
```python
SNAP_RPC=https://andro.rpc.m.stavr.tech:443
peers=e4c2267b90c7cfbb45090ab7647dc01df97f58f9@andromeda-m.peer.stavr.tech:4376
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.andromeda/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.andromeda/config/config.toml
andromedad tendermint unsafe-reset-all --home $HOME/.andromeda
systemctl restart andromedad && journalctl -u andromedad -f -o cat
```
# SnapShot Mainnet (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop andromedad
cp $HOME/.andromeda/data/priv_validator_state.json $HOME/.andromeda/priv_validator_state.json.backup
rm -rf $HOME/.andromeda/data
curl -o - -L http://andro.snapshot.stavr.tech:1030/andromeda/andromeda-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromeda --strip-components 2
curl -o - -L http://andro.wasm.stavr.tech:1017/wasm-andromeda.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromeda --strip-components 2
mv $HOME/.andromeda/priv_validator_state.json.backup $HOME/.andromeda/data/priv_validator_state.json
wget -O $HOME/.andromeda/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/addrbook.json"
sudo systemctl restart andromedad && journalctl -u andromedad -f -o cat
```


<h1 align="center"> 🔥AndromedaProtocol Testnet🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/AndromedaProtocol/Testnet)
=

# StateSync Andromedad Testnet (Temporarily disable)
```python
SNAP_RPC=http://andromedad.rpc.t.stavr.tech:4137
peers="d083506ef2e9d5f2ee22dabf4fa893a72e6cf483@andromedad.peer.stavr.tech:4376"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.andromedad/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.andromedad/config/config.toml
andromedad tendermint unsafe-reset-all --home $HOME/.andromedad
systemctl restart andromedad && journalctl -u andromedad -f -o cat
```
# SnapShot Testnet (~0.5 GB) (Temporarily disable)
```python
cd $HOME
apt install lz4
sudo systemctl stop andromedad
cp $HOME/.andromedad/data/priv_validator_state.json $HOME/.andromedad/priv_validator_state.json.backup
rm -rf $HOME/.andromedad/data
curl -o - -L http://andromedad.snapshot.stavr.tech:1021/andromedad/andromedad-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromedad --strip-components 2
curl -o - -L http://andromedad.wasm.stavr.tech:1002/wasm-andromedad.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromedad --strip-components 2
mv $HOME/.andromedad/priv_validator_state.json.backup $HOME/.andromedad/data/priv_validator_state.json
wget -O $HOME/.andromedad/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/addrbook.json"
sudo systemctl restart andromedad && journalctl -u andromedad -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER-M🔥:    https://explorer.stavr.tech/Andromeda-Mainnet            `Indexer "ON"` \
🔥EXPLORER-T🔥:    https://explorer.stavr.tech/Andromedad-testnet/staking            `Indexer "ON"` \
🔥API-M🔥:         https://andro.api.m.stavr.tech \
🔥API-T🔥:         https://andromedad.api.t.stavr.tech \
🔥RPC-M🔥:         https://andro.rpc.m.stavr.tech:443                  `Snapshot-interval = 100` \
🔥RPC-T🔥:         http://andromedad.rpc.t.stavr.tech:4137                  `Snapshot-interval = 100` \
🔥gRPC-M🔥:        http://andromedad.grpc.t.stavr.tech:132 \
🔥gRPC-T🔥:        http://andromedad.grpc.t.stavr.tech:11090 \
🔥peer-M🔥:        `e4c2267b90c7cfbb45090ab7647dc01df97f58f9@andromeda-m.peer.stavr.tech:4376` \
🔥peer-T🔥:        `d083506ef2e9d5f2ee22dabf4fa893a72e6cf483@andromedad.peer.stavr.tech:4376` \
🔥WASM-M🔥: updated every 2 hours `curl -o - -L http://andro.wasm.stavr.tech:1017/wasm-andromeda.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromeda --strip-components 2` \
🔥WASM-T🔥: updated every 2 hours `curl -o - -L http://andromedad.wasm.stavr.tech:1002/wasm-andromedad.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromedad --strip-components 2` \
🔥Genesis-M🔥: `wget -O $HOME/.andromeda/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/genesis.json"` \
🔥Genesis-T🔥: `wget -O $HOME/.andromedad/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/Testnet/genesis.json"` \
🔥Addrbook-M🔥: `wget -O $HOME/.andromeda/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/addrbook.json"` \
🔥Addrbook-T🔥: `wget -O $HOME/.andromedad/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/Testnet/addrbook.json"` \
🔥Auto_install script-T🔥: `wget -O adprotocol https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/Testnet/adprotocol && chmod +x adprotocol && ./adprotocol`

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

[raw json](https://rpc-check.androt.stavr.tech/androt/rpcandrot_result.json)
=

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.93.35:50657</td><td>galileo-3</td><td>Synergy_Nodes 🟢</td><td>3948149</td><td>0</td><td>False</td><td>0</td><td>2023-11-24T09:05:01.352301211UTC</td></tr><tr><td>65.108.199.120:61357</td><td>galileo-3</td><td>RAMZES 🟢</td><td>3948146</td><td>1</td><td>False</td><td>0</td><td>2023-11-24T09:04:43.158344594UTC</td></tr><tr><td>142.132.209.236:21257</td><td>galileo-3</td><td>a4951031-6d09-5ee9-9e28-e063741b480d 🔴</td><td>3948148</td><td>1</td><td>False</td><td>3</td><td>2023-11-24T09:04:56.500791448UTC</td></tr><tr><td>65.21.133.114:56657</td><td>galileo-3</td><td>Staketab 🔴</td><td>3948149</td><td>90001</td><td>False</td><td>2</td><td>2023-11-24T09:05:02.293362334UTC</td></tr><tr><td>65.109.70.45:15657</td><td>galileo-3</td><td>L0vd.com 🔴</td><td>3948149</td><td>659001</td><td>False</td><td>3</td><td>2023-11-24T09:05:00.982810378UTC</td></tr><tr><td>65.109.116.119:14757</td><td>galileo-3</td><td>semalist 🔴</td><td>3948145</td><td>2228721</td><td>False</td><td>1318</td><td>2023-11-24T09:04:35.967601985UTC</td></tr><tr><td>213.239.207.175:42657</td><td>galileo-3</td><td>landeros 🔴</td><td>3948143</td><td>2642001</td><td>False</td><td>72</td><td>2023-11-24T09:04:24.258963410UTC</td></tr><tr><td>161.97.152.157:27657</td><td>galileo-3</td><td>cardex 🟢</td><td>3948149</td><td>2945323</td><td>False</td><td>0</td><td>2023-11-24T09:05:01.939971137UTC</td></tr><tr><td>65.109.88.254:40657</td><td>galileo-3</td><td>ksalab 🔴</td><td>3948145</td><td>3000356</td><td>False</td><td>31921</td><td>2023-11-24T09:04:36.686387495UTC</td></tr><tr><td>78.46.103.246:60957</td><td>galileo-3</td><td>F5Nodes 🔴</td><td>3948149</td><td>3057001</td><td>False</td><td>24</td><td>2023-11-24T09:05:01.605293920UTC</td></tr><tr><td>65.108.227.112:14657</td><td>galileo-3</td><td>[NODERS]TEAM 🔴</td><td>3948143</td><td>3176323</td><td>False</td><td>959616</td><td>2023-11-24T09:04:24.624791805UTC</td></tr><tr><td>138.201.53.44:33657</td><td>galileo-3</td><td>EdWWWardo 🟢</td><td>3948144</td><td>3406335</td><td>False</td><td>0</td><td>2023-11-24T09:04:29.112194697UTC</td></tr><tr><td>194.34.232.224:56657</td><td>galileo-3</td><td>andromeda 🟢</td><td>3948145</td><td>3848145</td><td>False</td><td>0</td><td>2023-11-24T09:04:36.324320535UTC</td></tr><tr><td>65.21.170.3:32657</td><td>galileo-3</td><td>Munris 🔴</td><td>3948147</td><td>3848147</td><td>False</td><td>411</td><td>2023-11-24T09:04:50.090656352UTC</td></tr><tr><td>194.163.174.231:26677</td><td>galileo-3</td><td>AviaDoc_by_AviaOne 🟢</td><td>3948147</td><td>3928001</td><td>False</td><td>0</td><td>2023-11-24T09:04:49.724495078UTC</td></tr></table>
