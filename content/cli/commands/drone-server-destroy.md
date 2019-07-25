---
date: 2000-01-01T00:00:00+00:00
title: drone server destroy
author: bradrydzewski
toc: false
description: |
  Schedule a server instance for termination.
---

This subcommand instructs the autoscaler to gracefully terminate a running server. Please note this command requires administrative privileges.

Example usage:

```
$ drone server destroy i-f0e4c2f76c58916ec

Name:    i-f0e4c2f76c58916ec
Size:    m5.xlarge
Region:  us-east-1
Address: 198.51.100.245
State:   shutdown
```