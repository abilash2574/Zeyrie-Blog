---
title: "More Possibilities with Octave"
subtitle: ""
date: 2021-10-02T20:36:29+05:30
lastmod: 2021-10-02T20:36:29+05:30
draft: true
author: "Abilash S"
authorLink: "https://www.zeryie.in/"
description:
tags: ["octave", "machine_learning"]
categories: ["Machine Learning"]

resources:
- name: featured-image
  src: pics/octave-featured.png
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: true
lightgallery: false
license: ""

hiddenFromHomePage: false
hiddenFromSearch: false
---

This is the continuation of [Basics of Octave](https://www.blogs.zeyrie.in/octave_tutorial/). In this blog we will look what are the possibilities of operations in octave. 

<!-- more -->


## Some terminal Commands

We can use terminal commands inside octave shell, which can be used to open files, assign data sets, etc.. 

The commands used in the image below are:

- `pwd` - to show the path to current directory
- `dir` - files and folders in current directory
- `ls`  - list all the files in current directory

{{< image src="pics/terminal.png" caption="**Terminal Commands in Octave**">}}

## Finding Size of a matrix

{{< style "text-align: justify; em {color: #FF7777;}" >}}

To find the size of a matrix, we use the `size` functions, and this returns another matrix denoting _number of rows_ first and _number of columns_ second.

{{< /style >}}

```octave
A = [1 2; 3 4; 5 6];

size(A)
% ans = 

      3   2

```

{{< admonition info  "" >}}
It is to be noted that, `size` always returns another matrix. 
{{< /admonition >}}

To get the size of a specific dimension we use:

```octave
size(A, 1)
% ans = 3

size(A, 2)
% ans = 2
```

## Finding Length of a Vector

{{< style "text-align: justify; em {color: #FF7777;}" >}}

To find the length or size of an vector, we can use the `length` function. This function can be also used for matrices and it will return the largest size of an matrix dimension. Due to this, it is more useful for finding the length of a vector, which has only one column.

{{< /style >}}

```octave
v = [1; 2; 3; 4; 5; 6];

length(v)
% ans = 6

% if we use length on a martix such as A in the above code.

length(A)
% ans = 3

```

{{< admonition info  "" >}}

{{< style "text-align: justify; " >}}

`length` is not a meaningful function for matrices, as finding the largest size of a dimension will not actually make use understand whether it is the size of rows or columns. So its used to find the size of vectors.

{{< /style >}}

{{< /admonition >}}

## Load Varibles from files

We can load variables from files as well, to do so, at first we must move to the directory where the files are stored and then do as follows:

{{< image src="pics/load-variable.png" caption="**Loading variables from file**">}}

There are some other functions that are useful when dealing with variables and it is `who` and `whos` functions:

The `who` function will list all the variables we have created. `whos` functions will give a more detailed information about each variable.

{{< image src="pics/who&whos.png" caption="**`who` and `whos` functions**">}}

{{< admonition info  "" false >}}
{{< style "text-align: justify; " >}}

The `whos` function shows the `Attr`, `Name`, `Size` of matrix, `Bytes` as data, `class` denotes the data type of the variable

{{< /style >}}
{{< /admonition >}}

{{< admonition tip "" >}}

We can clear or delete a variable using the function `clear`. If we use `clear` without mentioning any variable after the function it will delete all variables.

```octave
clear ans

% this will clear the ans variable from the above example
```

{{< /admonition >}}

We can save a variable to a file using the `save` function as follows, which will create a new file:

{{< image src="pics/save.png" caption="**Using `save` function**">}}

{{< admonition info  "" false >}}

If we want to save this in a `txt` **ASCII** format, then use `save file_name.txt variable_name -ascii`. The normal save function creates files in a compressed way to save space.

{{< /admonition >}}

## Slicing and Selecting Varibles

We can select a specific value of a matrix using the following:

```octave
A = [1 2; 3 4; 5 6]
% A = 
    1   2
    3   4
    5   6
    
A(3, 2)
% ans = 6
```

As value of A is 

$$\begin{bmatrix}1 & 2 \\\3 & 4 \\\ 5 & 6 \end{bmatrix}$$

The above line take the value of $\bold{A_{32}}$ which is 6

We can slice the value of a matrix using

```octave
A(2, :)
```

**Results**:
$$\begin{bmatrix}3 & 4\end{bmatrix}$$

{{< admonition note  "" >}}
The `:` means every element along the row/column
{{< /admonition >}}

```octave
A(:, 2)
```

**Results**:
$$\begin{bmatrix}2 \\\ 4\\\ 6\end{bmatrix} $$

We can select the rows of a matrix and get all the elements of the matrix on the selected rows 

```octave
A( [1 3], : )
```

**Results**:
$$\begin{bmatrix}1 & 2\\\ 5 & 6\end{bmatrix}$$

## Appending and Assigning Matrix

We can assign a particular value for a element in matrix as follows:

```octave
A = [1 2; 3 4; 5 6];

A(:, 2) = [10; 11; 12];
```

So, $$ A = \begin{bmatrix} 1 & 2 \\\ 3 & 4 \\\ 5 & 6 \end{bmatrix} \\\ \textnormal{and the result will be } A = \begin{bmatrix} 1 & 10 \\\ 3 & 11 \\\ 5 & 12 \end{bmatrix}$$

And we can append more columns to a matrix as follows:

```octave
A = [A, [100; 101; 10]];
```

**Results** $$ A = \begin{bmatrix} 1 & 2 & 100 \\\ 3 & 4 & 101 \\\ 5 & 6 & 102 \end{bmatrix}$$

To append a row to an matrix we can do as:

```octave
A = [A; [11 22 33]];
```

**Results**: $$ A = \begin{bmatrix} 1 & 2 & 100 \\\ 3 & 4 & 101 \\\ 5 & 6 & 102 \\\ 11 & 22 & 33 \end{bmatrix}$$

## Joining two matrices

We can join the matrices as follows:

```octave
A = [1 2; 3 4; 5 6];
B = [10 11; 12 13; 14 15];

C = [A B]
```

**Results**: $$ C = \begin{bmatrix} 1 & 2 & 10 & 11 \\\ 3 & 4 & 12 & 13 \\\ 5 & 6 & 14 & 15 \end{bmatrix} $$

---

{{< admonition success  "Thank you for reading!" >}}
Thank you for reading till here, if you find this useful please share it with your friends. 
{{< /admonition >}}


