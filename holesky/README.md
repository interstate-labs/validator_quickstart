## Prerequisites

Ensure you have a running beacon client on your machine. Depending on the installation method, you may need to install additional dependencies.

Please note that Interstate supports **Holesky** network at this moment.

## Docker

Interstate provides maintained Docker images for the Interstate sidecar.<br>
Running the sidecar includes several steps
1. Run the commit-boost service
  - Update the `cb-config.toml` file
  - Generate `cb.docker-compose.yml` file
  - Run the commit-boost
2. Run the interstate-sidecar

Let's see one by one

### Run the commit-boost service

#### Update `cb-config.toml` file
Before running the commit-boost service, we need to update this file with our own settings.
```toml
[signer]
[signer.loader]
keys_path = "~/register_validator/assigned_data/keys" # Fixed path to the keys folder to run validator
secrets_path = "~/register_validator/assigned_data/secrets" # Fixed path to the secrets folder to run validator
```
You can keep the remaining addresses.

#### Generate `cb.docker-compose.yml` file
Use the following command to generate the `cb.docker-compose.yml` file for the next step.
```bash
./commit-boost init --config cb-config.toml
```

#### Run the commit-boost service
Use the following command to run the commit-boost service
```bash
./commit-boost start --docker cb.docker-compose.yml
```

### Run the interstate-sidecar
We already prepared the docker-compose.yml file which can be used to start the sidecar.
Run the following command:
```bash
docker compose up
```
