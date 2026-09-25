randomcontainers builds up-to-date container images for open-source software, starting with command-line tools that have no official image or none that keeps up with upstream releases. The images are built on Ubuntu and Alpine for linux/amd64 and linux/arm64, run as a non-root user and come with build provenance attestations. They are unofficial builds, not affiliated with or endorsed by the upstream projects.

| Image | What it does | `latest` includes |
|---|---|---|
| [yt-dlp](https://github.com/randomcontainers/yt-dlp) | Downloads video and audio from YouTube and many other sites | yt-dlp, FFmpeg, Deno |
| [ffmpeg](https://github.com/randomcontainers/ffmpeg) | Converts, filters and streams audio and video | FFmpeg |
| [imagemagick](https://github.com/randomcontainers/imagemagick) | Converts and edits images | ImageMagick, Ghostscript |
| [ghostscript](https://github.com/randomcontainers/ghostscript) | Renders and converts PostScript and PDF files | Ghostscript |
| [streamlink](https://github.com/randomcontainers/streamlink) | Saves live streams from Twitch, YouTube and other sites | Streamlink, FFmpeg |

The combined images are also published under their own names: `yt-dlp-ffmpeg`, `imagemagick-ghostscript` and `streamlink-ffmpeg`. Each has the same contents as the default image of its tool, and no slim tags.

## Pulling

```sh
docker pull ghcr.io/randomcontainers/yt-dlp
```

The same images can also be pulled as `randomcontainers.com/<name>`.

## Default and slim

`latest` is the tool plus what it most often needs, so common tasks work without extra setup. `slim` is the tool and its own runtime dependencies only, for building your own image on a base that stays up to date. FFmpeg and Ghostscript need nothing extra, so their `latest` and `slim` are the same image.

Alpine builds are tagged `alpine` and `slim-alpine`. Each image's README lists every tag.

## Updates

A new upstream release is picked up once it is a day old. Between releases, the tags of each tool's current version are rebuilt when the base image changes and at least every 7 days, and the default tags also when a tool included in the default image changes. Tags of older versions stay as they were last built. Tags that name a distro release, such as `<version>-ubuntu26.04`, are no longer rebuilt once the images move to the next release. Because tags are rebuilt in place, pin a digest where you need the same image every time. Each image's README describes how its upstream releases are picked up.

## Verifying

Every image is built in the repository of the same name, and its attestation is signed by the shared build workflow in [randomcontainers/ci](https://github.com/randomcontainers/ci). The GitHub CLI needs both repositories to check it:

```sh
gh attestation verify oci://ghcr.io/randomcontainers/<name>:<tag> \
  --repo randomcontainers/<name> --signer-repo randomcontainers/ci
```

## Request a tool

To suggest a tool, use the [Request a tool](https://github.com/randomcontainers/.github/issues/new?template=tool-request.yml) form. [CONTRIBUTING.md](https://github.com/randomcontainers/.github/blob/main/CONTRIBUTING.md) describes what makes a good fit and how packages are built.
