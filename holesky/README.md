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
BEACON_API_URL="http://cl-1-lighthouse-geth:4000"  # eth-docker-consensus-1 (Port 9000)

# Execution client API
EXECUTION_API_URL="http://el-1-geth-lighthouse:8545"  # eth-docker-execution-1 (Port 8545, assuming it's the JSON-RPC API)

# Engine API
ENGINE_API_URL="http://el-1-geth-lighthouse:8551"  # eth-docker-execution-1 (Port 8545, assuming it's also the engine API)

# Engine API JWT
JWT_HEX="0xdc49981516e8e72b401a63e6405495a32dafc3939b5d6d83cc319ac0388bca1b"  # To generate the JWT token run: openssl rand -hex 32 | tr -d "\n" > jwtsecret

# Fee recipient
FEE_RECIPIENT="0x65D08a056c17Ae13370565B04cF77D2AfA1cB9FA"  # Provide your Ethereum address for receiving fees

# The Interstate RPC port. This port must be exposed!
INTERSTATE_RPC_PORT="9061"  # eth-docker-mev-boost-1 (Port 8000)

# BLS commitment signing key
SIGNING_KEY="18d1c5302e734fd6fbfaa51828d42c4c6d3cbe020c42bab7dd15a2799cf00b82"  # Provide the appropriate BLS key

# The validator indexes for which to accept commitments. Can be specified as a range i.e. "1..96" (includes 96)
VALIDATOR_INDEXES="0..63"  # Provide your validator indexes

# Genesis fork version for Interstate
GENESIS_FORK_VERSION="0x10000038"

# Log
RUST_LOG="bolt_sidecar=trace"

```
You should update these fields with your own settings.

### Run the interstate-sidecar and commit-boost

#### Start the interstate-sidecar and commit-boost services

We already prepared the docker-compose.yml file which can be used to start the sidecar.
Run the following command:
```bash
docker compose up
```
