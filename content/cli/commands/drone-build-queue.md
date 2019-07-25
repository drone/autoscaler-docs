---
date: 2000-01-01T00:00:00+00:00
title: drone build queue
author: bradrydzewski
toc: false
draft: true
---

This subcommand prints a list of all running and pending builds in the queue. Please note this command requires administrative privileges.

Example usage:

```
$ drone build queue

octocat/hello-world #42
Status: pending
Event: push
Commit: 766d2d1fd691556c37ba023ca1a68592d303b651
Branch:master
Ref: refs/heads/master
Author: Octocat <octocat@github.com>
Message: Update the README
```
