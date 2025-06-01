---
title: "Extensionality vs Intensionality in Logic"
author: Sina Hazratpour
excerpt: ""
category: research notes
tags: extensionality, intensionality, logic, modal logic
permalink: /scribbling/20-03-2025-extensionality-vs-intensionality
collection: notes
type: "scribbling"
date: 20-03-2025
use_math: true
---

<!-- {% include macro %} -->

You might have come the words "extensionality" and "intensionality" in logic, type theory, interactive theorem proving, etc. Sometimes you hear people say Martin-Löf Type Theory (MLTT) is an intensional type theory, first order logic is an extensional, modal logic is intensional, etc. But why? What does it mean for a logic to be intensional or extensional? You might also have heard of things like _axiom of function extensionality_, or the _axiom of proposition extensionality_. Is the word "extensionality" used in the same sense here?

The German philosopher Gottlob Frege introduced the distinction between _intension_ and _extension_ to logic: In his terminology, it is the difference between the _Sinn_ (sense) and the _Bedeutung_ (reference) of a concept. 


Frege's 1982 paper "Über Sinn und Bedeutung" starts as follows:

> Equality gives rise to challenging questions which are not altogether easy to answer.
Is it a relation? A relation between objects, or between names or signs of objects? In
my Begriffschrift I assumed the latter. The reasons which seem to favour this are the
following: $a = a$ and $a = b$ are obviously statements of differing cognitive value; $a = a$ holds a priori and, according to Kant, is to be labeled analytic, while statements of
the form $a = b$ often contain very valuable extensions of our knowledge and cannot
always be established a priori. The discovery that the rising sun is not new every
morning, but always the same, was one of the most fertile astronomical discoveries.
Even to-day the identification of a small planet or a comet is not always a matter of
course. Now if we were to regard equality as a relation between that which the
names '$a$' and '$b$' designate, it would seem that $a = b$ could not differ from $a = a$ (i.e.
provided $a = b$ is true). A relation would thereby be expressed of a thing to itself,
and indeed one in which each thing stands to itself but to no other thing. 

This is already very interesting and adumberates the distinction between definitional/judgmental equality and propositional equality that we are familiar from type theory. From what I understand, Frege's concern in above
is the propositional equality, and he says the propositional equality $a = b$ is a relation between that which the
names '$a$' and '$b$' designate. Frege continues:

> What is intended to be said by $a = b$ seems to be that the signs or names '$a$' and '$b$'
designate the same thing, so that those signs themselves would be under discussion;
a relation between them would be asserted. But this relation would hold between the
names or signs only in so far as they named or designated something. It would be
mediated by the connexion of each of the two signs with the same designated thing.
But this is arbitrary. Nobody can be forbidden to use any arbitrarily producible event
or object as a sign for something. In that case the sentence $a = b$ would no longer
refer to the subject matter, but only to its mode of designation; we would express no
proper knowledge by its means. But in many cases this is just what we want to do. If
the sign '$a$' is distinguished from the sign 'b' only as object (here, by means of its
shape), not as sign (i.e. not by the manner in which it designates something), the
cognitive value of $a = a$ becomes essentially equal to that of $a = b$, provided $a = b$ is
true. A difference can arise only if the difference between the signs corresponds to a
difference in the mode of presentation of that which is designated. Let $a, b, c$ be the
lines connecting the vertices of a triangle with the midpoints of the opposite sides.
The point of intersection of $a$ and $b$ is then the same as the point of intersection of $b$
and $c$. So we have different designations for the same point, and these names ('point
of intersection of $a$ and $b$,' 'point of intersection of $b$ and $c$') likewise indicate the
mode of presentation; and hence the statement contains actual knowledge.

## Definitional equality vs propositional equality

The difference between an intension and an extension in contemporary logic comes from Frege, who distinguishes a concept's Sinn (sense) from its Bedeutung (reference).

The easiest way to illustrate the difference between sense and reference is through cases. The predicates "having a kidney" and "having a heart" clearly have different senses, but as a matter of contingent fact everything that has a kidney has a heart: hence we case the two terms are co-referential. The set of the renates = the set of the cordates, because set membership is extensional. First order logics, including set theory are all extensional in this sense. It doesn't matter whether we are talking about the set of the renates or the set of the cordates, because they are the same set, and we know they're the same set, because we define a set extensionally--i.e. purely by the reference of the terms. We don't need to know what the terms "renate" and "cordate" really mean, we just need to know which things they refer to.

An intensional logic, however we do need to know what the terms mean, because we want to ask not just about which things do, as a matter of contingent fact, happen to fall under those terms. For instance, modal logic is an intensional logic. Take the set of all things that have hearts. The sentence, "every renate is a cordate" can be checked by examining every item in the domain and checking that all the things that actually have kidneys also actually have hearts. But, "Necessarily, every renate is a cordate" can't be checked this way. Even if it is the case that all renates are actually cordates, this is just a contingent fact. So to establish the truth or falsity of the modal sentence requires me to have some kind of model that isn't just looking at the referents of the terms "renate" and "cordate", it's going to have to have something to do with knowing the meaning of the terms, etc.

It is because modal logic isn't extensional that lots of people in the first half of the 20th century were suspicious of it. (Think of Quine here.) That's the neat thing about Kripke style model theory for modal logic. It provides something that looks a lot like extensional semantic theory for an intensional logic. It doesn't make modal logic extensional, but it does open up the possibility of using nice model theoretical techniques that were designed for extensional logics on modal logic as well. Since getting access to those techniques, we can prove consistency, and some other metalogical results for some modal logics, which have led to renewed interest in these logics among philosophers.

There are other intensional logics as well. Modal logic is just one prominent example.
