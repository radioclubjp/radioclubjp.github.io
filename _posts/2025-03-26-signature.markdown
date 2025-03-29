---
layout: post
title:  "Parity of permutations"
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

Besides being a function, the signature homomorphism $\rho$ also has the special property that it's a homomorphism. The property is stated as follows: for distinct permutations $\sigma_1, \sigma_2 \in S_n$, 

\begin{equation}
\rho(\sigma_1 \sigma_2) = \rho(\sigma_1) \rho(\sigma_2)
\label{eq:signature-hom}
\end{equation}

## Every permutation can be represented as a product of transpositions

To see that each permutation can be expressed as a product of transpositions, consider that permutations $\sigma \in S_n$ correspond exactly to arrangements of boxes labeled $1$ through $n$. Multiplying a permutation by a transposition on the left, which is the same as function composition on the left, corresponds to switching the positions of two boxes. The claim that every permutation is expressible as a product of transpositions then boils down to the claim that every arrangement of boxes can be achieved by a series of swaps. This is obviously true: first swap the box labeled $1$ to the correct position, then that labeled $2$, and so on. In fact this shows that every permutation in $S_n$ can be expressed as a product of at most *n* transpositions. Actually, $n-1$ transpositions suffices, since by the time you've put $n-1$ boxes in their place, the final box will also necessarily be in its own place and no more swaps are needed.

## The lack of uniqueness of such representation and the fundamental fact

In the above section we gave a method to express a permutation as a product of transpositions. But that is by no means the only way to do so. Consider, for example, the fact that the identity permutation is expressible as a product of two transpositions $1 = (12)(12)$ as well as the product of zero transpositions, which is the identity. Here $(a \  b)$ for $a\neq b$ stands for the transposition which maps $a\to b$ and $b\to a$ and leaves other numbers fixed.

The mystery and the fundamental fact that this essay is concerned with, is the fact that no matter how you express a permutation as a product of transpositions, the parity of the number of factors doesn't vary. That's what makes our definition \eqref{eq:signature-def} well-defined. For if it were possible to express a permutation $\sigma$ both as a product of an even number of transpositions and as an odd number of transpositions, $\rho(\sigma)$ would have to equal both $-1$ and $1$, which is impossible. We call this claim the **fundamental fact** in the context of this essay though that's not a standard name.

Perhaps the reader immediately grasps why the fundamental fact must necessarily be true. If that's the case, then the author should not recommend they continue reading this essay, since it consists of an attempt to grapple with how unintuitive it is and to try to make it a little bit more intuitive, as well as explore different ways to prove the fundamental fact. 

## Graph theoretic interpretation of the fundamental fact

One way to look at the fundamental fact is as follows. For each $S_n$ we construct a graph. The vertices consist of permutations of $[n]$, i.e. the elements of $S_n$. Two permutations are connected by an edge if they differ by a transposition. That is, for two bijections $\sigma_1, \sigma_2 :[n] \to [n]$, there is an edge $(\sigma_1 \sigma_2)$ if there is a transposition $\tau \in S_n$ such that $\sigma_2 = \tau \sigma_1$. The edges don't need to have a direction since the relation is symmetric: as $\tau$ is a transposition, we have $\tau^2 = 1$ so $\tau \sigma_2 = \tau \tau \sigma_1 = \tau^2 \sigma_1 = 1\sigma_1  = \sigma_1$.

The fundamental fact then can be restated as follows. The graph of each $S_n$ can be divided into two nonempty groups of vertices $A$ and $B$ such that no two vertices in the same group are connected by an edge. That is, each edge in the graph connects a vertex in $A$ with a vertex in $B$.

If we have such a decomposition, suppose that the identity lies in $A$. If it lies in $B$, we switch the names of the groups. Then the signature of a permutation well defined: it's even when the permutation lies in $A$ and odd when it lies in $B$. It is then impossible for a permutation to be expressible as a product of both an even and an odd number of transpositions. That is because if a permutation is a product of $n$ transpositions, that means that to get to the permutation, you have to walk in the graph along $n$ edges. But since each edge you walk switches the group, that means the group you end up in is only a matter of the parity of the number of factors.

