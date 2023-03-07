# nolus-snap

<p align="center">
  <img height="100" height="auto" src="https://raw.githubusercontent.com/Nodeist/Kurulumlar/main/logos/nolus.png">
</p>


# Nolus Snapshot Setup

You can browse the [logs](https://nolus.elessarr.xyz/nolus/log.txt) for current snapshot date, block height, and file size information.


### Install lz4 (if needed)
```
sudo apt update
sudo apt install snapd -y
sudo snap install lz4
```

### Stop your node
```
sudo systemctl stop nolusd
```

### Reset your node
This will erase your node database. If you are already running validator, be sure you backed up your `priv_validator_key.json` prior to running the the command.

```
nolusd tendermint unsafe-reset-all --home $HOME/.nolus --keep-addr-book
```

### Download & Install the snapshot
```
curl -L https://nolus.elessarr.xyz/nolus/log.txt | lz4 -dc - | tar -xf - -C $HOME/.nolus --strip-components 2
```

### Restart Service & Check Log:
```
sudo systemctl start nolusd && journalctl -u nolusd -f --no-hostname -o cat
