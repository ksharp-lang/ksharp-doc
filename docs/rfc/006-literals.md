---
title: Literals
---

# Literals

Supported literals in k# are: strings, characters, numbers.

## String

```kotlin
"Single line"

"""
Multi Line
String
"""
```

## Character

```kotlin
'a'
```

:::note

k# uses UTF-8 for character and strings

:::

## Numbers

### Integers

```haskell
1  100 -50
```

### Decimals

```haskell
1.5 0.4 .3 -45.0 1e10
```

### Thousands separator

`k#` allows to use `_` as thousand separator

```fsharp
1_000_000
```

### Expressing numbers in different bases

1. binary

```fsharp
0b1001_0001
```

2. hexadecimal

```fsharp
0xFF00FF
```

3. Octal

```fsharp
0o1236
```
