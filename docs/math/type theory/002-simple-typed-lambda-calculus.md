---
title: Simple Typed Lambda Calculus
---

# Simple Typed Lambda Calculus

## The set of simple types

The set $\mathbb{T}$ of all simple types is $\mathbb{T} = \mathbb{V}\ |\ \mathbb{T} \to \mathbb{T}$

The set $\mathbb{V}$ also called type variables $\mathbb{V} = \{\alpha, \beta, \gamma, \dots \}$. 

Type variables $\mathbb{V}$ are abstract representations of basic types such as numbers, lists, etc.

Arrow types $\mathbb{T} \to \mathbb{T}$ represent functions. *Arrows types are right associative*

In order to express a `term` $M$ has a type $\gamma$, we denoted that as $M: \gamma$.

## Use of types in lambda calculus

### Application

if $M: \gamma \to \tau$ and $N: \gamma$, then $MN : \tau$

:::note Note

In $MN$ if $M: \dots_1 \to \dots_2$ then $N$ should match $\dots_1$

:::

### Abstraction

if $x: \delta$ and $M: \tau$, then $\lambda x. M : \delta \to \tau$


## Typing methods

There are two typing methods:

1. Typing a la Church, where the types are explicit defined for each term
2. Typing a la Curry, where the types are inferred from the expression

## Judgement $\vdash$

e.g $x: \alpha,\ y: (\alpha \to \alpha) \to \beta\ \vdash (\lambda z: \beta.\ \lambda u: \gamma.\ z)(yx): \gamma \to \beta$

This judgement can be read as follows:

> In the context $x: \alpha \to \alpha,\ y: (\alpha \to \alpha) \to \beta$ the term $(\lambda z: \beta.\ \lambda u: \gamma.\ z)(yx)$ has type $\gamma \to \beta$

## Derivation rules for Church's $\lambda\to$

1. Pre-typed $\lambda$-terms, $\Lambda_\mathbb{T}$

$\Lambda_\mathbb{T} = V|(\Lambda_\mathbb{T}\Lambda_\mathbb{T})|(\lambda V: \mathbb{T}. \Lambda_\mathbb{T}) $

### Statement, declaration, context, judgement

1. A *statement* is of the form $M: \delta$, where $M \in \Lambda_\mathbb{T}$ and $\delta \in \mathbb{T}$. In such a statement, $M$ is called *subject* and $\delta$ the type
2. A *declaration* is a statement whit a variable as subject
3. A *context* is a list of declarations with different subjects
4. A judgement has the form $\Gamma \vdash M: \delta$, with $\Gamma$ a context and $M: \delta$ a statement

### Premiss-conclussion format

$$
\frac{premiss1\ \ premiss2\ \dots\ premiss\ n}{conclussion}
$$

The meaning of this derivation schema is: if we know that premiss 1 up to premiss n hold, then the corresponding conclussion may be drawn. The number of premisses may be zero, in which case one only writes the conclussion (without the horizontal line)

### Derivations rules for $\lambda\to$

1. **Variable** 

<center>

$\Gamma \vdash x: \delta$ if $x: \delta \in \Gamma$

</center>

2. **Application**

$$
\frac{\Gamma \vdash M: \delta \to \tau\ \ \Gamma \vdash N: \delta}{\Gamma \vdash MN: \tau}
$$

3. *Abstraction*

$$
\frac{\Gamma, x: \delta \vdash M: \tau}{\Gamma \vdash \lambda x: \delta.\ M: \delta \to \tau}
$$
