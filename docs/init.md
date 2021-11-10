For new projects, it is possible to run `cz init`.

This command will prompt the user for information about the project and will
configure the selected file type (`pyproject.toml`, `.cz.toml`, etc.).

This will help you quickly set up your project with `commitizen`.

Currently `init` is detecting

1. Commit convention rules (`name`).
2. Version detection based on the existing tags (`version`).
3. Tag format, if your tag convention uses, for example `v*` in front of the version. (`tag_format`)

We hope to detect the files where the version is also repeated eventually,
like `package.json` or `__version__`.
