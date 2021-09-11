---
title: "Homework 2"
layout: single
---

### Objectives 

   - Continue exploring deterministic finite automata (DFAs) using code
   - Build upon previous assignments' code
   - Practice simulating computation

**Homework Problems**

* Simulating Computation for DFAs (2 points)

* DFAs and the Language They Recognize (2 points)

* DFA->XML (3 points)

* The Union Operation (2 points)

* README.md (1 point)

**Total**: 10 points 

**Submitting**

Submit your solution to this assignment in [Gradescope
`hw2`](https://www.gradescope.com/courses/219302/assignments/984728).

A submission must include the following files (**NOTE**: everything is
case-sensitive):

* a `Makefile` with the following targets:

  * `setup` (optional)

  * `run-hw2-dfa`

  * `run-hw2-dfalang`

  * `run-hw2-dfa2xml`

  * `run-hw2-union`

* a `README.md` containing the required information,

* and, files containing the solution to each problem.

## 1. Simulating Computation for DFAs

Recall the formal definition of computation from page 40 of the
textbook:

A finite automata $M = (Q,\Sigma,\delta,q\_0,F)$ _accepts_ a string $w =
w\_1,\ldots,w\_n$, where each character $w\_i \in \Sigma$, if there exists
a sequence of states $r\_0,\ldots,r\_n$, where $r\_i \in Q$, and:

* $r\_0=q\_0$

* $\delta(r\_i,w\_{i+1}) = r\_{i+1}, for i = 0,\ldots,n-1$

* $r\_n\in F$

This problem asks you to demonstrate, with code, that you understand
this concept.

**Your Tasks**

* Write a "run" predicate (a function or method that returns true or
  false) that takes two arguments, an instance of your DFA
  representation (as defined in an earlier assignment]) and a string,
  and "runs" the string on the DFA.

  The function should return true if the DFA accepts the string, and
  false otherwise.

* Then write a program that reads from `stdin` and feeds that input,
  along with the Figure 1.4’s DFA (i.e., the one created in an earlier
  assignment) to your "run" predicate. This program writes `accept` to
  `stdout` if the DFA accepts the input and `reject` otherwise.

  Your solution will be tested as follows:

  * `Makefile` **target name**: `run-hw2-dfa`

  * **Input** (from `stdin`): a (randomly generated) string in alphabet
    $\Sigma = \{`0`,`1`\}$

  * Expected **Output** (to `stdout`):

    * `accept`, if Figure 1.4’s DFA accepts input,

    * otherwise `reject` otherwise

  * **Example**:

    `printf "000111" | make -sf Makefile run-hw2-dfa`

    Output: `accept`

    `printf "10" | make -sf Makefile run-hw2-dfa`

    Output: `reject`

## 2. DFAs and the Language They Recognize

The ​_language_​ that a DFA _recognizes_ is the set of all strings
accepted by the DFA.

**Your Tasks**

* Write a function or method that, given an XML file containing an
  automaton element, constructs an instance of your DFA
  representation. You’ve already done the part of this which extracted
  the states, so now just extract the transitions.

* Using your predicate from Simulating Computation for DFAs, write a
  function or method that, given a DFA, prints all strings in the
  language that it recognizes, up to strings of length 5, one per line.

  You may find your solution to Homework 0 useful here.

Your solution will be tested as follows:

* `Makefile` **target name**: `run-hw2-dfalang`

* **Input** (from `stdin`): XML file name, containing a DFA automaton
  element

* Expected **Output** (to `stdout`): all strings in the language of
  the DFA, up to strings of length 5, one string per line (order
  doesn’t matter, since we’re printing a set)

* **Example**:

  You can test your program with [this file named `fig1.4.jff`]({{
  site.baseurl }}/assets/docs/fig1.4.jff) containing the DFA from
  Figure 1.4 of the textbook.

  `printf "fig1.4.jff" | make -sf Makefile run-hw2-dfalang`

  Output:

  `00001`
  `00011`
  `00100`
  `00101`
  `00111`
  `01001`
  `01011`
  `01100`
  `01101`
  `01111`
  `10000`
  `10001`
  `10011`
  `10100`
  `10101`
  `10111`
  `11001`
  `11011`
  `11100`
  `11101`
  `11111`
  `0001` 
  `0011` 
  `0100` 
  `0101` 
  `0111` 
  `1001` 
  `1011` 
  `1100` 
  `1101` 
  `1111` 
  `001`
  `011`
  `100`
  `101`
  `111`
  `01`
  `11`
  `1`

  **Example2**:

  You can test your program with [this file named `dfa-empty.jff`]({{
  site.baseurl }}/assets/docs/dfa-empty.jff) containing a DFA that
  only accepts the empty string.

  `printf "dfa-empty.jff" | make -sf Makefile run-hw2-dfa`

  Output:

   
   

  \(it’s an empty line)

