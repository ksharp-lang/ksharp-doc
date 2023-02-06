---
title: Indentation
---

# Indentation

`k#` allows use indentation for legibility. It is flexible about using spaces or tabs. 

## Expressions and indentation

You can use indentation with expressions to avoid use parenthesis when using operators. e.g this expression require parenthesis to make the sum an argument for the function

```haskell
sum 1 2 (3 + 4)
```

you can use indentation to get the same result

```haskell
sum 1
    2
    3 + 4
```

## Indentation and If expression

You can use indentation to make more readable the if expressions

```haskell
if condExpr 
    then trueExpr
    else falseExpr
```

or 

```haskell
if condExpr then
    trueExpr
    else falseExpr
```

:::note

For expressions the indentation level has no meaning, each new line no matter the indentation is a new expression

:::
