---
date: 2000-01-01T00:00:00+00:00
title: DRONE_INTERVAL
author: bradrydzewski
toc: false
---

The interval at which the autoscaler algorithm is run. This configuration parameter is of type [time.Duration](https://golang.org/pkg/time/#ParseDuration) and is optional, with a default value of 1 minute.

```
DRONE_INTERVAL=1h
DRONE_INTERVAL=1m
DRONE_INTERVAL=60s
DRONE_INTERVAL=30s
```
