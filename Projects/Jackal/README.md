<h1 align="center"> 🔥JACKAL🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Jakal)
=

<h1 align="center"> MAINNET</h1>

# StateSync Jackal Mainnet
```python
SNAP_RPC=http://jkl.rpc.m.stavr.tech:11127
peers="ddb821309deba8f274b18ef3ae8731f239569b5c@jkl.rpc.m.stavr.tech:11126"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.canine/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.canine/config/config.toml
canined tendermint unsafe-reset-all --home /root/.canine --keep-addr-book
systemctl restart canined && journalctl -u canined -f -o cat
```
# SnapShot (~1.2GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop canined
cp $HOME/.canine/data/priv_validator_state.json $HOME/.canine/priv_validator_state.json.backup
rm -rf $HOME/.canine/data
curl -o - -L http://jkl.snapshot.stavr.tech:1018/jackal/jackal-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.canine --strip-components 2
mv $HOME/.canine/priv_validator_state.json.backup $HOME/.canine/data/priv_validator_state.json
wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/addrbook.json"
sudo systemctl restart canined && journalctl -u canined -f -o cat
```

<h1 align="center"> TESTNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Jakal/Jackal-Testnet)
=

# StateSync Jackal Testnet
```python
SNAP_RPC=http://jkl.rpc.t.stavr.tech:19127
peers="80613772b20df144945801b42f327d0945a24374@jkltest.peer.stavr.tech:19126"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.canine/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.canine/config/config.toml
canined tendermint unsafe-reset-all --home /root/.canine --keep-addr-book
systemctl restart canined && journalctl -u canined -f -o cat
```
# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop canined
cp $HOME/.canine/data/priv_validator_state.json $HOME/.canine/priv_validator_state.json.backup
rm -rf $HOME/.canine/data
curl -o - -L http://jkltest.snapshot.stavr.tech:1015/jackalt/jackalt-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.canine --strip-components 2
mv $HOME/.canine/priv_validator_state.json.backup $HOME/.canine/data/priv_validator_state.json
wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/Jackal-Testnet/addrbook.json"
sudo systemctl restart canined && journalctl -u canined -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Jackal/staking		        `Indexer "ON"` \
🔥EXPLORER Testnet🔥:      https://explorer.stavr.tech/Jackal-Testnet/staking     `Indexer "ON"` \
🔥API Mainnet🔥: 			 		 https://jkl.api.m.stavr.tech \
🔥API Testnet🔥: 			 		 https://jkl.api.t.stavr.tech \
🔥RPC Mainnet🔥:           http://jkl.rpc.m.stavr.tech:11127              `Snapshot-interval = 300` \
🔥RPC Testnet🔥:           http://jkl.rpc.t.stavr.tech:19127              `Snapshot-interval = 100` \
🔥gRPC Mainnet🔥:          http://jkl.grpc.m.stavr.tech:5013 \
🔥gRPC Testnet🔥:          http://jkl.grpc.t.stavr.tech:5913 \
🔥peer Mainnet🔥:					 `ddb821309deba8f274b18ef3ae8731f239569b5c@jkl.peer.stavr.tech:11126` \
🔥peer Testnet🔥:					 `80613772b20df144945801b42f327d0945a24374@jkltest.peer.stavr.tech:19126` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/Jackal-Testnet/addrbook.json"``` \
🔥Auto_install script Mainnet🔥: ```wget -O jkl https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/jkl && chmod +x jkl && ./jkl``` \
🔥Auto_install script Testnet🔥: ```wget -O jkltest https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/Jackal-Testnet/jkltest && chmod +x jkltest && ./jkltest``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Jackal/Decentralization)🔥


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

[raw json Mainnet](https://rpc-check.jaclalm.stavr.tech/jaclalm/rpc-jaclalm-result.json) \
[raw json Testnet](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Jackal/Rpc-Check-Testnet)
=

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>167.142.158.242:36657</td><td>jackal-1</td><td>jackal-archive 🟢</td><td>6212455</td><td>2770293</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:42:51.008808779UTC</td></tr><tr><td>174.138.180.190:60857</td><td>jackal-1</td><td>UTSA_guide 🟢</td><td>6212428</td><td>5137845</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:40:14.198396486UTC</td></tr><tr><td>208.77.197.83:28657</td><td>jackal-1</td><td>vidulum.app 🟢</td><td>6212454</td><td>5722001</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:42:47.751769167UTC</td></tr><tr><td>94.130.13.187:24657</td><td>jackal-1</td><td>Huginn 🟢</td><td>6095000</td><td>5893001</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:43:11.768975240UTC</td></tr><tr><td>158.69.27.233:18657</td><td>jackal-1</td><td>KYN-RPC 🟢</td><td>6212416</td><td>6080001</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:39:06.869091461UTC</td></tr><tr><td>65.108.141.109:18657</td><td>jackal-1</td><td>node 🟢</td><td>6212414</td><td>6094001</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:38:53.746071978UTC</td></tr><tr><td>65.108.75.107:18657</td><td>jackal-1</td><td>node 🟢</td><td>6212432</td><td>6094001</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:40:37.672634934UTC</td></tr><tr><td>154.12.227.132:26657</td><td>jackal-1</td><td>D-stake 🔴</td><td>6212412</td><td>6098001</td><td>False</td><td>off</td><td>130238</td><td>2024-01-25T13:38:38.709976976UTC</td></tr><tr><td>65.21.90.141:12131</td><td>jackal-1</td><td>SerGo 🔴</td><td>6212417</td><td>6112417</td><td>False</td><td>off</td><td>51095</td><td>2024-01-25T13:39:11.305833609UTC</td></tr><tr><td>95.165.89.222:24474</td><td>jackal-1</td><td>maxfoton 🔴</td><td>6212443</td><td>6112443</td><td>False</td><td>off</td><td>117661</td><td>2024-01-25T13:41:43.524238037UTC</td></tr><tr><td>94.130.137.122:33657</td><td>jackal-1</td><td>Vagif 🔴</td><td>6212454</td><td>6112454</td><td>False</td><td>off</td><td>59998</td><td>2024-01-25T13:42:44.755248559UTC</td></tr><tr><td>37.27.61.49:43657</td><td>jackal-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>6212409</td><td>6142001</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:38:23.858256984UTC</td></tr><tr><td>65.109.118.148:26657</td><td>jackal-1</td><td>BccNodes-Relayer 🟢</td><td>6212437</td><td>6146801</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:41:09.177668679UTC</td></tr><tr><td>5.181.190.157:12857</td><td>jackal-1</td><td>StakeUp-rpc 🟢</td><td>6212037</td><td>6156001</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:38:35.811371570UTC</td></tr><tr><td>65.108.66.174:27657</td><td>jackal-1</td><td>hello-BccNodesRPC 🟢</td><td>6212440</td><td>6161301</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:41:22.150158549UTC</td></tr><tr><td>65.108.44.149:23657</td><td>jackal-1</td><td>ams 🟢</td><td>6212447</td><td>6177421</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:42:04.431727918UTC</td></tr><tr><td>65.108.41.177:26657</td><td>jackal-1</td><td>skynodejs 🔴</td><td>6212455</td><td>6187501</td><td>False</td><td>on</td><td>84602</td><td>2024-01-25T13:42:51.446407184UTC</td></tr><tr><td>65.109.116.57:13757</td><td>jackal-1</td><td>nkbblocks 🟢</td><td>6212460</td><td>6207001</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:43:22.736516505UTC</td></tr><tr><td>65.108.230.113:11127</td><td>jackal-1</td><td>STAVR-Service 🟢</td><td>6212448</td><td>6210701</td><td>False</td><td>on</td><td>0</td><td>2024-01-25T13:42:10.948155508UTC</td></tr></table>
