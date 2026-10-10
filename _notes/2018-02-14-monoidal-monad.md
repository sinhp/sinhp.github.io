---
title: "Notes on monoidal monad"
author: Sina Hazratpour
permalink: /scribbling/2018-02-14-monoidal-monads
collection: notes
type: "scribbling"
date: 2018-02-14
excerpt: "Notes from my Lab Lunch talk on February 13, 2018"
use_math: true
use_xypic: true
location: "Birmingham, UK"
---

{% include macro %}

`Abstract:`
In the talk, I introduce well-known and by now classical notion of monoidal monads. They are oplax monads on a monoidal category such that the monoidal structures are compatible with monad structures. These compatibility conditions are stated by several coherence axioms. These conditions can be wrapped in the following equivalent definition: A monoidal monad is a monad in the 2-category of monoidal categories, oplax monoidal functors, and monoidal transformations.  

I will then show that oplax monoidal structures of the monad, making it an oplax monoidal monad, is in one-to-one correspondence with monoidal structures of the Eilenberg–Moore category of algebras of that monad such that the forgetful functor from the category of algebras to the base category is strict monoidal. In other words, we get a lifting of the tensor structures of base category to tensor structures of the category of algebras over its objects. I give two important examples of such situation. The first is the symmetric algebra monoidal monad on the monoidal category of $k$-vector spaces over some field $k$. The algebras of this monad are commutative unital $k$-algebras, and the lifted tensor is the usual tensor of algebras. 
The second, which needs the dual (lax) notion, is the power set monad on the monoidal category of sets where tensor product is just cartesian product and unit is the terminal set. The algebras are complete join semi-lattices (aka sup-lattices) and tensoring of algebras is the tensoring of sup-lattices (which is how coproduct of frames is constructed.) The unit of tensor product is the free sup-lattice on one generator, i.e. the lattice containing two elements $\bot$ and $\top$ where $\bot \leq \top$. Here the forgetful functor is only lax monoidal, not strict.
Also, for any commutative monoid $M$, the delooping category $\bb{B} M$ is a monoidal category in which both tensoring and composition are given by multiplication in $M$. Any monoidal monad on $\bb{B} M$ is necessarily (isomorphic to) the identity monad.

`Notes:`
Notes from the talk <a href="/files/CT/monoidal-monad.pdf" target="_blank"> <i class="fa fa-file-pdf-o" aria-hidden="true"></i> </a>

---

### 1. Warm-up: commutative algebras and their tensor

Let $$k$$ be a field (algebraically closed, characteristic zero), and write $$k\text{-alg}$$ for the category of commutative unital $$k$$-algebras. Let

$$
T_n = k[x_1, \dots, x_n].
$$

The algebra $$T_n$$ is the free commutative $$k$$-algebra on $$n$$ generators, so for any $$A \in k\text{-alg}$$

$$
k\text{-alg}(T_n, A) \;\cong\; A^n = \{ (a_1, \dots, a_n) \mid a_i \in A \}, \qquad (\varphi \maps T_n \to A) \;\longmapsto\; \big(\varphi(x_1), \dots, \varphi(x_n)\big).
$$

**Definition.** For an ideal $$I \subseteq T_n$$ and $$A \in k\text{-alg}$$, the *$$A$$-points of the variety of $$I$$* are the common zeros

$$
V_I(A) = \{ \vec{x} \in A^n \mid f(\vec{x}) = 0 \;\; \forall f \in I \}.
$$

**Proposition.** $$V_I \maps k\text{-alg} \to \Set$$ is a representable functor, represented by $$T_n / I$$:

$$
V_I(A) \;\cong\; k\text{-alg}\big( k[x_1, \dots, x_n]/I, \, A \big), \qquad \varphi \;\longmapsto\; \big(\varphi(x_1), \dots, \varphi(x_n)\big).
$$

*Proof.* The tuple lands in $$V_I(A)$$: for $$f = \sum c_{\alpha} x_1^{\alpha_1} \cdots x_n^{\alpha_n} \in I$$, since $$\varphi$$ is a morphism of $$k$$-algebras,

$$
\begin{aligned}
f\big(\varphi(x_1), \dots, \varphi(x_n)\big)
&= \textstyle\sum c_{\alpha} \, \varphi(x_1)^{\alpha_1} \cdots \varphi(x_n)^{\alpha_n} \\
&= \varphi\big( \textstyle\sum c_{\alpha} \, x_1^{\alpha_1} \cdots x_n^{\alpha_n} \big) = \varphi(f) = 0_A.
\end{aligned}
$$

Conversely, a common zero $$\vec{a} \in V_I(A)$$ gives $$T_n \to A$$, $$x_i \mapsto a_i$$, which kills $$I$$ and hence factors through $$T_n / I$$. Naturality in $$A$$ is clear. $$\blacksquare$$

This suggests treating a $$k$$-algebra as a "space" through the functor it represents. The Yoneda embedding

$$
\mathrm{Spec} = \yon \maps k\text{-alg}^{\mathrm{op}} \longrightarrow \Psh(k\text{-alg}^{\mathrm{op}}) = [\, k\text{-alg}, \Set \,], \qquad \mathrm{Spec}_A = k\text{-alg}(A, -)
$$

sends $$A$$ to its functor of points. For example $$\mathrm{Spec}_{T_n}(B) = k\text{-alg}(T_n, B) \cong B^n$$ (affine $$n$$-space), and $$\mathrm{Spec}_{T_n/I} \cong V_I$$.

**Definition.** A *scheme* is a presheaf $$X \in [\, k\text{-alg}, \Set \,]$$ which is locally like $$\mathrm{Spec}$$. That is, $$X$$ is a Zariski sheaf covered by open subfunctors of the form $$\mathrm{Spec}_A$$.

**Remark.** Nothing above needs $$k$$ to be a field: $$k$$ can be any commutative unital ring. For $$k = \bb{Z}$$, the category $$\bb{Z}\text{-alg}$$ is just the category of commutative rings.

