---
title: "Homework 7"
layout: single
---

### NB. 

This is still a draft form, I'm developing, and hoping to develop
_with_ you all this time rather than merely _for_ you all. I've been
under-utilizing a _great_ resource, having a class of knowledgeable
developers. So let's spec this out together, come up with some
examples we can use to test, nail down the wording, and go from there.

The tricky bit is still going to be what I can auto-grade and framing
the questions so that we can readily decide them. 


### Objectives 

  - Explore PDAs viz. CFLs and CFGs

**Homework Problems**

* [Represent and Produce a PDA](#1-represent-and-produce-a-pda) (2 pts, 1 manually graded)

* [NFA->PDA](#2-regular-langs-are-context-free) (2 pts)

* [`run` for a PDA](#3-run-a-pda) (2 pts)

* [CFG->PDA](#5-convert-a-cfg) (2 pts)

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

Recall Definition ?? from textbook book. A PDA is an $n$-tuple
$\(...\)$, where:

* 

* 

* 

* 

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
  required to terminate on strings in $\Sigma^{*} \setminus L$.

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

### NB. Creating the above and testing. 

Right now, I don't have my own implementation. So I took our Dyck
language, changed parens to curlies, turned the grammar to CNF, added
`S->epsilon`, converted that to a PDA in JFLAP, wrote the JFLAP
output, and then modified that to (1) use parens again (2) use `$` as
the empty stack marker again, (3) added an additional state because
JFLAP starts by adding two symbols to the stack at once. 

I'm going to be able to test this by reading in your PDA and then
running it on some accepting programs, and make sure it accepts.
*AND/OR* I'll have to take your PDA, convert it to a CFG, convert that
CFG to some normalized form (GNF, CNF) and run it on a
randomly-generated collection of inputs in the language of the machine
and ensure that it corresponds with some known-good solution. And
this'll all have to be my code because as you know, JFLAP limitations.

## 2. Regular Langs are Context Free 

You will prove, by construction, the statement: "Every regular
language is context-free.". You will prove this statement by reading
in the XML description of an NFA, and producing as output an XML
description of a PDA that recognizes the same language. You will
likely find your work on NFAs from earlier assignments helpful. 


We will test your assignment by testing your PDA on a variety of
strings in the language of the NFA. We will also test your
implementation by running (a transformed version of) the resulting PDA
against a variety of strings and verifying that your machine accepts
strings in the language and that it does not accept strings in
$\Sigma^{*}$ that are not in the language.


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
Haven't done it yet, but take it through JFLAP if you want an example for right now. 
```

### NB. Testing 

See once again the above limitations in testing, together w/our
difficulties in implementing equality of PDAs. Even though all *good*
solutions are guaranteed to be PDAs describing regular languages, I
need to be prepared to test *arbitrary* PDAs, because I need to be
able to also determine *wrong* answers.

<!-- (2) NFA->PDA->XML. This seems like the easiest one, but we could -->
<!-- compare w/the Textbook pg 107. Say, don't use the textbook transition via CFG.  -->


## 3. Run a PDA

This problem asks you to demonstrate that you to implement `run` for a
PDA. There are two classes of problems we can ask you about: the PDAs
for which evaluation is guaranteed to terminate, and those for which
it is *not* guaranteed to terminate. You'll have to write your `run`
program so that it will terminate when it can, and we will have to be
careful to only ask you to output `reject` when you have a PDA that is
guaranteed to terminate for all paths through the machine. 

Your task is to accept, or when possibly reject, a string in 
$\Sigma^{*}$.

Again, we ask you to reject only when we provide you a PDA that is
guaranteed to terminate for all paths through the machine. 

### NB. Characterizing such PDAs isn't as simple as "no epsilon-push loops."

**Your Tasks**

* Given a string in $\Sigma^{*}$, decide if the string is in the
  language of the machine. 

Your solution will be tested as follows:

* **Input** (from `stdin`): A `.jff` file describing a PDA, and a
  string over the alphabet of the PDA, separated by a space.

* Expected **Output** (to `stdout`): 

    * `accept`, if this string is in the language of the grammar,

    * `reject`, if the PDA terminates in all paths through the machine
      and this string is not in the language of the grammar.
	  
	* otherwise, it's behavior is undefined.  

* `Makefile` **target name**: `run-hw7-run`

* **Example**:

  `printf "types.jff {fst:t1,snd:t2}" | make -sf Makefile run-hw7-run`

  Output: `accept`

  `printf "types.jff {f:stt1s,nd:a}n" | make -sf Makefile run-hw7-verify`

  Output: `reject`



<!-- ## 4. Produce a simultaneous derivation -->

<!-- You will implement a program that, given a JFLAP XML description of a -->
<!-- CFG, an intermediate source string in the language of that grammar, -->
<!-- and an intermediate target string in the language of that grammar, -->
<!-- will return a simultaneous derivation of the target from the source. -->
<!-- We guarantee that the strings we provide will be intermediate strings -->
<!-- of the grammar. See the both the discussion of Lemma 2.21 and the -->
<!-- discussion after Definition 2.2 ("yields", "derives") distinguishing -->
<!-- the language of the grammar from the language of intermediate strings -->

<!-- You will produce a derivation of the intermediate string in the -->
<!-- grammar. You will write out the sequence of strings in the derivation, -->
<!-- one per line, starting with the initial source string, and ending with -->
<!-- the target string in question. Our checks will ensure that this -->
<!-- sequence of strings in your derivation follows from the grammar. -->


<!-- **Your Tasks**  -->
 
<!--  * Given the name of a JFF file containing the description of a CFG, -->
<!--    an intermediate source string in the language of the grammar, and -->
<!--    an intermediate target string in the language of this grammar, -->
<!--    construct a valid simultaneous derivation in the language of the -->
<!--    grammar from the source to the target. -->

<!-- Your solution will be tested as follows: -->

<!-- * **Input** (from `stdin`): A filename, followed by a source string, -->
<!--   followed by a target string. These will be newline-separated, to -->
<!--   account for derivations beginning with and ending with the empty -->
<!--   string. Likewise you will use a blank link in your output to -->
<!--   indicate the empty string. -->

<!-- * Expected **Output** (to `stdout`):  -->

<!--    * a sequence of intermediate strings, one per line, representing a -->
<!--      valid simultaneous derivation in the grammar -->

<!-- * `Makefile` **target name**: `run-hw7-derive` -->

<!-- * **Example**: -->


<!--   `printf "types.jff\n{fst:V,L:T}\n{fst:t1,snd:t2}\n" | make -sf Makefile run-hw7-derive` -->

<!--   Output:  -->
  
<!--   ``` -->
<!--   {fst:V,L:T} -->
<!--   {fst:t1,snd:V} -->
<!--   {fst:t1,snd:t2} -->
<!--   ``` -->

<!--   `printf "types.jff\nT\n{fst:t1,snd:t2}\n" | make -sf Makefile run-hw7-derive` -->

<!--   ``` -->
<!--   T -->
<!--   {S} -->
<!--   {L:T,S} -->
<!--   {fst:V,L:T} -->
<!--   {fst:t1,snd:V} -->
<!--   {fst:t1,snd:t2} -->
<!--   ``` -->


<!-- ``````` -->



<!-- This problem asks you to demonstrate you understand the JFLAP CFG -->
<!-- format, to internalize a new technical term related to derivations, -->
<!-- and know what it means to *generate* strings a language. -->

<!-- You will below a JFLAP file containing a CFG representing the language -->
<!-- of types in a simple ML-like language. I include below a [diagram from -->
<!-- "Programming in Standard ML"]({{ site.baseurl }}/assets/images/types.jpeg) describing this same information. The -->
<!-- terminals of this grammar are the tokens, i.e., the "words", of the -->
<!-- language, which includes identifiers (like labels, ids, or type -->
<!-- variables), parens and curly braces, `→`, `*`, and punctuation (colon -->
<!-- and comma). This means all names would be leaves in a parse tree: we -->
<!-- don’t separate them into individual characters. Whitespace is not -->
<!-- included in the terminals and should be ignored. Notice that -->
<!-- real-world languages are more complex than the languages we have -->
<!-- thus-far worked with; this is just to describe a *type* in ML. -->

<!-- In fact, the JFLAP format requires the variables be (a subset of the) -->
<!-- single capital letters and treats any other characters as terminals. -->
<!-- You should adhere to this format. I've given you a version of this -->
<!-- situation with a fixed quantity of labels, type variables, and IDs to -->
<!-- both simplify your lives and to accommodate JFLAP. More specifically, -->
<!-- you will receive the name of a JFF file containing the description of -->
<!-- a CFG, and a number $n$ representing the maximum quantity of -->
<!-- simultaneous substitutions. -->

<!-- The productions of a grammar are also called (Cf. 2.1) "substitution -->
<!-- rules" or simply "rules." Define _simultaneous_ _substitution_ _into_ -->
<!-- $w$ _of_ $R$ as, if $w$ is a word $abXdcYdZX$, with $a$, $b$, $c$, -->
<!-- $d$, in $\Sigma$ and $X$, $Y$, $Z$ in $V$, as the set of all strings -->
<!-- produced by applying at most one rule from $R$ for each instance of -->
<!-- each variable in $w$. Note that not applying a rule to a variable is -->
<!-- also a valid operation. There are almost always more than one ways to -->
<!-- perform a simultaneous substitution into a string. To help you we use -->
<!-- the following one-character abbreviations: `T`ype, Type`V`ariable, -->
<!-- `I`d, `L`abel, T`U`ple (a parethesized grouping of types), and -->
<!-- `S`truct (a non-empty sequence of label-type pairs). -->

<!-- **Your Tasks**  -->

<!-- * Open and read in a file ([types.jff]({{ site.baseurl -->
<!--   }}/assets/docs/types.jff) for this example) containing a grammar -->

<!-- * Construct an instance of this grammar in the internal representation -->
<!--   you devised -->

<!-- * Generate the set of all strings in the language of the grammar -->
<!--   produced within a fixed number of simultaneous substitutions. -->

<!-- * Write out the set of strings one string per line -->

<!-- Your solution will be tested as follows: -->

<!-- * **Input** (from `stdin`): The name of a `.jff` file containing a -->
<!--   CFG, and a number $n$ -->

<!-- * Expected **Output** (to `stdout`): the set of all strings derivable -->
<!--   through up to $n$ simultaneous derivations, one string per line. -->

<!-- * `Makefile` **target name**: `run-hw7-generate-n` -->

<!-- * **Example**: -->

<!--   `printf "types.jff 2" | make -sf Makefile run-hw7-generate-n` -->

<!--   Output: -->

<!--   ``` -->
<!--   d -->
<!--   c -->
<!--   b -->
<!--   a -->
<!--   t4 -->
<!--   t3 -->
<!--   t2 -->
<!--   t1 -->
<!--   ```  -->
  
<!--   Please notice the set of strings gets dramatically larger as the -->
<!--   values of $n$ increases. -->
