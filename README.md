<h1 align=center>0g_validator_node</h1>

![0_AxKIus_I-soNSp03](https://github.com/user-attachments/assets/ff87260c-cb0d-4cbc-a235-2c8e67d5d89c)

## Hardware Requirement
|Key|Value|
|:--|:----|
|Memory|64 GB|
|CPU|8 cores|
|Disk|1 TB NVME SSD|
|Bandwidth|100 MBps|

# Installation
## Install 0gchaind via CLI
```bash
git clone -b v0.2.3 https://github.com/0glabs/0g-chain.git
./0g-chain/networks/testnet/install.sh
source ~/.profile
```
## Set Chain ID
```bash
0gchaind config chain-id zgtendermint_16600-2
```

## Initialize Node
```bash
0gchaind init <your_validator_name> --chain-id zgtendermint_16600-2
```

## Genesis & Seeds
```bash
sudo apt install -y unzip wget
rm ~/.0gchain/config/genesis.json
wget -P ~/.0gchain/config https://github.com/0glabs/0g-chain/releases/download/v0.2.3/genesis.json
0gchaind validate-genesis
```
### Add seed Nodes
The format of the config.toml file is as follows:
```toml
[p2p]

# ...

# Comma separated list of seed nodes to connect to
seeds = "<node-id>@<ip>:<p2p port>"
```
```toml
81987895a11f6689ada254c6b57932ab7ed909b6@54.241.167.190:26656,010fb4de28667725a4fef26cdc7f9452cc34b16d@54.176.175.48:26656,e9b4bc203197b62cc7e6a80a64742e752f4210d5@54.193.250.204:26656,68b9145889e7576b652ca68d985826abd46ad660@18.166.164.232:26656
```

# Start Testnet
```bash
0gchaind start
```

# Create Validator
```bash
0gchaind keys add <key_name> --eth
```

```bash
0gchaind tx staking create-validator \
  --amount=<staking_amount>ua0gi \
  --pubkey=$(0gchaind tendermint show-validator) \
  --moniker="<your_validator_name>" \
  --chain-id=zgtendermint_16600-2 \
  --commission-rate="0.10" \
  --commission-max-rate="0.20" \
  --commission-max-change-rate="0.01" \
  --min-self-delegation="1" \
  --from=<key_name> \
  --gas=auto \
  --gas-adjustment=1.4
```
