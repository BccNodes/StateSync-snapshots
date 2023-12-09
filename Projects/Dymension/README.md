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
🔥Auto_install script🔥: ```wget -O dym https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/dym && chmod +x dym && ./dym```

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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>146.19.24.101:26647</td><td>froopyland_100-1</td><td>duality 🔴</td><td>1614674</td><td>1</td><td>False</td><td>on</td><td>1</td><td>2023-12-08T23:48:03.490541334UTC</td></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>1614677</td><td>1</td><td>False</td><td>on</td><td>1</td><td>2023-12-08T23:48:18.176742073UTC</td></tr><tr><td>168.119.114.206:26657</td><td>froopyland_100-1</td><td>Crypton 🔴</td><td>1614678</td><td>1</td><td>False</td><td>off</td><td>1</td><td>2023-12-08T23:48:24.274950866UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>1614671</td><td>106001</td><td>False</td><td>off</td><td>2</td><td>2023-12-08T23:47:47.843670600UTC</td></tr><tr><td>89.116.31.118:26657</td><td>froopyland_100-1</td><td>cardex 🟢</td><td>1614673</td><td>293001</td><td>False</td><td>on</td><td>0</td><td>2023-12-08T23:47:56.317397754UTC</td></tr><tr><td>78.46.103.246:56657</td><td>froopyland_100-1</td><td>F5Nodes 🔴</td><td>1614670</td><td>407001</td><td>False</td><td>off</td><td>1</td><td>2023-12-08T23:47:41.684291079UTC</td></tr><tr><td>135.181.58.28:10357</td><td>froopyland_100-1</td><td>Validatrium.com 🟢</td><td>1614675</td><td>591001</td><td>False</td><td>on</td><td>0</td><td>2023-12-08T23:48:10.312829068UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>1614675</td><td>737456</td><td>False</td><td>on</td><td>1</td><td>2023-12-08T23:48:10.748324425UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>1614675</td><td>737456</td><td>False</td><td>off</td><td>1</td><td>2023-12-08T23:48:11.067602436UTC</td></tr><tr><td>74.208.16.201:26647</td><td>froopyland_100-1</td><td>sentinelCumulo 🟢</td><td>1614669</td><td>820001</td><td>False</td><td>on</td><td>0</td><td>2023-12-08T23:47:33.663802138UTC</td></tr><tr><td>136.243.88.91:3241</td><td>froopyland_100-1</td><td>node 🔴</td><td>1614675</td><td>922548</td><td>False</td><td>on</td><td>1</td><td>2023-12-08T23:48:11.329255199UTC</td></tr><tr><td>85.239.240.194:33657</td><td>froopyland_100-1</td><td>zardozmonopoly 🟢</td><td>1614679</td><td>935165</td><td>False</td><td>off</td><td>0</td><td>2023-12-08T23:48:31.852739185UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>1614676</td><td>1006001</td><td>False</td><td>on</td><td>1</td><td>2023-12-08T23:48:17.771943925UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>1614678</td><td>1150548</td><td>False</td><td>off</td><td>1</td><td>2023-12-08T23:48:26.937350031UTC</td></tr><tr><td>51.15.212.195:26657</td><td>froopyland_100-1</td><td>Meria 🟢</td><td>1614668</td><td>1238063</td><td>False</td><td>on</td><td>0</td><td>2023-12-08T23:47:30.202992674UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>1614670</td><td>1314670</td><td>False</td><td>on</td><td>1</td><td>2023-12-08T23:47:42.981446270UTC</td></tr><tr><td>142.132.134.112:23787</td><td>froopyland_100-1</td><td>dymension_rpc 🟢</td><td>1614674</td><td>1314674</td><td>False</td><td>on</td><td>0</td><td>2023-12-08T23:48:00.734615242UTC</td></tr><tr><td>167.86.127.105:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1614677</td><td>1318001</td><td>False</td><td>off</td><td>0</td><td>2023-12-08T23:48:21.425543539UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>1614669</td><td>1330001</td><td>False</td><td>on</td><td>1</td><td>2023-12-08T23:47:33.899616716UTC</td></tr><tr><td>194.163.185.53:14657</td><td>froopyland_100-1</td><td>megumii 🟢</td><td>1614670</td><td>1390788</td><td>False</td><td>on</td><td>0</td><td>2023-12-08T23:47:42.565641419UTC</td></tr><tr><td>15.235.160.84:31741</td><td>froopyland_100-1</td><td>node 🟢</td><td>1614669</td><td>1435053</td><td>False</td><td>on</td><td>0</td><td>2023-12-08T23:47:34.885363824UTC</td></tr><tr><td>89.117.49.68:26657</td><td>froopyland_100-1</td><td>dymension-test 🟢</td><td>1614678</td><td>1473622</td><td>False</td><td>on</td><td>0</td><td>2023-12-08T23:48:24.659535353UTC</td></tr><tr><td>88.99.61.173:36657</td><td>froopyland_100-1</td><td>deNodes 🔴</td><td>1614675</td><td>1501386</td><td>False</td><td>off</td><td>1</td><td>2023-12-08T23:48:09.930060119UTC</td></tr><tr><td>5.161.57.83:26557</td><td>froopyland_100-1</td><td>Provalidator 🔴</td><td>1614668</td><td>1503071</td><td>False</td><td>on</td><td>1</td><td>2023-12-08T23:47:30.852304457UTC</td></tr><tr><td>144.91.65.13:26697</td><td>froopyland_100-1</td><td>AviaDoc_by_AviaOne 🟢</td><td>1613483</td><td>1561776</td><td>False</td><td>on</td><td>0</td><td>2023-12-08T23:47:42.109644650UTC</td></tr><tr><td>195.14.6.191:26657</td><td>froopyland_100-1</td><td>01node 🔴</td><td>1614678</td><td>1561776</td><td>False</td><td>on</td><td>1</td><td>2023-12-08T23:48:23.982031235UTC</td></tr><tr><td>38.242.151.229:33657</td><td>froopyland_100-1</td><td>salomonval 🟢</td><td>1614677</td><td>1569001</td><td>False</td><td>off</td><td>0</td><td>2023-12-08T23:48:18.528465226UTC</td></tr><tr><td>37.27.54.228:14657</td><td>froopyland_100-1</td><td>Equinox 🔴</td><td>1614677</td><td>1589489</td><td>False</td><td>on</td><td>1</td><td>2023-12-08T23:48:21.087365313UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>1614674</td><td>1610001</td><td>False</td><td>on</td><td>1</td><td>2023-12-08T23:48:01.109759300UTC</td></tr><tr><td>135.181.210.171:17087</td><td>froopyland_100-1</td><td>STAVR-Service 🟢</td><td>1614670</td><td>1611589</td><td>False</td><td>on</td><td>0</td><td>2023-12-08T23:47:39.412006238UTC</td></tr></table>
