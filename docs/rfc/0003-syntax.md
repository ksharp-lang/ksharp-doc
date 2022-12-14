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
| 1   | `**`         |
| 2   | `* / %`      |
| 3   | `+ -`        |
| 4   | `<< >>`      |
| 5   | `< <= >= >`  |
| 6   | `== !=`      |
| 7   | `&`          |
| 8   | `^`          |
| 9   | &#124;       |
| 10  | `&&`         |
| 11  | &#124;&#124; |
| 12  | `=`          |

# Grammar

## Top level expressions

### Imports

> lowerCaseWord(import) [**moduleName**](#modulename) lowerCaseWord(as) lowerCaseName:**key** 

### ModuleName

> lowerCaseWord (operator(.) lowerCaseWord)*

:::tip

more about [modules](0005-modules.md)

:::

### Type

> lowerCaseWord(internal)? lowerCaseWord(type) upperCaseWord operator12(=) [**typeValue**](#typevalue)

:::tip

more about [type system](0001-typesystem.md)

:::

## typeValue

### Alias types

> upperCaseWord newLine

### Tuples types

> [**type**](#type) (, [**type**](#type))+
