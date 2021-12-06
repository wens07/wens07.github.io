### test
1. #[test]
2. #[ignore]
3. #[should_panic]
4. #[cfg(test)]
5. cargo test --test integration_test
   cargo test test_name

6. common function used in tests(naming convention rust knowns)
   tests/common/mod.rs

   other integration test can use the common function
    ```rust
    Filename: tests/integration_test.rs


        use adder;

        mod common;

        #[test]
        fn it_adds_two() {
            common::setup();
            assert_eq!(4, adder::add_two(2));
        }

    ```

7. A package can have multiple binary crates by placing files in the src/bin directory: each file will be a separate binary crate.
8. the entire module tree is rooted under the implicit module named crate.
9. package path
   A path can take two forms:
        An absolute path starts from a crate root by using a crate name or a literal crate.
        A relative path starts from the current module and uses self, super, or an identifier in the current module.

10. The way privacy works in Rust is that all items (functions, methods, structs, enums, modules, and constants) are private by default

11. we use pub before a struct definition, we make the struct public, but the struct’s fields will still be private.
    we make an enum public, all of its variants are then public