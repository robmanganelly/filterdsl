# Queries

A query in FilterDSL is a composition of one or more operations that together define the criteria for selecting data. Queries allow clients to express complex filtering logic in a structured and transport-agnostic manner.

## Structure of a Query

- A query is composed of one or more [operations](./operations.md).
- Operations can be grouped using the **group** field of an operation, allowing multiple operations to be combined under a single logical unit within the query. If an operation does not specify a group, it is assigned to a default group by the implementation.
- Inside a group, each operation must target a specific field in the data. It is recommended that the implementations define ways to alias fields in the database to prevent leaking internal schema details. However, alias should not be used to bypass the constraint of uniqueness of field names within a group.
- Operations inside a groups are evaluated as a logical `AND` , meaning that all operations in the group must be satisfied for the group to be considered true.
- When a query contains multiple groups, the groups are evaluated as a logical `OR`, meaning that if any group evaluates to true, the entire query is considered true.
