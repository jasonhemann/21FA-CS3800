---
title: "Homework 5"
layout: single
---


### Objectives 

  - Conclude discussion of pumping lemma for regular languages
  - Begin to explore material from chapter 2

**Homework Problems**

* [Pump a string](#1-pump-a-string) (2 pts)

* [String Derivations](#2-string-derivation) (2 pts)

* [Design a CFG](#3-design-a-cfg) (2 pts)

* [Design a PDA](#4-design-a-pda) (2 pts)

* [Closed Operations for CFLs](#5-closed-operations-for-cfls) (2)

* [Regular is Context-free?](#6-regular-is-context-free) (6 pts)

* README (2 pts)

**Total**: 32 points

**Submitting**

Submit this assignment at [Gradescope
`hw5`](https://www.gradescope.com/courses/219302/assignments/1043973).

The submission should include only pdf or plain text files.

Be sure to assign each page to the correct problem in Gradescope.

Also, don’t forget to submit a `README` file containing the required
information.

## 1. Pump a string.


## 2. String Derivations

Here’s a CFG representing a simple Java-like object-oriented language:

\left\langle CLASS\right\rangle     \rightarrow\texttt{class } \left\langle CLSID\right\rangle \texttt{ extends }      
                                               \left\langle CLSID\right\rangle \,\{\left\langle FLDDECLS\right\rangle  
                                               \left\langle CONS\right\rangle \left\langle METHS\right\rangle\}        
\left\langle FLDDECLS\right\rangle  \rightarrow\left\langle FLDDECL\right\rangle \left\langle FLDDECLS\right\rangle    
                                               \mid \varepsilon                                                        
\left\langle FLDDECL\right\rangle   \rightarrow\left\langle CLSID\right\rangle \left\langle                            
                                               FLDID\right\rangle\texttt{;}                                            
\left\langle CONS\right\rangle      \rightarrow\left\langle CLSID\right\rangle\(\left\langle                           
                                               ARGS\right\rangle)\{\texttt{super(}\left\langle                         
                                               EXPRS\right\rangle\texttt{)}; \left\langle FLDASSIGNS\right\rangle\}    
\left\langle FLDASSIGNS\right\rangle\rightarrow\left\langle FLDASSIGN\right\rangle \left\langle FLDASSIGNS\right\rangle
                                               \mid \varepsilon                                                        
\left\langle FLDASSIGN\right\rangle \rightarrow\texttt{this.}\!\left\langle FLDID\right\rangle \texttt{=} \left\langle 
                                               EXPR\right\rangle;                                                      
\left\langle METHS\right\rangle     \rightarrow\left\langle METH\right\rangle \left\langle METHS\right\rangle \mid     
                                               \varepsilon                                                             
\left\langle METH\right\rangle      \rightarrow\left\langle CLSID\right\rangle \left\langle                            
                                               METHID\right\rangle\(\left\langle ARGS\right\rangle)\{ \texttt{return } 
                                               \left\langle EXPR\right\rangle; \}                                      
\left\langle ARGS\right\rangle      \rightarrow\left\langle ARGS+\right\rangle \mid \left\langle ARG\right\rangle \mid 
                                               \varepsilon                                                             
\left\langle ARGS+\right\rangle     \rightarrow\left\langle ARG\right\rangle, \left\langle ARGS+\right\rangle \mid     
                                               \left\langle ARG\right\rangle                                           
\left\langle ARG\right\rangle       \rightarrow\left\langle CLSID\right\rangle \left\langle ARGID\right\rangle         
\left\langle CLSID\right\rangle     \rightarrow\textrm{ class names can be any string in \texttt{\[a-zA-Z\]+}}         
\left\langle METHID\right\rangle    \rightarrow\textrm{ method names can be any string in \texttt{\[a-zA-Z\]+}}        
\left\langle FLDID\right\rangle     \rightarrow\textrm{ field names can be any string \texttt{\[a-zA-Z\]+}}            
\left\langle ARGID\right\rangle     \rightarrow\textrm{ arg names can can be any string in \texttt{\[a-zA-Z\]+}}       
\left\langle EXPRS\right\rangle     \rightarrow\left\langle EXPRS+\right\rangle \mid \left\langle EXPR\right\rangle    
                                               \mid \varepsilon                                                        
\left\langle EXPRS+\right\rangle    \rightarrow\left\langle EXPR\right\rangle, \left\langle EXPRS+\right\rangle \mid   
                                               \left\langle EXPR\right\rangle                                          
\left\langle EXPR\right\rangle      \rightarrow\left\langle VAR\right\rangle \mid \left\langle                         
                                               EXPR\right\rangle\!.\!\left\langle FLDID\right\rangle \mid \left\langle 
                                               EXPR\right\rangle\!.\!\left\langle METHID\right\rangle\(\left\langle    
                                               EXPRS\right\rangle)\mid                                                 
                                               \texttt{new } \left\langle CLSID\right\rangle\(\left\langle             
                                               EXPRS\right\rangle) \mid (\left\langle CLSID\right\rangle)\left\langle  
                                               EXPR\right\rangle                                                       
\left\langle VAR\right\rangle       \rightarrow\textrm{ variable names can be any string in \texttt{\[a-zA-Z\]+}}      

\(Yes, real-world languages are much more complicated than textbook
examples.\)

The terminals of this grammar are the tokens, i.e., the "words", of the
language, which includes keywords (like `class`), identifiers (like
class or field names), parens, braces, and punctuation (like dot,
semicolon, or comma).

NOTE: this means all names (e.g., class names, variable names, etc.)
should be leaves in a parse tree. You don’t need to separate them into
individual characters.

Whitespace is not included in the terminals and should be ignored.

Give a parse tree or derivation for the following strings (i.e.,
programs):

* `class A extends Object { A() { super(); } }`

* `class Pair extends Object {`             
                                            
    `Object fst;`                           
    `Object snd;`                           
                                            
    `Pair(Object fst, Object snd) {`        
      `super(); this.fst=fst; this.snd=snd;`
    `}`                                     
                                            
    `Pair setfst(Object newfst) {`          
      `return new Pair(newfst, this.snd);`  
    `}`                                     
  `}`                                       

## 3. Design a CFG

Create a CFG that generates the following language L.

You can assume alphabet \Sigma = \{0,1\}.

L = \{w\mid w = \textrm{FLIP}(w)\}, where \textrm{FLIP} is from
\[missing\] in \[missing\].

## 4. Design a PDA

Create a pushdown automata that recognizes language L from [the previous
problem](#2-design-a-cfg).

You can either draw a diagram or give a formal description.

## 5. Closed Operations for CFLs

Show that the following operations are closed under context-free
languages:

* union

* concatentation

* Kleene star

## 6. Regular is Context-free?

You will prove, by construction, the statement: For any language A, if
A is regular, then A is also context-free. You will prove this by
consuming an XML file containing a description of a machine
recognizing language A, and you will produce (an XML description of) a
PDA recognizing that same machine.

