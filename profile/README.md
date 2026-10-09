randomcontainers builds up-to-date container images for open-source software, starting with command-line tools that have no official image or none that keeps up with upstream releases. The images are built on Ubuntu and Alpine for linux/amd64 and linux/arm64, run as a non-root user and come with build provenance attestations. They are unofficial builds, not affiliated with or endorsed by the upstream projects.

## Images

### Video and audio

| Image | What it does | `latest` includes |
|---|---|---|
| [yt-dlp](https://github.com/randomcontainers/yt-dlp) | Downloads video and audio from YouTube and many other sites | yt-dlp, FFmpeg, Deno |
| [streamlink](https://github.com/randomcontainers/streamlink) | Saves live streams from Twitch, YouTube and other sites | Streamlink, FFmpeg |
| [ffmpeg](https://github.com/randomcontainers/ffmpeg) | Converts, filters and streams audio and video | FFmpeg |
| [mediainfo](https://github.com/randomcontainers/mediainfo) | Reports the codecs, bit rates and tracks of video and audio files | MediaInfo, FFmpeg |
| [mkvtoolnix](https://github.com/randomcontainers/mkvtoolnix) | Creates, edits and extracts from Matroska and WebM files | MKVToolNix, FFmpeg, MediaInfo |
| [whisper-cpp](https://github.com/randomcontainers/whisper-cpp) | Transcribes and translates speech on the CPU (models not included) | whisper.cpp, FFmpeg |
| [vmaf](https://github.com/randomcontainers/vmaf) | Scores the quality of an encoded video against its source | VMAF, FFmpeg |
| [audiowaveform](https://github.com/randomcontainers/audiowaveform) | Generates waveform data and images from audio files | audiowaveform, FFmpeg |
| [srt](https://github.com/randomcontainers/srt) | Streams live video, sends files and tunnels TCP over SRT | SRT tools, FFmpeg |
| [shaka-packager](https://github.com/randomcontainers/shaka-packager) | Packages and encrypts video, audio and subtitles for DASH and HLS streaming | Shaka Packager, FFmpeg |

### Image files

| Image | What it does | `latest` includes |
|---|---|---|
| [imagemagick](https://github.com/randomcontainers/imagemagick) | Converts and edits images | ImageMagick, Ghostscript |
| [exiftool](https://github.com/randomcontainers/exiftool) | Reads, writes and removes metadata in images, video and documents | ExifTool, ImageMagick |
| [jpegoptim](https://github.com/randomcontainers/jpegoptim) | Makes JPEG files smaller | jpegoptim, ImageMagick |
| [libjpeg-turbo](https://github.com/randomcontainers/libjpeg-turbo) | Rotates, crops and optimizes JPEG files losslessly, and converts images to and from JPEG | libjpeg-turbo, ExifTool |
| [libheif](https://github.com/randomcontainers/libheif) | Converts HEIC and AVIF photos, and encodes images as HEIC or AVIF | libheif, ExifTool |
| [libvips](https://github.com/randomcontainers/libvips) | Converts, resizes and makes thumbnails of images, including very large ones | libvips |

### PDF and documents

| Image | What it does | `latest` includes |
|---|---|---|
| [ghostscript](https://github.com/randomcontainers/ghostscript) | Renders and converts PostScript and PDF files | Ghostscript |
| [qpdf](https://github.com/randomcontainers/qpdf) | Merges, splits, encrypts and repairs PDF files | qpdf, Ghostscript |
| [mupdf](https://github.com/randomcontainers/mupdf) | Renders, converts and edits PDF files, and converts EPUB and XPS | MuPDF |
| [poppler](https://github.com/randomcontainers/poppler) | Extracts text and images from PDF files and renders their pages | Poppler |
| [tesseract](https://github.com/randomcontainers/tesseract) | Reads text in scans and photos (OCR), with the English model | Tesseract, Poppler |
| [weasyprint](https://github.com/randomcontainers/weasyprint) | Turns HTML and CSS into PDF documents laid out for print | WeasyPrint, qpdf |

### Development

| Image | What it does | `latest` includes |
|---|---|---|
| [graphviz](https://github.com/randomcontainers/graphviz) | Draws graphs written in the DOT language | Graphviz |
| [doxygen](https://github.com/randomcontainers/doxygen) | Generates documentation from comments in source code | Doxygen, Graphviz |
| [sphinx](https://github.com/randomcontainers/sphinx) | Builds documentation from reStructuredText into HTML, LaTeX, ePub and man pages | Sphinx, Graphviz |
| [yamllint](https://github.com/randomcontainers/yamllint) | Checks YAML files for syntax errors and formatting problems | yamllint |
| [check-jsonschema](https://github.com/randomcontainers/check-jsonschema) | Validates JSON, YAML and TOML files against a JSON Schema, with schemas for CI configuration | check-jsonschema |
| [jsonnet](https://github.com/randomcontainers/jsonnet) | Evaluates, formats and lints Jsonnet configuration | Jsonnet (Go implementation) |
| [libxml2](https://github.com/randomcontainers/libxml2) | Checks, validates, formats and transforms XML files | libxml2, libxslt |
| [codespell](https://github.com/randomcontainers/codespell) | Finds and fixes common misspellings in source code and documentation | codespell |
| [vale](https://github.com/randomcontainers/vale) | Checks prose in Markdown, HTML and code comments against your style rules (styles not included) | Vale |
| [clang-format](https://github.com/randomcontainers/clang-format) | Formats C, C++, Java, JavaScript and other source code to a configured style | clang-format |
| [cppcheck](https://github.com/randomcontainers/cppcheck) | Finds bugs and undefined behavior in C and C++ code by static analysis | Cppcheck |
| [protoc](https://github.com/randomcontainers/protoc) | Generates code from Protocol Buffers .proto files | protoc |
| [duckdb](https://github.com/randomcontainers/duckdb) | Runs SQL queries on CSV, Parquet and JSON files and on DuckDB databases | DuckDB |

### Files and networks

| Image | What it does | `latest` includes |
|---|---|---|
| [7zip](https://github.com/randomcontainers/7zip) | Creates and extracts 7z, zip, tar and many other archives | 7-Zip |
| [rsync](https://github.com/randomcontainers/rsync) | Copies and synchronizes files, sending only what changed | rsync |
| [openssh-client](https://github.com/randomcontainers/openssh-client) | Logs in to SSH servers, copies files with scp and sftp, and manages keys | OpenSSH client |
| [iperf3](https://github.com/randomcontainers/iperf3) | Measures network throughput between two hosts | iperf3 |
| [nmap](https://github.com/randomcontainers/nmap) | Discovers hosts and services and scans ports, with Ncat and Nping | Nmap |
| [dig](https://github.com/randomcontainers/dig) | Queries DNS servers and sends dynamic updates | BIND 9 client tools |
| [tcpdump](https://github.com/randomcontainers/tcpdump) | Captures and decodes network packets | tcpdump |
| [tshark](https://github.com/randomcontainers/tshark) | Captures and decodes network traffic with Wireshark's dissectors, without the GUI | TShark, tcpdump |
| [openssl](https://github.com/randomcontainers/openssl) | Makes keys and certificates and tests TLS connections | OpenSSL |

The default images that add other tools are also published under their own names, with the same contents and no slim tags: `yt-dlp-ffmpeg`, `streamlink-ffmpeg`, `mediainfo-ffmpeg`, `mkvtoolnix-ffmpeg-mediainfo`, `whisper-cpp-ffmpeg`, `vmaf-ffmpeg`, `audiowaveform-ffmpeg`, `srt-ffmpeg`, `shaka-packager-ffmpeg`, `imagemagick-ghostscript`, `exiftool-imagemagick`, `jpegoptim-imagemagick`, `libjpeg-turbo-exiftool`, `libheif-exiftool`, `qpdf-ghostscript`, `tesseract-poppler`, `weasyprint-qpdf`, `doxygen-graphviz`, `sphinx-graphviz` and `tshark-tcpdump`. `check-jsonschema-yamllint` is published the same way but is not a default image: it adds yamllint to check-jsonschema. Where a default image adds another tool from this list, it is that tool's `slim` build: ImageMagick in `exiftool` and `jpegoptim`, for example, has no Ghostscript.

## Pulling

The images are published to the GitHub Container Registry as `ghcr.io/randomcontainers/<name>`:

```sh
docker pull ghcr.io/randomcontainers/yt-dlp
```

## Default and slim

`latest` is the tool plus what it most often needs, so common tasks work without extra setup. `slim` is the tool and its own runtime dependencies only, for building your own image on a base that stays up to date. Tools that need nothing extra, such as FFmpeg, Ghostscript and Nmap, have the same image under `latest` and `slim`.

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
