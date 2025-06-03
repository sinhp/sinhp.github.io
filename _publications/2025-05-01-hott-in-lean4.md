---
title: "HoTTLean: Formalizing the Meta-Theory of HoTT in Lean 4"
collection: publications
permalink: /publication/2025-05-01-hott-in-lean4
excerpt: 'with Steve Awodey, Mario Carneiro, Joseph Hua, Wojciech Nawrocki, Spencer Woolfson'
venue: 'Types 2025'
date: 2025-04-15
---

[Link to publication](https://msp.cis.strath.ac.uk/types2025/abstracts/TYPES2025_paper25.pdf)

`Introduction:` While elegant synthetic proofs such as those in Homotopy Type Theory (HoTT) are expected to “compile” to proofs of classical theorems when interpreted in suitable models, this idea has not yet been exploited in proof assistants. For example, Cubical Agda supports synthetic reasoning about cubical types, but its proofs have not been translated formally to facts about cubical sets, let alone their topological realizations. The HoTTLean project aims to bridge this gap by formalizing in Lean the semantics of a type theory we call HoTT0, a fragment of HoTT where univalence holds only on set-truncated types. We define the class of natural models [Awo18]() of HoTT0, and prove that its syntax has a sound interpretation in any such model. As one concrete instance, we formalize the groupoid model of HoTT0 [HS98](), providing a specific “compilation target” for synthetic proofs. Finally, we work toward embedding HoTT0 as a domain-specific language using Lean’s extensible syntax and meta-programming facilities [UdM20](). Overall, this allows users to write synthetic proofs in HoTT0 and use the interpretation to produce constructions pertaining to groupoids as defined in Mathlib, the standard library for mathematics in Lean [Com20](). Through its compositional and modular approach, our project not only provides a bridge between synthetic and classical mathematics, but also lays the foundations for formalized semantics of other internal languages such as (complete) HoTT [Uni13]() or directed type theory [Nor19]().