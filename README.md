# netns

[![Travis CI](https://img.shields.io/travis/genuinetools/netns.svg?style=for-the-badge)](https://travis-ci.org/genuinetools/netns)
[![GoDoc](https://img.shields.io/badge/godoc-reference-5272B4.svg?style=for-the-badge)](https://godoc.org/github.com/schahriar/netns)
[![Github All Releases](https://img.shields.io/github/downloads/genuinetools/netns/total.svg?style=for-the-badge)](https://github.com/schahriar/netns/releases)

Runc hook for setting up default bridge networking.

<!-- toc -->

- [Installation](#installation)
    + [Binaries](#binaries)
    + [Via Go](#via-go)
- [Usage](#usage)

<!-- tocstop -->

## Installation

#### Binaries

For installation instructions from binaries please visit the [Releases Page](https://github.com/schahriar/netns/releases).

#### Via Go

```console
$ go get github.com/schahriar/netns
```

## Usage

```console
$ netns -h
netns -  Runc hook for setting up default bridge networking.

Usage: netns <command>

Flags:

  --ipfile     file in which to save the containers ip address (default: .ip)
  --mtu        mtu for bridge (default: 1500)
  --state-dir  directory for saving state, used for ip allocation (default: /run/github.com/schahriar/netns)
  --bridge     name for bridge (default: netns0)
  -d           enable debug logging (default: false)
  --iface      name of interface in the namespace (default: eth0)
  --ip         ip address for bridge (default: 172.19.0.1/16)

Commands:

  create   Create a network.
  ls       List networks.
  rm       Delete a network.
  version  Show the version information.
```

Place this in the `Hooks.Prestart` field of your `runc` config.

```json
{
    ...
    "hooks": {
        "prestart": [
            {
                "path": "/path/to/netns"
            }
        ]
    },
    ...
}
```

**List network namespaces**

```console
$ sudo netns ls
IP                  LOCAL VETH          PID                 STATUS
172.19.0.3          netnsv0-21635       21635               running
172.19.0.4          netnsv0-21835       21835               running
172.19.0.5          netnsv0-22094       22094               running
172.19.0.6          netnsv0-25996       25996               running
```