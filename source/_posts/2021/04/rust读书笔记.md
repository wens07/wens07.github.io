---
layout: post
title: rust读书笔记
date: 2019-03-31 22:39:40
categories: 
  - [technique]
  - [随笔]
tags: [读书笔记, rust]
keywords: ["rust", "读书笔记"]
toc:
---

### basic concepts
- crate: rust package
- cargo: rust's build system and package manager
- prelude: pre-import module
  1. at the root of every crate, the compiler injects an implicit extern crate std;
  2. in every module, the compiler injects an implicit use std::prelude::v1::*; (for now)

<!-- more -->

- macros
  1. declarative macro  
    `macro_rules! vec{}`
  2. procedural macro (custom derive, attribute-like, function-like)
    ```rust
    use proc_macro;

    #[some_attribute]
    pub fn some_name(input: TokenStream) -> TokenStream {
    }

    // derive
    #[derive(HelloMacro)]
    struct Pancakes;

    fn main() {
        Pancakes::hello_macro();
    }
    ```

- main two return style
```rust
use std::error::Error;
use std::fs::File;

fn main() -> Result<(), Box<dyn Error>> {
    let f = File::open("hello.txt")?;

    Ok(())
}

fn main() {

}
```

- ownership
1. By default, variable bindings have 'move semantics.'
2. automatic referencing and dereferencing: Calling methods is one of the few places in Rust that has this behavior.
   > when you call a method with object.something(), Rust automatically adds in &, &mut, or * so object matches the signature of the method. In other words, the following are the same:
   ```
    p1.distance(&p2);
    (&p1).distance(&p2);
   ```

- Associated functions & methods

- traits
1. One restriction to note with trait implementations is that we can implement a trait on a type only if either the trait or the type is local to our crate.
2. trait as parameter AND trait bound
```rust
pub fn notify(item: &impl Summary) {
    println!("Breaking news! {}", item.summarize());
}

pub fn notify(item: &(impl Summary + Display)) {
}

fn some_function<T: Display + Clone, U: Clone + Debug>(t: &T, u: &U) -> i32 {}
fn some_function<T, U>(t: &T, u: &U) -> i32
    where T: Display + Clone,
          U: Clone + Debug{}
```

- lifetime 

1. `'static` means the reference can live in entire program.
2. lifetime ellision
>rule one : each parameter that is a reference gets its own lifetime parameter.
>
>rule two: if there is exactly one input lifetime parameter, that lifetime is assigned to all output lifetime parameters.
>
>rule three: if there are multiple input lifetime parameters, but one of them is &self or &mut self because this is a method, the lifetime of self is assigned to all output lifetime parameters.

```

### module
1. the path of module
- An absolute path starts from a crate root by using a crate name or a literal crate.
- A relative path starts from the current module and uses self, super, or an identifier in the current module.


2. nested path
```rust
// nested path
// --snip--
use std::cmp::Ordering;
use std::io;
// --snip--

// --snip--
use std::{cmp::Ordering, io};
// --snip--


use std::io;
use std::io::Write;

use std::io::{self, Write};

// bring all pub member to current scope
use std::collections::*;
```

