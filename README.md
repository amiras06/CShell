# C Shell

## Description

SimpleCShell is a basic shell implementation written in C. It allows users to execute commands in a terminal-like environment, supporting both simple commands (such as `ls` and `cd`) and complex commands using pipes and redirections. This project is designed to help understand command parsing, process creation, and inter-process communication in Unix-like systems.

## Features

- **Command Execution:**  
  Execute basic commands like `ls`, `cd`, and more.

- **Pipes and Redirections:**  
  Chain commands using pipes (`|`) and perform input/output redirection (`>`, `<`).

- **Custom Shell Prompt:**  
  Display a user-friendly prompt for entering commands.

- **Error Handling:**  
  Basic error reporting for invalid commands or syntax errors.

## Requirements

- A C compiler (e.g., `gcc`)
- Unix/Linux environment

## Compilation

To compile the project, open a terminal in the project's root directory and run:

```bash
make
```

For more details on the project structure and design decisions, please refer to the [architecture.md](architecture.md) file.
