---
date: 2000-01-01T00:00:00+00:00
title: drone build kill
author: bradrydzewski
toc: false
draft: true
---

This subcommand attempts to force cancel a zombie build that appears stuck with a running state. Please note this command requires administrative access to the repository.

Example usage:

```
$ drone build kill octocat/hello-world 42
```