`Pushouts are tensors.`
Let $$A, B, C$$ be commutative unital $$k$$-algebras, with $$f \maps A \to B$$ and $$g \maps A \to C$$. Then the square

$$
\xymatrix@C=5em@R=3.5em{
A \ar[r]^-{f} \ar[d]_-{g} & B \ar[d]^-{b \,\mapsto\, b \,{\otimes}\, 1} \\
C \ar[r]_-{c \,\mapsto\, 1 \,{\otimes}\, c} & B \,{\otimes_A}\, C \ar@{}[ul]|(.25){\ulcorner} }
$$

is a pushout of $$k$$-algebras. Here $$B$$ and $$C$$ are regarded as $$A$$-modules via $$f$$ and $$g$$, and

$$
B \otimes_A C = \mathrm{Free}(B \times C) /\!\sim, \qquad (f(a) \cdot b, \, c) \sim (b, \, g(a) \cdot c) \;\; (+\ \text{bilinearity}),
$$

so that $$f(a)b \otimes c = b \otimes g(a)c$$. The multiplication is $$(b \otimes c)(b' \otimes c') = bb' \otimes cc'$$.

*Proof.* Suppose $$\gamma \maps B \to D$$ and $$\delta \maps C \to D$$ satisfy $$\gamma f = \delta g$$:

$$
\xymatrix@C=4.5em@R=3em{
A \ar[r]^-{f} \ar[d]_-{g} & B \ar[d] \ar@/^1em/[ddr]^-{\gamma} & \\
C \ar[r] \ar@/_1em/[drr]_-{\delta} & B \,{\otimes_A}\, C \ar@{-->}[dr]|-{\exists!\,u} & \\
& & D }
$$

We want a unique $$u \maps B \otimes_A C \to D$$ with $$u(b \otimes 1) = \gamma(b)$$ and $$u(1 \otimes c) = \delta(c)$$. Since $$b \otimes c = (b \otimes 1)(1 \otimes c)$$, $$u$$ must be defined on basic tensors by

$$
u(b \otimes c) = \gamma(b) \cdot \delta(c).
$$

It is well defined because $$\gamma f = \delta g$$ and $$D$$ is commutative:

$$
u(f(a) b \otimes c) = \gamma(f(a)) \, \gamma(b) \, \delta(c) = \delta(g(a)) \, \gamma(b) \, \delta(c) = \gamma(b) \, \delta(g(a) c) = u(b \otimes g(a) c).
$$

Multiplicativity again uses commutativity of $$D$$. $$\blacksquare$$

`Localisation.` Take $$f \in A$$ and regard it as a map $$k[x] \to A$$, $$x \mapsto f$$. Inverting $$x$$ is a pushout, and pushouts paste:

$$
\xymatrix@C=5em@R=3em{
k[x] \ar[r]^-{\text{loc.}} \ar[d]_-{x \,\mapsto\, f} & k[x, x^{-1}] \ar[d] \\
A \ar[r]^-{\text{loc.}} \ar[d]_-{h} & A_f \ar[d] \ar@{}[ul]|(.25){\ulcorner} \\
B \ar[r]_-{\text{loc.}} & B_{h(f)} \ar@{}[ul]|(.25){\ulcorner} }
\qquad\qquad k[x, x^{-1}] \cong \frac{k[x,y]}{(xy - 1)}
$$

So $$A_f \cong A \otimes_{k[x]} k[x,x^{-1}]$$, base change gives $$B \otimes_A A_f \cong B_{h(f)}$$, and in particular $$A_f \otimes_A A_g \cong A_{fg}$$.

**Remark.** Every commutative ring $$R$$ is uniquely a commutative $$\bb{Z}$$-algebra, since $$\bb{Z}$$ is the initial commutative ring. So pushouts (and coproducts) of commutative rings can be computed as pushouts (and coproducts) of commutative $$\bb{Z}$$-algebras:

$$
\xymatrix@C=4em@R=3em{
A \ar[r]^-{f} \ar[d]_-{g} & B \ar[d] \\
C \ar[r] & B \,{\otimes_A}\, C \ar@{}[ul]|(.25){\ulcorner} }
\qquad\qquad
\xymatrix@C=4em@R=3em{
\bb{Z} \ar[r] \ar[d] & B \ar[d] \\
C \ar[r] & B \,{\otimes_{\bb{Z}}}\, C \ar@{}[ul]|(.25){\ulcorner} }
$$

In other words, the coproduct in $$k\text{-alg}$$ is $$\otimes_k$$: the cocartesian monoidal structure of $$k\text{-alg}$$ is the tensor of $$\mathbf{Vect}_k$$ *lifted* along the forgetful functor. Section 4 explains this lifting as a monoidal monad.

---

### 2. Monoidal monads

Fix a monoidal category $$(\cat{C}, \otimes, k, a, l, r)$$ with $$l_X \maps k \otimes X \to X$$ and $$r_X \maps X \otimes k \to X$$.

**Definition.** A *monoidal monad* (more precisely, an *opmonoidal* monad) $$S$$ on $$\cat{C}$$ is a monad $$(S, \eta, \mu)$$ on the category $$\cat{C}$$, together with

* a natural transformation $$\tau_{-,-} \maps S(- \otimes -) \To S(-) \otimes S(-) \maps \cat{C} \times \cat{C} \to \cat{C}$$, and
* a morphism $$\tau_k \maps S(k) \to k$$,

which satisfy the following compatibilities.

**(i) Unit coherence of $$\tau$$.** $$r_{SX} \circ (1 \otimes \tau_k) \circ \tau_{X,k} = S(r_X)$$ and $$l_{SX} \circ (\tau_k \otimes 1) \circ \tau_{k,X} = S(l_X)$$:

