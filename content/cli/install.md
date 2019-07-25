---
date: 2000-01-01T00:00:00+00:00
title: CLI Installation
author: bradrydzewski
weight: 1
toc: false
---

The official Drone command line tools include commands for working with the autoscaler. Official binary [releases](https://github.com/drone/drone-cli/releases) can be downloaded from GitHub.

Install on Linux:

```
curl -L https://github.com/drone/drone-cli/releases/download/v1.1.3/drone_linux_amd64.tar.gz | tar zx
sudo install -t /usr/local/bin drone
```

Install on OSX using [Homebrew](https://brew.sh/):

```
brew tap drone/drone
brew install drone
```

Install on Windows using [Scoop](http://scoop.sh/):

```
scoop install drone
```