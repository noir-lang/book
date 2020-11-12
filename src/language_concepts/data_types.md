# Data types

There are two subsets of data types that each datatype will fall into; fundamental and compound.

A **fundamental type** is a data type which is defined in the core language. This is not specific to Noir. Examples in modern programming languages such as Rust are u32, usize and char. 

A **compound type** is a type in the core language which must be defined using another type. Examples in modern programming languages are arrays, tuples and functions.

Although each value in a constraint system is fundamentally a field element, we add a layer of abstraction over this; each value can be _concealed_ or _revealed_. 

A **concealed value** is known only to the Prover, while, a **revealed value** is known by the Prover and Verifier. All concealed and revealed data types are _fundamental_ types.

## Concealed Types

Concealed types are usually referred to as witness values.

### Witness Type

A Witness type is the default concealed type.

### Integer Type

An integer type is a witness type which has been constrained using a range constraint. The Noir front-end currently supports arbitrary sized integer types.

> **Note:** The Aztec backend only supports even sized integer types currently, so while using the Aztec backend, only even sized integer types such as u32, u48 will produce proofs.

## Revealed Types

### Constants

A constant type is a value that does not change per circuit instance. This is different to a concealed type which changes per proof. If a constant type that is being used in your program in changed, then your circuit will also change.

### Public Types

A public type is a value that may change per circuit instance. Unlike Constants, changing a public value will not change the circuit 