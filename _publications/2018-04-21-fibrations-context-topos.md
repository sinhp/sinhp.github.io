---
title: "Fibration of contexts beget fibrations of toposes"
collection: publications
permalink: /publication/2018-04-21-fibrations-context-topos
excerpt: ''
date: 2018-04-21
venue: 'School of Computer Science, University of Birmingham'
use_math: true
---
<!-- include it up there if you have it
citation: 'Your Name, You. (2009). &quot;Paper Title Number 1.&quot; <i>Journal 1</i>. 1(1).'
-->


{% include macro %}

`Abstract:` We introduce a notion of (op)fibration in the 2-category Con of contexts.
We give a new characterization of weak fibrations internal in 2-categories. Using this
characterization, we establish that a context extension $\thT_1 \to \thT_0$ with (op)fibration
property and a model $M$ of $\thT_0$ in an elementary topos S with natural number object
gives rise to an (op)fibration of elementary toposes with codomain $\CS$.



`Introduction:` For many special constructions of topological spaces (which for us will be point-free,
and generalized in the sense of Grothendieck), a structure preserving morphism between
the presenting structures gives a map between the corresponding spaces. Two very
simple examples are: a function $f \maps X \to Y$ between sets already is a map between the
corresponding discrete spaces; and a homomorphism $f\maps K \to L$ between two distributive
lattices gives a map in the _opposite direction_ between their spectra. The covariance or
contravariance of this correspondence is a fundamental property of the construction.
In topos theory we can relativize this process: a presenting structure in an elementary
topos $\CE$ will give rise to a bounded geometric morphism $p\maps \CF \to \CE$, where $\CF$ is the topos
of sheaves over $\CE$ for the space presented by the structure. Then we commonly find that
the covariant or contravariant correspondence mentioned above makes every such $p$ an
opfibration or fibration in the 2-category of toposes and geometric morphisms.

If toposes are taken as bounded over some fixed base $\CS$, in the 2-category $\BTopos/S$,
then there are often easy proofs got by showing that the generic such p, taken over the
classifying topos for the relevant presenting structures, is an (op)fibration. See [[SVW13]](https://arxiv.org/abs/1310.0705) for some
simple examples. In the 2-category $\ETopos$ of arbitrary elementary toposes with nno, the
properties are stronger (because there are more 2-cells) and harder to prove – see [Joh02].
In this paper our main result (Theorem 7.2) is to show how to use the arithmetic
universe techniques of [Vic17] to get simple proofs in the generic style of the sharper,
base-independent (op)fibration results in ETop.
Our starting point is the following construction in [Vic17], using the 2-category $\Con$
of AU-sketches in [Vic16](https://arxiv.org/abs/1608.01559). Suppose $U \maps \thT_1 \to \thT_0$ is an extension map in $\Con$, and $M$ is a model of $\thT_0$ in $\CS$, an elementary topos with nno. Then there is a geometric theory $\thT_1/M$,
of models of $\thT_1$ whose $\thT_0$-reduct is $M$, and so we get a classifying topos $p\maps S[\thT_1/M] \to \CS$.
We prove that if $U$ is an (op)fibration, then so is $p$ in the sense of [Joh93](https://link.springer.com/article/10.1007/BF00880041).



**Fibration of contexts beget fibrations of toposes** <a href="/files/draft/prem-draft-fibrations-of-toposes.pdf" target="_blank"> <i class="fa fa-file-pdf-o" aria-hidden="true"></i> </a>, [arXiv:1808.08291](https://arxiv.org/abs/1808.08291)   
 _joint with Steve Vickers_, submitted to Theory and Application of Categories (TAC)
 
 



<!--
Recommended citation: Your Name, You. (2009). "Paper Title Number 1." <i>Journal 1</i>. 1(1).
-->
