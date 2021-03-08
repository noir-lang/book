# TornadoCash

Let's show an example of the TornadoCash circuit in Noir.

```rust,noplaypen
fn main(message : [62]u8, index : Field, hashpath : [40]Field, root : Field) {

    priv leaf = std::hash::hash_to_field(message);

    priv is_member = std::merkle::check_membership(root, leaf, index, hashpath);

    constrain is_member == 1;
}
```

The TornadoCash circuit involves a merkle membership proof that a leaf is in a merkle tree.

The above code uses the noir standard library to call both of the aforementioned components.

```rust,noplaypen
   priv leaf = std::hash::hash_to_field(message);
```

The message is hashed using `hash_to_field`. The specific hash function that is being used is chosen by the backend. The only requirement is that this hash function can heuristically be used as a random oracle. If only collision resistance is needed, then one can call `std::hash::pedersen` instead.

```rust,noplaypen
    priv is_member = std::merkle::check_membership(root, leaf, index, hashpath);
```

The leaf is then passed to a check_membership proof with the root, index and hashpath. `is_member` returns 1 if the leaf is a member of the merkle tree with the specified root, at the given index.

>Note: It is possible to re-implement the merkle tree implementation without standard library. However, for most usecases, it is enough. In general, the standard library will always opt to be as conservative as possible, while striking a balance between efficiency.

An example, the merkle membership proof, only requires a hash function that has collision resistance, hence a hash function like Pedersen is allowed, which in most cases is more efficient than the even more conservative sha256. 

```rust,noplaypen
    constrain is_member == 1;
```

This last line, constrains the variable to be equal to 1. If 1 was changed to 0, this would create a proof that the leaf was not present at that specific index for that specific root. _Importantly, it would not prove that this leaf was not in the merkle tree._ 

