---
title: Untyped lambda calculus
---

# Untyped lambda calculus

> Notes taken from *[Type Theory and Formal proof. An introduction](https://www.cambridge.org/core/books/type-theory-and-formal-proof/0472640AAD34E045C7F140B46A57A67C)*

## Construction principles

1. **Abstraction:** $\lambda x.M.$ (read as *abstraction of M over x*)
2. **Application** $M N$ (read as *application of M to N*). 

If it is necessary, some parentheses should be added during the construction process. e.g

Abstraction of $y$ over $\lambda. x - y$

$$
\lambda y.(\lambda x. x - y)
$$

## Functions of more than one argument: Currying

The function $f(x, y) = x^2 + y$ can be write as $\lambda x. (\lambda y. (x^2 + y))$.

## Lambda terms

Expressions in the lambda calculus are called $\lambda-term$. $\Lambda$ is the set of all $\lambda-terms$. To start with, we assume the existence of an infinite set $V$ of so-called variables: $V = \{x, y, z, ..\}$

1. **Variable:** if $u \in V$, then $u \in \Lambda$
2. **Application:** if $M$ and $N \in \Lambda$, then $(M N) \in \Lambda$
3. **Abstraction** if $u \in V$ and $M \in \Lambda$, then $(\lambda u. M) \in \Lambda$

so, $\Lambda = V|(\Lambda \Lambda)|(\lambda V. \Lambda)$

## Subterms

All $\lambda-term$ has sub terms defined as:

1. **Basis:** $Sub(x) = \{x\}$, for each $x \in V$
2. **Application:** $Sub((M N)) = Sub(M) \cup Sub(N) \cup \{(M N)\}$
3. **Abstraction:** $Sub((\lambda x.M)) = Sub(M) \cup \{(\lambda x.M)\}$

### Subterm properties

1. **Reflexivity:** For all $\lambda-terms\ M$, we have $M \in Sub(M)$
2. **Transitivity:** If $L \in Sub(M)$ and $M \in Sub(N)$, then $L \in Sub(N)$

### Proper subterm

$L$ is a proper subterm of $M$ if $L$ is a subterm of $M$, but $L \not \equiv M$

## Free and bound variables

1. **binding variable**: variable after $\lambda$ e.g. $\lambda x.$
2. **bound variable**: If a binding variable is used in the expression it is bound in the expression

### Free variables definition

$FV$ is the set of free variables of a $\lambda-term$

1. **Variable**: $FV(x) = \{x\}$
2. **Application**: $FV(MN) = FV(M) \cup FV(N)$
3. **Abstraction**: $FV(\lambda x. M) = FV(M) \setminus \{x\}$

## Closed $\lambda-term$

The $\lambda-term$ $M$ is closed if $FV(M) = \emptyset$. A closed $\lambda-term$ is also called a *combinator*. The set of all closed $\lambda-terms$ is denoted by $\lambda^0$

## $\alpha-conversion$

It is the possibility of renaming binding (and bound) variables. 

Let $M^{x \to y}$ denote the result of replacing every free occurrence of $x$ in $M$ by $y$. defined as: 
$\lambda x. M =_\alpha \lambda y. M^{x \to y}$, provided that $y \notin FV(M)$ and $y$ is not a binding variable in $M$

### Properties

1. **Compatibility**: if $M =_\alpha N$, then $ML =_\alpha NL$, $LM =_\alpha LN$ and, for arbitrary $z$, $\lambda z. M =_\alpha \lambda z. N$
2. **Reflexivity**: $M =_\alpha M$
3. **Symmetry**: If $M =_\alpha N$ then $N =_\alpha M$
4. **Transitivity**: If both $L =_\alpha M$ and $M =_\alpha N$, then $L =_\alpha N$

### $\alpha-variant$

If $M =_\alpha N$, then $M$ and $N$ are said to be $\alpha-convertible$ or $\alpha-equivalent$. $M$ is called an $\alpha-variant$ of $N$ (and vice versa) 


## Function evaluation process $\beta-reduction$

An expression of the form $(\lambda x. M)N$ can be rewritten to the expression $M[x:=N]$, i.e. the expressions $M$ in which every $x$ has been replaced with $N$. We call this process $\beta-reduction$ of $(\lambda x. M)N$ to $M[x:=N]$. e.g

1. $(\lambda x. x^2 + 1)(3)$ reduces to $(x^2 + 1)[x := 3]$ which is $3^2 + 1$.
2. $(\lambda z. (\lambda x. x)(\lambda y.y))$ reduces to $(\lambda z. (\lambda y. y))$

:::note 

Application is the construction of new expression, not the execution of the expression. It is only after the reduction of the latter term that we obtain the result of the application

:::

### Substitution

1. $x[x:=N] \equiv N$
2. $y[x:=N] \equiv y$ if $x \not\equiv y$
3. $(PQ)[x := N] \equiv P[x := N]\ Q[x := N]$
4. $(\lambda y. P)[x := N] \equiv \lambda z. (P^{y \to z}[x := N])$, if $\lambda z. P^{y \to z}$ is an $\alpha-variant$ of $\lambda y. P$ such that $z \notin FV(N)$


### One step $\beta$-*reduction* $\to_\beta$

The incentive to defining the relation $\to_\beta$ is the presence of an application term where the first part is an abstraction: $\lambda x. M$. Since an abstraction can be thought of as representing a function, we can conceive of part $N$ as an argument for this function.

1. **Basis**: $(\lambda x. M)N \to_\beta M[x:=N]$
   1. The subterm of the form $(\lambda x. M)N$ on the left hand side is called a *redex* (from *red*ucible *ex*pression). The subterm $M[x:=N]$ on the right hand side is called the *contractum* (of the redex)
2. **Compatibility**: $(M \to_\beta N)$, then $ML \to_\beta NL$, $LM \to_\beta LN$ and $\lambda x. M \to_\beta \lambda x. N$

### Zero or more steps $\beta$-*reduction* $\twoheadrightarrow_\beta$

$M \twoheadrightarrow_\beta N$ if there is $n \ge 0$ and there are terms $M_0$ to $M_n$ such that $M_0 \equiv M$, $M_n \equiv N$ and for all $i$ such that $0 \le i \lt n$: $M_i \to_\beta M_{i+1}$

Hence, if $M \twoheadrightarrow_\beta N$, there exists a chain of single-step $\beta$-*reductions*, starting with $M$ and ending with $N$:

$$
M \equiv M_0 \to_\beta M_1 \to_\beta M_2 \to_\beta \dots \to_\beta M_{n-2} \to_\beta M_{n-1} \to_\beta M_{n} \equiv N
$$

**Lemma:**

1. $\twoheadrightarrow_\beta$ extends $\to_\beta$, i.e. if $M \to_\beta N$, then  $M \twoheadrightarrow_\beta N$.
2. $\twoheadrightarrow_\beta$ is reflesive and transitive, i.e:
   1. (*refl*): for all $M: M \twoheadrightarrow_\beta M$,
   2. (*trans*): for all $L$, $M$ and $N$: if $L \twoheadrightarrow_\beta M$ and $M \twoheadrightarrow_\beta N$ then $L \twoheadrightarrow_\beta N$.

## $\beta$-conversion, $\beta$-equality, $=_\beta$

$M =_\beta N$ if there is an $n \ge 0$ and there are terms $M_0$ to $M_n$ such that $M_0 \equiv M, M_n \equiv N$ and for all $i$ such that $0 \le i \lt n$: either $M_i \to_\beta M_{i+1}$ or $M_{i+1} \to_\beta M_i$

For example: $(\lambda y. yv)z =_\beta (\lambda x. zx)v$ since we have the following chain, where $\leftarrow_\beta$ is the inverse of $\to_\beta$:

$$

(\lambda y. yv)z \to_\beta zv \leftarrow_\beta (\lambda x. zx)v

$$

$=_\beta$ is an equivalence relation, hence *reflexive, symmetric and transitive*

## $\beta$-normal form ($\beta$-nf)

1. $M$ is in $\beta$-normal form if $M$ does not contain any redex
2. $M$ has a $\beta$-normal form if there is an $N$ in $\beta$-normal form that $M =_\beta N$. Such an N is a $\beta$-normal form of $M$

When $M$ is in $\beta$-nf, then $M \twoheadrightarrow_\beta N$ implies $M \equiv N$

## Fixed point theorem

For all $L \in \Lambda$ there is $M \in \Lambda$ such that $LM =_\beta M$. e.g the function $f(n) = n^2$, has two fixed points $0$ and $1$. The successor function $s(n) = n + 1$ has no fixed point at all.
