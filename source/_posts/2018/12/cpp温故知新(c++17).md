---
layout: post
title: cpp温故知新(c++17)
date: 2018-12-07 22:39:40
categories: 
  - [technique]
  - [随笔]
tags: [读书笔记, c/c++]
keywords: ["c++", "c++17", 读书笔记]
toc:
---

### storage duration
- **automatic** storage duration  
The storage for the object is allocated at the beginning of the enclosing code block and deallocated at the end. All local objects have this storage duration, except those declared static, extern or thread_local.

- **static** storage duration  
 The storage for the object is allocated when the program begins and deallocated when the program ends. Only one instance of the object exists. All objects declared at namespace scope (including global namespace) have this storage duration, plus those declared with static or extern.

 - **thread_local** storage duration
 The storage for the object is allocated when the thread begins and deallocated when the thread ends. Each thread has its own instance of the object. Only objects declared thread_local have this storage duration. thread_local can appear together with static or extern to adjust linkage.

- **dynamic** storage duration
The storage for the object is allocated and deallocated per request by using dynamic memory allocation functions.

<!-- more -->
### linkage 
- no linkage  
  The name can be referred to only from the scope it is in.  
variables in block scope(except extern)

- static linkage  
  The name can be referred to from all scopes in the current translation unit.

variable in namespace scope
1. variabales in namespace scope declared *static*
2. const-qulified(or constexpr) variable not declared extern
2. data member in anonymous unions
3. variables in anonymous namespace

- external linkage
other variable in namespace scope


### perfect Forwarding
it used to reserve the r or l value property of a parameter in generic context.

### emplace_back vs push_back
1. emplace_back cannot use to initilize aggregated things.(up to c++17, it is specialized to none list in-place construction)


### container

1. vector vs deque
for small size use vector, otherwise use deque instead.



### new features

1. structured binding
auto [res1, res2] = ...

2. init statement of if or switch

3. constexpr if

4. c++11 unknow before
- function reload
```cpp
class Test {
private:
    std::string name{"wens"};

public:
    std::string getname() && { printf("in && function\n"); return name;}
    const std::string& getname() const& {  printf("in const& function\n"); return name;}
};


int main() {

    Test t;
    auto v = t.getname();
    printf("%s\n", typeid(v).name());
   
    auto a = Test{}.getname();
    printf("%s\n", typeid(a).name());
   


    getchar();
    return 0;

}

```

- value categories

expression -> glvalue(generalized lvalue) and rvalue  
glvalue -> lvalue and xvalue(expiring value)  
rvalue -> xvalue and prvalue(pure rvalue)  


simple:  
lvalue: everything has name and string literal (identiy of an object)  
prvalue: temporaries and other literal (perform initialization/compute an object)  
xvalue: value from std::move() (denote an object whose resource can be reused)  
**glvalue produce locations, prvalue preform initialize **

c++17:
prvalue perform initialization -> no temporary object yet
glvalue produce locations
materialization to get temporary object -> prvalue to xvalue conversion


### lambda funcion vs std::function

1. std::function cannot inline by compiler
2. when lambda with capture assigned to std::function, std::function will do heap allocation(some implementation may not heap-alloacte when less than specific threshhold) 

### sizeof & alignof
1. alignof(T) = max(alignof(member1), alignof(member2)...)
2. sizeof(T) % alignof(T) == 0


### determine compile type
1. `_MSC_VER`
2. `__clang__`
3. `__GNUC__`

### copy ellison for initialization from temporaries(prvalues) is required in c++17
callable copy/move constructor no longer required

```cpp
class Test {
public:
  Test() = default;
  //no copy/move constructor
  Test(const Test& ) = delete;
  Test(Test&& ) = delete;

};


void foo(Test t) {

}
foo( Test() ) //is ok in c++17

```

### auto decays
1. raw arrays convert to pointers
2. functions convert to function pointers
3. top-level references are removed
4. top-level const/volatile are removed

### initialization {}
- to pass mutiple parameters to ordinary constructors
  different types ok

- as an std::initializer_list<>
  must be homogeneous(same types or can conversion to the same type)
  only for {}

- () initialization for ordinary constructor only
  {} initialization for all constructors
  1. std::initialization_list<> constructors has higher priority
  2. but the default constructor has the highest priority


### enum initializaiont with integer
1. only with direct list initialization
2. if the enum has fixed underlying type
3. since c++17

```
enum class Salution{mr, ms};

Salution s{17}
```

### uniform initialization is not quite work with atomic and assert(maybe fixed int c++20)
1. atomic

```cpp
//with P0883 maybe fixed in c++20
std::atomic<int> x1;    //does zero initialize 
std::atomic<int> x2{};  //does not zero initialize

struct counter {
   int external_counter = 0;
   int count = 1;
};

std::atomic<counter> c1; //does not initialize with 0 and 1
std::atomic<counter> c2; //does also not initialize with 0 and 1

```

2. assert
```cpp
assert(c == std::complex(0, 0)); //ok
assert(c == std::complex{0, 0}); //does not compile
assert((c == std::complex{0, 0})); //ok
```


### compiler related

1. registers
rax(64) ->  eax(32) -> ax(16) -> ah(8) and al(8) (left bits zeroed)

`rax`: return value  
`rdi`: 1st param  
`rsi`: 2nd param



2. Underscore `(_)` is special, as C++ reserves the following to be used by the compiler and the standard library
- any identifier that starts with an `_` followed by an upper-case letter, and
- any identifier that contains two consecutive underscores `(i.e. __)` anywhere in its name

3. platform judge
```cpp
#if defined(_WIN32)
/* we're on windows */
#elif defined(__GNUC__) && !defined(__clang__)
/* we're on gcc ! */
#elif defined(__clang__)
/* we're on clang */
#else
/* ¯\_(ツ)_/¯ */
#endif
```


### practical performance practices
1. const & initialize
- always const
- always initialize
- use IIFE can help you initialize
- don't recalculate values that can be calculated once

2. list vs vector vs array vs containers
- always prefer std::array
- then std::vector

3. others
- avoid object copying
- avoid automatic conversion: using conversion explicit
- don't pass smart pointers
- avoid std::endl
- prefer return std::unique_ptr<T> to std::shared_ptr<T>

