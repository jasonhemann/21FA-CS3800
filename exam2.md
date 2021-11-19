---
title: "Exam 2"
layout: single
---

### Objectives 

  - Retrench material from second third of the course
  - Situate CFLs in the context of the regular languages
  - Extend our understanding of properties of CFLs through implementation

**Exam Problems**

* [JFLAP PDA Grammar](#1-jflap-pda-grammar) (3pts, manually graded)

* [Ambiguous Grammars](#2-ambiguous-grammars) (3pts, manually graded)

* [Concatenation of CFLs](#3-concatenation-of-cfls) (2pts, manually graded)

* [Kleene star of CFLs](#4-kleene-star-of-cfls) (2pts, manually graded)
  
* [Chomsky Normal Form](#5-chomsky-normal-form) (6pts, 2 manually graded)

* [A Novel Reduction](#6-a-novel-reduction) (4pts, 2 manually graded)

**Submitting**

Submit the solution to this exam in Gradescope.

The submission must include the following files (**NOTE**: everything is
case-sensitive):

* `exam2-pda-grammar.jff`

* `exam2-ambiguous.txt`

* `exam2-kleene.txt`

* `exam2-concat.txt`

* `exam2-chomsky.txt`

* `exam2-nsdfa2dfa.txt`

* a `Makefile` with the following targets:

  * `setup` (optional)
  
  * `run-exam2-chomsky`
  
  * `run-exam2-nsdfa2dfa`

* the source code files needed by your `Makefile`,

* a `README` containing
 
  * The time it took you
  
  * The resources you used

## 1. JFLAP PDA Grammar

Here's a warm-up problem. We know that for some finite number of tags,
we can regard XML as a context-free language. This means we can
construct a CFL for our automaton XML elements files. Here's the
convention we'll use.

```
a - automaton open 
u - automaton close 
s - single state tag
t - transition open
r - transition close
f - from open
o - from close 
x - to open
q - to close
p - push open
h - push close 
y - pop open 
z - pop close
e - read open
d - read end 
l - leaf aka some actual data 
```

Note that we're ignoring questions of duplicate state names, whether
or not there's a *single* initial state, etc. Furthermore *for this
question assume that transition elements always come* "from", then
"to", then "read", then "pop", then "push".

Your job is to construct a grammar describing JFLAP-like strings in
this language. For instance, one valid string would be
"asstfloxlqplhplzeldru". And as long as we aren't concerned with the
actual leaf data---if anything of the sort will do, then we could use
regular expression substitution to *produce* an automaton element as a
result.

```
<automaton>
<state id="0" name="q0"/>
<transition>
<to>l</to>
<from>l</from>
<read>l</read>
<pop>l</pop>
<push>l</push>
</transition>
</automaton>
```

**Your Task**

Produce a valid JFLAP XML file that contains a grammar for strings
over the alphabet $\\{a, u, s, t, r, f, o, x, q, p, h, y, z, e, d,
l\\}$. Name that file `exam2-pda-grammar.jff`. 

## 2. Ambiguous Grammars

By Definition 2.7, we know that a string $w$ is derived _ambiguously_
in a context-free grammar G if it has two or more different leftmost
derivations. We provide you here a grammar G 


```
A -> cdD
A -> cEf
D -> bE
D -> ε
E -> EaE
E -> EbE
E -> EEb
E -> d 
E -> g
```

and a file [leftmost.txt]({{ site.baseurl }}/assets/docs/leftmost.txt)
containing a leftmost derivation in that grammar. We use the same file
format as our simultaneous derivations, that is one string of the
derivation per line, starting at the start symbol and the final line
containing the string.

**Your Task**

In a file named `exam2-ambiguous.txt`, you will construct a _distinct_
leftmost derivation of that same string, thereby demonstrating that
this grammar is ambiguous. Your file will conform to the same file
format as our simultaneous derivations, that is one string of the
derivation per line, starting at the start symbol and the final line
containing the string. Of course, You can use your `generate-n`, your
`cfg2pda` and `run` for your PDA, or JFLAP to help you produce such a
derivation. But you don't need to; those are options.

## 3. Concatenation of CFLs. 

We have demonstrated that the _regular_ languages are closed under
union, concatenation, and the Kleene star. We have not yet however
proven these properties for the CFLs. Here you will accomplish one of
these. We already know that the CFLs are exactly the languages
generated by CFGs. To demonstrate the closure of CFGs under
concatenation, you will show how to produce a CFG generating the
language $L\_1 \circ L\_2$ from:

* a [CFG $G\_1$ generating language $L\_1$, with start symbol $S\_1$]({{ site.baseurl }}/assets/docs/grammar1.txt) and

* a [CFG $G\_2$ generating language $L\_2$, with start symbol $S\_2$]({{ site.baseurl }}/assets/docs/grammar2.txt)

I'm not being super clear right now about _how_ to generate the
concatenation of two CFLs, but I suggest thinking in terms of
productions--how what it would look like to generate a string in the
concatenation? You will put your grammar in the file
`exam2-kleene.txt`. You should come up with a simple solution, we will
deduct points for overly complicated solutions.

## 4. Kleene star for CFLs. 

Here you will accomplish another one of those tasks. To demonstrate
the closure of CFGs under Kleene star, you will show how to produce a
CFG generating the language $L^{*}$ when given 

* a [CFG $G$ generating language $L$]({{ site.baseurl }}/assets/docs/grammar3.txt)

Once again I'm not being super clear right now about how to generate
the Kleene star of a CFL, but think in terms of productions---what it
would look like to generate a string in the star-closure of the
language? You will put your grammar in the file `exam2-kleene.txt`.
You should come up with a simple solution, we will deduct points for
overly complicated solutions.

## 5. Chomsky Normal Form

One algorithm that we discussed for deciding membership in a
context-free language involved transforming a CFG $G$ into Chomsky
Normal Form (CNF). While the algorithm for translating a grammar into
CNF is, not very long as far as those things goes, it does contain
some subtleties. We aren't going to force you here to implement the
entire algorithm. We want you just to perform the "eliminate ε-rules"
portion of the transformation.

**Your Tasks**

You will implement the "eliminate ε-rules" portion of the CNF
algorithm Sipser describes in the proof of Theorem 2.9. Given

* an XML description of a CFG _where we have already built a new start
  state for you_ and _where the right-hand side_ of the first
  production in the grammar is the *old* start symbol

you will produce
  
* a program that will return an XML description of a CFG for an
  equivalent language but with the ε-transitions removed. To do this
  you'll likely want to decompose this into a couple of smaller
  functions implementing sub-computations, and 

* a file `exam2-chomsky.txt` describing your overall algorithm for
  solving this problem. You should walk us through your data types,
  your overall approach, the specific subroutines you implement to
  help solve this problem and the purposes of each, and any
  preconditions or invariants upon which you rely. I mean these
  specifically for the grammar transformation part; you do not need to
  e.g. recapitulate our XML format.

**HINTS**:

* **Consider carefully some special cases** What happens if your
  grammar has a production `G -> G` in it, and also `G -> ε`? What if
  it also contains `G -> GG`? More generally, the book talks about how
  to handle cases like `Y -> wXaXZv`, but you might need to treat
  special case instances like `Y -> wXXZv` because the
  right-next-to-each-other ones look like duplicates. Notice also that
  this algorithm cascades: Sipser tells us that if we remove `G -> ε`
  and we have `A -> G`, we'll need to *add* the rule `A -> ε`. That's
  a new ε rule we'll need to remove. Unless of course that you have
  already _removed_ the rule `A -> ε`. 
  
Your solution will be automatically tested as follows:

* **Input** (from `stdin`): the name of **an XML file** containing a
  CFG.

* Expected **Output** (to `stdout`): an automaton XML string
  containing a CFG that recognizes the same language, but that does
  not contain any ε-transitions, except potentially an ε transition
  from the start symbol.

* `Makefile` **target name**: `run-exam2-chomsky`

  You can test your program with these files:

  * [`grammar1.jff`]({{ site.baseurl }}/assets/docs/grammar1.jff)
  * [`grammar2.jff`]({{ site.baseurl }}/assets/docs/grammar2.jff)
  * [`grammar3.jff`]({{ site.baseurl }}/assets/docs/grammar3.jff)
  * [`grammar4.jff`]({{ site.baseurl }}/assets/docs/grammar4.jff)
  * [`grammar5.jff`]({{ site.baseurl }}/assets/docs/grammar5.jff)

* **Examples**:

  `printf "grammar1.jff" | make -sf Makefile run-exam2-chomsky`

  Output:

```
<structure>
<type>grammar</type>
<production><left>A</left><right>B</right></production>
<production><left>B</left><right>bccC</right></production>
<production><left>C</left><right>a</right></production>
</structure>
```

Please note also that my implementation renames and canonicalizes the
non-terminals; do not be alarmed if you have an equivalent grammar
using different non-terminal names.

## 6. A Novel Reduction

In this problem you will demonstrate that you understand the technique
of reduction by applying it in a new situation. DFAs are traditionally
limited to only one start state. In this problem we ease that
restriction for a type of machine we call nondeterministic-start DFAs
(nsDFAs). An nsDFA can have one **or more** start states, and an nsDFA
$M$ accepts a string $ w = w\_0 ... w\_n $ if there is a sequence of
states $q\_0 ... q\_n$ consistent with M's $\delta$ function and
$q\_0$ is any one of the machine's start states.

Your task here is to demonstrate that $A_{\textrm{nsDFAs}}
\leq_{\textrm{M}} A_{\textrm{DFA}}$ by implementing part of a
computable reduction from $\langle nsDFA , w \rangle$ to $\langle DFA,
w \rangle$.

**Your Task**

Specifically, define a data representation for nsDFAs, and implement a
language-preserving function `nsDFA->DFA` that, given

* an nsDFA recognizing language $A$

returns a DFA recognizing $A$. **You must implement this
programmatically**. That is, you should not write one-off solutions to
pass our test cases, but instead write a programmatic transformation.
We will verify this by manual code inspection.

**HINTS**:

* **Be careful and uniformly map symbols from the first alphabet to
  the second**. $\Sigma\_1 \cap \Sigma\_2$ may be non-empty.

* **Make sure and remember to write your data description for nsDFAs
  in your `README` file.**

Your solution will be tested as follows:

* **Input** (from `stdin`): the name of **a XML file describing an
  nsDFA for a language A**. An XML file describing an nsDFA is like
  one describing a DFA, except that in an nsDFA more than one state
  may have an `<initial/>` tag.

* Expected **Output** (to `stdout`): an automaton XML string
  representing a DFA that recognizes strings of the language $A$.

* `Makefile` **target name**: `run-exam2-nsdfa2dfa`

* **Example**:

  You can test your program with these files:

  * [`nsdfa-goodbad.xml`]({{ site.baseurl }}/assets/docs/nsdfa-goodbad.xml): recognizes the language $\\{\textrm{"good"}, \textrm{"bad"}\\}$

  `printf "nsdfa-goodbad.xml" | make -sf Makefile run-exam2-nsdfa2dfa`

  Output:

```
```

Together with knowing that we have a decider for $A_{\textrm{DFA}}}$
we can use this function to demonstrate that this new class of
automaton is also decidable. 

