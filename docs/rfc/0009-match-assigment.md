---
title: Match assignment expression
---

# Match assignment expression

`k#` use `=` as and match assignment operator. You can match values to variables, or the elements of a list, map or types. All match assignments are defined using `let` or `match` expressions

## Match a value to a variable (binding)

```haskell
x = 10
```

## Match a variable to a value

```haskell
10 = x
```

## Match tuples

```haskell
x, y = 10, 20
```

## Match lists

```haskell
[x, y] = [10, 20]
```

You can also match many arguments and the rest in a variable

```fsharp
[1, 2 | others] = [1, 2, 3]
3 = others //this is true
```

## Match types

```kotlin
Bool x = Bool True
```

If type have labels you can also use the labels to partial match a type

```kotlin
Username password: p = Username name: "user1" password: "12345678"
```

## Matching sets

With sets the match check the expression at the right contains the elements defined in the expression at the left

```fsharp
#[1, 2] = x // match x contains 1 and 2
```

## Matching maps

The keys matched must be exists in the map expression at the right

```kotlin
{"key1": x, "key2": y} = {"key1": "value"} //error key2 is not in the map expression at the right
```
