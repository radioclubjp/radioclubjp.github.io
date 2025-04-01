---
layout: post
title:  "On the parity of permutations"
date:   2025-03-26 1:00:22 +0200
categories: math
---


## Introduction

The signature homomorphism is one of the most beautiful and miraculous objects in mathematics. Its existence is a miracle explained by what we will call the fundamental fact. This post explores the meaning of the signature homomorphism, the fundamental fact and ways to prove it.

* This will become a table of contents (this text will be scrapped).
{:toc}

# Motivation

Let's start with a simple problem.

> Suppose you have $n$ boxes arranged in a row and labeled $1, 2, \ldots, n$. You are playing a game. An allowed move consists of picking two boxes and switching their positions. There's a catch - next to you there is a light. Initially the light starts off but each time you switch two boxes the light switches its state on $\to$ off and off $\to $ on. Your task: arrange a series of moves such that after performing them, the boxes are all back to their original positions, yet the light is on.

This is trivially impossible when you have only one box: there's nothing to switch. It's also impossible with two boxes: there are only two possible positions and a move must switch between the two. The positions correspond exactly to whether the light is on or off. What about three boxes? Do you understand intuitively why it's impossible for 3 boxes? What about 5 boxes?

The reader might benefit from trying the interactive version of the game with five boxes below (credit to Claude 3.7 Sonnet).

{% include signature-game.html %}

If you're anything like me and have a background in basic group theory and linear algebra, your mind probably immediately goes towards the signature homomorphism. In fact the set up of the problem corresponds almost exactly to the set up of the signature homomorphism. 

# Basic definitions

## The signature homomorphism 

The signature homomorphism is a function $\rho: S_n \to C_2$.
$S_n$ is the group of all permutations of the set $[n] := \{1,\ldots, n\} \subset \mathbb{N}$ . $C_2$ is the cyclic group of order two which may be regarded as the set $\{-1, 1\}$ under multiplication. 

It is defined as follows. Suppose you have a permutation $\sigma \in S_n$. Then we can express it as a product of **transpositions** (permutations which switch two elements and leave all other elements fixed), say $\sigma = \tau_1 \ldots \tau_k$ where each $\tau_i \in S_n$ is a transposition. We also accept the situation where the number of factors is $k=0$ and $\sigma = 1$ (the identity permutation).

\begin{equation}
\rho(\sigma) := (-1)^k
\label{eq:signature-def}
\end{equation}

We ignore everything about the factors themselves and only look at the number of them. More precisely, we look at the parity of the number of factors.

Besides being a function, the signature homomorphism $\rho$ also has the special property that it's a homomorphism. The property is stated as follows: for any permutations $\sigma_1, \sigma_2 \in S_n$, 

$$
\rho(\sigma_1 \sigma_2) = \rho(\sigma_1) \rho(\sigma_2)
$$

## Every permutation can be represented as a product of transpositions

To see that each permutation can be expressed as a product of transpositions, consider that permutations $\sigma \in S_n$ correspond exactly to arrangements of boxes labeled $1$ through $n$. Multiplying a permutation by a transposition on the left, which is the same as function composition on the left, corresponds to switching the positions of two boxes. The claim that every permutation is expressible as a product of transpositions then boils down to the claim that every arrangement of boxes can be achieved by a series of swaps. This is obviously true: first swap the box labeled $1$ to the correct position, then that labeled $2$, and so on. In fact this shows that every permutation in $S_n$ can be expressed as a product of at most *n* transpositions. Actually, $n-1$ transpositions suffices, since by the time you've put $n-1$ boxes in their place, the final box will also necessarily be in its own place and no more swaps are needed.

## The lack of uniqueness of such representation and the fundamental fact

In the above section we gave a method to express a permutation as a product of transpositions. But that is by no means the only way to do so. Consider, for example, the fact that the identity permutation is expressible as a product of two transpositions $1 = (12)(12)$ as well as the product of zero transpositions, which is the identity. Here $(a \  b)$ for $a\neq b$ stands for the transposition which maps $a\to b$ and $b\to a$ and leaves other numbers fixed.

The mystery and the **fundamental fact** that this essay is concerned with, is the fact that no matter how you express a permutation as a product of transpositions, the parity of the number of factors doesn't vary. That's what makes our definition \eqref{eq:signature-def} well-defined. For if it were possible to express a permutation $\sigma$ both as a product of an even number of transpositions and as an odd number of transpositions, $\rho(\sigma)$ would have to equal both $-1$ and $1$, which is impossible. We henceforth will refer to this claim freely as the fundamental fact.

Another way to rephrase the fundamental fact is by asserting that the identity permutation cannot be expressed as a product of an odd number of transposition. Indeed, it implies the fundamental fact since if a permutation can be expressed as both an even and an odd number of transpositions

$$
\begin{align*}
\sigma &= (a_1b_1)\ldots(a_kb_k) \\
\sigma &= (c_1d_1)\ldots (c_ld_l)
\end{align*}
$$

then the inverse of $\sigma$ is the same product of the permutations but in reverse:

$$
\sigma^{-1} = (c_ld_l)\ldots (c_1d_1)
$$

since to reverse a sequence of transpositions it's enough to perform the same transpositions in reverse order.

So that we can express the identity permutation using a product of an even and an odd number of transpositions (resulting in an odd number of transpositions)

$$
1 = \sigma \sigma^{-1} = (a_1b_1)\ldots (a_kb_k) (c_ld_l)\ldots (c_1d_1)
$$

which would be impossible if the identity could be expressed as a product of an odd number of transpositions. Conversely, if the identity can be expressed as a product of an odd number of transpositions, since it also can be expressed as a product of an even number of transpositions (an empty product of no transpositions: 0 is even), it would contradict the fundamental fact. Thus we find a simpler statement equivalent to the fundamental fact.

# A graph theoretic interpretation of the fundamental fact

One way to look at the fundamental fact is as follows. For each $S_n$ we construct a graph. The vertices consist of permutations of $[n]$, i.e. the elements of $S_n$. Two permutations are connected by an edge if they differ by a transposition. That is, for two bijections $\sigma_1, \sigma_2 :[n] \to [n]$, there is an edge $(\sigma_1 \sigma_2)$ if there is a transposition $\tau \in S_n$ such that $\sigma_2 = \tau \sigma_1$. The edges don't need to have a direction since the relation is symmetric: as $\tau$ is a transposition, we have $\tau^2 = 1$ so $\tau \sigma_2 = \tau \tau \sigma_1 = \tau^2 \sigma_1 = 1\sigma_1  = \sigma_1$.

