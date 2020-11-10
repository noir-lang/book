# Breakdown

## Anatomy of a Noir Project

Upon using the `new` command, Noir will create a Noir project. 

Noir Projects have the following structure:

    - bin
    - contract 
    - proofs

### Bin directory

This directory holds the source code for your Noir program. In future releases, this will be renamed to `src`.

Inside of the bin directory will be two files:

    - main.noir 
    - input.toml

#### main.noir

Noir currently does not support libraries. The main.noir file contains a `main` method, this method is the entry point into your Noir program. 

In our sample program, main.noir looks like this:

```
   fn main(x : Witness, y : Witness) {
        constrain x != y;
    }
```

The parameters `x` and `y` can be seen as the API for the program and must be supplied by the prover. These are supplied in the `input.toml` file.

### input.toml

The input.toml file is a file which the prover uses to input his witness values. In the hello world program the toml file looks like this:

```toml
        x = "5"
        y = "10"
```

When the command `noir prove my_proof` is executed, two processes happen. 

- First Noir creates a proof that `x` which holds the value of `5` and `y` which holds the value of `10` is not equal.This not equal constraint is due to the line `constrain x != y`.
- Then noir stores this proof in the directory `proofs` and names the proof `my_proof`.