# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0-beta.4] - 2026-11-20

### Fixed

- `dv data` writes a date-only column with the behavior UserLocal as a date and time in UTC, so its date is no longer one day early in a time zone ahead of UTC; export such tables again.

## [1.0.0-beta.3] - 2026-11-19

### Changed

- A `dv data` overlay name can have upper case letters and `_`, so it can be the name of a pipeline environment, for example `Contoso_Test`.

## [1.0.0-beta.2] - 2026-11-19

### Added

- `dv plugin register` registers a plugin DLL from attributes on its classes in a development environment: assembly, plugin types, steps, images, Custom APIs with their parameters and properties, and workflow activities, with `--dry-run`, `--solution` and the part options `--assembly`, `--steps` and `--apis`.
- `dv plugin inspect` reads and checks the registration attributes of a plugin DLL, without .NET.
- `dv plugin migrate` prints registration attributes for classes that use spkl attributes, with the step ids of the environment.
- `dv plugin register` also reads spkl `CrmPluginRegistration` attributes, so a spkl project registers without code changes.
- The `ppdo-cli-plugins` skill gives agents the attribute class file (`PluginRegistration.cs`) and the procedures to set up, change and deploy plugin registrations.
- `dv data export` writes the configuration data of a solution as YAML files in a `reference-data` folder (one file for each table or for each record, many-to-many links, and the files of file and image columns), with `--check` to find out-of-date files. A record is identified by its GUID, and a lookup is the GUID of its target.
- `dv data import` makes an environment equal to a `reference-data` folder and writes only the differences, with a plan (`--check`) and `--overlay` for the values of one environment (also a GUID that is different in that environment). It creates each record with the GUID of the file, and it never deletes.
- `dv data delete` deletes the records and removes the links that the delete modes of the schema give, after a person types `delete` at the terminal, or with `--yes` in a pipeline; `--check` lists each delete.
- `dv data convert` converts a Configuration Migration Tool `data.xml` and its schema to a `reference-data` folder; it reads the metadata of the environment (reads only) for the schema names and order of many-to-many relationships, and leaves out, with a warning, columns that cannot be written and relationships to tables outside the CMT schema, so the first export needs no hand edits.
- A `dv data` schema file accepts a full CMT `<fetch>` document in `fetchXmlFilter` and uses the `<filter>` elements of its `<entity>`.
- `dv data export` keeps the records and links deleted in the source environment in a deletion log, `data/.deleted`, by GUID, for tables and relationships with the delete mode `manifest` or `mirror`; the log only grows, and `dv data delete` deletes the logged records and removes the logged links in the target.
- `dv data delete` continues after a delete or link removal that Dataverse refuses, and reports it in `failures`; `--delete-log-file <file>` writes each record and link that it deleted to a JSON file.
- `dv data init` adds a schema file for each table from the metadata of the environment.
- `dv data export`, `import` and `convert` keep the attachments of notes and email attachments (`annotation.documentbody`, `activitymimeattachment.body`) as files in `data/files`, not as base64 text in the YAML.
- A `dv data` schema file can set the path of each file in `data/files` with a file name pattern (`files.name` for the table, `file` for one column), for example `"{objectid.name}/{$filename}"`.
- `dv data export`, `dv data import` and `dv data delete` show their progress on stderr with `--verbose`, and `--log-file <file>` keeps the progress, the retries, the result and the error in a file.
- The `ppdo-cli-data` skill gives agents the `dv data` commands, the `reference-data` folder and file formats, overlays, deletes, errors and pipeline steps.
- `schema/reference-data.schema.json` describes the format of a `dv data` schema file, so an editor can check it and complete its properties.

### Fixed

- A `.ppdo-cli.json` that pins no environment (for example one with only a `plugins` section) no longer stops commands with "names no environment"; the search goes on up to the git root, then to the default.
- `env pin` keeps the other keys of `.ppdo-cli.json`, such as `plugins`, instead of writing only the pins.
- `env unpin` removes only the pins, and deletes `.ppdo-cli.json` only when nothing else is in it.

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

[Unreleased]: https://github.com/PPDOStudio/ppdo-cli-release/compare/v1.0.0-beta.4...HEAD
[1.0.0-beta.4]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.4
[1.0.0-beta.3]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.3
[1.0.0-beta.2]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.2
[1.0.0-beta.1]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.1
[1.0.0-beta.0]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.0