The fundamental fact then can be restated as follows. The graph of each $S_n$ can be divided into two nonempty groups of vertices $A$ and $B$ such that no two vertices in the same group are connected by an edge. That is, each edge in the graph connects a vertex in $A$ with a vertex in $B$.

If we have such a decomposition, suppose that the identity lies in $A$. If it lies in $B$, we switch the names of the groups. Then the signature of a permutation well defined: it's even when the permutation lies in $A$ and odd when it lies in $B$. It is then impossible for a permutation to be expressible as a product of both an even and an odd number of transpositions. That is because if a permutation is a product of $n$ transpositions, that means that to get to the permutation, you have to walk in the graph along $n$ edges. But since each edge you walk switches the group, that means the group you end up in is only a matter of the parity of the number of factors.

Here's an example of such a partition of the graph of $S_3$. The group $A$ is shown on the left and the group $B$ is shown on the right.


  <img src="/assets/k33graph.svg" alt="K3,3" width="70%" height="auto" style="display: block;margin-bottom: 4rem;margin-top: 4rem; margin-left: auto; margin-right: auto;">

This diagram constitutes a proof that the fundamental fact is true for $S_3$. However, it's not obvious why such diagrams can be constructed more generally for $S_n$ where $n>3$. If the fundamental fact is true, it follows that they can be constructed but it's not obvious why the graph must be bipartite without assuming the fundamental fact. Thus, this section in no way constitutes a proof of the fundamental fact, only a different perspective on its significance.

# Determinants

The signature homomorphism $\rho$ can be used to define the determinant. Let $R$ be a commutative ring. If the reader is not familiar with the term, they are free to take $R$ to be equal to the set of rational numbers $\mathbb{Q}$ or the set of real numbers $\mathbb{R}$ or the set of complex numbers $\mathbb{C}$, as these are all common examples of commutative rings.

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
0 &= f(a+b, a+b) \quad \text{by property 1} \\[1em]
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

Consider n arbitrary vectors 
$ (v_{i})_{i=1}^{n} $ , each expressed in terms of the basis as 

$$v_i = \sum_{j} a_{ij} e_j \in V$$

with $(a_{ij}) \in R$. Then

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

## A proof by counting orbits

Permutations decompose the set $[n]$ into **orbits**. To understand orbits, we look at a permutation $\sigma: [n] \to [n]$ as an action which takes the box currently in the position $i$ and moves it to position $\sigma(i)$ for all $i\in [n]$.
We repeat this action many times and look at the set of positions that each box takes until it returns back to its original place. Such sets are called orbits. 

There are only finitely many places for the box to go, thus after some repetitions the box must return to a place it has been before.
Can it be that a permutation takes 1 to 2, then to 3, then to 2 again, and it continues to loop between 2 and 3?
The answer is no: every box must eventually return back to its original place for the following reason. A permutation is a bijection, which means that every element is mapped to by one and only one element. Were there any such loops with strings attached, there would be two elements mapping to the same element, which is an impossibility. Thus all orbits are loops and thus partition the set of positions.

For example, take $n=5$ and consider the permutation that consists of moving each box one position to the right except the last box, which goes to the front. The box in position 1 moves to position 2, then 3, then 4, then 5, then back to 1. Thus there is a single orbit, which is the whole set of positions.

As another example, consider the permutation which switches the positions of the first two boxes and leaves the other three boxes alone. Then box 1 moves to position 2, then back to position 1. That's an orbit. Boxes 3,4,5 always stay in their own place, giving us three more orbits. So in total there are four orbits.

We consider what happens to the number of orbits of a permutation after we compose the permutation with a transposition. We do that by considering two different cases.

First, consider the case where the two positions (say i and j) being transposed lie in different orbits. What happens is that all the other elements in the two orbits continue moving in much the same way, except when it's time to move to i, the box jumps to position j instead, and vice versa. The result of this is that the two orbits get stitched together and joined into one bigger orbit.

One may think of the two orbits in terms of two disconnected directed cycles. The effect on the graph of composing the permutation with a transposition is taking an edge in one cycle (possibly self-directed if the cycle has size one) that's directed towards i and redirecting it towards j in the other cycle. And vice versa with j. 

<img src="/assets/orbits.svg" alt="Two directed cycles with redirected edges" width="70%" height="auto" style="display: block; margin: 0 auto;">

Thus multiplying by a transposition in this case has the effect of reducing the number of orbits by one.

Now consider the case where $i,j$ lie in the same orbit. What multiplying by $(ij)$ does the orbits of the permutation is separate the orbit into two distinct orbits: the exact opposite of the previous case. For a visual, you can take the orbit at the bottom in the image above as the starting orbit. The resulting two orbits are pictured at the top.

Thus when $i,j$ lie in distinct orbits, the multiplication by a transposition has the effect of increasing the total number of orbits of the permutation by one.

Thus in either case, the multiplication of a permutation by a transposition has the effect of increasing or decreasing the number of orbits by one, which means the parity of the number of orbits must necessarily change. But therein lies our invariant: if a permutation were expressible as a product of both an even and an odd number of transpositions, the set of orbits of the permutation would have both an even and an odd number of orbits, which is impossible. Thus our fundamental fact is proven.

## A proof by counting inversions

Another popular proof of the fundamental fact proceeds by counting inversions. We view a permutation $\sigma: [n] \to [n]$ in terms of a row of boxes labeled 1 through n, such that the box with the label $i\in [n]$ takes the position $\sigma(i) \in [n]$. In this way, we equate a permutation with an arrangement of $n$ labeled boxes from left to right.

An **inversion** is a pair of boxes where the left label is a higher number than the right label. The quantity we will be concerned with is the parity of the total number of inversions of a permutation. 

Let's consider some examples. Suppose the boxes are arranged as 1,2,3,4,5, which corresponds to the identity permutation. In this permutation, there are no inversions, since in every pair, the left box has a lower number than the right box. In the permutation 2,1,3,4,5, there is exactly one inversion, that is the pair (1,2). The box on the left (box 2) has a higher label than the box on the right (box 1). Another example: consider the permutation 5,4,3,2,1. In this permutation, every pair of boxes is an inversion, because all the boxes are arranged in the opposite way than their labels. So in total there are $\binom{5}{2} = \frac{5(5-1)}{2} = 10$ inversions, which is the maximal number of inversions possible for $5$ boxes.

Now we claim that every transposition changes the parity of the number of inversions. The fundamental fact will then follow from it, since the number of inversions of a permutation is not dependent on the on the way you express it as a product of transpositions, and the parity of the number of inversions tells you whether the permutation can only be expressed as a product of an even number of transpositions or an odd number of transpositions.

