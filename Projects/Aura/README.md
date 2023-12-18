<h1 align="center"> 🔥Aura🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Aura)
=
<h1 align="center"> MAINNET</h1>


# State Sync
```python
SNAP_RPC=http://aura.rpc.m.stavr.tech:11047
SEEDS="7cefc9a64cd34f6de30e0289d16ee83978f309cc@aura.peers.stavr.tech:21056"
cp $HOME/.aura/data/priv_validator_state.json $HOME/.aura/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.aura/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.aura/config/config.toml
aurad tendermint unsafe-reset-all --home $HOME/.aura --keep-addr-book
mv $HOME/.aura/priv_validator_state.json.backup $HOME/.aura/data/priv_validator_state.json
curl -o - -L http://aura.wasm.stavr.tech:1001/wasm-aura.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.aura --strip-components 2
wget -O $HOME/.aura/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Aura/addrbook.json"
sudo systemctl restart aurad && journalctl -u aurad -f -o cat
```
# SnapShot (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop aurad
cp $HOME/.aura/data/priv_validator_state.json $HOME/.aura/priv_validator_state.json.backup
rm -rf $HOME/.aura/data
curl -o - -L http://aura.snapshot.stavr.tech:5015/aura/aura-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.aura --strip-components 2
curl -o - -L http://aura.wasm.stavr.tech:1102/wasm-aura.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.aura --strip-components 2
mv $HOME/.aura/priv_validator_state.json.backup $HOME/.aura/data/priv_validator_state.json
wget -O $HOME/.aura/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Aura/addrbook.json"
sudo systemctl restart aurad && journalctl -u aurad -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Aura-Mainnet/staking        `Indexer "ON"` \
🔥API🔥:          https://aura.api.m.stavr.tech \
🔥RPC🔥:          http://aura.rpc.m.stavr.tech:11047              `Snapshot-interval = 100` \
🔥gRPC🔥:         http://aura.grpc.m.stavr.tech:9901 \
🔥peer🔥:         `7cefc9a64cd34f6de30e0289d16ee83978f309cc@aura.peers.stavr.tech:21056` \
🔥WASM Mainnet🔥:`curl -o - -L http://aura.wasm.stavr.tech:1102/wasm-aura.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.aura --strip-components 2` \
🔥Addrbook🔥:  `wget -O $HOME/.aura/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Aura/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.aura/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Aura/genesis.json"` \
🔥Auto_install script🔥:`wget -O auram https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Aura/auram && chmod +x auram && ./auram`

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

[raw Mainnet json](https://rpc-check.auram.stavr.tech/auram/rpcauram_result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>148.251.88.145:10457</td><td>xstaxy-1</td><td>palamar-archive-node 🟢</td><td>4138138</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T05:19:40.863945978UTC</td></tr><tr><td>65.109.93.152:34657</td><td>xstaxy-1</td><td>AlxVoy 🟢</td><td>4138140</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T05:19:52.345770443UTC</td></tr><tr><td>142.132.202.86:30001</td><td>xstaxy-1</td><td>ramuchi.tech 🟢</td><td>4138141</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T05:19:55.506719506UTC</td></tr><tr><td>65.108.141.109:54657</td><td>xstaxy-1</td><td>node 🟢</td><td>4138139</td><td>151001</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T05:19:43.327221739UTC</td></tr><tr><td>65.108.75.107:54657</td><td>xstaxy-1</td><td>node 🟢</td><td>4138142</td><td>151001</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T05:20:00.247719326UTC</td></tr><tr><td>195.3.221.76:21657</td><td>xstaxy-1</td><td>stakr-space 🔴</td><td>4138135</td><td>864001</td><td>False</td><td>on</td><td>2000010</td><td>2023-12-18T05:19:21.317852584UTC</td></tr><tr><td>65.108.135.212:23357</td><td>xstaxy-1</td><td>2xStake.com 🔴</td><td>4138146</td><td>1292001</td><td>False</td><td>off</td><td>500059</td><td>2023-12-18T05:20:25.856712639UTC</td></tr><tr><td>174.138.180.190:60757</td><td>xstaxy-1</td><td>UTSA_guide 🟢</td><td>4138135</td><td>2058001</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T05:19:22.069754101UTC</td></tr><tr><td>185.162.249.161:28657</td><td>xstaxy-1</td><td>tienthuattoan 🟢</td><td>4138141</td><td>2511001</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T05:19:55.819301905UTC</td></tr><tr><td>208.77.197.83:27657</td><td>xstaxy-1</td><td>vidulum.app 🟢</td><td>4138134</td><td>3205801</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T05:19:16.762169904UTC</td></tr><tr><td>217.144.98.50:26657</td><td>xstaxy-1</td><td>Noderunners 🔴</td><td>4138141</td><td>3416001</td><td>False</td><td>off</td><td>2019398</td><td>2023-12-18T05:19:55.168192222UTC</td></tr><tr><td>95.217.207.236:27557</td><td>xstaxy-1</td><td>web34ever 🟢</td><td>4083908</td><td>3529001</td><td>False</td><td>off</td><td>0</td><td>2023-12-18T05:20:04.647637494UTC</td></tr><tr><td>65.108.195.29:51657</td><td>xstaxy-1</td><td>Staketab-snap 🟢</td><td>4138140</td><td>3761101</td><td>False</td><td>off</td><td>0</td><td>2023-12-18T05:19:51.931485543UTC</td></tr><tr><td>144.76.45.59:20657</td><td>xstaxy-1</td><td>RPCHuginn 🟢</td><td>4083908</td><td>3962157</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T05:19:52.598335888UTC</td></tr><tr><td>135.181.210.171:11047</td><td>xstaxy-1</td><td>STAVR-Service 🟢</td><td>4138145</td><td>4136501</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T05:20:19.317066701UTC</td></tr></table>
