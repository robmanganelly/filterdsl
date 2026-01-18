# Operations

This section describes the various operations available in the FilterDSL. Each operation can be used to manipulate and query data in different ways


## The Signature of an Operation

Each operation in the FilterDSL has a specific signature that defines the types of inputs it accepts and the type of output it produces. 
Understanding the signature of an operation is crucial for composing complex queries and ensuring type safety in your data manipulations.

An operation needs to specify the following:

- **Kind** The kind of the operation, which indicates what operators are applicable
- **Operator** The specific operator that the operation represents, see [Operators](./operators.md)
- **Operand** The operand(s) that the operation acts upon, always values of the supported types
- **Field** The field in the data that the operation targets, which determines where the operation is applied

No matter the transport mechanism, or any serialization format used, valid implementations of the FilterDSL must ensure that this signature is preserved and correctly interpreted.
Some implementations might add other fields to this signature for additional metadata or functionality, but the core signature must remain intact.
