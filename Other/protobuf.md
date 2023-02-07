# Protocol Buffers (protobuf)

- Data serialization format
- Small, fast, binary format
- Language and platform neutral

## General Notes

- Ideal for data up to a few MBs. It is still possible to use protobuf for larger data, but it is not recommended.
- Suitable for both ephemeral network traffic and long-term data storage.
- Supports backwards compatibility and easy evolution of data structures.

### Use Cases

#### Ideal

Structured, record-like, typed data.

- JSON-like data
- Database records
- API requests/responses

#### Not Ideal

- If the data is more than a few MBs, it is not recommended to use protobuf.
  - Can cause spikes in memory usage.
- Cannot compare protobufs without deserializing them.
  - Same data can have different binary serializations.
- Messages are not compressed by default.
  - It is possible to zip/gzip the data before converting it to protobuf.
- Not the most efficient for multi-dimensional arrays of floats.
  - Alternatives: [FITS](https://en.wikipedia.org/wiki/FITS)
- Not well supported in non-OO languages
- Not self-describing or human-readable
  - Requires a `.proto` file to deserialize the data.
- Not a format standard of any organization

![Protocol Buffers workflow](https://developers.google.com/static/protocol-buffers/docs/images/protocol-buffers-concepts.png)

## FAQ

- What is protobuf reflection?
  - Enables introspection and manipulation of protobuf messages at runtime.
  - Allows for dynamic creation, modification, and processing of messages.
  - Does not require pre-generated code or predefined message types.

---

Source: [Protocol Buffers](https://developers.google.com/protocol-buffers)