## 3. DFA->XML

**Your Tasks**

* Write a function that converts an instance of your DFA to an XML
  string corresponding to an automaton element.

* Implement the "three 1’s" DFA from class as an instance of your DFA
  representation.

* Write a program that when run, calls your DFA->XML function with this
  DFA as argument, and prints the result to `stdout`.

Your solution will be tested as follows:

* `Makefile` **target name**: `run-hw2-dfa2xml`

* **Input** (from `stdin`): none

* Expected **Output** (to `stdout`): XML representing the "three 1s" DFA
  from class

**Note**: Whitespace doesn’t matter for XML. So something like:

    `<state id="q1" name="q1"><initial/></state>`

is equivalent to:

```
    <state id="q1" name="q1">
        <initial/>
    </state>
```

## 4. The Union Operation

This question will ask you to demonstrate, with code, that you
understand the proof showing that the union operation is closed for
regular languages (Theorem 1.25).

To do so, you will have to put together everything you’ve done so far in
the homeworks.

**Your Task**

Implement a union operation for your DFAs. Specifically, write a
function that, given:

* a DFA recognizing language $A\_1$, and

* a DFA recognizing language $A\_2$

returns a DFA recognizing $A\_1 \cup A\_2$.

This solution implements the algorithm from Theorem 1.25 of the textbook
(so rereading that will be helpful), thus proving it.

Your solution will be tested as follows:

* `Makefile` **target name**: `run-hw2-union`

* **Input** (from `stdin`): the names of **two XML files**, separated by
  a space, each containing an automaton element representing a DFA

* Expected **Output** (to `stdout`):    an automaton XML string
  representing a DFA that is the union of the two inputs

* **Example**:

  You can test your program with these files:

  * [`dfa-a.xml`](dfa-a.xml): recognizes the language $\{"a"\}$

  * [`dfa-b.xml`](dfa-b.xml): recognizes the language $\{"b"\}$

  `printf "dfa-a.xml dfa-b.xml" | make -sf Makefile run-hw2-union`

  Output:

```
  <automaton>
  <state id="(1 1)" name="(1 1)"><initial/></state>
  <state id="(1 2)" name="(1 2)"><final/></state>
  <state id="(1 3)" name="(1 3)"></state>
  <state id="(2 1)" name="(2 1)"><final/></state>
  <state id="(2 2)" name="(2 2)"><final/></state>
  <state id="(2 3)" name="(2 3)"><final/></state>
  <state id="(3 1)" name="(3 1)"></state>
  <state id="(3 2)" name="(3 2)"><final/></state>
  <state id="(3 3)" name="(3 3)"></state>
  <transition><from>(1 1)</from><to>(2 3)</to><read>a</read></transition>
  <transition><from>(1 1)</from><to>(3 2)</to><read>b</read></transition>
  <transition><from>(1 2)</from><to>(2 3)</to><read>a</read></transition>
  <transition><from>(1 2)</from><to>(3 3)</to><read>b</read></transition>
  <transition><from>(1 3)</from><to>(2 3)</to><read>a</read></transition>
  <transition><from>(1 3)</from><to>(3 3)</to><read>b</read></transition>
  <transition><from>(2 1)</from><to>(3 3)</to><read>a</read></transition>
  <transition><from>(2 1)</from><to>(3 2)</to><read>b</read></transition>
  <transition><from>(2 2)</from><to>(3 3)</to><read>a</read></transition>
  <transition><from>(2 2)</from><to>(3 3)</to><read>b</read></transition>
  <transition><from>(2 3)</from><to>(3 3)</to><read>a</read></transition>
  <transition><from>(2 3)</from><to>(3 3)</to><read>b</read></transition>
  <transition><from>(3 1)</from><to>(3 3)</to><read>a</read></transition>
  <transition><from>(3 1)</from><to>(3 2)</to><read>b</read></transition>
  <transition><from>(3 2)</from><to>(3 3)</to><read>a</read></transition>
  <transition><from>(3 2)</from><to>(3 3)</to><read>b</read></transition>
  <transition><from>(3 3)</from><to>(3 3)</to><read>a</read></transition>
  <transition><from>(3 3)</from><to>(3 3)</to><read>b</read></transition>
  </automaton>
```
