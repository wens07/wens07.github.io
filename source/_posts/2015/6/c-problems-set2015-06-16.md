---
title: c-problems set
date: 2015-06-16 17:03:30
categories: technique
tags: c/c++
keywords: [c, problem]
toc:
---

### Linux program startup

![c linux startup](/images/c_linux_startup.png)

1. the shell or gui calls `execve()` which execute linux system call execve(), it will set up a stack for you, and push onto it **argc**, **argv**, **envp**. the filedescription  0, 1, 2 are left to whatever the shell set them to. The loader does much work for you setting up your relocations, and as we'll see much later, calling your preinitializers. When everything is ready, control is handed to your program by calling  _start().


### escape sequences in c
![escape sequence](/images/2015/c_escape_sequence.png)

> /000  ---- / 后面1,2,or 3三个8进制的数,表示character在character set中的值
  /xhh ----- / 后面任意个16进制的数,表示character在character set中的值

<!-- more -->
