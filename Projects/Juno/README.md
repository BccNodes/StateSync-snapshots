<h1 align="center"> 🔥JUNO🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Juno)
=

<h1 align="center"> MAINNET</h1>

# StateSync Juno Mainnet
```python
SNAP_RPC=http://juno.rpc.m.stavr.tech:1067
PEERS="9ec270e1b4cdd38557da9d374ae4333145ee9300@juno.peer.stavr.tech:1066"
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.juno/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.juno/config/config.toml
junod tendermint unsafe-reset-all
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.juno/config/app.toml
curl -o - -L http://juno.wasm.stavr.tech:1005/wasm-juno.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2
sudo systemctl restart junod && journalctl -u junod -f -o cat
```
# SnapShot (~12 GB) updated every 12 hours
```python
cd $HOME
snap install lz4
sudo systemctl stop junod
cp $HOME/.juno/data/priv_validator_state.json $HOME/.juno/priv_validator_state.json.backup
rm -rf $HOME/.juno/data
curl -o - -L http://juno.snapshot.stavr.tech:1024/juno/juno-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno --strip-components 2
curl -o - -L http://juno.wasm.stavr.tech:1005/wasm-juno.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2
mv $HOME/.juno/priv_validator_state.json.backup $HOME/.juno/data/priv_validator_state.json
wget -O $HOME/.juno/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/addrbook.json"
sudo systemctl restart junod && journalctl -u junod -f -o cat
```

<h1 align="center"> TESTNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Juno/Testnet)
=

# StateSync Juno Testnet (Temporarily stopped)
```python
SNAP_RPC=http://juno.rpc.t.stavr.tech:1067
PEERS="518d31bf039289b6c8d8defd7e9509d8e28b7cd3@junot.peer.stavr.tech:1066"
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.juno/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.juno/config/config.toml
junod tendermint unsafe-reset-all --home $HOME/.juno
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.juno/config/app.toml
curl -o - -L http://juno-t.wasm.stavr.tech:1001/wasm-junot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2
sudo systemctl restart junod && journalctl -u junod -f -o cat
```

# SnapShot (~5GB) updated every 5 hours (Temporarily stopped)
```python
cd $HOME
snap install lz4
sudo systemctl stop junod
cp $HOME/.juno/data/priv_validator_state.json $HOME/.juno/priv_validator_state.json.backup
rm -rf $HOME/.juno/data
curl -o - -L http://junot.snapshot.stavr.tech:1030/junot/junot-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno --strip-components 2
curl -o - -L http://juno-t.wasm.stavr.tech:1001/wasm-junot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2
mv $HOME/.juno/priv_validator_state.json.backup $HOME/.juno/data/priv_validator_state.json
wget -O $HOME/.juno/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/Testnet/addrbook.json"
sudo systemctl restart junod && journalctl -u junod -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Juno/staking		        `Indexer "ON"` \
🔥EXPLORER Testnet🔥:      https://explorer.stavr.tech/Juno-Testnet/staking       `Indexer "ON"` \
🔥API Mainnet🔥: 			 		 https://juno.api.m.stavr.tech \
🔥API Testnet🔥: 			 		 https://juno.api.t.stavr.tech \
🔥RPC Mainnet🔥:           http://juno.rpc.m.stavr.tech:1067              `Snapshot-interval = 1000` \
🔥RPC Testnet🔥:           http://juno.rpc.t.stavr.tech:1067              `Snapshot-interval = 1000` \
🔥gRPC Mainnet🔥:          http://juno.grpc.m.stavr.tech:504 \
🔥gRPC Testnet🔥:          http://juno.grpc.t.stavr.tech:504 \
🔥peer Mainnet🔥:					 `9ec270e1b4cdd38557da9d374ae4333145ee9300@juno.peer.stavr.tech:1066` \
🔥peer Testnet🔥:					 `eb4cbf9bfea70a9e02baffbe35df02f073c70049@junot.peer.stavr.tech:1066` \
🔥WASM Mainnet🔥: 		 ```curl -o - -L http://juno.wasm.stavr.tech:1005/wasm-juno.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2```		`updated every 10 minutes` \
🔥WASM Testnet🔥: 		 ```curl -o - -L http://juno-t.wasm.stavr.tech:1001/wasm-junot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2```   `updated every 5 minutes` \
🔥Genesis Mainnet🔥:     ```wget -O $HOME/.juno/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/genesis.json"``` \
🔥Genesis Testnet🔥:	 ```wget -O $HOME/.juno/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/Testnet/genesis.json"``` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.juno/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.juno/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/Testnet/addrbook.json"``` \
🔥Auto_install script Mainnet🔥: ```wget -O jun https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/jun && chmod +x jun && ./jun``` \
🔥Auto_install script Testnet🔥: ```wget -O juno-t https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/Testnet/juno-t && chmod +x juno-t && ./juno-t``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Juno/Decentralization)🔥

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

