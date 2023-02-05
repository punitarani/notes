# InterPlanetary File System

- IPFS is a decentralized, distributed file system.
- It aims to replace traditional methods of accessing and sharing data, such as HTTP.
- It uses a content-addressable file system, where files are referenced by their cryptographic hash.
- This makes IPFS resistant to censorship and data loss.
- IPFS enables the creation of a permanent, decentralized web.
- Content can be easily accessed and shared by anyone, anywhere.

## How IPFS Works

### File Storage

1. File is split into chunks.
   - Each chunk is cryptographically hashed.
   - Each chunk is given a Content Identifier (CID).
     - CID is a permanent record of that chunk.
2. Chunks are stored in a distributed network.
   - Chunks are stored on the closest peer to the chunk.
   - Chunks are stored redundantly on multiple peers.
3. The DHT is updated with the CID and the location of the chunks.

### File Retrieval

1. File is requested by CID.
   - Looks for the file in its local storage (cache).
   - A list of peers is retrieved from the DHT.
   - File is requested from the closest peer.
   - File is cached locally and becomes a provider.

## FAQ

- Free?
  - Open-source software. Can be used freely by anyone.
  - No licensing fees or costs associated with using IPFS.
  - Running an IPFS node or using IPFS services may incur costs.
