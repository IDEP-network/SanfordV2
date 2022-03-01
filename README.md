<h1><p align="center"><img alt="Banner" src="SanfordV2.png" /></p></h1>

<h1 align="center">Incentivized Network Sanford V2.0</h1>

## Requirements #
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
sudo cp SanfordV2/iond /usr/local/bin/
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
wget https://raw.githubusercontent.com/IDEP-network/SanfordV2/master/genesis.json
```

## Start Node

```
iond start
```

### Validator-Setup

- To get your Public Address
```
iond keys list
```
- Create a Validator

Before you can create your Validator, your node has to be synced up to the latest block of the chain. You can check this by:

```
iond status
```
If `catching_up` is `false` you are good to execute:

```
iond tx staking create-validator \
    --amount 10000000000idep \
    --commission-max-change-rate 0.01 \
    --commission-max-rate 0.2 \
    --commission-rate 0.1 \
    --from <YourWalletAddress> \
    --min-self-delegation 1 \
    --moniker <YourMoniker> \
    --pubkey $(iond tendermint show-validator) \
    --chain-id SanfordV2
```

### Seeds
```
32312653a1397f0912035d5a382e0e8664989a8f@137.184.192.7:26656
```

### FAQ
#### Example of a command to create a Validator
```
iond tx staking create-validator --amount 15000000000000idep --from idep1d2nqcwf9zz9fx7xlesyt0gc3utfxe2mk6nfwey --pubkey idepvalconspub1zcjduepqztw5yzm5wj0yc600aaemxlmda5488jv9hycxfnta3w7vz9jgpawqc9qnhs --commission-rate 0.01 --commission-max-rate 0.05 --commission-max-change-rate 0.005 --min-self-delegation 1 --chain-id SanfordV2
```

#### To know more about the commands and other parameters
```
iond tx staking create-validator --help
```
#### Tendermint API Documentation
https://v1.cosmos.network/rpc/v0.41.4

**Note:** IDEP Token has 8 decimal places. If you wish to run a validator with 100,000 tokens you must set the ammount to --ammount 10000000000000
