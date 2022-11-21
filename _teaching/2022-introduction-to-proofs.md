---	
title: "Introduction to Proofs with Lean (Fall 2022)"		
collection: teaching		
type: "Upper level undergraduate math course"		
permalink: /teaching/2022-introduction-to-proofs
venue: "Johns Hopkins University"		
date: 2022-08-28		
---	

 
This course introduces you to the the language of mathematics and the methods of mathematical proofs. We learn the rules of logic whereby we identify strategies for proving mathematical statements based on their logical structures. We will then learn about some elementary aspects of number systems, sets, functions, relations, inductive types (such as lists, trees, graphs), algebraic structures, and metric spaces. As we learn these topics, we teach our computers every piece of mathematics we learn, that is we learn mathematics by formalizing it in <a href="https://leanprover.github.io/" target="_blank"><font color="#68ACE5">Lean</font></a> interactive proof assistant. Formalization can be seen as a kind of computer programming: we will write mathematical definitions, theorems, and proofs in a  language that Lean can understand. In return, Lean provides instant feedback, helps us with writing our proofs and ultimately certifies the correctness of our proofs.

This course does not have any mathematical prerequisite, however, it is expected that you are familiar with basic high-school algebra. Although a basic programming experience can go far toward your excelling in this course, we actually don’t presuppose any background in formalization or in programming. 



### Course website 

[https://introproofs.github.io/](https://introproofs.github.io/s22/)



### Course Github Repository

- [ProofLab](https://github.com/sinhp/ProofLab )
  
- [Code Lectures](https://github.com/sinhp/ProofLab/tree/main/src/lectures)
  
- [Lecture Recordings](https://zoom.us/rec/share/Ey-JIyn13674zrkhQzWQjNM95EWkIj9o29yOlq_TQEJeiBS8ozNAn9pwTJ-8o0eN.m8igrUHwHN1v0BuG?startTime=1664818693000)


### What does Lean add? 

The main objective of adding Lean to this course was to improve understanding and facilitating the creation of proofs, as opposed to the main use of a proof assistant which is to formalize new mathematics. We use Lean for: 

-  checking the validity of our proofs, 
-  getting instant feedback to help students see potential mistakes in their mathematical reasoning and helping them with completing their proofs, 
-  formalizing and digitizing proofs thereby allowing students to have easier access to background knowledge on demand,
-  achieving a deeper understanding of many aspects of our pen-and-paper proofs by formalizing them.
- basic computation (with numbers, matrices, polynomials)

### Zulip Server
Lectures, homework, announcement, etc are announced on the [Zulip server](https://introproofs.zulipchat.com/login/) of the course. Plus, there is a very active stream of questions and answers where we debug code in real time. 


### Teaching workflow 

Teaching with a proof assistant has a very different workflow than the usual whiteboard/blackboard lectures or slide presentations. There is a different dynamic. More preparation is needed as there is always chance of things going wrong with live coding. One needs to make sure one imports the correct code libraries and make suitable dependencies. 

Here's my workflow in teaching with Lean : I usually spend about twenty to thirty minutes lecturing about the key concepts of each lesson, often sketching some informal and non-rigorous figures. We then spend the rest of class time (roughly about 45-55 minutes) to make these ideas precise and rigorous by writing our proofs in Lean.

I have only eight students, and I make them into 4 teams (rotating teams each lecture). For every line of code, I wait until the team whose turn it is to suggest a solution to the current Lean goal, and then I type their solution. If Lean gives us an error, I explain the error, and then I go to the next team and ask them if they have a solution. If no team at all gives a solution to the current goal, and this happened very rarely so far, I write my own solution, and we move on to the next lemma/theorem.

This semester, so far, everyone seems to be enthusiastic, and we usually end up proving some statement in multiple ways, since different students/teams like to propose their own distinct solutions with their own favorite tactic. For instance, some students love `apply`, some others are addicted to `have`, and two students who use `calc` whenever possible. 



		
