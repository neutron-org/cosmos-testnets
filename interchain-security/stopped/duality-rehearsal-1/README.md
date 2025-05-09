
# `duality` Chain Details

The `duality-rehearsal-1` chain will be launched as a Neutron persistent chain to test Interchain Security functionality.

* **Chain-ID**: `duality-rehearsal-1`
* **minimum-gas-prices**: ``
* **timeout_commit**: `2s`
* **Spawn time**: `2023-05-31T15:00:00Z`
* **GitHub repo**: [duality-labs/duality](https://github.com/duality-labs/duality.git)
* **Release**: [`v0.2.2`](https://github.com/duality-labs/duality/releases/tag/v0.2.2)
<!-- * **Genesis file with CCV state:** [duality-rehearsal-1-genesis.json](duality-rehearsal-1-genesis.json) -->

* **Reference binary**: [dualityd-linux-amd64](./dualityd-linux-amd64)
* **Binary sha256sum**: `054b8cf641d7e9877048896ebe08343c1e95f6a8e7c3a0be044b91401f558099`
* **Genesis file _without CCV state_:** [duality-rehearsal-1-genesis-without-ccv.json](duality-rehearsal-1-genesis-without-ccv.json), verify with `shasum -a 256 duality-rehearsal-1-genesis-without-ccv.json`
* **SHA256 for genesis file _without CCV state_**: `b569f67ecf0611e490cac7eb2e3b8343a959e63b54fa7a46cc5dd2bd6e27f85f`


* Genesis file hash
  * The SHA256 is used to verify against the genesis file (without CCV state) that the proposer has made available for review.
  * The `duality-rehearsal-1-genesis-without-ccv.json` file cannot be used to run the chain: it must be updated with the CCV (Cross Chain Validation) state after the spawn time is reached.
  * The genesis file includes funds for a relayer and a faucet account as well as account with funds for different internal needs, `signed_blocks_window` has been set to `864000`, and `min_signed_per_window` has been set to `5%`.
* Binary hash
  * The `dualityd-linux-amd64` binary is only provided to verify the SHA256. It was built with Interchain Security release [`v1.2.0-multiden`](https://github.com/cosmos/interchain-security/releases/tag/v1.2.0-multiden). You can generate the binary following the build instructions in that repo or using one of the scripts provided here.
* Spawn time
  * Even if a proposal passes, the CCV state will not be available from the provider chain until after the spawn time is reached.

> If you want to build genesis by your own please take into account difference between the `ccvconsumer` section generated by version v9.0.2 of `gaiad` and the `ccvconsumer` section required for duality to run. Please check and add `"soft_opt_out_threshold": "0.05"` to the `params` section if it absent.

For more information regarding the consumer chain creation process, see [CCV: Overview and Basic Concepts](https://github.com/cosmos/ibc/blob/main/spec/app/ics-028-cross-chain-validation/overview_and_basic_concepts.md).

## Endpoints

Endpoints are exposed as subdomains for the sentry and snapshot nodes (described below) as follows:

- `https://rpc.testnet-1.duality.xyz`
- `https://grpc.testnet-1.duality.xyz`
- `https://rest.testnet-1.duality.xyz` (or `https://lcd.testnet-1.duality.xyz`)

Seed nodes:
1. `75546756a3d3189594ebce101700605c1e956053@p2p.testnet-1.duality.xyz:26656`

## IBC Data

### Clients

* `07-tendermint-0`
  * Counterparty: [`provider`](/interchain-security/provider/README.md) `07-tendermint-14`

### Connections

* `connection-0`
  * Counterparty: [`provider`](/interchain-security/provider/README.md) `connection-10`

### Channels

* `channel-0`: consumer port
  * Counterparty: [`provider`](/interchain-security/provider/README.md) `channel-17`
* `channel-1`: transfer port
  * Counterparty: [`provider`](/interchain-security/provider/README.md) `channel-18`

## How to Join

### Hardware Requirements

* 4 Cores
* 32 GB RAM
* 2x512 GB SSD

### Software Versions

| Name               | Version  |
|--------------------|----------|
| Duality            | v0.2.2   |
| Go                 | v1.18.5  |

The scripts provided in this repo will install Duality and set up a Cosmovisor service with the auto-download feature enabled on your machine.

#### Bash Script

The script provided in this repo will install `dualityd` and set up a Cosmovisor service on your machine. 

Run script provided to set up a `duality-rehearsal-1` service:
* `join-rs-duality-rehearsal-1.sh` will create a `duality-rehearsal-1` service with `cosmovisor` support.
* Script must be run either as root or from a sudoer account.
* Script will attempt to build a binary from the [duality-labs/duality] repo.

### Node manual installation

Build and install the `dualityd` binary. 

```
$ git clone -b v0.2.2 https://github.com/duality-labs/duality.git
$ cd duality
$ make install
```

after installation please check installed version by running:

`dualityd version --long`

You should see the following:
```
name: Duality
server_name: dualityd
version: 0.2.2
commit: 98fc9734cfe79bf56015d630219d4ed30b02ae72
``` 
