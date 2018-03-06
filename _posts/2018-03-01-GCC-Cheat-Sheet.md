---
layout: single
title: GCC Cheat Sheet
excerpt: Examination of the steps GCC takes to compile programs
categories: [programming]
---

For the sake of example. We are going to have two files ```program.c``` and ```library.c```. program.c uses functions defined in library.c. _TODO:ADD HEADER FILES_

## GCC 

```bash
$ gcc program.c library.c -o program
```
Generates .o executable file

## Compilation

```bash
$ gcc -S program.c
$ gcc -S library.c
```
Generates text .s assembly files

## Assembly

```bash
$ as program.s -o program.o
$ as library.s -o library.o
or
$ gcc -c program.c -o program.o
```
Generates .o machine language assembly object files

## Linking

```bash
$ ld program.o library.o -o program
or
$ gcc program.o library.o
```
Links object files together and creates executable file

## Resources
The following resources were used while writing this page
* http://codingfreak.blogspot.com/2008/02/compilation-process-in-gcc.html
* http://cs-fundamentals.com/c-programming/how-to-compile-c-program-using-gcc.php