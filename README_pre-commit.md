# Pre-commit
It is a multi-language package manager for pre-commit hooks. You specify a list of hooks you want and pre-commit manages the installation and execution of any hook written in any language before every commit.
Git hook scripts are useful for identifying simple issues before submission to code review.
**This is only a local tool. When commit from git page this is not used**

# Usage
Command:
```console
$ pre-commit install --hook-type commit-msg
```
Creates a git hook script in .git/hooks/commit-msg to be called before a commit.
Once you have pre-commit installed, adding pre-commit plugins to your project is done with the .pre-commit-config.yaml configuration file.
Add a file called .pre-commit-config.yaml to the root of your project. The pre-commit config file describes what repositories and hooks are installed.
"entry" is the command to be executed. In this case calls "cz check --commit-msg-file" which calls cz checker for the commig message when execute command "git commit"
See [README_commitizen.md](README_commitizen.md)

# More info
see [https://pre-commit.com/](https://pre-commit.com/)
