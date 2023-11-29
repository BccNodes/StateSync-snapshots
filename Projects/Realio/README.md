<h1 align="center"> 🔥Realio🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Realio)
=

<h1 align="center"> MAINNET</h1>

# StateSync Realio Mainnet
```python
SNAP_RPC=http://realio.rpc.m.stavr.tech:21097
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.realio-network/config/config.toml
realio-networkd tendermint unsafe-reset-all --home /root/.realio-network
wget -O $HOME/.realio-network/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/addrbook.json"
sudo systemctl restart realio-networkd && journalctl -u realio-networkd -f -o cat
```
# SnapShot (~0.1 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop realio-networkd
cp $HOME/.realio-network/data/priv_validator_state.json $HOME/.realio-network/priv_validator_state.json.backup
rm -rf $HOME/.realio-network/data
curl -o - -L http://realio.snapshot.stavr.tech:1029/realio/realio-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.realio-network --strip-components 2
mv $HOME/.realio-network/priv_validator_state.json.backup $HOME/.realio-network/data/priv_validator_state.json
wget -O $HOME/.realio-network/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/addrbook.json"
sudo systemctl restart realio-networkd && journalctl -u realio-networkd -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:       https://explorer.stavr.tech/Realio-Mainnet  `Indexer "ON"` \
🔥EXPLORER Testnet🔥:         https://explorer.stavr.tech/Realio             `Indexer "ON"` \
🔥API Mainnet🔥:                    https://realio.api.m.stavr.tech \
🔥API Testnet🔥:                      https://realio.api.t.stavr.tech \
🔥RPC Mainnet🔥:                   http://realio.rpc.m.stavr.tech:21097              `Snapshot-interval = 100` \
🔥gRPC Mainnet🔥:                 http://realio.grpc.m.stavr.tech:9062 \
🔥peer Mainnet🔥:                   `0f1a87ee4400c0b6332343775a4ff659bc3daf29@realio.peers.stavr.tech:21096` \
🔥Genesis Mainnet🔥:     ```wget -O $HOME/.realio-network/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/genesis.json"``` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.realio-network/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.realio-network/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/Testnet/addrbook.json"```
:tools: **Auto_install script Mainnet(StateSync/SnapShot included):** ```wget -O realio https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/realio && chmod +x realio && ./realio```s

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

[raw json Mainnet](https://rpc-check.realiom.stavr.tech/realiom/rpc-realiom-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>135.181.114.86:25557</td><td>realionetwork_3301-1</td><td>NodeName 🔴</td><td>3938592</td><td>3529801</td><td>False</td><td>304745</td><td>2023-11-29T06:00:29.288904169UTC</td></tr><tr><td>65.109.28.177:30657</td><td>realionetwork_3301-1</td><td>AlxVoy 🔴</td><td>3938594</td><td>3560001</td><td>False</td><td>121223</td><td>2023-11-29T06:00:38.987790565UTC</td></tr><tr><td>46.17.250.108:56657</td><td>realionetwork_3301-1</td><td>Sr20de 🔴</td><td>3938593</td><td>3568001</td><td>False</td><td>84956</td><td>2023-11-29T06:00:33.355922189UTC</td></tr><tr><td>5.9.61.78:11657</td><td>realionetwork_3301-1</td><td>Kynraze 🔴</td><td>3938592</td><td>3717201</td><td>False</td><td>552817</td><td>2023-11-29T06:00:28.938780256UTC</td></tr><tr><td>65.109.29.224:28657</td><td>realionetwork_3301-1</td><td>Munris 🟢</td><td>3938592</td><td>3838592</td><td>False</td><td>0</td><td>2023-11-29T06:00:32.040737356UTC</td></tr><tr><td>65.21.90.141:12261</td><td>realionetwork_3301-1</td><td>SerGo 🔴</td><td>3938592</td><td>3838592</td><td>False</td><td>34999</td><td>2023-11-29T06:00:32.365591998UTC</td></tr><tr><td>173.249.59.70:32657</td><td>realionetwork_3301-1</td><td>moodman 🔴</td><td>3938593</td><td>3838593</td><td>False</td><td>111935</td><td>2023-11-29T06:00:36.613615654UTC</td></tr><tr><td>142.132.202.50:39657</td><td>realionetwork_3301-1</td><td>rpc 🔴</td><td>3938593</td><td>3873501</td><td>False</td><td>1706448</td><td>2023-11-29T06:00:33.951738806UTC</td></tr><tr><td>65.108.66.174:45657</td><td>realionetwork_3301-1</td><td>hello-BccNodesRPC 🟢</td><td>3938593</td><td>3883201</td><td>False</td><td>0</td><td>2023-11-29T06:00:36.334514389UTC</td></tr><tr><td>185.248.24.51:15257</td><td>realionetwork_3301-1</td><td>Moonbridge 🟢</td><td>3938592</td><td>3922801</td><td>False</td><td>0</td><td>2023-11-29T06:00:29.657777489UTC</td></tr><tr><td>192.99.160.197:10657</td><td>realionetwork_3301-1</td><td>BACKUP 🟢</td><td>3938560</td><td>3934401</td><td>False</td><td>0</td><td>2023-11-29T06:00:32.968633067UTC</td></tr><tr><td>135.181.210.171:21097</td><td>realionetwork_3301-1</td><td>STAVR-Service 🟢</td><td>3938593</td><td>3936901</td><td>False</td><td>0</td><td>2023-11-29T06:00:33.705290081UTC</td></tr></table>
