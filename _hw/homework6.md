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

The submission must include the following files (**NOTE**: everything is
case-sensitive):

* a `Makefile` with the following targets:

  * `setup` (optional)

  * `run-hw6-dyck`
  
  * `run-hw6-generate-n`

  * `run-hw6-verify`
  
  * `run-hw6-derive`

* a `README` containing the required information,

* the source code files needed by your `Makefile`,

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
assume alphabet $\Sigma = \\{(,),[,]\\}$.

$ L = \\{w \mid w = \textrm{ is a string of well-balanced matching brackets}\\}$. 


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

Your solution will be tested as follows:

* **Input** (from `stdin`): Nothing

* Expected **Output** (to `stdout`): an XML `structure` element,
  containing the productions of your grammar. Note we will manually
  inspect that you are in fact constructing the CFG and not just
  printing the output

* `Makefile` **target name**: `run-hw6-dyck`

* **Example**:

  `make -sf Makefile run-hw6-dyck`

  Output:


```
<structure>
<type>grammar</type>
<production><left>S</left><right>[S]</right></production>
<production><left>S</left><right>(S)</right></production>
<production><left>S</left><right>SS</right></production>
<production><left>S</left><right/></production>
</structure>
``` 


## 2. Generate Strings in a CFG

This problem asks you to demonstrate you understand the JFLAP CFG
format, to internalize a new technical term related to derivations,
and know what it means to *generate* strings a language.

You will below a JFLAP file containing a CFG representing the language
of types in a simple ML-like language. I include below a [diagram from
"Programming in Standard ML"]({{ site.baseurl }}/assets/images/types.jpeg) describing this same information. The
terminals of this grammar are the tokens, i.e., the "words", of the
language, which includes identifiers (like labels, ids, or type
variables), parens and curly braces, `->`, `*`, and punctuation (colon
and comma). This means all names would be leaves in a parse tree: we
don’t separate them into individual characters. Whitespace is not
included in the terminals and should be ignored. Notice that
real-world languages are more complex than the languages we have
thus-far worked with; this is just to describe a *type* in ML.

In fact, the JFLAP format requires the variables be (a subset of the)
single capital letters and treats any other characters as terminals.
You should adhere to this format. I've given you a version of this
situation with a fixed quantity of labels, type variables, and IDs to
both simplify your lives and to accommodate JFLAP. More specifically,
you will receive the name of a JFF file containing the description of
a CFG, and a number $n$ representing the maximum quantity of
simultaneous substitutions.

The productions of a grammar are also called (Cf. 2.1) "substitution
rules" or simply "rules." Define _simultaneous_ _substitution_ _into_
$w$ _of_ $R$ as, if $w$ is a word $abXdcYdZX$, with $a$, $b$, $c$,
$d$, in $\Sigma$ and $X$, $Y$, $Z$ in $V$, as the set of all strings
produced by applying at most one rule from $R$ for each instance of
each variable in $w$. Note that not applying a rule to a variable is
also a valid operation. There are almost always more than one ways to
perform a simultaneous substitution into a string. To help you we use
the following one-character abbreviations: `T`ype, Type`V`ariable,
`I`d, `L`abel, T`U`ple (a parethesized grouping of types), and
`S`truct (a non-empty sequence of label-type pairs).

**Your Tasks** 

* Open and read in a file ([types.jff]({{ site.baseurl
  }}/assets/docs/types.jff) for this example) containing a grammar

* Construct an instance of this grammar in the internal representation
  you devised

* Generate the set of all strings in the language of the grammar
  produced within a fixed number of simultaneous substitutions.

* Write out the set of strings one string per line

Your solution will be tested as follows:

* **Input** (from `stdin`): The name of a `.jff` file containing a
  CFG, and a number $n$

* Expected **Output** (to `stdout`): the set of all strings derivable
  through up to $n$ simultaneous derivations, one string per line.

* `Makefile` **target name**: `run-hw6-generate-n`

* **Example**:

  `printf "types.jff 5" | make -sf Makefile run-hw6-generate-n`

  Output:


