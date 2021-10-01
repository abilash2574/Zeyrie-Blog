---
title: "Octave Tutorial"
subtitle: ""
date: 2021-10-01T22:10:30+05:30
lastmod: 2021-10-01T22:10:30+05:30
draft: false
author: "Abilash S"
authorLink: "https://www.zeryie.in/"
description:
tags: ["octave", "machine_learning"]
categories: ["Machine Learning"]

resources:
- name: featured-image
  src: featured-image.webp
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: true
lightgallery: true
---

This is a tutorial in Octave. It can be used as reference for future, and its from basics

{{< admonition tip "" >}}
You can change the default prompt in octave by using `PS1('>> ');`
The string in single quotes will be replaced by the default prompt.
<br>
You can suppress the output that's print in the interactive session by ending the line of code with a `;`. This will suppress the output.
{{< /admonition >}}


{{< admonition info "" >}}
We can always use the `help` function in octave to get help  of any funtion.

```octave
help eye
```

This code will give you the man page for eye function
{{< /admonition >}}

## Basic Operations

#### 1. Arithmetic Operations

Some of the basic operations in Octave are:

```octave
5 + 8 
% >> ans = 13

6 * 2
% >> ans = 12

3 - 2
% >> ans = 1

6 / 2
% >> ans = 3

5 ^ 6
% >> ans = 15625
```

{{< admonition tip "" >}}
To write a comment in Octave we use `%` 
{{< /admonition >}}

#### 2. Logical Operations

Logical Operations that can be performed are:

```octave
1 == 2 % comparison operator. Gives False (0)
% >> ans = 0

1 ~= 2 % ~ is the not denoting sign. Gives True (1)
% >> ans = 1 

1 && 0    % is an AND operator, results 0
% >> ans = 0

1 || 0  % is an OR operator, results 1
% >> ans = 1

xor(1,0)    % is a XOR operator, results 1
% >> ans = 1
```

#### 3. Variables

To create a variable:

```octave
a = 3
% >> a = 3

a = 5;

b = 'hello world'
% >> b = hello world
```

We can assign results of operations to a variable by:

```octave
c = ( 3 >= 1 );
c
% >> c = 1

a = pi    % pi is a keyword that holds the value of pi
% >> a = 3.1416
```

We can explicitly display a variables value by:

```octave
disp(a)
% >> 3.1416

disp(sprintf('2 decimals: %0.2f', a))   % the sprintf is the same as printf in c, so is the string format
% >> 2 decimals: 3.14
```

And to display results with longer and shorter decimal places use: 

```octave
format long
a
% >> a = 3.141592653589793

format short
a 
% >> a = 3.14159 
```

#### 4. Creating Matrixes

We can create a matrix in octave as follows:

```octave
A = [1 2; 3 4; 5 6;]
% >> A = 
          1   2
          3   4
          5   6

```

Which can be also written as:

```octave
B = [1 2;
3 4;
5 6]
% >> B = 
        
        1   2
        3   4
        5   6
```

A `1 x 3` matrix can be created like this:

```octave
V = [1 2 3]
% >> V = 

        1   2   3

```

We can create a vector like this:

```octave
v = [1; 2; 3]
% >> v = 
        
        1
        2
        3
        
```


##### Range of values in Matrix

We can create a range of values in a matrix by:

```octave
v = 1:6
% >> v = 
        
        1     2     3     4     5     6

```

We can do more with this method:

```octave
v = 1:0.2:2
% >> v = 

        1.0000    1.2000    1.4000    1.6000  1.8000  2.0000
        
```

##### Other methods

We can create matrixes in some other methods as well:

```octave
ones(3, 3)
% >> ans = 
          1   1   1
          1   1   1
          1   1   1

ones(2,3)
% >> ans =
          
          1   1   1
          1   1   1
          
C = 2 * ones(2, 3)
% >> C = 

        2   2   2
        2   2   2

w = ones(1, 3) 
% >> w =

        1   1   1
        
w = zeros(1, 3)
% >> w = 
        
        0   0   0
        
% we can create randam matrixes as well 

w = rand(1,3)     % these are drawn from the uniform distributions between 0 and 1
% >> w =

        0.9315    0.5400    0.5123
        
x = randn(1, 3) % And so these are going to be three values drawn from a Gaussian distribution 
with mean zero and variance or standard deviation equal to one.
% >> x =

        -0.555935   -0.582991   0.013464
        
```

#### 5. Histogram

We can also create histograms:

```octave

w = -6 + sqrt(10) * (randn(1, 10000));

hist(w)

hist(w, 50)   % this will create 50 bars for the graph
```

This will output as follows:

{{< image src="pics/hist-1.png" caption="`hist(w) outputs`">}}

{{< image src="pics/hist-2.png" caption="`hist(w, 50)` outputs">}}

#### 6. Identity Matrix

We can create the identity matrix using `eye()` function as follows:

```octave
eye(4)
% >> ans =

Diagonal Matrix

        1   0   0   0
        0   1   0   0
        0   0   0   1
        0   0   0   1
        
I = eye(3)
% >> I = 

Diagonal Matrix
        
        1   0   0
        0   1   0
        0   0   1
        
```


