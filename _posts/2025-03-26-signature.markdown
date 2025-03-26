---
layout: post
title:  "A little something about the signature homomorphism"
date:   2025-03-26 1:00:22 +0200
categories: math
---


# Introduction

This post concerns the signature homomorphism. I think the signature homomorphism might be one of the most underappreciated objects in mathematics. I hope the reader will agree after they finish reading this post.

# Motivation

Let's start with a simple problem.

> Suppose you have $n$ boxes arranged in a row and labeled $1, 2, \ldots, n$. You are playing a game. An allowed move consists of picking two boxes and switching their positions. There's a catch - next to you there is a light. Initially the light starts off but each time you switch two boxes the light switches its state on $\to$ off and off $\to $ on. Your task: arrange a series of moves such that after performing them, the boxes are all back to their original positions, yet the light is on.

This is trivially impossible when you have only one box: there's nothing to switch. It's also impossible with two boxes: there are only two possible positions and a move must switch between the two. The positions correspond exactly to whether the light is on or off. What about three boxes? Do you understand intuitively why it's true for 3 boxes? What about 5 boxes?

A reader lacking in imagination will benefit from trying the interactive version of the game with five boxes below (credit: Claude 3.7 Sonnet).

{% include signature-game.html %}

If you're anything like me and have a background in basic group theory and linear algebra, your mind probably immediately goes towards the signature homomorphism. In fact the set up of the problem corresponds almost exactly to the set up of the signature homomorphism. 

# Basic defintions

The signature homomorphism is a function $\rho: S_n \to C_2$.
$S_n$ is the group of all permutations of the set $\{1,\ldots, n\} \subset \mathbb{N}$ . $C_2$ is the cyclic group of order two which may be regarded as the set $\{-1, 1\}$ under multiplication. 

It is defined as follows. Suppose you have a permutation $\sigma \in S_n$. Then we can express it as a product of **transpositions** (permutations which switch two elements and leave all other elements fixed), say $\sigma = \tau_1 \ldots \tau_k$ where each $\tau_i \in S_n$ is a transposition. We also accept the situation where the number of factors is $k=0$ and $\sigma = 1$ (the identity permutation).

\begin{equation}
\rho(\sigma) := (-1)^k
\label{eq:signature-def}
\end{equation}

We ignore everything about the factors themselves and only look at the number of them. More precisely, we look at the parity of the number of factors.

To see that each permutation can be expressed as a product of transpositions, consider that permutations $\sigma \in S_n$ correspond exactly to arrangements of boxes labeled $1$ through $n$. Multiplying a permutation by a transposition on the left, which is the same as function composition on the left, corresponds to switching the positions of two boxes. The claim that every permutation is expressible as a product of transpositions then boils down to the claim that every arrangement of boxes can be achieved by a series of swaps. This is obviously true: first swap the box labeled $1$ to the correct position, then that labeled $2$, and so on. In fact this shows that every permutation in $S_n$ can be expressed as a product of at most *n* transpositions. Actually, $n-1$ transpositions suffices, since by the time you've put $n-1$ boxes in their place, the final box will also necessarily be in its own place and no more swaps are needed.

In the above paragraph we gave one way to express a permutation as a product of transpositions. But that is by no means the only way to do so. Consider, for example, the fact that the identity permutation is expressible as a product of two transpositions $1 = (12)(12)$ as well as the product of zero transpositions, which is the identity. Here $(a \  b)$ for $a\neq b$ stands for the transposition which maps $a\to b$ and $b\to a$ and leaves other numbers fixed.

The mystery and the fundamental fact that this essay is concerned with, is the fact that no matter how you express a permutation as a product of transpositions, the parity of the number of factors doesn't vary. That's what makes our definition \eqref{eq:signature-def} well-defined. For if it were possible to express a permutation $\sigma$ both as a product of an even number of transpositions and as an odd number of transpositions, $\rho(\sigma)$ would have to equal both $-1$ and $1$, which is impossible. We call this claim the **fundamental fact** in the context of this essay (it's not actually called that way in mathematics).

Perhaps the reader immediately grasps why the fundamental fact must necessarily be true.If that's the case, then I should not recommend they continue reading this essay, since it's my attempt to grapple with how unintuitive it is and to try to make it a little bit more intuitive. This essay is 


