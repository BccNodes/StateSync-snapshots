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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>1651536</td><td>1</td><td>False</td><td>on</td><td>106989</td><td>2023-12-12T04:42:35.841383164UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>1651536</td><td>737456</td><td>False</td><td>off</td><td>104379</td><td>2023-12-12T04:42:33.125012645UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>1651536</td><td>1330001</td><td>False</td><td>on</td><td>110752</td><td>2023-12-12T04:42:12.466537626UTC</td></tr><tr><td>142.132.134.112:23787</td><td>froopyland_100-1</td><td>dymension_rpc 🟢</td><td>1651536</td><td>1351534</td><td>False</td><td>on</td><td>0</td><td>2023-12-12T04:42:27.730717406UTC</td></tr><tr><td>15.235.160.84:31741</td><td>froopyland_100-1</td><td>node 🟢</td><td>1651535</td><td>1435053</td><td>False</td><td>on</td><td>0</td><td>2023-12-12T04:42:13.416219951UTC</td></tr><tr><td>20.122.112.2:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1636516</td><td>1479282</td><td>False</td><td>on</td><td>0</td><td>2023-12-12T04:42:16.211349216UTC</td></tr><tr><td>88.99.61.173:36657</td><td>froopyland_100-1</td><td>deNodes 🔴</td><td>1651536</td><td>1501386</td><td>False</td><td>off</td><td>102042</td><td>2023-12-12T04:42:32.419264117UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>1651535</td><td>1649923</td><td>False</td><td>on</td><td>1</td><td>2023-12-12T04:42:16.536492543UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>1651535</td><td>1649923</td><td>False</td><td>on</td><td>1</td><td>2023-12-12T04:42:28.055482473UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>1651535</td><td>1649923</td><td>False</td><td>on</td><td>1</td><td>2023-12-12T04:42:35.518239982UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>1651535</td><td>1649923</td><td>False</td><td>off</td><td>1</td><td>2023-12-12T04:42:43.340898267UTC</td></tr><tr><td>5.161.57.83:26557</td><td>froopyland_100-1</td><td>Provalidator 🔴</td><td>1651535</td><td>1650923</td><td>False</td><td>on</td><td>1</td><td>2023-12-12T04:42:10.129368904UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>1651535</td><td>1650923</td><td>False</td><td>off</td><td>2</td><td>2023-12-12T04:42:21.246105958UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>1651535</td><td>1650923</td><td>False</td><td>on</td><td>1</td><td>2023-12-12T04:42:32.735207370UTC</td></tr><tr><td>37.27.54.228:14657</td><td>froopyland_100-1</td><td>Equinox 🔴</td><td>1651535</td><td>1650923</td><td>False</td><td>on</td><td>1</td><td>2023-12-12T04:42:36.207340302UTC</td></tr></table>