$$
\xymatrix@C=4em@R=3em{
S(X \,{\otimes}\, k) \ar[r]^-{\tau_{X,k}} \ar[d]_-{S(r_X)} & SX \,{\otimes}\, Sk \ar[d]^-{1 \,{\otimes}\, \tau_k} \\
SX & SX \,{\otimes}\, k \ar[l]^-{r_{SX}} }
\qquad\qquad
\xymatrix@C=4em@R=3em{
S(k \,{\otimes}\, X) \ar[r]^-{\tau_{k,X}} \ar[d]_-{S(l_X)} & Sk \,{\otimes}\, SX \ar[d]^-{\tau_k \,{\otimes}\, 1} \\
SX & k \,{\otimes}\, SX \ar[l]^-{l_{SX}} }
$$

**(ii) Associativity of $$\tau$$.** *(implicit in the talk)*

$$
\xymatrix@C=4em@R=3em{
S((X \,{\otimes}\, Y) \,{\otimes}\, Z) \ar[r]^-{\tau_{X \,{\otimes}\, Y, Z}} \ar[d]_-{S(a)} & S(X \,{\otimes}\, Y) \,{\otimes}\, SZ \ar[d]^-{\tau_{X,Y} \,{\otimes}\, 1} \\
S(X \,{\otimes}\, (Y \,{\otimes}\, Z)) \ar[d]_-{\tau_{X, Y \,{\otimes}\, Z}} & (SX \,{\otimes}\, SY) \,{\otimes}\, SZ \ar[d]^-{a} \\
SX \,{\otimes}\, S(Y \,{\otimes}\, Z) \ar[r]_-{1 \,{\otimes}\, \tau_{Y,Z}} & SX \,{\otimes}\, (SY \,{\otimes}\, SZ) }
$$

**(iii) Compatibility of $$\eta$$ with $$\tau$$.** $$\tau_k \circ \eta_k = 1_k$$ and $$\tau_{X,Y} \circ \eta_{X \otimes Y} = \eta_X \otimes \eta_Y$$:

$$
\xymatrix@C=4em@R=3.5em{
k \ar[d]_-{\eta_k} \ar[dr]^-{1_k} & \\
S(k) \ar[r]_-{\tau_k} & k }
\qquad\qquad
\xymatrix@C=4em@R=3.5em{
X \,{\otimes}\, Y \ar[d]_-{\eta_{X \,{\otimes}\, Y}} \ar[dr]^-{\eta_X \,{\otimes}\, \eta_Y} & \\
S(X \,{\otimes}\, Y) \ar[r]_-{\tau_{X,Y}} & SX \,{\otimes}\, SY }
$$

**(iv) Compatibility of $$\mu$$ with $$\tau$$.**

$$
\xymatrix@C=4em@R=3em{
S^2 k \ar[r]^-{S(\tau_k)} \ar[d]_-{\mu_k} & Sk \ar[d]^-{\tau_k} \\
Sk \ar[r]_-{\tau_k} & k }
$$

$$
\xymatrix@C=3.5em@R=3em{
S^2(X \,{\otimes}\, Y) \ar[r]^-{S(\tau_{X,Y})} \ar[d]_-{\mu_{X \,{\otimes}\, Y}} & S(SX \,{\otimes}\, SY) \ar[r]^-{\tau_{SX,SY}} & S^2X \,{\otimes}\, S^2Y \ar[d]^-{\mu_X \,{\otimes}\, \mu_Y} \\
S(X \,{\otimes}\, Y) \ar[rr]_-{\tau_{X,Y}} & & SX \,{\otimes}\, SY }
$$

**Remark (the 2-categorical slogan).** Axioms (i)–(ii) say exactly that $$(S, \tau)$$ is an oplax monoidal functor $$\cat{C} \to \cat{C}$$. Axioms (iii)–(iv) say that $$\eta \maps 1 \To S$$ and $$\mu \maps S^2 \To S$$ are monoidal transformations, where $$S^2$$ carries the composite oplax structure $$\tau_{SX,SY} \circ S(\tau_{X,Y})$$. Hence

$$
\text{monoidal monad on } \cat{C} \;=\; \text{monad on } \cat{C} \text{ in the 2-category } \mathbf{MonCat}_{\mathrm{oplax}}
$$

of monoidal categories, oplax monoidal functors and monoidal transformations. Moerdijk calls these *Hopf monads*. Bruguières–Virelizier call them *bimonads*, as they carry a monad structure and a compatible "comonoidal" structure, just as a bialgebra $$H$$ gives the bimonad $$H \otimes -$$ on $$\mathbf{Vect}_k$$.

---

### 3. Algebras inherit the tensor

Write $$\mathrm{Alg}(S)$$ for the Eilenberg–Moore category, with objects $$\tilde{A} = (A, \, \alpha \maps SA \to A)$$, and $$U_S \maps \mathrm{Alg}(S) \to \cat{C}$$ for the forgetful functor with left adjoint $$F_S$$.

**Proposition.** Let $$S$$ be a monoidal monad on a tensor category $$(\cat{C}, \otimes, k, a, l, r)$$. Then the category $$\mathrm{Alg}(S)$$ of $$S$$-algebras is again a tensor category, and $$U_S$$ is strict monoidal.

*Proof.* Recall the structure maps of $$S$$:

$$
\eta_X \maps X \to SX, \qquad \mu_X \maps S^2 X \to SX, \qquad \tau_{X,Y} \maps S(X \otimes Y) \to SX \otimes SY, \qquad \tau_k \maps Sk \to k.
$$

`Unit.` $$\tilde{k} = (k, \, \tau_k \maps S(k) \to k)$$ is an $$S$$-algebra. The unit law $$\tau_k \circ \eta_k = 1_k$$ and the associativity law $$\tau_k \circ \mu_k = \tau_k \circ S(\tau_k)$$ are exactly the $$\tau_k$$-halves of (iii) and (iv).

`Tensor.` For $$\tilde{A} = (A, \alpha \maps SA \to A)$$ and $$\tilde{B} = (B, \beta \maps SB \to B)$$, define

