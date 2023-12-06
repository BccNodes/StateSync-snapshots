<h1 align="center"> 🔥QUICKSILVER🔥</h1>

<h1 align="center"> MAINNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Quicksilver)
=

# StateSync
```python
SNAP_RPC=http://quick.rpc.m.stavr.tech:21027
peers="f2846ba84070d3fdc21c09ef44bac4eeed2f8722@quick.peers.stavr.tech:21026"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.quicksilverd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.quicksilverd/config/config.toml
quicksilverd tendermint unsafe-reset-all --home $HOME/.quicksilverd --keep-addr-book
systemctl restart quicksilverd && sudo journalctl -u quicksilverd -f -o cat
```

# SnapShot (~0.4GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop quicksilverd
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1false|" ~/.quicksilverd/config/config.toml
cp $HOME/.quicksilverd/data/priv_validator_state.json $HOME/.quicksilverd/priv_validator_state.json.backup
rm -rf $HOME/.quicksilverd/data
curl -o - -L http://quick.snapshot.stavr.tech:1009/quick/quick-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.quicksilverd --strip-components 2
mv $HOME/.quicksilverd/priv_validator_state.json.backup $HOME/.quicksilverd/data/priv_validator_state.json
wget -O $HOME/.quicksilverd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/addrbook.json"
sudo systemctl restart quicksilverd && journalctl -u quicksilverd -f -o cat
```

<h1 align="center"> TESTNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Quicksilver/Tetstnet)
=

# StateSync Testnet
```python
SNAP_RPC=http://quick.rpc.t.stavr.tech:20027
peers="b3b0b1dfa5feb35b6ed88f409c2e9182784e122c@quickt.peers.stavr.tech:20026"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.quicksilverd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" ~/.quicksilverd/config/config.toml
quicksilverd tendermint unsafe-reset-all --home $HOME/.quicksilverd
systemctl restart quicksilverd && sudo journalctl -u quicksilverd -f -o cat

```

# SnapShot Testnet (~0.2GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop quicksilverd
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1false|" ~/.quicksilverd/config/config.toml
cp $HOME/.quicksilverd/data/priv_validator_state.json $HOME/.quicksilverd/priv_validator_state.json.backup
rm -rf $HOME/.quicksilverd/data
curl -o - -L http://quickt.snapshot.stavr.tech:1016/quickt/quickt-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.quicksilverd --strip-components 2
mv $HOME/.quicksilverd/priv_validator_state.json.backup $HOME/.quicksilverd/data/priv_validator_state.json
wget -O $HOME/.quicksilverd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/Tetstnet/addrbook.json"
sudo systemctl restart quicksilverd && journalctl -u quicksilverd -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:        https://explorer.stavr.tech/Quicksilver-Mainnet/staking    `Indexer "ON"` \
🔥EXPLORER Testnet🔥:        https://explorer.stavr.tech/Quicksilver/staking	        `Indexer "ON"` \
🔥API Mainnet🔥: 			 https://quick.api.m.stavr.tech \
🔥API Testnet🔥: 			 https://quick.api.t.stavr.tech \
🔥RPC Mainnet🔥:             http://quick.rpc.m.stavr.tech:21027              `Snapshot-interval = 300` \
🔥RPC Testnet🔥:             http://quick.rpc.t.stavr.tech:20027              `Snapshot-interval = 100` \
🔥gRPC Mainnet🔥:                    http://quick.grpc.m.stavr.tech:9113 \
🔥gRPC Testnet🔥:                    http://quick.grpc.t.stavr.tech:9112 \
🔥peer Mainnet🔥:					 `f2846ba84070d3fdc21c09ef44bac4eeed2f8722@quick.peers.stavr.tech:21026` \
🔥peer Testnet🔥:					 `b3b0b1dfa5feb35b6ed88f409c2e9182784e122c@quickt.peers.stavr.tech:20026` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.quicksilverd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.quicksilverd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/addrbook.json"``` \
🔥Auto_install script Mainnet🔥: ```wget -O quick https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/quick && chmod +x quick && ./quick``` \
🔥Auto_install script Testnet🔥: ```wget -O quicktest https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/Tetstnet/quicktest && chmod +x quicktest && ./quicktest```


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

