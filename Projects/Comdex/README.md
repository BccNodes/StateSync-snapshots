<h1 align="center"> 🔥Comdex🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Comdex)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://comdex.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.comdex/config/config.toml
comdex tendermint unsafe-reset-all
wget -O $HOME/.comdex/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Comdex/addrbook.json"
curl -o - -L https://comdex.wasm.stavr.tech/wasm-comdex.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.comdex --strip-components 2
sudo systemctl restart comdex && sudo journalctl -u comdex -f -o cat
```
# SnapShot (~2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop comdex
cp $HOME/.comdex/data/priv_validator_state.json $HOME/.comdex/priv_validator_state.json.backup
rm -rf $HOME/.comdex/data
curl -o - -L https://comdex.snapshot.stavr.tech/comdex/comdex-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.comdex --strip-components 2
curl -o - -L https://comdex.wasm.stavr.tech/wasm-comdex.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.comdex --strip-components 2
mv $HOME/.comdex/priv_validator_state.json.backup $HOME/.comdex/data/priv_validator_state.json
wget -O $HOME/.comdex/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Comdex/addrbook.json"
sudo systemctl restart comdex && journalctl -u comdex -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Comdex-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://comdex.api.m.stavr.tech \
🔥RPC🔥:          https://comdex.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://comdex.grpc.m.stavr.tech:104 \
🔥seed🔥:      `c30dacf15e97a30b78792c7fa817fd2ef529b820@comdex.seed.stavr.tech:2026` \
🔥Genesis🔥:   `wget -O $HOME/.comdex/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Comdex/genesis.json"` \
🔥WASM🔥:      `curl -o - -L https://comdex.wasm.stavr.tech/wasm-comdex.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.comdex --strip-components 2` \
🔥Addrbook🔥:  `wget -O $HOME/.comdex/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Comdex/addrbook.json"` \
🔥Auto_install script🔥:`wget -O comdexm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Comdex/comdexm && chmod +x comdexm && ./comdexm`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Comdex/Decentralization)🔥
=
<h1 align="center"> RPC Scanning</h1>

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

[raw Mainnet json](https://rpc-check.comdexm.stavr.tech/comdexm/rpc-comdexm-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>46.166.172.230:26657</td><td>comdex-1</td><td>rpc-cherry 🟢</td><td>11643133</td><td>10400001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T13:28:42.072765474UTC</td></tr><tr><td>5.199.163.72:26657</td><td>comdex-1</td><td>cherry-comdex-mainnet-rpc 🟢</td><td>11643130</td><td>10982190</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T13:28:22.990555652UTC</td></tr><tr><td>62.171.182.242:56657</td><td>comdex-1</td><td>Snap2 🟢</td><td>11643119</td><td>10990001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T13:27:17.849875423UTC</td></tr><tr><td>65.108.101.19:24557</td><td>comdex-1</td><td>Validatrium-RPC 🟢</td><td>11643128</td><td>10990001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T13:28:12.170266237UTC</td></tr><tr><td>15.235.160.26:26657</td><td>comdex-1</td><td>rpc-ovh 🟢</td><td>11643120</td><td>10992661</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T13:27:24.949483163UTC</td></tr><tr><td>65.21.230.230:15657</td><td>comdex-1</td><td>Illuminati 🔴</td><td>11643125</td><td>10992661</td><td>False</td><td>off</td><td>640008</td><td>2024-02-05T13:27:51.224346825UTC</td></tr><tr><td>15.235.53.45:26657</td><td>comdex-1</td><td>Comdex-RPC 🟢</td><td>11643121</td><td>11315028</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T13:27:31.784463513UTC</td></tr><tr><td>57.128.20.238:42657</td><td>comdex-1</td><td>rpc 🟢</td><td>11643128</td><td>11551985</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T13:28:12.432277469UTC</td></tr><tr><td>66.45.246.166:2027</td><td>comdex-1</td><td>STAVR-Service 🟢</td><td>11643122</td><td>11639301</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T13:27:38.478624964UTC</td></tr></table>
