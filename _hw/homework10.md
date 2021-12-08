---
title: "Homework 10"
layout: single
---

### Objectives

-   More self-referencing exercises for TMs
-   Understand the complexity class P
-   Understand the class NP

**Homework Problems**

-   [Reference loop](https://jasonhemann.github.io/21FA-CS3800/hw/homework10/#1-reference-looppermalink)  (3 pts)

-   [Matrix Multiplication](https://jasonhemann.github.io/21FA-CS3800/hw/homework10/#2-matrix-multiplicationpermalink)  (2 pts, 1 graded manually)

-   [Modular Exponentiation](https://jasonhemann.github.io/21FA-CS3800/hw/homework10/#3-modexppermalink)  (3 pts, 2 graded manually)

- [3-colorability is in NP](https://jasonhemann.github.io/21FA-CS3800/hw/homework10/#4-3-colorability-is-in-nppermalink)  (2 pt, 1 graded manually)


**Total**: 10 points

**Submitting**

Submit this assignment on  [Gradescope](https://www.gradescope.com/).

The submission should contain only a zip archive of your code and the associated README. Don’t forget to submit a  `README`  file containing the required information, including time spent and resources consulted.

The submission must include the following files (**NOTE**: everything is case-sensitive):

-   `reference-loop-1.trm`

-   `reference-loop-2.trm`

-   a  `Makefile`  with the following targets:
    
    -   `setup`  (optional)
    
    -   `run-hw10-matrix`
        
    -   `run-hw10-modexp`
    
    -   `run-hw10-3-color`

-   a  `README`  containing the required information, including
    - Running time analysis for problem 2, 3, 4
    - Your time spent
    - Your resources referred

-   the source code files needed by your  `Makefile`.
   

## 1. Reference loop

This problem is taken from Sipser Exercise 6.6.

In the last HW, you wrote a Turing Machine (1# program) that outputs the description of itself, plus a hash symbol. In this problem, you need to write two *different* TMs that output the description of each other. Notice that both TMs take no inputs, so the direct application of the idea in the proof of Sipser Theorem 6.2 won't work!

**Your Tasks**

-   Write two *different* 1# programs: `reference-loop-1.trm`, `reference-loop-2.trm`. Their code has to be different, so you can't use two copies of the program SELF.
-  `reference-loop-1.trm` is a 1# program: when executed on empty registers, output the content of `reference-loop-2.trm` in R1.
-  `reference-loop-2.trm` is a 1# program: when executed on empty registers, output the content of `reference-loop-1.trm` in R1.

Your solution will be tested as follows: the output of the first program will be compared against the code of second program, and the output of the second compared against the code of the first.

    ```
    cat reference-loop-1.trm | ./trm 2>&1 50000 | tail -n 1 > rl1out.trm
    cat reference-loop-2.trm | ./trm 2>&1 50000 | tail -n 1 > rl2out.trm
    cmp --silent -- reference-loop-1.trm rl2out.trm && cmp --silent -- reference-loop-2.trm rl1out.trm && echo "matched"
    ```
    
    Output:
    
    ```
    matched
    ```
    
## Note on problem 2,3,4

In the following problems, you will be asked to prove that some language is in $P$, by providing a decider that runs in polynomial time. As usual, you can write in a programming language of your choice.

These problems will greatly resemble problems in coding interviews: write a program that efficiently solves a problem, and argue for its efficiency by analyzing its running time.

Since the running time analysis is not auto-gradable, you will *need* to write a brief running time analysis in your `README` file. **This part is crucial!** The analysis will take at least half of the grade weight for the problems, so write them carefully.

Recall that a TM is polynomial time if it runs in polynomial time of the *length* of its input, so if the input is a number $N$, a poly-time TM must halt in steps polynomial of $\log N$.

You can assume atomic, basic operations take 1 step to execute. So if you compute $a\times b$, or $b=\ell[i]$, the operation takes 1 step. However, if you call built-in functions in your programming language like `list.insert()` make sure you "unwrap" the function and argue for its running time.

A brief running time analysis can look like this:
```
The input is two numbers m,n, so the length is log m + log n.

The program has 2 for-loops:
 - The first loop runs log m times,
 - The second loop runs (log n)^2 times.
 - Everything in the loops runs in constant time since they
   are basic arithmetic operations.
Overall this runs in time polynomial to the input length.
```

## 2. Matrix Multiplication

In this problem, you will show the matrix multiplication language is in $P$.

The language MATMUL is described as follows:

$$  \begin{align*} \textit{MATMUL}=\{\langle &n,m,k, X,Y,Z\rangle :\\
& n,m,k\text{ are integers, }\\
&X\in\mathbb{Z}^{n\times m},Y\in \mathbb{Z}^{m\times k},Z\in \mathbb{Z}^{n\times k} \text{ are matrices,}\\
& XY=Z\} \end{align*}$$
In plain English, this is: given the dimension $n,m,k$, a $n$-by-$m$ matrix $X$, a $m$-by-$k$ matrix $Y$, and a result $n$-by-$k$ matrix $Z$, test whether $XY=Z$.

Show that $\textit{MATMUL}\in P$ by writing a polynomial time decider of the language, in a programming language of your choice.

Note that you will need to justify (in `README`) that the running time of your program is polynomial of the length of the input. (see **Note** above)

**Your Tasks**
 - Write a polynomial time decider for $\textit{MATMUL}$ (1pt). Specifically:
     -   **Input**  (from  `stdin`): 3 integers $n,m,k$ for dimensions, followed by:
         - $n$ lines of $m$ integers for $X$
         - $m$ lines of $k$ integers for $Y$
         - $n$ lines of $k$ integers for $Z$
(all integers won't be too large, standard `int` will do)
    
    -   Expected  **Output**  (to  `stdout`): a single bit: $1$ if $XY=Z$, $0$ if not.
 - Write a brief running time analysis in `README`. (1pt)

**Example**
```
4 2 3
1 2
1 3
6 2
5 1
3 6 1
-2 3 1
-1 12 3
-3 15 4
14 42 8
13 33 6
```

Output:
```
1
```

## 3. MODEXP

This problem is taken from Sipser Exercise 7.12.

In this problem, you will show the modular exponentiation language is in $P$.

The language MODEXP is described as follows:

$$  \begin{align*} \textit{MODEXP}=\{\langle a,b,c,p\rangle : a&,b,c,p \text{ are integers}\\
&\text{ such that } a^b\equiv c \pmod p\} \end{align*}$$

Show that $\textit{MODEXP}\in P$ by writing a polynomial time decider of the language, in a programming language of your choice.

A straightforward method is to compute $a^b\pmod p$ and compare it against $c$. However, the most obvious algorithm (computing $a^b$ in a for-loop) won't work, since an efficient algorithm must run in polynomial time of the *length* of $b$ (which, in turn, must run in $O(\log b)$, so logarithmic of $b$). A simple for-loop computing $a^b$ runs in time $O(b\log a)$, which is exponential (inefficient) in $\log b$.

A hint is to consider when $b$ is a power of 2. Is there any shortcut to compute $a^b$ in this case?

**Your Tasks**
 - Write a polynomial time decider for $\textit{MODEXP}$ (1pt). Specifically:
     -   **Input**  (from  `stdin`): 4 integers (won't be too large, standard `int` will do), corresponding to $a,b,c,p$.
    
    -   Expected  **Output**  (to  `stdout`): a single bit: $1$ if $a^b\equiv c\pmod p$, $0$ if not.
 - Write a brief running time analysis in `README`. The running time must be polynomial of $\log a, \log b, \log c,\log p$ (the size of the input). (2pt)

**Example**
```
7 18 9 11

Output:
1
```

## 4. 3-Colorability is in NP

In this problem, you will show the 3-colorability language is in $NP$.

A graph is (vertex/node) **3-colorable**, if it is possible to assign a color (out of 3 colors) to every node such that no two adjacent nodes (connected by an edge) share the same color.

For example, the triangle graph is 3-colorable (you assign a different color to every node), but the [tetrahedral graph](https://commons.wikimedia.org/wiki/Category:Complete_graph_K4) is not, since every pair of vertices are adjacent, and for 3 color you have to assign 2 vertices with the same color.

Formally, the language is:

$$  \begin{align*} \textit{3COLOR}=\{\langle G\rangle : G \text{ is a 3-colorable graph}\} \end{align*}$$

Show that $\textit{3COLOR}\in NP$ by writing a polynomial time *verifier* of the language, in a programming language of your choice. Recall that a $NP$ verifier takes in a problem and a certificate to the problem, usually a proposed "solution", and outputs $1$ if the solution is valid. In our case, the problem will be a graph $G$ and the certificate will be a 3-coloring (a function that maps each vertex to a color).

In this problem, we only consider *undirected, simple* graphs. So edges have no direction, and every pair of nodes share at most 1 edge.

**Your Tasks**
 - Write a polynomial time verifier for $\textit{3COLOR}$ (1pt). Specifically:
     -   **Input**  (from  `stdin`): a graph $G$ and a coloring function $f\colon V\to \{1,2,3\}$. Specifically, we input
         - $n$ for number of vertices, $m$ for number of edges
         - $m$ lines of integer pairs $v,w$, each pair denotes an edge $(v,w)$.
         - A line of $n$ integers in the range of $\{1,2,3\}$, denoting a coloring of the graph. The $i$-th integer denotes the proposed coloring of the $i$-th vertex.
    
    -   Expected  **Output**  (to  `stdout`): a single bit: $1$ if $f$ is a valid coloring of $G$, $0$ if not.
 - Write a brief running time analysis in `README`. The running time must be polynomial of the size of the input. (1pt)

**Example**
```
4 3
1 2
1 3
1 4
1 2 3 1

Output:
0
```
