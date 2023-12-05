<h1 align="center"> 🔥LAMBDA MAINNET🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Lambda)
=


# StateSync
```python
SNAP_RPC=http://lambda.rpc.m.stavr.tech:31327
peers="ebdd47f7babb184240258d2fc6fba61bd994edaa@lambda.peer.stavr.tech:31326" 
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.lambdavm/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.lambdavm/config/config.toml
lambdavm tendermint unsafe-reset-all --home $HOME/.lambdavm
systemctl restart lambdavm && journalctl -u lambdavm -f -o cat

```
# SnapShot (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop lambdavm
cp $HOME/.lambdavm/data/priv_validator_state.json $HOME/.lambdavm/priv_validator_state.json.backup
rm -rf $HOME/.lambdavm/data
curl -o - -L http://lambda.snapshot.stavr.tech:5016/lambda/lambda-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.lambdavm --strip-components 2
mv $HOME/.lambdavm/priv_validator_state.json.backup $HOME/.lambdavm/data/priv_validator_state.json
wget -O $HOME/.lambdavm/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lambda/addrbook.json"
sudo systemctl restart lambdavm && sudo journalctl -u lambdavm -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:      https://explorer.stavr.tech/Lambda/staking	        `Indexer "ON"` \
🔥API🔥: 			 		 https://lambda.api.m.stavr.tech \
🔥RPC🔥:           http://lambda.rpc.m.stavr.tech:31327	              `Snapshot-interval = 100` \
🔥gRPC🔥:          http://lambda.grpc.m.stavr.tech:2287 \
🔥peer🔥:					 `ebdd47f7babb184240258d2fc6fba61bd994edaa@lambda.peer.stavr.tech:31326` \
🔥Addrbook🔥:    ```wget -O $HOME/.lambdavm/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lambda/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O lamb https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lambda/lamb && chmod +x lamb && ./lamb```


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

[raw json Mainnet](https://rpc-check.lambm.stavr.tech/lambm/rpc-lambm-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>13.229.162.168:26657</td><td>lambda_92000-1</td><td>genesis2 🔴</td><td>10364985</td><td>1</td><td>False</td><td>16607038</td><td>2023-12-05T12:51:50.441296551UTC</td></tr><tr><td>13.229.27.15:26657</td><td>lambda_92000-1</td><td>genesis4 🔴</td><td>10364986</td><td>1</td><td>False</td><td>9887611</td><td>2023-12-05T12:51:53.501231309UTC</td></tr><tr><td>13.213.214.88:26657</td><td>lambda_92000-1</td><td>genesis1 🔴</td><td>10364986</td><td>1</td><td>False</td><td>107835</td><td>2023-12-05T12:51:54.881439036UTC</td></tr><tr><td>65.108.134.215:33657</td><td>lambda_92000-1</td><td>moodman 🔴</td><td>10364987</td><td>632001</td><td>False</td><td>1070005</td><td>2023-12-05T12:52:00.073325546UTC</td></tr><tr><td>65.109.84.19:26008</td><td>lambda_92000-1</td><td>bricks_lamb 🟢</td><td>7715743</td><td>7581001</td><td>False</td><td>0</td><td>2023-12-05T12:52:04.529038638UTC</td></tr><tr><td>65.21.141.82:21657</td><td>lambda_92000-1</td><td>kokos 🔴</td><td>10364986</td><td>7716001</td><td>False</td><td>546765</td><td>2023-12-05T12:51:57.330858123UTC</td></tr><tr><td>213.239.207.175:33657</td><td>lambda_92000-1</td><td>landeros 🔴</td><td>10364984</td><td>8136001</td><td>False</td><td>935554</td><td>2023-12-05T12:51:44.208143472UTC</td></tr><tr><td>65.109.88.254:29657</td><td>lambda_92000-1</td><td>ksalab 🔴</td><td>10364987</td><td>8715001</td><td>False</td><td>501430</td><td>2023-12-05T12:52:00.819503268UTC</td></tr><tr><td>209.182.238.19:46657</td><td>lambda_92000-1</td><td>SECARD 🔴</td><td>10364984</td><td>9443001</td><td>False</td><td>2092101</td><td>2023-12-05T12:51:49.458106532UTC</td></tr><tr><td>38.242.220.64:26657</td><td>lambda_92000-1</td><td>mahof 🔴</td><td>10364983</td><td>10131001</td><td>False</td><td>770350</td><td>2023-12-05T12:51:39.387086999UTC</td></tr><tr><td>185.215.167.227:13657</td><td>lambda_92000-1</td><td>MAHOF 🔴</td><td>10364986</td><td>10134001</td><td>False</td><td>2051510</td><td>2023-12-05T12:51:53.934680143UTC</td></tr><tr><td>23.88.91.115:26101</td><td>lambda_92000-1</td><td>RedHead 🔴</td><td>10364984</td><td>10264984</td><td>False</td><td>553202</td><td>2023-12-05T12:51:44.475066422UTC</td></tr><tr><td>65.21.90.141:12121</td><td>lambda_92000-1</td><td>SerGo 🔴</td><td>10364987</td><td>10264987</td><td>False</td><td>10521562</td><td>2023-12-05T12:52:01.178403884UTC</td></tr><tr><td>88.198.32.17:26657</td><td>lambda_92000-1</td><td>n0ok[MC] 🔴</td><td>10364988</td><td>10264988</td><td>False</td><td>1578630</td><td>2023-12-05T12:52:04.126785660UTC</td></tr><tr><td>130.255.170.126:36657</td><td>lambda_92000-1</td><td>Sr20de 🔴</td><td>10364984</td><td>10353001</td><td>False</td><td>671007</td><td>2023-12-05T12:51:44.912655570UTC</td></tr><tr><td>135.181.210.171:31327</td><td>lambda_92000-1</td><td>STAVR-Service 🟢</td><td>10364987</td><td>10361001</td><td>False</td><td>0</td><td>2023-12-05T12:51:59.728548931UTC</td></tr></table>
