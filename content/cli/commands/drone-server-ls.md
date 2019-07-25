---
date: 2000-01-01T00:00:00+00:00
title: drone server ls
author: bradrydzewski
toc: false
description: |
  Print a list of all server instances.
---

This subcommand prints a list of all registered servers. Please note this command requires administrative privileges.

Example usage:

```
$ drone server ls

i-f0e4c2f76c58916ec
i-258f246851bea091d
i-14d4247a2fc3e1869
i-4461b1816e13b7a21
```

Format the output using a custom Go template:

```
$ drone server ls --format="{{ .Name }} <{{ .Address }}>"

i-f0e4c2f76c58916ec <198.51.100.245>
i-258f246851bea091d <198.51.100.141>
i-14d4247a2fc3e1869 <198.51.100.88>
i-4461b1816e13b7a21 <198.51.100.72>
```
