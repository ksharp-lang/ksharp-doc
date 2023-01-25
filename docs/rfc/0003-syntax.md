---
title: k# syntax
---

# K# Syntax

## Lexer

### Tokens

|                                         |                                                      |
| --------------------------------------- | ---------------------------------------------------- |
| UppercaseWord                           | Represent types                                      |
| LowercaseWord                           | Represent parameters, functions or keywords          |
| WhiteSpace                              | `\n` is not a whitespace                             |
| NewLine                                 | `\n`                                                 |
| Integer                                 | 1 1000                                               |
| Float                                   | 1.5 .6                                               |
| Operator# `#` depends of the precedence | <code>+ - * / % > < = ! &  $ # ^ ? . \ &#124;</code> |
| Brackets, Parenthesis, Curly Braces     | `[] () {}`                                           |
| Comma                                   | `,`                                                  |

### General notes 

Each token can be separated by one or many `WhiteSpace` tokens. 

### Expression blocks

Using blocks is possible to divide the expression in many lines. The following lines should be have an indentation. All the lines with the same indentation level are part of the same expression e.g

```
let sum = 
    if condition then
        trueExpr
    else falseExpr
```

:::note Note 

Indentation can be spaces or tabs

:::

## Operator precedence

| #   | Operator     |
| --- | ------------ |
| 12  | `**`         |
| 11  | `* / %`      |
| 10  | `+ -`        |
| 9   | `<< >>`      |
| 8   | `< <= >= >`  |
| 7   | `== !=`      |
| 6   | `&`          |
| 5   | `^`          |
| 4   | &#124;       |
| 3   | `&&`         |
| 2   | &#124;&#124; |
| 1   | `$`          |
| 0   | `.`          |

# Grammar

## Top level expressions

### Import

> LowerCaseWord="import" [moduleName](#modulename) LowerCaseWord="as" LowerCaseName:**key** 

#### ModuleName

> LowerCaseWord (Operator="." LowerCaseWord)*

:::note

more about [modules](0005-modules.md)

:::

### Type

> (LowerCaseWord="internal")? LowerCaseWord="type" [typeName](#typename) Operator12="=" [typeExpression](#typeexpression) 

:::note

more about [type system](0001-typesystem.md)

:::

#### typeName 

> UpperCaseWord (LowerCaseWord:**params**)*

#### typeExpression 

> [typeValue](#typeValue) ([typeSetSeparator](#typesetseparator) [typeValue](#typevalue))*

#### typeValue

> [simpleType](#simpletype) ([typeValueSeparator](#typevalueseparator) [typeValue](#typevalue))?

#### simpleType

> (OpenParenthesis [typeValue](#typevalue) CloseParenthesis) | Label? [typeVariable](#typevariable) 

#### typeValueSeparator

> Operator3="->" | Comma

#### typeSetOperator

> Operator9="|" | Operator7="&"

#### typeVariable

> LowerCaseWord | UpperCaseWord

### Trait

> (LowerCaseWord="internal")? LowerCaseWord="trait" [typeName](#typename) Operator12="=" ([traitFunction](#traitfunction))+

#### traitFunction

> LowerCaseWord Operator="::" [typeValue](#typevalue)
