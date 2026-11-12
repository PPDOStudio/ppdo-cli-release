# Security policy

ppdo-cli signs in to Dataverse, Azure DevOps and Microsoft Graph and caches tokens on your machine, so we take security reports seriously.

## Report a vulnerability

Please don't open a public issue. Email **security@powerplatformdevops.studio** with:

- the ppdo-cli version (`ppdo-cli --version`) and your operating system;
- what the problem is and what someone could do with it;
- the steps or commands that show it, with tenant ids, URLs, names, tokens and secrets removed.

We'll reply to say we have your report, keep you told how the fix is going, and credit you in the changelog unless you'd rather we didn't.

## What counts

For example:

- a token, secret or certificate written somewhere it shouldn't be, or sent to a host other than the environment's own;
- an Azure DevOps PAT shown in any output, stored unencrypted on Windows, sent outside its one organization, or stored or changed without a person at a terminal;
- a way to get around a group's mode (`read-only`, `read-write`, `full`) or to widen it without a person at a terminal;
- a way for a repo's `.ppdo-cli.json`, a response from a service, or any other input to make ppdo-cli run something or write outside the folder it was given.

## Supported versions

Fixes go into the next release. While ppdo-cli is in beta, only the latest release is supported.
