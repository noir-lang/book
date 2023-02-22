# Noir Standard Library

Noir features a standard library with some ready-to-use, built-in structures.

## Arrays

For convenience, the STD provides some ready-to-use, common methods for arrays.

## Merkle Trees

Some constructs for merkle tree membership and root calculation are available.

## Cryptographic primitives.

Some cryptographic primitives are already developed and ready-to-use for any Noir project. To use them, just import the `std` library at the top of your file, like so:

```
use dep::std;
```

You should then have all the primitives available by calling `std::`. Example:

```
let data : [Field; 2] = [42, 42];
std::hash::pedersen(data);
```

## Existent cryptographic primitives

| Primitive       | Description                                                |
| :--             | :-----------------:                                        |
|  hash::sha512              | Sha512 hash                         |
|  hash::sha256              | Sha256 hash                         |
|  hash::blake2s              | Blake2 hash                           |
|  hash::pedersen              | Pedersen hash                          |
|  hash::mimc              | MiMC hash                          |
|  hash::mimc_bn254              | MiMC hash with hardcoded parameters for the BN254 curve                          |
|  scalar_mul::fixed_base              | Scalar multiplication on a fixed base [^note]                          |
|  schnorr::verify_signature              | Verifier for Schnorr signatures                          |

[^note]: Scalar multiplication over the embedded curve whose coordinates are defined by the configured noir field. For the BN254 scalar field, this is BabyJubJub or Grumpkin
