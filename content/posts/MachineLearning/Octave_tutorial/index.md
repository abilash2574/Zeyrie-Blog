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

## Basics

### Basic Operations

#### Arithmetic Operations

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

#### Logical Operations

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
