<h1 align="center"> 🔥Regen Network🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Regen)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://regen.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.regen/config/config.toml
regen tendermint unsafe-reset-all
wget -O $HOME/.regen/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Regen/addrbook.json"
sudo systemctl restart regen && sudo journalctl -u regen -f -o cat
```
# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop regen
cp $HOME/.regen/data/priv_validator_state.json $HOME/.regen/priv_validator_state.json.backup
rm -rf $HOME/.regen/data
curl -o - -L https://regen.snapshot.stavr.tech/regen/regen-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.regen --strip-components 2
mv $HOME/.regen/priv_validator_state.json.backup $HOME/.regen/data/priv_validator_state.json
wget -O $HOME/.regen/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Regen/addrbook.json"
sudo systemctl restart regen && journalctl -u regen -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Regen-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://regen.api.m.stavr.tech \
🔥RPC🔥:          https://regen.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://regen.grpc.m.stavr.tech:124 \
🔥seed🔥:      `dc7121500d58d40c98f06f14d5a9065935a7adf6@regen.seed.stavr.tech:2126` \
🔥Genesis🔥:   `wget -O $HOME/.regen/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Regen/genesis.json"` \
🔥Addrbook🔥:  `wget -O $HOME/.regen/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Regen/addrbook.json"` \
🔥Auto_install script🔥:`wget -O regenm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Regen/regenm && chmod +x regenm && ./regenm`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Regen/Decentralization)🔥
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

[raw Mainnet json](https://rpc-check.regenm.stavr.tech/regenm/rpc-regenm-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>3.23.48.152:26657</td><td>regen-1</td><td>rndArchive 🟢</td><td>14558978</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:07:20.903977612UTC</td></tr><tr><td>3.22.22.248:26657</td><td>regen-1</td><td>rnd-fullnode 🟢</td><td>14558978</td><td>4134001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:07:18.109953800UTC</td></tr><tr><td>104.236.201.138:26657</td><td>regen-1</td><td>vitwit-seed1 🟢</td><td>14558973</td><td>8943001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:06:50.159705445UTC</td></tr><tr><td>95.217.109.223:6767</td><td>regen-1</td><td>Spanish-rpc 🟢</td><td>14558981</td><td>10068001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:07:37.142904692UTC</td></tr><tr><td>5.9.99.172:22757</td><td>regen-1</td><td>BRAND-regen-relayer 🟢</td><td>14558981</td><td>10782501</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:07:37.643963052UTC</td></tr><tr><td>142.132.132.184:14857</td><td>regen-1</td><td>Validatrium.com-rpc 🟢</td><td>14558981</td><td>11175001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:07:37.399444010UTC</td></tr><tr><td>141.95.104.188:26657</td><td>regen-1</td><td>Stakely.io 🟢</td><td>14558976</td><td>13442501</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:07:09.096523353UTC</td></tr><tr><td>65.109.117.212:13041</td><td>regen-1</td><td>w3coins 🔴</td><td>14558988</td><td>13558988</td><td>False</td><td>off</td><td>23997177814</td><td>2024-02-05T11:08:19.723796273UTC</td></tr><tr><td>161.97.82.203:26657</td><td>regen-1</td><td>alex 🟢</td><td>14558979</td><td>13992001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:07:26.249137847UTC</td></tr><tr><td>57.128.20.238:51657</td><td>regen-1</td><td>rpc 🟢</td><td>14558980</td><td>13992001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:07:30.615066249UTC</td></tr><tr><td>134.209.237.188:26657</td><td>regen-1</td><td>test 🟢</td><td>14558983</td><td>13992001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:07:48.244768895UTC</td></tr><tr><td>135.181.216.151:30657</td><td>regen-1</td><td>fastsync 🟢</td><td>14558979</td><td>14457001</td><td>False</td><td>off</td><td>0</td><td>2024-02-05T11:07:25.934189082UTC</td></tr><tr><td>173.212.213.14:26657</td><td>regen-1</td><td>catBoss 🟢</td><td>14541288</td><td>14478001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:07:21.241321000UTC</td></tr><tr><td>202.65.150.1:1549</td><td>regen-1</td><td>snap 🟢</td><td>14558989</td><td>14552172</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:08:24.657146601UTC</td></tr><tr><td>135.181.210.171:2127</td><td>regen-1</td><td>STAVR-Service 🟢</td><td>14558986</td><td>14558901</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:08:07.126702869UTC</td></tr></table>