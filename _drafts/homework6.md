---
title: "Homework 6"
layout: single
---

### Objectives 

  - Explore CFLs from the perspective of context-free grammars

**Homework Problems**

* [Represent and Produce a CFG](#1-represent-and-produce-a-cfg) (2 pts, 1 manually graded) 

* [Generate Strings in a CFG](#2-generate-strings) (2 pts) 

* [Verify a Simultaneous Derivation](#3-verify-a-simultaneous-derivation) (2 pts)

* [Produce String Derivations](#4-check-string-derivations) (2 pts)

* README (2 pts)

**Total**: 10 points

**Submitting**

Submit this assignment on [Gradescope](https://www.gradescope.com).

The submission should contain only a zip archive of your code and the
associated README. Don’t forget to submit a `README` file containing
the required information, including time spent and resources
consulted.

## 1. Represent and Produce a CFG

This problems asks you to demonstrate you can design CFGs.

Recall Definition 2.2 from the book. A CFG is a 4-tuple
$\(V,\Sigma,R,S\)$, where:

* $V$ is a finite set of variables,

* $\Sigma$ is a finite alphabet,

* $R: V \times Stringof (V \Cup \Sigma)$ is a finite set of _rules_, and

* $S$ is the start variable

Given an English language description of a context free language, you
will write in your own internal representation a grammar generating
that language. Your grammar should be /unambiguous/. You will also
construct a function `CFG->XML` to output the result as an XML
element. Create a CFG that generates the following language L. You can
assume alphabet $\Sigma = \\{0,1\\}$.

$ L = \\{w \mid w = \textrm{FLIP}(w)\\}$, where $\textrm{FLIP}$ is the
FLIP language you already know.


**Your Tasks**

* Design a data representation for this formal definition of CFGs. You
  may use objects, structs, or anything else available in your language.

* Write up an informal description of your chosen representation in a
  section of your README, labeled `CFG Data Representation`.

* Implement your data representation in your chosen language.

* Create a CFG that generates the given language L. 

* Construct a function `CFG->XML` to output the result as an XML

You will produce as output an XML `structure` element containing the
productions of your grammar for this language. We will exercise your
output by testing it against a sequence of strings in the language.


```

```

## 2. Generate Strings in a CFG

This problem asks you to demonstrate you understand the JFLAP CFG
format and know what it means to *generate* strings a language. 

You will below a JFLAP file containing a CFG representing the language
of types in a simple ML-like language. I include below a [diagram from
"Programming in Standard ML"]({{
site.baseurl}}/assets/images/types.jpg) describing this same
information. The terminals of this grammar are the tokens, i.e., the
"words", of the language, which includes identifiers (like labels,
ids, or type variables), parens and curly braces, `->`, `*`, and
punctuation (colon and comma). This means all names would be leaves in
a parse tree: we don’t separate them into individual characters.
Whitespace is not included in the terminals and should be ignored.

In fact, the JFLAP format requires the variables be (a subset of the)
single capital letters and treats any other characters as terminals.
You should adhere to this format. I've given you a version of this
situation with a fixed quantity of labels, type variables, and IDs to
both simplify your lives and to accommodate JFLAP. More specifically,
you will receive the name of a JFF file containing the description of
a CFG, and a number $n$ representing the maximum quantity of
simultaneous substitutions.

The productions of a grammar are also called (Cf. 2.1) "substitution
rules" or simply "rules." Define /simultaneous substitution into $w$
of $R$/ as, if $w$ is a word $abXdcYdZX$, with $a$, $b$, $c$, $d, in
$\Sigma$ and $X$, $Y$, $Z$ in $V$, as the set of all strings produced
by applying at most one rule from $R$ for each instance of each
variable in $w$. Note that not applying a rule to a variable is also a
valid operation. There are almost always more than one ways to
perform a simultaneous substitution into a string. 

** Your Tasks** 

* Open and read in the `.jff` file describing this grammar

* Construct an instance of this grammar in the internal representation
  you devised

* Generate the set of all strings in the language of the grammar
  produced within a fixed number of simultaneous substitutions.

* Write out the set of strings one string per line

* 

```

```


## 3. Verify a Simultaneous Derivation

This problem asks you to demonstrate that you understand how to derive
strings from a grammar. 

Your task is to verify a simultaneous derivation of an intermediate
string from another intermediate string from the grammar you generated
in earlier problem. See the discussion after 2.2 distinguishing the
language of the grammar from the language of intermediate strings

Again, we ask you to produce /simultaneous derivations/.

** Your Tasks** 

* Given a grammar in XML format, and a putative simultaneous
  derivation, decide if this sequence represents a valid simultaneous
  derivation in the language of the grammar.



```

```


## 4. 

You will implement a program that, given a JFLAP XML description of a
CFG and a string in the language of that grammar, will return a
simultaneous derivation of that string. We guarantee that the strings
we provide will be strings in the language of the grammar.

You will produce a derivation of the string in your grammar. You
will write out the sequence of strings in the derivation, one per
line, starting with a string of just the initial symbol, and ending
with the string in question. Our checks will ensure that this sequence
of strings in your derivation follows from the grammar.

More specifically, you will receive the name of a JFF file containing
the description of a CFG, and a string in the language of this
grammar. 

**Your Tasks** 


```

```
