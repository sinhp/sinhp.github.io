---
collection: talks
title: "Formalization of Polynomial Functors in Lean 4"
permalink: /talks/Poly-Lean4-SwissMath
type: "SMS Spring Meeting on Formalization and Proof Assistants (March 25 - 27, 2026)"
venue: "Brig, Switzerland"
date: 2026-03-25
excerpt: "" 
---


<a href="/files/CT/SMS-poly-slides.pdf" target="_blank"> <i class="fa fa-file-pdf-o" aria-hidden="true"></i> Polynomial Functors in Lean 4 </a>

`Event URL` : [SMS Spring Meeting on Formalization and Proof Assistants](https://unidistance.ch/en/event/sms-spring-meeting-formalization-and-proof-assistants)



#### Abstract: 

Polynomial functors are one of the most useful tools in category theory. They have wide-ranging applications across functional programming, the semantics of dependent type theories, combinatorial species, and higher algebra. This talk presents a comprehensive formalization of polynomial functors in the Lean 4 proof assistant.

We begin by exploring the categorification of polynomials, moving from standard algebraic representations to modeling polynomial functors in the Category of Types and then generalizing to arbitrary Locally Cartesian Closed Categories (LCCCs), and then to general categories with two specified interrelated class of maps. We will discuss the challenges of implementing these concepts in Lean 4, including the need for a new API that for pullbacks that gives a better computational behavior for the applications we have in mind. This approach computes well and naturally induces cartesian monoidal structures on slice categories.

Furthermore, to avoid the long and tedious proofs that typically result from chaining the universal properties of various pullbacks and pushforwards, we refactored our formal proofs using the 2-categorical calculus of mates. This technique is purely equational, completely avoiding universal properties, and reduces the proofs of certain isomorphisms to checking the equality of horizontal and vertical pasting squares up to definitional equality.

Finally, we will demonstrate downstream applications—specifically, how this library serves as a crucial foundation for the [*HoTTLean*](https://github.com/sinhp/HoTTLean/tree/master/HoTTLean) project in doing synthetic homotopy theory and modeling type formers via Natural Models. We will conclude with a brief look at future directions, such as multivariable polynomials, formal differentiation, and applications to dynamical systems and open games.
