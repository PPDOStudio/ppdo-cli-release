# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0-beta.8] - 2026-11-25

### Added

- `ppdo-cli config edit` serves a local page where you manage identities, groups, environments and the mode of each group: see what each mode permits, review the diff of `config.json` and the same changes as commands, and save; a save that lets agents do more waits for `ppdo-cli approval grant <id>` in a terminal, and a Sign in button confirms that a browser, Windows broker or PAT identity works.

### Changed

- The sign-in pages of `auth login` and the PAT page have the look of the other ppdo-cli pages, in light and dark.

## [1.0.0-beta.7] - 2026-11-24

### Added

- `ppdo-cli spec preview <file>` shows the app an app spec describes in your browser, in the look of Power Apps and without an environment: its site map, views over the spec's sample data, and main forms, reloaded when you save the spec.
- Errors that need a sign-in or a person now have a `next` object that says what to run and whether an agent or only the person may run it.
- Without a terminal, a change that lets agents write somewhere new now creates an approval request: you grant it with `ppdo-cli approval grant <id>` at a terminal, and the agent waits with `approval wait <id>` and runs its command again.
- Without a terminal, `auth login` for a PAT identity opens a browser page where you paste the PAT, so an agent can start the sign-in without seeing the PAT.
- `ppdo-cli project init` adds the lean project scaffold and Studio's config files (`<Name>.json`, `<Name>.studio.json`, `Environments.json`, `deployPackages.json`) to a repository, never overwriting a file.
- `ppdo-cli project add-solution` adds a Dataverse solution to a project: it finds or creates the publisher and unmanaged solution, clones the source, and writes the solution's entries in `<Name>.json` and `deployPackages.json` and its `.version` file.
- `ppdo-cli spec validate`, `plan` and `apply` build an app spec (a JSON file of choices, tables, columns, lookups, many-to-many relationships and alternate keys) into a Dataverse environment and its solution, creating only what is missing.
- `spec build` builds source-backed web resources and writes verified artifacts for `spec plan` and `spec apply`.
- `spec build` runs each `npm` or `command` build into an empty output folder, so a webpack build that skips unchanged bundles still gives every web resource, and then puts back the old files it did not replace.
- `spec apply` can create multi-select choices, email, URL and phone columns, polymorphic lookups, lookups that cascade deletes, and custom activity tables.
- An app spec can have `views`: `spec apply` creates them, or replaces their query and columns when they differ, with filters that use option labels and many-to-many links.
- An app spec can have main `forms` with a header (whose columns take the form's labels or their own), tabs, sections, sub-grids and the timeline; on out-of-the-box tables such as account and contact, `spec apply` makes a new copy of the main form and changes the copy, never the system form.
- An app spec can have system `charts` and `dashboards` of charts and lists: `spec apply` creates them, or replaces them when they differ.
- An app spec can give each new table, and each app navigation item, an SVG icon: `spec apply` uploads the icons as web resources and sets them.
- `spec apply` creates the app spec's publisher and unmanaged solution when the environment does not have them, and `spec plan` shows them as its first steps.
- `spec plan` and `spec apply` read the environment several requests at a time and read each thing once, and `spec apply` creates a new table's columns (all but lookups) in the request that creates the table; both report how many seconds each part took.
- An app spec can give column settings (required or recommended, auditing, Advanced find, column security, autonumber, choice and Yes/No defaults, Yes/No labels, decimal ranges), `bigint`, `image`, `file` and `customer` columns, lookup relationship names and every cascade, many-to-many intersect names, and table settings such as auditing and change tracking.
- An app spec can give a date column's behaviour, a text column's format, and a lookup's cascade per target, and names an icon's web resource after its path next to the spec (`icons/x.svg` stays `<prefix>_/icons/x.svg`).
- `spec apply` updates the labels and settings of the tables and columns a spec creates when they differ from the spec, and never changes a column's type.
- An app spec can hold a table's own quick find, lookup, associated, advanced find, offline and Copilot views, view ids, joins, OR groups, quick find columns, hidden and unsortable cells, cell icons and grid settings, and raw FetchXML and layout XML for a view the structured fields cannot hold; `spec from-solution` writes each view in the structured form when it gives the same view, and as raw XML otherwise.
- An app spec can hold quick create, quick view and card forms, form ids, form libraries and event handlers, the form order, tabs with columns, sections of up to four columns, hidden and unlabelled tabs, sections and fields, and raw form XML that names the spec's views, forms and charts; `spec from-solution` writes each form in the structured form when it gives the same form, and as raw XML otherwise.
- An app spec can hold web resources as static files or source-build outputs (`webResources`): `spec apply` creates or updates and publishes them before the forms.
- An app spec can hold environment variables (text, number, yes/no and JSON) with their default and current value: `spec apply` creates or updates them, and `spec from-solution` writes the publisher's variables.
- An app spec can hold security roles with a privilege depth per table and other privileges by name: `spec apply` creates each role and gives it exactly those privileges, and `spec from-solution` writes the roles in the source.
- An app spec can hold plugin assemblies built from source: `spec apply` registers the types, steps, images and Custom APIs that their registration attributes declare, and `spec from-solution` names the C# project of each exported assembly it can find.
- An app spec can register plugin packages (`.nupkg`) that a `dotnet` build packs: `spec apply` uploads the package when its assemblies differ, then registers the steps and Custom APIs of those assemblies, and `spec from-solution` names the project of each exported package.
- `spec build` builds .NET projects without the Git commit in the informational version, so a commit that leaves a plugin's source as it is does not change its assembly, and packs a plugin package again on each build.
- An app spec can hold cloud flows from their definition JSON and the connection references they use: `spec apply` creates or updates each flow and turns it on or off, `spec plan` compares the definition by content and stops a flow that should be on while a reference it uses has no connection, and `spec from-solution` points each cloud flow at its exported definition.
- An app spec can hold classic workflows, business rules and actions from their exported XAML and settings: `spec apply` creates or updates each one (an active one is turned off for the update and on again), and `spec from-solution` points each one at its exported files.
- An app spec can hold organization settings (`settings`): columns of the organization row, such as auditing and session timeouts, and the environment values of setting definitions; `spec apply` sets them through the Web API, and `spec from-solution` writes the setting values the solutions carry.
- An app spec can pass through folders of an unpacked solution that it does not model (`passthrough`), such as canvas apps, Dataverse search, AI skills and duplicate rules: `spec apply` imports them into the spec's solution, `spec plan` compares them with an export of that solution, and `spec from-solution` writes one entry per solution for those folders.
- An app spec can hold PCF controls built from source: `spec apply` imports a new or changed control into the spec's solution and publishes it, `spec plan` asks for a higher version when the bundle changed but the version did not, and `spec from-solution` names the `.pcfproj` of each exported control it finds.
- An app spec can define Custom APIs with their request parameters and response properties, each implemented by a plugin type of a spec plugin: `spec apply` registers them with that assembly, and `spec from-solution` writes the APIs that only the solution defines.
- An app spec can name `dv data` folders in `referenceData`: `spec plan` shows each one's plan as a `data` step and `spec apply` imports it after everything else, with `--overlay` and `--no-overlay`; `spec from-solution` lists each solution's `reference-data` folder and gives the `dv data convert` command for CMT data.
- `project init` writes `.gitattributes` lines that keep `dv data` YAML files LF and the files of file and image columns binary.
- An app spec chart can keep its own look (`presentationXml`); a dashboard can give its components' widths, heights, search, letter bar, view picker and header colour, or be raw XML; an app can give its security roles by name, its settings and exact lists of views, forms and charts. `spec from-solution` writes all of these.
- An app spec can build into several solutions: `solutions` lists the others, and each element can name its `solution`; `spec apply` creates missing solutions with their version and description, and `spec from-solution` puts each element in the solution that first defined it.
- An app spec can have formula (Power Fx), calculated and rollup columns: `spec apply` creates them after the columns they read and updates a definition that differs, and `spec from-solution` writes them, with the XAML of calculated and rollup columns in `formulas/` next to the spec.
- `spec apply` saves a table's quick find view through an import of the spec's solution, because Dataverse refuses a Web API update of a quick find view with its search columns.
- `dv view` checks a quick find view's query without its search placeholders, so a quick find on a number column no longer fails the check.
- `ppdo-cli spec from-solution` writes an app spec from unpacked solution source, reading a project's solutions in deployment order, with a gaps file for each part the spec cannot hold yet.
- `ppdo-cli spec seed` upserts an app spec's `data` rows by their key columns, with choice labels, lookups by name and many-to-many links, and changes nothing on a rerun.
- An app spec can have model-driven `apps`: `spec apply` creates each app and its site map, puts the spec's tables, forms and views in it, and reports the app checker's warnings.
- A new agent skill, `ppdo-cli-build`, tells agents how to turn a Figma mockup, Azure DevOps stories or a brief into an app spec and apply it.
- PAT identities can share a Windows Credential Manager target with a PAT Manager canvas.
- `ppdo-cli repo create` creates a repository on GitHub or in an Azure DevOps project and pushes its first commit, with `--preview` and resume after a failed step.
- GitHub environments (`env add --github <owner>`) and the `gh_cli` sign-in method, which uses the GitHub CLI's sign-in for github.com only.

### Changed

- ppdo-cli now reads the optional PAT Manager organization configuration from `%LOCALAPPDATA%\PatManager\config\organisations.json`.
- The `ppdo-cli-build` skill now lists the known limits of app specs and what to do for each, and the README says that `spec plan` runs build commands when the cached outputs are stale.
- The agent skill now has agents set up identities, read-only groups and environments, and start `auth login` themselves, while you finish each sign-in in the browser and raise each mode at a terminal.

### Fixed

- `spec validate` accepts Custom API parameter names with hyphens, as Dataverse does.
- `spec from-solution` and `spec plan` find a plugin package that Dataverse named `<prefix>_<PackageId>` from the project's `PackageId` without the prefix.
- `spec from-solution` keeps an environment variable's definition when a later solution only names the variable.
- `spec from-solution` writes the Custom APIs of a plugin package whose class binds them with `[CrmPluginRegistration("<name>")]`, also when the name is a constant, and leaves out those that `[CustomApi]` defines.
- `dv plugin register` no longer fails when a step names a table that does not exist yet; the plan says the table has no filter for the message.
- `skills list` marks a linked skill whose target is gone as `broken`, and a deleted copy as `missing`, instead of showing it as installed.
- `repo create` refuses Windows drive-relative paths such as `C:dir`.

## [1.0.0-beta.6] - 2026-11-23

### Added

- A `dv data` lookup value can be the expression `{ $expr: businessunit.root }`, which the import resolves to the root business unit of the target environment, in a data file or an overlay.
- `dv data` role links (`teamroles_association`, `systemuserroles_association`) keep the root role, which has the same GUID in each environment; the import links the copy of the role in the business unit of the team or user, and the schema needs no file for `role`.
- A `dv data` table with `perEnvironment: true` can have a data file for each environment (`data/tables/<table>.<environment>.yaml`) beside the default file, for records that are different in an environment.
- `dv data import --environment-name <name>` and `dv data delete --environment-name <name>` use the data of one environment: its overlay, if any, and its file of each table with `perEnvironment`.

### Changed

- `dv data export` writes the root role of each role link in place of the copy of the business unit; export such relationships again.

## [1.0.0-beta.5] - 2026-11-20

### Added

- `dv data import --write-upsert` updates the existing records of seed tables (`write: create`) for one run; with `--only`, only the tables of the list.

### Changed

- `dv data import` lists each existing record of a seed table (`write: create`) that is different from the file as `kept`, with its differences, and counts it in `kept`; it still does not write it, and `--check` does not give exit 6 for it.
- The import warns when a seed table has the delete mode `mirror`.

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

[Unreleased]: https://github.com/PPDOStudio/ppdo-cli-release/compare/v1.0.0-beta.8...HEAD
[1.0.0-beta.8]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.8
[1.0.0-beta.7]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.7
[1.0.0-beta.6]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.6
[1.0.0-beta.5]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.5
[1.0.0-beta.4]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.4
[1.0.0-beta.3]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.3
[1.0.0-beta.2]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.2
[1.0.0-beta.1]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.1
[1.0.0-beta.0]: https://github.com/PPDOStudio/ppdo-cli-release/releases/tag/v1.0.0-beta.0
