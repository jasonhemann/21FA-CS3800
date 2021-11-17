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

* [Write to R2](#3-write-to-r2) (2 pts)

* [Move writer](#4-a-program-to-write-move-programs) (2 pts)

* [self\#](#5-self\#) (4 pts)

**Total**: 10 points

**Submitting**

Submit this assignment on [Gradescope](https://www.gradescope.com).

The submission should contain only a zip archive of your code and the
associated README. Don’t forget to submit a `README` file containing
the required information, including time spent and resources
consulted.

The submission must include the following files (**NOTE**: everything is
case-sensitive):

* `basic-program-interactions.trm` 

* `clear-and-move.trm`

* `write-to-r2.trm`

* `move-writer.trm`

* `self-hash.trm`

* a `README` containing the required information,

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
$ printf "1##1##1#1#1##1##1##1#1#1##" | ./trm 2>&1
Add# 1
...
R1: ##11###11#

Done. Executed 10 instructions.
##11###11#
$
```

To run with automation, provide `trm` two arguments: first, the
maximum number of steps to execute, and then the frames per second of
an animation of the machine's operation. For this assignment, all of
your programs should successfully halt, according to the 1# definition
of halting.


## 1. Basic program interaction 

In lecture, we looked at programs to add data to trm registers, and a
program to move data from R2 to R1. Write a trm program that will fill
R1 with the data `1#1#`, fill R2 with the data `11#1##`, and R3 with
the datum `1#`. 

**Your Tasks**

* Write a file `basic-program-interactions.trm` containing a 1#
  program to halt with the aforementioned data written to the
  appropriate registers, with all other registers empty. 
  
Your solution will be tested as follows:

* **Example**:

  ```
  cat basic-program-interactions.trm | ./trm 2>&1 | tail -n 6 | head -n 3
  ```

  Output: 

  ```
  R1: 1#1#
  R2: 11#1##
  R3: 1# 
  ```

## 2. Clear and move

Write a program that clears R3 and then swaps the contents of R1 and
R2 (using the now-empty R3). You can test this program by, for
instance, first passing your solution to problem 1 to `trm` followed
immediately by your solution to this problem and ensure that you get
the correct output.

```
$ cat <(basic-program-interaction.trm) <(clear-and-move.trm) | ./trm 
```

**Your Tasks**

* Write a file `clear-and-move.trm` containing a 1# program to swap
  the contents of R1 and R2 emptying R3. Your program should terminate
  with the values of R1 and R2 swapped, and with all other registers
  empty.
  
Your solution will be tested as follows:

* **Example**:

  ```
  cat <(basic-program-interaction.trm) <(clear-and-move.trm) | ./trm 2>&1 | tail -n 5 | head -n 2
  ```

  Output: 

  ```
  Coming
  ```


## 3. Write to R2

Create a program write-to-2 with the following feature: If we start
write-to-2 with x in R1 and R2 empty, we eventually halt with a word
$y = \phi_{\textrm{write-to-2}}(x)$ in R2 and all other registers
empty; moreover, running y with all registers empty results in x back
in R2 (not R1) and all other registers empty.


**Your Tasks**

* Write a file `write-to-2.trm` containing a 1# program that, when
  begun with `x` in R1, writes a program y to R2 and halts with all
  other registers empty. That program `y` it generates should be a
  program that, when run with all registers empty, halts with the
  original string `x` in R2 and all other registers empty.

  
Your solution will be tested as follows:

* **Example**:

  ```
  cat <(write-to-2.trm) <(printf "R111#111") | ./trm 2>&1 | tail -n 5 | head -n 2
  ```

  Output: 

  ```
  Coming
  ```

* **Example**:

  ```
  cat <(write-to-2.trm) <(printf "???") | ./trm 2>&1 | tail -n 4 | head -n 1 | ./trm
  ```

  Output: 

  ```
  Coming
  ```


## 4. A program to write move programs

Look carefully at your solution to problem 1. The data `1#1#` and
`11#1##` are actually also code---these are 1# programs. Your solution
to problem 1 is an instance of using a 1# program to write another 1#
program. Here we will work with and use `write` and `move` to
construct other program-writing programs. Write a file
`move-writer.trm` which writes move programs. In more detail, if m and
n are different numbers in unary, we want $\phi\_{p}(m,n)$ to be a
program $\textrm{move}_{m,n}$ as we described it in Lesson 1. (If
either m or n is not a unary numeral, then we don't care what
$\phi\_{p}(m,n)$ is. Please note that you can seed registers with
values in the following manner:

```
$ printf "1# R111111 R111" | ./trm
Add1 1

IN: Add1 1
R1: 1111111
R2: 111

Done. Executed 1 instructions.
1111111
```


**Your Tasks**

* Write a file `move-writer.trm` containing a 1# program that, when
  executed in a machine with unary number $m$ in R1 and unary number
  $n$ in R2, halts with a program y in R1 and all other registers
  empty. This program y should be a program that computes $move{m,n}$,
  that is, it is a program that when run on a machine with data in Rm,
  halts with those same data in Rn, and all other registers empty.
  
Your solution will be tested as follows:

* **Example**:

  ```
  cat <(move-writer.trm) <(printf "R | ./trm | tail -n 1
  ```

  Output: 

  ```
  Coming
  ```

* **Example**:

  ```
  cat move-writer.trm | ./trm | tail -n 1 | sed 's/.$//' | ./trm `
  ``

  Output: 

  ```
  Coming
  ```


## 5. self\# 

Write a program p which, when started on all empty registers writes
itself to R1 but rather writes itself followed by a `#` symbol. In
other words, $\phi_{p}()  = p + \\#$

**Your Tasks**

* Write a file `self-hash.trm` containing a 1# program that, when
  executed in a machine with all registers empty, writes to R1 itself
  followed by a `#` symbol and all other registers empty.
  
Your solution will be tested as follows:

* **Example**:

  ```
  self-hash.trm | ./trm | tail -n 1
  ```

  Output: 

  ```
  Coming
  ```

* **Example**:

  ```
  cat self-hash.trm | ./trm | tail -n 1 | sed 's/.$//' | ./trm `
  ``

  Output: 

  ```
  Coming
  ```
