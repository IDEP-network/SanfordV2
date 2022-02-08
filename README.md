# Incentivized-testnet Sanford V2

# Requirements #
* Latest Version of Ubuntu
* 4 CPU Processor
* 8-16 GB Ram
* 1 TB Storage

### Incentivized-testnet Sanford is utilizing Cosmos version 0.44.5

## Setup

**Prerequisites:** Make sure to have [Golang >=1.17](https://golang.org/).

- Download the IDEP client binary iond
```
git clone https://github.com/IDEP-network/SanfordV2.git
```

- Move/Copy the binary to /usr/local/bin/
```
sudo cp incentivized-testnet/binary/iond /usr/local/bin/
```

- Add permissions to the binary
```
sudo chmod a+x /usr/local/bin/iond
```

## Install Wasmvm dependency
```
go get -u github.com/CosmWasm/wasmvm@v1.0.0-beta4
cd $HOME/go/pkg/mod/github.com/\!cosm\!wasm/wasmvm@v1.0.0-beta4/api
chmod +x libwasmvm.so
```

### Add LD_LIBRARY_PATH
```
echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/go/pkg/mod/github.com/\!cosm\!wasm/wasmvm@v1.0.0-beta4/api" >> $HOME/.bash_profile
source $HOME/.bash_profile
```

- Check the binary commands with
```
iond -h
```

## Full-Node Initialization
```
iond init <moniker> --chain-id SanfordNetworkV2
iond keys add <accountname>
```
- Save the mnemonic in a safe place and dont share it with anyone

- Add seeds and persistent_peers to config.toml

- Next make your way to the nodes config directory, remove the genesis.json and replace it with the one provided in this repo
```
cd ~/.ion/config/

rm genesis.json
wget https://raw.githubusercontent.com/IDEP-network/SanfordV2/main/genesis.json
```

## Start Node

```
iond start
```

