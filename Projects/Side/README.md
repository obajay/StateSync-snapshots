<h1 align="center"> 🔥Side🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Side_Protocol)
=

<h1 align="center"> TESTNET</h1>

# StateSync Side Testnet
```python
SNAP_RPC=https://side.rpc.t.stavr.tech:443
peers="fe54f3964664592b3be89eb685cc72e9aecb14e9@side-t.seed.stavr.tech:21306"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.side/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.side/config/config.toml
sided tendermint unsafe-reset-all --home /root/.side
wget -O $HOME/.side/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Side_Protocol/addrbook.json"
systemctl restart sided && journalctl -u sided -f -o cat
```
# SnapShot (~0.3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop sided
cp $HOME/.side/data/priv_validator_state.json $HOME/.side/priv_validator_state.json.backup
rm -rf $HOME/.side/data
curl -o - -L https://side-t.snapshot.stavr.tech/side-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.side --strip-components 2
mv $HOME/.side/priv_validator_state.json.backup $HOME/.side/data/priv_validator_state.json
wget -O $HOME/.side/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Side_Protocol/addrbook.json"
sudo systemctl restart sided && journalctl -u sided -f -o cat
```
 <h1 align="center"> Useful Tools</h1>
 
🔥EXPLORER🔥: https://explorer.stavr.tech/Side-Testnet/        `Indexer "ON"` \
🔥API🔥:      https://side.api.t.stavr.tech \
🔥RPC🔥:      https://side.rpc.t.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:     http://side.grpc.t.stavr.tech:9917 \
🔥peer🔥:     `fe54f3964664592b3be89eb685cc72e9aecb14e9@side-t.seed.stavr.tech:21306` \
🔥Addrbook🔥: ```wget -O $HOME/.side/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Side_Protocol/addrbook.json"``` \
🔥Auto_install script🔥:  `wget -O sidem https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Side_Protocol/sidem && chmod +x sidem && ./sidem`

<h1 align="center"> RPC Scanning</h1>

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

[raw Testnet json](https://rpc-check.sidet.stavr.tech/sidet/rpc-sidet-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>148.251.235.130:21657</td><td>side-testnet-3</td><td>Staketab-snap 🟢</td><td>20169</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-03-28T11:57:00.077697419UTC</td></tr><tr><td>65.21.137.227:21657</td><td>side-testnet-3</td><td>2xStake.com 🟢</td><td>20169</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:57:02.405618246UTC</td></tr><tr><td>65.108.141.228:26657</td><td>side-testnet-3</td><td>pro-nodes75 🔴</td><td>20169</td><td>1</td><td>False</td><td>on</td><td>856</td><td>2024-03-28T11:57:02.693155400UTC</td></tr><tr><td>135.181.216.54:3451</td><td>side-testnet-3</td><td>node 🔴</td><td>20170</td><td>1</td><td>False</td><td>off</td><td>1000100</td><td>2024-03-28T11:57:07.773845054UTC</td></tr><tr><td>202.182.119.24:26657</td><td>side-testnet-3</td><td>freebird 🟢</td><td>20170</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:57:09.007411225UTC</td></tr><tr><td>135.181.210.171:21307</td><td>side-testnet-3</td><td>STAVR-Service 🟢</td><td>20172</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:57:21.582695519UTC</td></tr><tr><td>95.216.242.118:36657</td><td>side-testnet-3</td><td>Sr20de 🔴</td><td>20173</td><td>1</td><td>False</td><td>on</td><td>1014098</td><td>2024-03-28T11:57:23.918197564UTC</td></tr><tr><td>185.188.249.46:45657</td><td>side-testnet-3</td><td>BonyNodePublic 🟢</td><td>20167</td><td>1001</td><td>False</td><td>off</td><td>0</td><td>2024-03-28T11:57:03.398619633UTC</td></tr></table>