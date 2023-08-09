---
title: Traits
---

# Traits

Trait allows you to define a set of methods that can be used in any type. This is similar to interfaces in C# or Java.

```scala
trait Num a =
    sum  :: a -> a -> a
    prod :: a -> a -> a
```

methods can have a default implementation

```scala
trait Eq a =
    (=) :: a -> a -> Bool
    (!=) :: a -> a -> Bool

    (=) a b = not (a != b)
    (!=) a b = not (a = b)
```

# Implementing traits

Using `impl` you can define the implementation of a trait for a type

```rust
impl Eq for Num =
    (=) a b = ...
```

you can also use native when implementing the trait methos

```rust
impl Eq for Num =
    native (=) a b
```

annotations also are allowed when implementing the trait methods

```rust
impl Eq for Num =
    @name("equals" for=["java"]) 
    (=) a b = False
```
