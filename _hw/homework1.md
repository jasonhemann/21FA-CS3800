---
title: "Homework 1"
layout: single
---

### Objectives 

  - Explore deterministic finite-state automata (DFAs) using code. 
  - Define a representation for DFAs in the datatypes of your language
  - Implement your first DFA
  
This short assignment starts exploring deterministic finite automata
(DFAs) using code.

**Homework Problems**

* A Data Representation for DFAs (4 points) (3 pts manually graded)

* A First DFA (5 points)

* README.md (1 point)

**Total**: 10 points

**Submitting**

Submit your solution to this assignment in Gradescope.

A correct submission must include the following files (**NOTE**:
everything is case-sensitive):

* a `Makefile` with the following targets:

  * `setup` (optional)

  * `run-hw1-dfa`

* a file `README.md` containing your DFA data representation (see A
  Data Representation for DFAs), and the other required information,

* and finally, files containing the solution to each problem.

## 1. A Data Representation for DFAs

Since DFAs are a model of computation, we will use code as one way to
study them. 

To manipulate anything with code, we must have a representation, i.e.,
a _data representation_, of that thing in our program. Note that this
representation is distinct from the actual thing being studied and can
vary from program to program.

For example, we might choose to represent a phone number as a 32-bit
integer. The natural numbers are a mathematical concept and can have
many ​_different_​ representations in code, e.g., `Int`, `BigInt`,
`Float`, `Double`, etc. Each of those choices has benefits and
deficiencies. Other real-world concepts, say a phone book, or a
network of people, might require more sophisticated data structures,
e.g., a dict or a graph, respectively, to represent them in a program.

**Your Tasks**

* Recall Definition 1.5 from the book: a DFA is a 5-tuple
  $\(Q,\Sigma,\delta,q\_0,F\$), where:

  * $Q$ is a finite set called the states,

  * $\Sigma$ is a finite set called the alphabet,

  * $\delta:Q\times\Sigma\rightarrow Q$ is the transition function,

  * $q\_0\in Q$ is the start state, and

  * $F\subseteq Q$ is the set of accept states.

  Our first task is to design a data representation for this
  mathematical DFA definition.

  You may use objects, structs, or anything else available in your
  language.

  You may need to create multiple data representations, for various
  parts of the DFA.

* Write up an informal description of your chosen representation in a
  section of your README.md file, labeled `DFA Data Representation`.
  See the source code of this file if you do not know how to create a
  section in markdown.

  For example, here's one in Racket:

```
# DFA Data Representation: 
                                                        
  A State is a string
  A Symbol is a 1-char string

  A DFA is a (struct states alpha delta start accepts) where:
  - states is a list of State
  - alpha is a list of Symbol
  - delta is a hash of State Symbol -> Symbol
  - start is a State
  - accept is a list of State
```

  Note that `struct`s, `string`s, `list`s, and `hash`es are data
  structures in my language. Your data representation will vary
  depending on your chosen language and the available constructs in that
  language. For example, if you’re using Java, you might choose an
  `Object` instead of a `struct`.

## 2. A First DFA

Now we will implement our DFA data representation and use it to create a
DFA.

**Your Tasks**

* Implement your data representation in your chosen language.

* Write a program that implements the DFA from **Figure 1.4** of the
  textbook ​_as an instance of the DFA data representation that you have
  chosen_​. This program must also respond to the following `stdin`
  inputs as follows:

  * `states`: print out the states, one per line, in no particular order

  * `alpha`: print out the alphabet, one char per line, in no particular
    order

  * `transitions`: print out, in no particular order, each possible
    transition on its own line: "from" state first, followed by input
    char, followed by "to" state, with a space separating each.

  * `start`: print out the start state, on its own line

  * `accepts`: print out the accept states, one per line, in no
    particular order

* **Example**:

  `printf "states" | make -sf Makefile run-hw1-dfa`

  Output:

```
  q1
  q2
  q3
```

  `printf "transitions" | make -sf Makefile run-hw1-dfa`

  Output:

```
  q1 0 q1
  q1 1 q2
  q2 0 q3
  q2 1 q2
  q3 0 q2
  q3 1 q2
```

**NOTE**: Don’t submit a program that just directly prints the expected
outputs, e.g., `printf "q1\nq2\nq3\n"`. The program must actually
construct an instance of your DFA data structure, and then query it
to produce to the requested information.

\(We will check all submitted code to make sure.\)
