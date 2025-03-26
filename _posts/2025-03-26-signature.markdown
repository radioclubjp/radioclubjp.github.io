---
layout: post
title:  "Parity of permutations"
date:   2025-03-26 1:00:22 +0200
categories: math
---


# Introduction

The signature homomorphism is one of the most beautiful and miraculous objects in mathematics. Its existence is a miracle explained by what we will call the fundamental fact. This post explores the meaning of the signature homomorphism, the fundamental fact and ways to prove it.

# Motivation

<img src="/assets/BoxGame.png" alt="box game" width="600"/>

Let's start with a simple problem.

> Suppose you have $n$ boxes arranged in a row and labeled $1, 2, \ldots, n$. You are playing a game. An allowed move consists of picking two boxes and switching their positions. There's a catch - next to you there is a light. Initially the light starts off but each time you switch two boxes the light switches its state on $\to$ off and off $\to $ on. Your task: arrange a series of moves such that after performing them, the boxes are all back to their original positions, yet the light is on.

This is trivially impossible when you have only one box: there's nothing to switch. It's also impossible with two boxes: there are only two possible positions and a move must switch between the two. The positions correspond exactly to whether the light is on or off. What about three boxes? Do you understand intuitively why it's true for 3 boxes? What about 5 boxes?

The reader might benefit from trying the interactive version of the game with five boxes below (credit to Claude 3.7 Sonnet).

{% include signature-game.html %}

If you're anything like me and have a background in basic group theory and linear algebra, your mind probably immediately goes towards the signature homomorphism. In fact the set up of the problem corresponds almost exactly to the set up of the signature homomorphism. 

# Basic definitions

The signature homomorphism is a function $\rho: S_n \to C_2$.
$S_n$ is the group of all permutations of the set $[n] := \{1,\ldots, n\} \subset \mathbb{N}$ . $C_2$ is the cyclic group of order two which may be regarded as the set $\{-1, 1\}$ under multiplication. 

It is defined as follows. Suppose you have a permutation $\sigma \in S_n$. Then we can express it as a product of **transpositions** (permutations which switch two elements and leave all other elements fixed), say $\sigma = \tau_1 \ldots \tau_k$ where each $\tau_i \in S_n$ is a transposition. We also accept the situation where the number of factors is $k=0$ and $\sigma = 1$ (the identity permutation).

\begin{equation}
\rho(\sigma) := (-1)^k
\label{eq:signature-def}
\end{equation}

We ignore everything about the factors themselves and only look at the number of them. More precisely, we look at the parity of the number of factors.

To see that each permutation can be expressed as a product of transpositions, consider that permutations $\sigma \in S_n$ correspond exactly to arrangements of boxes labeled $1$ through $n$. Multiplying a permutation by a transposition on the left, which is the same as function composition on the left, corresponds to switching the positions of two boxes. The claim that every permutation is expressible as a product of transpositions then boils down to the claim that every arrangement of boxes can be achieved by a series of swaps. This is obviously true: first swap the box labeled $1$ to the correct position, then that labeled $2$, and so on. In fact this shows that every permutation in $S_n$ can be expressed as a product of at most *n* transpositions. Actually, $n-1$ transpositions suffices, since by the time you've put $n-1$ boxes in their place, the final box will also necessarily be in its own place and no more swaps are needed.

In the above paragraph we gave one way to express a permutation as a product of transpositions. But that is by no means the only way to do so. Consider, for example, the fact that the identity permutation is expressible as a product of two transpositions $1 = (12)(12)$ as well as the product of zero transpositions, which is the identity. Here $(a \  b)$ for $a\neq b$ stands for the transposition which maps $a\to b$ and $b\to a$ and leaves other numbers fixed.

Besides being a function, the signature homomorphism $\rho$ also has the special property that it's a homomorphism. The property is stated as follows: for distinct permutations $\sigma_1, \sigma_2 \in S_n$, 

\begin{equation}
\rho(\sigma_1 \sigma_2) = \rho(\sigma_1) \rho(\sigma_2)
\label{eq:signature-hom}
\end{equation}

