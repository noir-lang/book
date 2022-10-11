# Mutability

Variables in noir can be declared mutable via the `mut` keyword.
Mutable variables can be reassigned to via
an assignment expression.

```rust,noplaypen
let x = 2;
x = 3; // error: x must be mutable to be assigned to

let mut y = 3;
let y = 4; // OK
```

The `mut` modifier can also apply to patterns:

```rust,noplaypen
let (a, mut b) = (1, 2);
a = 11; // error: a must be mutable to be assigned to
b = 12; // OK

let mut (c, d) = (3, 4);
c = 13; // OK
d = 14; // OK

// etc.
let MyStruct { x: mut y } = MyStruct { x: a }
// y is now in scope
```

Note that mutability in noir is local and everything is passed by value, so if a
called function mutates its parameters then the parent function will keep the old value of the parameters.

```rust,noplaypen
fn main() -> Field {
    let x = 3;
    helper(x);
    x // x is still 3
}

fn helper(mut x: i32) {
    x = 4;
}
```

### Why only local mutability?

Witnesses in a proving system are immutable in nature.
Noir aims to _closely_ mirror this setting without applying additional overhead to the user.
Modeling a mutable reference is not as straightforward as on conventional architectures and
would incur some possibly unexpected overhead.
