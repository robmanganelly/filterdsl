# Operators

- Operators are keywords that will shape the filter operation
- Operators must be unique
- Operators may need a specific set of terms to function
- Operators are grouped by subgroups

## Some important terms

Primitive Element: used to refer to

- booleans
- numbers (integers, floats, ...)
- strings

Non Primitive Element: used to refer to

- Functions
- Class instances
- Arrays (or any other implementation of Data Structures)
- Symbols (for the languages that have them)

## Operator groups

- Equality
  Primarily intended for primitive operands. It can be composed on other groups. See details on this   specification
  - 'eq'
    Primitive Element a equals to Primitive Element b
  - 'neq'
    Primitive Elemeent a not equal to Primitive Element b
- DateRange
  This is a subset of range. For better semantics, use it when you are not planning to pass floating
  point operands.
  Supports Equality operators
  - 'bt'
    any date between two dates a and b. Dates represented with timestamps should be considered valid
    to be used with this operator. a and b are included 
  - 'nbt'
    any date not between two dates a and b. a and b are also excluded
  - 'af'
    any date after a date A, where A is not included. timestamps apply
  - 'bf'
    any date before a date B, where B is not included. timestamps apply
  - 'iaf'
    Inclusive after. Any date equal or after a date A. timestamps apply
  - 'ibf'
    Inclusive before. Any date equal or before a date A. timestamps apply
