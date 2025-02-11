# comdex-test-1
> This is comdex testnet chain
> GENESIS NOT PUBLISHED
> PEERS NOT PUBLISHED

1st testnet for comdex-official/comdex application.

## Hardware Requirements
* **Minimal**
    * 1 GB RAM
    * 25 GB HDD
    * 1.4 GHz CPU
* **Recommended**
    * 2 GB RAM
    * 100 GB HDD
    * 2.0 GHz x2 CPU

## Operating System
* Linux/Windows/MacOS(x86)
* **Recommended**
    * Linux(x86_64)

## Installation Steps
>Prerequisite: go1.17+ required. [ref](https://golang.org/doc/install)

>Prerequisite: git. [ref](https://github.com/git/git)

>Optional requirement: GNU make. [ref](https://www.gnu.org/software/make/manual/html_node/index.html)

* Clone git repository
```shell
git clone https://github.com/comdex-official/comdex.git
```
* Checkout latest tag
```shell
cd comdex
git fetch --tags
git checkout v0.0.1
```
* Install
```shell
make all
```

### Generate keys

`comdex keys add [key_name]`

or

`comdex keys add [key_name] --recover` to regenerate keys with your [BIP39](https://github.com/bitcoin/bips/tree/master/bip-0039) mnemonic


## Validator setup

### Before genesis: Accepting Genesis Validators

* [Install](#installation-steps) comdex core application
* Initialize node
```shell
comdex init {{NODE_NAME}} --chain-id comdex-test-1
comdex add-genesis-account {{KEY_NAME}} 100000000000000ucmdx
comdex gentx {{KEY_NAME}} 10000000ucmdx \
--chain-id comdex-test-1 \
--moniker="{{VALIDATOR_NAME}}" \
--commission-max-change-rate=0.01 \
--commission-max-rate=1.0 \
--commission-rate=0.07 \
--details="XXXXXXXX" \
--security-contact="XXXXXXXX" \
--website="XXXXXXXX"
```
* Copy the contents of `${HOME}/.comdex/config/gentx/gentx-XXXXXXXX.json`.
* Fork the [repository](https://github.com/comdex-official/networks/)
* Create a file `gentx-{{VALIDATOR_NAME}}.json` under the testnet/comdex-test-1/gentxs folder in the forked repo, paste the copied text into the file. Find reference file gentx-examplexxxxxxxx.json in the same folder.
* Run `comdex tendermint show-node-id` and copy your nodeID.
* Run `ifconfig` or `curl ipinfo.io/ip` and copy your publicly reachable IP address.
* Create a file `peers-{{VALIDATOR_NAME}}.json` under the testnet/comdex-test-1/peers folder in the forked repo, paste the copied text from the last two steps into the file. Find reference file peers-examplexxxxxxxx.json in the same folder.
* Create a Pull Request to the `main` branch of the [repository](https://github.com/comdex-official/networks)
>**NOTE:** The Pull Request will be merged by the maintainers to confirm the inclusion of the validator at the genesis. The final genesis file will be published under the file testnet/comdex-test-1/final_genesis.json.
* Replace the contents of your `${HOME}/.comdex/config/genesis.json` with that of testnet/comdex-test-1/genesis_final.json.
* Copy below node as `persistent_peers` or `seeds` in `${HOME}/.comdex/config/config.toml`
 
```shell
   TO BE PUBLISHED
```
* Start node
```shell
comdex start
```

### Post genesis

* [Install](#installation-steps) comdex core application
* Initialize node
```shell
comdex init {{NODE_NAME}}
```
* Replace the contents of your `${HOME}/.comdex/config/genesis.json` with that of testnet/comdex-test-1/genesis.json from the `main` branch of [repository](https://github.com/comdex-official/networks).
* Copy below node as `persistent_peers` or `seeds` in `${HOME}/.comdex/config/config.toml`
```shell
   TO BE PUBLISHED
```
* Start node
```shell
comdex start
```
* Acquire $CMDX by sending a message to the developers channel in [Discord](https://discord.gg/gH6RTrnexk).
* Run `comdex tendermint show-validator` and copy your consensus public key.
* Send a create-validator transaction
```
comdex tx staking create-validator \
--from {{KEY_NAME}} \
--amount XXXXXXXXucmdx \
--pubkey comdexvalconspubXXXXXXXX
--chain-id comdex-test-1 \
--moniker="{{VALIDATOR_NAME}}" \
--commission-max-change-rate=0.01 \
--commission-max-rate=1.0 \
--commission-rate=0.07 \
--min-self-delegation="1" \
--details="XXXXXXXX" \
--security-contact="XXXXXXXX" \
--website="XXXXXXXX"
```
## Version
This chain is currently running on Comdex [v0.0.1](https://github.com/comdex-official/comdex/releases/tag/v0.0.1)
Commit Hash: 92b28a8fa64d2b05e80456a8718d6b5ca516c999
>Note: If your node is running on an older version of the application, please update it to this version at the earliest to avoid being exposed to security vulnerabilities /defects.

## Binary
The binary can be downloaded from [here](https://github.com/comdex-official/comdex/releases/tag/v0.0.1).

## Explorer
The explorer for this chain is hosted [here](::To be published)

## Genesis Time
The genesis transactions sent before 1200HRS UTC 15th October 2021 will be used to publish the final_genesis.json at 1400HRS UTC 15th October 2021. 
