<h1 align="center"> 🔥Ojo🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Ojo)
=

<h1 align="center"> TESTNET</h1>

# StateSync Ojo Testnet
```python
SNAP_RPC=http://ojo.rpc.t.stavr.tech:37097
peers="1f091cf9567c0d72a0f93877007379e0298b8860@ojo.peer.stavr.tech:37096"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.ojo/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.ojo/config/config.toml
ojod tendermint unsafe-reset-all --home /root/.ojo --keep-addr-book
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.ojo/config/app.toml
sudo systemctl restart ojod && journalctl -u ojod -f -o cat
```
# SnapShot (~0.4 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop ojod
cp $HOME/.ojo/data/priv_validator_state.json $HOME/.ojo/priv_validator_state.json.backup
rm -rf $HOME/.ojo/data
curl -o - -L http://ojo.snapshot.stavr.tech:1026/ojo/ojo-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.ojo --strip-components 2
mv $HOME/.ojo/priv_validator_state.json.backup $HOME/.ojo/data/priv_validator_state.json
wget -O $HOME/.ojo/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/addrbook.json"
sudo systemctl restart ojod && journalctl -u ojod -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:        https://explorer.stavr.tech/Ojo-Devnet/staking        `Indexer "ON"` \
🔥API🔥:                     https://ojo.api.t.stavr.tech \
🔥RPC🔥:                    http://ojo.rpc.t.stavr.tech:37097              `Snapshot-interval = 100` \
🔥gRPC🔥:                  http://ojo.grpc.t.stavr.tech:7729 \
🔥peer🔥:                   `1f091cf9567c0d72a0f93877007379e0298b8860@ojo.peer.stavr.tech:37096` \
🔥Genesis🔥:    ```wget -O $HOME/.ojo/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/genesis.json"``` \
🔥Addrbook🔥:    ```wget -O $HOME/.ojo/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O ojjo https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/ojjo && chmod +x ojjo && ./ojjo``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Ojo/Decentralization)🔥



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

[raw json Testnet](https://rpc-check.ojot.stavr.tech/ojot/rpc-ojot-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.108.199.120:54657</td><td>ojo-devnet</td><td>RAMZES 🔴</td><td>4725876</td><td>306156</td><td>False</td><td>on</td><td>15420</td><td>2023-12-30T04:21:52.056063163UTC</td></tr><tr><td>136.243.88.91:7331</td><td>ojo-devnet</td><td>ojo_testnet 🔴</td><td>4725877</td><td>308845</td><td>False</td><td>on</td><td>1000</td><td>2023-12-30T04:21:58.343936690UTC</td></tr><tr><td>142.132.209.236:21657</td><td>ojo-devnet</td><td>node 🔴</td><td>4725880</td><td>350001</td><td>False</td><td>on</td><td>1999</td><td>2023-12-30T04:22:14.321615829UTC</td></tr><tr><td>65.109.70.45:16657</td><td>ojo-devnet</td><td>L0vd.com 🔴</td><td>4725882</td><td>695918</td><td>False</td><td>off</td><td>998</td><td>2023-12-30T04:22:25.176680145UTC</td></tr><tr><td>65.109.93.152:33657</td><td>ojo-devnet</td><td>AlxVoy 🔴</td><td>4725880</td><td>2319801</td><td>False</td><td>on</td><td>4536782</td><td>2023-12-30T04:22:14.036280342UTC</td></tr><tr><td>213.239.207.175:47657</td><td>ojo-devnet</td><td>landeros 🔴</td><td>4725879</td><td>2714001</td><td>False</td><td>off</td><td>11083</td><td>2023-12-30T04:22:09.274553290UTC</td></tr><tr><td>158.220.92.97:26677</td><td>ojo-devnet</td><td>AVIAONE 🔴</td><td>4725879</td><td>2754001</td><td>False</td><td>on</td><td>13867</td><td>2023-12-30T04:22:09.032804316UTC</td></tr><tr><td>77.54.1.75:1203</td><td>ojo-devnet</td><td>don 🔴</td><td>4725880</td><td>2906401</td><td>False</td><td>on</td><td>10</td><td>2023-12-30T04:22:17.152042697UTC</td></tr><tr><td>95.217.225.212:36657</td><td>ojo-devnet</td><td>Firstcome 🔴</td><td>4725877</td><td>2985946</td><td>False</td><td>on</td><td>13566</td><td>2023-12-30T04:21:58.088261040UTC</td></tr><tr><td>213.239.194.132:50657</td><td>ojo-devnet</td><td>semalist 🔴</td><td>4725876</td><td>3223522</td><td>False</td><td>on</td><td>19037</td><td>2023-12-30T04:21:52.285688861UTC</td></tr><tr><td>95.217.224.252:19657</td><td>ojo-devnet</td><td>Galaxynode 🔴</td><td>4725881</td><td>3685492</td><td>False</td><td>on</td><td>11888</td><td>2023-12-30T04:22:22.147773323UTC</td></tr><tr><td>65.108.238.61:20657</td><td>ojo-devnet</td><td>alex 🔴</td><td>4725876</td><td>4158001</td><td>False</td><td>on</td><td>11359</td><td>2023-12-30T04:21:51.732992880UTC</td></tr><tr><td>78.46.99.50:22657</td><td>ojo-devnet</td><td>Staketab 🔴</td><td>4725882</td><td>4254801</td><td>False</td><td>on</td><td>1276</td><td>2023-12-30T04:22:25.421296143UTC</td></tr><tr><td>178.18.254.211:11657</td><td>ojo-devnet</td><td>CosmoBook 🔴</td><td>4725880</td><td>4392001</td><td>False</td><td>off</td><td>1057</td><td>2023-12-30T04:22:16.714456722UTC</td></tr><tr><td>51.159.220.202:26657</td><td>ojo-devnet</td><td>Blockscope.net 🔴</td><td>4725876</td><td>4425001</td><td>False</td><td>on</td><td>981</td><td>2023-12-30T04:21:51.352260710UTC</td></tr><tr><td>94.130.142.94:34657</td><td>ojo-devnet</td><td>EdWWWardo 🟢</td><td>4725879</td><td>4438946</td><td>False</td><td>on</td><td>0</td><td>2023-12-30T04:22:11.629460175UTC</td></tr><tr><td>142.132.134.112:25357</td><td>ojo-devnet</td><td>Pro-Nodes75 🔴</td><td>4725876</td><td>4625876</td><td>False</td><td>on</td><td>24651</td><td>2023-12-30T04:21:55.222014338UTC</td></tr><tr><td>65.21.170.3:38657</td><td>ojo-devnet</td><td>Munris 🔴</td><td>4725877</td><td>4625877</td><td>False</td><td>off</td><td>20123</td><td>2023-12-30T04:21:57.649484564UTC</td></tr><tr><td>65.108.227.112:15057</td><td>ojo-devnet</td><td>[NODERS]TEAM 🔴</td><td>4725881</td><td>4625881</td><td>False</td><td>off</td><td>9999</td><td>2023-12-30T04:22:22.533255668UTC</td></tr><tr><td>138.201.85.176:26697</td><td>ojo-devnet</td><td>ojo-devnet 🔴</td><td>4725882</td><td>4625882</td><td>False</td><td>on</td><td>1000024000</td><td>2023-12-30T04:22:24.851922559UTC</td></tr><tr><td>88.198.32.17:39657</td><td>ojo-devnet</td><td>node 🔴</td><td>4725880</td><td>4710001</td><td>False</td><td>on</td><td>80975</td><td>2023-12-30T04:22:17.386624114UTC</td></tr><tr><td>135.181.210.171:37097</td><td>ojo-devnet</td><td>STAVR-Service 🟢</td><td>4725876</td><td>4725101</td><td>False</td><td>on</td><td>0</td><td>2023-12-30T04:21:52.943592376UTC</td></tr></table>
