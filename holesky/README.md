## Prerequisites

Ensure you have a running beacon client on your machine. Depending on the installation method, you may need to install additional dependencies.

Please note that Interstate supports **Holesky** network at this moment.

## Docker

Interstate provides maintained Docker images for the Interstate sidecar.

1. [Install the Docker Engine](https://docs.docker.com/engine/install/)
2. [Install the Docker Compose](https://docs.docker.com/compose/install/)
3. Copy the [Docker Compose configuration](https://github.com/interstate-labs/preconf-network/blob/main/validator-operator-setup/holesky/docker-compose.yml) in a directory of your choice.
4. In the same directory, copy the [launch.env](https://github.com/interstate-labs/preconf-network/blob/main/validator-operator-setup/holesky/launch.env) file and fill in the required environment variables.
  - Set generated JWT key.
    - Copy the content of JWT secret key file which were generated for running beacon node client.
    - Update the field `JWT_HEX` with the key data.
  - Enter BLS key.
    For the `SIGNING_KEY` field in `launch.env` file, you can list your BLS commit signing key.
  - Update API env variables

Then, in the same directory, run the following command:
```bash
docker compose up
```
