<h1 align="center"> 🔥LikeCoin🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Likecoin)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=http://like.rpc.m.stavr.tech:1007
SEEDS=fd7589625f4ad41bb93f96f4c962ed6638426497@like.peer.stavr.tech:1006
cp $HOME/.liked/data/priv_validator_state.json $HOME/.liked/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.liked/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.liked/config/config.toml
liked tendermint unsafe-reset-all --home $HOME/.liked --keep-addr-book
mv $HOME/.liked/priv_validator_state.json.backup $HOME/.liked/data/priv_validator_state.json
wget -O $HOME/.liked/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Likecoin/addrbook.json"
sudo systemctl restart liked && journalctl -u liked -f -o cat
```
# SnapShot (~50 GB) updated every 24 hours
```python
SOON
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Likecoin-M        `Indexer "ON"` \
🔥API🔥:          https://like.api.m.stavr.tech \
🔥RPC🔥:          http://like.rpc.m.stavr.tech:1007              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://like.grpc.m.stavr.tech:2000 \
🔥peer🔥:         `fd7589625f4ad41bb93f96f4c962ed6638426497@like.peer.stavr.tech:1006` \
🔥Addrbook🔥:  `wget -O $HOME/.liked/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Likecoin/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.liked/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Likecoin/genesis.json"` \
🔥Auto_install script🔥:`wget -O likem https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Likecoin/likem && chmod +x likem && ./likem`

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

[raw Mainnet json](https://rpc-check.likem.stavr.tech/likem/rpc-likem-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>154.12.227.117:26657</td><td>likecoin-mainnet-2</td><td>50%Banana 🔴</td><td>12073601</td><td>1</td><td>False</td><td>808970001</td><td>2023-12-05T12:16:12.086624814UTC</td></tr><tr><td>34.66.248.218:26657</td><td>likecoin-mainnet-2</td><td>dataxStaking 🔴</td><td>12073603</td><td>1</td><td>False</td><td>21729844821</td><td>2023-12-05T12:16:23.021664287UTC</td></tr><tr><td>203.135.141.208:26657</td><td>likecoin-mainnet-2</td><td>YasuArchive01 🟢</td><td>12073606</td><td>1</td><td>False</td><td>0</td><td>2023-12-05T12:16:38.305865853UTC</td></tr><tr><td>154.53.63.22:26657</td><td>likecoin-mainnet-2</td><td>martianforest 🔴</td><td>12073606</td><td>1</td><td>False</td><td>879058201</td><td>2023-12-05T12:16:40.948223360UTC</td></tr><tr><td>144.126.131.195:26657</td><td>likecoin-mainnet-2</td><td>WeLike 🔴</td><td>12073602</td><td>5101130</td><td>False</td><td>115326974196</td><td>2023-12-05T12:16:17.272605884UTC</td></tr><tr><td>80.41.220.205:26657</td><td>likecoin-mainnet-2</td><td>kamkcir 🔴</td><td>12073607</td><td>5504726</td><td>False</td><td>2488831205</td><td>2023-12-05T12:16:51.665885722UTC</td></tr><tr><td>157.230.253.116:26657</td><td>likecoin-mainnet-2</td><td>SupportHK 🔴</td><td>12073608</td><td>5874201</td><td>False</td><td>8797746921</td><td>2023-12-05T12:16:54.688505128UTC</td></tr><tr><td>188.166.226.230:26657</td><td>likecoin-mainnet-2</td><td>PM 🔴</td><td>12073606</td><td>7730955</td><td>False</td><td>22429725113</td><td>2023-12-05T12:16:41.982473159UTC</td></tr><tr><td>35.221.209.211:26657</td><td>likecoin-mainnet-2</td><td>Oursky 🔴</td><td>12073607</td><td>8394252</td><td>False</td><td>29555751158</td><td>2023-12-05T12:16:49.296627866UTC</td></tr><tr><td>207.180.238.137:26657</td><td>likecoin-mainnet-2</td><td>moonbeam-RPC 🟢</td><td>12073601</td><td>9234583</td><td>False</td><td>0</td><td>2023-12-05T12:16:12.422493837UTC</td></tr><tr><td>157.230.252.47:26657</td><td>likecoin-mainnet-2</td><td>NTUTBlockchain 🔴</td><td>12073603</td><td>9318400</td><td>False</td><td>890171118</td><td>2023-12-05T12:16:22.320607404UTC</td></tr><tr><td>111.235.217.51:26657</td><td>likecoin-mainnet-2</td><td>bubbletea 🔴</td><td>12073604</td><td>9332583</td><td>False</td><td>1004574753</td><td>2023-12-05T12:16:26.897567210UTC</td></tr><tr><td>45.33.97.75:26657</td><td>likecoin-mainnet-2</td><td>CoderNoah 🔴</td><td>12073606</td><td>11014944</td><td>False</td><td>19249607815</td><td>2023-12-05T12:16:39.981427750UTC</td></tr><tr><td>172.105.153.187:26657</td><td>likecoin-mainnet-2</td><td>mn 🔴</td><td>12073609</td><td>11233444</td><td>False</td><td>50169245105</td><td>2023-12-05T12:16:57.486355798UTC</td></tr><tr><td>165.22.106.32:26657</td><td>likecoin-mainnet-2</td><td>Liker.Social 🔴</td><td>12073604</td><td>11800823</td><td>False</td><td>45182038991</td><td>2023-12-05T12:16:30.813113283UTC</td></tr><tr><td>66.45.246.166:1007</td><td>likecoin-mainnet-2</td><td>STAVR-Service 🟢</td><td>12073604</td><td>11931594</td><td>False</td><td>0</td><td>2023-12-05T12:16:27.517869887UTC</td></tr><tr><td>165.232.173.74:26657</td><td>likecoin-mainnet-2</td><td>leafwind 🔴</td><td>12073606</td><td>12022645</td><td>False</td><td>40472049128</td><td>2023-12-05T12:16:39.306114288UTC</td></tr><tr><td>167.99.71.225:26657</td><td>likecoin-mainnet-2</td><td>liker_mxp_v2 🔴</td><td>12073610</td><td>12063837</td><td>False</td><td>26773886957</td><td>2023-12-05T12:17:06.648395181UTC</td></tr></table>