To prove this fact, first prove that it's enough to prove it for the case of adjacent transpositions (where you swap the places of two adjacent boxes). That is because every transposition can be expressed as an odd number of adjacent transpositions: suppose there are $n$ boxes between the two boxes $i,j$ in question, where box $i$ is to the left of box $j$. Then we transpose them first by moving $j$ $n+1$ places to the left so that it's adjacent to the left of $i$, then we move the box $i$ $n$ places to the right to the original position of box $j$. So in total we have $2n + 1$ moves with the effect of swapping the positions of boxes $i$ and $j$, while leaving the positions of all the other boxes untouched. The number $2n+1$ is odd no matter what $n$ is.
Thus if every adjacent transposition switches the parity of the number of inversions, then a transposition, which can be expressed as an odd number of adjacent switches, must also switch the parity of the number of inversions, which is what was to be proven.

Now the final part is almost obvious. When you switch the positions of two adjacent boxes, the only pair of boxes which changes their order is exactly the pair of boxes you're switching. If that pair was not an inversion, it becomes an inversion, because the order is reversed. If it was an inversion before, it ceases to be an inversion after the swap. In any case, the number of inversions changes by 1 or -1, which necessarily switches the parity of the total number of inversions, which is what was to be proven.

# Determinants without the fundamental fact?

This chapter presents the proof which is the reason for this post. The proof is based on Claude Chevalley's textbook "Fundamental Concepts in Algebra". The core idea is contained in the book but I have taken the liberty to modify and simplify it in order to make the relationships more direct and streamlined.

We have already discussed the relationship between the determinant and the signature homomorphism. Each has a simple defining property, and the existence of one easily implies the existence of the other. We have seen the formula for the determinant in terms of the signature homomorphism and the formula for the signature homomorphism in terms of the determinant before.

When first encountering the signature homomorphism, it's tempting to notice that it behaves much like the determinant and attempt to prove its existence and the fundamental fact using the determinant. However, one runs into an issue of circularity: in most presentations, determinant is defined (or, in some cases, proven to be well-defined) using the fundamental fact.

I have previously thought it was unavoidable that in a treatment of the determinant and the symmetric groups the fundamental fact must come logically prior and be proven in a technical, combinatorial way. However, Chevalley's textbook has shown that another way was possible. It is possible to develop a satisfactory theory of antisymmetry and determinants in a self-contained way and have the fundamental fact drop out naturally from the theory you develop. In fact, in Chevalley's textbook, the signature homomorphism is actually defined in terms of the determinant. Meanwhile, the determinant is defined in terms of certain algebra structures which we will describe in the following sections.


## Algebras

For a commutative ring $R$ (for example, it could be the set of integers, $\mathbb{Z}$, rational numbers $\mathbb{Q}$, the real numbers $\mathbb{R}$ or the complex numbers $\mathbb{C}$), we say that an $R$-module $A$ is an algebra if it has a $R$-bilinear map $A \times A \to A$, which we call the multiplication on $A$, which is associative. We also require $A$ to contain an element $1 \in A$ that acts as a unit on both sides for the multiplication. Note that we do not require the multiplication on $A$ to be commutative, even though we require that the ring $R$ is commutative.

## Tensor products

In this section we will define and give reason to believe in some basic properties of tensor products. The approach taken in this section is not standard and reflect my personal taste. The reason for this divergence will be explained later. The reader already familiar with tensor products and their properties may safely skip this section as the relevance of the divergence from the standard presentation does not extend beyond the section.

Let $M,N$ be $R$-modules for a commutative ring $R$. Let $T$ be another $R$-module and consider a general bilinear (that is, linear in each argument map) $f: M \times N \to T$. That is, a function of two arguments $f(m,n)$ such that 

$$
\begin{array}{rl}
f(am_1 + bm_2, n) &= af(m_1, n) + bf(m_2, n) \\
f(m, an_1 + bn_2) &= af(m,n_1) + bf(m, n_2)
\end{array}
$$

Bilinear maps are more complicated than linear maps (i.e. homomorphisms). We want to treat it as a homomorphism, just like all other maps between modules. The product $M\times N$ can be given a module structure through component wise addition and multiplication by an element in $R$. Then $f$ becomes a map between two modules, and one might hope that it's a homomorphism. Alas, this is not true in general. This is because if $f$ were a $R$-module homomorphism from the module $MxN$ to the module $T$, then we would have for $r \in R$, $(ra, rb) = r(a,b)$, thus

$$
f(ra, rb) = f(r(a,b)) = rf(a,b)
$$

the last equality by the hypothesis that $f$ is $R$-linear.
However, since $f$ is also bilinear,

$$
f(ra,rb) = rf(a,rb) = r^2f(a,b)
$$

But $r^2f(a,b) \neq rf(a,b)$ in general, so this doesn't work. We need a different approach.

Fortunately, there is such an approach. That approach is through **tensor products**. It's accomplished not by giving a different module structure to $M\times N$ but rather by changing the domain module slightly.

The new domain module is denoted as $M \otimes N$ and referred to as the tensor product of $M$ and $N$. It is defined as follows:

consider the set of all formal $R$-linear combinations of pairs $(m,n), m\in M, n\in N$. Many definitions require that the formal terms commute with each other, so that $r_1(m_1, n_1) + r_2(m_2, n_2)= r_2 (m_2, n_2) + r_1(m_1, n_1)$, but that is not in fact necessary. To add two formal expressions in $X$, simply write them side by side and write a plus sign between them. To multiply a formal expression by an element in $R$, we simply multiply all the coefficients of all the terms by that number. We do not care what's inside the brackets.

To obtain $M \otimes N$ from $X$, we impose a certain condition. Two formal expressions in $X$ are declared to be equivalent if and only if they evaluate to the same result for all bilinear maps $M \times N \to T$, where $T$ can be any $R$-module. To evaluate an expression in $X$ on a bilinear map $f$, we use the following formula

$$
f(r_1(m_1, n_1) + r_2(m_2, n_2)) = r_1 f(m_1, n_1) + r_2f(m_2, n_2)
$$

$M \otimes N$ is defined to be the resulting set of equivalence classes. There is a natural map $X \to M \otimes N$ taking each element of $X$ to its equivalence class.

The image of a formal expression $(m,n) \in X$ is denoted by $m \otimes n \in M \otimes N$. Addition of elements in $M \otimes N$ is defined by picking respective expressions in $X$ that represent them, adding the expressions and mapping them back to the tensor product. The result is seen to be independent of choices of representatives since different choices evaluate to the same thing under every multilinear map. In much the same way we define the multiplication of a tensor by an element in $R$, by lifting to a formal expression, multiplying each term by an element in $R$, and bringing the result back to the tensor space.

Note that in general not all tensors can be written in the form $m \otimes n$. The most we can hope for is some linear combination of such terms, without any way to combine them. The tensors that can be written in such a way are called **decomposable** tensors.

