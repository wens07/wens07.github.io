---
layout: post
title: design_pattern
date: 2019-03-01 22:39:40
categories: 
  - [technique]
  - [随笔]
tags: [读书笔记, c/c++]
keywords: ["c++", "读书笔记"]
toc:
---

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