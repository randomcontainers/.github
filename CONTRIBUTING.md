# Contributing

This guide applies to every randomcontainers repository that does not have its own CONTRIBUTING.md.

## Requesting a tool

Use the [Request a tool](https://github.com/randomcontainers/.github/issues/new?template=tool-request.yml) form. A tool is a good fit when:

- it is open source and used from the command line;
- upstream publishes versioned releases on PyPI, as GitHub releases or as tags in a GitHub repository, so new versions can be picked up automatically;
- no maintained image already has upstream version tags, Ubuntu and Alpine variants, a default and a slim image, a non-root user, amd64 and arm64 builds, and build provenance.

Name the images you tried and what they lack; that usually decides a request. If you want to write the package yourself, say so on the form. Once a request is accepted, a maintainer creates the repository and you open a pull request against it. When that pull request is merged, the package is added to the build list in randomcontainers/ci.

## How a package is laid out

Each tool has a repository named after it, for example [randomcontainers/yt-dlp](https://github.com/randomcontainers/yt-dlp).

| File | Contents |
|---|---|
| `package.yml` | Name, license, upstream version source, entrypoint, tests, usage examples and combined images. |
| `Dockerfile.ubuntu`, `Dockerfile.alpine` | One build per distribution. Both take the build arguments `BASE_IMAGE` and `VERSION`, and the final stage is named `slim`. |
| `runtime-deps.ubuntu`, `runtime-deps.alpine` | Runtime packages the build cannot detect by scanning binaries, such as `python3` or fonts. |
| `requirements.lock` | Hash-locked Python dependencies, for Python tools only. |
| `.github/workflows/build.yml` | Calls the shared build workflow in [randomcontainers/ci](https://github.com/randomcontainers/ci). It is the same file in every package repository. |

A few rules keep the images consistent and let tools be combined into one image:

- Everything the tool adds goes under `/usr/local`. A Python tool gets a virtual environment at `/usr/local/lib/<name>`, and only the tool's own commands are linked into `/usr/local/bin`.
- `/usr/local/share/randomcontainers/<name>/` holds the version, the upstream source URLs, the upstream license files and `runtime-deps`, the list of distribution packages the tool needs at run time. The final stage installs those packages, `ca-certificates` and `tini`, and nothing else. A runtime dependency that the build does not find by scanning the binaries goes into `runtime-deps.<distro>`, not into an install command.
- The image works in `/work` as UID 1000, and must also work with any other `--user`.

Combined images, such as yt-dlp with FFmpeg, are declared under `combos` in the owning tool's `package.yml`. Their repositories (for example randomcontainers/yt-dlp-ffmpeg) are generated from that file, so changes belong in the owning tool's repository.

Upstream versions, source checksums and lock files are updated automatically. Leave them out of pull requests.

## Building and testing locally

You need Docker with buildx. Build the slim image for your own platform:

```sh
git clone https://github.com/randomcontainers/yt-dlp
cd yt-dlp
VERSION=$(docker run --rm -i mikefarah/yq:4 '.upstream.version' < package.yml)
docker buildx build -f Dockerfile.ubuntu --target slim \
  --build-arg BASE_IMAGE=ubuntu:26.04 --build-arg VERSION="$VERSION" \
  --load -t local/yt-dlp:slim .
```

For Alpine, use `-f Dockerfile.alpine` and `BASE_IMAGE=alpine:3.24`. CI takes its base images from [`distros.yml`](https://github.com/randomcontainers/ci/blob/main/distros.yml) in randomcontainers/ci. Packages built from a source tarball also need `--build-arg SOURCE_SHA256=...` with the value of `upstream.artifact.sha256`, and compiled packages accept `--build-arg JOBS=<n>` to limit parallel compile jobs.

Run each entry under `test` in `package.yml` the way CI does: as your own user, with an empty directory mounted at `/work` and `VERSION` set.

```sh
work=$(mktemp -d)
docker run --rm --user "$(id -u):$(id -g)" -v "$work:/work" -e VERSION="$VERSION" \
  --entrypoint sh local/yt-dlp:slim -euc 'yt-dlp --version | tee version.txt'
```

With rootless Docker, use `--user 0:0` instead. To build and test the way CI does, including the default image, use `rc` as described in [Building an image locally](https://github.com/randomcontainers/ci#building-an-image-locally).

Check Dockerfiles with hadolint and shell scripts with ShellCheck. Run both from the repository root, so that hadolint reads the repository's `.hadolint.yaml` if it has one:

```sh
docker run --rm -v "$PWD:/mnt:ro" -w /mnt hadolint/hadolint hadolint Dockerfile.ubuntu Dockerfile.alpine
docker run --rm -v "$PWD:/mnt:ro" koalaman/shellcheck:stable path/to/script.sh
```

On every pull request, CI builds both distributions on native amd64 and arm64 runners, checks each image's configuration, installed packages and shared libraries, and runs the tests. It also builds and tests the default image when the other tools in it are already published. Images are published only from `main`.

## Pull requests

- Keep each pull request to one change, and say why it is needed: link the upstream changelog entry or issue, or paste the error it fixes.
- Add or extend a `test` entry in `package.yml` for behavior you add or fix.
- Install software from distribution packages, hash-locked requirements or checksummed downloads. No `curl | sh` and no unverified downloads.
- Don't edit `.github/workflows/build.yml` in a package repository. Changes to the build belong in randomcontainers/ci.
- Don't edit generated combined-image repositories.
- CI must pass for both distributions and both platforms.

Contributions are accepted under the license of the repository you contribute to. Everyone taking part is expected to follow the [code of conduct](https://github.com/randomcontainers/.github/blob/main/CODE_OF_CONDUCT.md).
