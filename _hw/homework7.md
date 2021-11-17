---
title: "Homework 7"
layout: single
---

## Still drafty but better 


### Objectives 

  - Explore PDAs viz. CFLs and CFGs

**Homework Problems**

* [Represent and Produce a PDA](#1-represent-and-produce-a-pda) (2 pts, 1 manually graded)

* [NFA->PDA](#2-regular-langs-are-context-free) (2 pts)

* [`run` for a PDA](#3-run-a-pda) (2 pts)

* [CFG->PDA](#4-convert-a-cfg) (2 pts)

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

  * `run-hw7-representation`
  
  * `run-hw7-nfa2pda`

  * `run-hw7-run`

  * `run-hw7-cfg2pda`

* a `README` containing the required information,

* the source code files needed by your `Makefile`,

## 1. Represent and Produce a PDA

For this problem I want you to design PDAs.

Recall Definition 2.13 from textbook book. A PDA is an $6$-tuple
$\(Q, \Sigma, \Gamma, \delta, q_{0}, F\)$, where:

* $Q$ is the set of states

* $\Sigma$ is the input alphabet

* $\Gamma$ is the stack alphabet

* $\delta: \times \Sigma_{\epsilon} \times \Gamma_{\epsilon} \longrightarrow \textit{P}(Q \times \Gamma_{\epsilon})$ is the transition function

* $q_{0} \in Q$ is the start state and 

* $F \subseteq Q$ is the set of accept states.

Given an English language description of a context free language, you
will write in your own internal representation a grammar generating
that language. Your grammar should be /unambiguous/. You will also
construct a function `CFG->XML` to output the result as an XML
element. Create a CFG that generates the following language L. You can
assume alphabet $\Sigma = \\{(,),[,]\\}$.

### NB. AFAIK, no benefit from switching the language.

$ L = \\{w \mid w = \textrm{ is a string of well-balanced matching brackets}\\}$. 


**Your Tasks**

* Design a data representation for this formal definition of PDAs. You
  may use objects, structs, or anything else available in your language.

* Write up an informal description of your chosen representation in a
  section of your README, labeled `PDA Data Representation`.

* Implement your data representation in your chosen language.

* Create a PDA that accepts the given language L. Your PDA is not
  required to terminate on strings in $\Sigma^{\*} \setminus L$.

* Construct a function `PDA->XML` to output the result as an XML

You will produce as output an XML `structure` element containing the
productions of your grammar for this language. We will certainly
exercise your output by testing it against a sequence of strings in
the language.

Your solution will be tested as follows:

* **Input** (from `stdin`): Nothing

* Expected **Output** (to `stdout`): an XML `structure` element,
  containing a PDA recognizing your language. Note we will manually
  inspect that you are in fact constructing the PDA and not just
  printing the output.

* `Makefile` **target name**: `run-hw7-representation`

* **Example**:

  `make -sf Makefile run-hw7-representation`

  Output: (a PDA with a language equivalent to that of)

```
<structure>
<type>pda</type>
<automaton>
<state id="0" name="q0">
<initial/>
</state>
<state id="3" name="q3">
</state>
<state id="1" name="q1">
</state>
<state id="2" name="q2">
<final/>
</state>
<transition>
<from>1</from>
<to>1</to>
<read>[</read>
<pop>[</pop>
<push/>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read>(</read>
<pop>(</pop>
<push/>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read>]</read>
<pop>]</pop>
<push/>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read>)</read>
<pop>)</pop>
<push/>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>F</pop>
<push>SB</push>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>S</pop>
<push>CE</push>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>S</pop>
<push>AB</push>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>S</pop>
<push>CD</push>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>S</pop>
<push>SS</push>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>S</pop>
<push/>
</transition>
<transition>
<from>1</from>
<to>2</to>
<read/>
<pop>$</pop>
<push/>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>E</pop>
<push>SD</push>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>S</pop>
<push>AF</push>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>C</pop>
<push>(</push>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>D</pop>
<push>)</push>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>A</pop>
<push>[</push>
</transition>
<transition>
<from>0</from>
<to>3</to>
<read/>
<pop/>
<push>$</push>
</transition>
<transition>
<from>3</from>
<to>1</to>
<read/>
<pop/>
<push>S</push>
</transition>
<transition>
<from>1</from>
<to>1</to>
<read/>
<pop>B</pop>
<push>]</push>
</transition>
</automaton>
</structure>
``` 

### Testing

I'm going to be able to test this by reading in your PDA and make sure
it accepts on some known strings in the language. I have my CFG->CNF
implementation, but not PDA->CFG, so I won't automatically check that
the language of the grammar is *exactly* the language in question.

## 2. Regular Langs are Context Free 

You will prove, by construction, the statement: "Every regular
language is context-free.". You will prove this statement by reading
in the XML description of an NFA, and producing as output an XML
description of a PDA that recognizes the same language. You will
likely find your work on NFAs from earlier assignments helpful. 

Your solution will be tested as follows:

* **Input** (from `stdin`): name of an XML file describing a JFLAP
  NFA.

* Expected **Output** (to `stdout`): an XML `structure` element,
  containing a PDA recognizing that same language. 

* `Makefile` **target name**: `run-hw7-nfa2pda`

* **Example**:

  `printf "nfa-efgstar.jff" | make -sf Makefile run-hw7-nfa2pda`

  Output: (a PDA with a language equivalent to that of)

```
<automaton>
<state id="0" name="A-0"><initial/></state>
<state id="1" name="A-1"><final/></state>
<state id="2" name="A-2"></state>
<state id="3" name="A-3"></state>
<state id="4" name="A-4"></state>
<state id="5" name="A-5"></state>
<state id="6" name="A-6"></state>
<state id="7" name="A-7"></state>
<state id="8" name="A-8"></state>
<state id="9" name="A-9"></state>
<transition><from>3</from><to>1</to><read/><pop/><push/></transition>
<transition><from>6</from><to>7</to><read>f</read><pop/><push/></transition>
<transition><from>7</from><to>8</to><read/><pop/><push/></transition>
<transition><from>8</from><to>9</to><read>g</read><pop/><push/></transition>
<transition><from>1</from><to>0</to><read/><pop/><push/></transition>
<transition><from>0</from><to>1</to><read/><pop/><push/></transition>
<transition><from>0</from><to>2</to><read/><pop/><push/></transition>
<transition><from>2</from><to>4</to><read/><pop/><push/></transition>
<transition><from>4</from><to>5</to><read>e</read><pop/><push/></transition>
<transition><from>5</from><to>6</to><read/><pop/><push/></transition>
<transition><from>9</from><to>3</to><read/><pop/><push/></transition>
</automaton>
```

### NB. Testing 

We will test your assignment by testing your PDA on a variety of
strings in the language of the NFA. Even though all *good* solutions
are guaranteed to be PDAs describing regular languages, I need to be
prepared to test *arbitrary* PDAs, because I need to be able to also
determine *wrong* answers. 

## 3. Run a PDA

This problem asks you to demonstrate that you to implement `run` for a
PDA. There are two classes of problems we can ask you about: the PDAs
for which evaluation is guaranteed to terminate, and those for which
it is *not* guaranteed to terminate. You'll have to write your `run`
program so that it will terminate when it can. 

We will also have you optionally take a maximum number, an upper
bound, for the number of transitions to make (in any individual path,
so non-deterministically trying each of 5 different choices from state
A only counts as one in each of those individual paths). So if your
machine accepts within $n$ steps, you `accept`. If your PDA finitely
halts for all paths through the machine and none of the paths through
that machine accept, or none of the paths through the machine accept
within $n$ steps, reject.

Your task is to accept a string in $\Sigma^{\*}$ when that string is in
the language of the machine. If we give you that upper bound, `reject`
when the PDA we give you does not accept within the maximum number of
steps. Further, when the PDA we give you is a decider, your
implementation should also reject a string in $\Sigma^{\*}$ when that
string is not in the language of the machine. Because of exponential
blow-up, we will only exercise this latter capacity on small examples.

Characterizing the PDAs that are deciders isn't as simple as "no
epsilon-push loops"---consider other loops for instance, that
repeatedly push and pop the same symbol.

**Your Tasks**

* Given a string in $\Sigma^{\*}$, accept if the string is in the
  language of the machine, reject if the string is not accepted within
  a given bound, or if the machine is a decider, reject if the string
  is not in the language of the machine.

Your solution will be tested as follows:

* **Input** (from `stdin`): A `.jff` file describing a PDA, a string
  over the alphabet of the PDA, *and optionally a max number of
  transitions in a path to look for before rejecting*, separated by a
  space.

* Expected **Output** (to `stdout`): 

    * `accept`, if this string is in the language of the grammar,

    * `reject`, if the PDA terminates in all paths through the machine
      and this string is not in the language of the grammar.
	  
	* otherwise, it's behavior is undefined.  

* `Makefile` **target name**: `run-hw7-run`

* **Example**:

  `printf "types-pda.jff {fst:t1,snd:t2}" | make -sf Makefile run-hw7-run`

  Output: `accept`

  `printf "types-pda.jff {fst:t1,snd:t2} 50" | make -sf Makefile run-hw7-run`

  Output: `accept`

  `printf "terminating-types-pda.jff {f:stt1s,nd:a}n 50" | make -sf Makefile run-hw7-verify`

  Output: `reject`

## 4. Convert a CFG

You will implement a program that, given a JFLAP XML description of a
CFG, will return a JFLAP XML description of a PDA with an equivalent
language to the language of the CFG. Recall that two languages are
equivalent when they contain the same strings. We will test that your
PDA accepts strings that it should. We will not *directly* test that
your PDA accepts only those strings. 

**Your Tasks**

Your solution will be tested as follows:

* **Input** (from `stdin`): A `.jff` file describing a CFG.

* Expected **Output** (to `stdout`): an XML `structure` element,
  containing a PDA recognizing the language of the CFG.

* `Makefile` **target name**: `run-hw7-cfg2pda`

* **Example**:

  `printf "types.jff" | make -sf Makefile run-hw7-cfg2pda`

  Output: 
  
  ```

  ```

  `printf "terminating-types-pda.jff" | make -sf Makefile run-hw7-cfg2pda`

  Output: 
  
  ```
  
  ```

## NB. Testing

We will have to test that by transforming your machine to a CFG,
transforming that CFG to CNF, and transforming the resulting CFG
*back* to a PDA, and then testing _that_ PDA.

Dang. It'd be easier if I had *you* all write those programs and then
I could test them more directly. I could just give you the tests and
have you all implement them. 

Need also to think about the time complexity of the solutions we come
up with. I know there are *significantly* more efficient mechanisms
for doing some of these things, but I haven't programmed them, so I
don't know how complicated they are to get right, or how tedious, or
how much more efficient they are in practice.
