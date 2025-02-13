<h1 align="center"> 🔥Uptick🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Uptick)
=

<h1 align="center"> MAINNET</h1>

# StateSync Uptick Mainnet
```python
SNAP_RPC=https://uptick.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.uptickd/config/config.toml
uptickd tendermint unsafe-reset-all --home $HOME/.uptickd
wget -O $HOME/.uptickd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Uptick/addrbook.json"
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.uptickd/config/app.toml
sudo systemctl restart uptickd && journalctl -u uptickd -f -o cat
```
# SnapShot (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop uptickd
cp $HOME/.uptickd/data/priv_validator_state.json $HOME/.uptickd/priv_validator_state.json.backup
rm -rf $HOME/.uptickd/data
curl -o - -L http://uptick.snapshot.stavr.tech:1027/uptickd/uptickd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.uptickd --strip-components 2
mv $HOME/.uptickd/priv_validator_state.json.backup $HOME/.uptickd/data/priv_validator_state.json
wget -O $HOME/.uptickd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Uptick/addrbook.json"
sudo systemctl restart uptickd && journalctl -u uptickd -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:         https://explorer.stavr.tech/Uptick-Mainnet      `Indexer "ON"` \
🔥EXPLORER Testnet🔥:           https://explorer.stavr.tech/uptick/staking        `Indexer "ON"` \
🔥API Mainnet🔥:                      https://uptick.api.m.stavr.tech \
🔥API Testnet🔥:                        https://uptick.api.t.stavr.tech \
🔥RPC🔥:                         https://uptick.rpc.m.stavr.tech:443              `Snapshot-interval = 100` \
🔥gRPC🔥:                                    http://uptick.grpc.m.stavr.tech:1901 \
🔥peer🔥:                                    `ee147b5a411750138a7add20dd004e4f8f1a2179@uptick.peers.stavr.tech:3156` \
🔥Genesis🔥:    ```wget -O $HOME/.uptickd/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Uptick/genesis.json"``` \
🔥Addrbook🔥:    ```wget -O $HOME/.uptickd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Uptick/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O uptickm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Uptick/uptickm && chmod +x uptickm && ./uptickm``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Uptick/Decentralization)🔥

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

[raw json Mainnet](https://rpc-check.uptickm.stavr.tech/uptickm/rpc-uptickm-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>168.119.75.7:26657</td><td>uptick_117-1</td><td>exp 🟢</td><td>4605201</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:57:03.478730381UTC</td></tr><tr><td>130.255.170.126:26657</td><td>uptick_117-1</td><td>Sr20de 🔴</td><td>4706891</td><td>4354901</td><td>False</td><td>off</td><td>557163</td><td>2024-02-05T11:57:03.922169972UTC</td></tr><tr><td>116.202.217.20:60757</td><td>uptick_117-1</td><td>dteam 🟢</td><td>4706893</td><td>4459901</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:57:15.878910900UTC</td></tr><tr><td>18.138.220.30:26657</td><td>uptick_117-1</td><td>cosmos-alliance 🔴</td><td>4706891</td><td>4551001</td><td>False</td><td>on</td><td>2272087</td><td>2024-02-05T11:57:02.956048467UTC</td></tr><tr><td>176.38.50.93:21357</td><td>uptick_117-1</td><td>ToTheMars 🟢</td><td>4706893</td><td>4588301</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:57:10.541421693UTC</td></tr><tr><td>142.132.152.46:27657</td><td>uptick_117-1</td><td>stakr-space 🔴</td><td>4706891</td><td>4603978</td><td>False</td><td>on</td><td>578701</td><td>2024-02-05T11:57:03.222907441UTC</td></tr><tr><td>65.108.195.29:21657</td><td>uptick_117-1</td><td>Staketab-snap 🟢</td><td>4706893</td><td>4605001</td><td>False</td><td>off</td><td>0</td><td>2024-02-05T11:57:12.984078501UTC</td></tr><tr><td>144.76.29.90:60957</td><td>uptick_117-1</td><td>UTSA_guide 🟢</td><td>4706891</td><td>4615501</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:56:59.698706398UTC</td></tr><tr><td>46.4.121.72:11557</td><td>uptick_117-1</td><td>nkbblocks 🟢</td><td>4706893</td><td>4620001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:57:15.310033944UTC</td></tr><tr><td>135.181.210.171:3157</td><td>uptick_117-1</td><td>STAVR-Service 🟢</td><td>4706893</td><td>4706001</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T11:57:16.274968942UTC</td></tr></table>