Here's an example of such a partition of the graph of $S_3$. The group $A$ is shown on the left and the group $B$ is shown on the right.


  <img src="/assets/k33graph.svg" alt="K3,3" width="70%" height="auto" style="display: block;margin-bottom: 4rem;margin-top: 4rem; margin-left: auto; margin-right: auto;">



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

Let's consider some examples. Suppose the boxes are arranged as 1,2,3,4,5, which corresponds to the identity permutation. In this permutation, there are no inversions, since in every pair, the left box has a lower number than the right box. In the permutation 2,1,3,4,5, there is exactly one inversion, that it the pair (1,2). The box on the left (box 2) has a higher label than the box on the right (box 1). Another example: consider the permutation 5,4,3,2,1. In this permutation, every pair of boxes is an inversion, because all the boxes are arranged in the opposite way than their labels. So in total there are $5 * (5-1) = 20$ inversions, which is the maximal number of inversions possible for $5$ boxes.

Now we claim that every transposition changes the parity of the number of inversions. The fundamental fact will then follow from it, since the number of inversions of a permutation is not dependent on the on the way you express it as a product of transpositions, and the parity of the number of inversions tells you whether the permutation can only be expressed as a product of an even number of transpositions or an odd number of transpositions.

To prove this fact, first prove that it's enough to prove it for the case of adjacent transpositions (where you swap the places of two adjacent boxes). That is because every transposition can be expressed as an odd number of adjacent transpositions: suppose there are $n$ boxes between the two boxes $i,j$ in question, where box $i$ is to the left of box $j$. Then we transpose them first by moving $j$ $n+1$ places to the left so that it's adjacent to the left of $i$, then we move the box $i$ $n$ places to the right to the original position of box $j$. So in total we have $2n + 1$ moves with the effect of swapping the positions of boxes $i$ and $j$, while leaving the positions of all the other boxes untouched. The number $2n+1$ is odd no matter what $n$ is.
Thus if every adjacent transposition switches the parity of the number of inversions, then a transposition, which can be expressed as an odd number of adjacent switches, must also switch the parity of the number of inversions, which is what was to be proven.

Now the final part is almost obvious. When you switch the positions of two adjacent boxes, the only pair of boxes which changes their order is exactly the pair of boxes you're switching. If that pair was not an inversion, it becomes an inversion, because the order is reversed. If it was an inversion before, it ceases to be an inversion after the swap. In any case, the number of inversions changes by 1 or -1, which necessarily switches the parity of the total number of inversions, which is what was to be proven.

# Determinants without the fundamental fact?

This chapter presents the proof which is the reason for this post. The proof is based on Claude Chevalley's textbook "Fundamental Concepts in Algebra". The core idea is contained in the book but the author of this blog post has taken the liberty to modify and simplify it in order to make the relationships more direct and streamlined.

We have already discussed the relationship between the determinant and the signature homomorphism. Each has a simple defining property, and the existence of one easily implies the existence of the other. We have seen the formula for the determinant in terms of the signature homomorphism and the formula for the signature homomorphism in terms of the determinant before.

When first encountering the signature homomorphism, it's tempting to notice that it behaves much like the determinant and attempt to prove its existence and the fundamental fact using the determinant. However, one runs into an issue of circularity: in most presentations, determinant is defined (or, in some cases, proven to be well-defined) using the fundamental fact.

The author of this post previously thought it was unavoidable that in a treatment of the determinant and the symmetric groups the fundamental fact must come logically prior and be proven in a technical, combinatorial way. However, Chevalley's textbook has shown that another way was possible. It is possible to develop a satisfactory theory of antisymmetry and determinants in a self-contained way and have the fundamental fact drop out naturally from the theory you develop. In fact, in Chevalley's textbook, the signature homomorphism is actually defined in terms of the determinant. Meanwhile, the determinant is defined in terms of certain algebra structures which we will describe in the following sections.

## Tensor products

