---
title: linux_programming
date: 2019-08-23 08:40:59
updated: 2019-08-23 08:40:59
categories:  technique
tags: [c++, linux]
keywords: [c++, linux]
toc:
---

### select() vs poll() vs epoll()

1. select()
`int select(int nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, struct timeval *timeout);`

2. poll()
```cpp
int poll (struct pollfd *fds, unsigned int nfds, int timeout);

struct pollfd {
      int fd;
      short events; 
      short revents;
};

```

3. epoll()
`epoll_create(), epoll_ctl(), epoll_wait()`


- select() have three bitmask-based set of fds(fd-set), poll() only have signle array of fds(pollfd structure)
- select() will reconstruct the fds, so should build each set before each call; poll() has seperate events and returned events, so it don't need.

- select() and poll() manage everything in user mode and send sets each time to wait on, to add another fd we need to add it to the set and call select()/poll() again();  however epoll() use epoll_create to create context in the kernel mode, using epoll_ctl to update the context.


<!-- more -->