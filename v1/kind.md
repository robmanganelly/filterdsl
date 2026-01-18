# Operation Kind

The **kind** of an [operation](./operations.md) in FilterDSL specifies the category of the operation, which determines the set of [operators](./operators.md) that can be applied to it.
Each kind represents a different type of data or operation context, such as numeric, string, date, or boolean operations.

Understanding the kind of an operation is essential for ensuring that the correct operators are used and that the operation behaves as expected.
The kind helps enforce type safety and guides the implementation in interpreting and executing the operation correctly.

Common kinds of operations include:

- **Numeric**
  Use this kind for operations that involve querying numeric fields
  Operands Type: Numbers (integer or floating point, including all numeric types supported by the language of the implementation)
  Operators: `Equality`, `Comparison`
- **String**
  Use this kind for operations that involve querying string fields
  Operands Type: Strings
  Operators: `Equality`, `String`
- **Date**
  Use this kind for operations that involve querying date or timestamp fields
  Operands Type: Dates (usually serialized as ISO 8601 strings) or Timestamps (represented as unix epoch time, since we're looking client-server compatible and js uses milliseconds since epoch)
  Operators: `Equality`, `Date`,
- **Boolean**
  Use this kind for operations that involve querying boolean fields
  Operands: Booleans
  Operators: `Boolean`
- **Range**
  Use this kind for operations that involve querying numeric ranges
  Operands Type: Numbers (integer or floating point, including all numeric types supported by the language of the implementation)
  Operators: `Range`
- **DateRange**
  Use this kind for operations that involve querying date or timestamp ranges
  Operands Type: Dates or Timestamps (represented as unix epoch time, since we're looking client-server compatible and js uses milliseconds since epoch)
  Operators: `Range`
- **Set**
  Use this kind for operations that involve querying a set of values. If the values are not unique, the implementation should handle duplicates appropriately.It is up
  to the specific application logic to decide whether to support duplicates or not.
  Operands Type: Arrays or Sets of values (the type of the elements should match the type of the field being queried)
  Operators: `Set`

Implementations of FilterDSL must respect the kind of each operation and ensure that only valid operators for that kind are allowed. This helps maintain the integrity and correctness of the filter queries.
Some kinds are added to enhance semantics, and may be representable using a more broader kind. Our recommendation is to always use the most specific kind that accurately represents the operation's intent.

## Kind Specific Values

Some values must be represented in a specific format depending on the kind of the operation. For example:

- **Range** values will be always passed as an object with 2 fields, `from` and `to`, representing the lower and upper bounds of the range, respectively.
- **Date** values may be represented as a unix epoch time in milliseconds, to ensure compatibility between client and server implementations (given that most clients are using Javascript). It is also possible that values are serialized into ISO 8601 strings. The implementation must account for this and correctly parse both formats. It's also valid that the implementation specifies whether it prefers one format over the other. Clients should be at least aware of any limitation and parse their input accordingly.
- **Set** values should be represented as an array or set of values, where the type of each element matches the type of the field being queried. Implementations should handle duplicates according to the application logic.
- **DateRange** values will be always passed as an object with 2 fields, `from` and `to`, representing the lower and upper bounds of the date range, respectively. The values can be represented as unix epoch time in milliseconds or ISO 8601 strings, similar to individual Date values.
