
# Field

After declaring a Field, you can use these common methods on it [^migrationNote]:

## to_le_bits

Transforms the field into an array of bits, Little Endian.

``` rust
fn to_le_bits<N>(_x : Field, _bit_size: u32) -> [u1; N]
```

example:

``` rust
fn main() {
    let field = 2
    let bits = field.to_le_bits(32);
}
```

## to_le_bytes

Transforms into an array of bytes, Little Endian

``` rust
fn to_le_bytes(_x : Field, byte_size: u32) -> [u8]
```

example:

```rust
fn main() {
    let field = 2
    let bytes = field.to_le_bytes(4);
}
```

## to_le_radix

Decomposes into a vector over the specificed base, Little Endian

```rust
fn to_le_radix(_x : Field, _radix: u32, _result_len: u32) -> [u8]
```

example:

```rust
fn main() {
    let field = 2
    let radix = field.to_le_radix(256, 4);
}
```

## to_be_radix

Decomposes into a vector over the specificed base, Big Endian

```rust
fn to_be_radix(_x : Field, _radix: u32, _result_len: u32) -> [u8]
```

example:

```rust
fn main() {
    let field = 2
    let radix = field.to_be_radix(256, 4);
}
```

## pow_32

Returns the value to the power of the specificied exponent

```rust
fn pow_32(self, exponent: Field) -> Field
```

example:

```rust
fn main() {
    let field = 2
    let pow = field.pow_32(4);
    constrain pow == 16;
}
```
