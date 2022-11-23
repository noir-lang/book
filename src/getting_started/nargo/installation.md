# Installation

## Setup

1. Install [Git] and [Rust].

   Optionally you can install [Noir VS Code extension] for syntax highlighting as well.

2. Download Noir's source code from Github by running:

   ```bash
   $ git clone git@github.com:noir-lang/noir.git
   ```

3. Change directory into the Nargo crate by running:

   ```bash
   $ cd noir/crates/nargo
   ```

[git]: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
[rust]: https://www.rust-lang.org/tools/install
[noir vs code extension]: https://marketplace.visualstudio.com/items?itemName=noir-lang.noir-programming-language-syntax-highlighter

There are then two approaches to proceed, differing in how the proving backend is installed:

## Option 1: WASM Executable Backend

**Platforms Supported:** Linux, macOS, Windows

4. Go into `nargo/Cargo.toml` and replace `aztec_backend = ...` with the following:

   ```
   aztec_backend = { optional = true, package = "barretenberg_wasm", git = "https://github.com/noir-lang/aztec_backend", rev = "fb42a54a04f3952f422e8fa4eff4f8eb2ca4e51b" }
   ```

## Option 2: Compile Backend from Source

**Platforms Supported:** Linux, macOS

The [barretenberg] proving backend is written in C++, hence compiling it from source would first require certain dependencies to be installed.

For macOS users, installing through [Homebrew] is highly recommended.

4. Install [CMake], [LLVM] and [OpenMP] by running:

   _macOS_

   ```bash
   $ brew install cmake llvm libomp
   ```

   _Linux_

   ```bash
   TBC
   ```

   <!---
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

[barretenberg]: https://github.com/AztecProtocol/aztec-connect/tree/master/barretenberg
[homebrew]: https://brew.sh/
[cmake]: https://cmake.org/install/
[llvm]: https://llvm.org/docs/GettingStarted.html
[openmp]: https://openmp.llvm.org/

## Continue with Installation

5. Install Nargo by running:

   ```bash
   $ cargo install --locked --path=.
   ```

6. Check if the installation was successful by running:

   ```
   $ nargo --help
   nargo 0.1
   Kevaundray Wedderburn <kevtheappdev@gmail.com>
   Noir's package manager

   USAGE:
      nargo [SUBCOMMAND]

   FLAGS:
      -h, --help       Prints help information
      -V, --version    Prints version information

   SUBCOMMANDS:
      build       Builds the constraint system
      compile     Compile the program and its secret execution trace into ACIR format
      contract    Creates the smart contract code for circuit
      gates       Counts the occurences of different gates in circuit
      help        Prints this message or the help of the given subcommand(s)
      new         Create a new binary project
      prove       Create proof for this program
      verify      Given a proof and a program, verify whether the proof is valid
   ```
