# Noir Standard Library

Noir features a standard library with some ready-to-use, built-in structures. To use them, you should import the `std` library, like so:

``` rust

use dep::std;
```

You should then have these constructs available. For example, you can now call the `std::hash::pedersen` function like so:

``` rust
let data : [Field; 2] = [42, 42];
std::hash::pedersen(data);
```