$$
\tilde{A} \otimes \tilde{B} := \big( A \otimes B, \; S(A \otimes B) \xrightarrow{\;\tau_{A,B}\;} SA \otimes SB \xrightarrow{\;\alpha \otimes \beta\;} A \otimes B \big).
$$

To check that this is an $$S$$-algebra, we first need the unit law. It uses the compatibility of $$\eta$$ with $$\tau_{X,Y}$$ ($$\tau \circ \eta = \eta \otimes \eta$$):

$$
\xymatrix@C=4em@R=3.5em{
A \,{\otimes}\, B \ar[d]_-{\eta_{A \,{\otimes}\, B}} \ar[dr]|-{\eta_A \,{\otimes}\, \eta_B} \ar@/^1.2em/[drr]^-{1} & & \\
S(A \,{\otimes}\, B) \ar[r]_-{\tau_{A,B}} & SA \,{\otimes}\, SB \ar[r]_-{\alpha \,{\otimes}\, \beta} & A \,{\otimes}\, B }
$$

so that $$(\alpha \otimes \beta) \circ \tau_{A,B} \circ \eta_{A \otimes B} = \alpha \eta_A \otimes \beta \eta_B = 1$$.

Next, associativity. The top-right square is naturality of $$\tau$$, the bottom-right square says $$\alpha$$ and $$\beta$$ are algebras, and the left region is the compatibility (iv) of $$\mu$$ with $$\tau_{X,Y}$$:

$$
\xymatrix@C=3.5em@R=3em{
S^2(A \,{\otimes}\, B) \ar[r]^-{S(\tau_{A,B})} \ar[dd]_-{\mu_{A \,{\otimes}\, B}} & S(SA \,{\otimes}\, SB) \ar[r]^-{S(\alpha \,{\otimes}\, \beta)} \ar[d]^-{\tau_{SA,SB}} & S(A \,{\otimes}\, B) \ar[d]^-{\tau_{A,B}} \\
& S^2A \,{\otimes}\, S^2B \ar[r]^-{S\alpha \,{\otimes}\, S\beta} \ar[d]^-{\mu_A \,{\otimes}\, \mu_B} & SA \,{\otimes}\, SB \ar[d]^-{\alpha \,{\otimes}\, \beta} \\
S(A \,{\otimes}\, B) \ar[r]_-{\tau_{A,B}} & SA \,{\otimes}\, SB \ar[r]_-{\alpha \,{\otimes}\, \beta} & A \,{\otimes}\, B }
$$

For algebra maps $$h \maps \tilde{A} \to \tilde{A}'$$ and $$g \maps \tilde{B} \to \tilde{B}'$$, the map $$h \otimes g$$ is again an algebra map, by naturality of $$\tau$$. So $$\otimes$$ is a functor $$\mathrm{Alg}(S) \times \mathrm{Alg}(S) \to \mathrm{Alg}(S)$$.

`Unitors and associator.` $$\tilde{k}$$ is the unit of the tensor in $$\mathrm{Alg}(S)$$: we show $$\tilde{k} \otimes \tilde{A} \cong \tilde{A}$$, where

$$
\tilde{k} \otimes \tilde{A} = \big( k \otimes A, \; S(k \otimes A) \xrightarrow{\tau_{k,A}} Sk \otimes SA \xrightarrow{\tau_k \otimes \alpha} k \otimes A \big),
$$

via $$l_A$$. We need $$l_A$$ to be an algebra map. The upper triangle is the unit coherence (i) of $$\tau_{X,Y}$$ and $$\tau_k$$, and the lower region follows from $$\tau_k \otimes \alpha = (1 \otimes \alpha)(\tau_k \otimes 1)$$ and naturality of $$l$$:

$$
\xymatrix@C=5em@R=3em{
S(k \,{\otimes}\, A) \ar[r]^-{S(l_A)} \ar[d]_-{\tau_{k,A}} & SA \ar[dd]^-{\alpha} \\
Sk \,{\otimes}\, SA \ar[ur]|-{l_{SA}(\tau_k \,{\otimes}\, 1)} \ar[d]_-{\tau_k \,{\otimes}\, \alpha} & \\
k \,{\otimes}\, A \ar[r]_-{l_A} & A }
$$

The right unitor $$r_A$$ is symmetric. That the associator $$a_{A,B,C}$$ is an algebra map is precisely the associativity axiom (ii). The pentagon and triangle identities hold because they hold in $$\cat{C}$$, and $$U_S$$ is faithful.

`Strictness.` By construction

$$
U_S(\tilde{k}) = k, \qquad U_S(\tilde{A} \otimes \tilde{B}) = U_S(\tilde{A}) \otimes U_S(\tilde{B}) = A \otimes B,
$$

and $$U_S$$ sends the unitors and associator of $$\mathrm{Alg}(S)$$ to those of $$\cat{C}$$. So $$U_S$$ is a strict monoidal functor. $$\blacksquare$$

$$
\xymatrix@C=3em@R=3em{
\mathrm{Alg}(S) \ar[d]_-{U_S} & \tilde{A} \;=\; (A,\; SA \xrightarrow{\;\alpha\;} A) \ar@{|->}[d] \\
\cat{C} & A }
$$

The construction can be run backwards.

**Theorem** (Moerdijk). For a monad $$S$$ on a monoidal category $$\cat{C}$$ there is a bijection

$$
\left\{ \begin{array}{c} \text{opmonoidal structures} \\ (\tau_{X,Y}, \tau_k) \text{ on } S \end{array} \right\}
\;\longleftrightarrow\;
\left\{ \begin{array}{c} \text{monoidal structures on } \mathrm{Alg}(S) \\ \text{with } U_S \text{ strict monoidal} \end{array} \right\}.
$$

*Proof sketch.* Given a monoidal structure on $$\mathrm{Alg}(S)$$ strictly preserved by $$U_S$$, the unit is $$\tilde{k} = (k, \tau_k)$$ for a unique $$\tau_k \maps Sk \to k$$. Put

