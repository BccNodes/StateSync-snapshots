<h1 align="center"> 🔥OKP4🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/OKP4)
=

# StateSync
```python
SNAP_RPC=http://okp.rpc.t.stavr.tech:10097
peers="3301c449cf9706c35a0fafb7b97d20e40cdb96df@okp.peer.stavr.tech:10096"
sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.okp4d/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.okp4d/config/config.toml
okp4d tendermint unsafe-reset-all --home /root/.okp4d --keep-addr-book
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.okp4d/config/app.toml
systemctl restart okp4d && journalctl -u okp4d -f -o cat

```
# SnapShot (~0.4 GB) updated every 5 hours
```python
cd $HOME
snap install lz4
sudo systemctl stop okp4d
cp $HOME/.okp4d/data/priv_validator_state.json $HOME/.okp4d/priv_validator_state.json.backup
rm -rf $HOME/.okp4d/data
curl -o - -L http://okp.snapshot.stavr.tech:1011/okp/okp-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.okp4d --strip-components 2
mv $HOME/.okp4d/priv_validator_state.json.backup $HOME/.okp4d/data/priv_validator_state.json
wget -O $HOME/.okp4d/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/OKP4/addrbook.json"
sudo systemctl restart okp4d && journalctl -u okp4d -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:          https://explorer.stavr.tech/OKP4-Testnet/staking        Indexer "ON" \
🔥API🔥:                       https://okp4.api.t.stavr.tech \
🔥RPC🔥:                      http://okp.rpc.t.stavr.tech:10097                  Snapshot-interval = 300 \
🔥gRPC🔥:                    http://okp.grpc.t.stavr.tech:8029 \
🔥peer🔥:                     `3301c449cf9706c35a0fafb7b97d20e40cdb96df@okp.peer.stavr.tech:10096` \
🔥Addrbook🔥:    ```wget -O $HOME/.okp4d/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/OKP4/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O okp https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/OKP4/okp && chmod +x okp && ./okp```

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

[raw json Testnet](https://rpc-check.okpt.stavr.tech/okpt/rpc-okpt-result.json)
=




<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.21.170.3:42657</td><td>okp4-nemeton-1</td><td>Munris 🔴</td><td>5338390</td><td>1</td><td>False</td><td>452544</td><td>2023-12-03T01:33:22.416750457UTC</td></tr><tr><td>136.243.88.91:6041</td><td>okp4-nemeton-1</td><td>Enigma 🔴</td><td>5338390</td><td>1123444</td><td>False</td><td>10001</td><td>2023-12-03T01:33:25.029714162UTC</td></tr><tr><td>38.242.251.204:36657</td><td>okp4-nemeton-1</td><td>Lexar 🔴</td><td>5338382</td><td>3052301</td><td>False</td><td>71497</td><td>2023-12-03T01:32:37.271199123UTC</td></tr><tr><td>161.97.77.219:36657</td><td>okp4-nemeton-1</td><td>Apollo 🔴</td><td>5338390</td><td>3888601</td><td>False</td><td>41580</td><td>2023-12-03T01:33:22.739254066UTC</td></tr><tr><td>65.21.187.101:26657</td><td>okp4-nemeton-1</td><td>SmartHamster 🔴</td><td>5338383</td><td>3902606</td><td>False</td><td>370484</td><td>2023-12-03T01:32:42.405933143UTC</td></tr><tr><td>15.235.53.45:2031</td><td>okp4-nemeton-1</td><td>Zenscape 🔴</td><td>5338390</td><td>5086501</td><td>False</td><td>49653</td><td>2023-12-03T01:33:25.724496635UTC</td></tr><tr><td>213.239.207.175:38657</td><td>okp4-nemeton-1</td><td>landeros 🔴</td><td>5338389</td><td>5148001</td><td>False</td><td>139157</td><td>2023-12-03T01:33:21.654436797UTC</td></tr><tr><td>51.158.73.82:26657</td><td>okp4-nemeton-1</td><td>Meria 🔴</td><td>5338384</td><td>5160205</td><td>False</td><td>9606</td><td>2023-12-03T01:32:53.523840361UTC</td></tr><tr><td>167.235.21.165:46657</td><td>okp4-nemeton-1</td><td>HSS 🔴</td><td>5338381</td><td>5171001</td><td>False</td><td>23999</td><td>2023-12-03T01:32:34.776601929UTC</td></tr><tr><td>178.18.254.211:10657</td><td>okp4-nemeton-1</td><td>CosmoBook 🔴</td><td>5338389</td><td>5172801</td><td>False</td><td>269233</td><td>2023-12-03T01:33:19.098953280UTC</td></tr><tr><td>65.108.134.215:26657</td><td>okp4-nemeton-1</td><td>moodman 🔴</td><td>5338382</td><td>5238382</td><td>False</td><td>452624</td><td>2023-12-03T01:32:39.643302558UTC</td></tr><tr><td>65.21.90.141:12231</td><td>okp4-nemeton-1</td><td>SerGo 🔴</td><td>5338384</td><td>5238384</td><td>False</td><td>85482</td><td>2023-12-03T01:32:53.146261998UTC</td></tr><tr><td>65.108.131.190:23457</td><td>okp4-nemeton-1</td><td>okp4 🔴</td><td>5338386</td><td>5238386</td><td>False</td><td>452475</td><td>2023-12-03T01:33:02.053816558UTC</td></tr><tr><td>142.132.202.50:11111</td><td>okp4-nemeton-1</td><td>cryptobtcbuyer 🔴</td><td>5338386</td><td>5238386</td><td>False</td><td>134927</td><td>2023-12-03T01:33:04.381533626UTC</td></tr><tr><td>94.130.137.122:29657</td><td>okp4-nemeton-1</td><td>Vagif 🔴</td><td>5338389</td><td>5238389</td><td>False</td><td>339037</td><td>2023-12-03T01:33:21.375471632UTC</td></tr><tr><td>65.109.117.212:13091</td><td>okp4-nemeton-1</td><td>w3coins 🔴</td><td>5338390</td><td>5238390</td><td>False</td><td>20000</td><td>2023-12-03T01:33:26.068632505UTC</td></tr><tr><td>135.181.210.171:10097</td><td>okp4-nemeton-1</td><td>STAVR-Service 🟢</td><td>5338382</td><td>5336401</td><td>False</td><td>0</td><td>2023-12-03T01:32:40.035444470UTC</td></tr></table>