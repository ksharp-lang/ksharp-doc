---
title: if expression
---

# if expression

`k#` allows `if` expressions to define control flows

```haskell
if expr then trueExpr else falseExpr
```

If `trueExpr` type is unit then you can omit the `else` part

```haskell
if expr then trueExpr
```


## Nested if

In `k#` the if can be nested inside `trueExpr` or `falseExpr` 

```haskell
if expr then
    if expr2 then trueExpr
else falseExpr
```
