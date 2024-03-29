<h1 align="center"> 🔥Teritori🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Teritori)
=

# StateSync Mainnet
```python
SNAP_RPC=https://teritori.rpc.m.stavr.tech:443
peers="ab77fecd8c58d89a1bd28bc198449aa2d7fb8740@teritori.peers.stavr.tech:38026"
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.teritorid/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.teritorid/config/config.toml
teritorid tendermint unsafe-reset-all --home $HOME/.teritorid --keep-addr-book
curl -o - -L http://teritori.wasm.stavr.tech:1011/wasm-teritori.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.teritorid --strip-components 2
wget -O $HOME/.teritorid/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Teritori/addrbook.json"
sudo systemctl restart teritorid && journalctl -u teritorid -f -o cat
```

# SnapShot Mainnet (~0.7 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop teritorid
cp $HOME/.teritorid/data/priv_validator_state.json $HOME/.teritorid/priv_validator_state.json.backup
rm -rf $HOME/.teritorid/data
curl -o - -L http://teritori.snapshot.stavr.tech:1001/teritori/teritori-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.teritorid --strip-components 2
mv $HOME/.teritorid/priv_validator_state.json.backup $HOME/.teritorid/data/priv_validator_state.json
wget -O $HOME/.teritorid/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Teritori/addrbook.json"
sudo systemctl restart teritorid && journalctl -u teritorid -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Teritori-Main/staking      `Indexer "ON"` \
🔥EXPLORER Testnet🔥:        https://explorer.stavr.tech/Teritori/staking            `Indexer "ON"` \
🔥API Mainnet🔥:                   https://teritori.api.m.stavr.tech \
🔥RPC🔥:                                   https://teritori.rpc.m.stavr.tech                         `Snapshot-interval = 100` \
🔥API Testnet🔥:                     https://teritori.api.t.stavr.tech \
🔥peer🔥:                     `ab77fecd8c58d89a1bd28bc198449aa2d7fb8740@teritori.peers.stavr.tech:38026` \
🔥gRPC🔥:                                http://teritori.grpc.m.stavr.tech:6705 \
🔥WASM🔥: ```curl -o - -L http://teritori.wasm.stavr.tech:1011/wasm-teritori.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.teritorid --strip-components 2``` updated every 2 hours \
🔥Addrbook-M🔥:    ```wget -O $HOME/.teritorid/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Teritori/addrbook.json"``` \
🔥Addrbook-T🔥:    ```wget -O $HOME/.teritorid/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Teritori/Teritori%20testnet/addrbook.json"``` \
🔥Auto_install script-M🔥: ```wget -O teritorm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Teritori/teritorm && chmod +x teritorm && ./teritorm``` \
🔥Auto_install script-T🔥: ```wget -O teritor https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Teritori/Teritori%20testnet/teritor && chmod +x teritor && ./teritor```

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

[raw json Mainnet](https://rpc-check.teritorim.stavr.tech/teritorim/rpc-teritorim-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.108.199.120:36657</td><td>teritori-1</td><td>RAMZES 🔴</td><td>8068291</td><td>5996001</td><td>False</td><td>on</td><td>784782</td><td>2024-03-28T10:28:31.761872045UTC</td></tr><tr><td>95.214.53.76:11957</td><td>teritori-1</td><td>Equinox 🔴</td><td>8068283</td><td>7203180</td><td>False</td><td>on</td><td>1545333</td><td>2024-03-28T10:27:42.386525176UTC</td></tr><tr><td>65.108.70.119:27657</td><td>teritori-1</td><td>Hermes 🟢</td><td>8068319</td><td>7203180</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T10:31:13.391961022UTC</td></tr><tr><td>144.76.29.90:36657</td><td>teritori-1</td><td>UTSA_guide 🟢</td><td>8068312</td><td>7208001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T10:30:32.399784358UTC</td></tr><tr><td>152.53.22.65:26610</td><td>teritori-1</td><td>DeFi100-iCosmosDAO 🔴</td><td>8068337</td><td>7536429</td><td>False</td><td>on</td><td>1448304</td><td>2024-03-28T10:32:58.087820615UTC</td></tr><tr><td>65.109.92.240:20027</td><td>teritori-1</td><td>Aurie 🔴</td><td>8068322</td><td>7568001</td><td>False</td><td>on</td><td>119310</td><td>2024-03-28T10:31:30.192635461UTC</td></tr><tr><td>152.53.34.76:26610</td><td>teritori-1</td><td>Nodehub 🔴</td><td>8068338</td><td>7580883</td><td>False</td><td>on</td><td>65696</td><td>2024-03-28T10:33:04.873549827UTC</td></tr><tr><td>65.108.141.109:15657</td><td>teritori-1</td><td>node 🟢</td><td>8068318</td><td>7714496</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T10:31:06.261894673UTC</td></tr><tr><td>75.119.146.181:19657</td><td>teritori-1</td><td>geonodes 🔴</td><td>8068315</td><td>7747478</td><td>False</td><td>on</td><td>37840</td><td>2024-03-28T10:30:51.387997846UTC</td></tr><tr><td>65.108.75.107:15657</td><td>teritori-1</td><td>node 🟢</td><td>8068331</td><td>7995732</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T10:32:24.742539008UTC</td></tr><tr><td>135.181.210.171:38027</td><td>teritori-1</td><td>STAVR-Service 🟢</td><td>8068281</td><td>8067001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T10:27:35.887551367UTC</td></tr></table>
