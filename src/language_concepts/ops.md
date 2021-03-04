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
|  <             | constrains one value to be less than the other | Upper bound must have a known bit size |
|  <=             | constrains one value to be less than or equal to the other | Upper bound must have a known bit size |
|  >             | constrains one value to be more than the other | Upper bound must have a known bit size |
|  >=             | constrains one value to be more than or equal to the other | Upper bound must have a known bit size |
|  ==             | constrains one value to be equal to the other | Both types must not be constants |
|  !=             | constrains one value to not be equal to the other | Both types must not be constants |

### Predicate Operators

`<,<=, !=, == , >, >=` are known are predicate/comparison operations because they compare two values. This differs from the operations such as `+` where the operands are used in _computation_.

### Bitwise Operations Example

```rust,noplaypen 
fn main(x : Field) {
    priv y = x as u32;
    priv z = y & y;
}
```

`z` is implicitly constrained to be the result of `y & y`. The `&` operand is used to denote bitwise `&`. 

> `x & x` would not compile as `x` is a Witness and not an integer type.
