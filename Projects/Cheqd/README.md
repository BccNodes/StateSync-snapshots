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




<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>78.46.83.78:26657</td><td>cheqd-mainnet-1</td><td>cstp-cheqd 🔴</td><td>11495684</td><td>1</td><td>False</td><td>on</td><td>2365025334</td><td>2024-01-11T05:39:52.132313359UTC</td></tr><tr><td>13.59.81.97:26657</td><td>cheqd-mainnet-1</td><td>ydp1-chqd 🔴</td><td>11495686</td><td>1</td><td>False</td><td>on</td><td>37459705030</td><td>2024-01-11T05:40:04.281471174UTC</td></tr><tr><td>167.235.133.235:26657</td><td>cheqd-mainnet-1</td><td>danubetech-v2 🔴</td><td>11495688</td><td>1</td><td>False</td><td>on</td><td>13292099545</td><td>2024-01-11T05:40:17.342049031UTC</td></tr><tr><td>158.220.102.32:26657</td><td>cheqd-mainnet-1</td><td>vmi1259816.contaboserver.net 🟢</td><td>11495696</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-11T05:41:06.513354090UTC</td></tr><tr><td>208.77.197.82:33657</td><td>cheqd-mainnet-1</td><td>vidulum.app 🟢</td><td>11495696</td><td>8384004</td><td>False</td><td>on</td><td>0</td><td>2024-01-11T05:41:04.165389137UTC</td></tr><tr><td>135.181.6.249:26657</td><td>cheqd-mainnet-1</td><td>verio-id 🟢</td><td>9196500</td><td>8896499</td><td>False</td><td>on</td><td>0</td><td>2024-01-11T05:39:52.550809093UTC</td></tr><tr><td>65.21.20.218:26657</td><td>cheqd-mainnet-1</td><td>Blockval_Node 🟢</td><td>11495691</td><td>9634953</td><td>False</td><td>on</td><td>0</td><td>2024-01-11T05:40:29.910843061UTC</td></tr><tr><td>149.102.137.113:26657</td><td>cheqd-mainnet-1</td><td>node101 🔴</td><td>11495693</td><td>10276869</td><td>False</td><td>on</td><td>7245006964</td><td>2024-01-11T05:40:47.861345222UTC</td></tr><tr><td>80.39.181.74:30657</td><td>cheqd-mainnet-1</td><td>Validavia 🔴</td><td>11495689</td><td>10423019</td><td>False</td><td>on</td><td>2288699044</td><td>2024-01-11T05:40:19.877586504UTC</td></tr><tr><td>142.132.248.253:22257</td><td>cheqd-mainnet-1</td><td>Blackhox 🔴</td><td>11495694</td><td>10538869</td><td>False</td><td>on</td><td>2242211499</td><td>2024-01-11T05:40:54.922762611UTC</td></tr><tr><td>66.45.246.166:26337</td><td>cheqd-mainnet-1</td><td>Paradigm 🔴</td><td>11495693</td><td>10979869</td><td>False</td><td>on</td><td>206321</td><td>2024-01-11T05:40:50.499622725UTC</td></tr><tr><td>206.189.247.12:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>11495685</td><td>11245685</td><td>False</td><td>on</td><td>40621550326</td><td>2024-01-11T05:40:01.175611458UTC</td></tr><tr><td>134.209.190.126:26657</td><td>cheqd-mainnet-1</td><td>seerbytes 🔴</td><td>11495688</td><td>11245688</td><td>False</td><td>on</td><td>222001984</td><td>2024-01-11T05:40:17.080532112UTC</td></tr><tr><td>51.145.165.17:26657</td><td>cheqd-mainnet-1</td><td>DIDLab 🔴</td><td>11495690</td><td>11245689</td><td>False</td><td>on</td><td>20123441232</td><td>2024-01-11T05:40:26.290683257UTC</td></tr><tr><td>13.244.233.116:26657</td><td>cheqd-mainnet-1</td><td>DIDx 🔴</td><td>11495690</td><td>11245690</td><td>False</td><td>on</td><td>3710352823</td><td>2024-01-11T05:40:27.172717798UTC</td></tr><tr><td>159.69.174.238:26657</td><td>cheqd-mainnet-1</td><td>node0-monokee 🔴</td><td>11495691</td><td>11245691</td><td>False</td><td>on</td><td>15711410032</td><td>2024-01-11T05:40:29.573172721UTC</td></tr><tr><td>143.110.218.56:26657</td><td>cheqd-mainnet-1</td><td>continuumloop-mn 🔴</td><td>11495691</td><td>11245691</td><td>False</td><td>on</td><td>6341236720</td><td>2024-01-11T05:40:30.631158212UTC</td></tr><tr><td>206.189.25.194:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>11495692</td><td>11245692</td><td>False</td><td>on</td><td>40621550326</td><td>2024-01-11T05:40:45.414168120UTC</td></tr><tr><td>135.181.210.171:26337</td><td>cheqd-mainnet-1</td><td>STAVR-Service 🟢</td><td>11495685</td><td>11490869</td><td>False</td><td>on</td><td>0</td><td>2024-01-11T05:40:01.513401611UTC</td></tr></table>
