# Noir Standard Library

Noir features a standard library with some ready-to-use, built-in structures. To use them, you should import the `std` library, like so:

``` rust

use dep::std;
```

You should then have these constructs available. Example:

``` rust
let data : [Field; 2] = [42, 42];
std::hash::pedersen(data);
```

## Field

After declaring a Field, you can use these common methods on it [^migrationNote]:

| Method   | Description                                                                                                                   | Example                        |
|:---------|-------------------------------------------------------------------------------------------------------------------------------|--------------------------------|--------------------------------|
|to_le_bits| Transforms into an array of bits, Little Endian | `field.to_le_bits()` |
|to_le_bytes| Transforms into an array of bytes, Little Endian | `field.to_le_bytes(byte_size)` |
|to_radix| Decomposes into a vector over the specificed base | `field.to_radix(radix_base, vector)`
|pow_32| Returns the value to the power of the specificied exponent | `field.to_pow(2)` |

## Array

For convenience, the STD provides some ready-to-use, common methods for arrays[^migrationNote]:

| Method   | Description                                                                                                                   | Example                        |
|:---------|-------------------------------------------------------------------------------------------------------------------------------|--------------------------------|--------------------------------|
| len      | Returns the length of an array                                                                                                | `array.len()`                  |
| sort | Sorts the array with a built-in function                                                                                           | `array.sort()`                 |
| sort_via | Sorts with a custom sorting function                                                                                          | `array.sort_via(|a, b| a < b)` |
| fold     | Applies a function to each element of the array, returning the final accumulated value. First parameter is the initial value. | `array.fold(0, |a, b| a < b)`  |
| reduce   | Same as fold, but uses the first element as starting element                                                                  | `array.reduce(|a, b| a < b)`   |
| all      | Returns true if all the elements satisfy the given predicate                                                                  | `array.all(|a, b| a < b)`      |
| any      | Returns true if any of the elements satisfy the given predicate                                                               | `array.any(|a, b| a < b)`      |

[^migrationNote]: Migration Note: These methods were previously used like `std::field::to_le_bits()`. For the sake of ease of use and readability, this syntax is now deprecated, and you should use the respective `impl` as suggested (`your_field_var.to_le_bits()`)

## Merkle Trees

Some constructs for merkle tree membership and root calculation are available.

| Method   | Description                                                                                                                   | Example                        | Obs                        |
|:---------|-------------------------------------------------------------------------------------------------------------------------------|--------------------------------|--------------------------------|
| check_membership      | Returns 1 if the specified leaf is at the given index on a tree                                                                                                | `merkle::check_membership(root, leaf, index, hashpath)`                  | Implementation provided by barretenberg |
| check_membership_in_noir      | Returns 1 if the specified leaf is at the given index on a tree                                                                                                | `merkle::check_membership_in_noir(root, leaf, index, hashpath)`                  | Computed in noir, so it works in all backends |
| compute_root_from_leaf      | Returns the root of the tree from the provided leaf and its hashpath, using pedersen hash                                                                                                | `merkle::compute_root_from_leaf(leaf, index, hashpath)`                  |

## Cryptographic primitives

Some cryptographic primitives are already developed and ready-to-use for any Noir project:

| Primitive                 | Description                                             | Example                        | Obs |
|:--------------------------|---------------------------------------------------------| ----                        | -----|
| sha512              | Sha512 hash                                             | `hash::sha512()`                        |
| sha256              | Sha256 hash                                             |`hash::sha256()`                        |
| blake2s             | Blake2 hash                                             |`hash::blake2s()`                        | Implementation provided by barretenberg |
| pedersen            | Pedersen hash                                           |`hash::pedersen()`                        | Implementation provided by barretenberg |
| mimc                | MiMC hash                                               |`hash::mimc()`                        |
| mimc_bn254          | MiMC hash with hardcoded parameters for the BN254 curve |`hash::mimc_bn254()`                        |
| fixed_base    | Scalar multiplication on a fixed base [^note]           |`scalar_mul::fixed_base()`                        | Implementation provided by barretenberg |
| verify_signature | Verifier for Schnorr signatures                         | `schnorr::verify_signature`                        | Implementation provided by barretenberg |
| verify_signature | Verifier for ECDSA Secp256k1 signatures                         | `ecdsa_secp256k1::verify_signature`                        | Implementation provided by barretenberg |

[^note]: Scalar multiplication over the embedded curve whose coordinates are defined by the configured noir field. For the BN254 scalar field, this is BabyJubJub or Grumpkin
