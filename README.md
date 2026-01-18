# FilterDSL

## Overview

FilterDSL is a transport-agnostic domain-specific language for expressing complex filter criteria as a shared contract between clients and APIs. It defines syntax and semantics only, independent of HTTP, WebSockets, or execution, enabling validation, reuse, and translation across systems.

FDSL defines **only the filter syntax and semantics** and does not attempt to enforce transport (HTTP GET/POST, WebSockets, etc.) or execution (SQL, NoSQL, search engines).

### Goals

- Shared, versionable filter contract
- Deterministic and composable syntax
- Transport- and implementation-neutral
- Easy to validate and translate

### Non-goals

- No transport handling
- No query execution
- No persistence layer

### Desired use case

This contract is intended to be used as a specification for client–server systems, allowing clients to send complex filter queries and servers to validate and fulfill them, independently of the languages in which each is implemented.

### Status

Early-stage. API and syntax may evolve.

### License

[MIT](./LICENSE)

## Usage

### Sections

- [Operators](./v1/operators.md)
- [Operations](./v1/operations.md)
  - [Kind](./v1/kind.md)
- [Queries](./v1/queries.md)