$$
\tau_{X,Y} \maps F_S(X \otimes Y) \longrightarrow F_S X \otimes F_S Y
$$

for the unique algebra map extending $$\eta_X \otimes \eta_Y \maps X \otimes Y \to SX \otimes SY$$. This is the transpose of $$\eta \otimes \eta$$ along $$F_S \dashv U_S$$, which is legitimate because $$F_S X \otimes F_S Y$$ is an algebra with underlying object $$SX \otimes SY$$. Explicitly $$\tau_{X,Y} = \xi_{X,Y} \circ S(\eta_X \otimes \eta_Y)$$, where $$\xi_{X,Y} \maps S(SX \otimes SY) \to SX \otimes SY$$ is the structure map of the algebra $$F_S X \otimes F_S Y$$. Axiom (iii) is the defining property of the transpose, (iv) says $$\tau_{X,Y}$$ is an algebra map, and (i), (ii) come from the unitors and associator of $$\mathrm{Alg}(S)$$ being algebra maps. The two constructions are mutually inverse. $$\blacksquare$$

---

### 4. Example: the symmetric algebra monad

`Idea.` For a vector space $$V$$ over $$k$$, let $$\Sym V$$ be the free commutative algebra over $$V$$.

`Construction.` Regard $$V$$ as a set, and consider the algebra generated by $$V$$ using the operations

1. addition and scalar multiplication: $$x, y \in V \mapsto x + y \in \langle V \rangle$$, and $$x \in V, \lambda \in k \mapsto \lambda x \in \langle V \rangle$$;
2. an associative, commutative binary operation $$x, y \mapsto x \cdot y$$,

subject to the equations $$(x \cdot y) \cdot z = x \cdot (y \cdot z)$$, $$(\lambda x) \cdot (\lambda' y) = (\lambda \lambda')(x \cdot y)$$ and $$x \cdot (y + z) = x \cdot y + x \cdot z$$.

**Proposition.** $$\Sym V$$ is a commutative graded algebra, spanned by the $$p$$-fold products $$v_1 \cdots v_p$$, that is, by elements of

$$
\Sym^p V = V^{\otimes p} / S_p, \qquad\qquad S_p \times V^{\otimes p} \longrightarrow V^{\otimes p}, \quad \big(\sigma, \, v_1 \otimes \cdots \otimes v_p\big) \longmapsto v_{\sigma(1)} \otimes \cdots \otimes v_{\sigma(p)}.
$$

`More generally.` Suppose $$(\cat{C}, \otimes, k)$$ is a symmetric monoidal category with countable coproducts, and $$V \in \cat{C}$$. Form the tensor powers $$V^{\otimes n}$$ and their countable coproduct

$$
TV = \bigoplus_{n \geq 0} V^{\otimes n} \;\in\; \cat{C}.
$$

**Q: Is $$TV$$ a monoid object in $$\cat{C}$$?** Yes, if the tensor product distributes over (these) coproducts. The unit $$k = V^{\otimes 0} \hookrightarrow TV$$ is the inclusion of a summand, and the multiplication $$m \maps TV \otimes TV \to TV$$ is

$$
\Big( \bigoplus_{m \geq 0} V^{\otimes m} \Big) \otimes \Big( \bigoplus_{n \geq 0} V^{\otimes n} \Big)
\;\cong\; \bigoplus_{m, n \geq 0} V^{\otimes m} \otimes V^{\otimes n}
\;\cong\; \bigoplus_{m, n \geq 0} V^{\otimes (m+n)}
\longrightarrow TV.
$$

In fact $$TV$$ is the *free* monoid on $$V$$. To make it commutative we symmetrise each summand.

`Action of the symmetric group.` The symmetry of $$\otimes$$ gives a group homomorphism

$$
S_n \longrightarrow \aut_{\cat{C}}(V^{\otimes n}) \subseteq \cat{C}(V^{\otimes n}, V^{\otimes n}), \qquad \sigma \longmapsto \hat{\sigma}, \qquad \hat{\sigma} \hat{\tau} = \widehat{\sigma \tau},
$$

with $$\hat{\sigma}(v_1 \otimes \cdots \otimes v_n) = v_{\sigma(1)} \otimes \cdots \otimes v_{\sigma(n)}$$ (up to the usual inverse).

Now let $$\cat{C}$$ be $$k$$-linear (hom-sets are $$k$$-vector spaces and composition is bilinear), with $$\mathrm{char}\, k = 0$$. Define

$$
p_n \maps V^{\otimes n} \to V^{\otimes n}, \qquad p_n = \frac{1}{n!} \sum_{\sigma \in S_n} \hat{\sigma}.
$$

**Lemma.** $$p_n^2 = p_n$$.

*Proof.* This is the general fact that averaging over a finite group $$G$$ is idempotent. With $$\mathrm{avg}(G) = \frac{1}{\lvert G \rvert} \sum_{g \in G} g$$ in the group algebra, for each fixed $$g$$ the map $$h \mapsto gh$$ is a bijection of $$G$$, so $$\sum_{h} gh = \sum_h h$$. Hence

$$
\mathrm{avg}(G)^2 = \frac{1}{\lvert G \rvert^2} \sum_{g \in G} \sum_{h \in G} gh = \frac{1}{\lvert G \rvert^2} \sum_{g \in G} \lvert G \rvert \, \mathrm{avg}(G) = \mathrm{avg}(G).
$$

Apply this to $$S_n \to \cat{C}(V^{\otimes n}, V^{\otimes n})$$: $$p_n^2 = \frac{1}{n!}\frac{1}{n!} \sum_{\sigma, \tau \in S_n} \widehat{\sigma \tau} = p_n$$. $$\blacksquare$$

**Example ($$n = 2$$).** $$S_2 = \{ 1, \sigma \}$$ with $$\hat{1}(v_1 \otimes v_2) = v_1 \otimes v_2$$ and $$\hat{\sigma}(v_1 \otimes v_2) = v_2 \otimes v_1$$. Then

