# Commands

## `nargo help [subcommand]`

Prints the list of available commands or specific information of a subcommand.

_Arguments_

- `<subcommand>` - The subcommand whose help message to display

## `nargo new <package_name> [path]`

Creates a new Noir project.

_Arguments_

- `<package_name>` - Name of the package
- `<path>` - The path to save the new project

## `nargo build`

Generate the `toml` files for specifying in/output values of the Noir program.

## `nargo prove <proof_name>`

Creates a proof for the program.

_Arguments_

- `<proof_name>` - The name of the proof

## `nargo verify <proof>`

Given a proof and a program, verify whether the proof is valid.

_Arguments_

- `<proof>` - The proof to verify

## `nargo contract`

Generate a smart contract verifier for the program.

## `nargo compile <circuit_name>`

Compile the program and its secret execution trace into Abstract Circuit Intermediate Representation (ACIR) format.

_Arguments_

- `<circuit_name>` - The name of the ACIR file
