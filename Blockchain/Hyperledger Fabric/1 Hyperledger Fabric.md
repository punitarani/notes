# Hyperledger Fabric

Hyperledger Fabric is an open-source platform for building decentralized, blockchain-based applications and networks, hosted by the Linux Foundation.
It provides a modular architecture with a high degree of configurability and a consensus mechanism for ordering transactions.
Fabric allows for the creation of private, permissioned networks with a restricted membership, and supports smart contract execution, known as Chaincode.

## Background on Blockchain

Blockchain is a shared and replicated transaction system
that is updated using smart contracts
and consistently synchronized through a consensus mechanism.

### Distributed Ledger

- Records all transactions that occur in the network.
- Decentralized and distributed across many network participants.
- Each participant contributes to maintaining the ledger.
- Data is append-only, immutable and cryptographically secured.

### Smart Contracts

- Logic for transactions on the network.
- Provides controlled access to the ledger.
- Allow for the automation of complex processes.
- Encapsulate information and simplify interactions with the ledger.

### Consensus

- Process of synchronizing ledger transactions across the network.
- Ensure that only approved transactions are committed to the ledger.

## [Applications of Blockchain](../0%20Blockchain.md#applications-of-blockchain)

## Hyperledger Fabric Summary

- Private and Permissioned Blockchain.
- Participants are enrolled through a trusted Membership Service Provider (MSP).
- Pluggable everything: storage formats, consensus mechanisms, MSPs.
- Channels can be used to isolate transactions within a network.
  - Create network of networks.
- Shared ledger has 2 components: World State and Transaction Log.
  - World State: Current state of the ledger. The database of the ledger.
  - Transaction Log: History of all transactions for the world state.
  - Default storage is LevelDB (key-value store).
- Smart contracts are written in Chaincode and invoked by the client application.
  - Chaincode mostly interacts with the world state not the transaction log.
  - Chaincode can be written in Go, Node.js, and Java.
- Consensus has to be FIFO and supports pluggable consensus mechanisms.
