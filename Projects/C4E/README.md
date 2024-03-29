<h1 align="center"> 🔥C4E🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/C4E)
=

<h1 align="center"> MAINNET</h1>

# StateSync C4E Mainnet
```python
SNAP_RPC=https://c4e.rpc.m.stavr.tech:443
peers="fbf9a48eca1ba873ad766e2cb72a0562596a248f@c4e.peer.stavr.tech:17096"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.c4e-chain/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.c4e-chain/config/config.toml
c4ed tendermint unsafe-reset-all --home /root/.c4e-chain --keep-addr-book
sudo systemctl restart c4ed && journalctl -u c4ed -f -o cat
```
# SnapShot (~0.1 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop c4ed
cp $HOME/.c4e-chain/data/priv_validator_state.json $HOME/.c4e-chain/priv_validator_state.json.backup
rm -rf $HOME/.c4e-chain/data
curl -o - -L http://c4e.snapshot.stavr.tech:1018/c4e/c4e-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.c4e-chain --strip-components 2
mv $HOME/.c4e-chain/priv_validator_state.json.backup $HOME/.c4e-chain/data/priv_validator_state.json
wget -O $HOME/.c4e-chain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/addrbook.json"
sudo systemctl restart c4ed && journalctl -u c4ed -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER MAINNET🔥:  https://explorer.stavr.tech/C4E/staking            `Indexer "ON"` \
🔥EXPLORER TESTET🔥:   https://explorer.stavr.tech/C4E-Testnet/staking     `Indexer "ON"` \
🔥API MAINNET🔥:       https://c4e.api.m.stavr.tech \
🔥API TESTNET🔥:       https://c4e.api.t.stavr.tech \
🔥RPC🔥:               https://c4e.rpc.m.stavr.tech:443                  `Snapshot-interval = 100` \
🔥gRPC🔥:              http://c4e.grpc.m.stavr.tech:7029 \
🔥peer🔥:              `fbf9a48eca1ba873ad766e2cb72a0562596a248f@c4e.peer.stavr.tech:17096` \
🔥Addrbook-M🔥:    ```wget https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/genesis.json -O $HOME/.c4e-chain/config/genesis.json``` \
🔥Addrbook-T🔥:    ```wget -O $HOME/.c4e-chain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/C4E_Testnet/addrbook.json"``` \
🔥Auto_install script-M🔥: ```wget -O c4 https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/c4 && chmod +x c4 && ./c4``` \
🔥Auto_install script-T🔥: ```wget -O c4et https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/C4E_Testnet/c4et && chmod +x c4et && ./c4et```

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/C4E/Decentralization)🔥
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

[raw json](https://rpc-check.c4e.stavr.tech/c4e/rpc-c4e-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>79.137.68.96:26657</td><td>perun-1</td><td>archive-node2 🟢</td><td>7779187</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:31.916061099UTC</td></tr><tr><td>65.108.70.119:33657</td><td>perun-1</td><td>AlxVoy 🟢</td><td>7779612</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:45.995493163UTC</td></tr><tr><td>149.202.66.111:26657</td><td>perun-1</td><td>archive-node1 🟢</td><td>7779615</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:23:02.319317002UTC</td></tr><tr><td>185.245.182.192:46657</td><td>perun-1</td><td>Meerlabs 🔴</td><td>7779616</td><td>1051501</td><td>False</td><td>on</td><td>344615</td><td>2024-03-28T13:23:07.319167837UTC</td></tr><tr><td>185.215.167.18:26657</td><td>perun-1</td><td>Rawalot 🔴</td><td>7779618</td><td>1090501</td><td>False</td><td>on</td><td>450091</td><td>2024-03-28T13:23:18.340471383UTC</td></tr><tr><td>209.182.239.169:46657</td><td>perun-1</td><td>SECARD 🔴</td><td>7779614</td><td>2616101</td><td>False</td><td>off</td><td>749308</td><td>2024-03-28T13:22:57.646334872UTC</td></tr><tr><td>89.117.58.109:26657</td><td>perun-1</td><td>medes 🔴</td><td>7779617</td><td>2826001</td><td>False</td><td>off</td><td>891025</td><td>2024-03-28T13:23:13.758790652UTC</td></tr><tr><td>65.108.141.109:39657</td><td>perun-1</td><td>node 🟢</td><td>7779610</td><td>5303301</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:34.254634122UTC</td></tr><tr><td>185.252.235.83:26657</td><td>perun-1</td><td>Alien 🔴</td><td>7779615</td><td>6502501</td><td>False</td><td>on</td><td>648215</td><td>2024-03-28T13:23:02.585485182UTC</td></tr><tr><td>38.242.220.64:16657</td><td>perun-1</td><td>MAHOF 🟢</td><td>7779615</td><td>6885501</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:23:00.012641954UTC</td></tr><tr><td>142.132.136.106:25657</td><td>perun-1</td><td>services 🟢</td><td>7779613</td><td>7012001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:48.579749169UTC</td></tr><tr><td>65.109.30.185:26657</td><td>perun-1</td><td>c4e-sentry2-mainnet 🟢</td><td>7779616</td><td>7284001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:23:07.025060858UTC</td></tr><tr><td>77.55.216.80:26657</td><td>perun-1</td><td>c4e-sentry4-mainnet 🟢</td><td>7779612</td><td>7297001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:45.695904205UTC</td></tr><tr><td>65.108.75.107:39657</td><td>perun-1</td><td>node 🟢</td><td>7779613</td><td>7300001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:48.886091266UTC</td></tr><tr><td>5.135.141.191:26657</td><td>perun-1</td><td>c4e-sentry1-mainnet 🟢</td><td>7779610</td><td>7300501</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:31.085538227UTC</td></tr><tr><td>142.132.157.153:27257</td><td>perun-1</td><td>oadsuigasgoasdhgsaogadg 🟢</td><td>7779609</td><td>7574001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:28.808267974UTC</td></tr><tr><td>116.202.217.20:56657</td><td>perun-1</td><td>dteam 🟢</td><td>7779610</td><td>7660701</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:31.620145216UTC</td></tr><tr><td>168.119.226.107:26957</td><td>perun-1</td><td>c4e_rpc 🟢</td><td>7779611</td><td>7679611</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:38.972458449UTC</td></tr><tr><td>65.108.124.219:31657</td><td>perun-1</td><td>MantiCore 🔴</td><td>7779612</td><td>7679612</td><td>False</td><td>off</td><td>730039</td><td>2024-03-28T13:22:45.374294926UTC</td></tr><tr><td>65.108.121.227:16657</td><td>perun-1</td><td>landeros-rpc 🟢</td><td>7779610</td><td>7771501</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:31.400431426UTC</td></tr><tr><td>135.181.210.171:17097</td><td>perun-1</td><td>STAVR-Service 🟢</td><td>7779613</td><td>7777901</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T13:22:49.181787348UTC</td></tr></table>
