---
layout: post
title: design_pattern
date: 2019-03-01 22:39:40
updated: 2023-10-24
categories:
  - [technique]
  - [随笔]
tags: [读书笔记, c/c++]
keywords: ["c++", "读书笔记"]
toc:
---

## basic principle
- SOLID
>> S: single resposibility<br>
   O: open-closed: open for extension, closed for modification<br>
      **simple shoud not go back to code/modify somthing haveing writtern adn tested**
   L: liskov substitution<br>
      **if interface is ok to type A, it should also is ok to its inherited type B**
   I: interface segregation<br>
   D: dependency inversion<br>
      **high level module should not depend on low level; absraction should not depend on detail**

## creatation patterns
### factory method pattern

1. Delegation of object creation to  factory method
2. Extensibility by permitting arbitrary many factory methods
3. Code reuse through runtime polymorphism
4. Decouple initialization of factories from  creating connections

<!-- more -->
```cpp
struct Connection {
    virtual ~Connection() = default;
    virtual send() = 0;
};

struct TcpConnection: public Connection {
    send() override {
        implementations....
    }

};

struct UdpConnection: public Connection {
    send() override {
        implementations....
    }

};

struct ConnectionFactory {
    virtual ~ConnectionFactory() = default;
    virtual std::unique_ptr<ConnectionFactory> make() = 0;
};

struct TcpConnectionFactory: public ConnectionFactory {
    std::unique_ptr<ConnectionFactory> make() override {
        implementations...
    }
};

struct UdpConnectionFactory: public ConnectionFactory {
    std::unique_ptr<ConnectionFactory> make() override {
        implementations...
    }
};

```

### abstract factory pattern
something similar to factory method, but factory method for single objects, however abstract factory 
is for some related objects.

### builder pattern
usually used to create an object with different parts
> 1. object  2. abstract builder & concrete builder(to create object) 3. the client(a class) to make object 

### prototype pattern
create object by clone(reuse) existed object

## structural patterns
### composite pattern
- array backed propertyp
```cpp
class widget {
enum abilities {strenth, agi, teli, count};
std::array<int, count> properties;
};

```
## behavior patterns
### command pattern
used to encapsulate the object to a command class.


### NON-Virtual Interface pattern(NVI) -- Template Method Pattern


### M&M rule
mutable and mutex(or atomic) should go together