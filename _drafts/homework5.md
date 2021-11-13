---
title: "Homework 5"
layout: single
---

### Objectives 

  - Explore CFLs from several different points of view
  - Conclude relating regular languages to material of chapter 2

**Homework Problems**

* [Design a CFG](#1-design-a-cfg) (2 pts) 

* [Consume a CFG and Check String Derivations](#2-check-string-derivations) (2 pts)

* [Design, concat, and run a PDA](#3-design-a-pda) (2 pts)

* [Regular implies context-free](#4-regular-implies-context-free) (2 pts)

* README (2 pts)

**Total**: 10 points

**Submitting**

Submit this assignment on [Gradescope](https://www.gradescope.com).

The submission should contain only a zip archive of your code and the
associated README. Don’t forget to submit a `README` file containing
the required information, including time spent and resources
consulted.


## 1. Design a CFG

- Construct your own data representation of a CFG. 
- Given an English language description of a grammar, you will write the grammar in your own internal rep.
- CFG->XML-JFLAP (if distinct from Sipser)

(2) English Description -> (derivation + CFG for language -> XML)
Given an English language description of a context free language, you
will write a grammar generating that language, and output the result
as XML.

<!-- . Your grammar should be /unambiguous/ -->

Create a CFG that generates the following language L.

You can assume alphabet \Sigma = \{0,1\}.

$ L = \\{w \mid w = \textrm{FLIP}(w)\\}$, where $\textrm{FLIP}$ is the
language you already know from earlier.


You will produce as output an XML element describing the grammar of
this language. We will exercise your output by testing it against a
sequence of strings in the language. 


## 2. String Derivations

- XML->CFG 
- Generate strings/n 
- In-language (easy, after generate)

(2) XML->CFG + confirm or disconfirm derivations

You will implement `xml2cfg`, a program that, given a JFLAP XML
description of a CFG and a string over the input alphabet of that
grammar, will return either a derivation of that string in the
grammar, or fail, a sentinel value showing that the string in question
is not in the language of the grammar. 

You will also implement a generate-string operator that will produce
the derivation of a string in the language of the grammar, if
possible. You should implement this with a procedure `generate`, that
produces a derivation of a string in the language if possible and
produces false otherwise.

Remember you should implement leftmost derivations.

You will find below a CFG representing the language of types in a
simple ML-like language. I include below a [diagram from "Programming
in Standard ML"]({{ site.baseurl}}/assets/images/types.jpg) describing
this same information. Your job is to (1) open and read in the `.jff`
file describing this construction, (2) construct an internal
representation of your own devise, (3) produce a derivation of the
following in your grammar. You will write out the sequence of strings
in the derivation, one per line, starting with the initial symbol, and
ending with the string in question. Our checks will ensure that this
sequence of strings in your derivation follows from the grammar.

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

## 3. Design a PDA

- XML-PDA-JFLAP->PDA-JFLAP
- PDA-JFLAP->PDA-SIPSER
- Union/Kleene/Concat,whichever is most interesting-PDA-Sipser 
- run-PDA-Sipser 

(2) XML1, XML2 ->PDA A o B , run-PDA

Take in via command line a filename of an XML description of a JFLAP
PDA and a string. 

Produce PDA1 in your own internal representation.

Together with PDA2 from the next problem, construct a PDA that is the
concatenation of PDA1 and PDA2.

Output "accept" or "reject" if that string is/is not in the language
of PDA1 o PDA2.


## 4. Regular Implies Context-free

- NFA -> PDA-Sipser 
- PDA-Sipser->PDA-JFLAP
- PDA-JFLAP->XML-PDA-JFLAP

(2) NFA->PDA->XML. This seems like the easiest one, but we could
compare w/the Textbook pg 107. Say, don't use the textbook transition via CFG. 

"Every regular language is context-free." You will prove this
statement by reading in the XML description of an NFA, and producing
as output an XML description of a PDA that recognizes the same
language. We will test your implementation by running the resulting
PDA against a variety of strings and verifying that your machine
accepts strings in the language and rejects strings in $\Sigma^{*}$
that are not in the language. 

You will prove, by construction, the statement: For any language A, if
A is regular, then A is also context-free. You will prove this by
consuming an XML file containing a description of an NFA machine
recognizing language A, and you will produce (an XML description of) a
PDA recognizing that same machine. You will likely find your work on
NFAs from earlier assignments helpful. We will test your assignment by
testing your PDA on a variety of inputs.


```

```

