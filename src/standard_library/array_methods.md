
# Array

For convenience, the STD provides some ready-to-use, common methods for arrays[^migrationNote]:

## len

Returns the length of an array

```rust
fn len<T, N>(_array: [T; N]) -> comptime Field
```

example

```rust
fn main() {
    let array = [42, 42]
    constrain arr.len() == 2;
}
```

## sort

Returns a new sorted array with a built-in function. Original array remains untouched.

```rust
fn sort<T, N>(_array: [T; N]) -> Self
```

example

```rust
fn main() {
    let arr = [42, 32]
    let sorted = arr.sort();
    constrain sorted == [32, 42];
}
```

## sort_via

Sorts the array with a custom sorting function

```rust
fn sort_via<T, N>(mut a: [T; N], ordering: fn(T, T) -> bool) -> Self
```

example

```rust
fn main() {
    let arr = [42, 32]
    let sorted_ascending = arr.sort_via(|a, b| a < b);
    constrain t == [32, 42]; // verifies

    let sorted_descending = arr.sort_via(|a, b| a > b);
    constrain t == [32, 42]; // does not verify
}
```

## fold

Applies a function to each element of the array, returning the final accumulated value. The first parameter is the initial value.

One should know ihis is a left fold, meaning that the function is always applied to the leftiest element. So for a given call the expected result would be equivalent to:

```rust
let a1 = [1];
let a2 = [1, 2];
let a3 = [1, 2, 3];

let f = |a, b| a - b;
a1.fold(10, f)  //=> f(10, 1)
a2.fold(10, f)  //=> f(f(10, 1), 2)
a3.fold(10, f)  //=> f(f(f(10, 1), 2), 3)
```

```rust
fn fold<U>(mut accumulator: U, f: fn(U, T) -> U) -> U
```

example:

``` rust

fn main() {
    let arr = [2,2,2,2,2]
    let folded = arr.fold(0, |a, b| a + b);
    constrain folded == 10;
}

```

## reduce

Same as fold, but uses the first element as starting element.

```rust
fn reduce<T, N>(f: fn(T, T) -> T) -> T 
```

example:

```rust
fn main() {
    let arr = [2,2,2,2,2]
    let reduced = arr.reduce(|a, b| a + b);
    constrain reduced == 10;
}
```

## all

Returns true if all the elements satisfy the given predicate

```rust
fn all<T, N>(predicate: fn(T) -> bool) -> bool
```

example:

```rust
fn main() {
    let arr = [2,2,2,2,2]
    let all = arr.all(|a| a == 2);
    constrain all == true;
}
```

## any

Returns true if any of the elements satisfy the given predicate

```rust
fn any<T, N>(predicate: fn(T) -> bool) -> bool
```

example:

```rust
fn main() {
    let arr = [2,2,2,2,5]
    let any = arr.any(|a| a == 5);
    constrain any == true;
}

```

[^migrationNote]: Migration Note: These methods were previously free functions, called via `std::array::len()`. For the sake of ease of use and readability, these functions are now methods and the old syntax for them is now deprecated.
