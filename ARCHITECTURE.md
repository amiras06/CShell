## Detailed Implementation Overview

Our project is composed of several files:

- **commands.c:**  
  This file contains most of the functionality related to executing both internal and external commands. For the `-L` option of `pwd` and `cd`, we used the environment variable `getenv()` because it follows symbolic links, unlike the `-P` option which does not. Therefore, we used the `getcwd()` function. In the special case of `cd` when the provided path does not make sense, our solution is to construct a new path by simplifying the input path; if the simplified path is valid, we change to that directory, otherwise we perform a physical interpretation of the path. For external commands, we use an array of strings to store the command name along with its various parameters and options, and then execute it using `execvp()`. For the `exit` command, a global variable `return_value` stores the return value of the last executed command and is also used when displaying the prompt.

- **star.c:**  
  This file handles pattern expansion for patterns containing `*` and `**`. We used a data structure called `TreeNode` to represent the file hierarchy. We modified some functions found online (such as `creeNode`, `freeTree`, and `TraversDFS`) to suit our needs. The function `get_match_dirs` retrieves all directories and files that match a given pattern containing only `*`. It checks if each element matches the pattern using the `match` function, and if so, adds it to the hierarchy. The function `get_arborescence` recursively traverses a directory and its subdirectories, adding all directory and file names to a tree. Using this tree, the function `get_paths_dbl_star` finds all paths that match the given pattern, effectively resolving the `**` pattern issue.

- **redirection.c:**  
  This file is used to manage the various possible redirections. First, a function determines which type of redirection should be executed (standard input, standard output, or standard error redirection). Based on the result, another function identifies the exact redirection type (e.g., with or without overwriting, appending, etc.), and finally, the redirections are performed using `dup2`.

- **Pipeline Execution:**  
  Pipelines are handled separately from `redirection.c` because the function that executes them uses the `launch` function from the main file `slash.c`. Our overall approach is to first split the pipeline into two parts: the first part is the very first command in the pipeline, and the second part contains the rest. We then call the `launch` function (see its description in `slash.c`), which re-invokes the pipeline execution with the second part of the pipeline. This process continues until the entire pipeline has been executed, using `fork`, pipes, and redirection of both standard output and standard input.

- **Signal Handling:**  
  In the `main` function (located in `slash.c`), we set up a `SIG_IGN` handler for the `SIGINT` and `SIGTERM` signals. When an external command is executed, we reset the handler to `SIG_DFL` for these two signals in the child process so that they are not ignored.
