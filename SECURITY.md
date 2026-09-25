# Security policy

## Reporting a vulnerability

Report vulnerabilities privately through GitHub's private vulnerability reporting on the affected repository: open its Security tab and choose "Report a vulnerability", or go to `https://github.com/randomcontainers/<repository>/security/advisories/new`. If you are not sure which repository is affected, report it on [randomcontainers/ci](https://github.com/randomcontainers/ci/security/advisories/new).

Do not open a public issue or pull request for a vulnerability. Include the image and digest if one is involved, what an attacker could do, and how to reproduce it. We aim to reply within 7 days.

## Scope

This policy covers the published images and what builds them:

- build recipes: Dockerfiles, `package.yml`, lock files and the generated files in combined-image repositories
- the GitHub Actions workflows and the `rc` tool in [randomcontainers/ci](https://github.com/randomcontainers/ci), including the automation that updates versions and repositories

Examples: a build that downloads something without verifying it, a workflow that exposes a token or can be triggered to publish untrusted code, or an image that ships a file or package it should not.

Out of scope:

- Vulnerabilities in the packaged tools themselves. Report them to the upstream project under its own security policy. When upstream releases a fix, the images pick it up automatically, usually about a day after the release.
- Known vulnerabilities in Ubuntu or Alpine packages. The supported tags below are rebuilt whenever the base image changes and at least every 7 days, which picks up distribution fixes. If a fix published by the distribution is still missing from a supported tag a week later, open a regular issue in the image's repository.

## Supported versions

Only the tags of the upstream version currently in a package's `package.yml` receive fixes: `latest`, `slim`, their `ubuntu` and `alpine` variants, and the version tags of that release. `latest`, `slim` and their variants move to each new upstream release. Between releases, all of these tags are rebuilt when the base image changes and at least every 7 days, and the default tags also when a tool included in the default image changes.

Tags of older upstream versions stay as they were last built. Tags that name a distro release, such as `<version>-ubuntu26.04` or `<version>-alpine3.24`, are no longer rebuilt once the project moves to the next release of that distro.

## Verifying an image

Each image has a build provenance attestation. Check it with the GitHub CLI:

```sh
gh attestation verify oci://ghcr.io/randomcontainers/<name>:<tag> \
  --repo randomcontainers/<name> --signer-repo randomcontainers/ci
```

`--repo` is the repository the image is built in, which has the image's name. The attestation is signed by the shared build workflow in [randomcontainers/ci](https://github.com/randomcontainers/ci), so the check fails without `--signer-repo randomcontainers/ci`.
