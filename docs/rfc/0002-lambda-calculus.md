---
title: Lambda calculus
---

# $\lambda$-calculus


## Defining functions

Function name should star with a lowercase letter

```haskell
sum a b = a + b
```

*k#* tries to infer the types of the function. You can also define the function types:

```haskell
sum :: (Num a) => a -> a -> a
sum a b = a + b
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
