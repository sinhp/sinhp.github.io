---
layout: archive
title: "Lean Interactive Theorem Prover"
permalink: /lean-projects/
author_profile: true
---


<h2><font color="#800020"> Formalization Projects </font></h2>
{% include base_path %}
{% for post in site.lean-projects reversed %}
  {% include archive-single-lean.html %}
{% endfor %}

<!-- {% include base_path %}
{% for post in site.lean reversed %}
  {% include archive-single-lean.html %}
{% endfor %} -->


<h2><font color="#800020">Linear Algebra Game</font></h2>
With Alex Bentkamp, Jon Eugester, and Marcus Zibrowius, we developed the <a href="https://adam.math.hhu.de/#/g/hhu-adam/robo"><font color="#800020">Linear Algebra Game</font></a> for teaching a seminar course on proof-based linear algebra to undergraduate students at Heinrich Heine University, Düsseldorf. We also maintain the <a href="https://adam.math.hhu.de"><font color="#800020">Lean Game Server</font></a>. You can make your own game using the <a href="https://github.com/hhu-adam/GameSkeleton"><font color="#800020">Game Skeleton</font></a>.

<!-- See more about this in the following link below from a talk I gave at the Hausdorff Research Institute in Mathematics (HIM), Bonn.  -->

<!-- <a href="https://www.youtube.com/watch?v=f8LuzA7k4K4"><i class="fa fa-fw fa-youtube" aria-hidden="true"></i> Linear Algebra Game in Lean4</a> -->


<h2><font color="#800020"> Contribution to Mathlib </font></h2>

- [Locally Cartesian Closed Categories ](https://github.com/leanprover-community/mathlib4/pull/22321)
- [Monoidal and Cartesian Distributive Categories](https://github.com/leanprover-community/mathlib4/pull/20182)
- [Grothendieck construction for category-valued functors](https://github.com/leanprover-community/mathlib4/blob/master/Mathlib/CategoryTheory/Grothendieck.lean)
- [Cartesian closedness of sheaf categories, with Dagur Asgeirsson, Jon Eugster](https://github.com/leanprover-community/mathlib4/pull/15262)
- [Stonean is precoherent, with Dagur Asgeirsson, Jon Eugster, Boris Bolvig Kjær, Nima Rasekh](https://github.com/leanprover-community/mathlib4/pull/6725)
- [Grothendieck construction for type-valued functors](https://github.com/leanprover-community/mathlib4/blob/master/Mathlib/CategoryTheory/Elements.lean)
- [ExtrDisc is precoherent, with Dagur Asgeirsson, Jon Eugster, Boris Bolvig Kjær, Nima Rasekh](https://github.com/leanprover-community/mathlib4/pull/5861)
- [Profinite is precoherent](https://github.com/leanprover-community/mathlib4/pull/5858)
- [Various basic API lemmas in set theory](https://github.com/leanprover-community/mathlib4/blob/master/Mathlib/Data/Set/Basic.lean)
- [Triple adjunctions of slice cateogries](https://github.com/leanprover-community/mathlib4/pull/14519)
- [Wide subcategories]()

<h2><font color="#800020"> Teaching with Lean Interactive Theorem Prover</font></h2>

<h3> Introduction to Proofs </h3>

1. [Johns Hopkins University, Fall 2023](https://github.com/sinhp/ProofLab4/tree/master)
2. [Johns Hopkins University, Fall 2022](https://sinhp.github.io/teaching/2022-introduction-to-proofs-with-Lean)
3. [Johns Hopkins University, Spring 2022](https://introproofs.github.io/s22)
4. [Johns Hopkins University, Fall 2021](https://introproofs.github.io/jhu301-f21/)

