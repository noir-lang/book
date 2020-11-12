# Operations

## Table of Supported Operations

| Operation      | Description          | Requirements     |
| :-- | :-----------------:         | -----------: |
|  +             | Adds two concealed types together   | Types must be concealed    |
|  -             | Subtracts two concealed types together | Types must be concealed |
|  *             | Multiplies two concealed types together | Types must be concealed |
|  /             | Divides two concealed types together | Types must be concealed |
|  ^             | XOR two concealed types together | Types must be integer |
|  &             | AND two concealed types together | Types must be integer |

### Bitwise Operations Example

```rust 
fn main(x : Witness) {
    priv y = x as u32;
    priv z = y & y;
}
```

`z` is implicitly constrained to be the result of `y & y`. The `&` operand is used to denote bitwise `&`. 

> `x & x` would not compile as `x` is a Witness and not an integer type.
