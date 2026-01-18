# Queries

A query in FilterDSL is a composition of one or more operations that together define the criteria for selecting data. Queries allow clients to express complex filtering logic in a structured and transport-agnostic manner.

## Structure of a Query

A query is represented as a JSON object with the following structure:

- `operations`: A mapping of operation identifiers to operation objects. Each operation object defines a specific filter criterion.
- `groups` (optional): A mapping of group identifiers to arrays of operation identifiers. Each group represents a logical combination of operations that can be evaluated together.
- `meta`: Metadata about the query, including the number of operations and the version of the FilterDSL specification.

## Group Specification

> Future versions may introduce a different group structure to enable more complex logical combinations beyond the current AND/OR semantics.

Groups are optional and defined as a mapping from group identifiers to arrays of operation identifiers. Each group represents a logical combination of operations that can be evaluated together. Implementations may use these groups to optimize query execution or to apply logical operators such as AND/OR to the grouped operations.

There is no special meaning to the group identifiers themselves; they are opaque strings used to reference sets of operations.
The same applies to the group identifiers used within the `groups` mapping; they are simply references to sets of operations and do not carry any inherent meaning.

Implementations may enforce additional constraints on group identifiers, such as maximum length or allowed characters, but these constraints are not defined by the FilterDSL specification itself.

Operations inside a group are evaluated as a logical `AND`, meaning that all operations in the group must be satisfied for the group to be considered true.
When a query contains multiple groups, the groups are evaluated as a logical `OR`, meaning that if any group evaluates to true, the entire query is considered true.

Inside a group, each operation must target a specific field in the data. It is recommended that the implementations define ways to alias fields in the database to prevent leaking internal schema details. However, alias should not be used to bypass the constraint of uniqueness of field names within a group.

## Query metadata

Additionally, the query may contain metadata fields that provide additional context or instructions for processing the query.
In this version, the following metadata fields are supported:

- count: specifies the number of operations being passed in the query. It is used for validation purposes in the cases where the payload can be truncated or incomplete. The count is optional. if not found, the implementation should assume the received operations as the complete set.
- version: specifies the version of the FilterDSL specification that the query adheres to.
