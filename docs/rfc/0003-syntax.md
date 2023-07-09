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

Indentation can be spaces or tabs. More about [indentation](#indentation)

:::

## Operator precedence

| #   | Operator     | Associativity |
| --- | ------------ | ------------- |
| 12  | `**`         | left          |
| 11  | `* / %`      | left          |
| 10  | `+ -`        | left          |
| 9   | `<< >>`      | left          |
| 8   | `< <= >= >`  | left          |
| 7   | `== !=`      | left          |
| 6   | `&`          | left          |
| 5   | `^`          | left          |
| 4   | &#124;       | left          |
| 3   | `&&`         | left          |
| 2   | &#124;&#124; | left          |
| 1   | `$`          | left          |
| 0   | `.`          | left          |

# Grammar

## Lexical tokens

### Built-in Tokens

<<<<<<< syntax-doc
| token           | Definition                                          |
| --------------- | --------------------------------------------------- |
| letter          | Unicode categories: lowercase, uppercase, titlecase |
| lowerCaseLetter | Unicode lowercase character                         |
| upperCaseLetter | Unicode uppercase character                         |
| digit           | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9                        |
=======
| token           | Definition                                                                          |
| --------------- | ----------------------------------------------------------------------------------- |
| letter          | Unicode categories: lowercase, uppercase, titlecase                                 |
| lowerCaseLetter | Unicode lowercase character                                                         |
| upperCaseLetter | Unicode uppercase character                                                         |
| digit           | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9                                                        |
| o               | Represent an allowed [indentation offset](/rfc/indentation)                         |
| whiteSpace      | " ", "\t"                                                                           |
| operator        | Any [supported operator](#operator-precedence-and-associativity) or custom operator |

:::note 

Each token can be separated by one or many `<whiteSpace>` tokens. 

:::
>>>>>>> local

### Tokens

```bnf
<wordLetter> ::= <letter> | <digit> | "_"
<lowerCaseWord> ::= <lowerCaseLetter> <wordLetter>*
<upperCaseWord> ::= <upperCaseLetter> <wordLetter>*
<word> ::= <lowerCaseWord> | <upperCaseWord>
<functionName>  ::= <lowerCaseWord> (<operator> <word>)+
<string> ::= "\"" <unicodeChar> "\""
<multiLineString> ::= "\"\"\"" <unicodeChar> "\"\"\""
```

## Top level expressions

### Import

```bnf
<import> ::= "import" <moduleName> ("as" <key>)?
<key>    ::= <lowerCaseWord>
<moduleName> ::= <lowerCaseWord> ("." <lowerCaseWord>)*
```

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

<<<<<<< syntax-doc
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
=======
:::


### Annotations

```bnf
<annotation> ::= <o> "@" <annotationName> <annotationParams>?

<annotationName> ::= <lowerCaseWord>
<annotationParams> ::= "(" ")" 
                       | <o> "(" <annotationParam> <o> <annotationParam>* ")"
<annotationParam> ::= <annotationParamName> "=" <annotationParamValue>
                      | <annotationParamValue>
<annotationParamName> ::= <lowerCaseWord> | <upperCaseWord> | <functionName>
<annotationParamValue> ::= <annotation>
                           | <array> 
                           | <string> 
                           | <multiLineString> 
                           | <boolLiteral>
<array> ::= "[" <o> <annotationParamValue> ("," <o> <annotationParamValue>)* "]"
<boolLiteral> ::= "True" | "False"
```

:::note

more about [annotations](0004-annotations.md)

:::
>>>>>>> local