In this section we will define and give reason to believe in some basic properties of tensor products. The approach taken in this section is not standard and reflect the tastes of the author. The reason for this divergence will be explained later. The reader already familiar with tensor products and their properties may safely skip this section as the relevance of the divergence from the standard presentation does not extend beyond the section.

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

The three properties above are usually taken as part of the definition of the tensor product. However, the author feels that such a presentation somewhat obscures the purpose of the tensor product, which is to linearize bilinear maps, i.e. to make them into homomorphisms. Instead of starting with these formal properties of tensors, we start with their purpose at the core of the definition, which is to make bilinear maps into homomorphisms/linear maps, and derive the formal properties as a natural consequence. 

A curious thing about the unusual approach to the tensor product that we presented is that it's **impredicative**. That means, in the definitions, it refers to itself. That is because it defines the tensor product in therms of all bilinear maps, while the map $\otimes: (m,n) \mapsto m \otimes n$ is a bilinear map, so it's one of the bilinear maps the definition refers to. This is not a problem in mathematics because the universe is assumed to be fixed, and the purpose of a definition is merely to delineate something that is already there, rather than be an act of creation. For more on predicativity and approaches to the foundations of mathematics which try to avoid it, a good reference is the article ["Predicativity"](https://math.stanford.edu/~feferman/papers/predicativity.pdf) by Solomon Feferman. 

It also follows directly from the properties shown above that the map $\otimes : M \times N \to M \otimes N$ which sends $(m,n) \mapsto m \otimes n$ is a bilinear map itself.

Now suppose $f: M \times N \to T$ is a bilinear map of $R$-modules. We have described how to evaluate formal expressions in $X$ using $f$. If two expressions in $X$ represent the same tensor in $M \otimes N$, then their evaluation at $f$ will be the same by definition of the tensor product. Thus we obtain a well-defined map $\bar{f}: M \otimes N \to T$ which inputs a tensor, and evaluates one of its representatives in $X$ using $f$. The map $\bar{f}$ is easily verified to be a homomorphism of $R$-modules, i.e. a linear map. Moreover, this now-linear map $\bar{f}$ preserves all the information that $f$ has in the following way: the composition $M \times N \to_\otimes M \otimes N \to_f T$ is equal to the original bilinear map $f$.

Moreover, the map $\bar{f}$ is the only map with this property. For it's easy to see that its values are forced at tensors of the form $m \otimes n$ to be $f(m,n)$. Then the fact that the map is required to be $R$-linear also forces its value on all other combinations, thus all elements of $M \otimes N$. 

Thus for any bilinear map of R-modules $f: M \times N \to T$, there always exists a $\bar{f}: M \otimes N \to T$ such that $\bar{f} \circ \otimes = f$, i.e. $\bar{f}(m \otimes n) = f(m,n)$ for all $(m,n) \in M \times N$. This is called the **universal property** of the tensor product. It is often used as the definition of the tensor product and when it's taken as such, it is used to prove that the tensor product is independent of implementation (the way to construct the map satisfying this property): any two modules satisfying this property are isomorphic.

The tensor product of two modules generalizes well into the tensor product of multiple modules. Thus for example we set $M_1 \otimes M_2 \otimes M_3 := (M_1 \otimes M_2) \otimes M_3$. It is a fact that that there is a natural isomorphism $\bar{q}: (M_1 \otimes M_2) \otimes M_3 \cong M_1 \otimes (M_2 \otimes M_3)$, which is the linearization of the bilinear map $q: (M_1 \otimes M_2) \times M_3 \to M_1 \otimes (M_2 \otimes M_3)$ which is defined by setting $q((m_1\otimes m_2), m_3) = m_1 \otimes (m_2 \otimes m_3)$.

Thus when we have a tensor product of multiple spaces, it algebraically doesn't matter which way we put the brackets. And in fact these iterated tensor products satisfy an equivalent universal property of their own, but where instead of considering bilinear maps you consider trilinear or generally multilinear maps. Thus going back to our discussion of the determinant, it is an multilinear function in each argument, thus it induces a module homomorphism $\bar{\det}: \underbrace{V \otimes \ldots \otimes V}_n  \to R$, which has all the same information as the original determinant function.

## The tensor algebra