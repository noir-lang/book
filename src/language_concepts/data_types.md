# Data types

Noir has several varieties of data types: the primitive `Field` type, integer types, `bool`, arrays, structs, and tuple types.

Although each value in a constraint system is fundamentally a field element, we add a layer of abstraction over this;
each value can be _concealed_ (a private type) or _revealed_ (a public type).

A **private value** is known only to the Prover, while, a **public value** is known by the Prover and Verifier.
All public and private values are primitive types, though individual
fields of a struct may also be marked private or public.

Note that the terms private and public when applied to a type (e.g. in `pub Field`) have a different meaning than when
applied to a function `pub fn foo() { ... }`.
The later is a visibility modifier familiar to those coming from existing
langauges, while the former can be thought of as a visibility modifier for the Verifier.
So a `pub Field` would be visible to the Verifier while a `Field` would not (private is the default modifier).

## Primitive Types

Any of these types can be private (the default) or public (via a `pub` modifier).

Note that private types are also referred to as witnesses.

#### Field Type

A field type corresponds to a native field type in the backend. Usually this is a (roughly) 256-bit integer.
This should generally be the default type reached for to solve problems. Using a smaller integer type like `u64` incurs
extra range constraints and so is less efficient rather than more.

```rust,noplaypen
fn main(x : Field, y : Field) {
    let z = x + y;
}
```

`x`, `y` and `z` are witness types (private `Field`). Using the `let` keyword we derived a new witness `z` which is constrained to be equal to `x + y`.

#### Integer Type

An integer type is a witness type which has been constrained using a range constraint.
The Noir front-end currently supports arbitrary sized integer types.

Below we show the integer type in action:

```rust,noplaypen
fn main(x : Field) {
    let y = x as u24;
}
```

`x` and `y` are both private types (witnesses), however `y` is an integer type.
If `y` exceeds the range \\([0,2^{24}-1]\\) then any proof created will output false by the verifier.

> **Note:** The Aztec backend supports even and odd sized integer types, so while using the Aztec backend, even sized integer types such as u32, u48, as well as odd sized integer types such as u5, u3 will produce proofs.

#### Constants

A constant type is a value that does not change per circuit instance. This is different to a witness which changes per proof.
If a constant type that is being used in your program is changed, then your circuit will also change.

Below we show how to declare a constant value:

```rust,noplaypen
fn main() {
    let a: comptime Field = 5;

    // `comptime Field` can also be inferred:
    let a = 5;
}
```

Note that variables declared as mutable may not be constants:

```rust,noplaypen
fn main() {
    // error: Cannot mark a comptime type as mutable - any mutation would remove its const-ness
    let mut a: comptime Field = 5;

    // a inferred as a private Field here
    let mut a = 5;
}
```

#### Globals

Noir also supports global variables. However, they must be compile-time variables. If `comptime` is not explicitly written in the type annotation the compiler will implicitly specify the declaration as compile-time. They can then be used like any other compile-time variable inside functions. The global type can also be inferred by the compiler entirely. Globals can also be used to specify array annotations for function parameters and can be imported from submodules. 

Globals are currently limited to Field, integer, and bool literals.

```rust,noplaypen
global N: Field = 5; // Same as `global N: comptime Field = 5`

fn main(x : Field, y : [Field; N]) {
    let res = x * N;

    constrain res == y[0];

    let res2 = x * mysubmodule::N;
    constrain res != res2;
}

mod mysubmodule {
    use dep::std;

    global N: Field = 10;

    fn my_helper() -> comptime Field {
        let x = N;
        x
    }
}
```

#### `pub` Modifier

A public type is a value that may change per circuit instance. Unlike Constants, changing a public value will not change the circuit.

```rust,noplaypen
fn main(x : pub Field) {

}
```

As of the beta release, public types can only be declared through parameters on `main`.
In the code, they are treated no differently to witness types.

> **Note:** This behaviour and type will change in future releases, to catch a linearity bug in user code.

## Compound Types

Noir also supports arrays, structs, and tuples whose elements may be public or private.

#### Arrays

An array is a data structure which allows you to group together data types.
All values in an array must be of the same type (i.e., they're homogeneous).

```rust,noplaypen
fn main(x : Field, y : Field) {
    let my_arr = [x, y];
}
```

Note that currently Noir only supports arrays with integer or `Field` elements.

> **Example:** An array of `Field` types cannot be grouped together with an array of integer types.

#### Structs

Structs can be used to group together multiple different types:

```rust,noplaypen
struct Operation {
    lhs: Field,
    opcode: u8,
    rhs: Field,
}

fn main() {
    let opcode = 3 as u8;

    // operation: Operation
    let operation = Operation {
        lhs: 0,
        rhs: 1,
        opcode,
    }

    let zero = operation.lhs;
}
```

Structs can also be destructured in a pattern, binding each field to a new variable:

```rust,noplaypen
fn main() {
    let Operation { lhs, rhs: the_rhs, opcode: _ } = get_operation();
    // lhs and the_rhs are now in scope
}
```

#### Tuples

Noir also supports tuples, which can be thought of as anonymous structs with integers as field names.

```rust,noplaypen
fn main() {
    let tuple = (1, 2);
    let (a, b) = tuple;

    let (c, d, mut (e, f)) = (3, 4, (5, 6));
}
```

Tuple fields can be accessed via destructuring as above or via member access syntax.
The first field name of a tuple is `0`, then `1` and so on:

```
fn main() {
    // tuple: (comptime Field, comptime Field, comptime Field, comptime Field)
    let tuple = (5, 6, 7, 8);

    let five = tuple.0;
    let eight = tuple.3;
}
```