[raw json Mainnet](https://rpc-check.quickm.stavr.tech/quickm/rpc-quickm-result.json) \
[raw json Testnet](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Quicksilver/Rpc-Check-Testnet)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.108.228.245:13657</td><td>quicksilver-2</td><td>RPC 🟢</td><td>4933028</td><td>2174401</td><td>False</td><td>on</td><td>0</td><td>2023-12-06T19:02:02.849813228UTC</td></tr><tr><td>94.16.123.116:26647</td><td>quicksilver-2</td><td>YTWOFUND_PERIPHER 🟢</td><td>4933019</td><td>2741001</td><td>False</td><td>on</td><td>0</td><td>2023-12-06T19:01:12.691433258UTC</td></tr><tr><td>65.108.226.26:16657</td><td>quicksilver-2</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>4933021</td><td>3251001</td><td>False</td><td>on</td><td>0</td><td>2023-12-06T19:01:22.186586462UTC</td></tr><tr><td>85.10.197.58:11157</td><td>quicksilver-2</td><td>BRAND-quicksilver-relayer 🟢</td><td>4933018</td><td>3397566</td><td>False</td><td>on</td><td>0</td><td>2023-12-06T19:01:09.929993946UTC</td></tr><tr><td>65.109.28.177:28657</td><td>quicksilver-2</td><td>AlxVoy 🟢</td><td>4933031</td><td>3562001</td><td>False</td><td>off</td><td>0</td><td>2023-12-06T19:02:19.919937985UTC</td></tr><tr><td>95.217.202.49:31657</td><td>quicksilver-2</td><td>rpc 🟢</td><td>4933020</td><td>4001544</td><td>False</td><td>on</td><td>0</td><td>2023-12-06T19:01:13.616445119UTC</td></tr><tr><td>174.138.180.190:61157</td><td>quicksilver-2</td><td>UTSA_guide 🟢</td><td>4933017</td><td>4525955</td><td>False</td><td>on</td><td>0</td><td>2023-12-06T19:01:03.157308764UTC</td></tr><tr><td>142.132.136.106:22657</td><td>quicksilver-2</td><td>SERVICES 🟢</td><td>4932731</td><td>4691001</td><td>False</td><td>on</td><td>0</td><td>2023-12-06T19:01:13.210846341UTC</td></tr><tr><td>65.108.195.29:31127</td><td>quicksilver-2</td><td>Staketab-snap 🟢</td><td>4933015</td><td>4726501</td><td>False</td><td>off</td><td>0</td><td>2023-12-06T19:00:52.183923413UTC</td></tr><tr><td>51.68.170.145:26657</td><td>quicksilver-2</td><td>openbitlab 🟢</td><td>4933013</td><td>4826255</td><td>False</td><td>on</td><td>0</td><td>2023-12-06T19:00:39.542585507UTC</td></tr><tr><td>47.147.226.147:51657</td><td>quicksilver-2</td><td>Node15 🟢</td><td>4933025</td><td>4884752</td><td>False</td><td>off</td><td>0</td><td>2023-12-06T19:01:45.938317647UTC</td></tr><tr><td>46.4.121.72:26657</td><td>quicksilver-2</td><td>nkbblocks 🟢</td><td>4933018</td><td>4900327</td><td>False</td><td>on</td><td>0</td><td>2023-12-06T19:01:09.684540443UTC</td></tr><tr><td>161.97.82.203:26257</td><td>quicksilver-2</td><td>Fort 🟢</td><td>4933007</td><td>4915202</td><td>False</td><td>on</td><td>0</td><td>2023-12-06T19:00:05.696089960UTC</td></tr><tr><td>135.181.210.171:21027</td><td>quicksilver-2</td><td>STAVR-Service 🟢</td><td>4933018</td><td>4931001</td><td>False</td><td>on</td><td>0</td><td>2023-12-06T19:01:10.294394864UTC</td></tr></table>