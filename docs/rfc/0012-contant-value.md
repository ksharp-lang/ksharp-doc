---
title: Constant value
---

# Constant value

Constant value are literals or function calls that always resolve to the same value.

```haskell
10, "Hello world"
```

## Function as constant values

A function could be treated as constant value, if they return the same value, the expression that the function invoke is constant. 

:::warning

`pub` functions can't be treated as constant value when they are imported. If the function is [cloned](0005-modules.md#cloning-functions-from-different-modules) and the function could be treated as constant value, calling the cloned function will be treated as constant value in the module where it was imported. 

:::

## Let as constant values

Let is constant if all assignments and the expression are constant

```fsharp
//constant let
let x = 10
    y = 20
    x + y
```

```fsharp
//no constant let
let x = noConstsntFunction 10
    y = 20
    x + y
```

## Collections as constant values

Collection are constants if their elements are constants

```fsharp
//constant collection
[10, 20, 30]

//no constant collection
{(noContantFunction 10):"key"}
```

:::note Note

If an `if` or `match` is constant then the expression is evaluated in compile time

:::
