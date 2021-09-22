---
title: "Homework 3"
layout: single
---

### Objectives 

   - Explores non-deterministic finite automata (NFAs) using code.

**Homework Problems**

* A Data Representation for NFAs (3 points, manually graded)

* NFAs and the Language They Recognize (2 points)

* The Union Operation, on NFAs (2 points)

* NFA -> DFA  (2 points)

* `README` (1 point)

**Total**: 10 points

**Submitting**

Submit the solution to this assignment in Gradescope.

A submission must include the following files (**NOTE**: everything is
case-sensitive):

* a `Makefile` with the following targets:

  * `setup` (optional)

  * `run-hw3-nfalang`

  * `run-hw3-union`

  * `run-hw3-nfa2dfa` (optional)

* a `README` containing an NFA data representation (see A Data
  Representation for NFAs), and the other required information,

* the source code files needed by your `Makefile`,

* and a pdf or plain-text file containing the answer to NFAs vs DFAs.

## 1. A Data Representation for NFAs

Recall Definition 1.37 from the book. An NFA is a 5-tuple
$\(Q,\Sigma,\delta,q\_0,F\)$, where:

* $Q$ is a finite set of states,

* $\Sigma$ is a finite alphabet,

* $\delta:Q\times\Sigma\_\epsilon\rightarrow \mathcal{P}(Q)$ is the
  transition function mapping a state and a (possibly empty string)
  input to a ​_set of states_​,

* $q\_0\in Q$ is the start state, and

* $F\subseteq Q$ is the set of accept states.

It’s nearly identical to the definition for DFAs, except for the
transition function.

**Your Tasks**

* Design a data representation for this formal definition of NFAs. You
  may use objects, structs, or anything else available in your language.

* Write up an informal description of your chosen representation in a
  section of your README, labeled `NFA Data Representation`.

* Implement your data representation in your chosen language.

## 2. NFAs and the Language They Recognize

This problem asks to demonstrate that you understand computation with
NFAs.

The language that an NFA recognizes is the set of all strings accepted
by the NFA.

**Your Tasks**

* Write a predicate that takes an input string and an instance of your
  NFA and "runs" it on the NFA. It should return true if the NFA accepts
  the input, and false otherwise.

* Write a function or method that receives an XML file containing an
  automaton element and constructs an instance of your NFA.

  **NOTE**: The XML structure for an NFA is the same as a DFA, except:

  * NFAs may have multiple transitions with the same `from` and
    `read`.

    For example, Figure 1.27’s XML below has two `transition`s for `from
    1`, `read 1`:

```
    <transition><from>1</from><to>1</to><read>1</read></transition>
    <transition><from>1</from><to>2</to><read>1</read></transition>
```

  * Also, the `read` element may be empty. This represents an
    $\varepsilon$ empty string transition.

    For example, Figure 1.27’s XML given below has:

```
    <transition><from>2</from><to>3</to><read/></transition>
```

  You must decide how to parse and organize these in your
  representation.

* Using your predicate from above, write a function or method that,
  given an NFA, prints all strings in the language that it recognizes,
  up to strings of length 5, one per line.

  You may find your solution to an earlier problem useful here.

Your solution will be tested as follows:

* **Input** (from `stdin`): XML file name, containing an NFA automaton
  element

* Expected **Output** (to `stdout`):      all strings in the language of
  the NFA, up to strings of length 5, one string per line

* `Makefile` **target name**: `run-hw3-nfalang`

* **Example**:

  You can test your program with [this file named
  `fig1.27-nfa.jff`]({{ site.baseurl }}/assets/docs/fig1.27-nfa.jff) containing the NFA from figure
  1.27 of the textbook.

  `printf "fig1.27-nfa.jff" | make -sf Makefile run-hw3-nfalang`

  Output:

```
  00011
  00101
  00110
  00111
  01010
  01011
  01100
  01101
  01110
  01111
  10011
  10100
  10101
  10110
  10111
  11000
  11001
  11010
  11011
  11100
  11101
  11110
  11111
  0011 
  0101 
  0110 
  0111 
  1010 
  1011 
  1100 
  1101 
  1110 
  1111 
  011
  101
  110
  111
  11
```

