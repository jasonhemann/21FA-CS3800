---
title: "Exam 1"
layout: single
---

### Objectives 

  - Retrench material from first third of the course
  - Assess learning and understanding thus far 
  - Set the stage for future learning 

**Exam Problems**

* [Set difference](#1-set-difference) 

* [Boolean Decision Diagrams](#2-boolean-decision-diagrams)

* [Intersection of DFAs](#3-the-intersection-operation) 

* [NFA for a language](#4-nfa-for-a-language)

* [Union vs Concat](#5-union-vs-concat)

* [Homomorphism of Regular Languages](#6-homomorphism-of-regular-languages)

<!-- * [A Novel Proof by Construction](#7-a-novel-proof-by-construction) -->

**Submitting**

Submit the solution to this exam in Gradescope.

The submission must include the following files (**NOTE**: everything is
case-sensitive):

* a `Makefile` with the following targets:

  * `setup` (optional)

  * `run-exam1-setdiff`

  * `run-exam1-bdd`
  
  * `run-exam1-intersection`

  * `run-exam1-nfa2xml`

  * `run-exam1-unionconcat`
  
  * `run-exam1-homomorphism`
  
  <!-- * `run-exam1-nsdfa2dfa` -->

* a `README` containing the required information,

* the source code files needed by your `Makefile`,

## 1. Set Difference

The _set difference_ of a set $S\_1$ and a set $S\_2$, written $S\_1
\- S\_2$ or $S\_1 \setminus S\_2$, is a set whose elements must be
in $S\_1$ but not in $S\_2$.

**Your Task**

Write the following program:

* **Input** (from `stdin`): a set $S\_1$ of strings (of alphanumeric
  characters), where set elements are separated with a space

* **Output** (to `stdout`): the set difference of the input set $S\_1$
  and $S\_2 = \\{\textrm{"bat"}, \textrm{"horse"}, \textrm{"turtle"},
  \textrm{"fish"}, \textrm{"squirrel"}, \textrm{"bird"}\\}$. Separate
  each element in the output with a space.

* `Makefile` **target name**: `run-exam1-setdiff`

* **Example**:

  `printf "bat cat" | make -sf Makefile run-exam1-setdiff`

  Output:

```
cat
```

\(Note: you will represent the empty set with a blank line.)

## 2. Boolean Decision Diagrams

A _Boolean function_ $f(x\_1,...,x\_n)$ is a function that accepts
Boolean arguments as inputs and produces a Boolean result. Common
Boolean functions include `and`, `or` and `xor` with their usual
logical interpretations.

We can describe Boolean functions over $\Sigma = \\{0, 1\\}$ (using
$0$ for false and $1$ for true) as DFAs. More specifically, we can
implement a DFA M that accepts strings $x = x\_1,...,x\_k$ that have a
prefix $x\_1,...,x\_i$ sufficient to show that $f(x\_1,...,x\_n) = 1$.
_Order_ the variables $x\_1$, then $x\_2$, etc---that is, so your
decision-making branches first on $x\_1$, etc. Your DFA will, per
force, implement a kind of [Ordered Boolean Decision Diagram
(BDD)](https://en.wikipedia.org/wiki/Binary_decision_diagram).

**Your Task**

For the function $f$ given below,

$f(x\_{1}, x\_{2}, x\_{3}) = (\lnot x\_{1} \wedge \lnot x\_{2} \wedge \lnot x\_{3}) \vee (x\_{1} \wedge x\_{2}) \vee (x\_{2} \wedge x\_{3})$.

Using your own data representation, you will construct a DFA that
accepts $x = x\_1,...,x\_k$ if and only if $x$ has a prefix
$x\_1,...,x\_i$ sufficient to show that $f(x\_1,...,x\_n) = 1$. 

Then write a program that reads from `stdin` and feeds that input,
along with your newly-constructed DFA (i.e., the one corresponding to
$f$) to your “run” predicate. Your program will write `accept` to
`stdout` if the DFA accepts the `input` and `reject` otherwise. You
will likely find your solution to Homework 2 helpful for this last
part.

**We will be manually inspecting your code to ensure that you have
constructed this DFA from your own internal representation, so make
sure and write for us in your README your data description of a DFA in
your language so we can compare against it** (You only need to write
your data description of a DFA in README file once, this is just to
reiterate and remind you).

Your solution will be tested as follows:

* **Input** (from `stdin`): a (randomly generated) string in alphabet
  $\Sigma = \\{0, 1\\}$

* Expected **Output** (to `stdout`): 

    * `accept`, if input string $x$ has a prefix $x\_1,...,x\_i$
sufficient to show that $f(x\_1,...,x\_n) = 1$.

    * `reject` otherwise

* `Makefile` **target name**: `run-exam1-bdd`

* **Example**:

  `printf "" | make -sf Makefile run-exam1-bdd`

  Output: `reject`

  `printf "1" | make -sf Makefile run-exam1-bdd`

  Output: `reject`

  `printf "11" | make -sf Makefile run-exam1-bdd`

  Output: `accept`

  `printf "00000" | make -sf Makefile run-exam1-bdd`

  Output: `accept`

  `printf "011" | make -sf Makefile run-exam1-bdd`

  Output: `accept`


## 3. The Intersection Operation

**Your Task**

First, implement intersection for your DFAs. Specifically, write a
function that, given:

* a DFA recognizing language $A\_1$, and

* a DFA recognizing language $A\_2$

returns a DFA recognizing $A\_1 \cap A\_2$. Your construction will be
almost the same as you implementation of Union from Homework 2. See
footnote 3 in the proof of Theorem 1.25 in the Sipser text for the
modifications to implement intersection. **Implement intersection
following this style**

Then, create a "password checking" machine PW that uses your new
`intersection` operator construct the DFA that is the intersection of
DFAs for the four languages, i.e., $A\_1 \cap A\_2 \cap A\_3 \cap
A\_4$. You can construct your internal representation of these four
DFAs by hand, or construct them by hand in JFLAP and then import them
via XML, or construct them by transformation from some other
representation.

You may assume the alphabet \Sigma = `{A,B,C,a,b,c,1,2,3,!}`.

* $A\_1 = \\{w \mid \textrm{length of } w \textrm{ is at least } 3\\}$

* $A\_2 = \\{w \mid w \textrm{ contains an uppercase letter}\\}$

* $A\_3 = \\{w \mid w \textrm{ contains a number}\\}$

* $A\_4 = \\{w \mid w \textrm{ contains a non-alphanumeric symbol}\\}$

Your solution will be tested as follows:

* `Makefile` **target name**: `run-exam1-intersection`

* **Input** (from `stdin`): An arbitrary string with chars in alphabet
  $\Sigma$

* Expected **Output** (to `stdout`): `valid` if PW accepts the input,
  `invalid` otherwise.

* **Examples**:

  `printf "abc" | make -sf Makefile run-exam1-intersection`

  Output: `invalid`

  `printf "abc1" | make -sf Makefile run-exam1-intersection`

  Output: `invalid`

  `printf "Abc1!" | make -sf Makefile run-exam1-intersection`

  Output: `valid`

**However, once again, your solution must actually construct the four
DFAs and then intersect them together. We will be manually inspecting
your code to ensure that in either case you create these four DFAs, in
own internal representation, so make sure and write for us in your
README your data description of a DFA in your language so we can
compare against it** (You only need to write your data description of
a DFA in README file once, this is just to reiterate and remind you).

## 4. NFA for a language

**Your Task**

Construct a NFA for the language over $\Sigma = \\{0, 1, 2\\}$ of
$\\{ w \mid w\_0 , ... , w\_n \textrm{ where every third character is
 a } 0 \\}$
 
To help clarify for you the language, we include some strings in this
language below (notice the first line deliberately a blank).

```

11
2
210
210120
1101102
```

Using your own data representation, you will construct a NFA
recognizing this language. When invoked, your program will you will
produce an XML representation of this NFA. You will likely find your
solution to Homework 2 helpful for this last part.

**We will be manually inspecting your code to ensure that you have
constructed this NFA from your own internal representation, so make
sure and write for us in your README your data description of a NFA in
your language so we can compare against it**.

* **Input** (from `stdin`): none

* Expected **Output** (to `stdout`): an automaton XML string
  representing a NFA that recognizes strings of the language described
  above.

* `Makefile` **target name**: `run-exam1-nfa2xml`

* **Example**:

  `make -sf Makefile run-exam1-nfa2xml`

  Output:
  
  ```
  ```

\(Output here deliberately omitted.)

## 5. Union vs Concat

One day, a student in class asked - "Why would we want to implement
the concatenation of two languages when we have already implemented
the union? Isn't union more general?"

The answer to this student's question is "No. For two arbitrary
languages $L\_1$ and $L\_2$, we can assume neither that $L\_1 \cup
L\_2$ is a subset of $L\_1 \circ L\_2$, nor that $L\_1 \circ L\_2$ is
a subset of $L\_1 \cup L\_2$.

To demonstrate this, given:

* an NFA $N\_1$ recognizing language $L\_1$, and

* an NFA $N\_2$ recognizing language $L\_2$

you will produce the set of strings that demonstrate the difference
between their union and their concatenation.

Specifically, when given the names of two XML files containing NFAs,
your program will: 

 - read in these NFAs
 - construct $N\_1 \circ N\_2$
 - construct $N\_1 \cup N\_2$
 - and returns all strings up to and including length 5 recognized by
   $(N\_1 \circ N\_2) \setminus (N\_1 \cup N\_2)$, one string per
   line.

We are not particular as to how you accomplish this last step. You may
implement difference for NFAs. You might instead/also use solutions to
some in-class exercises. You might use solutions to some earlier parts
of this exam. . You will likely find it helpful to re-use parts of
your solutions to Homework 3,

**Note: This question does assume you have completed the `concat`
question on HW4. If you have not, use the extra time today to complete
it now and then use your solution here.**

* `Makefile` **target name**: `run-exam1-unionconcat`

* **Example**:

  You can test your program with these files:

  * [`nfa-abc.xml`]({{ site.baseurl }}/assets/docs/nfa-abc.xml): recognizes the language $\\{\textrm{"abc"}\\}$

  * [`nfa-efgstar.xml`]({{ site.baseurl }}/assets/docs/nfa-efgstar.xml): recognizes the language $\\{\textrm{""}, \textrm{"efg"}, \textrm{"efgefg"}, ... \\}$

  `printf "nfa-abc.xml nfa-efgstar.xml" | make -sf Makefile run-exam1-unionconcat`

  Output:

```
```

## 6. Homomorphism of Regular Languages

In this problem you will demonstrate that you understand closure of
regular languages under novel operations by implementing a
constructive proof that the regular languages are closed under
homomorphism. 

**Your Task**

Implement the homomorphism operation for NFAs. Specifically, write a
function that, given:

* an NFA recognizing language $A$ over alphabet $\Sigma\_1$

* a mapping $f$ from $\Sigma\_1$ to $\Sigma\_2$

returns an NFA recognizing $f(A)$, the image of language $A$ under the
mapping $f$.

To do this, you’ll likely need to be construct an internal
representation of the provided mapping, and to be able to extract
individual components of an NFA instance, e.g., the states,
transitions, etc., and use them to create a new NFA.

**HINTS**:

* **Be careful and uniformly map symbols from the first alphabet to
  the second**. $\Sigma\_1 \cap \Sigma\_2$ may be non-empty.

Your solution will be tested as follows:

* **Input** (from `stdin`): the name of **a XML file**, then a space,
  then **a sequence of pairs of symbols** taken in turn first from
  $\Sigma\_1$ then from $\Sigma\_2$.

* Expected **Output** (to `stdout`): an automaton XML string
  representing an NFA that recognizes strings of the language $f(A)$.

* `Makefile` **target name**: `run-hw3-homomorphism`

* **Example**:

  You can test your program with these files:

  * [`nfa-a.xml`]({{ site.baseurl }}/assets/docs/nfa-a.xml): recognizes the language $\{"a"\}$

  `printf "nfa-a.xml a n b f" | make -sf Makefile run-exam1-homomorphism`

  Output:

```
```

<!-- ## 7. A Novel Proof by construction -->

<!-- In this problem you will demonstrate that you understand the technique -->
<!-- of proof by construction by applying it in a new situation. DFAs are -->
<!-- traditionally limited to only one start state. In this problem we ease -->
<!-- that restriction for a type of machine we call nondeterministic-start -->
<!-- DFAs (nsDFAs). An nsDFA can have one **or more** start states, and an -->
<!-- nsDFA $M$ accepts a string $ w = w\_0 ... w\_n $ if there is a -->
<!-- sequence of states $q\_0 ... q\_n$ consistent with M's $\delta$ -->
<!-- function and $q\_0$ is any one of the machine's start states. -->

<!-- Your task is to demonstrate that nsDFAs are no more powerful than DFAs -->
<!-- by implementing a constructive proof. -->

<!-- **Your Task** -->

<!-- Define a data representation for nsDFAs, and implement a -->
<!-- language-preserving function `nsDFA->DFA`. Specifically, write a -->
<!-- function that, given -->

<!-- * an nsDFA recognizing language $A$ -->

<!-- returns a DFA recognizing $A$. **You must implement this -->
<!-- programmatically**. That is, you should not write one-off solutions to -->
<!-- pass our test cases, but instead write a programmatic transformation. -->
<!-- We will verify this by manual code inspection. -->

<!-- **HINTS**: -->

<!-- * **Be careful and uniformly map symbols from the first alphabet to -->
<!--   the second**. $\Sigma\_1 \cap \Sigma\_2$ may be non-empty. -->

<!-- * **Make sure and remember to write your data description for nsDFAs -->
<!--   in your `README` file.** -->

<!-- Your solution will be tested as follows: -->

<!-- * **Input** (from `stdin`): the name of **a XML file describing an -->
<!--   nsDFA for a language A**. An XML file describing an nsDFA is like -->
<!--   one describing a DFA, except that in an nsDFA more than one state -->
<!--   may have an `<initial/>` tag. -->

<!-- * Expected **Output** (to `stdout`): an automaton XML string -->
<!--   representing a DFA that recognizes strings of the language $A$. -->

<!-- * `Makefile` **target name**: `run-exam1-nsdfa2dfa` -->

<!-- * **Example**: -->

<!--   You can test your program with these files: -->

<!--   * [`nsdfa-goodbad.xml`]({{ site.baseurl }}/assets/docs/nsdfa-goodbad.xml): recognizes the language $\\{\textrm{"good"}, \textrm{"bad"}\\}$ -->

<!--   `printf "nsdfa-goodbad.xml" | make -sf Makefile run-exam1-nsdfa2dfa` -->

<!--   Output: -->

<!-- ``` -->
<!-- ``` -->


