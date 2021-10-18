---
title: "Homework 5"
layout: single
---


### Objectives 

  - Conclude discussion of pumping lemma for regular languages
  - Begin to explore material from chapter 2

**Homework Problems**

* [Pump a string](#1-pump-a-string) (2 pts)

* [String Derivations](#2-string-derivation) (2 pts)

* [Design a CFG](#3-design-a-cfg) (2 pts)

* [Design a PDA](#4-design-a-pda) (2 pts)

* [Closed Operations for CFLs](#5-closed-operations-for-cfls) (2)

* [Regular is Context-free?](#6-regular-is-context-free) (6 pts)

* README (2 pts)

**Total**: 32 points

**Submitting**

Submit this assignment at [Gradescope
`hw5`](https://www.gradescope.com/courses/219302/assignments/1043973).

The submission should include only pdf or plain text files.

Be sure to assign each page to the correct problem in Gradescope.

Also, don’t forget to submit a `README` file containing the required
information.

<!-- ## 1. Pump a string. -->

<!-- Your job here is to, given both a regular expression describing an -->
<!-- infinite language and a string in the language of that expression, -->
<!-- come up with a division into components $x$, $y$, and $z$ such that -->
<!-- for any choice of $i$, any $xy^{i}z$ is also a string in the language -->
<!-- of that regular expression.  -->

<!-- More specifically, we will provide you the name of a `.jff` file -->
<!-- containing the description of a regular expression,  -->


## 2. String Derivations

You will find below a CFG representing the language of types in a
simple ML-like language. I include below a [diagram from "Programming
in Standard ML"]({{ site.baseurl}}/assets/images/types.jpg) describing
this same information. Your job is to (1) open and read in the JFF
file describing this construction, (2) construct an internal
representation of your own devise, (3) derive the following strings in
your grammar. You will write out the sequence of strings in the
derivation, one per line, starting with the initial symbol, and ending
with the string in question. We will check that this sequence of
strings follows the grammar. 

More specifically, you will receive the name of a JFF file containing
the description of a CFG, and a string in the language of this
grammar. 





The terminals of this grammar are the tokens, i.e., the "words", of the
language, which includes keywords (like `class`), identifiers (like
class or field names), parens, braces, and punctuation (like dot,
semicolon, or comma).

NOTE: this means all names (e.g., class names, variable names, etc.)
should be leaves in a parse tree. You don’t need to separate them into
individual characters.

Whitespace is not included in the terminals and should be ignored.

Give a parse tree or derivation for the following strings (i.e.,
programs):

* 

* 


## 3. Design a CFG

Create a CFG that generates the following language L.

You can assume alphabet \Sigma = \{0,1\}.

$ L = \\{w \mid w = \textrm{FLIP}(w)\\}$, where $\textrm{FLIP}$ is the
language you already know from earlier.


You will produce as output an XML element describing the grammar of
this language. We will exercise your output by testing it against a
sequence of strings in the language. 

## 4. Design a PDA

Create a pushdown automata that recognizes language L from [the previous
problem](#2-design-a-cfg).

You can either draw a diagram or give a formal description.

## 5. Closed Operations for CFLs

Show that the following operations are closed under context-free
languages:

* union

* concatentation

* Kleene star

## 6. Regular is Context-free?

You will prove, by construction, the statement: For any language A, if
A is regular, then A is also context-free. You will prove this by
consuming an XML file containing a description of a machine
recognizing language A, and you will produce (an XML description of) a
PDA recognizing that same machine.