```
Coming
``` 

## 3. Verify a Simultaneous Derivation

This problem asks you to demonstrate that you understand how to derive
strings from a grammar. 

Your task is to verify a putative simultaneous derivation of a string
in the language of the grammar, starting with the string containing
only the start symbol.

Again, we ask you to verify /simultaneous derivations/.

**Your Tasks** 

* Given a putative simultaneous derivation, decide if this sequence
  represents a valid simultaneous derivation in the language of the
  grammar of `types.jff`.

Your solution will be tested as follows:

* **Input** (from `stdin`): A putative simultaneous derivation, one
  intermediate string per line, starting with the string containing
  only the initial symbol on the first line.

* Expected **Output** (to `stdout`): 

    * `accept`, if this sequence represents a valid simultaneous
      derivation in the grammar,

    * otherwise `reject` otherwise

* `Makefile` **target name**: `run-hw6-verify`

* **Example**:

  `printf "T\n{S}\n{L:T,S}\n{fst:V,L:T}\n{fst:t1,snd:V}\n{fst:t1,snd:t2}\n" | make -sf Makefile run-hw6-verify`

  Output: `accept`

  `printf "T\n{T}\n{L:T,S}\n{fst:V,L:T}\n{fst:t1,snd:V}\n{fst:t1,snd:t2}\n" | make -sf Makefile run-hw6-verify`

  Output: `reject`

  `printf "T\n{S}\n{L:T,S}\n{fst:V,L:T}\n" | make -sf Makefile run-hw6-verify`

  Output: `reject`

  `printf "T\n{S}\n{L:T,S}\n{fst:V,L:V}\n{fst:t1,snd:V}\n{fst:t1,snd:t2}\n" | make -sf Makefile run-hw6-verify`

  Output: `reject`

  `printf "T\n{S}\n{L:T,S}\n{fst:V,L:T}\n{fst:V,L:V}\n{fst:t1,snd:t2}\n" | make -sf Makefile run-hw6-verify`

  Output: `accept`

## 4. Produce a simultaneous derivation

You will implement a program that, given a JFLAP XML description of a
CFG, an intermediate source string in the language of that grammar,
and an intermediate target string in the language of that grammar,
will return a simultaneous derivation of the target from the source.
We guarantee that the strings we provide will be intermediate strings
of the grammar. See the discussion after 2.2 distinguishing the
language of the grammar from the language of intermediate strings

You will produce a derivation of the intermediate string in the
grammar. You will write out the sequence of strings in the derivation,
one per line, starting with the initial source string, and ending with
the target string in question. Our checks will ensure that this
sequence of strings in your derivation follows from the grammar.


**Your Tasks** 
 
 * Given the name of a JFF file containing the description of a CFG,
   an intermediate source string in the language of the grammar, and
   an intermediate target string in the language of this grammar,
   construct a valid simultaneous derivation in the language of the
   grammar from the source to the target.

Your solution will be tested as follows:

* **Input** (from `stdin`): A filename, followed by a source string,
  followed by a target string. These will be newline-separated, to
  account for derivations beginning with and ending with the empty
  string. Likewise you will use a blank link in your output to
  indicate the empty string.

* Expected **Output** (to `stdout`): 

    * a sequence of intermediate strings, one per line, representing a
      valid simultaneous derivation in the grammar

* `Makefile` **target name**: `run-hw6-derive`

* **Example**:


  `"types.jff\n{fst:V,L:T}\n{fst:t1,snd:t2}\n" | make -sf Makefile run-hw6-derive`

  Output: 
  
  ```
  {fst:V,L:T}
  {fst:t1,snd:V}
  {fst:t1,snd:t2}
  ```

  Output: `accept`

  `"types.jff\nT\n{fst:t1,snd:t2}\n" | make -sf Makefile run-hw6-derive`

  ```
  T
  {T}
  {L:T,S}
  {fst:V,L:T}
  {fst:t1,snd:V}
  {fst:t1,snd:t2}
  ```
