# Docker Compose Bitcoin

This is my personal compose for composing a bitcoin node, electrum server, and lightning server.

# Config

The `.env` file contains variables that are substitutions in the `docker-compose.yaml` via statments like `${variable-name}`. The `.env` file is loaded by default by docker-compose and should not be checked into source control, i.e. `.gitignore`.

# Starting
Starting requires `docker-compose`, and can be installed via `apt`. To start the containers:

```bash
docker-compose up -d
```

# Stopping
Stopping the containers does not erase the volumes which is good. To stop all the containers:

```bash
docker-compose down
```

To stop a single container, first gets it's name from the `docker-compose.yaml` file. For example, this stops the electrumx container

```bash
docker-compose stop electrumx
```

# Volumes
Each service has filesystem state that is mapped to a docker volume. Volumnes can be listed after containers are up and running for the first time:

```bash
docker volume ls
```

To access a volume, use docker to inspect its mount point on the local filesystem, which shows where it's mounted. See variable `Mountpoint` in the output from the command below:

```bash
docker inspect compose-bitcoin_bitcoind
```

# Logs
Logs can be viewed for one container at a time. To list all containers:

```bash
docker ps -a
```

To get logs from a container:

```bash
docker logs compose-bitcoin_bitcoind_1
```

To follolw logs from a container:

```bash
docker logs -f compose-bitcoin_bitcoind_1
```
