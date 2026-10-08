---
title: "A Certifying Proof Assistant for Synthetic Mathematics in Lean"
collection: publications
permalink: /publication/2026-01-08-cpp-HoTTLean
venue: 'CPP 2026'
date: 2026-01-08
paperurl: 'https://dl.acm.org/doi/10.1145/3779031.3779087'
---

<h7> <strong> with S. Awodey, M. Carneiro, J. Hua, W. Nawrocki, Shuge Rong , Yiming Xu \ </strong></h7>

![A Certifying Proof Assistant for Synthetic Mathematics in Lean]({{ base_path }}/images/SynthMath-cpp-paper.png)

**Abstract.** *Synthetic* theories such as homotopy type theory axiomatize classical mathematical objects such as spaces up to homotopy. Although theorems in synthetic theories translate to theorems about the axiomatized structures on paper, this fact has not yet been exploited in proof assistants. This makes it challenging to formalize results in classical mathematics using synthetic methods. For example, Cubical Agda supports reasoning about cubical types, but cubical proofs have not been translated to proofs about cubical set models, let alone their topological realizations. To bridge this gap, we present SynthLean: a proof assistant that combines reasoning using synthetic theories with reasoning about their models. SynthLean embeds Martin-Löf type theory as a domain-specific language in Lean, supporting a bidirectional workflow: constructions can be made internally in Martin-Löf type theory as well as externally in a model of the theory. A certifying normalization-by-evaluation typechecker automatically proves that internal definitions have sound interpretations in any model; conversely, semantic entities can be axiomatized in the syntax. Our implementation handles universes, Σ, Π, and identity types, as well as arbitrary axiomatized constants. To provide a familiar experience for Lean users, we reuse Lean’s tactic language and syntax in the internal mode, and base our formalization of natural model semantics on Mathlib. By taking a generic approach, SynthLean can be used to mechanize various interpretations of internal languages such as the groupoid, cubical, or simplicial models of homotopy type theory in HoTTLean.
