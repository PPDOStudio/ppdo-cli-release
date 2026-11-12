# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0-beta.1] - 2026-11-12

### Added

- The `pat` sign-in method signs in to one Azure DevOps organization with a personal access token.

### Security

- Child processes no longer get the environment variables that hold a client secret or a PAT.
- Azure DevOps tokens are no longer sent to a URL whose path uses `..` or `%2e%2e` segments to reach another organization.

## [1.0.0-beta.0] - 2026-11-12

First public release, on npm as `@ppdostudio/ppdo-cli`. Free to use under the ppdo-cli Free Use Licence.

### Added

- `ppdo-cli identity`, `group` and `env` set up accounts, groups with a safety mode, and the environments in each group.
- `ppdo-cli group discover` finds the Dataverse environments a group's account can reach.
- `ppdo-cli env use` sets the default environment, and `env pin` sets the environments for a repo.
- `ppdo-cli auth login|logout|status|token` signs identities in and out, and shows their sign-in status and tokens.
- A browser sign-in shows a sign-in ID in the terminal and on its pages, so several sign-ins at once can be told apart.
- `ppdo-cli whoami` shows which environment, mode and account each service uses.
- `ppdo-cli dv api` and `ado api` send any Dataverse or Azure DevOps request.
- `ppdo-cli dv query|get|create|update|delete|batch` read and write Dataverse rows.
- `ppdo-cli dv upsert|associate|disassociate` create or update many rows and link records.
- `ppdo-cli dv fn|action` call Dataverse functions and actions.
- `ppdo-cli dv history` shows who changed a record.
- `ppdo-cli dv metadata` reads and creates tables, columns, choices and keys.
- `ppdo-cli dv solution` lists, exports, imports and manages solutions.
- `ppdo-cli dv solution unpack|pack|clone|sync` keep solutions in source control without pac.
- `ppdo-cli dv publisher` lists and creates publishers.
- `ppdo-cli dv component` and `dv dependency` show a component's layers and dependencies.
- `ppdo-cli dv envvar|connref|connection` manage environment variables and connection references.
- `ppdo-cli dv workflow` lists cloud flows and other processes, turns them on and off, and shows flow runs.
- `ppdo-cli dv plugin` shows plugin registrations and trace logs, and turns steps on and off.
- `ppdo-cli dv job` follows system jobs.
- `ppdo-cli dv org|setting|team|role|user|access` show environment details, security and record access.
- `ppdo-cli dv view|form|webresource` edit views, forms and web resources as files.
- `ppdo-cli ado project|repo|pipeline|run` work with projects, repositories and pipeline runs.
- `ppdo-cli ado pr|wi` work with pull requests and work items.
- `ppdo-cli ado user|vargroup|environment|pool` look up users, variable groups, pipeline environments and agent pools.
- `ppdo-cli graph group` looks up Entra groups.
- `ppdo-cli skills` installs the agent skills into Claude Code or GitHub Copilot.
- `ppdo-cli commands` lists every command and whether it reads or writes.
- Three agent skills ship with the CLI: `ppdo-cli`, `ppdo-cli-dataverse` and `ppdo-cli-devops`.
- Each group's mode (`read-only`, `read-write` or `full`) limits what commands can change.
- `--dry-run` shows a request without sending it.
- `--env a,b` and `--group` run a read command against several environments.
- `--client-id` runs commands as an app (service principal) with no config.
- Output is JSON by default, or `-o ndjson|table|tsv`.
- The config is JSON, with a JSON schema for editors.
- `THIRD-PARTY-NOTICES` lists the open source packages bundled into ppdo-cli and their licences.

[Unreleased]: https://github.com/PPDOStudio/ppdo-cli-release/compare/v1.0.0-beta.1...HEAD
[1.0.0-beta.1]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.1
[1.0.0-beta.0]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.0