$$
p_2(v_1 \otimes v_2) = \tfrac{1}{2}(\hat{1} + \hat{\sigma})(v_1 \otimes v_2) = \tfrac{1}{2}\big( v_1 \otimes v_2 + v_2 \otimes v_1 \big),
$$

$$
\begin{aligned}
p_2\Big( \tfrac{1}{2}(v_1 \otimes v_2 + v_2 \otimes v_1) \Big) &= \tfrac{1}{4}(v_1 \otimes v_2 + v_2 \otimes v_1) + \tfrac{1}{4}(v_2 \otimes v_1 + v_1 \otimes v_2) \\
&= \tfrac{1}{2}(v_1 \otimes v_2 + v_2 \otimes v_1).
\end{aligned}
$$

For $$n = 3$$, $$p_3$$ averages over the six symmetries of a triangle with vertices labelled $$1, 2, 3$$. Writing $$v_i v_j v_l$$ for $$v_i \otimes v_j \otimes v_l$$,

$$
p_3(v_1 v_2 v_3) = \tfrac{1}{6}\big( \underbrace{v_1 v_2 v_3 + v_2 v_3 v_1 + v_3 v_1 v_2}_{\text{rotations}} + \underbrace{v_1 v_3 v_2 + v_3 v_2 v_1 + v_2 v_1 v_3}_{\text{reflections}} \big).
$$

`Splitting.` If idempotents split in $$\cat{C}$$, we can form the "cokernel" of $$p_n$$. Write

$$
V^{\otimes n} \xrightarrow{\;r\;} \Sym^n V \xrightarrow{\;s\;} V^{\otimes n}, \qquad s r = p_n, \quad r s = 1,
$$

with $$r(v_1 \otimes \cdots \otimes v_n) = [v_1 \cdots v_n]$$.

**Remark.** If $$e \maps A \to A$$ is idempotent and $$A \xrightarrow{r} B \xrightarrow{s} A$$ splits it, then $$r$$ is a coequaliser of $$e$$ and $$1_A$$:

$$
\xymatrix@C=3.5em@R=3em{
A \ar@<0.6ex>[r]^-{e} \ar@<-0.6ex>[r]_-{1} & A \ar[r]^-{r} \ar[dr]_-{f} & B \ar@{-->}[d]^-{\exists!\, x \,=\, fs} \\
& & C }
$$

Indeed, given $$f$$ with $$fe = f$$, put $$x = fs$$. Then $$xr = fsr = fe = f$$, and if also $$x'r = f$$ then $$x' = x'rs = fs = x$$.

Then

$$
\Sym V = \bigoplus_{n \geq 0} \Sym^n V
$$

is the free commutative monoid object on $$V$$ in $$(\cat{C}, \otimes, k)$$: for every commutative monoid $$A$$,

$$
\xymatrix@C=4em@R=3em{
V \ar[r]^-{\eta_V} \ar[dr]_-{\forall f} & \Sym\,V \ar@{-->}[d]^-{\exists!\, \bar{f}} \\
& A }
$$

**Proposition.** $$\Sym$$-algebras are exactly the commutative unital $$k$$-algebras: $$\mathrm{Alg}(\Sym) \simeq k\text{-alg}$$.

**$$\Sym$$ is a monoidal monad on $$(\mathbf{Vect}_k, \otimes, k)$$.** Using the theorem of Section 3, let $$\tau_{V,W}$$ be the unique algebra map extending $$\eta_V \otimes \eta_W$$:

$$
\tau_{V,W} \maps \Sym(V \otimes W) \longrightarrow \Sym V \otimes \Sym W,
$$

$$
(v_1 \otimes w_1) \cdots (v_n \otimes w_n) \longmapsto (v_1 \cdots v_n) \otimes (w_1 \cdots w_n),
$$

$$
\tau_k \maps \Sym(k) = k[x] \longrightarrow k, \qquad x \longmapsto 1.
$$

The lifted tensor of $$\tilde{A}, \tilde{B} \in k\text{-alg}$$ is $$A \otimes_k B$$ with $$(a \otimes b)(a' \otimes b') = aa' \otimes bb'$$, with unit $$k$$. By Section 1 this is the coproduct in $$k\text{-alg}$$, and $$U_{\Sym}$$ is strict monoidal.

---

### 5. Example: the power set monad and sup-lattices

$$
\mathrm{Alg}(\mathcal{P}) \xrightarrow{\;U_{\mathcal{P}}\;} (\Set, \times, 1) \circlearrowleft \mathcal{P}, \qquad 1 = \ast = \{ \mathrm{pt} \}.
$$

Let $$\mathcal{P}$$ be the power set monad: $$\eta_X(x) = \{x\}$$ and $$\mu_X = \bigcup$$. Its algebras are sup-lattices, and the structure maps are joins: $$(X, \, \alpha \maps \mathcal{P} X \to X)$$ with $$\alpha = \bigvee$$. Write $$\mathbf{CjSLat} \simeq \mathrm{Alg}(\mathcal{P})$$ for the category of complete join semi-lattices and maps preserving all joins.

**Proposition.** The category $$\mathbf{CjSLat}$$ of complete join semi-lattices is symmetric monoidal closed.

**Definition.** If $$M, N, L$$ are sup-lattices, then $$f \maps M \times N \to L$$ is a *bimorphism* of sup-lattices if $$f$$ preserves suprema in each variable, i.e.

$$
f\Big( \bigvee_{i \in I} x_i, \, y \Big) = \bigvee_{i \in I} f(x_i, y) \qquad \text{and} \qquad f\Big( x, \, \bigvee_{j \in J} y_j \Big) = \bigvee_{j \in J} f(x, y_j).
$$

In $$\mathbf{CjSLat}$$, $$M \otimes N$$ is the codomain of the universal bimorphism:

$$
\xymatrix@C=4em@R=3em{
M \,{\times}\, N \ar[r]^-{\,{\otimes}\,} \ar[dr]_-{f} & M \,{\otimes}\, N \ar@{-->}[d]^-{\exists!\, \bar{f}} \\
& L }
$$

