# Getting help with ppdo-cli

## Look here first

- The [README](README.md): install, setting up identities, groups and environments, safety modes and every command.
- `ppdo-cli <command> --help`: each command's options, with examples.
- `ppdo-cli whoami --check`: which environment, mode and account each service uses, and whether sign-in works.
- The error itself: every error is one JSON object on stderr, and most have a `hint` with the command to run next. The exit code says what kind of problem it is (see the README).

## Ask

Open an issue and pick the form that fits:

- **Bug report**: a command failed or did something wrong.
- **Feature request**: a command or option you'd like.
- **Question**: how to do something.

Include the ppdo-cli version (`ppdo-cli --version`), the command and the JSON error. Remove tenant ids, environment and organization names, URLs, user names, tokens and secrets first, and never paste the output of `ppdo-cli auth token`.

For a security problem, don't open an issue: see [SECURITY.md](SECURITY.md).
