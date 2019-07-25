---
date: 2000-01-01T00:00:00+00:00
title: drone server env
author: bradrydzewski
toc: false
description: |
  Print instance connection details as Docker environment
  variables.
---

This subcommand prints environment variables to dictate that docker should run a command against a particular server node.

Example usage:

```
$ drone server env agent-f0e4c2f7

export DOCKER_TLS=1
export DOCKER_TLS_VERIFY=
export DOCKER_CERT_PATH=/home/octocat/.drone/certs/agent-f0e4c2f7
export DOCKER_HOST=tcp://192.168.99.101:2376

# Run this command to configure your shell:
# eval "$(drone server env agent-f0e4c2f7)"
```

Example shell configuration:

```
$ eval "$(drone server env agent-f0e4c2f7)"
$ docker version

Client:
 Version:	18.03.0-ce
 API version:	1.35 (downgraded from 1.37)
 Go version:	go1.9.4
 Git commit:	c160c73
 Built:	Thu Feb 22 02:34:03 2018
 OS/Arch:	darwin/amd64
 Experimental:	false
 Orchestrator:	swarm

Server:
 Engine:
  Version:	17.12.0-ce
  API version:	1.35 (minimum version 1.12)
  Go version:	go1.9.2
  Git commit:	c97c6d6
  Built:	Wed Dec 27 20:09:53 2017
  OS/Arch:	linux/amd64
  Experimental:	false
```

The example above requires Docker client version 18.03.0 or higher.

## Shell Support

The default configuration is intended for bash and zsh. However, Drone support multiple shell environments including bash, powershell, and fish.

For fish shell:

```
$ drone server env agent-f0e4c2f7 --shell=fish

sex -x DOCKER_TLS "1";
set -x DOCKER_TLS_VERIFY "";
set -x DOCKER_CERT_PATH "/home/octocat/.drone/certs/agent-f0e4c2f7";
set -x DOCKER_HOST tcp://192.168.99.101:2376;

# Run this command to configure your shell:
# eval "$(drone server env agent-f0e4c2f7 --shell=fish)"
```

For powershell:

```
drone server env agent-f0e4c2f7 --shell=powershell

$Env:DOCKER_TLS = "1"
$Env:DOCKER_TLS_VERIFY = ""
$Env:DOCKER_CERT_PATH = "/home/octocat/.drone/certs/agent-f0e4c2f7"
$Env:DOCKER_HOST = "tcp://192.168.99.101:2376"

# Run this command to configure your shell:
# drone server env agent-f0e4c2f7 --shell=powershell | Invoke-Expression
```