The tensor $$M \otimes N$$ can be obtained as a quotient of the free sup-lattice $$\mathcal{P}(M \times N)$$ on $$M \times N$$, by the equivalence relation generated by the following, so that $$M \otimes N = \mathcal{P}(M \times N) /\!\sim$$:

$$
\bigvee_{i \in I} (x_i \otimes y) \sim \Big( \bigvee_{i \in I} x_i \Big) \otimes y, \qquad \bigvee_{j \in J} (x \otimes y_j) \sim x \otimes \Big( \bigvee_{j \in J} y_j \Big).
$$

Note in particular (taking $$I = \emptyset$$) that $$0 = 0 \otimes y = x \otimes 0$$ for all $$x, y$$.

`Unit of tensor on CjSLat.` The unit is the free (complete) sup-lattice on one generator, $$\mathcal{P}1 = \{ \bot \leq \top \}$$. Then $$\mathcal{P}1 \otimes M \cong M \cong M \otimes \mathcal{P}1$$, via

$$
\mathcal{P}1 \otimes M \xrightarrow{\;\cong\;} M, \qquad \bot \otimes m \mapsto 0, \qquad \top \otimes m \mapsto m.
$$

The analogy with abelian groups is close:

| | $$\mathbf{CjSLat}$$ | $$\mathbf{AbGrp}$$ |
|---|---|---|
| tensor | $$M \otimes N = \mathcal{P}(M \times N)/\!\sim$$ | $$A \otimes B = \mathrm{Fr}_{\mathrm{Ab}}(A \times B)/\!\sim$$ |
| unit = free on one generator | $$\mathcal{P}1 = \{\bot \leq \top\}$$ | $$\bb{Z}$$ |
| "sums" | $$\bigvee_{i \in I} a_i$$, any $$I$$ | $$\sum_{i \in I} a_i$$, $$I$$ finite |
| internal hom | join-preserving maps | group homomorphisms |

**Remark (duality).** Write $$M^{\mathrm{op}}$$ for the opposite poset (category). It is again a sup-lattice, since a complete lattice has all meets. A join-preserving map $$M \to N$$ has a meet-preserving right adjoint $$N \to M$$, i.e. a join-preserving map $$N^{\mathrm{op}} \to M^{\mathrm{op}}$$. Writing $$[M, N]$$ for the internal hom (the closed structure),

$$
[M, (\mathcal{P}1)^{\mathrm{op}}] \cong [\mathcal{P}1, M^{\mathrm{op}}] \cong M^{\mathrm{op}},
$$

$$
\begin{aligned}
{[M, N]} &\cong [N^{\mathrm{op}}, M^{\mathrm{op}}] \\
&\cong [N^{\mathrm{op}}, [M, (\mathcal{P}1)^{\mathrm{op}}]] \\
&\cong [N^{\mathrm{op}} \otimes M, (\mathcal{P}1)^{\mathrm{op}}] \\
&\cong (N^{\mathrm{op}} \otimes M)^{\mathrm{op}}.
\end{aligned}
$$

Also (replacing $$N$$ by $$N^{\mathrm{op}}$$) $$M \otimes N \cong [M, N^{\mathrm{op}}]^{\mathrm{op}}$$: the tensor is given by hom.

**Remark.** All of this can be done internally: $$\mathbf{CjSLat}(\CS)$$ for any elementary topos $$\CS$$. In that case the unit is $$\mathcal{P}1 \cong \Omega$$, the subobject classifier.

**Remark (lax vs oplax).** This example is not an instance of Section 3, and the reason is worth spelling out.

On a *cartesian* monoidal category every monad is uniquely opmonoidal, via $$\tau_{X,Y} = \langle S\pi_1, S\pi_2 \rangle$$ and $$\tau_1 \maps S1 \to 1$$. For $$\mathcal{P}$$ this is $$R \mapsto (\pi_1 R, \pi_2 R)$$. The tensor it lifts to $$\mathrm{Alg}(\mathcal{P})$$ is the cartesian product $$M \times N$$ of sup-lattices (in fact a biproduct), with unit the one-point lattice.

The sup-lattice tensor instead comes from the **lax** monoidal structure: $$\varphi_{X,Y} \maps \mathcal{P}X \times \mathcal{P}Y \to \mathcal{P}(X \times Y)$$, $$(A, B) \mapsto A \times B$$, and $$\varphi_1 \maps 1 \to \mathcal{P}1$$, $$\ast \mapsto \top$$. This makes $$\mathcal{P}$$ a *commutative monad* in the sense of Kock. For a commutative monad, $$\tilde{A} \otimes \tilde{B}$$ is the reflexive coequaliser in $$\mathrm{Alg}(S)$$

$$
\xymatrix@C=6em{ F_S(SA \,{\otimes}\, SB) \ar@<0.7ex>[r]^-{F_S(\alpha \,{\otimes}\, \beta)} \ar@<-0.7ex>[r]_-{\mu \,\circ\, F_S(\varphi_{A,B})} & F_S(A \,{\otimes}\, B) } \longrightarrow \tilde{A} \otimes \tilde{B}
$$

whose maps out classify bimorphisms. The unit is the free algebra $$F_S(k)$$.
Now $$U_{\mathcal{P}}(M \otimes N) \neq M \times N$$. There is only a comparison $$M \times N \to U_{\mathcal{P}}(M \otimes N)$$, the universal bimorphism, so **$$U_{\mathcal{P}}$$ is lax monoidal but not strict**.

In slogan form: *opmonoidal monads lift the tensor, commutative monads induce a new one.*

**Remark (property vs structure).** On $$\Set$$, a set can carry many sup-lattice structures. Over $$\mathbf{Pos}$$, however, the down-set monad is a KZ (lax-idempotent) monad, so the fibres of $$\mathbf{CjSLat} \to \mathbf{Pos}$$ are propositions: being a sup-lattice is a property of a poset, not extra structure.