[raw json Mainnet](https://rpc-check.junom.stavr.tech/junom/rpc-junom-result.json) \
[raw json Testnet](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Juno/Rpc-Check-Testnet)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>93.189.27.177:26657</td><td>juno-1</td><td>blockpitnode 🟢</td><td>13450874</td><td>9074001</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:03:06.805097834UTC</td></tr><tr><td>66.172.36.140:11657</td><td>juno-1</td><td>node 🟢</td><td>13450877</td><td>11389910</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:03:16.666732617UTC</td></tr><tr><td>148.113.159.221:36657</td><td>juno-1</td><td>thick_boi 🟢</td><td>12265007</td><td>11722438</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:02:36.258551997UTC</td></tr><tr><td>65.108.98.235:38857</td><td>juno-1</td><td>sentry-4 🟢</td><td>13450850</td><td>11772968</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:01:43.972287788UTC</td></tr><tr><td>135.181.1.44:26657</td><td>juno-1</td><td>rpc-3 🟢</td><td>13450853</td><td>12279533</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:01:58.783044276UTC</td></tr><tr><td>141.94.195.104:26657</td><td>juno-1</td><td>rpc-8 🟢</td><td>13450861</td><td>12279533</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:02:24.696779790UTC</td></tr><tr><td>65.21.74.247:24657</td><td>juno-1</td><td>#SoloNation 🔴</td><td>13450846</td><td>12379123</td><td>False</td><td>on</td><td>2678</td><td>2024-01-27T18:01:32.800802648UTC</td></tr><tr><td>213.239.213.142:12657</td><td>juno-1</td><td>BRAND-juno-relayer 🟢</td><td>13450803</td><td>12429275</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T17:59:08.968234649UTC</td></tr><tr><td>66.172.36.139:11657</td><td>juno-1</td><td>node 🟢</td><td>13450799</td><td>12454834</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T17:59:02.460383184UTC</td></tr><tr><td>65.108.44.124:36010</td><td>juno-1</td><td>bricks_juno 🟢</td><td>13450856</td><td>12480440</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:02:09.766251092UTC</td></tr><tr><td>57.128.20.238:34657</td><td>juno-1</td><td>rpc 🟢</td><td>13450863</td><td>12683032</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:02:29.275323267UTC</td></tr><tr><td>142.132.253.13:49657</td><td>juno-1</td><td>rpcs 🟢</td><td>13450824</td><td>12960671</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:00:18.333070182UTC</td></tr><tr><td>138.201.21.121:24957</td><td>juno-1</td><td>Validatrium-rpc 🟢</td><td>13450790</td><td>13084801</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T17:58:28.416295943UTC</td></tr><tr><td>65.108.125.93:26657</td><td>juno-1</td><td>juno 🟢</td><td>13450817</td><td>13110265</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T17:59:57.418754299UTC</td></tr><tr><td>75.26.237.223:36657</td><td>juno-1</td><td>test 🟢</td><td>13450882</td><td>13142921</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:03:36.095520850UTC</td></tr><tr><td>176.9.139.74:36657</td><td>juno-1</td><td>myrpc 🟢</td><td>13450874</td><td>13186740</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:03:07.237361067UTC</td></tr><tr><td>95.168.173.33:18657</td><td>juno-1</td><td>JUNO-mainnet-prod 🔴</td><td>13450919</td><td>13200919</td><td>False</td><td>on</td><td>6358</td><td>2024-01-27T18:05:42.450173955UTC</td></tr><tr><td>194.163.172.115:12657</td><td>juno-1</td><td>Stake&Relax-juno-main 🟢</td><td>13450848</td><td>13284001</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:01:39.498938123UTC</td></tr><tr><td>135.181.210.171:1067</td><td>juno-1</td><td>STAVR-Service 🟢</td><td>13450908</td><td>13288194</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:05:01.446171967UTC</td></tr><tr><td>135.148.171.218:26657</td><td>juno-1</td><td>https://reece.sh 🟢</td><td>13450908</td><td>13350908</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:05:02.069538153UTC</td></tr><tr><td>65.108.40.61:28657</td><td>juno-1</td><td>29391 🟢</td><td>13450831</td><td>13414703</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:00:42.283065261UTC</td></tr><tr><td>202.65.150.1:1528</td><td>juno-1</td><td>snap 🟢</td><td>13450867</td><td>13444234</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T18:02:45.573731938UTC</td></tr></table>
