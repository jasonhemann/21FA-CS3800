---
title: "Homework 11"
layout: single
---

### Objectives 

  - Explore Poly-time reduction in the context of classes P, NP

**Homework Problems**

* Freebie for submitting (1 pts)

* [Mirrored](#1-mirrored) (3 pts, manually graded)

* [EULPATHCOMP](#2-eulpathcomp) (3 pts, manually graded)

* [UNDIRHAMPATH](#3-undirhampath) (3 pts, manually graded)

**Total**: 10 points

**Submitting**

Submit this assignment on [Gradescope](https://www.gradescope.com).

The submission should contain only a zip archive of your solutions.

The submission must include the following files:

* `mirrored.txt` 

* `eulpathcomp.txt` 

* `undirhampath.txt` 

## General Instructions

Recall that a decision problem is a yes-or-no question that can be
asked about one of any of an infinite number of possible inputs. The
subset of the possible inputs (these are strings for us) for which the
problem returns "yes" is a language. So we can squint at a particular
language A over some $\Sigma^{\*}$, and read that as a decision
problem asking to compute which members of $\Sigma^{\*}$ are in A.
Likewise we can squint at the decision problem as implicitly defining
a language, the language of strings for which the answer to the
decision problem is "yes."

Recall further that, for decision problems $P$, $Q$, a reduction from $P$ to
$Q$ is an algorithm that takes an instance $I\_{P}$ of problem $P$ as
input and returns instance $I\_{Q}$ of problem $Q$ as output such that
the yes/no answer to $I\_{P}$ is the same as the yes/no answer to
$I\_{Q}$. Cf. 5.17 and 5.20 in §5.3. 

Finally, recall that, for decision problems $P$, $Q$, a
polynomial-time reduction from $P$ to $Q$ is a reduction from $P$ to
$Q$ where the algorithm runs in time polynomial in $\|I\_{P}\|$, the
size of the instance $I\_{P}$. Cf. 7.28 and 7.29 in §7.4.

## 1. Mirrored

Let's remind ourselves about where we saw reductions in an earlier
context: _mapping reducibility_. Let us define $R$ as follows: 

 $R = \\{<M> \mid M \textrm{ is a TM that accepts } w \textrm{ iff } w^{\texit{R}} \\}$

You will show that R is undecidable using mapping reducibility. 

**Your Tasks**

* Describe, in prose-y pseudocode or a mixture of both, an informal
  description of your algorithm that will implement a reduction of
  some undecidable problem to membership in R. Your solution should
  look similar in form to Example 5.24, for instance.

* Submit this in `mirrored.txt`. 

## 2. EULPATHCOMP

Let us define $\textit{EULPATHCOMP}$ as follows:

$ \textit{EULPATHCOMP} = \\{<G,s,t> \mid G \textrm{ is a complete undirected graph that contains a path from } s \textrm{ to } t \textrm{ through every edge in } G \\}$. 

Let us define $\textit{EULCIRCUITCOMP}$ as follows:

$ \textit{EULCIRCUITCOMP} = \\{<G> \mid G \textrm{ is a complete undirected graph that contains an eulerian circuit} \\}$. 

You will show that $\textit{EULPATHCOMP} =\_{P}
\textit{EULCIRCUITCOMP}$ by showing $\textit{EULPATHCOMP} \leq\_{P}
\textit{EULCIRCUITCOMP}$ and $\textit{EULCIRCUITCOMP} \leq\_{P}
\textit{EULPATHCOMP}$. You might consider investigating the Seven
Bridges of Konigsburg Problem.

**Your Tasks**

* Describe, in pseudocode or prose or a mixture of both, an informal
  description of your algorithm that will implement a reduction from
  $\textit{EULPATHCOMP}$ to $\textit{EULCIRCUITCOMP}$.

* Describe, in pseudocode or prose or a mixture of both, an informal
  description of your algorithm that will implement a reduction from
  $\textit{EULCIRCUITCOMP}$ to $\textit{EULPATHCOMP}$.
  
* Submit these both in `eulpathcomp.txt`. 

## 3. UNDIRHAMPATH

Let us define $\textit{UNDIRHAMPATH}$ as follows:

$ \textit{UNDIRHAMPATH} = \\{<G> \mid G \textrm{ is an undirected graph with a Hamiltonian path} \\}$. 

Let us define $\textit{UNDIRHAMCIRCUIT}$ as follows:

$ \textit{UNDIRHAMCIRCUIT} = \\{<G> \mid G \textrm{ is an undirected graph with a Hamiltonian circuit} \\}$. 

You will show that $\textit{UNDIRHAMPATH} =\_{P}
\textit{UNDIRHAMCIRCUIT}$, in a similar fashion.

**Your Tasks**

* Describe, in pseudocode or prose or a mixture of both, an informal
  description of your algorithm that will implement a reduction from
  $\textit{UNDIRHAMPATHP}$ to $\textit{UNDIRHAMCIRCUIT}$.

* Describe, in pseudocode or prose or a mixture of both, an informal
  description of your algorithm that will implement a reduction from
  $\textit{UNDIRHAMCIRCUIT}$ to $\textit{UNDIRHAMPATHP}$.
  
* Submit these both in `undirhampath.txt`. 