We can easily verify many properties of tensors by considering the properties of an arbitrary bilinear map. Thus for example we can verify that

$$
\begin{array}{rl}
(rm) \otimes n = r (m \otimes n) = m \otimes (rn)
\end{array}
$$

because if $f$ is an arbitrary bilinear map, 

$$
\begin{array}{rl}
f(rm, n) = rf(m,n) = f(r(m,n)) = f(m, rn)
\end{array}
$$.

In much the same way we verify that 

$$
m_1 \otimes n + m_2 \otimes n = (m_1 + m_2) \otimes n
$$

$$
m \otimes n_1 + m \otimes n_2 = m \otimes (n_1 + n_2)
$$

by seeing that the formal expressions that represent them evaluate to the same result for all bilinear maps.

The three properties above are usually taken as part of the definition of the tensor product. However, I feel that such a presentation somewhat obscures the purpose of the tensor product, which is to linearize bilinear maps, i.e. to make them into homomorphisms. Instead of starting with these formal properties of tensors, we start with their purpose at the core of the definition, which is to make bilinear maps into homomorphisms/linear maps, and derive the formal properties as a natural consequence. 

A curious thing about the unusual approach to the tensor product that we presented is that it's **impredicative**. That means, in the definitions, it refers to itself. That is because it defines the tensor product in therms of all bilinear maps, while the map $\otimes: (m,n) \mapsto m \otimes n$ is a bilinear map, so it's one of the bilinear maps the definition refers to. This is not a problem in mathematics because the universe is assumed to be fixed, and the purpose of a definition is merely to delineate something that is already there, rather than be an act of creation. For more on predicativity and approaches to the foundations of mathematics which try to avoid it, a good reference is the article ["Predicativity"](https://math.stanford.edu/~feferman/papers/predicativity.pdf) by Solomon Feferman. 

It also follows directly from the properties shown above that the map $\otimes : M \times N \to M \otimes N$ which sends $(m,n) \mapsto m \otimes n$ is a bilinear map itself.

Now suppose $f: M \times N \to T$ is a bilinear map of $R$-modules. We have described how to evaluate formal expressions in $X$ using $f$. If two expressions in $X$ represent the same tensor in $M \otimes N$, then their evaluation at $f$ will be the same by definition of the tensor product. Thus we obtain a well-defined map $\bar{f}: M \otimes N \to T$ which inputs a tensor, and evaluates one of its representatives in $X$ using $f$. The map $\bar{f}$ is easily verified to be a homomorphism of $R$-modules, i.e. a linear map. Moreover, this now-linear map $\bar{f}$ preserves all the information that $f$ has in the following way: the composition $M \times N \to_\otimes M \otimes N \to_f T$ is equal to the original bilinear map $f$.

Moreover, the map $\bar{f}$ is the only map with this property. For it's easy to see that its values are forced at tensors of the form $m \otimes n$ to be $f(m,n)$. Then the fact that the map is required to be $R$-linear also forces its value on all other combinations, thus all elements of $M \otimes N$. 

Thus for any bilinear map of R-modules $f: M \times N \to T$, there always exists a $\bar{f}: M \otimes N \to T$ such that $\bar{f} \circ \otimes = f$, i.e. $\bar{f}(m \otimes n) = f(m,n)$ for all $(m,n) \in M \times N$. This is called the **universal property** of the tensor product. It is often used as the definition of the tensor product and when it's taken as such, it is used to prove that the tensor product is independent of implementation (the way to construct the map satisfying this property): any two modules satisfying this property are isomorphic.

The tensor product of two modules generalizes well into the tensor product of multiple modules. Thus for example we set $M_1 \otimes M_2 \otimes M_3 := (M_1 \otimes M_2) \otimes M_3$. It is a fact that that there is a natural isomorphism $\bar{q}: (M_1 \otimes M_2) \otimes M_3 \cong M_1 \otimes (M_2 \otimes M_3)$, which is the linearization of the bilinear map $q: (M_1 \otimes M_2) \times M_3 \to M_1 \otimes (M_2 \otimes M_3)$ which is defined by setting $q((m_1\otimes m_2), m_3) = m_1 \otimes (m_2 \otimes m_3)$.

Thus when we have a tensor product of multiple spaces, it algebraically doesn't matter which way we put the brackets. And in fact these iterated tensor products satisfy an equivalent universal property of their own, but where instead of considering bilinear maps you consider trilinear or generally multilinear maps. Thus going back to our discussion of the determinant, it is an multilinear function in each argument, thus it induces a module homomorphism $\bar{\det}: \underbrace{V \otimes \ldots \otimes V}_n  \to R$, which has all the same information as the original determinant function.

## The tensor algebra

Now that we've described how tensors work, we can discuss **tensor algebras**. Tensor algebras provide a way to multiply elements of modules while imposing as few restrictions as possible. For example, the tensor algebra over $M = \mathbb{R}^3$ allows one to multiply two three dimensional vectors $v_1, v_2 \in M$. However, this will not be the cross product, where the result lives in the same three dimensional space, nor the dot product, where the result is a scalar. Instead, the product will live in the tensor product $M \otimes M$, and its value is, as should be easy to guess by now, $v_1 \otimes v_2$. It's important to note that this multiplication is not commutative. In general $v_1 \otimes v_2 \neq v_2 \otimes v_1$. We can multiply the result by yet another vector $v_3 \in V$ to get $v_1 \otimes v_2 \otimes v_3$. In general, we define the product on two tensors $t_1 \in M^{\otimes m} = \underbrace{V \otimes \ldots \otimes M}_n$ and $t_2 \in M^{\otimes n}$ by the tensor product map $M^{\otimes m} \times  M^{\otimes n} \to M^{\otimes m + n}$.

This gives us many different tensors of many different lengths but we want to collect them all into one set, so that multiplication inside of this set keeps you inside the same set. For this purpose, we construct the **direct sum**

$$
A_M = \bigoplus_{n=0}^{\infty} M^{\otimes n}
$$

where $M^{\otimes 0}$ is defined to be the ring $R$ in consideration, viewed as an $R$-module. Thus the elements of $A_M$ are finite sums of tensors from any $M^{\otimes n}$.

The tensor algebra is a **graded algebra**, since it's a direct sum of submodules $M_n := M^{\otimes n}$ and multiplying an element of $M_n$ with an element with $M_m$ returns an element of $M_{m+n}$. We say that an element $m \in M_i$ has **degree i**.

Thus in the case $M = \mathbb{R}^3$, $R= \mathbb{R}$, if we let $(e_i)_{i=1}^3$ be the standard basis vectors, we have $e_1 e_2 = e_1 \otimes e_2 \in M^{\otimes 2} \subset A_M$. We can have elements of $A_M$ of mixed degree, for example $e_1 \otimes e_3 + e_2 \in A_M$. The multiplication of such terms is by distributing over the terms and multiplying the individual tensor products. 

$$
\begin{align*}
&(e_1 \otimes e_3 + e_2)(1 + e_2) = (e_1 \otimes e_3 + e_2)1 + (e_1 \otimes e_3 + e_2)e_2 \\
&= e_1 \otimes e_3 + e_2 +  (e_1 \otimes e_3)e_2 + e_2 e_2 \\
&=e_1 \otimes e_3 + e_2 +  e_1 \otimes e_3 \otimes e_2 + e_2 \otimes e_2
\end{align*}
$$

We identify $M_1$, the elements of the first degree, with $M$, so that $M \subset A_M$.

Much like the tensor product satisfies a universal property with respect to bilinear and multilinear maps, the tensor algebra satisfies a similar yet slightly distinct universal property. It concerns homomorphisms of algebras. 

Suppose $M$ is an $R$-module, $T$ is an $R$-algebra and $f: M \to T$ is an $R$-linear map. Then $f$ extends in a unique way to a homomorphism of *algebras*

$\bar{f}: A_M \to T$.

It is defined on generators by the formula

$$
\bar{f}(r_1 m_1 \otimes \ldots \otimes m_k) = r_1 f(m_1)\ldots f(m_k)
$$

end extended by the homomorphism properties to all of $A_M$.

## The exterior algebra

Over every $R$-module $M$ there exists the **exterior algebra** $E_M$. The idea behind it is to make the tensor algebra antisymmetric. That is, if $m_1, m_2 \in M$, we want to have $m_1m_2 = -m_2m_1 \in E_M$, which is generally not true for the tensor algebra $A_M$. However, we can make it true by passing to a quotient space of $A_M$. Consider the ideal $I$ in $A_M$ generated by elements of the form $m \otimes m$. Thus all elements of the form $v_1(m \otimes m)v_2 \in I$ for $v_1, v_2 \in A_M$. Define $E_M$ to be the quotient space $A_M/I$. Thus all elements in $I$ become zero in $E_M$. In particular, if $m_1, m_2 \in M$, we have

$$
\begin{align*}
(m_1 + m_2)(m_1 + m_2) = 0
\end{align*}
$$

so 

$$
\begin{align*}
\underbrace{m_1m_1}_{=0} + m_1m_2 + m_2m_1 + \underbrace{m_2m_2}_{=0} = 0
\end{align*}
$$

and thus in $E_M$, 

$$
m_1m_2 = -m_2m_1
$$

From this we derive the fact that in a product expression such as $x=m_1\ldots m_k$, swapping $m_i$ with $m_j$ for $i \neq j$ results in $-x$. This is because any swap of two elements can be arranged as an odd number of adjacent swaps, each one flipping the sign, as was already discussed in the section on proof by counting inversions.

Looking at this, one is tempted to do the following. To prove the fundamental fact for $S_n$, simply pick an expression $m_1\ldots m_n$ in $E_M$ and declare the sign $\rho(\sigma)$ of a permutation $\sigma \in S_n$ to be defined by $m_{\sigma(1)}\ldots m_{\sigma(n)} = \rho(\sigma) m_1 \ldots m_n$. Indeed, flipping any two elements in the product expression is the same as flipping the sign, so that we seem to get a clear invariant which allows us to easily prove the fundamental theorem. 

However, there's a catch. For $\rho(\sigma)$ to be well defined in the above expression the whole expression $m_1 \ldots m_n$ has to be nonzero. Indeed, consider the simple case $n=2$ and $m_1 = m_2$. Then $m_1m_2 = m_1m_1 = 0$. It's true that $m_1m_2 = -m_2m_1$ in this case but that doesn't tell us anything and doesn't provide us with an invariant since we also have $m_1m_2 = m_2m_1$, so should the sign be $-1$ or $1$?

Thus we see that to define the sign of a permutation in $S_n$ using the exterior algebra in this way requires us to first find a product of $n$ elements of $M$ that is nonzero. And this isn't exactly trivial.

A natural choice is to take $M=R^n$ and to take the elements $m_i$ to be the standard basis vectors $e_i \in M$. However, how would you prove that $e_1 \ldots e_n \neq 0$? That is, why can't $e_1 \ldots e_n \in A_M$ be expressed as a sum of elements of the form $a(t\otimes t)b \in A_M$?
Proving this directly seems to be quite difficult. However, a map to be considered in a next section will simplify things greatly.

## Tensor Product of Graded Algebras

Before proceeding, it's important to define another notion, which is that of a tensor product of two graded algebras an algebra. That is, if $A,B$ are graded $R$-algebras, we already know that $A\otimes B$ is an $R$-module but we also want to add a structure of multiplication, so that it becomes an $R$-algebra. Since $A,B$ are algebras, they can be decomposed into a direct sum of submodules of homogeneous elements of differing degrees: $A = \bigoplus_{i=0}^\infty A_i$ and  $B = \bigoplus_{i=0}^\infty B_i$.

The underlying set of the algebra will be the same as that of the tensor product. It decomposes into a direct sum

$$
\begin{align*}
A \otimes B = (\bigoplus_{i=0}^\infty A_i) \otimes B = \bigoplus_{i=0}^\infty A_i \otimes B \\
=  \bigoplus_{i=0}^\infty A_i \otimes (\bigoplus_{i=0}^\infty B_i) = \bigoplus_{i,j=0}^\infty A_i \otimes B_j
\end{align*}
$$

Let's call $T= A \otimes B$ and $T_{i,j} = A_i \otimes B_j$. We define multiplication, which is a bilinear map $T \times T \to T$ on elements of the type $a_i\otimes b_j \in T_{i,j}$ and extend by linearity to all elements. We set

$$
(a_i \otimes b_j)(a_k \otimes b_l) :=(-1)^{kj} (a_ia_k \otimes b_j b_l)
$$

Thus we multiply the corresponding pairs in order (note that the multiplication in $T$ is not necessarily commutative) and crucially add a sign. The sign generally ensures that if the algebras $A,B$ are antisymmetric (a notion that we will not define here), the resulting algebra $T$ is also antisymmetric. The sign will also be crucial in our calculations going further. 

Next, we prove that the multiplication so defined is associative. It's enough to verify it for triples of elements in $T_ij$. Thus suppose for $i = 1, 2,3$, we have $a_{j_i} \otimes b_{k_i} \in T_{j_i, k_i}$.

Using the fact that $b_{k_1} b_{k_2} \in B_{k_1 + k_2}$, 

$$
\begin{align*}
&((a_{j_1}\otimes b_{k_1})  (a_{j_2}\otimes b_{k_2})) (a_{j_3}\otimes b_{k_3}) = (-1)^{k_1j_2} (a_{j_1}a_{j_2} \otimes b_{k_1}b_{k_2}) (a_{j_3}\otimes b_{k_3}) \\
= &(-1)^{k_1j_2} (-1)^{(k_1 + k_2)j_3 } (a_{j_1}a_{j_2}a_{j_3} \otimes b_{k_1}b_{k_2}b_{k_3}) \\
= &(-1)^{k_1j_2 + k_1 j_3 + k_2 j_3} (a_{j_1}a_{j_2}a_{j_3} \otimes b_{k_1}b_{k_2}b_{k_3})
\end{align*}
$$

meanwhile associating brackets the other way, we find

$$
\begin{align*}
&(a_{j_1}\otimes b_{k_1})  ((a_{j_2}\otimes b_{k_2}) (a_{j_3}\otimes b_{k_3}) = (a_{j_1}\otimes b_{k_1})  ((-1)^{k_2j_3} a_{j_2} a_{j_3} \otimes b_{k_2} b_{k_3}) \\
= & (-1)^{k_2j_3} (a_{j_1}\otimes b_{k_1}) (a_{j_2} a_{j_3} \otimes b_{k_2} b_{k_3}) \\
= & (-1)^{k_2j_3} (-1)^{k_1 (j_2 + j_3)} (a_{j_1}a_{j_2}a_{j_3} \otimes b_{k_1}b_{k_2}b_{k_3}) \\
= & (-1)^{k_2j_3 + k_1 j_2 + k_1 j_3} (a_{j_1}a_{j_2}a_{j_3} \otimes b_{k_1}b_{k_2}b_{k_3})
\end{align*}
$$

which is equal to what was obtained above. Therefore the product is associative for terms of the form $T_{i,j}$, which are the generators of $T$, thus the product associative for all terms.

Note that multiplying an element of $T_{i,j}$ by an element of $T_{k,l}$ yields an element of $T_{i+k, j+l}$. Thus there is a natural grading of $T$ given by 

$$
T_n = \bigoplus_{i+j = n} T_{i,j} = T_{0, n} \oplus \ldots \oplus T_{n, 0}
$$

## The analyzing map

### Definition
We present a map which will give us a lot of insight into the exterior algebra and will allow us to see that that the product of basis elements as described above is nonzero

Let $M$ be an arbitrary $R$-module. Denote by $E_M$ the exterior algebra on $M$. Let $T = E_M \otimes E_M$ given the graded algebra structure defined in the above section.

 First consider the map $f: M \to E_M \otimes E_M$ defined by 

 $$
f(m) = 1 \otimes m + m \otimes 1
 $$

 Remembering the way the multiplication in our algebra $T$ was defined and noting that for $m \in M \subset E_M$, $m^2 = 0$ by definition of the exterior algebra, we find the curious property that

 $$
 \begin{align*}
  &f(m)^2 = f(m)f(m) = (1 \otimes m + m \otimes 1)(1 \otimes m + m \otimes 1) \\
= &(1 \otimes m)(1 \otimes m) + (1 \otimes m)(m \otimes 1) + (m \otimes 1)(1 \otimes m) + (m \otimes 1)(m \otimes 1) \\
= &(-1)^{1 * 0 }1 \otimes m^2 + (-1)^{1*1} m\otimes m + (-1)^{0*0} m \otimes m + (-1)^{0 * 1} m^2 \otimes 1 \\
= &-m \otimes m + m \otimes m = 0
\end{align*}
 $$
 
 thus 

 $$
f(m)^2 = 0
 $$

 By the universal property of the tensor algebra, if $A_M$ denotes the tensor algebra of $M$, there exists an algebra homomorphism

 $$
\bar{f}: A_M \to E_M \otimes E_M
 $$

 which extends $f$ in the unique way, so that $\bar{f}\mid_M = f$. However, the curious property that $f(m)^2 = 0$ ensures that also $\bar{f}(m^2) = 0$ for all $m \in M \subset A_M$, thus $\bar{f}$ vanishes on the ideal $J$ used in the definition of the exterior algebra as a quotient of the tensor algebra. That means that $\bar{f}$ induces an algebra homomorphism

 $$
U: E_M \mapsto E_M \otimes E_M
 $$

If this sounds overly formal, you can simply think of $U$ as the unique algebra homomorphism from $E_M$ to $E_M \otimes E_M$ defined for $m \in M \subset E$ by

$$
U(m) = 1 \otimes m + m \otimes 1
$$

and extended to all of $E_M$ using the properties of homomorphisms. The preceding paragraph simply serves to justify the existence (i.e. the consistency) of such a homomorphism.

The map $U$ is called the **analyzing map**. 

### Example evaluation

To see it in action, let's try to evaluate it at more complicated elements, say a product $m_1m_2 \in E$ of elements in $M$. We get

$$
\begin{align*}
  & U(m_1m_2) = U(m_1)U(m_2)  &\text{since $U$ is a homomorphism} \\
= & (1 \otimes m_1 + m_1 \otimes 1)(1 \otimes m_2 + m_2 \otimes 1) \\
= & 1 \otimes m_1m_2 - m_2 \otimes m_1 + m_1 \otimes m_2  + m_1 m_2 \otimes 1
\end{align*}
$$

In the resulting expression we can see that all terms belong to distinct components $T_{i,j} = E_i \otimes E_j$, with the exception of the two middle terms which both belong to $T_{1,1}$. However, in the terms in $T_{1,1}$, all terms are simple tensor products of elements of $M$, the alternating algebra structure is gone. 

### Evaluation at a product of n terms

In general for $n$ terms $m_1 \ldots m_n$, we write $S_{1i} = m_i \otimes 1$ and $S_{2i} = 1 \otimes m_i$ so that $U(m_i) = S_{1i} + S_{2i}$. Then 

$$
\begin{align*}
  & U(m_1 \ldots m_n) = U(m_1) \ldots U(m_n)\\
= & (L_{11} + L_{21})\ldots (L_{1n} + L_{2n}) =  \sum_{\tau} \prod_{i=1}^n S_{\tau(i)i}
\end{align*}
$$

where the sum is over all functions $\tau: [n] \to \\{1,2\\}$. However, if $L \subset [n]$ denotes the set of elements such that $\tau(i) = 1$ and $R \subset [n]$ denotes the complement in $[n]$, we find that for a suitable $N$, 

$$
\prod_{i=1}^n S_{\tau(i)i} = (-1)^N (\prod_{i \in L} m_i) \otimes (\prod_{i \in R} m_i)
$$

All indexed products are ordered in an ascending order with respect to the indices. The precise sign $(-1)^N$ in the above expression is not necessary to understand in later sections. However for the sake of completeness we give an account of it. The reader might want to skip this explanation.

The sign $(-1)^N$ is related to the way the factors $S_{1i}$ and $S_{2i}$ interleave. $N$ is exactly the number of pairs $i<j$ such that $i \in R$ and $j \in L$. To see this, first we note that

$$
\begin{align*}
\prod_{i\in L}S_{1i} = \prod_{i\in L} (m_i \otimes 1) = \prod_{i\in L}m_i \otimes 1 \\
\prod_{i\in R}S_{2i} = \prod_{i\in L} (1 \otimes m_i) = 1 \otimes \prod_{i\in R}m_i
\end{align*}
$$

which means that 

$$
\begin{align*}
  &\prod_{i\in L}S_{1i} \prod_{i\in R}S_{2i} = (\prod_{i\in L}m_i \otimes 1) (1 \otimes \prod_{i\in R}m_i) \\
= & (-1)^{0*0} \prod_{i\in L}m_i \otimes \prod_{i\in R}m_i = \prod_{i\in L}m_i \otimes \prod_{i\in R}m_i
\end{align*}
$$

To get the product $\prod_{i=1}^n S_{\tau(i)i}$ in the form $\prod_{i\in L}S_{1i} \prod_{i\in R}S_{2i}$, we need to perform a series of swaps, so that all the factors $S_{1i}$ end up on the left of $S_{2j}$. We only need to swap adjacent factors of the form $S_{2j}S_{1i}$ and since $S_{2j}S_{1i} = - S_{1i}S_{2j}$, each such swap introduces a minus sign. There are as many such swaps to be done as there are pairs $i<j$ such that $i\in R$, $j \in L$, since the factors $S_{2i}, S_{1j}$ corresponding each such pair must eventually become adjacent and be swapped, and conversely each pair to be swapped corresponds to such a factor.

Putting it all together 

$$
U(m_1 \ldots m_n) = \sum_{L \subset [n], R = [n] \setminus L} \pm \prod_{i\in L}m_i \otimes \prod_{i\in R}m_i
$$

### A coassociativity property

The analyzing map satisfies a curious property that's similar in some ways to associativity and can be described as reversed associativity or coassociativity. To explain, consider an $R$-bilinear map $M \otimes M \to M$. Let $I: M \to M$ be the identity map. Then the associativity of $f$ may be stated by asserting the equality of two functions $M \otimes M \otimes M \to M$:

$$
f\circ (f \otimes I) = f \circ (I \otimes f)
$$

Evaluated at generators, this states that

$$
f(f(a\otimes b) \otimes c) = f(a \otimes f(b \otimes c))
$$

Note that we implicitly use the natural isomorphism $(M \otimes M) \otimes M \to M \otimes (M \otimes M)$.

The dual property that the analyzing map $U$ satisfies is the equality of functions $E_M \to E_M \otimes E_M \otimes E_M$ going the other way:

$$
(U\otimes I)\circ U = (I \otimes U) \circ U
$$

Since the maps in question are algebra homomorphisms (with $E_M \otimes E_M \otimes E_M$ given the product algebra structure), it's enough to verify this relation on the generators $m \in M$ of the algebra $E_M$:

$$
\begin{align*}
  & (U\otimes I)\circ U (m) = (U\otimes I)(m \otimes 1 + 1 \otimes m) = U(m) \otimes 1 + U(1) \otimes m \\
= & (m \otimes 1 + 1 \otimes m) \otimes 1 + (1 \otimes 1) \otimes m = m \otimes 1 \otimes 1 + 1 \otimes m \otimes 1 + 1 \otimes 1 \otimes m
\end{align*}
$$

similarly we find

$$
\begin{align*}
  & (I\otimes U)\circ U (m) = (I\otimes U)(m \otimes 1 + 1 \otimes m) = m \otimes U(1) + 1 \otimes U(m) \\
= & m \otimes (1 \otimes 1) + 1 \otimes (m \otimes 1 + 1 \otimes m) = m \otimes 1 \otimes 1 + 1 \otimes m \otimes 1 + 1 \otimes 1 \otimes m
\end{align*}
$$

So we see that the maps agree on the generators of the algebras, thus they must be equal.

### Iterated analyzing map

Much like the associativity of multiplication ensures that product expressions like $abcd$ well defined without worrying about where to put the brackets, even though the product operation is binary, the dual associativity property described above lets us obtain an iterated map $U^n : E_M \to E_M^{\otimes n + 1}$ in a natural way. It is defined recursively as follows

$$
\begin{align*}
U^0 &= I \\
U^1 &= U \\
U^{n+1} &= (I \otimes \ldots \otimes I \otimes U)\circ U^{n}
\end{align*}
$$

That is, to calculate $U^{n+1}$, we first calculate $U^n$, which is a sum of tensors with $n+1$ factors, and to each term apply $U$ in the last factor. In fact, we could equally well apply it to any of the other $n$ factors and get the same result by the dual associativity property described above. It does not matter which factor we apply the map $U$ to, as long as we do so consistently for all terms.

Another way to formulate the recursive relation is by writing

$$
U^{n+1} = (I \otimes U^n) \circ U
$$

Indeed, this is seen to be equivalent by induction:

Assume the inductive hypothesis that $U^{n} = (I \otimes U^{n-1}) \circ U$. By substituting the definition of $U^{n+1}$ we find that:

$$
\begin{align*}
& U^{n+1} := (I \otimes \ldots \otimes U) \circ U^n \\
= & (I \otimes \ldots \otimes I  \otimes U) \circ (I \otimes U^{n-1}) \circ U  \quad \text{by inductive hypothesis} \\
= & (I \otimes (I \otimes \ldots \otimes I \otimes U)) \circ (I \otimes U^{n-1}) \circ U \\
=  & (I \otimes ((I \otimes \ldots \otimes I \otimes U)\circ U^{n-1})) \circ U \\
& (I \otimes U^n) \circ U \\
\end{align*}
$$

### Analyzing the exterior product of n basis elements

From now on $M = R^n$ is the free and $e_i \in M$ are the standard basis elements of $M$, where $M$ is regarded as a subset of $E_M$. At this point all the pieces are ready for us to show why $\pi = e_1 \ldots e_n \neq 0 \in E_M$. We do that by applying the iterated analyzing map $U^{n-1}$ to $\pi$ to obtain an element of $E^{\otimes n}$ which we will show is nonzero.

First, note that every element $x \in M$ can be written as $x = \sum_{i=1}^n a_i e_i$. Since $M$ is a direct summand $E_{M,1}$ of $E_M$ in the grading $E_M = \bigoplus_{i=0}^\infty E_i$,  each $x \in E_M$ can be written as

$$
x = x' + m = x' + \sum_{i=1}^n a_i e_i
$$

where $m \in M$, $x' \in \bigoplus_{i\neq1} E_i$ and $m = \sum_{i=1}^n a_i e_i$.

For each $i\in [n]$ define a linear form $e_i^* : E_M \to R$ by 

$$e_i^*(x) = a_i$$

where $x$ and $a_i$ are as above.


Consider the $n$-linear form $t: E^{\otimes n} \to R$ given by $e_1^* \otimes \ldots \otimes e_n^*$, i.e. defined on the generators $x_1 \otimes \ldots \otimes x_n \in  E^{\otimes n}$ by 

$$
t(x_1 \otimes \ldots \otimes x_n) = e_1^*(x_1) \ldots e_n^*(x_n)
$$

Note that 

$$
t(e_1 \otimes \ldots \otimes e_n) = e_1^*(e_1) \ldots e_n^*(e_n) = 1
$$

We evaluate $t$ on $U^{n-1}(e_1\ldots e_n)$.

Recall that $U(e_1 \ldots e_n)$ can be decomposed as as sum over all subsets $S \subset [n]$ of distinct elements of the following form

$$
\pm \prod_{i\in S} e_i \otimes \prod_{i\notin S} e_i 
$$

$1\leq k \leq n$ define $t_k = e_k^* \otimes \ldots \otimes e_n^*$. Thus we find that

$$
\begin{align*}
  & t(U^{n-1}(e_1 \ldots e_n)) = t_1((I \otimes U^{n-2}) \circ U(e_1 \ldots e_n)) \\
= & t_1((I \otimes U^{n-2})( \sum_{S \subset [n]}  \pm \prod_{i\in S} e_i \otimes \prod_{i\notin S} e_i ) \\
= & t_1(\sum_{S \subset [n]} \pm \prod_{i\in S} e_i \otimes  U^{n-2}(\prod_{i\notin S} e_i) ) \\
= & \sum_{S \subset [n]} \pm e_1^*(\prod_{i\in S} e_i)  t_2 (U^{n-2}(\prod_{i\notin S} e_i))
\end{align*}
$$

Note that  $e_1^*(\pm (\prod_{i\in S} e_i)) = 0$ for all terms except one: 

it vanishes for all homogeneous terms of degree $\neq 1$ in $E_M$, and among the terms of degree $1$, $e_1^*(e_j) = 0$ for $j \neq 1$ by by definition. Thus the only term left in the sum above is when $S = \\{ 1 \\}$, so the whole sum is equal to

$$
\begin{align*}
\pm e_1^*(e_1)  t_2 (U^{n-2}(\prod_{i\notin \\{1\\}} e_i)) = \pm t_2 (U^{n-2}(e_2 \ldots e_n))
\end{align*}
$$

Applying the same reasoning again $n-1$ times we find that

$$
t(U^{n-1}(e_1\ldots e_n)) = \pm 1 \neq 0
$$

Thus it follows that

$$
e_1 \ldots e_n \neq 0
$$

which proves the fundamental fact. 


### Summary and additional notes

Our aim was to prove that $\pi = e_1 \ldots e_n \neq 0$ in $E_M$ for $M = R^n$. Instead of dealing with the complicated algebraic object $E_M$ directly, we applied the iterated analyzing map $U^{n-1} : E_M \to E_M^{\otimes n}$ to $\pi$ get terms consisting purely of tensor products of elements of $M$, thus divorced from the complexities of $E_M$. Although not all terms of $U^{n-1}(\pi)$ had this form, the other terms fall into distinct direct sum components which were able to safely ignore in our calculations.

Much like the study of natural numbers becomes easier by studying their factors, we studied elements in the exterior algebra by looking at ways to factorize them through the analyzing map. The formula we obtained for the analyzing map applied to a product of elements of $M$ was a sum of many different elements in $E_M \otimes E_M$ which when evaluated at the algebra multiplication map $E_M \otimes E_M \to E_M$ were equal to the original product. An element of $E_M \otimes E_M$ which multiplied equals to $x \in E_M$ may be regarded as a way to factorize $x$. The iterated analyzing map then outputted a sum of many distinct ways to factorize it into $n$ elements in the exterior algebra. Naturally, some of the ways turned out to be quite simple and much more amenable to analysis.

In a sense, we've traded the complexity of antisymmetry in favor of complexity of having multiple terms and multiple tensor factors. However, since analyzing multiple tensors factors and multiple terms are easier than analyzing the exterior algebra directly, the trade was favorable and we were able to obtain our result.

What's nice about this is that all the tools used in the derivation are not specific technical tricks used for this specific problem but are very natural tools in algebra. The analyzing map $U$ for example is used to define the wedge product of two forms, by setting 

$$
\phi \wedge \psi := (\phi \otimes \psi) \circ U
$$

This makes the dual space $E_M^*$ of $E_M$ into an algebra. The identity is given by the form $\varepsilon : E_M \to R$ which is nonzero only on homogeneous elements of degree $0$ and sends $\varepsilon(1) = 1$. The multiplication $\wedge$ is seen to be an associative operation exactly because the analyzing map $U$ is coassociative as proven in an earlier section:

$$
\begin{align*}
  & (\phi_1 \wedge \phi_2) \wedge \phi_3  \\
= & (((\phi_1 \otimes \phi_2) \circ U ) \otimes \phi_3 )\circ U \\
= & (\phi_1 \otimes \phi_2 \otimes \phi_3) \circ (U \otimes I) \circ U \\
= &  (\phi_1 \otimes \phi_2 \otimes \phi_3) \circ (I \otimes U) \circ U \\
= &  (\phi_1 \otimes (\phi_2 \otimes \phi_3 ) \circ U ) \circ U  \\
= & \phi_1 \wedge (\phi_2 \wedge \phi_3) 
\end{align*}
$$

The wedge product is extensively used in various fields of mathematics including differential geometry.

We can also now easily prove the existence of the determinant satisfying the basic properties by defining

$$
\det(v_1, \ldots , v_n) := (e_1^* \otimes \ldots \otimes e_n^*) \circ U^{n-1} (v_1\ldots v_n) = (e_1^* \wedge \ldots \wedge e_n^*) (v_1 \ldots v_n)
$$

Thus we see that a satisfactory development of basic exterior algebra can be given which avoids technical combinatorial lemmas about permutations and avoids explicitly relying on combinatorial homomorphisms. Rather, the development stands on its own, and its many fruits include the fundamental fact.
