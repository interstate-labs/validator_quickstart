## Interstate

Interstate is a proposer commitment network that sits on top of Flashbots / MEV Boost. It costs next to nothing for the validator to run, adds next to no additional slash risk, and generates additional block rewards on top of MEV-Boost.

We are a sidecar that auctions off the transaction inclusion rights to users that seek to buy preconfirmations, and apps that seek to buy blockspace for blockspace futures.

Have an ethereum validator running and run our sidecar as well to begin earning rewards.

## Prerequisites

Ensure you have a running beacon client on your machine. Depending on the installation method, you may need to install additional dependencies.

Please note that Interstate supports **Holesky** network at this moment.

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

#### 1) Update `cb-config.toml` file
Before running the sidecar service, we need to update this file with our own settings.
```toml
[signer]
[signer.loader]
keys_path = "~/register_validator/assigned_data/keys" # Fixed path to the keys folder to run validator
secrets_path = "~/register_validator/assigned_data/secrets" # Fixed path to the secrets folder to run validator
```
You can keep the remaining config settings.

#### 2) Update `launch.env` file
The `launch.env` file is the place where all the environment variables for the sidecar are placed.
```bash
# Beacon client API
BEACON_API_URL="http://consensus:5052"  # eth-docker-consensus-1 (Port 9000)

# Execution client API
EXECUTION_API_URL="http://execution:8545"  # eth-docker-execution-1 (Port 8545, assuming it's the JSON-RPC API)

# Engine API
ENGINE_API_URL="http://execution:8545"  # eth-docker-execution-1 (Port 8545, assuming it's also the engine API)

# Engine API JWT
JWT_HEX=""  # To generate the JWT token run: openssl rand -hex 32 | tr -d "\n" > jwtsecret

# Fee recipient
FEE_RECIPIENT=""  # Provide your Ethereum address for receiving fees

# ...

# BLS commitment signing key
SIGNING_KEY="put your BLS commitment signing key"  # Provide the appropriate BLS key

# The validator indexes for which to accept commitments. Can be specified as a range i.e. "1..96" (includes 96)
VALIDATOR_INDEXES="put your validator indices"  # Provide your validator indexes

# ...
```
You should update these fields with your own settings.

### Run the interstate-sidecar

#### Start the interstate-sidecar service

We already prepared the docker-compose.yml file which can be used to start the sidecar.
Run the following command:
```bash
docker compose up
```
