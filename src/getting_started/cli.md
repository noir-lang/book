# Command Line Tool: nargo

`nargo` is a command line tool for interacting with Noir programs (e.g. compiling, proving, verifying and more).

Alternatively, if you intend to perform the same interactions in TypeScript, you can skip the installations below.

## Setup

1. Install [Rust](https://www.rust-lang.org/tools/install)

2. Download Noir's source code from Github by running:

   ```bash
   $ git clone git@github.com:noir-lang/noir.git
   ```

3. Change directory into the nargo crate by running:

   ```bash
   $ cd noir/crates/nargo
   ```

There are then two approaches to proceed, differing in how the proving backend is installed:

## Option 1: WASM Executable Backend

**Platforms Supported:** Linux, macOS, Windows

4. Go into `nargo/Cargo.toml` and replace `aztec_backend = ...` with the following:

   ```
   aztec_backend = { optional = true, git = "https://github.com/noir-lang/aztec_backend", features = ["wasm-base"] , default-features = false }
   ```

> **Note:** `nargo contract` has not been implemented yet for _wasm-base_ `nargo` installations.

## Option 2: Compile Backend from Source

**Platforms Supported:** Linux, macOS

The [barretenberg] proving backend is written in C++, hence compiling it from source would first require certain dependencies to be installed.

For macOS users, installing [Homebrew] is highly recommended.

4. Install [CMake], [LLVM] and [OpenMP] by running:

   <!---
   TODO: Supplement Linux scripts.

   Linux's command for openMP from barretenberg's GitHub README:

   ```bash
   RUN git clone -b release/10.x --depth 1 https://github.com/llvm/llvm-project.git \
   && cd llvm-project && mkdir build-openmp && cd build-openmp \
   && cmake ../openmp -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ -DLIBOMP_ENABLE_SHARED=OFF \
   && make -j$(nproc) \
   && make install \
   && cd ../.. && rm -rf llvm-project
   ```
   --->

   _macOS_

   ```bash
   $ brew install cmake llvm libomp
   ```

[barretenberg]: https://github.com/AztecProtocol/aztec-connect/tree/master/barretenberg
[homebrew]: https://brew.sh/
[cmake]: https://cmake.org/install/
[llvm]: https://llvm.org/docs/GettingStarted.html
[openmp]: https://openmp.llvm.org/

## Continue with Installation

5. Install nargo by running:

   ```bash
   $ cargo install --locked --path=.
   ```

6. Check if the installation was successful by running:

   ```bash
   $ nargo help
   ```
