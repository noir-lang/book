
# Field

After declaring a Field, you can use these common methods on it [^migrationNote]:

## to_le_bits

Transforms the field into an array of bits, Little Endian.

``` rust
fn to_le_bits(_x : Field, _bit_size: u32) -> [u1]
```

example:

``` rust
fn main(field : pub Field) {
    let t = field.to_le_bits(32);
    constrain t == t;
}
```

## to_le_bytes

Transforms into an array of bytes, Little Endian

``` rust
fn to_le_bits(_x : Field, _bit_size: u32) -> [u1]
```

example:

```rust
fn main(field : pub Field) {
    let t = field.to_le_bytes(4);
    constrain t == t;
}
```

## to_radix

Decomposes into a vector over the specificed base

```rust
fn to_radix(_x : Field, _radix: u32, _result_len: u32) -> [u8]
```

example:

```rust
fn main(field : pub Field) {
    let t = field.to_radix(256, 4);
    constrain t == t;
}
```

## pow_32

Returns the value to the power of the specificied exponent

```rust
fn pow_32(self, exponent: Field) -> Field
```

example:

```rust
// field = 2
fn main(field : pub Field) {
    let t = field.pow_32(4);
    constrain t == 16;
}
```
