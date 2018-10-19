# Singularity CRI

[![CircleCI](https://circleci.com/gh/sylabs/cri.svg?style=svg&circle-token=276de7aa1d82749ecf8ed6513c72399041885dec)](https://circleci.com/gh/sylabs/cri)
<a href="https://app.zenhub.com/workspace/o/sylabs/cri/boards"><img src="https://raw.githubusercontent.com/ZenHubIO/support/master/zenhub-badge.png"></a>

This repository contains Singularity implementation of [Kubernetes CRI](https://github.com/kubernetes/community/blob/master/contributors/devel/container-runtime-interface.md). Singularity CRI consists of
two separate services: runtime and image, each of which implements K8s RuntimeService and ImageService respectively.


The CRI is currently under development and passes 10/71 [validation tests](https://github.com/kubernetes-sigs/cri-tools/blob/master/docs/validation.md).

## Quick Start

To work on Singularity CRI install the following:

- [git](https://git-scm.com/downloads)
- [go](https://golang.org/doc/install)
- [dep](https://golang.github.io/dep/docs/installation.html)
- [gometalinter](https://github.com/alecthomas/gometalinter#installing)
- [singularity](https://github.com/singularityware/singularity/blob/master/INSTALL.md)

Make sure you configured [go workspace](https://golang.org/doc/code.html).

To set up project do the following:

```bash
$ go get https://github.com/sylabs/cri
$ cd $GOPATH/src/github.com/sylabs/cri
$ make dep
```
After this steps you can start working on the project.

Make sure to run linters before submitting a PR:

```bash
make lint
```
## Install dependencies

Sylabs CRI
 - Install and setup a go 1.10 development environment.
 - Install  build-essential/Development tools and libssl-dev uuid-dev squashfs-tools -- packages
 - Install [singularity](https://github.com/singularityware/singularity) 3.0+


## Running and testing

To build server you can use Makefile:

```bash
make build
```

This will produce the _sycri_ binary with CRI server implementation appear in a bin directory.

To start CRI server simply run _sycri_ binary. By default CRI listens for requests on
`unix:///var/run/singularity.sock` and stores image files at `/var/lib/singularity`. This behaviour may be configured
with flags, run `./sycri -h` for more details.

##
To run unit tests you can use Makefile:
```bash
make test
```

##
For live testing we suggest using [`crictl`](https://github.com/kubernetes-sigs/cri-tools/blob/master/docs/crictl.md).


## Project Structure

```
- cmd/
    - server/		Singularity CRI server
    - test/		CLI to call Singularity CRI
- pkg/
    - image/		Image service implementation
    - runtime/		Runtime service implementation
    - singularity/	Common for services Singularity constants
- vendor/		Vendored dependencies (generated by dep)
- Gopkg.lock		Generated dependency graph (generated by dep)
- Gopkg.toml		Dependency rules (used by dep)
```

## Resources

* [How to Write Go Code](https://golang.org/doc/code.html)
* [Effective Go](https://golang.org/doc/effective_go.html)
* [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)
* [GitHub Flow](https://guides.github.com/introduction/flow/)
* [Standard Go Project Layout](https://github.com/golang-standards/project-layout)
* [CRI tools](https://github.com/kubernetes-sigs/cri-tools)
