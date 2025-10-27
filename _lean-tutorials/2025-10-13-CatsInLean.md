---
layout: single
title: "A User's Guide to Category Theory in Lean"
collection: lean_tutorials
permalink: /lean-tutorials/2025-10-13-CatsInLean
excerpt: 'Principles, tips and tricks'
date: 2025-10-13
use_math: true
author_profile: false
toc: true
toc_sticky: true
---

<!-- {% include toc %} -->

<!-- # What Are Categories? -->

At the most basic level, a category is a collection of objects and morphisms (arrows) between them, satisfying certain axioms. Categories may appear as categories of mathematical structures and the transformations between instances of certain structures, e.g. the category of groups, where the objects are groups and the morphisms are group homomorphisms. Category theory studies these structures and their relationships using the language of categories. In developing mathematics using category theory, we isolate phenomena that hold for purely formal reasons from those whose proofs require techniques particular to a given structure or a specific way of constructing objects. The advantage of category-theoretic approach is that it allows us to construct objects and prove theorems in a way that scale better, since a formal category-theoretic argument is agnostic to the specific foundation (e.g. ZF(C) set theories, type theories, etc.), can be reproduced in a wide variety of contexts, and can be applied to many different situations. For instance, the idea of adjoining formal inverses for some elements in an algebraic structure (e.g. monoids, commutative rings, etc.) are instances of a formal construction called localization (aka category of fractions). 

Further, category theory provides us with linguistic tools to describe mathematical phenomena which were previously inexpressible: universal properties, adjunctions, duality, natural transformations, canonical maps, uniqueness up to a contractible space of choice, coherence, and more. Many of the basic objects of study in modern algebraic topology, algebraic geometry, and homological algebra would be impossible to define without category theoretic language. Category theory is the best organizational tool for mathematical structures we know. It also acts as a central hub connecting many disparate scientific disciplines. 


# Categories in Lean 4

Lean is very much a community-driven evolving system, and the category theory library is no exception. In fact, the category theory library has gone through several iterations of crucial API redesigns. As such it is important to bear that in mind and take some of the code in below with caution. The code on mathlib gets updated, refactored, and sometimes migrated to a different module. This may mean that some of the code snippets below may not be up-to-date and some of the links to mathlib4 documentation may not point to the correct place, or nowhere at all. If you come across such issues, please do let me know. My contact is on the home page of this website.

Alright, the warning is out of the way, let's get started. 


## First-Order Language of Categories

One can encode the language of categories as a kind of first-order language (more precisely, an essentially algebraic theory) as follows: There is a sort $Obj$ for objects, a sort $Mor$ for morphisms, and functions $src, tgt : Mor \rightarrow Obj$ for the source and target of a morphism. There is a function $id : Obj \rightarrow Mor$ assigning to each object its identity morphism, and a partial function $comp : Mor \times Mor \rightharpoonup Mor$ for composition of morphisms, defined on pairs $(f,g)$ where $tgt(f) = src(g)$. By partial function, we mean that $comp$ is not defined for all pairs of morphisms, but only for those that are composable. One way to make this precise is to define $comp$ as a binary relation symbol on $Mor \times Mor \times Mor$, where $comp(f,g,h)$ means that $f$ and $g$ are composable and their composition is $h$. In particular we add an axioms stating that if $comp(f,g,h)$ holds, then $tgt(f) = src(g) \wedge tgt(g) = src(h) \wedge src(f) = src(h)$.

The axioms are that composition is associative and that identity morphisms act as identities for composition. You can write them as first-order sentences if you like:
- $\forall f \in Mor, comp \, (id \, (src \, f), f) = f \wedge comp \, (f, id \, (tgt \, f)) = f$
- $\forall f,g,h \in Mor, tgt(f) = src(g) \wedge tgt(g) = src(h) \Rightarrow comp \, (comp \, (f,g), h) = comp \, (f, comp \, (g,h))$

Usually, we can add a bit of syntactic sugar for better ergonomics. We write $X \xrightarrow{f} Y$ to mean that $f$ is a morphism with source $X$ and target $Y$, $f \in Mor$ with $src(f) = X$ and $tgt(f) = Y$. We can write $X \xrightarrow{f} Y \xrightarrow{g} Z$ to mean that $f$ and $g$ are composable morphisms, and we can write $X \xrightarrow{f} Y \xrightarrow{g} Z \xrightarrow{h} W$ to mean that $f,g,h$ are composable triples. We can write $g \circ f$ for $comp(f,g)$, and we can write $1_X$ for $id(X)$. With this notation the axioms become:
- $\forall X \in Obj, \forall f : X \xrightarrow{} Y, 1_Y \circ f = f \wedge f \circ 1_X = f$
- $\forall f : W \xrightarrow{} X, \forall g : X \xrightarrow{} Y, \forall h : Y \xrightarrow{} Z, (h \circ g) \circ f = h \circ (g \circ f)$

