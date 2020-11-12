# Functions

Functions in Noir follow the same semantics of Rust, Noir does not support early returns.


To declare a function the `fn` keyword is used.

```rust 
fn foo() {}
```

All parameters in a function must have a type and all types are known at compile time. The parameter is pre-pended with a colon and the parameter type. Multiple parameters are separated using a comma. 

```rust 
fn foo(x : Witness, y : Public){}
```

The return type of a function can be stated by using the `->` arrow notation. The function below states that the foo function must return a Witness. If the function returns no value, then the arrow is omitted.

```rust 
fn foo(x : Witness, y : Public) -> Witness{
    x + y
}
```