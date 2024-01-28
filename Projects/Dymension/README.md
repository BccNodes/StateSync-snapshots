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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>136.38.55.33:26657</td><td>froopyland_100-1</td><td>Silk Nodes 🟢</td><td>2328452</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T15:22:21.791062315UTC</td></tr><tr><td>51.15.212.195:26657</td><td>froopyland_100-1</td><td>Meria 🟢</td><td>1651535</td><td>1238063</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T15:21:04.934646880UTC</td></tr><tr><td>167.86.127.105:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1651535</td><td>1318001</td><td>False</td><td>off</td><td>0</td><td>2024-01-28T15:22:20.847296523UTC</td></tr><tr><td>74.208.16.201:26647</td><td>froopyland_100-1</td><td>sentinelCumulo 🟢</td><td>2328440</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T15:21:08.841942225UTC</td></tr><tr><td>65.108.206.118:60757</td><td>froopyland_100-1</td><td>lesnik_utsa 🔴</td><td>2328444</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:21:29.129648795UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>2328444</td><td>1652923</td><td>False</td><td>off</td><td>3</td><td>2024-01-28T15:21:29.816567555UTC</td></tr><tr><td>136.243.88.91:3241</td><td>froopyland_100-1</td><td>node 🔴</td><td>2328449</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:22:02.929080123UTC</td></tr><tr><td>46.4.99.152:31741</td><td>froopyland_100-1</td><td>node 🟢</td><td>2328450</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T15:22:05.381750324UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>2328451</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:22:13.885603169UTC</td></tr><tr><td>168.119.114.206:26657</td><td>froopyland_100-1</td><td>Crypton 🔴</td><td>2328454</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-28T15:22:28.830977691UTC</td></tr><tr><td>146.19.24.101:26647</td><td>froopyland_100-1</td><td>duality 🔴</td><td>2328447</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:21:47.896267318UTC</td></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>2328451</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:22:14.304284940UTC</td></tr><tr><td>195.14.6.191:26657</td><td>froopyland_100-1</td><td>01node 🔴</td><td>2328454</td><td>1655732</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:22:28.531941025UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>2328440</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:21:09.108678810UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>2328449</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:21:58.115809656UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>2328449</td><td>1656584</td><td>False</td><td>off</td><td>1</td><td>2024-01-28T15:22:02.636208386UTC</td></tr><tr><td>89.117.49.68:26657</td><td>froopyland_100-1</td><td>dymension-test 🔴</td><td>2328454</td><td>1723012</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:22:29.193468689UTC</td></tr><tr><td>192.99.160.197:26657</td><td>froopyland_100-1</td><td>NodeName 🟢</td><td>1829304</td><td>1826584</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T15:22:34.072179747UTC</td></tr><tr><td>194.233.90.134:26657</td><td>froopyland_100-1</td><td>geonodes 🔴</td><td>2328447</td><td>2015001</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:21:48.839400425UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>2328442</td><td>2028442</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:21:20.550794443UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>2328455</td><td>2060558</td><td>False</td><td>off</td><td>1</td><td>2024-01-28T15:22:34.368563463UTC</td></tr><tr><td>142.132.134.112:23787</td><td>froopyland_100-1</td><td>dymension_rpc 🟢</td><td>2328447</td><td>2076584</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T15:21:47.071059683UTC</td></tr><tr><td>88.99.61.173:36657</td><td>froopyland_100-1</td><td>deNodes 🔴</td><td>2328448</td><td>2077398</td><td>False</td><td>off</td><td>1</td><td>2024-01-28T15:21:55.345355757UTC</td></tr><tr><td>167.235.9.223:61557</td><td>froopyland_100-1</td><td>F5Nodes 🔴</td><td>2328445</td><td>2100380</td><td>False</td><td>off</td><td>1</td><td>2024-01-28T15:21:36.228602200UTC</td></tr><tr><td>152.53.16.17:14657</td><td>froopyland_100-1</td><td>Equinox 🔴</td><td>2328440</td><td>2169800</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:21:08.027529122UTC</td></tr><tr><td>135.181.210.171:17087</td><td>froopyland_100-1</td><td>STAVR-Service 🟢</td><td>2328441</td><td>2225118</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T15:21:13.583718959UTC</td></tr><tr><td>5.161.57.83:26557</td><td>froopyland_100-1</td><td>Provalidator 🔴</td><td>2328439</td><td>2266474</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:21:05.553334709UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>2328447</td><td>2312923</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T15:21:47.524879956UTC</td></tr><tr><td>144.91.65.13:26697</td><td>froopyland_100-1</td><td>AviaDoc_by_AviaOne 🟢</td><td>2328431</td><td>2315718</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T15:21:20.188233219UTC</td></tr></table>
