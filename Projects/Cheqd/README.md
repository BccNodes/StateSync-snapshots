<h1 align="center"> 🔥CHEQD🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Cheqd)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=http://cheqd.rpc.m.stavr.tech:26337
SEEDS=46bb1e68fcc2750ecdc4253986d653f4bd7228ef@cheqd.peer.stavr.tech:21016
cp $HOME/.cheqdnode/data/priv_validator_state.json $HOME/.cheqdnode/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.cheqdnode/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.cheqdnode/config/config.toml
cheqd-noded tendermint unsafe-reset-all --home $HOME/.cheqdnode --keep-addr-book
mv $HOME/.cheqdnode/priv_validator_state.json.backup $HOME/.cheqdnode/data/priv_validator_state.json
sudo systemctl restart cheqd-noded && journalctl -u cheqd-noded -f -o cat
```
# SnapShot (~3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop cheqd-noded
cp $HOME/.cheqdnode/data/priv_validator_state.json $HOME/.cheqdnode/priv_validator_state.json.backup
rm -rf $HOME/.cheqdnode/data
curl -o - -L http://cheqd.snapshot.stavr.tech:4/cheqd/cheqd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.cheqdnode --strip-components 2
mv $HOME/.cheqdnode/priv_validator_state.json.backup $HOME/.cheqdnode/data/priv_validator_state.json
wget -O $HOME/.cheqdnode/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/addrbook.json"
sudo systemctl restart cheqd-noded && journalctl -u cheqd-noded -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Cheqd-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://cheqd.api.m.stavr.tech \
🔥RPC🔥:          http://cheqd.rpc.m.stavr.tech:26337              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://cheqd.grpc.m.stavr.tech:9337 \
🔥peer🔥:         `46bb1e68fcc2750ecdc4253986d653f4bd7228ef@cheqd.peer.stavr.tech:21016` \
🔥Addrbook🔥:  `wget -O $HOME/.cheqdnode/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.cheqdnode/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/genesis.json"` \
🔥Auto_install script🔥:`wget -O cheqdm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/cheqdm && chmod +x cheqdm && ./cheqdm`

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

[raw Mainnet json](https://rpc-check.cheqdm.stavr.tech/cheqdm/rpc-cheqdm-result.json)
=




<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>78.46.83.78:26657</td><td>cheqd-mainnet-1</td><td>cstp-cheqd 🔴</td><td>10991802</td><td>1</td><td>False</td><td>on</td><td>2347496334</td><td>2023-12-07T17:12:18.027098725UTC</td></tr><tr><td>13.59.81.97:26657</td><td>cheqd-mainnet-1</td><td>ydp1-chqd 🔴</td><td>10991804</td><td>1</td><td>False</td><td>on</td><td>35201252815</td><td>2023-12-07T17:12:30.104486595UTC</td></tr><tr><td>167.235.133.235:26657</td><td>cheqd-mainnet-1</td><td>danubetech-v2 🔴</td><td>10991807</td><td>1</td><td>False</td><td>on</td><td>10292099545</td><td>2023-12-07T17:12:44.203402897UTC</td></tr><tr><td>158.220.102.32:26657</td><td>cheqd-mainnet-1</td><td>vmi1259816.contaboserver.net 🟢</td><td>10991815</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2023-12-07T17:13:30.163140842UTC</td></tr><tr><td>75.119.159.96:26657</td><td>cheqd-mainnet-1</td><td>vaipoa.node 🔴</td><td>10991815</td><td>1</td><td>False</td><td>on</td><td>22467243837</td><td>2023-12-07T17:13:30.502282169UTC</td></tr><tr><td>208.77.197.82:33657</td><td>cheqd-mainnet-1</td><td>vidulum.app 🟢</td><td>10991814</td><td>8384004</td><td>False</td><td>on</td><td>0</td><td>2023-12-07T17:13:25.698445614UTC</td></tr><tr><td>135.181.6.249:26657</td><td>cheqd-mainnet-1</td><td>verio-id 🟢</td><td>9196500</td><td>8896499</td><td>False</td><td>on</td><td>0</td><td>2023-12-07T17:12:18.375457502UTC</td></tr><tr><td>65.21.20.218:26657</td><td>cheqd-mainnet-1</td><td>Blockval_Node 🟢</td><td>10991808</td><td>9634953</td><td>False</td><td>on</td><td>0</td><td>2023-12-07T17:12:53.826114865UTC</td></tr><tr><td>149.102.137.113:26657</td><td>cheqd-mainnet-1</td><td>node101 🔴</td><td>10991811</td><td>10276869</td><td>False</td><td>on</td><td>7229458600</td><td>2023-12-07T17:13:09.652155707UTC</td></tr><tr><td>80.39.181.74:30657</td><td>cheqd-mainnet-1</td><td>Validavia 🔴</td><td>10991807</td><td>10423019</td><td>False</td><td>on</td><td>2286466185</td><td>2023-12-07T17:12:46.786165220UTC</td></tr><tr><td>142.132.248.253:22257</td><td>cheqd-mainnet-1</td><td>Blackhox 🔴</td><td>10991813</td><td>10538869</td><td>False</td><td>on</td><td>2226330412</td><td>2023-12-07T17:13:18.719840497UTC</td></tr><tr><td>206.189.247.12:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>10991804</td><td>10741804</td><td>False</td><td>on</td><td>40519770383</td><td>2023-12-07T17:12:26.973040181UTC</td></tr><tr><td>13.245.249.96:26657</td><td>cheqd-mainnet-1</td><td>DIDx 🔴</td><td>10991806</td><td>10741806</td><td>False</td><td>on</td><td>3651151550</td><td>2023-12-07T17:12:39.356359102UTC</td></tr><tr><td>134.209.190.126:26657</td><td>cheqd-mainnet-1</td><td>seerbytes 🔴</td><td>10991807</td><td>10741807</td><td>False</td><td>on</td><td>223928156</td><td>2023-12-07T17:12:43.879532917UTC</td></tr><tr><td>51.145.165.17:26657</td><td>cheqd-mainnet-1</td><td>DIDLab 🔴</td><td>10991808</td><td>10741808</td><td>False</td><td>on</td><td>19108866787</td><td>2023-12-07T17:12:51.193032359UTC</td></tr><tr><td>159.69.174.238:26657</td><td>cheqd-mainnet-1</td><td>node0-monokee 🔴</td><td>10991808</td><td>10741808</td><td>False</td><td>on</td><td>14718172998</td><td>2023-12-07T17:12:53.511635617UTC</td></tr><tr><td>143.110.218.56:26657</td><td>cheqd-mainnet-1</td><td>continuumloop-mn 🔴</td><td>10991809</td><td>10741809</td><td>False</td><td>on</td><td>6659934298</td><td>2023-12-07T17:12:54.687712993UTC</td></tr><tr><td>206.189.25.194:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>10991811</td><td>10741811</td><td>False</td><td>on</td><td>40519770383</td><td>2023-12-07T17:13:07.309748910UTC</td></tr><tr><td>66.45.246.166:26337</td><td>cheqd-mainnet-1</td><td>Paradigm 🔴</td><td>10991812</td><td>10979869</td><td>False</td><td>on</td><td>1</td><td>2023-12-07T17:13:12.274915116UTC</td></tr><tr><td>135.181.210.171:26337</td><td>cheqd-mainnet-1</td><td>STAVR-Service 🟢</td><td>10991804</td><td>10986869</td><td>False</td><td>off</td><td>0</td><td>2023-12-07T17:12:27.386650578UTC</td></tr></table>