# Hello, World

Now that we have installed Noir, it's time to make our first hello world program!

## Creating a Project Directory

Noir code can live anywhere on your computer. Lets create a Projects folder in the `Home` to house our Noir programs.

For Linux, macOS, and PowerShell on Windows, enter this in your terminal:

```sh
$ mkdir ~/projects
$ cd ~/projects
```

For Windwows CMD, enter this:

```sh
> mkdir "%USERPROFILE%\projects"
> cd /d "%USERPROFILE%\projects"
```

## Compiling Our First Project

Now that we are in the projects directory, enter the following command:

```sh
nargo new hello_world
```

We use the `new` command to create a new Noir project. This project will be located in the `hello_world` folder.

Now `cd` into the `hello_world` folder and enter this:

```
$ nargo build
```

Now that the project is built, we need to create a proof of correct execution. 
Edit the file `Prover.toml` with the following content:

```
x = "1"
y = "2"
```

and edit the `Verifier.toml` file with the following content:

```
y = "2"
setpub = []
```

Now you can run the proof generation and verification commands:
```
$ nargo prove my_proof
$ nargo verify my_proof
true
```

Congratulations, you have now created and verified a proof for your very first Noir program!

In the next section, we will go into more detail on exactly what just happened.
