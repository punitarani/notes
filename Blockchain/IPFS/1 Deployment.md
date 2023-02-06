# Deploying IPFS

## Private IPFS Network

**System**: Raspberry Pi 4 4GB

**OS**: Ubuntu Server 22.04.1 64-bit

```bash
cd ~
mkdir ipfs
cd ipfs
```

### IPFS Installation

1. Download the [IPFS Kubo Docker Image](https://hub.docker.com/r/ipfs/kubo/).

   ```bash
   docker pull ipfs/kubo
   ```

2. Create the data and staging directories.

   ```bash
   mkdir data
   mkdir staging
   ```

   ```bash
   export ipfs_data=~/ipfs/data
   export ipfs_staging=~/ipfs/staging
   ```

3. Start a Private IPFS Container

   It is critical to include one of the following params:

   - `IPFS_SWARM_KEY`: This is the swarm key used to encrypt the IPFS network.
   - `IPFS_SWARM_KEY_FILE`: This is the path to the file containing the swarm key to use.

   `IPFS_SWARM_KEY_FILE` is the preferred method, as it allows the swarm key to be stored in a secure location.

   Use the following command to generate a random swarm key:

   ```bash
   openssl rand -hex 32 > swarm.key
   ```

   Use the following command to start the IPFS container:

   ```bash
   docker run -d --name ipfs_host -e IPFS_SWARM_KEY_FILE="~/ipfs/swarm.key" -v $ipfs_staging:/export -v $ipfs_data:/data/ipfs -p 4001:4001 -p 4001:4001/udp -p 127.0.0.1:8080:8080 -p 127.0.0.1:5001:5001 ipfs/kubo:latest
   ```

   If the IPFS container does not need to be private, use the following command:

   ```bash
   docker run -d --name ipfs_host -v $ipfs_staging:/export -v $ipfs_data:/data/ipfs -p 4001:4001 -p 4001:4001/udp -p 127.0.0.1:8080:8080 -p 127.0.0.1:5001:5001 ipfs/kubo:latest
   ```

   - `docker run`: This is the command to run a new Docker container.
   - `-d`: This flag runs the container in the background (i.e., as a daemon).
   - `--name ipfs_host`: This flag gives the container a name `ipfs_host`.
   - `-v $ipfs_staging:/export`: This flag mounts a volume from the host to the container, using the host path specified in the $ipfs_staging environment variable and mapping it to the `/export` directory in the container.
   - `-v $ipfs_data:/data/ipfs`: This flag also mounts a volume, with the host path specified in the `$ipfs_data` environment variable, to the `/data/ipfs` directory in the container.
   - `-p 4001:4001`: This flag maps port `4001` on the host to port `4001` in the container, allowing access to IPFS API.
   - `-p 4001:4001/udp`: This flag maps the UDP version of port `4001` on the host to port `4001` in the container, allowing access to IPFS API over UDP.
   - `-p 127.0.0.1:8080:8080`: This flag maps port `8080` on the host's loopback interface (i.e., `127.0.0.1`) to port `8080` in the container, allowing access to IPFS Gateway.
   - `-p 127.0.0.1:5001:5001`: This flag maps port `5001` on the host's loopback interface to port `5001` in the container, allowing access to IPFS Swarm.
   - `ipfs/kubo:latest`: This is the image name and tag used to run the container. It specifies to run the latest version of the `ipfs/kubo` image.

4. Watch the logs and wait for IPFS to start.

   ```bash
    docker logs -f ipfs_host
   ```

   - `docker logs`: This command is used to view the logs of a container.
   - `-f`: This flag follows the logs, so you can see the container start.

   ```bash
   Gateway (readonly) server listening on /ip4/0.0.0.0/tcp/8080
   ```

5. Run IPFS commands with `docker exec ipfs_host ipfs <args...>`

   - Test by adding a file to IPFS.

     ```bash
     echo "Hello World!" > "$ipfs_staging/hello_world"
     docker exec ipfs_host ipfs add -r /export/hello_world
     ```

     Output:

     ```bash
     added QmfM2r8seH2GiRaC4esTjeraXEachRt8ZsSeGaWTPLyMoG hello_world
     ```

   - Check the file was added to IPFS.

     ```bash
     docker exec ipfs_host ipfs cat /ipfs/QmfM2r8seH2GiRaC4esTjeraXEachRt8ZsSeGaWTPLyMoG
     ```

     Output:

     ```bash
     Hello World!
     ```

6. Stop the IPFS container.

   ```bash
   docker stop ipfs_host
   ```

   Use this to restart the container:

   ```bash
   docker start ipfs_host
   ```

---

Files:

- `hello_world`: `QmfM2r8seH2GiRaC4esTjeraXEachRt8ZsSeGaWTPLyMoG`
- `printing_greetings`: `Qmdbd9iBHSKM3SQ9G849YBiczsbPUGUu3pNPgZnigs8Cb5`

---

Source: [IPFS Kubo Documentation](https://docs.ipfs.tech/install/run-ipfs-inside-docker/)
