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

## Creating a Noir Sample Program

Now that we are in the projects directory, enter the following command:

```sh
noir new hello_world
```

We use the `new` command to create a new Noir project. This project will be located in the `hello_world` folder.

Now `cd` into the `hello_world` folder and enter this:

```
$ noir prove my_proof
$ noir verify my_proof
true
```

Congratulations, you have now created and verified your very first Noir program! In the next section, we will go into more detail on exactly what just happened.