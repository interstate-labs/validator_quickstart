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
There are pre-funded accounts which holds test ETH of the network to use for validator registration.
```
[
    (
        "0x8943545177806ED17B9F23F0a21ee5948eCaa776",
        "bcdf20249abf0ed6d944c0288fad489e33f66b3960d9e6229c1cd214ed3bbe31",
    ),
    (
        "0xE25583099BA105D9ec0A67f5Ae86D90e50036425",
        "39725efee3fb28614de3bacaffe4cc4bd8c436257e2c8bb887c4b5c4be45e76d",
    ),
    (
        "0x614561D2d143621E126e87831AEF287678B442b8",
        "53321db7c1e331d93a11a41d16f004d7ff63972ec8ec7c25db329728ceeb1710",
    ),
    (
        "0xf93Ee4Cf8c6c40b329b0c0626F28333c132CF241",
        "ab63b23eb7941c1251757e24b3d2350d2bc05c3c388d06f8fe6feafefb1e8c70",
    ),
    (
        "0x802dCbE1B1A97554B4F50DB5119E37E8e7336417",
        "5d2344259f42259f82d2c140aa66102ba89b57b4883ee441a8b312622bd42491",
    ),
    (
        "0xAe95d8DA9244C37CaC0a3e16BA966a8e852Bb6D6",
        "27515f805127bebad2fb9b183508bdacb8c763da16f54e0678b16e8f28ef3fff",
    ),
    (
        "0x2c57d1CFC6d5f8E4182a56b4cf75421472eBAEa4",
        "7ff1a4c1d57e5e784d327c4c7651e952350bc271f156afb3d00d20f5ef924856",
    ),
    (
        "0x741bFE4802cE1C4b5b00F9Df2F5f179A1C89171A",
        "3a91003acaf4c21b3953d94fa4a6db694fa69e5242b2e37be05dd82761058899",
    ),
    (
        "0xc3913d4D8bAb4914328651C2EAE817C8b78E1f4c",
        "bb1d0f125b4fb2bb173c318cdead45468474ca71474e2247776b2b4c0fa2d3f5",
    ),
    (
        "0x65D08a056c17Ae13370565B04cF77D2AfA1cB9FA",
        "850643a0224065ecce3882673c21f56bcf6eef86274cc21cadff15930b59fc8c",
    ),
    (
        "0x3e95dFbBaF6B348396E6674C7871546dCC568e56",
        "94eb3102993b41ec55c241060f47daa0f6372e2e3ad7e91612ae36c364042e44",
    ),
    (
        "0x5918b2e647464d4743601a865753e64C8059Dc4F",
        "daf15504c22a352648a71ef2926334fe040ac1d5005019e09f6c979808024dc7",
    ),
    (
        "0x589A698b7b7dA0Bec545177D3963A2741105C7C9",
        "eaba42282ad33c8ef2524f07277c03a776d98ae19f581990ce75becb7cfa1c23",
    ),
    (
        "0x4d1CB4eB7969f8806E2CaAc0cbbB71f88C8ec413",
        "3fd98b5187bf6526734efaa644ffbb4e3670d66f5d0268ce0323ec09124bff61",
    ),
    (
        "0xF5504cE2BcC52614F121aff9b93b2001d92715CA",
        "5288e2f440c7f0cb61a9be8afdeb4295f786383f96f5e35eb0c94ef103996b64",
    ),
    (
        "0xF61E98E7D47aB884C244E39E031978E33162ff4b",
        "f296c7802555da2a5a662be70e078cbd38b44f96f8615ae529da41122ce8db05",
    ),
    (
        "0xf1424826861ffbbD25405F5145B5E50d0F1bFc90",
        "bf3beef3bd999ba9f2451e06936f0423cd62b815c9233dd3bc90f7e02a1e8673",
    ),
    (
        "0xfDCe42116f541fc8f7b0776e2B30832bD5621C85",
        "6ecadc396415970e91293726c3f5775225440ea0844ae5616135fd10d66b5954",
    ),
    (
        "0xD9211042f35968820A3407ac3d80C725f8F75c14",
        "a492823c3e193d6c595f37a18e3c06650cf4c74558cc818b16130b293716106f",
    ),
    (
        "0xD8F3183DEF51A987222D845be228e0Bbb932C222",
        "c5114526e042343c6d1899cad05e1c00ba588314de9b96929914ee0df18d46b2",
    ),
    (
        "0xafF0CA253b97e54440965855cec0A8a2E2399896",
        "4b9f63ecf84210c5366c66d68fa1f5da1fa4f634fad6dfc86178e4d79ff9e59",
    ),
]
```
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
