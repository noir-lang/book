# Generics

Generics allow you to use the same functions with multiple different concrete data types. You can read more about the concept of generics in the Rust documentation [here](https://doc.rust-lang.org/book/ch10-01-syntax.html).

Here is a trivial example showing the identity function that supports any type. In Rust, it is common to refer to the most general type as `T`. We follow the same convention in Noir.

```rust noplaypen
fn id<T>(x: T) -> T  {
    x
}
```

## Arbitrary length arrays

This concept is more useful for more specific types, like number generics. These can be used to define a function that iterates over an array of arbitrary length.

```rust noplaypen
struct RepeatedValue<T> {
    value: T,
    count: comptime Field,
}

impl<T> RepeatedValue<T> {
    fn new(value: T) -> Self {
        Self { value, count: 1 }
    }

    fn increment(mut repeated: Self) -> Self {
        repeated.count += 1;
        repeated
    }

    fn print(self) {
        for _i in 0 .. self.count {
            dep::std::println(self.value);
        }
    }
}

fn main() {
    let mut repeated = RepeatedValue::new("Hello!");
    repeated = repeated.increment();
    repeated.print();
}
```

The `print` function will print `Hello!` an arbitrary number of times, twice in this case.

## Function Generics

It can also be useful to create generic functions that will work over all types, `T`.

For example, how can we write a generic equality function for arrays of any type, `T`?

```rust noplaypen
fn array_eq<T, N>(array1: [T; N], array2: [T; N], elem_eq: fn(T, T) -> bool) -> bool {
    if array1.len() != array2.len() {
        false
    } else {
        let mut result = true;
        for i in 0 .. array1.len() {
            result &= elem_eq(array1[i], array2[i]);
        }
        result
    }
}

fn main() {
    constrain array_eq([1, 2, 3], [1, 2, 3], |a, b| a == b);

    // We can use array_eq even for arrays of structs, as long as we have
    // an equality function for these structs we can pass in
    let array = [MyStruct::new(), MyStruct::new()];
    constrain array_eq(array, array, MyStruct::eq);
}
```

You can see an example of generics in the tests [here](https://github.com/noir-lang/noir/blob/master/crates/nargo/tests/test_data/generics/src/main.nr).
