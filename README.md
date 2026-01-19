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

### Examples

These examples use JSON to represent a FilterDSL numeric operation. Any serializable format can be used to represent the operation, as long as it adheres to the FilterDSL specification.

Let's look for **elements where the age is between 30 and 40, and the name is "John"**

```json
{
  "operations": {
    "0": {
      "kind": "Range",
      "field": "age",
      "operator": "bt",
      "operand": {
        "from": 30,
        "to": 40
      }
    },
    "1": {
      "kind": "String",
      "field": "name",
      "operator": "eq",
      "operand": "John"
    }
  },
  "meta": {
    "count": 2,
    "version": "1.0"
  }
}
```

Or we can search for **elements where the age is greater than 25, and the name is "Jane" or "John"**

```json
{
  "operations": {
    "0": {
      "kind": "Numeric",
      "field": "age",
      "operator": "gt",
      "operand": 25
    },
    "1": {
      "kind": "String",
      "field": "name",
      "operator": "eq",
      "operand": "Jane"
    },
    "2": {
      "kind": "String",
      "field": "name",
      "operator": "eq",
      "operand": "John",
    },
  },
  "groups": {
    "0": ["0", "1"],
    "1": ["0", "2"]
  },
  "meta": {
    "count": 4,
    "version": "1.0"
  }
}
```

groups are optional and defined as a mapping from group identifiers to arrays of operation identifiers. Each group represents a logical combination of operations that can be evaluated together. Implementations may use these groups to optimize query execution or to apply logical operators such as AND/OR to the grouped operations.

There is no special meaning to the operation identifiers themselves; they are opaque strings used to reference sets of operations.
The same applies to the group identifiers used within the `groups` mapping; they are simply references to sets of operations and do not carry any inherent meaning.

Implementations may enforce additional constraints on group identifiers, such as maximum length or allowed characters, but these constraints are not defined by the FilterDSL specification itself.

## Error Handling

Our recommendation is to only return errors when the filter query is invalid according to the FilterDSL specification. This includes cases such as:

- Unknown operators
- Invalid operand types
- Malformed operation map (duplicated operation identifiers)
- Malformed range objects
- Malformed group definitions
- Malformed metadata definition

Errors should be descriptive enough to allow clients to correct their queries without exposing internal implementation details.
We recommend attaching an error code or identifier to each error to facilitate programmatic handling by clients.

> Future versions of this specification may issue a standardized set of error codes for common validation errors.
> Error codes will be designed to be stable across versions to allow clients to handle errors programmatically.

The above recommendation should not conflict with application specific validation rules (i.e: age cannot be negative or age must be less than 150), but the implementation should not try to enforce these rules as part of the FilterDSL validation. We strongly recommend decoupling application-specific validation from FilterDSL validation.

## Versioning

FilterDSL is designed to be versionable. Each version of the specification may introduce new operators, kinds, or other changes. Implementations should indicate which version of the specification they support and handle version differences appropriately.

Version will be specified in the `meta.version` field of the query. the values will be strings representing the version number, such as `"1.0"`. we don't account for patch versions since, in this context, minor version changes are expected to be backward compatible and patch versions are not considered significant for the specification.
Major and minor version will follow the semantic versioning convention, where the major version indicates breaking changes and the minor version indicates backward-compatible additions or changes.

## Reference

- [Operators](./v1/operators.md)
- [Operations](./v1/operations.md)
  - [Kind](./v1/kind.md)
- [Queries](./v1/queries.md)
