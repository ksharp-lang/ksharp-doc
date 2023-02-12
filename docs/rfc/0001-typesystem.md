---
title: k# Type system
---

# k# Type system

The propose model for *k#* is algebraic data types. All types should start with a capital letter. `Int`, `String`

## Type aliases

It will possible in *k#* define aliases of types. The benefit of aliases is to encode meaning into the type.

```haskell
type Age = Int
```

## Tuples

Type product allows create type combinations. It is called tuples in other languages.

```fsharp
type Point = Int, Int
```

## Unions type

Union types is used to define many combinations of types. they require a `Type Label` at the beginning. Each type label is separated using pipe `|`

```haskell
type Maybe a = Just a | Nothing
```

Union types also are used to define enumerations

```haskell
type Weekend = Saturday | Sunday
```

## Function types

*k#* use currying function style like $\lambda$ calculus. Each function receive an argument and return a value. 

```haskell
type Sum = Int -> Int -> Int
```

### Function type declarations

Functions also can define their types using type declarations

```haskell
add :: Num a -> Num a -> Num a
add a b = a + b
```

Those type declaration are optional, `k#` can infer them when compiling the functions

## Parametric types

*k#* should support parametric types over all forms of types. e.g 

```haskell
type Map a b = Map a b
type Option a = Some a | None
type ToString a = a -> String
```

Parameters should stars with a lowercase letter.

## Traits 

*k#* support traits to define a type which support a collection of functions. A trait requires a type over the methods apply. This type is a *parameter*

```scala
trait Num a =
    sum  :: a -> a -> a
    prod :: a -> a -> a
```

### Traits in algebraic types

Use a trait is similar to using a type

```haskell
type Sum a = Num a -> Num a -> Num a 
type NumMap k v= Map (Num k) v
```

### Intersection types

They are used when you need a type who implements many traits

```haskell
type OrdNum = Ord & Num
```

## Using labels on types

*k#* allows labeled types while composing new types. It allows define records

```haskell
type User = 
    name: String
    password: String

-- Same as
type User = String String
```

behind the scene *k#* creates functions for the labels with the definition

```haskell
type name = User -> String
type name = User -> String -> User
type password = User -> String
type password = User -> String -> User
```

:::note Note 

Labels have meaning on tuples and unions, for the other types they are informative.

:::

## Constrained types

They are like aliases but with a expression, creating a sub set of the type

```fsharp
type PositiveNum a = Num a => it >= 0
type Age = Int => it > 0 && it < 200
```

## Instancing types

All types in *k#* can be instanced using a function with the name of the type. e.g

```haskell
user1 = (User name="hjerez" password="A password")
user2 = (User "hjerez" "A password")
```

## Built-in types

1. List = `List type`
2. Map = `Map key value`
3. Tuple = `Int, Int`
4. Numbers = `Byte`, `Short`, `Int`, `UInt`, `Long`, `Double`, `Float`
5. String = `List Char` or `String`
6. Character = `Char`
