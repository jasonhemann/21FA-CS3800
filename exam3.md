---
title: "Exam 3"
layout: single
---

### Objectives 

**Exam Problems**

* [Pumping Lemma for CFLs](#1-pumping-lemma-for-cfls) (3pts manually graded)

* [Chomsky Normal Form](#2-chomsky-normal-form) (7pts, 2 manually graded)

* [1\# Duplicating Program](#3-duplicating-program) (4pts, 2 manually graded)

* [Undecidability by Reduction](#4-undecidability-by-reduction) (3pts, manually graded)

* [Graph Components](#5-graph-components) (3pts, manually graded)


**Submitting**

Submit the solution to this exam in Gradescope.

The submission must include the following files (**NOTE**: everything is
case-sensitive):

* `exam3-pumping.txt`

* `exam3-remove-units.txt`

* `exam3-normalize.txt`

* `exam3-duplicating-program.trm`

* `exam3-duplicating-program.txt`

* `exam3-undecidability-by-reduction.txt`

* `exam3-graph-components.txt`

* a `Makefile` with the following targets:

  * `run-exam3-remove-units`
  
  * `run-exam3-normalize`
  
  * `run-exam3-chomsky`

* the source code files needed by your `Makefile`,

* a `README` containing
 
  * The time you took on exam
  
  * Resources consulted


## 1. Pumping Lemma for CFLs

I feel obligated to include *some* question on the pumping lemma. So
here's one that's not so bad but that gets at the idea. Use the
context free pumping lemma to prove, by contradiction, that the
following language L is not context-free.

$ \textrm{L}  = \\{ 0^{i}1^{j}0^{i} \mid i \leq j \\} $


**Your Tasks**

You will find we started this proof for you in a file named
[`exam3-pumping.txt`]({{ site.baseurl
}}/assets/docs/exam3-pumping.txt). You should complete this proof.
Your solution should resemble Example 2.36. In this file you should
first assume, toward contradiction, that L is context-free and let $p$
be the pumping length.

Your solution should include your choice of a string $s$, followed by
your argument (by cases) that $s$ cannot be pumped.



**HINTS**:

* **Think carefully about your choice of string $s$** Find a $s$ that
  helps capture the "essence" of what makes the language not
  context-free.


## 2. Chomsky Normal Form 

As you know, the algorithm for translating a grammar into CNF is short
but subtle. Here, you will complete your implementation of the CNF
transformation. You are responsible for implementing two methods:
`remove-units` and `normalize`. We will test these methods independent
of one another, and we will also test them in sequence. For one point,
we test these methods with your `run-exam3-chomsky`, which will use
your `run-exam2-chomsky` from Exam 2 for an end-to-end test of your
full CNF algorithm.

**Your Tasks** **(Plural)** 

You will implement the "remove unit rules" portion of the CNF
algorithm Sipser describes in the proof of Theorem 2.9. Recall a unit
rule is a rule of the form `A -> B`: when the right-hand side of a
grammar rule is precisely one non-terminal. Given

* an XML description of a CFG _where we have already built a new start
  state_ and _eliminated the ε transitions_

you will produce 

* an XML automaton element describing an equivalent grammar but
  without any unit rules.

* a file `exam3-remove-units.txt` describing your overall algorithm for
  solving this problem. You should walk us through your data types,
  your overall approach, the specific subroutines you implement to
  help solve this problem and the purposes of each, and any
  preconditions or invariants upon which you rely. I mean these
  specifically for the grammar transformation part; you do not need to
  e.g. recapitulate our XML format.

**Also** 

You will also implement the "normalize rules" portion of the CNF
algorithm. Given

* an XML description of a CFG _where we have already built a new start
  state_, _eliminated the ε transitions_, and _removed the unit rules_

you will produce 

* an XML automaton element describing an equivalent grammar but where
  every rule has at most two symbols on the right-hand side.

* a file `exam3-normalize.txt` describing your overall algorithm for
  solving this problem. You should walk us through your data types,
  your overall approach, the specific subroutines you implement to
  help solve this problem and the purposes of each, and any
  preconditions or invariants upon which you rely. I mean these
  specifically for the grammar transformation part; you do not need to
  e.g. recapitulate our XML format.

**HINTS**:

* **Consider carefully some special cases** What happens if your
  grammar has a production `G -> G` in it? What if it has a production
  `A -> B` `B -> a` and `A -> a`? What about chains, including cycles like
  `A -> B` `B -> C` and `C -> A`? 
  
* **Remember the caveats from the last problem, too**
  
* **Notice the description of step 4 in Example 2.10** In Example 2.1
  Sipser actually disobeys his own algorithm, in order to simplify his
  presentation. 
  
* You should be able to write your `run-exam3-chomsky` Makefile target as follows:
  EDIT: What I wrote was inaccurate, because they are taking filenames as arguments. 
  Instead, just call you other targets in sequence, piping the output to an intermediate file. 
  Or you can choose to write a separate file that does the work of chaining your earlier procedures together, if you wish.


  You can test your program with these files:

  * [`jflap-without-epsilons.jff`]({{ site.baseurl }}/assets/docs/jflap-without-epsilons.jff)
  * [`jflap-without-epsilons-2.jff`]({{ site.baseurl }}/assets/docs/jflap-without-epsilons-2.jff)
  * [`jflap-without-units.jff`]({{ site.baseurl }}/assets/docs/jflap-without-units.jff)
  * [`jflap-without-units-2.jff`]({{ site.baseurl }}/assets/docs/jflap-without-units-2.jff)
  * [`jflap-basic-grammar.jff`]({{ site.baseurl }}/assets/docs/jflap-basic-grammar.jff)

Your solution will be automatically tested as follows:

* **Input** (from `stdin`): the name of **an XML file** containing a
  CFG.

* Expected **Output** (to `stdout`): an automaton XML string
  containing a CFG that recognizes the same language, but that does
  not contain any unit rules.

* `Makefile` **target name**: `run-exam3-remove-units`

* **Examples**:

  `printf "jflap-without-epsilons.jff" | make -sf Makefile run-exam3-remove-units`

  Output:

```
<structure>
<type>grammar</type>
<production>
<left>S</left>
<right>a</right>
</production>
<production>
<left>S</left>
<right>b</right>
</production>
<production>
<left>A</left>
<right>a</right>
</production>
<production>
<left>B</left>
<right>a</right>
</production>
<production>
<left>A</left>
<right>b</right>
</production>
</structure>
```

  `printf "jflap-without-epsilons-2.jff" | make -sf Makefile run-exam3-remove-units`

  Output:

```
<structure>
<type>grammar</type>
<production><left>B</left><right>FE</right></production>
<production><left>D</left><right>FE</right></production>
<production><left>A</left><right>FE</right></production>
<production><left>C</left><right>FE</right></production>
<production><left>F</left><right>a</right></production>
<production><left>E</left><right>FE</right></production>
<production><left>E</left><right>b</right></production>
</structure>
```

* **Input** (from `stdin`): the name of **an XML file** containing a
  CFG .

* Expected **Output** (to `stdout`): an automaton XML string
  containing a CFG that recognizes the same language, but that does
  not contain any rules with right-hand sides of length three or
  greater.

* `Makefile` **target name**: `run-exam3-normalize`

* **Examples**:

  `printf "jflap-without-units.jff" | make -sf Makefile run-exam3-normalize`

  Output:

```
<structure>
<type>grammar</type>
<production>
<left>S</left>
<right>GP</right>
</production>
<production>
<left>G</left>
<right>a</right>
</production>
<production>
<left>P</left>
<right>HQ</right>
</production>
<production>
<left>H</left>
<right>b</right>
</production>
<production>
<left>Q</left>
<right>IX</right>
</production>
<production>
<left>I</left>
<right>c</right>
</production>
<production>
<left>X</left>
<right>AB</right>
</production>
<production>
<left>B</left>
<right>g</right>
</production>
<production>
<left>A</left>
<right>f</right>
</production>
</structure>
```

  `printf "jflap-without-units-2.jff" | make -sf Makefile run-exam3-normalize`

  Output:

```
<structure>
<type>grammar</type>
<production><left>F</left><right>KJ</right></production>
<production><left>E</left><right>PO</right></production>
<production><left>O</left><right>NG</right></production>
<production><left>N</left><right>t</right></production>
<production><left>P</left><right>p</right></production>
<production><left>H</left><right>AB</right></production>
<production><left>B</left><right>CI</right></production>
<production><left>C</left><right>e</right></production>
<production><left>A</left><right>d</right></production>
<production><left>D</left><right>ML</right></production>
<production><left>L</left><right>Ey</right></production>
<production><left>M</left><right>b</right></production>
<production><left>J</left><right>HD</right></production>
<production><left>K</left><right>x</right></production>
<production><left>I</left><right>z</right></production>
<production><left>G</left><right>f</right></production>
</structure>
```

* **Input** (from `stdin`): the name of **an XML file** containing a
  CFG .

* Expected **Output** (to `stdout`): an automaton XML string
  containing a CFG that recognizes the same language, but that does
  not contain any rules with right-hand sides of length three or
  greater.

* `Makefile` **target name**: `run-exam3-chomsky`

* **Examples**:

  `printf "jflap-basic-grammar.jff" | make -sf Makefile run-exam3-chomsky`

  Output:

```
<structure>
<type>grammar</type>
<production><left>G</left><right>JB</right></production>
<production><left>A</left><right>HU</right></production>
<production><left>U</left><right>TH</right></production>
<production><left>T</left><right>J</right></production>
<production><left>I</left><right>JA</right></production>
<production><left>B</left><right>HS</right></production>
<production><left>S</left><right>RH</right></production>
<production><left>R</left><right>J</right></production>
<production><left>I</left><right>HQ</right></production>
<production><left>Q</left><right>PH</right></production>
<production><left>P</left><right>J</right></production>
<production><left>G</left><right>HC</right></production>
<production><left>C</left><right>DH</right></production>
<production><left>D</left><right>J</right></production>
<production><left>I</left><right>JO</right></production>
<production><left>O</left><right>NH</right></production>
<production><left>N</left><right>H</right></production>
<production><left>G</left><right>JE</right></production>
<production><left>E</left><right>FH</right></production>
<production><left>F</left><right>H</right></production>
<production><left>H</left><right>ML</right></production>
<production><left>L</left><right>Kc</right></production>
<production><left>K</left><right>b</right></production>
<production><left>M</left><right>a</right></production>
<production><left>G</left><right>HH</right></production>
<production><left>I</left><right>HH</right></production>
<production><left>J</left><right>f</right></production>
</structure>
```


## 3. A 1\# Duplicating Program

We saw before quines, programs that write their own source code, and
we saw pairs of programs that write one another. Here's yet another
take on programs that print programs. Now I want you to write a
program that produces two copies of its own source. The security
conscious among you may recognize such a program as a relative of a
[rabbit virus](https://en.wikipedia.org/wiki/Fork_bomb).


**Your Tasks**

Using the same techniques and sub-programs you used in the past
(`diag`, `write`, `move`, etc) produce 

* a program that writes two copies of
its own source code. That is to say, you should write a program $p$
such that $φ_{p}() = p + p$. Write your program in a file named
`exam3-duplicating-program.trm`.

* a description of what your program does and why. If you can only
  complete a portion of the program, you can use this to provide a
  description of your partial solution, and an explanation of what you
  think is missing. Submit this in `exam3-duplicating-program.txt`.

** Examples ** 

  We will test your program as follows:

  * You have a program that produces some output.
    ```
    cat exam3-duplicating-program.trm | ./trm 100000 -1 2>&1 | tail -n 1 
	```
	This should produce two copies of your program as a result. 

  * You have a program that produces some output and when we run it on its own output it again produces output 
    ```
	cat exam3-duplicating-program.trm | ./trm 100000 -1 2>&1 | tail -n 1 | ./trm 100000 -1 2>&1 | tail -n 1 
	``` 
    This should produce four copies of your program as a result
	
  * You have a program that, when we submit it twice, is the same as running your program twice
    ```
	diff <(cat exam3-duplicating-program.trm exam3-duplicating-program.trm | ./trm 100000 -1 2>&1) <(cat exam3-duplicating-program.trm | ./trm 100000 -1 2>&1 | tail -n 1 | ./trm 100000 -1 2>&1 | tail -n 1) 
	``` 
	Running your program through trm twice should be the same as running two copies of your program through trm once. 

## 4. Undecidability by Reduction

Consider the below definition of language $A$:

$ \textrm {A} = \\{\langle M \rangle \mid M \textrm{ is a Turing machine that accepts exactly all the odd length strings}\\}$

**Your Tasks**

Show that $A$ undecidable by constructing a reduction to $A$ from some
undecidable language. Describe, using prose, prose-y pseudocode, or a
mixture of both, a TM deciding membership in $A$. Your answer should
resemble the proofs in Section 5.1 of Sipser. Submit this in a file
named `exam3-undecidability-by-reduction.txt`.

**HINTS**:

* **You should consider the variety of undecidable languages we studied.**


## 5. Graph Components

In a directed graph, a **weakly connected component** is a subgraph
where all the nodes of that subgraph are connected to each other by an
_undirected_ path along the edges. Show that the following language is
in $\textbf{P}$ by describing an algorithm polynomial in the size of
the graph G to decide membership in $\textrm{2COMPONENTS}$.

$ \textrm{2COMPONENTS} =  \\{ \left \langle G \right \rangle \mid G \textrm{ is a directed graph and has at least two weakly connected components} \\}$

**Your Task**

Describe---using prose, prose-y pseudocode, or a mixture of both---an
informal description of your algorithm to decide membership in
$\textrm{2COMPONENTS}$. You may use assume as "library routines" any
polynomial-time algorithms we have discussed in class or on homework.
You should argue that your algorithm is polynomial time in the style
you used on Homework 10 problems 2 and 3. Note, you do not need to
implement this algorithm. Submit this in a file named
`exam3-graph-components.txt`. 

**HINTS**:

* **Recall how we measured the size of a graph.**


