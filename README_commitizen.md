## Commitizen

# Usage
You have 2 ways of use:
    - Use "cz c" command which is an inquirer to fill all fields necessary for a correct commit message and then checks the message using commitizen following definition of file cz.json
    - Use "git commit" command, providing a commit message, which will call git hook that will call "entry" of ".pre-commit-config.yaml" file, which contains "cz check --commit-msg-file" that will check commit message using commitizen following definition of file cz.json. This method needs pre-commit tool. see [README_pre-commit.md](README_pre-commit.md)
