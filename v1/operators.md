# Operators

- Operators are keywords that will shape the filter operation
- Operators must be unique
- Operators may need a specific set of terms to function
- Operators are grouped by subgroups

## Some important terms and conditions

Primitive Element: used to refer to

- booleans
- numbers (integers, floats, ...)
- strings

Non Primitive Element: used to refer to

- Functions
- Class instances
- Arrays (or any other implementation of Data Structures)
- Symbols (for the languages that have them)

Operands: values that operators act upon. They can be either primitive or non-primitive elements.

Extensible groups: Some groups can be used to extend other groups, allowing for the creation of more complex and flexible filter expressions over time. Any implementation of an extensible group must ensure that the operators coming from the extended group are supported and do not conflict with the existing operators. The specification will explicitly define which groups are extensible

## Operator groups

- **Equality**
  Applicable to primitive elements, usually numbers and strings. Booleans are defined as a special case of equality for better semantics
  - `eq` : Equals
    A primitive operand X is equal to a primitive operand Y
  - `neq` : Not Equals
    A primitive operand X is not equal to a primitive operand Y
- **Range**
  Applicable to numeric operands
  - `bt` : Between
    A numeric operand X is greater than or equal to numeric operand Y and less than or equal to numeric operand Z
  - `nbt` : Not Between
    A numeric operand X is less than numeric operand Y or greater than numeric operand Z
  - `ebt` : Exclusive Between
    A numeric operand X is greater than numeric operand Y and less than numeric operand Z
  - `enbt` : Exclusive Not Between
    A numeric operand X is less than or equal to numeric operand Y or greater than or equal to numeric operand Z
- **Date**
  Applicable to date operands, where timestamps are also considered.
  - `af` : After
    A date operand X is after date operand Y
  - `bf` : Before
    A date operand X is before date operand Y
  - `iaf` : Inclusive After
    A date operand X is after or equal to date operand Y
  - `ibf` : Inclusive Before
    A date operand X is before or equal to date operand Y
- **Comparison**
  Applicable to numeric operands
  - `gt` : Greater Than
    A numeric operand X is greater than numeric operand Y
  - `lt` : Less Than
    A numeric operand X is less than numeric operand Y
  - `gte` : Greater Than or Equal To
    A numeric operand X is greater than or equal to numeric operand Y
  - `lte` : Less Than or Equal To
    A numeric operand X is less than or equal to numeric operand Y
- **Enumerable**
  Applicable to operands that can be enumerated, such as arrays or sets.
  The operation will be always check one value against a collection of values.
  Values can be primitive or non-primitive elements as long as they are comparable.
  - `in` : In
  - `nin` : Not In
- **Boolean**
  Applicable to boolean operands. Special case of equality for better semantics.
  - `is` : Is
    A boolean operand X is true/false
  - `isn` : Is Not
    A boolean operand X is not true/false
- **Set**
  Applicable to set operands. Sets are collections of unique elements.
  elements can be primitive or non-primitive as long as the implementation checks and enforces uniqueness.
  - `seq` : Set Equality
    Two set operands X and Y are equal if they contain exactly the same elements, regardless of order.
  - `sup` : Superset
    A set operand X is a superset of set operand Y if all elements of Y are also elements of X, regardless of order, or X having additional elements not in Y.
  - `sub` : Subset
    A set operand X is a subset of set operand Y if all elements of X are also elements of Y, regardless of order, or Y having additional elements not in X.
  - `psup` : Proper Superset
    A set operand X is a proper superset of set operand Y if X is a superset of Y and X contains at least one element not in Y.
  - `psub` : Proper Subset
    A set operand X is a proper subset of set operand Y if X is a subset of Y and Y contains at least one element not in X.
  - `int` : Intersection
    A set operand X intersects with set operand Y if they share at least one common element.
  - `nint` : Not Intersection
    A set operand X does not intersect with set operand Y if they share no common elements.
- **String**
  Applicable to string operands.
  - `cn` : Contains
    A string operand X contains string operand Y if Y is a substring of X.
  - `ncn` : Not Contains
    A string operand X does not contain string operand Y if Y is not a substring of X.
  - `st` : Starts With
    A string operand X starts with string operand Y if X begins with Y.
  - `nst` : Not Starts With
    A string operand X does not start with string operand Y if X does not begin with Y.
  - `end` : Ends With
    A string operand X ends with string operand Y if X ends with Y.
  - `nend` : Not Ends With
    A string operand X does not end with string operand Y if X does not end with Y.
  - `icn` : Case Insensitive Contains
    A string operand X contains string operand Y if Y is a substring of X, ignoring case.
  - `nicn` : Case Insensitive Not Contains
    A string operand X does not contain string operand Y if Y is not a substring of X, ignoring case.
  - `ist` : Case Insensitive Starts With
    A string operand X starts with string operand Y if X begins with Y, ignoring case.
  - `nist` : Case Insensitive Not Starts With
    A string operand X does not start with string operand Y if X does not begin with Y, ignoring case.
  - `iend` : Case Insensitive Ends With
    A string operand X ends with string operand Y if X ends with Y, ignoring case.
  - `niend` : Case Insensitive Not Ends With
    A string operand X does not end with string operand Y if X does not end with Y, ignoring case.
