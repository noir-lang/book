# Data types

There are two subsets of data types that each datatype will fall into; fundamental and compound.

A **fundamental type** is a data type which is defined in the core language. This is not specific to Noir. Examples in modern programming languages such as Rust are u32, usize and char. 

A **compound type** is a type in the core language which must be defined using another type. Examples in modern programming languages are arrays, tuples and functions.

Although each value in a constraint system is fundamentally a field element, we add a layer of abstraction over this; each value can be _concealed_ or _revealed_. 

A **concealed value** is known only to the Prover, while, a **revealed value** is known by the Prover and Verifier. All concealed and revealed values are _fundamental_ types.

## Fundamental Types

### Concealed Types

Concealed types are generally referred to as witnesses.

#### Witness Type

A Witness type is the default concealed type. Here's an example that shows declaration and usage of the Witness type.

```rust
fn main(x : Witness, y : Witness) {
    priv z = x + y;
}
```

`x`, `y` and `z` are Witness types. Using the `priv` keyword we derived new Witness type `z` which is constrained to be equal to `x + y`.

#### Integer Type

An integer type is a witness type which has been constrained using a range constraint. The Noir front-end currently supports arbitrary sized integer types.

Below we show the integer type in action:

```rust
fn main(x : Witness) {
    priv y = x as u24;
}
```

`x` and `y` are both concealed types, however `y` is an integer type. If `y` exceeds the range \\([0,2^{24}-1]\\) then any proof created will output false by the verifier.

> **Note:** The Aztec backend only supports even sized integer types currently, so while using the Aztec backend, only even sized integer types such as u32, u48 will produce proofs.

### Revealed Types

#### Constants

A constant type is a value that does not change per circuit instance. This is different to a concealed type which changes per proof. If a constant type that is being used in your program in changed, then your circuit will also change.

Below we show how to declare a constant value:

```rust
fn main() {
    const a = 5;
}
```


#### Public Types

A public type is a value that may change per circuit instance. Unlike Constants, changing a public value will not change the circuit.

```rust
fn main(x : Public) {

}
```
As of the beta release, public types can only be declared through type parameters. In the code, they are treated no differently to witness types. 

> **Note:** This behaviour and type will change in future releases, to catch a linearity bug in user code.

## Compound Types

Compound types are declared using the `let` keyword. Currently arrays are the only supported compound type.

#### Arrays 

An array is a data structure which allows you to group together data types. All values in an array must be of the same type; homogeneous. 

```rust
fn main(x : Witness, y : Witness) {
    let my_arr = [x, y];
}
```

> **Example:** An array of Witness types cannot be grouped together with an array of Integer types.