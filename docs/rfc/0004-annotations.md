---
title: Annotations
---

Annotations in k# are used to influence the compiler and optimizer.

:::note

If the goal is produce code, refers to macros.

:::

Annotations go before the element marked using `@annotationName`

```typescript
@sideEffect
let log x = println x 
```

## Annotations

### sideEffect or impure

Functions marked with this annotation has side effects, so calling this function is not guarantied return the same result

```typescript
@sideEffect
let log x = println x

@impure
let random = rand
```
:::note

If a function `a` use a impure function `b` then `a` is impure

:::

### name

Used to define the name of the function, depending the target language

```typescript
@name("round-value" for=["clojure"])
@name("RoundValue", for=["c#", "f#"])
let roundValue value decimals = ... 
```

:::note Note

Compiler support different rules for function names depending the language. 

:::

### if

Instruct the compiler the function should compile only for target language

```typescript
@if("java" "c#")
let fn = ... //if target language is java or c# compiler compiles this function
```
