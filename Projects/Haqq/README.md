<h1 align="center"> 🔥HAQQ🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/haqq)
=
# SnapShot (Temporarily stopped)
```python
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop haqqd
rm -rf $HOME/.haqqd/data/
mkdir $HOME/.haqqd/data/

# download archive
cd $HOME
wget http://haqq.snapshot.stavr.tech:7150/haqqddata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf haqqddata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.haqqd/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/Canto/priv_validator_state.json"
cd && cat .haqqd/data/priv_validator_state.json

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm haqqddata.tar.gz
systemctl restart haqqd && journalctl -u haqqd -f -o cat
```
