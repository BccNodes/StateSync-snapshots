<h1 align="center"> 🔥Dymension🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Dymension)
=

<h1 align="center"> TESTNET</h1>

# StateSync Dymension Testnet
```python
SNAP_RPC=https://dym.rpc.t.stavr.tech:443
peers="263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.dymension/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.dymension/config/config.toml
dymd tendermint unsafe-reset-all --home /root/.dymension
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
systemctl restart dymd && journalctl -u dymd -f -o cat

```
# SnapShot (~3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop dymd
cp $HOME/.dymension/data/priv_validator_state.json $HOME/.dymension/priv_validator_state.json.backup
rm -rf $HOME/.dymension/data
curl -o - -L http://dymension.snapshot.stavr.tech:1019/dymension/dymension-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dymension --strip-components 2
mv $HOME/.dymension/priv_validator_state.json.backup $HOME/.dymension/data/priv_validator_state.json
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
sudo systemctl restart dymd && journalctl -u dymd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Dymension-testnet/staking        `Indexer "ON"` \
🔥API🔥:          https://dymension.api.t.stavr.tech \
🔥RPC🔥:          https://dym.rpc.t.stavr.tech:443                  `Snapshot-interval = 100` \
🔥gRPC🔥:         http://dymension.grpc.t.stavr.tech:7119 \
🔥peer🔥:         `263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086` \
🔥Genesis🔥:     ```wget https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/genesis.json -O $HOME/.dymension/config/genesis.json``` \
🔥Addrbook🔥:    ```wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O dym https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/dym && chmod +x dym && ./dym``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Dymension/Decentralization)🔥


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

[raw json](https://rpc-check.dymt.stavr.tech/dymt/rpc-dymt-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>136.38.55.33:26657</td><td>froopyland_100-1</td><td>Silk Nodes 🟢</td><td>1967666</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-04T00:42:28.792932258UTC</td></tr><tr><td>51.15.212.195:26657</td><td>froopyland_100-1</td><td>Meria 🟢</td><td>1651535</td><td>1238063</td><td>False</td><td>on</td><td>0</td><td>2024-01-04T00:41:29.745933015UTC</td></tr><tr><td>167.86.127.105:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1651535</td><td>1318001</td><td>False</td><td>off</td><td>0</td><td>2024-01-04T00:42:27.661623062UTC</td></tr><tr><td>74.208.16.201:26647</td><td>froopyland_100-1</td><td>sentinelCumulo 🟢</td><td>1967656</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-04T00:41:31.334686756UTC</td></tr><tr><td>15.235.160.84:31741</td><td>froopyland_100-1</td><td>node 🟢</td><td>1967656</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-04T00:41:33.349308298UTC</td></tr><tr><td>65.108.206.118:60757</td><td>froopyland_100-1</td><td>lesnik_utsa 🔴</td><td>1967659</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-04T00:41:46.962937283UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>1967659</td><td>1652923</td><td>False</td><td>off</td><td>2</td><td>2024-01-04T00:41:47.717890574UTC</td></tr><tr><td>88.99.61.173:36657</td><td>froopyland_100-1</td><td>deNodes 🔴</td><td>1967663</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-04T00:42:11.794284743UTC</td></tr><tr><td>135.181.58.28:10357</td><td>froopyland_100-1</td><td>Validatrium.com 🟢</td><td>1967663</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-04T00:42:12.258472128UTC</td></tr><tr><td>136.243.88.91:3241</td><td>froopyland_100-1</td><td>node 🔴</td><td>1967664</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-04T00:42:17.591511616UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>1967665</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-04T00:42:24.107452128UTC</td></tr><tr><td>168.119.114.206:26657</td><td>froopyland_100-1</td><td>Crypton 🔴</td><td>1967666</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-04T00:42:31.786810777UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>1967667</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-04T00:42:37.333166823UTC</td></tr><tr><td>146.19.24.101:26647</td><td>froopyland_100-1</td><td>duality 🔴</td><td>1967662</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-04T00:42:05.273062962UTC</td></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>1967665</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-04T00:42:24.557661409UTC</td></tr><tr><td>195.14.6.191:26657</td><td>froopyland_100-1</td><td>01node 🔴</td><td>1967666</td><td>1655732</td><td>False</td><td>on</td><td>1</td><td>2024-01-04T00:42:31.419887844UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>1967656</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-04T00:41:31.695814685UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>1967663</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-04T00:42:12.726041333UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>1967664</td><td>1656584</td><td>False</td><td>off</td><td>1</td><td>2024-01-04T00:42:17.253687484UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>1967658</td><td>1667658</td><td>False</td><td>on</td><td>1</td><td>2024-01-04T00:41:42.444984253UTC</td></tr><tr><td>142.132.134.112:23787</td><td>froopyland_100-1</td><td>dymension_rpc 🟢</td><td>1967661</td><td>1667661</td><td>False</td><td>on</td><td>0</td><td>2024-01-04T00:42:02.346813893UTC</td></tr><tr><td>89.117.49.68:26657</td><td>froopyland_100-1</td><td>dymension-test 🟢</td><td>1967667</td><td>1723012</td><td>False</td><td>on</td><td>0</td><td>2024-01-04T00:42:32.242734060UTC</td></tr><tr><td>38.242.151.229:33657</td><td>froopyland_100-1</td><td>salomonval 🟢</td><td>1967665</td><td>1773995</td><td>False</td><td>off</td><td>0</td><td>2024-01-04T00:42:25.153150005UTC</td></tr><tr><td>192.99.160.197:26657</td><td>froopyland_100-1</td><td>NodeName 🟢</td><td>1829304</td><td>1826584</td><td>False</td><td>on</td><td>0</td><td>2024-01-04T00:42:36.988548614UTC</td></tr><tr><td>135.181.210.171:17087</td><td>froopyland_100-1</td><td>STAVR-Service 🟢</td><td>1967657</td><td>1905398</td><td>False</td><td>on</td><td>0</td><td>2024-01-04T00:41:37.938981987UTC</td></tr><tr><td>66.45.236.14:46657</td><td>froopyland_100-1</td><td>Galaxynode 🟢</td><td>1967656</td><td>1938874</td><td>False</td><td>on</td><td>0</td><td>2024-01-04T00:41:32.353957823UTC</td></tr><tr><td>5.161.57.83:26557</td><td>froopyland_100-1</td><td>Provalidator 🔴</td><td>1967656</td><td>1943652</td><td>False</td><td>on</td><td>1</td><td>2024-01-04T00:41:30.467321394UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>1967661</td><td>1962923</td><td>False</td><td>on</td><td>1</td><td>2024-01-04T00:42:02.824223284UTC</td></tr></table>
