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

## `nargo prove <proof_name>`

Creates a proof for the program.

_Arguments_

- `<proof_name>` - The name of the proof

## `nargo verify <proof>`

Given a proof and a program, verify whether the proof is valid.

_Arguments_

- `<proof>` - The proof to verify

## `nargo contract`

Generate a Solidity smart contract verifier for the program.

## `nargo compile [FLAGS] <circuit_name>`

Compile the program and its secret execution trace into [ACIR](../../acir.md) format.

_Arguments_

- `<circuit_name>` - The name of the ACIR file
- `[FLAGS]` - Add `--witness` to compile the witness file as well

_Usage_

Running the command would create a new folder `build` with the compiled `<circuit_name>.acir` file in your project directory.

To also compile a witness file, fill in the values in `Prover.toml` generated from `nargo check` and run the command with the `--witness` flag. A `<circuit_name>.tr` file would be compiled in the `build` folder.

> **Info:** The `.acir` file is the ACIR of your Noir program, and the `.tr` file is the witness file. The witness file can be considered as program inputs parsed for your program's ACIR.
>
> The files compiled can be passed into a TypeScript project for proving and verification. See the [TypeScript](../typescript.md#proving-and-verifying-externally-compiled-files) section to learn more.
