---
date: 2000-01-01T00:00:00+00:00
title: DRONE_AGENT_IMAGE
author: bradrydzewski
toc: false
---

A string field, configures the agent Docker image. The agent is a daemon that polls the central Drone server for tasks. When the autoscaler provisions an instance, it installs a single agent on the instance.

```
DRONE_AGENT_IMAGE=drone/agent:1
```
