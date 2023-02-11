---
title: Modules
---

# Modules

In `k#` each file is a module. The path where the file is located represent the module name. e.g /ksharp/common/file.ks
the module name is `ksharp.common.file`

## Term scope

Be default all functions are private and all types are public, to make a function visible in other scopes add `pub` scope

```rust
pub fn sum a b = a + b
```

use `internal` to prevent export a type declaration


```kotlin
internal type Integer = Int
```

:::note

You can't use a `internal` type with a `pub function`

:::

## Importing modules

use `import` expressions to load the public terms of a module

```dart
import ksharp.common.file as file
```

### Accessing a term inside a module

By using the '.' operator you can access the functions inside a module. 

```rust
file.load "File Name"
```

:::note

Spaces is not allowed between module key, `.` and function value

:::

### Cloning functions from different modules

You can clone functions using `@clone` macro. 

```kotlin
@clone newFuncName functionToClone
```

Cloning allow use external functions as constant values. 

:::warning

Only works with function defined in the same library. 

:::
