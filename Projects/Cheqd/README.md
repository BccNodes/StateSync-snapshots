<h1 align="center"> 🔥CHEQD🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Cheqd)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://cheqd.rpc.m.stavr.tech:443
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
🔥RPC🔥:          https://cheqd.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://cheqd.grpc.m.stavr.tech:9337 \
🔥peer🔥:         `46bb1e68fcc2750ecdc4253986d653f4bd7228ef@cheqd.peer.stavr.tech:21016` \
🔥Addrbook🔥:  `wget -O $HOME/.cheqdnode/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.cheqdnode/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/genesis.json"` \
🔥Auto_install script🔥:`wget -O cheqdm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/cheqdm && chmod +x cheqdm && ./cheqdm` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Cheqd/Decentralization)🔥

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




<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>78.46.83.78:26657</td><td>cheqd-mainnet-1</td><td>cstp-cheqd 🔴</td><td>11759098</td><td>1</td><td>False</td><td>on</td><td>2374609134</td><td>2024-01-29T05:25:10.554016233UTC</td></tr><tr><td>13.59.81.97:26657</td><td>cheqd-mainnet-1</td><td>ydp1-chqd 🔴</td><td>11759102</td><td>1</td><td>False</td><td>on</td><td>38129023235</td><td>2024-01-29T05:25:37.030281856UTC</td></tr><tr><td>167.235.133.235:26657</td><td>cheqd-mainnet-1</td><td>danubetech-v2 🔴</td><td>11759107</td><td>1</td><td>False</td><td>on</td><td>13297099545</td><td>2024-01-29T05:26:12.548782026UTC</td></tr><tr><td>158.220.102.32:26657</td><td>cheqd-mainnet-1</td><td>vmi1259816.contaboserver.net 🟢</td><td>11759132</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-29T05:28:37.081149104UTC</td></tr><tr><td>208.77.197.82:33657</td><td>cheqd-mainnet-1</td><td>vidulum.app 🟢</td><td>11759131</td><td>8384004</td><td>False</td><td>on</td><td>0</td><td>2024-01-29T05:28:28.484590129UTC</td></tr><tr><td>135.181.6.249:26657</td><td>cheqd-mainnet-1</td><td>verio-id 🟢</td><td>9196500</td><td>8896499</td><td>False</td><td>on</td><td>0</td><td>2024-01-29T05:25:17.090237219UTC</td></tr><tr><td>149.102.137.113:26657</td><td>cheqd-mainnet-1</td><td>node101 🔴</td><td>11759120</td><td>10276869</td><td>False</td><td>on</td><td>7249092474</td><td>2024-01-29T05:27:26.225750579UTC</td></tr><tr><td>80.39.181.74:30657</td><td>cheqd-mainnet-1</td><td>Validavia 🔴</td><td>11759109</td><td>10423019</td><td>False</td><td>on</td><td>2383796995</td><td>2024-01-29T05:26:21.280269489UTC</td></tr><tr><td>142.132.248.253:22257</td><td>cheqd-mainnet-1</td><td>Blackhox 🔴</td><td>11759126</td><td>10538869</td><td>False</td><td>on</td><td>2267459902</td><td>2024-01-29T05:27:58.232985394UTC</td></tr><tr><td>65.21.20.218:26657</td><td>cheqd-mainnet-1</td><td>Blockval_Node 🟢</td><td>11759113</td><td>11356095</td><td>False</td><td>on</td><td>0</td><td>2024-01-29T05:26:45.677927993UTC</td></tr><tr><td>51.159.165.38:26657</td><td>cheqd-mainnet-1</td><td>cheqd-validator-temp 🔴</td><td>11759128</td><td>11446869</td><td>False</td><td>on</td><td>10408936791</td><td>2024-01-29T05:28:13.150204047UTC</td></tr><tr><td>66.45.246.166:26337</td><td>cheqd-mainnet-1</td><td>Paradigm 🔴</td><td>11759120</td><td>11505869</td><td>False</td><td>on</td><td>206321</td><td>2024-01-29T05:27:37.209645084UTC</td></tr><tr><td>206.189.247.12:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>11759100</td><td>11509100</td><td>False</td><td>on</td><td>40844923570</td><td>2024-01-29T05:25:25.751733124UTC</td></tr><tr><td>134.209.190.126:26657</td><td>cheqd-mainnet-1</td><td>seerbytes 🔴</td><td>11759107</td><td>11509107</td><td>False</td><td>on</td><td>221759950</td><td>2024-01-29T05:26:12.278637728UTC</td></tr><tr><td>51.145.165.17:26657</td><td>cheqd-mainnet-1</td><td>DIDLab 🔴</td><td>11759111</td><td>11509111</td><td>False</td><td>on</td><td>19087991194</td><td>2024-01-29T05:26:33.856326715UTC</td></tr><tr><td>13.244.233.116:26657</td><td>cheqd-mainnet-1</td><td>DIDx 🔴</td><td>11759112</td><td>11509112</td><td>False</td><td>on</td><td>3716478323</td><td>2024-01-29T05:26:36.769268505UTC</td></tr><tr><td>159.69.174.238:26657</td><td>cheqd-mainnet-1</td><td>node0-monokee 🔴</td><td>11759113</td><td>11509113</td><td>False</td><td>on</td><td>15211157917</td><td>2024-01-29T05:26:41.258698407UTC</td></tr><tr><td>143.110.218.56:26657</td><td>cheqd-mainnet-1</td><td>continuumloop-mn 🔴</td><td>11759114</td><td>11509114</td><td>False</td><td>on</td><td>6351374939</td><td>2024-01-29T05:26:50.439808372UTC</td></tr><tr><td>206.189.25.194:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>11759119</td><td>11509119</td><td>False</td><td>on</td><td>40844923570</td><td>2024-01-29T05:27:17.575339954UTC</td></tr><tr><td>135.181.210.171:26337</td><td>cheqd-mainnet-1</td><td>STAVR-Service 🟢</td><td>11759100</td><td>11754869</td><td>False</td><td>on</td><td>0</td><td>2024-01-29T05:25:26.087042451UTC</td></tr></table>
