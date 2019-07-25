---
date: 2000-01-01T00:00:00+00:00
title: DRONE_POOL_MIN_AGE
author: bradrydzewski
toc: false
---

Defines the minimum age a server must reach before it can be
terminated. This configuration parameter is of type `time.Duration` and
is required, with a default value of 1 hour.

```
DRONE_POOL_MIN_AGE=24h
DRONE_POOL_MIN_AGE=60m
DRONE_POOL_MIN_AGE=30m
DRONE_POOL_MIN_AGE=15m
```

