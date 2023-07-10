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

| token           | Definition                                                                          |
| --------------- | ----------------------------------------------------------------------------------- |
| letter          | Unicode categories: lowercase, uppercase, titlecase                                 |
| lowerCaseLetter | Unicode lowercase character                                                         |
| upperCaseLetter | Unicode uppercase character                                                         |
| digit           | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9                                                        |
| +               | Represent a normal [indentation offset](/rfc/indentation)                           |
| *               | Represent a repeating [indentation offset](/rfc/indentation)                        |
| ?               | Represent an optional [indentation offset](/rfc/indentation)                        |
| whiteSpace      | " ", "\t"                                                                           |
| operator        | Any [supported operator](#operator-precedence-and-associativity) or custom operator |

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
<character> ::= "'" <unicodeChar> "'"
<string> ::= "\"" <unicodeChar>+ "\""
<multiLineString> ::= "\"\"\"" <unicodeChar> "\"\"\""
<integer> ::= <digit>+
<hexInteger> ::= "0x" <hexDigit>+
<hexDigit> ::= <digit> | "a" | "b" | "c" | "d" | "e" | "f"
<octalInteger> ::= "0o" <octalDigit>+
<octalDigit> ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7"
<binaryInteger> ::= "0b" <binaryDigit>+
<binaryDigit> ::= "0" | "1"
<float> ::= <digit>+ "." <digit>+
```

## Top level expressions

### Import

```bnf
<import> ::= <+> "import" <moduleName> ("as" <key>)?
<key>    ::= <lowerCaseWord>
<moduleName> ::= <lowerCaseWord> ("." <lowerCaseWord>)*
```

:::note

more about [modules](0005-modules.md)

:::

### Type and Traits

```bnf
<type> ::= <+> "internal"? "type" <typeName> "=" <typeExpression>
<trait> ::= <+> "internal"? "trait" <typeName> "=" <*> <traitFunction>+
<typeDeclaration> ::= <+> <functionName> <typeParam>* "=" <typeValue>
 
<typeName> ::= <upperCaseWord> <typeParam>*

<typeExpression> ::= <?> <typeValue> (<typeSetSeparator> <typeValue>)*
<traitFunction> ::= <functionName> "::" <?> <typeValue>

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
<annotation> ::= <+> "@" <annotationName> <annotationParams>?

<annotationName> ::= <lowerCaseWord>
<annotationParams> ::= "(" ")" 
                       | <?> "(" <annotationParam> <?> <annotationParam>* ")"
<annotationParam> ::= <annotationParamName> "=" <annotationParamValue>
                      | <annotationParamValue>
<annotationParamName> ::= <lowerCaseWord> | <upperCaseWord> | <functionName>
<annotationParamValue> ::= <annotation>
                           | <array> 
                           | <string> 
                           | <multiLineString> 
                           | <boolLiteral>
<array> ::= "[" <?> <annotationParamValue> ("," <?> <annotationParamValue>)* "]"
<boolLiteral> ::= "True" | "False"
```

:::note

more about [annotations](0004-annotations.md)

:::

### Expressions

```bnf
<expression> ::= <+> <exprOperator0>
<exprOperator0> ::= <exprOperator1> <operator0> <exprOperator0>
<exprOperator1> ::= <exprOperator2> <operator1> <exprOperator1>
<exprOperator2> ::= <exprOperator3> <operator2> <exprOperator2>
<exprOperator3> ::= <exprOperator4> <operator3> <exprOperator3>
<exprOperator4> ::= <exprOperator5> <operator4> <exprOperator4>
<exprOperator5> ::= <exprOperator6> <operator5> <exprOperator5>
<exprOperator6> ::= <exprOperator7> <operator6> <exprOperator6>
<exprOperator7> ::= <exprOperator8> <operator7> <exprOperator7>
<exprOperator8> ::= <exprOperator9> <operator8> <exprOperator8>
<exprOperator9> ::= <exprOperator10> <operator9> <exprOperator9>
<exprOperator10> ::= <exprOperator11> <operator10> <exprOperator10>
<exprOperator11> ::= <exprOperator12> <operator11> <exprOperator11>
<exprOperator12> ::= <exprOperator> <operator12> <exprOperator12>
<exprOperator> ::= <exprValue> <operator> <exprOperator>

<exprValue> ::= "(" <expression> ")"
                | <literal>
                | <ifExpr>
                | <letExpr>
                | <matchExpr>
                | <functionCall>
                | <tupleExpr>

<literal> ::= <character>
              | <string>
              | <multiLineString>
              | <integer>
              | <hexInteger>
              | <octalInteger>
              | <binaryInteger>
              | <float>
              | <unit>
              | <list>
              | <set>
              | <map>
              | <binding>

<unit> ::= "()"
<list> ::= "[" <expression> ("," <expression>)* "]"
<set> ::= "#[" <expression> ("," <expression>)* "]"
<map> ::= "{" <entry> ("," <entry>)* "}"
<entry> ::= <expression> ":" <expression>
<binding> ::= <lowerCaseWord> 
              | <upperCaseWord>
              | <functionName>
              | <operatorFunctionName>
<operatorFunctionName> ::= "(" <operator> ")"

<ifExpr> ::= <+> "if" <expression> "then" <expression> "else" <expression>
<letExpr> ::= <+> "let" <*> <letBinding>+ "then" <expression>
<matchExpr> ::= <+> "match" <*> <expression> "with" <matchBranch>+
<letBinding> ::= <matchBinding> = <expression>
<matchBranch> ::= <matchBinding> "then" <expression>

<functionCall> ::= <functionCallName> <*> <functionCallParams>?
<functionCallName> ::= <functionName> | <operatorFunctionName>
<functionCallParams> ::= <exprValue>+
```
