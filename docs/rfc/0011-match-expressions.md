---
title: Match expressions
---

# Match expressions

Use `match` expressions to create expressions that are executed if a match assignment is true

```fsharp
match expr with
    [] -> "Empty"
    [1 | rest] -> "Has elements"
```

## combining matches with AND and OR

use `&&` or `||` to match the value with many expressions 

```fsharp
match expr with
    [] && [1] -> "Do something"
    [1 | rest] -> "Do another thing"
```

## Exhausting a match with _

`k#` will validate the `match` expression always returns a value. You can use `_` to assert any value when create a match with infinite possible number of values.

```fsharp
match expr with
    1 -> "One"
    2 -> "Two"
    _ -> "Other value"
```

## Calling functions in match clauses

If you want to use the expr into a match clause, you can combine many clauses with `&&` 

```fsharp
match expr with
    x && even x -> "Even"
    _ -> "Odd"
```

:::note

To know more about the expressions used in match check [match assignment expressions](#match-assigment)

:::
