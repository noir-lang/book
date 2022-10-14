# TypeScript

Interactions with Noir programs can also be performed in TypeScript, which can come in handy when writing tests or when working in TypeScript-based projects like [Hardhat].

The following sections use the [_Standard Noir Example_] as an example to dissect a typical Noir workflow in TypeScript, with specific focus on its:

- Test script [`1_mul.ts`]
- Noir program [main.nr]
- Verifier contract generator script [generate_sol_verifier.ts]

[Hardhat]: https://hardhat.org/
[_Standard Noir Example_]: https://github.com/vezenovm/basic_mul_noir_example
[`1_mul.ts`]: https://github.com/vezenovm/basic_mul_noir_example/blob/master/test/1_mul.ts
[main.nr]: https://github.com/vezenovm/basic_mul_noir_example/blob/master/circuits/src/main.nr
[generate_sol_verifier.ts]: https://github.com/vezenovm/basic_mul_noir_example/blob/master/scripts/generate_sol_verifier.ts

## Setup

Install Noir dependencies in your project by running:

```bash
$ yarn add @noir-lang/noir_wasm @noir-lang/barretenberg @noir-lang/aztec_backend
```

And import the applicable functions into your TypeScript file by adding:

```ts
// 1_mul.ts
import { compile, acir_from_bytes } from '@noir-lang/noir_wasm';
import { setup_generic_prover_and_verifier, create_proof, verify_proof, create_proof_with_witness } from '@noir-lang/barretenberg/dest/client_proofs';
import { packed_witness_to_witness, serialise_public_inputs, compute_witnesses } from '@noir-lang/aztec_backend';
```

## Compiling

To begin proving and verifying a Noir program, it first needs to be compiled by calling `noir_wasm`'s `compile` function:

```ts
// 1_mul.ts
const compiled_program = compile(path.resolve(__dirname, "../circuits/src/main.nr"));
```

The `compiled_program` returned by the function contains the Abstract Circuit Intermediate Representation (ACIR) and the Application Binary Interface (ABI) of your Noir program. They shall be stored for proving your program later:

```ts
// 1_mul.ts
let acir = compiled_program.circuit;
const abi = compiled_program.abi;
```

## Specifying Inputs

Having obtained the compiled program, the program inputs shall then be specified in its ABI.

_Standard Noir Example_ is a program that multiplies input `x` with input `y` and returns the result:

```noir
# main.nr
fn main(x: u32, y: pub u32) -> pub u32 {
    let z = x * y;
    z
}
```

Hence, one valid scenario for proving could be `x = 3`, `y = 4` and `return = 12`:

```ts
// 1_mul.ts
abi.x = 3;
abi.y = 4;
abi.return = 12;
```

> **Note:** Return values are also required to be specified, as they are merely syntax sugar of inputs with equality constraints.

## Initializing Prover & Verifier

Prior to proving and verifying, the prover and verifier have to first be initialized by calling `barretenberg`'s `setup_generic_prover_and_verifier` with your Noir program's ACIR:

```ts
// 1_mul.ts
let [prover, verifier] = await setup_generic_prover_and_verifier(acir);
```

## Proving

The Noir program can then be executed and proved by calling `barretenberg`'s `create_proof` function:

```ts
// 1_mul.ts
const proof = await create_proof(prover, acir, abi);
```

## Verifying

The `proof` obtained can be verified by calling `barretenberg`'s `verify_proof` function:

```ts
// 1_mul.ts
const verified = await verify_proof(verifier, proof);
```

The function should return `true` if the entire process is working as intended, which can be asserted if you are writing a test script:

```ts
// 1_mul.ts
expect(verified).eq(true);
```

## Verifying with Smart Contract

Alternatively, a verifier smart contract can be generated in TypeScript as well:

```ts
// generate_sol_verifier.ts
import { writeFileSync } from 'fs';

...

const sc = verifier.SmartContract();
syncWriteFile("../contracts/plonk_vk.sol", sc);

...

function syncWriteFile(filename: string, data: any) {
    writeFileSync(join(__dirname, filename), data, {
      flag: 'w',
    });
}
```

Which can then be used to verify Noir proofs: 

```ts
// 1_mul.ts
import { ethers } from "hardhat";
import { Contract, ContractFactory, utils } from 'ethers';

...

// Deploy verifier contract
let Verifier: ContractFactory;
let verifierContract: Contract;

before(async () => {
    Verifier = await ethers.getContractFactory("TurboVerifier");
    verifierContract = await Verifier.deploy();
});

...

const sc_verified = await verifierContract.verify(proof);
expect(sc_verified).eq(true)
```

For more inspiration on ways to interact with Noir programs in TypeScript, see the full scripts [`1_mul.ts` of _Standard Noir Example_] and [`mm.ts` of _Mastermind in Noir_].

[`1_mul.ts` of _Standard Noir Example_]: https://github.com/vezenovm/basic_mul_noir_example/blob/master/test/1_mul.ts
[`mm.ts` of _Mastermind in Noir_]: https://github.com/vezenovm/mastermind-noir/blob/master/test/mm.ts