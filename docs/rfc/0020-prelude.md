---
title: Prelude
---

# Prelude

Prelude is the base library loaded by default in all `k#` modules

## Types

### Numeric types

All numbers are type of trait `Num a`. Other numeric types are:

1. `Byte`: number of 8 bits
2. `Short`: number of 16 bits
3. `Int`: number of 32 bits
4. `Long`: number of 64 bits
5. `BigInt`: for larger numbers more of 64 bits
6. `Float`: decimal number of 32 bits
7. `Double`: decimal number of 64 bits
8. `BigDecimal`: for large decimal more of 64 bits

### Inference of constant numeric types

Constant numeric follow this rules:

1. If the number is used in a function the the number is coerced to the expected argument type
1. In case the argument type is not defined in the function then
   1. If number is decimal choose `Double`
   2. If the number is integer choose `Int` or `Long` depending of the number size.

:::warning Warning

Coercion follow the following rules:

1. `decimal` types can coerce to an `integer` type
2. number must fit into the type. e.g. Compiler can allow coerce `10000` into a `Byte` type

:::

### Numeric trait 

1. `(+) a a`: addition 
2. `(-) a a`: subtraction 
3. `(*) a a`: multiplication
4. `(/) a a`: division
5. `(%) a a`: modulus
6. `(**) a a`: exponentiation

### Character types

1. `Char`: a character e.g. `'a'`
2. `String`: a list of character e.g. `"Hello World"`

:::note

A string is also interpreted as `List Char`

:::

### Collection types

1. `List` is a collection of the same type e.g. `List Int`
2. `Set` not allow duplicates. e.g. `Set Int`
3. `Map` key value store. e.g. `Map String Int`

