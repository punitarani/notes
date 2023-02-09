# Getting Started with Hyperledger Fabric

## Installation on Raspberry Pi 4

**System**: Raspberry Pi 4 4GB
**OS**: Ubuntu Server 22.04.1 64-bit

### Prerequisites

[Hyperledger Fabric Docs](https://hyperledger-fabric.readthedocs.io/en/release-2.5/prereqs.html)

```bash
sudo apt-get -y install git curl docker-compose
```

#### Docker

Start Docker daemon and enable it to start when system starts

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

#### Go

[Go Downloads](https://go.dev/dl/)

```bash
cd ~
curl -OL https://go.dev/dl/go1.20.linux-arm64.tar.gz
sudo tar -C /usr/local -xvf go1.20.linux-arm64.tar.gz
```

```bash
sudo nano ~/.profile
```

Add the following to the end of the file:

`export PATH=$PATH:/usr/local/go/bin`

```bash
source ~/.profile
```

### Fabric and Fabric Samples

[Fabric Test Network](https://hyperledger-fabric.readthedocs.io/en/release-2.5/test_network.html)

```bash
mkdir -p $HOME/go/src/github.com/punitarani
cd $HOME/go/src/github.com/punitarani
curl -sSLO https://raw.githubusercontent.com/hyperledger/fabric/main/scripts/install-fabric.sh && chmod +x install-fabric.sh
sudo ./install-fabric.sh d s 
```

This will install the following:

- `docker` to use Docker to download the Fabric Container Image
- `samples` to clone the fabric-samples github repo to the current directory

The following will not be installed:

- `binaries`: Fabric Binaries
- `podman`: Podman Fabric Container Image

#### Run Fabric (Test Network)

```bash
cd fabric-samples/test-network
sudo ./network.sh down
sudo ./network.sh up
```

##### Troubleshooting

```bash
./network.sh up
Using docker and docker-compose
Starting nodes with CLI timeout of '5' tries and CLI delay of '3' seconds and using database 'leveldb' with crypto from 'cryptogen'
Peer binary and configuration files not found..

Follow the instructions in the Fabric docs to install the Fabric Binaries:
https://hyperledger-fabric.readthedocs.io/en/latest/install.html
```

**Cause**: Issue installing Fabric Binaries

Tried on both 32-bit and 64-bit Ubuntu Server 22.04

**Learned that Hyperledger Fabric is not natively compatible with Raspberry Pi, or specifically ARM64.**
