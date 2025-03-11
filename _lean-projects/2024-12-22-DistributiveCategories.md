---
title: "Monoidal and Cartesian Distributive Categories in Lean 4"
collection: lean
permalink: /lean/2024-12-22-DistributiveCategories
excerpt: ''
date: 2024-12-22
link: https://github.com/leanprover-community/mathlib4/pull/20182
---

This PR defines monoidal and cartesian distributive categories, develop the API, and prove some main results. We show a closed monoidal category is distributive.

We also show that, for a category `C` with binary coproducts, the category of endofunctors `C ⥤ C` is left distributive. This requires the following new file which develops a convenient API for the binary (co)products in the functor categories:
`CategoryTheory/Limits/FunctorCategory/Shapes/BinaryProducts`

In `Mathlib/CategoryTheory/Distributive/Cartesian` we show that the coproduct coprojections are monic in a cartesian distributive category.