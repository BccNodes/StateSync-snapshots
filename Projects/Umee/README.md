<h1 align="center"> 🔥Umee🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Umee)
=
# StateSync Umee
```python
SNAP_RPC=http://umee.rpc.m.stavr.tech:10457
peers="c014463cb2de618bef420e40f503c5e57decade4@umee.peers.m.stavr.tech:10456"
sed -i -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.umee/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.umee/config/config.toml
umeed tendermint unsafe-reset-all --home $HOME/.umee
wget -O $HOME/.umee/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/addrbook.json"
sudo systemctl restart umeed && journalctl -u umeed -f -o cat
```
# SnapShot (~0.9 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop umeed
cp $HOME/.umee/data/priv_validator_state.json $HOME/.umee/priv_validator_state.json.backup
rm -rf $HOME/.umee/data
curl -o - -L http://umee.snapshot.stavr.tech:1000/umee/umee-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.umee --strip-components 2
wget -O $HOME/.umee/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/addrbook.json"
mv $HOME/.umee/priv_validator_state.json.backup $HOME/.umee/data/priv_validator_state.json
sudo systemctl restart umeed && journalctl -u umeed -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Umee/staking             `Indexer "ON"` \
🔥EXPLORER Testnet🔥:        https://explorer.stavr.tech/umee-canon/staking      `Indexer "ON"` \
🔥API Mainnet🔥:                   https://umee.api.m.stavr.tech \
🔥API Testnet🔥:                     https://umee.api.t.stavr.tech \
🔥RPC🔥:                                   http://umee.rpc.m.stavr.tech:10457                     `Snapshot-interval = 300` \
🔥gRPC🔥:                              http://umee.grpc.m.stavr.tech:1190 \
🔥peer🔥:                     `c014463cb2de618bef420e40f503c5e57decade4@umee.peers.m.stavr.tech:10456` \
🔥Addrbook🔥:    ```wget -O $HOME/.umee/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O Ume https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/Ume && chmod +x Ume && ./Ume```

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

[raw json Mainnet](https://rpc-check.umeem.stavr.tech/umeem/rpc-umeem-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>148.251.88.145:10257</td><td>umee-1</td><td>node 🟢</td><td>9561500</td><td>5050395</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:22:39.802303014UTC</td></tr><tr><td>135.125.4.73:26657</td><td>umee-1</td><td>rpc-1.umee.nodes.guru 🟢</td><td>9747815</td><td>5167386</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:24:23.727542123UTC</td></tr><tr><td>213.246.45.198:26657</td><td>umee-1</td><td>id577 🔴</td><td>9747798</td><td>7100001</td><td>False</td><td>on</td><td>35117505</td><td>2023-12-19T09:22:44.269854527UTC</td></tr><tr><td>5.9.106.214:10257</td><td>umee-1</td><td>node 🟢</td><td>9747810</td><td>7942001</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:23:54.280951889UTC</td></tr><tr><td>95.216.76.51:26657</td><td>umee-1</td><td>Egozit 🔴</td><td>9747815</td><td>8262001</td><td>False</td><td>off</td><td>37992791</td><td>2023-12-19T09:24:23.354883259UTC</td></tr><tr><td>85.10.197.58:13657</td><td>umee-1</td><td>BRAND-umee-main 🟢</td><td>9747801</td><td>8427832</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:23:03.689036000UTC</td></tr><tr><td>65.108.106.252:26657</td><td>umee-1</td><td>qubelabs 🔴</td><td>9747801</td><td>8825432</td><td>False</td><td>on</td><td>36486849</td><td>2023-12-19T09:23:04.018898831UTC</td></tr><tr><td>23.88.7.159:11057</td><td>umee-1</td><td>StakeVillage_guide 🔴</td><td>9747808</td><td>9137726</td><td>False</td><td>on</td><td>1402112</td><td>2023-12-19T09:23:44.554582742UTC</td></tr><tr><td>95.217.202.49:27657</td><td>umee-1</td><td>rpc 🟢</td><td>9747807</td><td>9440090</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:23:35.763477588UTC</td></tr><tr><td>194.60.201.146:26657</td><td>umee-1</td><td>medium-rpc 🟢</td><td>9747799</td><td>9484365</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:22:52.805392841UTC</td></tr><tr><td>65.108.235.36:19657</td><td>umee-1</td><td>umee-yieldmos-2 🟢</td><td>9747791</td><td>9575548</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:22:02.699946932UTC</td></tr><tr><td>95.216.77.56:26657</td><td>umee-1</td><td>L0vd2 🔴</td><td>9747817</td><td>9647817</td><td>False</td><td>off</td><td>37144225</td><td>2023-12-19T09:24:41.001454409UTC</td></tr><tr><td>195.201.174.109:26657</td><td>umee-1</td><td>iptrade_ibc 🟢</td><td>9747803</td><td>9686001</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:23:14.522267305UTC</td></tr><tr><td>65.21.91.99:16857</td><td>umee-1</td><td>Staketab-snapshot 🟢</td><td>9747804</td><td>9721001</td><td>False</td><td>off</td><td>0</td><td>2023-12-19T09:23:16.971550575UTC</td></tr><tr><td>94.250.203.6:26697</td><td>umee-1</td><td>AlexRPC 🟢</td><td>9747800</td><td>9722001</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:22:57.319154530UTC</td></tr><tr><td>185.162.249.161:27657</td><td>umee-1</td><td>ttt 🟢</td><td>9747807</td><td>9733423</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:23:36.128418685UTC</td></tr><tr><td>202.65.150.1:1556</td><td>umee-1</td><td>snap 🟢</td><td>9747809</td><td>9742023</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:23:49.845556734UTC</td></tr><tr><td>135.181.210.171:10457</td><td>umee-1</td><td>STAVR-Service 🟢</td><td>9747816</td><td>9744001</td><td>False</td><td>on</td><td>0</td><td>2023-12-19T09:24:30.381620394UTC</td></tr></table>