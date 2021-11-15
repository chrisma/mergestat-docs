---
sidebar_position: 1
---

# Installation

## Homebrew

Currently, `homebrew` is one of the easier installation paths for the CLI.

```
brew tap askgitdev/askgit
brew install askgit
```

## Pre-Built Binaries

The [latest releases](https://github.com/askgitdev/askgit/releases) should have pre-built binaries for Mac and Linux.
You can download and add the `askgit` binary somewhere on your `$PATH` to use.
`libaskgit.so` is also available to be loaded as a SQLite run-time extension.

## Go

[`libgit2`](https://libgit2.org/) is a build dependency (used via [`git2go`](https://github.com/libgit2/git2go)) and must be available on your system for linking.

The following (long 😬) `go install` commands can be used to install a binary via the go toolchain.

On Mac:
```
CGO_CFLAGS=-DUSE_LIBSQLITE3 CGO_LDFLAGS=-Wl,-undefined,dynamic_lookup go install -tags="sqlite_vtable,vtable,sqlite_json1,static,system_libgit2" github.com/askgitdev/askgit@latest
```

On Linux:
```
CGO_CFLAGS=-DUSE_LIBSQLITE3 CGO_LDFLAGS=-Wl,--unresolved-symbols=ignore-in-object-files go install -tags="sqlite_vtable,vtable,sqlite_json1,static,system_libgit2" github.com/askgitdev/askgit@latest
```

See the [`Makefile`](https://github.com/askgitdev/askgit/blob/main/Makefile) for more context.
Checking out this repository and running `make` in the root will produce two files in the `.build` directory:

  1. `askgit` - the CLI binary (which can then be moved into your `$PATH` for use)
  2. `libaskgit.so` - a shared object file [SQLite extension](https://www.sqlite.org/loadext.html) that can be used by SQLite directly

## Using Docker

Build an image locally using docker

```
docker build -t askgit:latest .
```

Or use an official image from [docker hub](https://hub.docker.com/repository/docker/augmentable/askgit)

```
docker pull augmentable/askgit:latest
```