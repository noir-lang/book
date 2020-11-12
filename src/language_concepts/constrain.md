# Constrain Statement

Noir includes a special keyword `constrain` which will explicitly constrain the expression that follows, as long as the operation is a predicate/comparison.

### Constrain statement example

```rust 
fn main(x : Witness, y : Witness) {
    constrain x == y
}
```
 
The above snippet compiles because `==` is a predicate operation. Conversely, the following will not compile:

```rust 
fn main(x : Witness, y : Witness) {
    constrain x + y
}
```

> The rationale behind this not compiling is due to ambiguity. It is not clear if the above should equate to `x + y == 0` or if it should check the truthiness of the result.