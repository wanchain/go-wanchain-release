# go-wanchain-release

Official prebuilt release binaries of **`gwan`**, the Wanchain full-node client.

This repository hosts ready-to-run executables for each tagged release so that
node operators do not need a Go toolchain to get started. Every release is
published on the [**Releases**](https://github.com/wanchain/go-wanchain-release/releases)
page as a set of compressed archives.

## Downloads

Grab the archive that matches your operating system and CPU architecture from the
[latest release](https://github.com/wanchain/go-wanchain-release/releases/latest):

| Platform | Architecture | Archive |
| --- | --- | --- |
| Linux | x86-64 | `gwan-linux-amd64.tgz` |
| Linux | ARM64 | `gwan-linux-arm64.tgz` |
| Windows | x86-64 | `gwan-windows-amd64.tgz` |
| macOS | Apple Silicon (ARM64) | `gwan-darwin-arm64.tgz` |

Each archive contains a single executable: `gwan` on Linux/macOS, `gwan.exe` on
Windows. The Linux and Windows builds are statically linked, so they run on a
wide range of distributions without extra system libraries.

## Install

### Linux / macOS

Linux need Ubuntu24 or above
```bash
# Replace the file name with the archive you downloaded
tar -xzf gwan-linux-amd64.tgz

# (Optional) move it onto your PATH
sudo mv gwan /usr/local/bin/

gwan version
```

### Windows

Extract `gwan-windows-amd64.tgz` with any tool that understands `.tgz`
(e.g. 7-Zip or `tar` in PowerShell), then run:

```powershell
.\gwan.exe version
```

## Verify your download

Every release includes a checksum table in its notes. After downloading, compare
the MD5 of your archive against the value listed on the release page:

```bash
# Linux
md5sum gwan-linux-amd64.tgz

# macOS
md5 gwan-darwin-arm64.tgz
```

If the values do not match, do **not** run the binary — re-download it.

## Quick start

```bash
# Print the client version and exit
gwan version

# Show all available options
gwan --help

# Start a node (example)
gwan --datadir /path/to/data
```

## Docker

Official images are published to Docker Hub:

```bash
docker pull wanchain/client-go:latest
docker run -it wanchain/client-go:latest gwan version
```

## Building from source

These binaries are produced from the main Wanchain client source code. If you
prefer to build `gwan` yourself, refer to the build instructions in the main
project. Reproducing a release locally typically uses static linking, e.g.:

```bash
CGO_ENABLED=1 go build -trimpath \
  -tags 'osusergo netgo' \
  -ldflags "-s -w -linkmode external -extldflags '-static'" \
  -o gwan ./cmd/geth
```

## Release contents

For each release you will find:

- One archive per supported platform (see the table above).
- A checksum table for verifying the archives.
- Release notes describing the changes included in that version.

## License

The Wanchain client is released under the GNU Lesser General Public License v3.0
(LGPL-3.0), the same license as the upstream go-ethereum project. The
command-line client (`gwan`) is licensed under the GNU General Public License
v3.0 (GPL-3.0).
