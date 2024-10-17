## Interstate

Interstate is a proposer commitment network that sits on top of Flashbots / MEV Boost. It next to nothing for the validator to run, adds next to no additional slash risk, and generates up to 2x additional block rewards on top of MEV-Boost.

We are a sidecar that auctions off the transaction inclusion rights to users that seek to buy preconfirmations, and apps that seek to buy blockspace for blockspace futures.

Have an ethereum validator running and run our sidecar as well to begin earning rewards.

## EL/CL/VL nodes

Interstate is running on its private network at this moment. To run interstate sidecar, you need to spin up the EL/CL/VC nodes on your machine.
https://github.com/interstate-labs/interstate-testnet/tree/main/network-configs
This is the network-configs setup for the private network.

### Spin up nodes with eth-docker
You can spin up EL/CL/VC nodes with [eth-docker](https://github.com/eth-educators/eth-docker).

#### Clone the eth-docker repo
Just clone the eth-docker with the following command.
```bash
https://github.com/eth-educators/eth-docker
```
Inside the eth-docker folder, install the required apps.
```bash
./ethd install
```

#### Config the eth-docker
Use the following command to enter to the ethd config setup screen.
```bash
./ethd config
```
1. Select the **Custom Testnet** for **Select the Network** step.
2. Use the following network-configs for the following form.
https://github.com/interstate-labs/interstate-testnet/tree/main/network-configs.
3. Select **Ethereum Nodes** for the next step.
4. Select **Geth** and **lighthouse** for EL and CL node types.
5. Select other settings

#### Spin up the nodes
Use the following command to spin up the nodes.
```bash
./ethd up
```

### Register Validators
Get 32 eth.
And here's a guide to register validators for a custom testnet.
https://parithosh.com/2021/06/09/2021-09-06-eth2-deposits/

> TIP: You can use the following secret values for the current testnet.
```
DEPOSIT_AMOUNT=32000000000
FORK_VERSION="0x10000038"
DEPOSIT_CONTRACT_ADDRESS="0x4242424242424242424242424242424242424242"
FORCE_DEPOSIT=true
```

Also in the exec_deposit script, you should replace `--network$ETH1_NETWORK with --connection=http://162.55.190.235:35245`
After deposit the test ETHs for validator, you can generate the keystores using the following command.
```
eth2-val-tools keystores --source-mnemonic "$VALIDATORS_MNEMONIC" --insecure --source-min $ACC_START_INDEX --source-max $ACC_END_INDEX
```
This will create `assigned_data` directory which holds `keys` and `secrets` folder.
You should copy these two folders inside `[eth-docker folder path]/.eth/validator_keys` and run `ethd keys import` to import keys for ethd validator instance.

## Docker

Interstate provides maintained Docker images for the Interstate sidecar.<br>
Running the sidecar includes several steps. This is a high level overview, the steps are provided below:
1. Set the environment variables
  - Update the `cb-config.toml` file
  - Update `launch.env` file
2. Run the interstate-sidecar
  - Start the interstate-sidecar service

Let's see one by one

### Set the environment variables

#### 1) Update `cb-config.toml` file for commit-boost
Before running the sidecar service, we need to update this file with our own settings.

- Get the genesis time of beacon node by using the api follow
` beacon_url/eth/v1/beacon/genesis `
- Update `genesis_time_sec` in `cb-config.toml` file
You can keep the remaining config settings.

#### 2) Update `launch.env` file for interstate-sidecar
The `launch.env` file is the place where all the environment variables for the sidecar are placed.
```bash
# Prepopulated with the setup for eth-docker: https://github.com/eth-educators/eth-docker. You will have to change this if you setup a different way.

# Beacon client API
BEACON_API_URL="http://consensus:5052"  # eth-docker-consensus-1 (Port 9000)

# Execution client API
EXECUTION_API_URL="http://execution:8545"  # eth-docker-execution-1 (Port 8545, assuming it's the JSON-RPC API)

# Engine API
ENGINE_API_URL="http://execution:8551"  # eth-docker-execution-1 (Port 8545, assuming it's also the engine API)

# Engine API JWT
JWT_HEX="0x8d584b6fda83df471979118a63494d61ffd7084a149b33be3e0ab8ea92fb4bc9"  # To generate the JWT token run: openssl rand -hex 32 | tr -d "\n" > jwtsecret

# Fee recipient
FEE_RECIPIENT="0x675Fd297A916874d5518CC335f28b7a529A7c3Ac"  # Provide your Ethereum address for receiving fees

# The Interstate RPC port. This port must be exposed!
INTERSTATE_RPC_PORT="9061"  # interstate-boost (Port 9061)

# BLS commitment signing key
SIGNING_KEY="0x00bc72598d6ba483ec5aad004e1f7a59121f1a210bb26efe3d682e37e941c475"  # Provide the appropriate BLS key

# The validator indexes for which to accept commitments. Can be specified as a range i.e. "1..96" (includes 96)
VALIDATOR_INDEXES="64..79"  # Provide your validator indexes

# Genesis fork version for Interstate
GENESIS_FORK_VERSION="0x10000038"

```
You should update these fields with your own settings.

### Run the interstate-sidecar and commit-boost

#### Start the interstate-sidecar and commit-boost services

We already prepared the docker-compose.yml file which can be used to start the sidecar.
Run the following command:
```bash
docker compose up
```
