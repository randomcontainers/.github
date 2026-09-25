# Getting help

## Problems with an image

Open an issue in the repository of the image you use, for example [randomcontainers/yt-dlp](https://github.com/randomcontainers/yt-dlp/issues). That covers missing libraries or features, wrong or missing tags, permission errors on mounted directories, and images that fall behind upstream. For a combined image such as `yt-dlp-ffmpeg`, use the repository of the tool it belongs to, here randomcontainers/yt-dlp.

The bug report form asks for the image digest. Get it with:

```sh
docker image inspect --format '{{index .RepoDigests 0}}' ghcr.io/randomcontainers/yt-dlp:latest
```

Each image's README covers usage, tags and file permissions.

## Problems with the tool itself

If the tool behaves the same way outside the container at the same version, the problem is upstream. Report it to the upstream project; each image's README links to its issue tracker.

Don't report container problems to the upstream projects. These images are unofficial and not affiliated with them.

## Other problems and requests

- New tools: use the [Request a tool](https://github.com/randomcontainers/.github/issues/new?template=tool-request.yml) form.
- The build workflows: open an issue in [randomcontainers/ci](https://github.com/randomcontainers/ci/issues).
- Security issues: follow [SECURITY.md](https://github.com/randomcontainers/.github/blob/main/SECURITY.md) and report privately.

There is no paid support.
