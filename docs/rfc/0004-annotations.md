---
title: Annotations
---

Annotations in `k#` are used to influence the compiler and optimizer.

:::note

If the goal is produce code, refers to macros.

:::

Annotations go before the element who is going to be marked, using `@annotationName`

```typescript
@sideEffect
log x = println x 
```

## Annotations

### sideEffect or impure

Functions marked with this annotation has side effects, so calling this function is not guarantied return the same result

```typescript
@sideEffect
log x = println x

@impure
random = rand
```
:::note

If a function `a` use a impure function `b` then `a` is impure.

:::

:::tip

The `@impure` annotation is always calculated, this annotation is for documentation purposes, compiler always ignore the annotation.

:::

### pure

Functions marked with this annotation has not side effects, so calling this function is guarantied return the same result

```typescript
@pure
native sum a b
```

:::note

The `@pure` only applies for native functions. uses in other functions are ignored by the compiler

:::

### constant

Functions marked with this annotation are considered constant values

```typescript
@constant
native pi
```

:::note

The `@constant` only applies for native functions. uses in other functions are ignored by the compiler

:::

### name

Used to define the name of the function, depending the target language

```typescript
@name("round-value", for=["clojure"])
@name("RoundValue", for=["c#", "f#"])
roundValue value decimals = ... 
```

:::note Note

Compiler support different rules for function names depending the language. 

:::

### if

Instruct the compiler the function should compile only for target language

```typescript
@if(["java", "c#"])
fn = ... //if target language is java or c# compiler compiles this function
```

## Annotation value types supported

The annotation values can be of the following types:

1. String
2. Number
3. Boolean: true, false
4. Annotation
5. List of String, Number or Annotations

All values inside annotation should have a label, the first value could not have a label, in this case the label is default

```typescript
@if(default=["java"])

// the same as

@if(["java"])
```

:::warning

If an annotation has the same label for a value, the las define value is used.

```typescript
@if("java", "c#")

// is the  same as

@if("c#")
```

:::
