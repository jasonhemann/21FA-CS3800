---
title: "Homework 0"
layout: single
---
	
### Objectives 
  
  - Introduce some possibly-new tools for build and interaction.
  - Select the technology (language, etc.) you will use for this course. 
  - Begin exploratory programming to prepare for later assignments.

This homework ensures that everyone is familiar with the infrastructure
of the course.

**Language and Tools**

This course requires programming and expects students to already know
how to program. Thus we won’t dictate what language to use, or how to
structure your code.

​_You must decide all that for yourself_​ (starting with this
assignment).

For those who are unsure, a "high-level" language like Python or Racket
is probably best suited for completing the small tasks you will be asked
to do. Using a verbose language like Java or C++ will likely make things
harder.

Also, good, general programming habits is always a good idea since you
may need to:

* reuse code,

* and may occasionally present your solutions.

**Common Infrastructure**

The only requirement is that each homework submission must hook into
 our infrastructure (Docker containers running Ubuntu Linux 18.04).

Thus, while you may develop in any environment, you should ensure that
it works in our environment, and ideally you'll use `login-students`
or the Khoury virtual machines.

Input and output will be handled with `stdin`, `stdout`, as well as
files, and we’ll use [[Makefiles]] to run the assignments.

**Homework Problems**

The problems below will introduce each of these in more detail:

* `Makefile`s

* Hello, World!, with `stdin` and `stdout` (2 points)

* Sets and Alphabets (3 points)

* Subsets and Power Sets (2 points)

* Parsing XML Files (2 points)

* README (1 point)

**Total**: 10 points

**Submitting**

Submit your solution to this assignment in Gradescope.

A submission must include the following files (**NOTE**: everything is
case-sensitive):

* a `Makefile` with the following targets (see the `Makefile`s problem
  for details):

  * `setup`

  * `run-hw0-stdio`

  * `run-hw0-alphabet`

  * `run-hw0-powerset`

  * `run-hw0-xml`

* a `README` with the following information:

  * **Time spent** (in hours) on the assignment.

    This will help me gauge whether assignments are too easy or hard.

  * Any other **books or websites you used**.

    You may of course consult other reference sources to learn the
    course materials.

    Again, however, any work you submit must be your own.

* and finally, files containing the solution to each problem.

## 1. `Makefile`s

Since students will be using different programming languages, we need a
common way to run submitted assignments. We will do this with
[[Makefiles]].

In general, a `Makefile` (case-sensitive) is a script consisting of a
series of commands, each on its own tab-indented (not spaces) line.

Commands in a `Makefile` must be labeled with a _target_, which appears
on its own line before the commands and is followed by a colon (no space
in between).

Specifically, `Makefile`s in this course accomplish two things:

* they install the compilers and libraries needed to run an assignment,
  and

* they enable running all assignments in a uniform way.

### 1.1. Installing Infrastructure

The Gradescope grading environment starts with nothing installed, so
each homework submission must include a way to install the programs
needed to run itself.

That being said, **the grader will pre-install the following
packages**:

* `build-essential`

* `python3`

* `default-jdk`

* `nodejs`

* `racket`

This means that if you choose to use a language included in these
packages, e.g., C, C++, Python, Java, JavaScript, or Racket, then you
can (probably) skip to the next section.

The rest of this section explains how to use the `Makefile` to manually
install the language of your choice. Specifically, commands must be
labeled with a `setup` target. We will use Racket (my language of
choice) as an example.

**Example**:

