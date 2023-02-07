# Protocol Buffers (protobuf)

- Data serialization format
- Small, fast, binary format
- Language and platform neutral

## General Notes

- Ideal for data up to a few MBs. It is still possible to use protobuf for larger data, but it is not recommended.
- Suitable for both ephemeral network traffic and long-term data storage.
- Supports backwards compatibility and easy evolution of data structures.

Code Examples: [github.com/protocolbuffers/protobuf/examples](https://github.com/protocolbuffers/protobuf/tree/main/examples)

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

## `.proto` file

- Describes the structure of a message
- Required for all messages

Unlike JSON or XML, protobuf does not have a built-in way to describe the structure of a message.
Instead, a `.proto` file is used to describe the structure of a message.
This file is then used to generate code for the desired language.

When sending data, it is critical to send the `.proto` file along with the data.
This allows the receiving party to deserialize the data into the correct structure.

Examples:
[`status.proto`](https://github.com/googleapis/googleapis/blob/a4f2de456480c0a4ed9feeeaa1f8ee620bbef23a/google/rpc/status.proto)
[`timestamp.proto`](https://github.com/protocolbuffers/protobuf/blob/e5bbcd20d3623733e8c3d36a427c2800022434e1/src/google/protobuf/timestamp.proto)

### Syntax

```proto
// First non-empty, non-comment line of the file must specify the syntax.
syntax = "proto3";


// package defines the namespace for the generated code.
package mypackage;


// import allows for importing definitions from other files.
// public imports are visible to other files that import this file.
// private imports are only visible to this file.
// public imports usually go first, not required.
import public "dir/other_public.proto";
import "dir/other.proto";

import "google/protobuf/timestamp.proto";


// enum allows for defining a set of named constants.
enum Gender {
    UNKNOWN = 0;
    MALE = 1;
    FEMALE = 2;
}


// message defines a structure.
message Person {
    string name = 1;
    int32 id = 2;
    Gender gender = 3;

    // Nested enum
    enum PhoneType {
        MOBILE = 0;
        HOME = 1;
        WORK = 2;
    }

    // Nested message
    message PhoneNumber {
        string number = 1;
        PhoneType type = 2;
    }

    // repeated field allows for a list of values
    repeated string hobbies = 4;

    // Use a field from another file
    google.protobuf.Timestamp last_updated = 5;
}

// Each .proto file can contain multiple messages.
```

### Data Types (Scalar)

- double
- float
- int32
- int64
- uint32
- uint64
- sint32
- sint64
- fixed32
- fixed64
- sfixed32
- sfixed64,
- bool
- string
- bytes

Read more: [Scalar Value Types](https://developers.google.com/protocol-buffers/docs/proto3#scalar)

## Installation and Usage

### protoc

Check `protoc` installation with `protoc --version`

#### Installing `protoc` on Windows

1. Download the latest release from [github.com/protocolbuffers/protobuf/releases](https://github.com/protocolbuffers/protobuf/releases)
2. Extract the zip file to a directory
    - Ideally, to "C:\Program Files\protoc-<version>-win64"
3. Add the directory to the `PATH` environment variable
    - `C:\Program Files\protoc-<version>-win64\bin`

### Go plugin and package

#### protoc-gen-go

Read more: [Go Tutorial](https://protobuf.dev/getting-started/gotutorial/)

Install Go protobuf plugin:

```bash
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
```

Check that the plugin is installed:

```bash
protoc-gen-go --version
```

#### Go package

```go
import "google.golang.org/protobuf/proto"
```

This is the latest module superseding `github.com/golang/protobuf`.
It has updated and simplified API and support for protobuf reflection.

#### Generate Go code

```bash
protoc -I=<import_dir> --go_out=<output_dir> <proto_file>
```

## FAQ

- What is protobuf reflection?
  - Enables introspection and manipulation of protobuf messages at runtime.
  - Allows for dynamic creation, modification, and processing of messages.
  - Does not require pre-generated code or predefined message types.

---

Source: [Protocol Buffers](https://developers.google.com/protocol-buffers)
