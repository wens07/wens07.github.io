---
title: c/cpp-useful-tools
date: 2015-06-15 11:57:15
categories: technique
tags: c/c++
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




