<h1 align="center"> 🔥Decentr🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Decentr)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://decentr.rpc.m.stavr.tech:443
SEEDS=1f5497f2b4f6adb3b803c17c3b005f637fcaec2d@decentr.peer.stavr.tech:1066
cp $HOME/.decentr/data/priv_validator_state.json $HOME/.decentr/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.decentr/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.decentr/config/config.toml
decentrd tendermint unsafe-reset-all --home $HOME/.decentr --keep-addr-book
mv $HOME/.decentr/priv_validator_state.json.backup $HOME/.decentr/data/priv_validator_state.json
sudo systemctl restart decentrd && journalctl -u decentrd -f -o cat
```
# SnapShot (~0.3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop decentrd
cp $HOME/.decentr/data/priv_validator_state.json $HOME/.decentr/priv_validator_state.json.backup
rm -rf $HOME/.decentr/data
curl -o - -L http://decentr.snapshot.stavr.tech:9/decentr/decentr-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.decentr --strip-components 2
mv $HOME/.decentr/priv_validator_state.json.backup $HOME/.decentr/data/priv_validator_state.json
wget -O $HOME/.decentr/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Decentr/addrbook.json"
sudo systemctl restart decentrd && journalctl -u decentrd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Decentr-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://decentr.api.m.stavr.tech \
🔥RPC🔥:          https://decentr.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://decentr.grpc.m.stavr.tech:2060 \
🔥peer🔥:         `1f5497f2b4f6adb3b803c17c3b005f637fcaec2d@decentr.peer.stavr.tech:1066` \
🔥Addrbook🔥:  `wget -O $HOME/.decentr/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Decentr/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.decentr/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Decentr/genesis.json"` \
🔥Auto_install script🔥:`wget -O decentrm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Decentr/decentrm && chmod +x decentrm && ./decentrm`

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

[raw Mainnet json](https://rpc-check.decentrm.stavr.tech/decentrm/rpc-decentrm-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>162.55.160.1:26657</td><td>mainnet-3</td><td>melpomene 🟢</td><td>12751340</td><td>1688950</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:32:19.061330553UTC</td></tr><tr><td>135.181.149.127:26657</td><td>mainnet-3</td><td>calliope 🟢</td><td>12751341</td><td>1688950</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:32:21.568271452UTC</td></tr><tr><td>167.235.20.88:26657</td><td>mainnet-3</td><td>thalia 🟢</td><td>12751342</td><td>1688950</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:32:27.421220460UTC</td></tr><tr><td>65.108.77.98:26687</td><td>mainnet-3</td><td>StakeLab 🔴</td><td>12751342</td><td>1688950</td><td>False</td><td>on</td><td>5658381</td><td>2024-02-05T11:32:27.778546048UTC</td></tr><tr><td>135.181.149.160:26657</td><td>mainnet-3</td><td>poseidon 🟢</td><td>12751343</td><td>1688950</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:32:32.578010564UTC</td></tr><tr><td>162.55.40.104:26657</td><td>mainnet-3</td><td>hera 🟢</td><td>12751343</td><td>1688950</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:32:34.933471692UTC</td></tr><tr><td>95.217.209.39:26657</td><td>mainnet-3</td><td>terpsichore 🟢</td><td>12751344</td><td>1688950</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:32:41.521696918UTC</td></tr><tr><td>167.235.25.46:26657</td><td>mainnet-3</td><td>ares 🟢</td><td>12751345</td><td>1688950</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:32:43.805432889UTC</td></tr><tr><td>167.235.18.78:26657</td><td>mainnet-3</td><td>zeus 🟢</td><td>12751345</td><td>1688950</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:32:46.107395444UTC</td></tr><tr><td>167.235.25.45:26657</td><td>mainnet-3</td><td>euterpe 🟢</td><td>12751345</td><td>1688950</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:32:46.343958864UTC</td></tr><tr><td>159.69.189.120:26657</td><td>mainnet-3</td><td>hermes 🟢</td><td>12751345</td><td>1688950</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:32:48.623494000UTC</td></tr><tr><td>95.168.173.33:12657</td><td>mainnet-3</td><td>%{name}% 🔴</td><td>12751341</td><td>8964001</td><td>False</td><td>on</td><td>4263175</td><td>2024-02-05T11:32:22.764618703UTC</td></tr><tr><td>167.235.9.223:60757</td><td>mainnet-3</td><td>F5Nodes 🔴</td><td>12751341</td><td>12380001</td><td>False</td><td>off</td><td>562</td><td>2024-02-05T11:32:23.076981241UTC</td></tr><tr><td>66.45.246.166:1067</td><td>mainnet-3</td><td>STAVR-Service 🟢</td><td>12751341</td><td>12748001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:32:22.202483623UTC</td></tr></table>
