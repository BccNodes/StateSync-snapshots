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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>136.38.55.33:26657</td><td>froopyland_100-1</td><td>Silk Nodes 🟢</td><td>2094448</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-12T16:13:06.423871197UTC</td></tr><tr><td>51.15.212.195:26657</td><td>froopyland_100-1</td><td>Meria 🟢</td><td>1651535</td><td>1238063</td><td>False</td><td>on</td><td>0</td><td>2024-01-12T16:11:59.971182571UTC</td></tr><tr><td>167.86.127.105:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1651535</td><td>1318001</td><td>False</td><td>off</td><td>0</td><td>2024-01-12T16:13:05.531450601UTC</td></tr><tr><td>74.208.16.201:26647</td><td>froopyland_100-1</td><td>sentinelCumulo 🟢</td><td>2094437</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-12T16:12:03.525437110UTC</td></tr><tr><td>65.108.206.118:60757</td><td>froopyland_100-1</td><td>lesnik_utsa 🔴</td><td>2094440</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:12:19.733253186UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>2094440</td><td>1652923</td><td>False</td><td>off</td><td>303</td><td>2024-01-12T16:12:20.382943739UTC</td></tr><tr><td>135.181.58.28:10357</td><td>froopyland_100-1</td><td>Validatrium.com 🟢</td><td>2079018</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-12T16:12:46.242845660UTC</td></tr><tr><td>136.243.88.91:3241</td><td>froopyland_100-1</td><td>node 🔴</td><td>2094445</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:12:51.307715800UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>2094447</td><td>1652923</td><td>False</td><td>on</td><td>301</td><td>2024-01-12T16:12:59.854732510UTC</td></tr><tr><td>168.119.114.206:26657</td><td>froopyland_100-1</td><td>Crypton 🔴</td><td>2094449</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-12T16:13:11.272067583UTC</td></tr><tr><td>146.19.24.101:26647</td><td>froopyland_100-1</td><td>duality 🔴</td><td>2094443</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:12:38.395416864UTC</td></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>2094447</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:13:00.246293685UTC</td></tr><tr><td>195.14.6.191:26657</td><td>froopyland_100-1</td><td>01node 🔴</td><td>2094449</td><td>1655732</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:13:10.991941255UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>2094437</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:12:03.794962389UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>2094444</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:12:46.585936046UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>2094445</td><td>1656584</td><td>False</td><td>off</td><td>1</td><td>2024-01-12T16:12:51.052318315UTC</td></tr><tr><td>89.117.49.68:26657</td><td>froopyland_100-1</td><td>dymension-test 🔴</td><td>2094449</td><td>1723012</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:13:11.609618063UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>2094439</td><td>1794439</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:12:13.253958850UTC</td></tr><tr><td>192.99.160.197:26657</td><td>froopyland_100-1</td><td>NodeName 🟢</td><td>1829304</td><td>1826584</td><td>False</td><td>on</td><td>0</td><td>2024-01-12T16:13:16.437815327UTC</td></tr><tr><td>95.217.222.4:26657</td><td>froopyland_100-1</td><td>STAVR_guide 🔴</td><td>2094447</td><td>1971362</td><td>False</td><td>off</td><td>1</td><td>2024-01-12T16:13:01.071575600UTC</td></tr><tr><td>194.233.90.134:26657</td><td>froopyland_100-1</td><td>geonodes 🔴</td><td>2094443</td><td>2015001</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:12:39.360553401UTC</td></tr><tr><td>5.161.57.83:26557</td><td>froopyland_100-1</td><td>Provalidator 🔴</td><td>2094436</td><td>2016682</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:12:00.625339339UTC</td></tr><tr><td>89.116.31.118:26657</td><td>froopyland_100-1</td><td>cardex 🟢</td><td>2079018</td><td>2059995</td><td>False</td><td>on</td><td>0</td><td>2024-01-12T16:12:33.115328694UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>2094450</td><td>2060558</td><td>False</td><td>off</td><td>1</td><td>2024-01-12T16:13:16.685426144UTC</td></tr><tr><td>142.132.134.112:23787</td><td>froopyland_100-1</td><td>dymension_rpc 🟢</td><td>2094443</td><td>2076584</td><td>False</td><td>on</td><td>0</td><td>2024-01-12T16:12:37.523614291UTC</td></tr><tr><td>88.99.61.173:36657</td><td>froopyland_100-1</td><td>deNodes 🔴</td><td>2094444</td><td>2077398</td><td>False</td><td>off</td><td>1</td><td>2024-01-12T16:12:45.860768534UTC</td></tr><tr><td>135.181.210.171:17087</td><td>froopyland_100-1</td><td>STAVR-Service 🟢</td><td>2094438</td><td>2081084</td><td>False</td><td>on</td><td>0</td><td>2024-01-12T16:12:08.226262710UTC</td></tr><tr><td>144.91.65.13:26697</td><td>froopyland_100-1</td><td>AviaDoc_by_AviaOne 🟢</td><td>2093235</td><td>2081084</td><td>False</td><td>on</td><td>0</td><td>2024-01-12T16:12:12.831600444UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>2094443</td><td>2082923</td><td>False</td><td>on</td><td>1</td><td>2024-01-12T16:12:37.971817543UTC</td></tr></table>
