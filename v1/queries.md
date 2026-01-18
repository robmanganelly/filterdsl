# Queries

A query in FilterDSL is a composition of one or more operations that together define the criteria for selecting data. Queries allow clients to express complex filtering logic in a structured and transport-agnostic manner.

## Structure of a Query

- A query is composed of one or more [operations](./operations.md).
- Operations can be grouped using the **group** field of an operation, allowing multiple operations to be combined under a single logical unit within the query. If an operation does not specify a group, it is assigned to a default group by the implementation.
- Inside a group, each operation must target a specific field in the data. It is recommended that the implementations define ways to alias fields in the database to prevent leaking internal schema details. However, alias should not be used to bypass the constraint of uniqueness of field names within a group.
- Operations inside a groups are evaluated as a logical `AND` , meaning that all operations in the group must be satisfied for the group to be considered true.
- When a query contains multiple groups, the groups are evaluated as a logical `OR`, meaning that if any group evaluates to true, the entire query is considered true.

## Query metadata

Additionally, the query may contain metadata fields that provide additional context or instructions for processing the query.
In this version, the following metadata fields are supported:

- count: specifies the number of operations being passed in the query. It is used for validation purposes in the cases where the payload can be truncated or incomplete. The count is optional. if not found, the implementation should assume the received operations as the complete set.
- version: specifies the version of the FilterDSL specification that the query adheres to.
