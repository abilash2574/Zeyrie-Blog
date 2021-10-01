---
title: "How to Repair Flatpak"
subtitle: ""
date: 2021-09-21T12:07:23+05:30
draft: false
author: "Abilash S"
authorLink: "https://www.zeryie.in/"
description:
tags: ["linux", "flatpak"]
categories: ["Linux", ]

resources:
- name: featured-image
  src: thumbnail_1.png
- name: featured-image-preview
  src: thumbnail.jpg

toc:
  enable: false
math:
  enable: false
lightgallery: true
license: ""
hiddenFromHomePage: false 
hiddenFromSearch: false 
---

Installing software in linux can be tricky sometimes, especially when we are using the terminal. To solve this we got the GUI package installers, and one such installer is flatpak, which is quite easy to handle naturally. But this doesn't mean it won't get broken sometimes.

  So in this article we solve an common error that occurs mainly due to come interruptions during the installation of an application in flatpak. These interruptions can be a network failure, something going wrong randomly, which stops the installation mid way. 
  
<!--more-->

# How to fix "Aborted due to failure" error in Flatpak

{{< youtube id="smF09IPJyf0" autoplay="true" title="How to repair flatpak package installer">}}

To repair the flatpak installer use the following command:

{{< admonition warning "" >}}
Do not use this command with sudo permissions.
{{< /admonition >}}

```sh
flatpak repair --user
```
