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
3. tracy
4. heaptrack

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
3. `gdb --args pizzamaker --deep-dish --toppings=pepperoni` `(gdb) set args [the arg list]`  `(gdb) show args`
4. `macro expand task_is_stopped_or_traced(init_task)`
4. `ctrl+x+a`  toggle to / from tui mode
   `ctrl+p / ctrl+n` previous or next command in tui mode
   `ctrl+x+2` swith between windows
5. `ctrl+l` clear the gdb commandline or reflesh the screen
6. `set print pretty on`  open print pretty
7. `set print array-indexes on` open array index
8. `info share`  no info in bt, maybe miss sharelib  
    `info source` show info for current source file  
    `set substitute-path from to` set the source file
9. `file the_exec_file`  no info in bt, maybe not read the symble of executable
10. `start` go to program start(main function, generally)
11. `record` debug reverse
12. `g++ -g3` for macro info, which -g is g2 for default
13. `dprintf location, format_string`  dynamic printf in gdb
14. `show non-stop/ show scheduler-locking`  gdb non-stop mode or all-stop mode
15. set coredump
>> 默认corefile是生成在程序的执行目录下或者程序启动调用了chdir之后的目录,我们可以通过设置生成corefile的格式来控制它，让其生成在固定的目录下。

>> /proc/sys/kernel/core_uses_pid可以控制产生的core文件的文件名中是否添加pid作为扩展，如果添加则文件内容为1，否则为0
/proc/sys/kernel/core_pattern可以设置格式化的core文件保存位置或文件名，比如原来文件内容是core-%e

>>
```bash
# echo "/home/wens07/programming/build/core_%e_%p" > /proc/sys/kernel/core_pattern
将会控制所产生的core文件会存放到corefile目录下，产生的文件名为core-命令名-pid-时间戳

或者

$ sysctl -w kernel.core_pattern=/corefile/core-%e-%p-%t
如果想让每次启动都保存设置，则需要写入配置文件中.

# echo "kernel.core_pattern=/home/wens07/programming/build/core_%e_%p" >> /etc/sysctl.conf
# sysctl -p /etc/sysctl.conf

kernel.core_pattern =/home/wens07/programming/build/core_%e_%p
关于格式的的控制有如下几个参数：

复制代码
%%：相当于%
%p：相当于<pid>
%u：相当于<uid>
%g：相当于<gid>
%s：相当于导致dump的信号的数字
%t：相当于dump的时间
%e：相当于执行文件的名称
%h：相当于hostname
```
16. using gdbserver  
```bash
# remote target
gdbserver localhost:<port-numer> <program> <args>

# local host
gdb 
file <program>
target remote <ip-of-target>:<port-numer>
set sysroot <path-to-sysroot>
```
