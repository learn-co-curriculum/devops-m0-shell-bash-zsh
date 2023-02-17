# Shells Configuration and Environment Variables

## Learning goals

- Understand the differences between `bash`, `zsh`, and `sh`
- Understand basic shell configuration
- Learn what the environmtal variables and `PATH` are and what they are used for

## Introduction

As we explored in the previous chapters, shells provide us with a way of interacting with the operating system. Given how ubiquitous their usage is in both development and IT, it's only natural that there are various offerings available, each with their own strengths and weaknesses. In this lesson we'll take a look at the most popular options, as well as how you can go about configuring them.

- **`sh`**: Simple and basic shell that is the ancestor of most modern shells, being compatible with almost all *Unix*-like systems. It lacks a lot of the more advanced features of `bash` and `zsh`.
- **`bash`**: The most commonly used shell in *Linux*, also compatible with most open-source systems in the same way `sh` is. It extends on `sh` by adding better and more ergonomic scripting functionality, as well as more built-in commands. `bash` is what we focus on in this course, and what the default shell is on most *Linux* distributions.
- **`zsh`**: A powerful shell designed for interaction; it builds *on top* of `bash` to provide more ergonomic features, like better auto-complete, theming, customization, etc. `zsh` is popular among developers who use the shell every day on their own computers, preferring its advanced customization options and ergonomics.

## Configuration

It is extremely common for users to customize their shell; you can change various aspects, such as the keybinds, environment variables, themes and colors, etc. 

To customize your shell, you can create/edit its specific shell initialization script. In the case of `bash`, you can find it (or create it) in `~/.bashrc`. This file is simply a bash script that gets ran every time you start your shell.

So if for example, you make your `~/.bashrc` resemble something like:

```bash
echo "Shell started!"
```

Every time you start your shell, it will output `Shell started!` at the top.

Since the script only gets ran when the shell gets initialized, if you make changes and want to apply them to the currently active shell, you can run the `source ~/.bashrc` command, which will reinitalize your shell with the new `.bashrc` file. Keep in mind since this file is located in your home directory (`~`), if you login as a different user, a different initialization script will be used. You can set system-wide initialization scripts, but this varies depending on what operating system distribution you are using.

## Environment Variables

One of the most common, if not *the* most common customization users apply to their shell, are the addition/modification of *environment variables*.

An **environment variable** is essentially the same thing as a standard variable in shell scripting, with the notable difference that environment variables keep their data and become accessible by other processes and programs. They are a fundamental part of the system and provide ways to store configuration settings and all kinds of information that can be accessed by other programs/scripts.

In order to set an environment variable, you just define the variable using the `export` modifier, e.g: `export NAME="Joe"`. You can run this command straight in the shell to define the environment variable for the lifetime of that shell, or add it as a line in the initialization script (`.bashrc`).

To view all the currently defined environment variables, you can run the `env` or `printenv` command. 

Once an environment variable is defined, any script or program that tries to use it will have access to it. For instance, you could write a script that checks if an environment variable is set, and if it is, use it later on.

You can also print the value of any environment variable using `echo`, e.g: `echo $NAME`.

> **Note:** Conventionally, environment variables are defined using all caps. For example, NAME, PATH, DATE_OF_BIRTH, etc.

## PATH

The `PATH` variable is an environment variable present in most operating systems in order to make their programs/executables available to the shell without having to specify the literal location of the program/executable.

For example, if you have a program called `calculator` and it exists in the `/home/joe/Programs/calculator` directory, every time you want to run the program, unless you're in the directory already, you have to type the entire path out (e.g. `/home/joe/Programs/calculator 3+5`). If instead you wish to be able to run `calculator 3+5`, you can add the `/home/joe/Programs` directory to the `PATH` variable. This is why programs located in the `/bin` and other system folders don't need the full path specified.

The `PATH` variable is simply a string of text containing a list of directories, separated by a colon (`:`). You can run `echo $PATH` to get a list of the current directories that exist in it.

If you want to edit the variable to add a new directory, all you need to do is set it in your `.bashrc`:

```bash
export PATH="/path/to/directory:$PATH"
```

## Conclusion

Understanding how `PATH` and environment variables work is crucial for a lot of the software development process, especially when it comes to automating development and deployment. While some of the other uses for environment variables might seem a bit unclear right now, you will gain insight as to how useful they are in the upcoming modules. 
