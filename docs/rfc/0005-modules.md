---
title: Modules
---

# Modules

In `k#` each file is a module. The path where the file is located represent the module name. e.g /ksharp/common/file.ks
the module name is `ksharp.common.file`

## Term scope

Be default all functions are private and all types are public, to make a function visible in other scopes add `pub` scope

```rust
pub sum a b = a + b
```

use `internal` to prevent export a type declaration

```kotlin
internal type Integer = Int
```

:::note

You can't use a `internal` type with a private `function`

:::

## Importing modules

use `import` expressions to load the public terms of a module

```dart
import ksharp.common.file as file
```
