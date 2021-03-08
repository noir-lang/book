# Breakdown

This section breaks down our hello world program in section _1.2_. We elaborate on the project structure and what the `prove` and `verify` commands did in the previous section, and usage of the `contract` command.

## Anatomy of a Nargo Project

Upon using the `new` command, Nargo will create a Noir project. 

Noir Projects have the following structure:

    - src
    - Prover.toml
    - Verifier.toml
    - Nargo.toml

_contract_ and _proofs_ directories will not be immediately visible until you create a contract or proof respectively.

### Source directory

This directory holds the source code for your Noir program.

Inside of the src directory will be a single file:

    - main.nr

#### main.nr

The main.nr file contains a `main` method, this method is the entry point into your Noir program. 

In our sample program, main.nr looks like this:

```
fn main(x : Field, y : Field) {
    constrain x != y;
}
```

The parameters `x` and `y` can be seen as the API for the program and must be supplied by the prover. Since neither `x` nor `y` is marked as public, the verifier does not supply any inputs, when verifying the proof. 

The prover supplies the values for `x` and `y` in the `Prover.toml` file.

#### Prover.toml

The Prover.toml file is a file which the prover uses to supply his witness values(both private and public). 

In our hello world program the Prover.toml file looks like this:

```toml
x = "5"
y = "10"
```

When the command `nargo prove my_proof` is executed, two processes happen:

- First, Noir creates a proof that `x` which holds the value of `5` and `y` which holds the value of `10` is not equal.This not equal constraint is due to the line `constrain x != y`.

> **Note:** We have not expanded on the meaning of the syntax `constrain x != y` as it is not the focus of this chapter.

- Second, Noir creates and stores the proof of this statement in the `proofs` directory and names the proof file `my_proof`. Opening this file will display the proof in hex format.

## Verifying a Proof

When the command `nargo verify my_proof` is executed, two processes happen:

- Noir checks in the `proofs` directory for a file called `my_proof`

- If that file is found, the proof's validity is checked.

> **Note:** The validity of the proof is linked to the current Noir program; if the program is changed and the verifier verifies the proof, it will fail because the proof is not valid for the _modified_ Noir program. 

## Contract

This directory holds the compiled _Ethereum_ contract for the current Noir program. The contract is not automatically compiled when the `prove` or `verify` command is ran. To compile execute the following:


> **Note:** At the time of pre-alpha, Nargo supports only one backend which is Aztec-Barretenberg. This backend only allows you to compile from a Noir program to an Ethereum contract. It is possible for Noir to compile to another smart contract platform as long as the backend supplies an implementation.  

```sh
$ nargo contract
```