# Functions

Functions in Noir follow the same semantics of Rust, Noir does not support early returns.


To declare a function the `fn` keyword is used.

```rust,noplaypen 
fn foo() {}
```

All parameters in a function must have a type and all types are known at compile time. The parameter is pre-pended with a colon and the parameter type. Multiple parameters are separated using a comma. 

```rust,noplaypen 
fn foo(x : Witness, y : Public){}
```

The return type of a function can be stated by using the `->` arrow notation. The function below states that the foo function must return a Witness. If the function returns no value, then the arrow is omitted.

```rust,noplaypen 
fn foo(x : Witness, y : Public) -> Witness{
    x + y
}
```

## Call Expressions

Calling a function in Rust is executed by using the function name and passing the necessary arguments the function header.

Below we show how to call the `foo` function from the main function using a call expression:

```rust,noplaypen
fn main(x : Witness, y : Witness) {
    priv z = foo(x);
}

fn foo(x : Witness) -> Witness {
    x + x
}
```