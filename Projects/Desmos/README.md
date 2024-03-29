<h1 align="center"> 🔥Desmos🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Desmos)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://desmos.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.desmos/config/config.toml
desmos tendermint unsafe-reset-all
wget -O $HOME/.desmos/config/addrbook.json "https://raw.githubusercontent.com/nodersteam/cosmos-adrbook/main/desmos/addrbook.json"
curl -o - -L https://desmos.wasm.stavr.tech/wasm-desmos.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.desmos --strip-components 2
sudo systemctl restart desmos && sudo journalctl -u desmos -f -o cat
```
# SnapShot (~0.9 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop desmos
cp $HOME/.desmos/data/priv_validator_state.json $HOME/.desmos/priv_validator_state.json.backup
rm -rf $HOME/.desmos/data
curl -o - -L https://desmos.snapshot.stavr.tech/desmos/desmos-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.desmos --strip-components 2
curl -o - -L https://desmos.wasm.stavr.tech/wasm-desmos.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.desmos --strip-components 2
mv $HOME/.desmos/priv_validator_state.json.backup $HOME/.desmos/data/priv_validator_state.json
wget -O $HOME/.desmos/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Desmos/addrbook.json"
sudo systemctl restart desmos && journalctl -u desmos -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Desmos-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://desmos.api.m.stavr.tech \
🔥RPC🔥:          https://desmos.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://desmos.grpc.m.stavr.tech:108 \
🔥seed🔥:      `a225d2e2dfe610993d83bf5e25025bde3ef38095@desmos.seed.stavr.tech:1046` \
🔥Genesis🔥:   `wget -O $HOME/.desmos/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Desmos/genesis.json"` \
🔥WASM🔥:      `curl -o - -L https://desmos.wasm.stavr.tech/wasm-desmos.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.desmos --strip-components 2` \
🔥Addrbook🔥:  `wget -O $HOME/.desmos/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Desmos/addrbook.json"` \
🔥Auto_install script🔥:`wget -O desmosm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Desmos/desmosm && chmod +x desmosm && ./desmosm`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Desmos/Decentralization)🔥
=
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

[raw Mainnet json](https://rpc-check.desmosm.stavr.tech/desmosm/rpc-desmosm-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>35.201.187.22:26657</td><td>desmos-mainnet</td><td>datax 🔴</td><td>13138565</td><td>1</td><td>False</td><td>on</td><td>2068062</td><td>2024-03-28T14:23:45.253675429UTC</td></tr><tr><td>203.135.141.134:26657</td><td>desmos-mainnet</td><td>UD 🔴</td><td>13138571</td><td>8770001</td><td>False</td><td>on</td><td>998956</td><td>2024-03-28T14:24:21.079791905UTC</td></tr><tr><td>185.225.232.183:26657</td><td>desmos-mainnet</td><td>srqn 🔴</td><td>13138572</td><td>11894001</td><td>False</td><td>off</td><td>713308</td><td>2024-03-28T14:24:23.404571934UTC</td></tr><tr><td>144.91.125.55:26657</td><td>desmos-mainnet</td><td>techbnz 🔴</td><td>13138572</td><td>11894501</td><td>False</td><td>off</td><td>636929</td><td>2024-03-28T14:24:25.734645663UTC</td></tr><tr><td>65.21.91.99:36657</td><td>desmos-mainnet</td><td>Staketab-snap 🟢</td><td>13138574</td><td>12792001</td><td>False</td><td>off</td><td>0</td><td>2024-03-28T14:24:38.781312219UTC</td></tr><tr><td>66.45.246.166:1047</td><td>desmos-mainnet</td><td>STAVR-Service 🟢</td><td>13138574</td><td>13135501</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T14:24:38.494138935UTC</td></tr></table>
