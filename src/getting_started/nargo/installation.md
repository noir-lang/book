# Installation

Ways to install Nargo are described in ascending order of complexity below.

## Option 1: Binaries

**Platforms Supported:** macOS, Windows

1. Create a directory to host the binary. For example, run:

   ```bash
   mkdir ~/nargo
   ```

2. Download the binary package from GitHub into the directory created in Step 1:

   - [macOS (Apple Silicon)](https://github.com/kobyhallx/build-noir/suites/9553357751/artifacts/454490397)
   - [macOS (Intel)](https://github.com/kobyhallx/build-noir/suites/9553357751/artifacts/454490398)
   - [Windows](https://github.com/kobyhallx/build-noir/suites/9553445421/artifacts/454485541)

3. Paste and run the following in the terminal to extract and expose the binary:

   _macOS (Apple Silicon)_

   ```bash
   cd ~/nargo && \
   unzip nargo-aarch64-apple-darwin.zip && \
   chmod +x nargo && \
   echo '\nexport PATH=$PATH:~/nargo' >> ~/.zshrc && \
   source ~/.zshrc
   ```

   To Test: _macOS (Intel)_

   ```bash
   cd ~/nargo && \
   unzip nargo-x86_64-apple-darwin.zip && \
   chmod +x nargo && \
   echo '\nexport PATH=$PATH:~/nargo' >> ~/.zshrc && \
   source ~/.zshrc
   ```

   To Test: _Windows_

   ```bash
   cd ~/nargo && \
   unzip nargo-x86_64-pc-windows-msvc.zip && \
   setx PATH "~/nargo;%PATH%"
   ```

4. Check if the installation was successful by running `nargo --help`.

   If you are prompted with an OS alert, follow the instructions to grant the necessary permissions:

   - _macOS_

     Proceed with "Show in Finder", then right-click and open the nargo executable. You can close the new terminal that popped up and `nargo` should now be accessible.

   For a successful installation, you should see something similar to the following after running the command:

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

Optionally you can also install [Noir VS Code extension] for syntax highlighting.

## Option 2: Compile from Source

**Platforms Supported:** Linux, macOS (and Windows with Option 2.1)

### Setup

1. Install [Git] and [Rust]. Optionally you can also install [Noir VS Code extension] for syntax highlighting.

2. Download Noir's source code from Github by running:

   ```bash
   git clone git@github.com:noir-lang/noir.git
   ```

3. Change directory into the Nargo crate by running:

   ```bash
   cd noir/crates/nargo
   ```

[git]: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
[rust]: https://www.rust-lang.org/tools/install
[noir vs code extension]: https://marketplace.visualstudio.com/items?itemName=noir-lang.noir-programming-language-syntax-highlighter

There are then two approaches to proceed, differing in how the proving backend is installed:

### Option 2.1: WASM Executable Backend

**Platforms Supported:** Linux, macOS, Windows

4. Go into `nargo/Cargo.toml` and replace `aztec_backend = ...` with the following:

   ```
   aztec_backend = { optional = true, package = "barretenberg_wasm", git = "https://github.com/noir-lang/aztec_backend", rev = "fb42a54a04f3952f422e8fa4eff4f8eb2ca4e51b" }
   ```

### Option 2.2: Compile Backend from Source

**Platforms Supported:** Linux, macOS

The [barretenberg] proving backend is written in C++, hence compiling it from source would first require certain dependencies to be installed.

For macOS users, installing through [Homebrew] is highly recommended.

4. Install [CMake], [LLVM] and [OpenMP] by running:

   _macOS_

   ```bash
   brew install cmake llvm libomp
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

### Continue with Installation

5. Install Nargo by running:

   ```bash
   cargo install --locked --path=.
   ```

6. Check if the installation was successful by running `nargo --help`:

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
