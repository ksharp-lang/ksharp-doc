---
title: Lambda calculus
---

# Functions


## Defining functions

Function name should star with a lowercase letter

```haskell
sum a b = a + b
```

*k#* tries to infer the types of the function. You can also define the function types:

```fsharp
sum a: Num b: Num = a + b
```

## Currying

*k#* allows currying functions

```haskell
-- sum2 :: (Num a) => a -> a
sum2 = sum 2
```

## Compositing functions

The functions should receive one argument only.

```haskell
sum2 = sum 2
sum3 = sum 3
sum5 = sum2 . sum3 --read as apply sum2 after sum3
x = sum5 3 -- x is 8
```

## Operators 

:::note 

For operator precedence look [here](0003-syntax.md#operator-precedence)

:::

All operators are infix functions. 

```haskell
1 + 2
```

To use the operator as prefix function wrap the operator inside parenthesis

```haskell
(+) 1 2
```

## Function precedence

function has less precedence than operators.

```haskell
abs -3 * 4 
```

is the same as

```haskell
(double 3) * 5
```
