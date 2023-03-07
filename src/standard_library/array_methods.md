
# Array

For convenience, the STD provides some ready-to-use, common methods for arrays[^migrationNote]:

## len

Returns the length of an array

```rust
fn len(_array: Self) -> comptime Field
```

example

```rust
// arr = [42, 42]
fn main(arr : pub [Field; 2]) {
    let t = arr.len();
    constrain t == 2;
}
```

## sort

Sorts the array with a built-in function

```rust
fn sort(_array: Self) -> Self
```

example

```rust
// arr = [42, 32]
fn main(arr : pub [u32; 2]) {
    let t = arr.sort();
    constrain t == [32, 42];
}
```

## sort_via

Sorts the array with a custom sorting function

```rust
fn sort_via(mut a: Self, ordering: fn(T, T) -> bool) -> Self
```

example

```rust
// arr = [42, 32]
fn main(arr : pub [u32; 2]) {
    let t = arr.sort_via(|a, b| a < b);
    constrain t == [32, 42]; // verifies

    let t = arr.sort_via(|a, b| a > b);
    constrain t == [32, 42]; // does not verify

}
```

## fold

Applies a function to each element of the array, returning the final accumulated value. First parameter is the initial value

```rust
fn fold<U>(self, mut accumulator: U, f: fn(U, T) -> U) -> U
```

example:

``` rust

// arr = [2,2,2,2,2]
fn main(arr : [Field; 5]) {
    let folded = arr.fold(0, |a, b| a + b);
    constrain folded == 10;
}

```

## reduce

Same as fold, but uses the first element as starting element

```rust
fn reduce(self, f: fn(T, T) -> T) -> T 
```

example:

```rust
// arr = [2,2,2,2,2]
fn main(arr : [Field; 5]) {
    let reduced = arr.reduce(|a, b| a + b);
    constrain reduced == 10;
}
```

## all

Returns true if all the elements satisfy the given predicate

```rust
fn all(self, predicate: fn(T) -> bool) -> bool
```

example:

```rust
// arr = [2,2,2,2,2]
fn main(arr : [Field; 5]) {
    let all = arr.all(|a| a == 2);
    constrain all == true;
}
```

## any

Returns true if any of the elements satisfy the given predicate

```rust
fn any(self, predicate: fn(T) -> bool) -> bool
```

example:

```rust
// arr = [2,2,2,2,5]
fn main(arr : [Field; 5]) {
    let any = arr.any(|a| a == 5);
    constrain any == true;
}

```

[^migrationNote]: Migration Note: These methods were previously free functions, called via `std::field::to_le_bits(my_field)`. For the sake of ease of use and readability, these functions are now methods and the old syntax for them is now deprecated.