The mystery and the fundamental fact that this essay is concerned with, is the fact that no matter how you express a permutation as a product of transpositions, the parity of the number of factors doesn't vary. That's what makes our definition \eqref{eq:signature-def} well-defined. For if it were possible to express a permutation $\sigma$ both as a product of an even number of transpositions and as an odd number of transpositions, $\rho(\sigma)$ would have to equal both $-1$ and $1$, which is impossible. We call this claim the **fundamental fact** in the context of this essay (it's not actually called that way in mathematics).

Perhaps the reader immediately grasps why the fundamental fact must necessarily be true. If that's the case, then the author should not recommend they continue reading this essay, since it consists of an attempt to grapple with how unintuitive it is and to try to make it a little bit more intuitive, as well as explore different ways to prove the fundamental fact. 

## Another way to think of the fundamental fact

One way to look at the fundamental fact is as follows. For each $S_n$ we construct a graph. The vertices consist of permutations of $[n]$, i.e. the elements of $S_n$. Two permutations are connected by an edge if they differ by a transposition. That is, for two bijections $\sigma_1, \sigma_2 :[n] \to [n]$, there is an edge $(\sigma_1 \sigma_2)$ if there is a transposition $\tau \in S_n$ such that $\sigma_2 = \tau \sigma_1$. The edges don't need to have a direction since the relation is symmetric: as $\tau$ is a transposition, we have $\tau^2 = 1$ so $\tau \sigma_2 = \tau \tau \sigma_1 = \tau^2 \sigma_1 = 1\sigma_1  = \sigma_1$.

The fundamental fact then can be restated as follows. The graph of each $S_n$ can be divided into two nonempty groups of vertices $A$ and $B$ such that no two vertices in the same group are connected by an edge. That is, each edge in the graph connects a vertex in $A$ with a vertex in $B$.

If we have such a decomposition, suppose that the identity lies in $A$. If it lies in $B$, we switch the names of the groups. Then the signature of a permutation well defined: it's even when the permutation lies in $A$ and odd when it lies in $B$. It is then impossible for a permutation to be expressible as a product of both an even and an odd number of transpositions. That is because if a permutation is a product of $n$ transpositions, that means that to get to the permutation, you have to walk in the graph along $n$ edges. But since each edge you walk switches the group, that means the group you end up in is only a matter of the parity of the number of factors.

Here's an example of such a partition of the graph of $S_3$. The group $A$ is shown on the left and the group $B$ is shown on the right.


<div class="large-svg-container">
  {% include k33graph.svg %}
</div>


# Determinants

$\rho$ can be used to define the determinant. Let $R$ be a commutative ring. If the reader is not familiar with the term, they are free to take $R$ to be equal to the set of rational numbers $\mathbb{Q}$ or the set of real numbers $\mathbb{R}$ or the set of complex numbers $\mathbb{C}$, as these are all common examples of commutative rings.

Fix $n \in \mathbb{N}$ and let $V = R^n$ be the free $R$-module of rank $n$. That is, the space of n-tuples of elements of $R$, written $(r_i)= (r_1,\ldots,r_n) \in R^n,  \ r_i \in R$. Elements in $V$ may be added together:

$$(r_1,\ldots, r_n )+ (t_1, \ldots, t_n) = (r_1 + t_1, \ldots, r_n + t_n)$$

and multiplied by an element $a \in R$:

$$ a (r_1, \ldots, r_n) = (ar_1, \ldots, ar_n)$$

The space has a natural choice for a basis $e_i \in V$ where each $e_i$ is a n-tuple which has component $1$ in the $i$'th place and $0$ in every other place. Thus every $(r_i) \in V$ may be expressed as

$$(r_i) = \sum_{i=1}^{n}r_ie_i$$

The determinant is a multilinear map (that is, a map that is linear in every argument when keeping the other arguments fixed)

$$\det: V^n \to R$$

uniquely defined by the following two properties:

1.  $\det(v_1,\ldots, v_n) = 0$ if any $v_i = v_j$ for $i \neq j$. I.e. it's antisymmetric.
2. $\det(e_1,\ldots, e_n) = 1$

The reason why the first property has to do with antisymmetry is simple. For if in the expression $\det(v_1, \ldots, v_n)$, for $i < j$ we make the substitutions $v_i = a+b$ and  $v_j = a+b$ and letting $f(a,b)$ be the corresponding determinant with these substitutions, we find that 

$$
\begin{array}{rl}
0 &= f(a+b, a+b) \quad \tag{by property 1} \\[1em]
&= f(a+b, a) + f(a+b, b) \\[1em]
&= \underbrace{f(a, a)}_{= 0} + f(a,b) + f(b,a) + \underbrace{f(b, b)}_{= 0} \\
&= f(a,b) + f(b,a)
\end{array}
$$

thus $f(a,b) = -f(b,a)$. That means that if in the determinant you switch the places of two arguments, you get the same value except multiplied by $-1$.

This property is very closely related to the signature homomorphism. In fact, by applying a series of permutations to the arguments in $\det(e_1, \ldots, e_n)$, by looking at the sign of the final result, we can read off the sign of the permutation. In fact, we can even define the signature homomorphism $\rho$ in this way:

if $\sigma : [n] \to [n]$ is a permutation in $S_n$, then we define 

$$
\det(e_{\sigma(1)}, \ldots, e_{\sigma(n)} ) = \rho(\sigma) \det(e_1, \ldots, e_n)
$$

Thus the existence of the determinant implies the fundamental fact as well as the existence of the signature homomorphism.

How about the other way around? Does the existence of the signature homomorphism imply the existence of the determinant?

Consider $n$ arbitrary vectors $(v_i)_{i=1}^n$, each expressed in terms of the basis as $v_i = \sum_j a_{ij} e_j \in V$, $(a_{ij}) \in R$.


$$
\begin{array}{rl}
\det(v_1, \ldots, v_n) &= \det(\sum_j a_{1j} e_j, \ldots , \sum_j a_{nj} e_j) \\
&= \sum_{1 \leq i_1, \ldots, i_n \leq n} \det(a_{1i_1} e_{i_1}, \ldots, a_{ni_n} e_{i_n})  &\text{by multilinearity of det} \\
&= \sum_{1 \leq i_1, \ldots, i_n \leq n} a_{1i_1}\ldots a_{ni_n} \det(e_{i_1}, \ldots, e_{i_n})  &\text{also by multilinearity} \\
\end{array}
$$

Now by property 1 of the determinant, if in a term some $i_j = i_k$ for $i \neq k$, then $\det(e_{i_1}, \ldots, e_{i_n}) = 0$. So the only nonzero terms in the sum above are the terms where all the indices $(i_j)_j$ are distinct. This happens exactly when $j \mapsto i_j$ defines a permutation of $[n]$. Thus the sum reduces to the sum over all permutations of $S_n$, which is equal to

$$
\begin{array}{rl}
\sum_{\sigma \in S_n} a_{1\sigma(1)}\ldots a_{n\sigma(n)} \det(e_{\sigma(1)}, \ldots, e_{\sigma(n)}) 
&= \sum_{\sigma \in S_n} \rho(\sigma) a_{1\sigma(1)}\ldots a_{n\sigma(n)} \underbrace{\det(e_1, \ldots, e_n)}_{=1} \\
&= \sum_{\sigma \in S_n} \rho(\sigma) a_{1\sigma(1)}\ldots a_{n\sigma(n)} 
\end{array}
$$


The last expression is referred to as the Leibniz expansion of the determinant and is often taken as the definition of the determinant.


# Elementary proofs of the fundamental fact

There are a number of different popular elementary proofs of the fundamental fact in the literature. We present a few of them in this chapter. They are not hard proofs. However, they are not very natural and have the unfortunate appearance of being rather technical and not very illuminating. That is not to say they aren't valid proofs: they're completely valid. However, later I will present what I think is a better and a more natural proof, which is the main motivating reason behind the article.

## Proofs using counting orbits

Permutations decompose the set $[n]$ into **orbits**. An orbit is just 