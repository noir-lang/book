# Commands

## `nargo help [subcommand]`

Prints the list of available commands or specific information of a subcommand.

_Arguments_

- `<subcommand>` - The subcommand whose help message to display

## `nargo new <package_name> [path]`

Creates a new Noir project.

_Arguments_

- `<package_name>` - Name of the package
- `[path]` - The path to save the new project

## `nargo check`

Generate the `Prover.toml` and `Verifier.toml` files for specifying prover and verifier in/output values of the Noir program respectively.

## `nargo execute`

Runs the Noir program and prints its return value.

- `<witness_name>` - The name of the witness

## `nargo prove <proof_name>`

Creates a proof for the program.

_Arguments_

- `<proof_name>` - The name of the proof

## `nargo verify <proof>`

Given a proof and a program, verify whether the proof is valid.

_Arguments_

- `<proof>` - The proof to verify

## `nargo codegen-verifier`

Generate a Solidity verifier smart contract for the program.

## `nargo preprocess <build_artifact>`

Generate proving and verification keys from a build artifact file.

## `nargo compile <circuit_name>`

Compile the program and its secret execution trace into a JSON build artifact file containing the ACIR representation, and the ABI of the circuit. This build artifact can then be used to generate and verify proofs.

_Arguments_

- `<circuit_name>` - The name of the circuit file

> The files compiled can be passed into a TypeScript project for proving and verification. See the [TypeScript](../typescript.md#proving-and-verifying-externally-compiled-files) section to learn more.
