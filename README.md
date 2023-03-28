# Commitizen-Enhanced

Based on [commitizen](https://github.com/commitizen-tools/commitizen)

# Info
This tool is a inquirer to help create a correct commit message and check using git hook scripts.
Git hook scripts are useful for identifying simple issues before submission to code review.

Project was forked and modified to support following features:
- "multiline" type
- "max_len" property to check line length
- "retry" propoerty to send last commit without inquire questions
- "force_commit" property to force commit even when commit message has errors
- feat confirmation. This allow to do check even for unconfirmed commit messages

# Install
## Once per PC:

```console
$ sudo pip3 install -U Commitizen pre-commit
$ sudo pip3 install -U ."
```

## Once per git project:

Add [.pre-commit-config.yaml](example/.pre-commit-config.yaml) and [cz.json](example/cz.json) files to git project's root directory

```console
$ pre-commit install --hook-type commit-msg
$ pre-commit autoupdate
```

# More info
[README_pre-commit.md](README_pre-commit.md)
[README_commitizen.md](README_commitizen.md)

# Files changed:
    - .pre-commit-config.yaml:
        - Run local cz for this project
    - commitizen/commands/commit.py:
        - Add ["commitizen"]["customize"]["retry"] = <true/false> for cz.json
            [true] Uses last commit message without doing any question
            [false] Starts to make each question defined in cz.json
        - Add ["commitizen"]["customize"]["questions"][0]["type"] = "multiline" for cz.json
        - Add ["commitizen"]["customize"]["force_commit"] = <true/false> for cz.json
            When this is true, tries "git commit" command even when "cz check" command fails (only when commit is confirmed)
        - Add check_only feature when commit is not confirmed.
            This is retrieved from customize.py. When the commit message is not confirmed, check_only is set to true
    - commitizen/cz/customize/customize.py:
        - Add ["commitizen"]["customize"]["max_len"] = <number> for cz.json
            By default it's 100
        - Add hidden "confirmation" question prompt at end of questions
        - Add check_only feature when commit is not confirmed
            A "confirmation" hidden question prompt is added at end of questions. The answer is then transmited to commit.py.
    - commitizen/git.py:
        - Add check_only feature
            This runs "cz check" command but not "git commit" command

# Step by step
    1. commitizen/commands/commit.py:__call__():
        1. commitizen/commands/commit.py:prompt_commit_questions():
            1. Call commitizen/cz/customize/customize.py:questions():
                1. Parses cz.json and makes each question, inside ["commitizen"]["customize"]["questions"] of cz.json file, to the user.
            2. At end of all questions, calls commitizen/cz/customize/customize.py:message() with all answers:
                If this commit was not confirmed (last question made to user), prepend "|nonconfirmed|" no commit message
        2. if commit msg starts with "|nonconfirmed|" means that the message was not confirmed by the user. We will still check the message but not do the commit. ("|nonconfirmed|" string is removed from commit message)
        3. call commitizen/git.py:commit():
            1. Add check_only feature
            returns {"c":c, "c2":c2}
            c is return of "cz check" command
            c2 is return of "git commit" command