## 3. The Union Operation, on NFAs

This problem asks you to demonstrate that you understand the NFA-based
proof showing that the union operation is closed for regular languages.

**Your Task**

Implement the union operation for NFAs. It should be much easier than
the DFA version.

Specifically, write a function that, given:

* an NFA recognizing language $A\_1$, and

* an NFA recognizing language $A\_2$

returns an NFA recognizing $A\_1 \cup A\_2$.

To do this, you’ll need to be able to extract individual components of
an NFA instance, e.g., the states, transitions, etc., and use them to
create a new NFA.

**HINTS**:

* When combining NFAs **be careful with duplicate state names**. The
  input NFAs may use the same state names, so you may want to first
  rename them to something unique.

* One or two tests may use input NFAs with **different alphabets**. In
  these cases, the new machine will not only have to combine the
  alphabets, but it may also have to add new transitions to each machine
  to handle the new input symbols.

Your solution will be tested as follows:

* **Input** (from `stdin`): the names of **two XML files**, separated by
  a space, each containing an automaton element representing an NFA

* Expected **Output** (to `stdout`):    an automaton XML string
  representing an NFA that is the union of the two inputs

* `Makefile` **target name**: `run-hw3-union`

* **Example**:

  You can test your program with these files:

  * [`nfa-a.xml`](nfa-a.xml): recognizes the language $\{"a"\}$

  * [`nfa-b.xml`](nfa-b.xml): recognizes the language $\{"b"\}$

  `printf "nfa-a.xml nfa-b.xml" | make -sf Makefile run-hw3-union`

  Output:

```
  <automaton>
  <state id="q217" name="q217"><initial/></state>
  <state id="1" name="1"></state>
  <state id="2" name="2"><final/></state>
  <state id="3" name="3"></state>
  <state id="1214" name="1214"></state>
  <state id="2215" name="2215"><final/></state>
  <state id="3216" name="3216"></state>
  <transition><from>q217</from><to>1</to><read/></transition>
  <transition><from>q217</from><to>1214</to><read/></transition>
  <transition><from>1</from><to>2</to><read>a</read></transition>
  <transition><from>1</from><to>3</to><read>b</read></transition>
  <transition><from>2</from><to>3</to><read>a</read></transition>
  <transition><from>2</from><to>3</to><read>b</read></transition>
  <transition><from>3</from><to>3</to><read>a</read></transition>
  <transition><from>3</from><to>3</to><read>b</read></transition>
  <transition><from>1214</from><to>3216</to><read>a</read></transition>
  <transition><from>1214</from><to>2215</to><read>b</read></transition>
  <transition><from>2215</from><to>3216</to><read>a</read></transition>
  <transition><from>2215</from><to>3216</to><read>b</read></transition>
  <transition><from>3216</from><to>3216</to><read>a</read></transition>
  <transition><from>3216</from><to>3216</to><read>b</read></transition>
  </automaton>
```

## 4. NFA -> DFA (Optional Bonus)

This problem asks you to demonstrate that you understand the proof of
Theorem 1.39.

In other words, implement a function or method that converts an NFA from
the A Data Representation for NFAs problem to a DFA (from \[missing\],
\[missing\] problem).

Your solution should emit a DFA `automaton` XML element. The solution
from HW2 will be useful here: use the solution from \[missing\] to write
the XML output, and use the solution from \[missing\] to check that your
output is actually a valid DFA.

Your solution will be tested as follows:

* **Input** (from `stdin`): the name of an XML file containing an
  automaton element representing an NFA

* Expected **Output** (to `stdout`):      an automaton element
  representing an equivalent DFA

* `Makefile` **target name**: `run-hw3-nfa2dfa`

* **Example**:

  You can test your program with this file: [`fig1.27-nfa.jff`]({{
  site.baseurl }}/assets/docs/fig1.27-nfa.jff)

  `printf "fig1.27-nfa.jff" | make -sf Makefile run-hw3-nfa2dfa`

  Output:

