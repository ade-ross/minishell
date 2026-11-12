# minishell

A small Bash-like shell written in C for the 42 school curriculum. It reads a line, parses it, and runs the commands the way a real shell would, with pipes, redirections, quoting, environment variables and its own builtins.

## Features

- **Prompt** with line editing and history (GNU readline)
- **Quoting:** single quotes keep everything literal, double quotes allow `$` expansion
- **Variables:** `$VAR` and `$?` (exit status of the last command)
- **Pipes:** `cmd1 | cmd2 | cmd3`
- **Redirections:** `<`, `>`, `>>`, and here-documents with `<<`
- **Builtins:** `echo`, `cd`, `pwd`, `export`, `unset`, `env`, `exit`
- **External commands** found through `PATH` or run by relative or absolute path
- **Signals:** `Ctrl-C` and `Ctrl-\` are handled, including while a here-document is being read

## How it works

Each line goes through the same steps: read it, split it into tokens while respecting quotes, expand variables, build a list of commands with their redirections, then run it. Commands run in child processes created with `fork`, with `pipe` and `dup2` wiring the stages of a pipeline together and `execve` launching external programs.

## Build and run

You need a C compiler, `make` and the readline development package (on Debian or Ubuntu: `sudo apt install libreadline-dev`).

```bash
make
./minishell
```

```
minishell> echo hello | tr a-z A-Z
HELLO
minishell> export X=42
minishell> echo $X
42
```

## Authors

Built by Alessandro De Rossi and Mohamed Shahein ([Elephantinho](https://github.com/Elephantinho)) at 42 Florence.
