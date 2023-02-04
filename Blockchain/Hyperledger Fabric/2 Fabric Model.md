# Hyperledger Fabric Model

## Assets

- Assets are the things that are being transacted on the network.
  - Can be tangible (real estate and hardware) to the intangible (contracts and intellectual property).
- Represented as key-value pairs. Can be binary and/or JSON.
- State changes recorded as transactions on a Channel ledger.

## Chaincode

- Business logic that governs the assets on the network.
- Rules for modifying data on the ledger.

1. Initialized through a transaction proposal.
2. Executed against the ledger's current state.
3. Results in a write set (key-value pairs) that is submitted to the network.

## Ledger Features

- Ledger is composed of:
  1. World State: state database to maintain current fabric state
  2. Transaction Log: blocks of immutable and sequenced records of transactions.
- Sequenced, tamper-resistant and cryptographically verifiable state transitions.
- Each transaction is committed as: create, update or delete.

Features:

- Query and Update ledger using key-based lookups, range and composite key queries.
- Read-only queries using a rich query language (RQL) (if using CouchDB as state db).
- Read-only history queries: query history for a key, enabling data provenance cases.

- Transactions consist of versions of:
  - Read set: KVP that were read by the chaincode.
  - Write set: KVP that were written by the chaincode.
- Transactions contain signatures of every endorsing peer before submission to the ordering service.
- Transactions are ordered into blocks are delivered to peers on a channel by the ordering service.

- Peers validate transactions and enforce endorsement policies.
- Versioning check is performed before appending a block.
  - Ensures that the state for assets have not changed since chaincode execution.
- Once a transaction is validated and committed, it is immutable.
- Channel's ledger contains a configuration block defining:
  - Policies
  - Access Control Lists
  - Other pertinent information
- Channels contain MSP instances allowing for crypto materials to be derived from different CAs.

Read More: [Ledger](https://hyperledger-fabric.readthedocs.io/en/latest/ledger/ledger.html)

## Privacy

- Ledger exists ona per-channel basis
  - Can be shared across entire network, or privatized to select participants.
- Chaincode can be installed on peers that need access to specific asset states.
  - If chaincode is not installed on a peer, it cannot interface with the ledger.
- Collection is used to segregate data in a private database.
  - Logically separate from the channel ledger
  - Accessible only to the authorized subset of organizations.
- Network -> Channel -> Collection.

- Data within chaincode can be encryption (partial or full).
  - Use any common cryptographic algorithm before sending transaction to ordering service.
  - Once encrypted data is written to the ledger, it can only be decrypted by authorized parties.

Read More: [Private Data](https://hyperledger-fabric.readthedocs.io/en/latest/private-data-arch.html)

## Security & Membership Services

Read More: [Security Model](https://hyperledger-fabric.readthedocs.io/en/latest/security_model.html)

## Consensus

- Full-circle verification of the correctness of a set of transactions comprising a block.
  - More than just a specific algorithm within a specific function.
  - It is the byproduct of the ongoing verification throughout a transaction's lifecycle.
- Critical throughout the entire transaction flow.
  - From proposal and endorsement to ordering, validation and commitment.
- Consensus is achieved after the order and results of a transactions have met the endorsement policies.
  - Prior to commitment, peers use system chaincodes to ensure endorsements and permissions of entities.
  - Versioning check is performed before appending a block.
    - Ensures that the state for assets have not changed since chaincode execution.
  - Final check to protect against double spending.
    - Prevent data integrity compromise. Allow functions execution against non-static variables.
- Access control lists are implemented on hierarchical layers of the network
  - From ordering service down to channels.

Read More: [Transaction Flow](https://hyperledger-fabric.readthedocs.io/en/latest/txflow.html)

---

_Source: [Hyperledger Fabric Documentation](https://hyperledger-fabric.readthedocs.io/en/latest/)_
