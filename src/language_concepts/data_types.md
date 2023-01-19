# Data Types

Every value in Noir is specified with a certain data type, which informs Noir tools how to work with that data when processing Noir programs.

All values in Noir are fundamentally `Field` elements. For a more approachable developing experience, abstractions are added on top to introduce different data types in Noir.

Noir has two category of data types: primitive types (e.g. `Field`, integer, `bool`) and compound types (e.g. array, tuple, struct). Each value can either be private or public.

## Private & Public Types

A **private value** is known only to the Prover, while a **public value** is known by both the Prover and Verifier. All public and private values are primitive types, though individual fields of compound types may also be marked private or public.

> **Note:** For Noir programs using public smart contract verifiers, public values defined in such programs can be considered as public knowledge once their proofs are verified on-chain.

Public data types are treated no differently to private types apart from the fact that their values will be revealed in proofs generated. Simply changing the value of a public type will not change the circuit (where the same goes for changing values of private types as well).

_Private_ are also referred to as _witnesses_ sometimes.

> **Note:** The terms private and public when applied to a type (e.g. `pub Field`) have a different meaning than when applied to a function (e.g. `pub fn foo() {}`).
>
> The latter is a visibility modifier familiar to those coming from other languages, while the former can be thought of as a visibility modifier for the Verifier to interpret.

### pub Modifier

All data types in Noir are private by default. Types are explicitly declared as public using the `pub` modifier:

```rust,noplaypen
fn main(x : Field, y : pub Field) -> pub Field {
    x + y
}
```

In this example, the first input (i.e. `x`) is private while the second input (i.e. `y`) and the return value (i.e. `x + y`) are public.

> **Note:** As of this moment, public types can only be declared through parameters on `main`.

## Primitive Types

A primitive type represents a single value. They can be private or public.

### The Field Type

The `Field` type corresponds to the native field type of the proving backend. For example, this would be a (roughly) 256-bit integer when using the default TurboPlonk backend.

Fields are simply defined with the keyword `Field`:

```rust,noplaypen
fn main(x : Field, y : Field)  {
    let z = x + y;
}
```

`x`, `y` and `z` are all private `Field` in this example. Using the `let` keyword we derived a new private value `z` constrained to be equal to `x + y`.

If efficiency is of priority, `Field` should be used as the default type for solving problems. Using smaller integer types (e.g. `u64`) incurs extra range constraints.

### Integer Types

An integer type is a range constrained `Field` value, and the Noir frontend currently supports unsigned, arbitrary-sized integer types.

An integer type is specified first with the letter `u`, indicating its unsigned nature, followed by its length in bits (e.g. `32`). For example, a `u32` variable can store a value in the range of \\([0,2^{32}-1]\\):

```rust,noplaypen
fn main(x : Field, y : u32) {
    let z = x as u32 + y;
}
```

`x`, `y` and `z` are all private values in this example. However, `x` is a `Field` while `y` and `z` are unsigned 32-bit integers. If `y` or `z` exceeds the range \\([0,2^{32}-1]\\), proofs created will be rejected by the verifier.

> **Note:** The default TurboPlonk backend supports both even (e.g. `u16`, `u48`) and odd (e.g. `u5`, `u3`) sized integer types.

### The Boolean Type

A boolean type in Noir has two possible values: `true` and `false`, and is specified using `bool`. For example:

```rust,noplaypen
fn main() {
    let t = true; // type implicitly interpreted
    let f: bool = false; // type explicit annotated
}
```

> **Note:** When returning a boolean value, it will show up as a value of 1 for `true` and 0 for `false` in _Verifier.toml_.

The main usage of the boolean type is in conditionals (e.g. `if` expressions, `constrain`). More about conditionals are covered in the [Control Flow](./control_flow.md) and [Constrain Statement](./constrain.md) sections.

## Compound Types

A compound type groups together multiple values into one type. Elements within a compound type can be private or public.

### The Array Type

An array is one way of grouping together values into one compound type:

```rust,noplaypen
fn main(x : Field, y : Field) {
    let my_arr = [x, y];
}
```

All elements in an array must be of the same type (i.e. homogeneous). That is, `Field` values cannot be grouped together with integer values in one array for example.

Noir currently supports arrays with `Field` or integer elements only.

### The Tuple Type

A tuple collects multiple values like an array, but with the added ability to collect values of different types:

```rust,noplaypen
fn main() {
    let tup: (u8, u64, Field) = (255, 500, 1000);
}
```

One way to access tuple elements is via destructuring using pattern matching:

```rust,noplaypen
fn main() {
    let tup = (1, 2);

    let (one, two) = tup;

    let three = one + two;
}
```

Another way to access tuple elements is via direct member access, using a period (`.`) followed by the index of the element we want to access. Index `0` corresponds to the first tuple element, `1` to the second and so on:

```rust,noplaypen
fn main() {
    let tup = (5, 6, 7, 8);

    let five = tup.0;
    let eight = tup.3;
}
```

### Structs

A struct is used for grouping multiple related values of different types like a tuple, with the added ability to name the pieces of data (also referred to as _fields_).

> **Note:** The naming of _fields_ here is unrelated to Noir's `Field` type. It simply mimics Rust's convention.

When defining a struct, you will name the struct and every fields within as `key: type` pairs. A struct can hold fields of different types:

```rust,noplaypen
struct Animal {
    hands: Field,
    legs: Field,
    eyes: u8,
}
```

An instance of struct can then be created with concrete values in `key: value` pairs. Struct fields are accessible using their given names, instead of by their order like in arrays and tuples:

```rust,noplaypen
fn main() {
    let legs = 4;

    let dog = Animal {
        hands: 0,
        legs,
        eyes: 2, // type implicitly interpreted
    };

    let zero = dog.hands;
}
```

Structs can also be destructured in a pattern, binding each field to a new variable:

```rust,noplaypen
fn main() {
    let Animal { hands, legs: feet, eyes } = get_octopus();

    // hands, feet and eyes are now in scope
    let ten = hands + feet + eyes as u8;
}

fn get_octopus() -> Animal {
    let octopus = Animal {
        hands: 0,
        legs: 8,
        eyes: 2,
    };

    octopus
}
```

The new variables can be bound with names different from the original struct field names, as showcased in the `legs --> feet` binding in the example above.