Here is an example `Makefile` (case-sensitive) with a `setup` target
that installs the [Racket](https://racket-lang.org/) language from the
`apt` package manager:

`Makefile` (uses `apt`)

```
setup:  # this is the target name
        # each command must be on a new tab-indented line
        apt-get install -y racket
```

\(You’ll have root access so no need to run commands with `sudo`.)

Alternatively this example downloads and installs Racket to a local
subdirectory:


`Makefile` (installs locally)

```
setup:  # this is the target name
        # each command must be on a new tab-indented line
        wget -q https://mirror.racket-lang.org/installers/7.8/racket-7.8-x86_64-linux.sh
        chmod +x racket-7.8-x86_64-linux.sh
        ./racket-7.8-x86_64-linux.sh --in-place --dest racket
```

Any installation method is fine, so long as the rest of your `Makefile`
works correctly.

**Your Task** (if not using pre-installed packages)

Create a `Makefile` with a `setup` target that installs your chosen
language, tools, etc.

Test your `setup` script with the `make` command, e.g.:

`make -f Makefile setup`

### 1.2. Running Individual Problems

Each problem below specifies an additional target, which you must add to
the `Makefile`, and which we will use to run and grade your hw
submission.

## 2. Hello, World!, with `stdin` and `stdout`

We will primarily use `stdin` and `stdout` to communicate with your
programs.

Consult your language docs if you are unsure how to read/write from
these streams.

**Your Task**

* In your chosen language, write a program that reads from `stdin`, and
  then writes that entire input to `stdout` ​_three times_​, each on its
  own line.

* Add a `run-hw0-stdio` target to your `Makefile` that runs this
  program. Here’s an example `Makefile`

```
setup:  # is a comment
        # ... setup steps from before run-hw0-stdio:
          racket hw0-stdio.rkt # this line must start with a tab character
```

We will run your submission with a command like:

`printf "Hello, World!" | make -sf Makefile run-hw0-stdio`

The grader would then check for the following output:

```
Hello, World!
Hello, World!
Hello, World!
```

## 3. Sets and Alphabets

A _set_ is a mathematical object that represents a group of other
mathematical objects such as numbers, strings, and even other sets. You
will use them a lot in this course.

Set elements are unique, i.e., a set cannot contain two of the same
element.

On paper, sets are often written with brace notation, e.g., `{0,1}`, and
can be infinite in size. This problem will require you to manipulate
sets programatically.

An _alphabet_, often denoted with the \Sigma symbol (Greek letter
Sigma), is a set of characters from which strings in a _language_ may be
created.

**Your Task**

Write the following program:

* **Input** (from `stdin`): a string whose characters represent an
  alphabet \Sigma

* **Output** (to `stdout`): all possible strings of length 3
  that may be created from \Sigma.

  In other words, you are computing the _cartesian product_
  $\Sigma\times\Sigma\times\Sigma$.

  Print strings one per line in any order (but there should be no
  duplicates).

* Add a target named `run-hw0-alphabet` to your `Makefile` that runs
  your solution.

* **Example**:

  `printf "01" | make -sf Makefile run-hw0-alphabet`

  Example output:

```
  000
  001
  010
  011
  100
  101
  110
  111
```

## 4. Subsets and Power Sets

A _subset_ A of a set S, written A\subset S or A\subseteq S (the latter
means that A may be equal to S), is a set whose elements must be in S.

The _power set_ of a set S, sometimes written \mathcal{P}(S), is the set
of all subsets of S.

Write the following program:

* **Input** (from `stdin`): a set of strings (of alphanumeric
  characters), where set elements are separated with a space

* **Output** (to `stdout`): the power set of the input set, with each
  subset on its own line (subsets can appear in any order); separate
  elements in a subset with a space

* `Makefile` **target name**: `run-hw0-powerset`

* **Example**:

  `printf "a b c" | make -sf Makefile run-hw0-powerset`

  Output:

```

  a
  b
  a b
  c
  a c
  b c
  a b c
```

  \(Note: there’s an initial blank line, representing the empty set.)

## 5. Parsing XML Files

We’ll occasionally use XML, a common data format, to communicate with
your programs.

Here is an example:

`"XML Example"`

```
<automaton>
  <!--The list of states.-->
  <state id="0" name="q1"><initial/></state>
  <state id="1" name="q2"><final/></state>
  <state id="2" name="q3"></state>

  <!--The list of transitions.-->
  <transition>
    <from>0</from>
    <to>0</to>
    <read>0</read>
  </transition>

  <transition>
    <from>1</from>
    <to>1</to>
    <read>1</read>
  </transition>

  <transition>
    <from>0</from>
    <to>1</to>
    <read>1</read>
  </transition>

  <transition>
    <from>2</from>
    <to>1</to>
    <read>0</read>
  </transition>

  <transition>
    <from>1</from>
    <to>2</to>
    <read>0</read>
  </transition>

  <transition>
    <from>2</from>
    <to>1</to>
    <read>1</read>
  </transition>
</automaton>
```

In general, an XML document consists of nested pairs of opening and
closing _tags_ that can have arbitrary names, e.g., the `<automaton> ...
</automaton>` above.

An opening tag can have several _attributes_, each with an associated
_value_, e.g., the `state` tag above has attributes `id` and `name`.

Anything between the tags is called its _content_, which can be
arbitrary strings or more tags. A pair of open/close tags, its
attributes, and its content is called an _element_.

If an element has no content or attributes, it is ​_empty_​ and may be
written as a single _self-closing_ tag, e.g., `<initial />` or `<final
/>` from above.

This problem deals with automaton elements (like above) with a special
structure.

**The `automaton` Element**

An `automaton` element consists of `transition` and `state` elements.

* A `state` element:

  * must have `id` and `name` attributes,

  * and its content may include ​_empty_​ `initial` or `final` elements

* A `transition` element must include `from`,   `to`, and `read`
  elements:

  * the content of a `from` or `to` element is a state `id` (not the
    `name`),

  * and the `read` element is an alphanumeric character.

**Your Task**

Find a library (or write your own) and use it to write a program that
parses an XML file containing an `automaton` element and extract its
`states`.

The given file may contain other elements as well so just parse the XML
generally.

Though you are responsible for finding and learning a library, you might
find something like `xml.etree.ElementTree` in Python, or
`javax.xml.parsers` in Java, useful.

Specifically, write the following program:

* **Input** (from `stdin`): the name of a XML ​_file_​ that contains an
  `automaton` element

* **Output** (to `stdout`): on separate lines:

  * the `name` attributes (not the `id`) of the `state` elements, with a
    space in between each,

  * the start state, and

  * the accept states, with a space in between each.

* `Makefile` **target name**: `run-hw0-xml`

* **Example**:

  You can test your program with [this file named
  `fig1.4.jff`](fig1.4.jff) containing the XML above (right-click and
  choose "Save as").

  `printf "fig1.4.jff" | make -sf Makefile run-hw0-xml`

  Output:

```
  q1 q2 q3
  q1
  q2
```

## 6. README

**Your Task**

Create a `README` file (case-sensitive) with the following information:

* **Time spent** (in hours) on the assignment.

  This will help me gauge whether assignments are too easy or hard.

* The names of **other students you worked with**.

  You may discuss homework with other students but any submitted work
  ​_must be your own work_​. In other words, you must come up with your
  solutions independently.

  See the syllabus for more information.

* Any other **books or websites you used**.

  You may of course consult other reference sources to learn the course
  materials.

  Again, however, any work you submit must be your own.
