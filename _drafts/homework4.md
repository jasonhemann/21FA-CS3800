---
title: "Homework 4"
layout: single
---

### Objectives 

  - explore NFAs and their relation to regular expressions 
  - explore other closure property of regular langs 

**Homework Problems**

* [Concatentation](#1-concatentation) (2 pt)

* [Kleene Star](#2-kleene-star)       (2 pt) 

* [A Regular Expression Matcher](#3-a-regular-expression-matcher) (4 pts)

* [The FLIP Operation](#4-the-flip-operation) (2 pts)


**Total**: 10 points

**Submitting**

Submit the solution to this assignment in Gradescope.

The submission must include the following files (**NOTE**: everything is
case-sensitive):

* a `Makefile` with the following targets:

  * `setup` (optional)

  * `run-hw4-regexp`

* a `README` containing the required information,

* the source code files needed by your `Makefile`,

## 1. Concatentation

**Your Task**

Implement concatentation for your NFAs from the previous assignment.

Specifically, write a function that, given:

* an NFA recognizing language $A\_1$, and

* an NFA recognizing language $A\_2$

returns an NFA recognizing $A\_1 \circ A\_2$.

To do this, you’ll need to be able to extract individual components of
an NFA instance, e.g., the states, transitions, etc., and use them to
create a new NFA.

Figure 1.48 from the textbook should be helpful here.

**NOTE**: When combining NFAs **be careful with duplicate state names**.
Since the given files may use the same state names, it may be a good
idea to first rename them to something unique.

## 2. Kleene Star

**Your Task**

Implement the Kleene Star operation for your NFAs from the last
assignment.

Specifically, write a function that, given an NFA recognizing language
$A$, returns an NFA recognizing $A^\*$.

To do this, you’ll need to be able to extract individual components of
an NFA instance, e.g., the states, transitions, etc., and use them to
create a new NFA.

Figure 1.50 from the textbook should be helpful here.

## 3. A Regular Expression Matcher

This problem will show you that you’ve almost implemented (the core of)
a regular expression matcher, which is found in nearly every programming
language! Congrats!

> The regexp matcher included with most PLs are of course much more
> efficient, and have many more bells and whistles than the
> theoretical models we are studying. But the basic behavior is indeed
> the same.

To complete it, you’ll just need use your NFA datastructure from HW3, in
combination with the union, concatenation, and Kleene star operations
you implemented so far.

You will also need the definition (Def 1.52) of Regular Expressions from
the textbook, which are defined using exactly these three operations:

R is a _regular expression_ if R is either:

* $a$ for some $a \in \Sigma$ (an alphabet),

* the empty string $\varepsilon$,

* the empty set $\emptyset$,

* $R\_1 \cup R\_2$, sometimes written $R\_1\mid R\_2$, where $R\_1$ and $R\_2$
  are regular expressions,

* $R\_1 \circ R\_2$, sometimes written $R\_1R\_2$, where $R\_1$ and $R\_2$ are
  regular expressions,

* $R\_1^\*$, where $R\_1$ is a regular expression.

**Your Task**

Use Lemma 1.55 and the closed NFA operations you’ve implemented to
create an equivalent NFA for each of the regular expressions below
(these are all from Example 1.53 in the textbook).

Assume that $\Sigma = \{0,1\}$, a $^+$ means "1 or more", and a $\Sigma$ in a
regular expression below means $0\cup 1$.

* $0^\*10^\* = \{w \mid w \textrm{ contains a single } 1\}$

* $\Sigma^\*1\Sigma^\* = \{w \mid w \textrm{ has at least one } 1\}$

* $\Sigma^\*001\Sigma^\* = \{w \mid w \textrm{ contains the string } 001 \textrm{ as a substring}\}$

* $1^\*(01^+)^\* = \{w \mid \textrm{every } 0 \textrm{ in } w \textrm{ is followed by at least one } 1\}$

* $\(\Sigma\Sigma\)^\* = \{w \mid w \textrm{ is a string of even length}\}$

* $\(\Sigma\Sigma\Sigma\)^\* = \{w \mid \textrm{the length of } w \textrm{ is a multiple of } 3\}$

* $01 \cup 10 = \{01,10\}$

* $0\Sigma^\*0\cup 1\Sigma^\*1\cup 0\cup 1 = \{w\mid w \textrm{ starts and ends with the same symbol}\}$

* $\(0\cup\varepsilon\)1^\* = 01^\*\cup1^\*$

* $\(0\cup\varepsilon\)\(1\cup\varepsilon\) = \{\varepsilon,0,1,01\}$

* $1^\*\emptyset = \emptyset$

* $\emptyset^\* = \{\varepsilon\}$

Each NFA you create is doing exactly the same thing as a real regexp
matcher! To prove this to you, the grader will test your submission
using the regexp implementation from an actual PL (e.g., could be Perl,
Python, Java, Racket, etc.).

Specifically, your solution will be tested as follows:

* **Input** (from `stdin`): a number, from 1 to 12 (inclusive),
  corresponding to one of the regular expression examples from above

* Expected **Output** (to `stdout`): An XML automaton element
  representing an NFA that recognizes the same language (for strings up
  to length 5) as the regular expression corresponding to the input
  number.

  To be considered correct, **this NFA must have been constructed from
  smaller NFAs using union, concat, and star as described in Lemma
  1.55**. We will inspect your source code to ensure this.

  To further illustrate what I mean, here is a snippet of (Racket) code
  from our sample solution:

```
  ;; Part of our sample solution, to illustrate what you should do

  (define N0 (mk-single-char-nfa "0")) ; NFA recognizing {"0"}
  (define N1 (mk-single-char-nfa "1")) ; NFA recognizing {"1"}
  (define N0* (nfa* N0)) ; NFA recognizing {"", "0", "00", "000", ...}

  (case (read-stdin)
    ["1" (nfa->xml (nfa-concat (nfa-concat N0* N1) N0*))]
    ....)
```
* `Makefile` **target name**: `run-hw4-regexp`

* **Example**:

  `printf "1" | make -sf Makefile run-hw4-regexp`

  Output:

```
  <automaton>
  <state id="0" name="q164"><initial/></state>
  <state id="1" name="N01"></state>
  <state id="2" name="N02"></state>
  <state id="3" name="N13178"></state>
  <state id="4" name="N14179"></state>
  <state id="5" name="q164180"><final/></state>
  <state id="6" name="N01181"></state>
  <state id="7" name="N02182"><final/></state>
  <transition><from>0</from><to>3</to><read/></transition>
  <transition><from>0</from><to>1</to><read/></transition>
  <transition><from>1</from><to>2</to><read>0</read></transition>
  <transition><from>2</from><to>3</to><read/></transition>
  <transition><from>2</from><to>1</to><read/></transition>
  <transition><from>3</from><to>4</to><read>1</read></transition>
  <transition><from>4</from><to>5</to><read/></transition>
  <transition><from>5</from><to>6</to><read/></transition>
  <transition><from>6</from><to>7</to><read>0</read></transition>
  <transition><from>7</from><to>6</to><read/></transition>
  </automaton>
```

**More Hints:**

To further help you, below are the exact regexp patterns (each
corresponds to a numbered example from above) that the grader will use
to grade your output NFA (the grader will only check strings up to
length 5).

Note that in typical regexp matching, a union of single chars, e.g., 0
\cup 1, is typically written `[01]`, while the "vertical bar" $\mid$ is a
more general union operation.

* `"0*10*"`

* `"[01]*1[01]*"`

* `"[01]*001[01]*"`

* `"1*(01+)*"`

* `"([01][01])*"`

* `"([01][01][01])*"`

* `"01|10"`

* `"0[01]*0|1[01]*1|0|1"`

* `"01*|1*"`

* `"^$|^0$|^1$|^01$"`

  \(won’t work without the `^` or `$`, which stand for "string start"
  and "string end", respectively, demonstrating that there ​_are_​ some
  differences between the theoretical regular expressions we study in
  class, and the regexp matching available in programming languages)

* `"\b\B"` (pattern that won’t match anything)

* `""`

With these, you should be able to easily test your solution on your own
using the regexp library in your favorite language. Make sure to choose
"exact match" ("partial match" is the default in some langs and will not
recognize the same language), which corresponds to the textbook’s notion
of matching.  Specifically, for any given string in the language of
alphabet $\Sigma = \{0,1\}$ (up to length 5), your NFA should accept the
string **if and only if** the equivalent regexp pattern matches on the
string.

Finally, if you still need more explanations, the internet has plenty of
sites dedicated to learning about, and interactively exploring regexps,
e.g., [regexr.com](https://regexr.com/) or
[regex101.com](https://regex101.com/).

## 4. The FLIP Operation

Define the $\textrm{FLIP}$ operation on a language to be:

$\textrm{FLIP}(L) = \{c\_n \ldots c\_0 \mid c\_0\ldots c\_n \in L\}, \textrm{where } c\_i \in \Sigma$

Prove that regular languages are closed under the \textrm{FLIP}
operation by reading in the name of [an XML file describing a DFA]({{
site.baseurl}}/assets/fig1.4.jff) for the language and producing a
description of the resulting language as an NFA. We will test your
machine by running it against a variety of outputs.



