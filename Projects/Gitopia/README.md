<h1 align="center"> 🔥Gitopia🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Gitopia)
=

<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=http://gitopia.rpc.m.stavr.tech:51057
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.gitopia/config/config.toml
gitopiad tendermint unsafe-reset-all --home /root/.gitopia
wget -O $HOME/.gitopia/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Gitopia/addrbook.json"
systemctl restart gitopiad && journalctl -u gitopiad -f -o cat
```
# SnapShot (~2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop gitopiad
cp $HOME/.gitopia/data/priv_validator_state.json $HOME/.gitopia/priv_validator_state.json.backup
rm -rf $HOME/.gitopia/data
curl -o - -L http://gitopia.snapshot.stavr.tech:1030/gitopia/gitopia-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.gitopia --strip-components 2
mv $HOME/.gitopia/priv_validator_state.json.backup $HOME/.gitopia/data/priv_validator_state.json
wget -O $HOME/.gitopia/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Gitopia/addrbook.json"
sudo systemctl restart gitopiad && journalctl -u gitopiad -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:      https://explorer.stavr.tech/Gitopia-M/staking  `Indexer "ON"` \
🔥API🔥: 			 		 https://gitopia.api.m.stavr.tech \
🔥RPC🔥:           http://gitopia.rpc.m.stavr.tech:51057              `Snapshot-interval = 300` \
🔥GRPC🔥:          http://gitopia.grpc.m.stavr.tech:5123 \
🔥peer🔥:					 `6f9f729f2d4a9c3cbab3130157f5200a61bbb273@gitopia.peers.stavr.tech:51056` \
🔥Addrbook🔥:    ```wget -O $HOME/.gitopia/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Gitopia/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O gitopm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Gitopia/gitopm && chmod +x gitopm && ./gitopm```


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

[raw Mainnet json](https://rpc-check.gitopm.stavr.tech/gitopm/rpc-gitopm-result.json)
=

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>174.138.180.190:46657</td><td>gitopia</td><td>UTSA_guide 🟢</td><td>9884496</td><td>6071990</td><td>False</td><td>0</td><td>2023-11-30T00:18:46.316022244UTC</td></tr><tr><td>213.239.194.132:14157</td><td>gitopia</td><td>semalist 🔴</td><td>9884510</td><td>6071990</td><td>False</td><td>428783</td><td>2023-11-30T00:19:08.122529881UTC</td></tr><tr><td>144.76.174.27:21657</td><td>gitopia</td><td>kokos 🔴</td><td>9884519</td><td>6071990</td><td>False</td><td>936373</td><td>2023-11-30T00:19:22.116977165UTC</td></tr><tr><td>142.132.202.86:20001</td><td>gitopia</td><td>ramuchi.tech 🟢</td><td>9884517</td><td>6548337</td><td>False</td><td>0</td><td>2023-11-30T00:19:19.337746959UTC</td></tr><tr><td>65.108.226.26:20657</td><td>gitopia</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>9884530</td><td>6846001</td><td>False</td><td>0</td><td>2023-11-30T00:19:39.307990316UTC</td></tr><tr><td>65.108.141.109:30657</td><td>gitopia</td><td>node 🟢</td><td>9884517</td><td>6931333</td><td>False</td><td>0</td><td>2023-11-30T00:19:18.779093035UTC</td></tr><tr><td>135.181.133.249:12857</td><td>gitopia</td><td>StakeUp_rpc 🟢</td><td>9884518</td><td>8010001</td><td>False</td><td>0</td><td>2023-11-30T00:19:19.746011815UTC</td></tr><tr><td>65.108.75.107:30657</td><td>gitopia</td><td>node 🟢</td><td>9884526</td><td>8802845</td><td>False</td><td>0</td><td>2023-11-30T00:19:32.664731640UTC</td></tr><tr><td>148.251.235.130:11657</td><td>gitopia</td><td>snap-gitopia 🟢</td><td>9884517</td><td>9516001</td><td>False</td><td>0</td><td>2023-11-30T00:19:19.053945903UTC</td></tr><tr><td>185.248.24.51:15457</td><td>gitopia</td><td>Moonbridge 🟢</td><td>9884510</td><td>9781501</td><td>False</td><td>0</td><td>2023-11-30T00:19:07.795855947UTC</td></tr></table>
