---
title: "How to Install Arch Linux"
subtitle: ""
date: 2021-09-22T23:01:27+05:30
lastmod: 2021-09-22T23:01:27+05:30
draft: true
author: "Abilash S"
authorLink: "https://www.zeryie.in/"
description:
tags:
categories:

resources:
- name: featured-image
  src: featured-image.webp
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: false
lightgallery: false
license: ""

hiddenFromHomePage: false
hiddenFromSearch: false
---

In this tutorial, we will learn how to install arch linux, 

<!--more-->


# Getting Started

So, lets first head to the official {{< link href="https://archlinux.org/download/" content="Arch linux" title="Visit Arch linux download page" >}} website's download page to download the iso file for installation.

In this page, you have different options to download the image file for different purposes. Choose the one that suits your case. 

This tutorial will complete until we install all the necessary packages and tools for our arch system to boot.

# Creating a Bootable installation media

# Booting into the installation media

# Installation

## Setup the keyboard layout

{{< admonition info "" >}}
By default the keyboard layout is set to en-us!
{{< /admonition >}}

To list all the availabe keyboard layouts:

```sh
ls /usr/share/kbd/keymaps/**/*.map.gz | less
```

Then to load the layout:

```sh
loadkeys de-latin1
```


## Connet to Internet

To verify if you have an active connection, you can use ping 

{{< admonition tip "To check if you have internet connection" >}}
You can use `ping`, as follows:
```sh
ping www.google.com
```
{{< /admonition >}}

<!-- Write here how to connect to a wifi network -->


## Update the system clock

To update the system clock run:

```sh
timedatectl set-ntp true
```

To verify if the above command worked current:

```sh 
timedatectl status
```

## Partitioning the disk

