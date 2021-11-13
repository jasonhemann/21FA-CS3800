---
title: "Homework 9"
layout: single
---

### Objectives 

  - Explore text register machines and elementary programs
  - Construct programs to populate registers and manipulate register data
  - Connect meta-programming theory in Sipser to actual practice
  - Explore applications of s-m-n and recursion theorems. 

**Homework Problems**

* [Basic program interaction](#1-basic-program-interaction) (1 pt) 

* [Clear and move](#2-clear-and-move) (1 pt)

* [Design, concat, and run a PDA](#3-design-a-pda) (2 pts)

* [A program to write a program](#a-program-to-write-a-program) (2 pts)

* [self\#](#self\#) (4 pts)

**Total**: 10 points

**Submitting**

Submit this assignment on [Gradescope](https://www.gradescope.com).

The submission should contain only a zip archive of your code and the
associated README. Don’t forget to submit a `README` file containing
the required information, including time spent and resources
consulted.

## Notes on readings.

The assigned readings and reference material (see Enrichment page or
schedule for links) reference a different, web-based interpreter. The
Enrichment page links to the interpreter we will use. Simply download
the repository and `make` in that directory. Some parts of the reading
that reference how to interact with the interpreter will thus be
incorrect, and you can skip the "Using the interpreter" section. To
provide our interpreter a program, we pass the program in using
`printf` and pipe `|` it in to the `trm` program. By default the `trm`
program will execute it's input for up to 1000 steps. You can write
your programs in a file and then `cat` them into the interpreter too,
if you wish.


```
$ printf "1##1##1#1#1##1##1##1#1#1##" | ./trm 
Add# 1
...
R1: ##11###11#

Done. Executed 10 instructions.
##11###11#
$
```

To run with automation, provide `trm` two arguments: first, the
maximum number of steps to execute, and then the frames per second of
an animation of the machine's operation. 


## 1. Basic program interaction 

In lecture, we looked at programs to add data to trm registers, and a
program to move data from R2 to R1. Write a trm program that will fill
R1 with the data `1#1#`, fill R2 with the data `11#1##`, and R3 with
the datum `1#`.


## 2. Clear and move

Write a program that clears R3 and then swaps the contents of R1 and
R2 (using the now-empty R3). You can test this program by, for
instance, first passing your solution to problem 1 to `trm` followed
immediately by your solution to this problem and ensure that you get
the correct output.

```
$ cat <(basic-program-interaction.trm) <(clear-and-move.trm) > ./trm 
```

## 3. Write to R2

Create a program write-to-2 with the following feature: If we start
write-to-2 with x in R1 and R2 empty, we eventually halt with a word
$y = \phi_{\textrf{write-to-2}}(x)$ in R2 and all other registers
empty; moreover, running y with R2 empty results in x back in R2 (not
R1) and all other registers empty.

## 4. A program to write a program. 

Look carefully at your solution to problem 1. The data `1#1#` and
`11#1##` are actually also code---these are 1# programs. Your solution
to problem 1 is an instance of using a 1# program to write another 1#
program. 


## 5. self\# 

Write a program p which, when started on all empty registers writes
itself to R1 but rather writes itself followed by a `#` symbol. In
other words, $\phi_{p}()  = p + #$


