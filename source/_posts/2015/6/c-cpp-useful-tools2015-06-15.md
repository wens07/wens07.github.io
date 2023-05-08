---
title: c/cpp-useful-tools
date: 2015-06-15 11:57:15
categories: technique
tags: [c/c++, command, tool]
keywords: [c, c++, tool]
toc:
---

### cdecl

 Cdecl  (and  c++decl) is a program for encoding and decoding C (or C++) type declarations.

 [cdecl online website](http://cdecl.org/)

### size(on mac)

size -- print the size of the sections in an object file.
`size -x(print by hex) -l -m a.out`

<!-- more -->
### otool(on mac)

otool -- object file displaying tool.
`otool -s __TEXT(which segment) __text(which section) a.out`

### nm(on mac)
see the symbol table
`nm libwens.so`

### strings
find the printable strings in a object, or other binary, file


### clang++ & g++ options
1. -fno-elide-constructors


### debugging & profiling

1. valgrind
2. windows debug runtime

### define config
```cpp

#if defined(_MSC_VER)
#   if _MSC_VER <= 1900
#       error Boost.PFR library requires MSVC with c++17 support (Visual Studio 2017 or later).
#   endif
#elif __cplusplus < 201402L
#   error Boost.PFR library requires at least C++14.
#endif
```

### static code analyzer
1. clang static analyzer
2. pvs-studio
3. cppchecker

### dynamic analyzer
1. valgrind
2. Dr.Memory
3. Intel Inspector

### compile analyzer
1. Address sanitizer
2. Memory sanitizer
3. Thread sanitizer
`clang main.cpp -o main -fsanitizer=address | memory | thread`

### performance profile tool
1. intel vtune amplifier


### gdb
1. `break xxxx if xxxx`
2.  break then execute command
```
(gdb) b do_mmap_pgoff
Breakpoint 1 at 0xffffffff8111a441: file mm/mmap.c, line 940.
(gdb) command 1
Type commands for when breakpoint 1 is hit, one per line.
End with a line saying just "end".
>print addr
>print len
>print prot
>end
(gdb)
```
3. `gdb --args pizzamaker --deep-dish --toppings=pepperoni`
4. `macro expand task_is_stopped_or_traced(init_task)`
4. `ctrl+x+a`  toggle to / from tui mode
   `ctrl+p / ctrl+n` previous or next command in tui mode
   `ctrl+x+2` swith between windows
5. `ctrl+l` clear the gdb commandline or reflesh the screen
6. `set print pretty on`  open print pretty
7. `info share`  no info in bt, maybe miss sharelib
8. `file the_exec_file`  no info in bt, maybe not read the symble of executable
9. `start` go to program start(main function, generally)