---

### 6. Finite vs complete joins

The free–forgetful adjunctions factor through join semi-lattices:

$$
\xymatrix@R=3.5em{
\mathbf{CjSLat} \ar@<1ex>[d]^-{U_1} \\
\mathbf{jSLat} \ar@<1ex>[u]^-{F_1} \ar@{}[u]|{\dashv} \ar@<1ex>[d]^-{U_0} \\
\Set \ar@<1ex>[u]^-{F_0} \ar@{}[u]|{\dashv} }
$$

**$$F_0$$.** For a set $$X$$, $$F_0(X)$$ is the set of finite subsets of $$X$$, and $$(F_0 X, \cup, \emptyset)$$ is the free join semi-lattice on $$X$$. For a join semi-lattice $$A$$ and a function $$f \maps X \to A$$, let $$\bar{f}$$ be the unique extension of $$f$$ to a morphism of join semi-lattices:

$$
\xymatrix@C=5em@R=3em{
X \ar[r]^-{x \,\mapsto\, \{x\}} \ar[dr]_-{f} & F_0(X) \ar@{-->}[d]^-{\bar{f}} \\
& A }
\qquad\qquad
\bar{f}(\Gamma) = \bigvee_{\gamma \in \Gamma} f(\gamma) \in A, \quad \Gamma \subseteq X \text{ finite}.
$$

**$$F_1$$.** For a join semi-lattice $$A$$, $$F_1(A) := \mathcal{I}A$$ is the set of ideals of $$A$$ (down-closed subsets closed under finite joins), and there is a full and faithful (one-to-one) map

$$
A \hookrightarrow \mathcal{I}A, \qquad a \longmapsto {\downarrow} a, \qquad {\downarrow} a \vee {\downarrow} b = {\downarrow}(a \vee b).
$$

Then $$(\mathcal{I}A, \vee, \{0\})$$ is a complete join semi-lattice, where $$I \vee J$$ is the ideal generated by $$\{ i \vee j \mid i \in I, \, j \in J \}$$. A join semi-lattice map $$g \maps A \to C$$ into a sup-lattice extends uniquely: since every ideal is the join of its principal ideals, $$I = \bigvee_{a \in I} {\downarrow} a$$,

$$
\xymatrix@C=4em@R=3em{
A \ar@{^{(}->}[r]^-{\downarrow(-)} \ar[dr]_-{g} & \mathcal{I}A \ar@{-->}[d]^-{\bar{g}} \\
& C }
\qquad\qquad
\bar{g}({\downarrow} a) := g(a), \qquad \bar{g}(I) = \bar{g}\Big( \bigvee_{a \in I} {\downarrow} a \Big) = \bigvee_{a \in I} g(a).
$$

The composite $$F_1 F_0 X = \mathcal{I}(F_0 X)$$ is the set of ideals of finite subsets, i.e. all subsets of $$X$$: $$F_1 F_0 \cong \mathcal{P}$$. Write $$F$$ for the finite power set monad $$U_0 F_0$$ and $$\mathcal{P}$$ for the power set monad. Both are commutative monoidal monads on $$(\Set, \times, 1)$$:

$$
\xymatrix@C=2em@R=3.5em{
(\mathrm{Alg}(F), \,{\otimes}\,, F1) \ar[d]_-{U_F} & & (\mathrm{Alg}(\mathcal{P}), \,{\otimes}\,, \mathcal{P}1) \ar[d]^-{U_{\mathcal{P}}} \\
(\Set, \times, 1) \;\circlearrowleft\; F & & (\Set, \times, 1) \;\circlearrowleft\; \mathcal{P} }
$$

$$
\mathrm{Alg}(F) \simeq \mathbf{jSLat}, \qquad \mathrm{Alg}(\mathcal{P}) \simeq \mathbf{CjSLat},
$$

with $$F1 = \mathcal{P}1 = \{ \bot \leq \top \}$$ as the tensor unit in both cases.

---

### 7. A degenerate example

Let $$M$$ be a commutative monoid and $$\bb{B} M$$ its delooping: one object $$\ast$$, with $$\bb{B}M(\ast, \ast) = M$$. By Eckmann–Hilton, $$\bb{B} M$$ is monoidal with both $$\otimes$$ and $$\circ$$ given by multiplication. An endofunctor is a monoid map $$\varphi \maps M \to M$$, and a monad $$(\varphi, \eta, \mu)$$ consists of elements $$\eta, \mu \in M$$. The unit laws give $$\mu \eta = 1 = \mu \varphi(\eta)$$, so $$\eta$$ is invertible. Naturality of $$\eta$$ gives $$\eta m = \varphi(m) \eta$$, so $$\varphi(m) = m$$. Hence every monad on $$\bb{B} M$$, monoidal or not, is isomorphic to the identity monad.

---

`Further Reading:`
* Kock, A. (1968) 'Monads on symmetric monoidal closed categories', Arch. Math (1970) 21: 1. https://doi.org/10.1007/BF01220868

* Moerdijk, I (2002). '[Monads on tensor categories](https://www.sciencedirect.com/science/article/pii/S0022404901000962?via%3Dihub)', Journal of Pure and Applied Algebra, Volume 168, Issues 2–3, 23 March 2002, Pages 189-208

* Simon Willerton (2008), 'A diagrammatic approach to Hopf monads', [arXiv:0807.0658](https://arxiv.org/abs/0807.0658)

* Lack, S. & Street, R. (2002) 'The formal theory of monads II', Journal of Pure and Applied Algebra
Volume 175, Issues 1–3, Pages 243-265 

* Bruguières, A. & Virelizier, A. (2007) 'Hopf monads', Advances in Mathematics 215(2), 679–733.

* Joyal, A. & Tierney, M. (1984) 'An extension of the Galois theory of Grothendieck', Memoirs of the AMS 309 (for the monoidal category of sup-lattices).