You can absolutely formalize this in Lean. All you need to do is to define the following structure:

```c
structure MyCategory where
    Obj : Type u
    Mor : Type v
    src : Mor → Obj
    tgt : Mor → Obj
    id : Obj → Mor
    comp (f g : Mor) : (tgt f = src g) → Mor
    id_src : ∀ (x : Obj), src (id x) = x
    id_tgt : ∀ (x : Obj), tgt (id x) = x
    comp_src : ∀ {f g : Mor} (h : tgt f = src g), src (comp f g h) = src f
    comp_tgt : ∀ {f g : Mor} (h : tgt f = src g), tgt (comp f g h) = tgt g
    comp_id_left : ∀ {f : Mor}, comp (id (src f)) f = f
    comp_id_right : ∀ {f : Mor}, comp f (id (tgt f)) = f
    comp_assoc : ∀ {f g k : Mor} (h1 : tgt f = src g) (h2 : tgt g = src k),
      comp (comp f g h1) k h2 = comp f (comp g k h2) h1
```

We can even formalize the first-order language of categories in Lean and study its models.
First-order languages are formalized in Lean, see [`Mathlib.ModelTheory.Syntax`](https://leanprover-community.github.io/mathlib4_docs/Mathlib/ModelTheory/Syntax.html#FirstOrder.Language.Theory). 

## A (Dependent) Type Theoric Formalization of Categories

It was rather telling that the first ergonomics notation we introduced above was $X \xrightarrow{f} Y$. This is because working with categories in practice, we really don't care much about the total collections of all morphisms, rather we care about morphisms between specific objects. For instance in any category of spaces the morphisms $1 \rightarrow X$ are the points of $X$. Or in the category of toposes, for any geometric theory $\mathbf{T}$, there is a classifying topos $\mathbf{Set}[\mathbf{T}]$ such that for any Grothendiek topos $\mathcal{E}$, the morphisms $\mathcal{E} \to \mathbf{Set}[\mathbf{T}]$ are in one-to-one correspondence with the models of $\mathbf{T}$ in $\mathcal{E}$. In the topological spaces $X \to \mathbf{B} G$ are $G$-torsors on $X$, or in the category of semirings, $\mathbb{N} [X] \to R$ is the underlying set of $R$.

The notation $X \xrightarrow{f} Y$ is actually a dependent type notation.  The morphism $X \xrightarrow{f} Y$ is not just an element of some type $Mor$, but it is an element of a type that depends on the objects $X$ and $Y$. Other than these conceptual considerations, the dependent type theoretic formalization of categories is syntactically more concise and cleaner. No preconidtion is needed to compose morphisms, and the axioms are simpler to state.

Categories are implemented using type classes. If you have not seen type classes before, one useful way to think about a type class is as a record (or structure) where there is a usually a canonical instance of that said structure for a given type. For instance, the `Add` type class is a structure that has a binary operation `add : α → α → α`, and for many types `α` there is a canonical way to add two elements of `α`. For example, for `Nat` the canonical addition is the usual addition of natural numbers, and for `List α` the canonical addition is list concatenation. When you declare a type class `instance` for a type, you are telling Lean what the canonical way to add two elements of that type is. You can discover the instance of additions on polynomials using `#synth Add (Polynomial R)` upon which LeanInfoView displays `Polynomial.add'` and further inspection reveals that it is defined as follows:
```
private irreducible_def add : R[X] → R[X] → R[X]
  | ⟨a⟩, ⟨b⟩ => ⟨a + b⟩
```
Here `R[X]` is the type of polynomials with coefficients in `R`, implemented as sequences `ℕ → R` of coefficients with finite support. The addition of two polynomials is then defined by the addition their underlying functions. 

Then, when you use the `+` operator for adding two polynomials in your code, Lean will automatically find the appropriate instance of the `Add` type class for polynomials and use the `add` function defined in that instance to perform the addition. Of course this picture gets soon very complicated, as we add more type classes and instances to the mix, and Lean has to search through a potentially large number of instances to find the right one. This search is known as the type class inference or instance synthesis or resolution (although resolution is a more general term that applies to other kinds of inference as well).
To see how this was implemented in Lean, you can check out "Tabled Typeclass Resolution" paper by Selsam, Ullrich, and de Moura.
<!-- 
here: https://arxiv.org/abs/2001.04301 (page 11) -->

All this to say that categories are implemented as a type class in Lean. As usual, refactoring is a good idea for complex structures, and so the `Category` type class extends a more basic `CategoryStruct` type class which in turn extends a `Quiver` type class. A quiver is a directed graph, i.e. a collection of objects and morphisms between them, without any composition or identity morphisms.

```c
class Quiver (V : Type u) where
  Hom : V → V → Sort v
```  

The following type class extends `Quiver` by adding identity morphisms and composition of morphisms, so the structure of a category without the axioms. 

```c
class CategoryStruct (obj : Type u) : Type max u (v + 1) extends Quiver.{v + 1} obj where
  id : ∀ X : obj, Hom X X
  comp : ∀ {X Y Z : obj}, (X ⟶ Y) → (Y ⟶ Z) → (X ⟶ Z)
```

You have perhpas noted that this definition uses two universe levels `u` and `v`. The level `u` controls the size of the type of objects, while the level `v` controls the size of the type of morphisms. I will comment more on universe levels later in the following sections.

Finally the `Category` type class adds the axioms of a category:

```c
class Category (obj : Type u) : Type max u (v + 1) extends CategoryStruct.{v} obj where
  id_comp : ∀ {X Y : obj} (f : X ⟶ Y), 𝟙 X ≫ f = f 
  comp_id : ∀ {X Y : obj} (f : X ⟶ Y), f ≫ 𝟙 Y = f
  assoc : ∀ {W X Y Z : obj} (f : W ⟶ X) (g : X ⟶ Y) (h : Y ⟶ Z), (f ≫ g) ≫ h = f ≫ g ≫ h
```

The formalization of categories in [`Mathlib.CategoryTheory.Category.Basic`](https://leanprover-community.github.io/mathlib4_docs/Mathlib/CategoryTheory/Category/Basic.html). has slighyly more in it and has some automation baked in. 

```c
@[pp_with_univ, stacks 0014]
class Category (obj : Type u) : Type max u (v + 1) extends CategoryStruct.{v} obj where
  id_comp : ∀ {X Y : obj} (f : X ⟶ Y), 𝟙 X ≫ f = f := by cat_disch
  comp_id : ∀ {X Y : obj} (f : X ⟶ Y), f ≫ 𝟙 Y = f := by cat_disch
  assoc : ∀ {W X Y Z : obj} (f : W ⟶ X) (g : X ⟶ Y) (h : Y ⟶ Z), (f ≫ g) ≫ h = f ≫ g ≫ h := by
    cat_disch
```

### Notations

We use the `⟶` (type it in VSCode with the command `\hom`) arrow to denote sets of morphisms, as in `X ⟶ Y`.
This leaves the actual category implicit; it is inferred from the type of `X` and `Y` by typeclass inference.

We use `𝟙` (type `\b1`) to denote identity morphisms, as in `𝟙 X`.

We use `≫` (type `\gg`) to denote composition of morphisms, as in `f ≫ g`, which means "`f` followed by `g`".
You may prefer write composition in the usual convention, using `⊚` (type `\oo` or `\circledcirc`), as in `f ⊚ g` which means "`g` followed by `f`". To do so you'll need to add this notation locally, via

```c
local notation f ` ⊚ `:80 g:80 := category.comp g f
```

We use `≅` (type `\cong`) for isomorphisms.


### Functors and Natural Transformations

Functors (which are a structure, not a typeclass) are defined in [`Mathlib.CategoryTheory.Functor.Basic`](https://leanprover-community.github.io/mathlib4_docs/Mathlib/CategoryTheory/Functor/Basic.html),
along with identity functors and functor composition.

We use `⥤` (`\func`) to denote functors, as in `C ⥤ D` for the type of functors from `C` to `D`.

We use `F.obj X` to denote the action of a functor on an object.

We use `F.map f` to denote the action of a functor on a morphism`.

Functor composition can be written as `F ⋙ G`.

Natural transformations, and their compositions, are defined in [`Mathlib.CategoryTheory.NatTrans`](https://leanprover-community.github.io/mathlib4_docs/Mathlib/CategoryTheory/NatTrans.html).

The category of functors and natural transformations between fixed categories `C` and `D`
is defined in [`Mathlib.CategoryTheory.Functor.Category`](https://leanprover-community.github.io/mathlib4_docs/Mathlib/CategoryTheory/Functor/Category.html).

We use `τ.app X` for the components of a natural transformation. 

<code>  τ.app X : F.obj X ⟶ G.obj X</code>

Otherwise, we mostly use the notation for morphisms in any category:

We use `F ⟶ G` (`\hom` or `-->`) to denote the type of natural transformations, between functors
`F` and `G`.
We use `F ≅ G` (`\iso`) to denote the type of natural isomorphisms.

For vertical composition of natural transformations we just use `≫`. For horizontal composition,
use `hcomp`.

### Operations on Categories

Cartesian products of categories, functors, and natural transformations appear in
[`Mathlib.CategoryTheory.Products.Basic`](https://leanprover-community.github.io/mathlib4_docs/Mathlib/CategoryTheory/Products/Basic.html).

The category of types, and the hom pairing functor, are defined in [`Mathlib.CategoryTheory.Types`](https://leanprover-community.github.io/mathlib4_docs/Mathlib/CategoryTheory/Types.html).


### Limits and Colimits

<button>_TODO_</button>

#### Terminal objects 

You should use hypothesis of the form `(X : C) (h : IsTerminal X)` rather than `HasTerminal C`, since the former is more general, it is more constructive, and works in more situations. Here's an example: let's say we want to define a functor from a category `C` to the slice category over the terminal object in `C`. We can do this as follows:

```c
def Functor.toOverTerminal' [HasTerminal C] : C ⥤ Over (⊤_ C) :=
  Functor.toOverTerminal (⊤_ C) (terminalIsTerminal)
```

Note that `⊤_ C` is a choice of a terminal object in `C` from the assumption `HasTerminal C`. This choice is made by the non-constructive axiom of choice. In mathlib we prefer the following more general and more constructive definition:

```c
def Functor.toOverTerminal (X : C) (h : IsTerminal X) : C ⥤ Over X where
  obj X := Over.mk <| h.from X
  map {X Y} f := Over.homMk f
```

Now we obtain `Functor.toOverTerminal'` as a special case of `Functor.toOverTerminal` by supplying a specific terminal object and a proof that it is terminal.

```c
def Functor.toOverTerminal' [HasTerminal C] : C ⥤ Over (⊤_ C) :=
  Functor.toOverTerminal (⊤_ C) (terminalIsTerminal)
```

### Equality of objects 

<button>_Unfinished (wip)_</button>

In category theory, we usually avoid talking about equality of objects. The philosophically correct notion of sameness (identity) in categories is isomorphism. Obsiously an object `X` is equal to itself and there is an identity morphism `𝟙 X : X ⟶ X`, which in fact in an isomorphism (this is a theorem!), and therefore `X` is identical to itself in this broader notion of 
identity. 

Since a category is implemented as a type class structure in Lean, we can always ask whether two objects are equal using the built-in equality relation of the carrier type. If `X Y : C` are objects in a category `C`, the expression `X = Y` is well-typed and has the type `Prop`. If you want to assert equality of objects in your hypotheses, you can do so using `h : X = Y` where `h` is a proof of the equality. However, if you look through the mathlib4 category theory library, you will find that equality of objects is rarely used. Instead, we use isomorphisms. Even if `X` and `Y` happen to be equal as objects with the witness `h : X = Y`, we usually prefer to work with the isomorphism `eqToIso h : X ≅ Y` induced by the equality proof `h`. In mathlib4, the equality type is defined inductively with only one constructor: 
```c
inductive Eq : α → α → Prop where
  /-- `Eq.refl a : a = a` is reflexivity, the unique constructor of the
  equality type. See also `rfl`, which is usually used instead. -/
  | refl (a : α) : Eq a a
```  
So we can define `eqToIso` by recursion on the equality proof `h`, so that if `h` is `rfl` (i.e. reflexivity proof), then `eqToIso h` is the identity isomorphism `iso.refl X`.

Aside from the philosophical considerations, there are practical reasons to avoid equality of objects for doing category theory in Lean. The main reason is that the implementation of categories as a dependent type, that is the type of morphisms `X ⟶ Y` depends on the objects `X` and `Y`. This soon leads to problems with rewriting along equalities dependent on other equalities. 

```c
variable {C D E : Type*} [Category C] [Category D] [Category E] 
    (F G : C ⇒ D) (H : D ⇒ E)

example {X Y : C} (f : X ⟶ Y) (h : F ⋙ H = G ⋙ H) [IsIso (H.map (F.map f))] :
   IsIso (H.map (G.map f)) := by 
   rw [← Functor.comp_map]
   rw [← h]

```
The first line after `by` changes the goal from `IsIso (H.map (G.map f))` to `IsIso ((G ⋙ H).map f)`. After that we would like to replace `G ⋙ H` with `F ⋙ H` using the equality proof `h`. 



```c
CategoryTheory.Over.mk_left.{v₁, u₁} {T : Type u₁} [Category.{v₁, u₁} T] {X Y : T} (f : Y ⟶ X) : (Over.mk f).left = Y
```