```
  <automaton>
  <state id="()" name="()"></state>
  <state id="(q1)" name="(q1)"><initial/></state>
  <state id="(q2)" name="(q2)"></state>
  <state id="(q1 q2)" name="(q1 q2)"></state>
  <state id="(q3)" name="(q3)"></state>
  <state id="(q1 q3)" name="(q1 q3)"></state>
  <state id="(q2 q3)" name="(q2 q3)"></state>
  <state id="(q1 q2 q3)" name="(q1 q2 q3)"></state>
  <state id="(q4)" name="(q4)"><final/></state>
  <state id="(q1 q4)" name="(q1 q4)"><final/></state>
  <state id="(q2 q4)" name="(q2 q4)"><final/></state>
  <state id="(q1 q2 q4)" name="(q1 q2 q4)"><final/></state>
  <state id="(q3 q4)" name="(q3 q4)"><final/></state>
  <state id="(q1 q3 q4)" name="(q1 q3 q4)"><final/></state>
  <state id="(q2 q3 q4)" name="(q2 q3 q4)"><final/></state>
  <state id="(q1 q2 q3 q4)" name="(q1 q2 q3 q4)"><final/></state>
  <transition><from>()</from><to>()</to><read>0</read></transition>
  <transition><from>()</from><to>()</to><read>1</read></transition>
  <transition><from>(q1)</from><to>(q1)</to><read>0</read></transition>
  <transition><from>(q1)</from><to>(q1 q2 q3)</to><read>1</read></transition>
  <transition><from>(q2)</from><to>(q3)</to><read>0</read></transition>
  <transition><from>(q2)</from><to>()</to><read>1</read></transition>
  <transition><from>(q1 q2)</from><to>(q1 q3)</to><read>0</read></transition>
  <transition><from>(q1 q2)</from><to>(q1 q2 q3)</to><read>1</read></transition>
  <transition><from>(q3)</from><to>()</to><read>0</read></transition>
  <transition><from>(q3)</from><to>(q4)</to><read>1</read></transition>
  <transition><from>(q1 q3)</from><to>(q1)</to><read>0</read></transition>
  <transition><from>(q1 q3)</from><to>(q1 q2 q3 q4)</to><read>1</read></transition>
  <transition><from>(q2 q3)</from><to>(q3)</to><read>0</read></transition>
  <transition><from>(q2 q3)</from><to>(q4)</to><read>1</read></transition>
  <transition><from>(q1 q2 q3)</from><to>(q1 q3)</to><read>0</read></transition>
  <transition><from>(q1 q2 q3)</from><to>(q1 q2 q3 q4)</to><read>1</read></transition>
  <transition><from>(q4)</from><to>(q4)</to><read>0</read></transition>
  <transition><from>(q4)</from><to>(q4)</to><read>1</read></transition>
  <transition><from>(q1 q4)</from><to>(q1 q4)</to><read>0</read></transition>
  <transition><from>(q1 q4)</from><to>(q1 q2 q3 q4)</to><read>1</read></transition>
  <transition><from>(q2 q4)</from><to>(q3 q4)</to><read>0</read></transition>
  <transition><from>(q2 q4)</from><to>(q4)</to><read>1</read></transition>
  <transition><from>(q1 q2 q4)</from><to>(q1 q3 q4)</to><read>0</read></transition>
  <transition><from>(q1 q2 q4)</from><to>(q1 q2 q3 q4)</to><read>1</read></transition>
  <transition><from>(q3 q4)</from><to>(q4)</to><read>0</read></transition>
  <transition><from>(q3 q4)</from><to>(q4)</to><read>1</read></transition>
  <transition><from>(q1 q3 q4)</from><to>(q1 q4)</to><read>0</read></transition>
  <transition><from>(q1 q3 q4)</from><to>(q1 q2 q3 q4)</to><read>1</read></transition>
  <transition><from>(q2 q3 q4)</from><to>(q3 q4)</to><read>0</read></transition>
  <transition><from>(q2 q3 q4)</from><to>(q4)</to><read>1</read></transition>
  <transition><from>(q1 q2 q3 q4)</from><to>(q1 q3 q4)</to><read>0</read></transition>
  <transition><from>(q1 q2 q3 q4)</from><to>(q1 q2 q3 q4)</to><read>1</read></transition>
  </automaton>
```
