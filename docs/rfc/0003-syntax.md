---
title: k# syntax
---

# K# Syntax

## General notes 

### Expression blocks

Using blocks is possible to divide the expression in many lines. The following lines should be have an indentation. All the lines within the same indentation offset are part of the same expression e.g

```f#
let sum = 
    if condition then 
        trueExpr
    else falseExpr
```

:::note Note 

Indentation can be spaces or tabs. More about [indentation](#indentation)

:::

### Operator precedence and associativity

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

<<<<<<< HEAD
| token           | Definition                                                                          |
| --------------- | ----------------------------------------------------------------------------------- |
| letter          | Unicode categories: lowercase, uppercase, titlecase                                 |
| lowerCaseLetter | Unicode lowercase character                                                         |
| upperCaseLetter | Unicode uppercase character                                                         |
| digit           | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9                                                        |
| o               | Represent an allowed [indentation offset](/rfc/indentation)                         |
| whiteSpace      | " ", "\t"                                                                           |
| operator        | Any [supported operator](#operator-precedence-and-associativity) or custom operator |
=======
| token           | Definition                                                  |
| --------------- | ----------------------------------------------------------- |
| letter          | Unicode categories: lowercase, uppercase, titlecase         |
| lowerCaseLetter | Unicode lowercase character                                 |
| upperCaseLetter | Unicode uppercase character                                 |
| digit           | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9                                |
| o               | Represent an allowed [indentation offset](/rfc/indentation) |
| whiteSpace      | " ", "\t"                                                   |
>>>>>>> origin/main

:::note 

Each token can be separated by one or many `<whiteSpace>` tokens. 

:::

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
<import> ::= <o> "import" <moduleName> ("as" <key>)?
<key>    ::= <lowerCaseWord>
<moduleName> ::= <lowerCaseWord> ("." <lowerCaseWord>)*
```

:::note

more about [modules](0005-modules.md)

:::

### Type and Traits

```bnf
<type> ::= <o> "internal"? "type" <typeName> "=" <typeExpression>
<trait> ::= <o> "internal"? "trait" <typeName> "=" <o> <traitFunction>+
<typeDeclaration> ::= <o> <functionName> <typeParam>* "=" <typeValue>
 
<typeName> ::= <upperCaseWord> <typeParam>*

<typeExpression> ::= <o> <typeValue> (<typeSetSeparator> <typeValue>)*
<traitFunction> ::= <functionName> "::" <o> <typeValue>

<typeValue> ::= <simpleType> (<typeValueSeparator> <typeValue>)?

<simpleType> ::= <label>? <typeValue>
                 | <label>? "(" <typeValue> ")"
                 | <label>? <typeVariable>

<typeVariable> ::= <typeConstructor>
                   | <typeParam>

<functionName> ::= <lowerCaseWord>
<typeConstructor> ::= <upperCaseWord> 
<typeParam> ::= <lowerCaseWord>
<label> ::= <lowerCaseWord> ":"

<typeSetOperator> ::= "|" | "&"
<typeValueOperator> ::= "->" | ","
```

:::note

more about [type system](0001-typesystem.md)

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
