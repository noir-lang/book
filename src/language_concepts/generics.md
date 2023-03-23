# Generics

Generics allow you to use the same functions with multiple different concrete data types. You can read more about the concept of generics in the Rust documentation [here](https://doc.rust-lang.org/book/ch10-01-syntax.html).

For example, you may need functions that add `u8` and `u32` integers. Instead of having to write two functions that do the same thing, you can write one function that works for both using generics.

```rust noplaypen
fn add<T>(a : T, b : T) -> T {
  return a + b
}
```

This concept also works with implementations of structs. For example

```rust noplaypen
struct BigInt<N> {
    limbs: [u32; N],
}

impl<N> BigInt<N> {
    // `N` is in scope of all methods in the impl
    fn first(first: BigInt<N>, second: BigInt<N>) -> Self {
        constrain first.limbs != second.limbs;
        first
    }

    fn second(first: BigInt<N>, second: Self) -> Self {
        constrain first.limbs != second.limbs;
        second
    }
}
```

You can see an example of generics in the tests [here](https://github.com/noir-lang/noir/blob/master/crates/nargo/tests/test_data/generics/src/main.nr).
