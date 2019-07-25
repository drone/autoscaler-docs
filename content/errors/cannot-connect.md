---
date: 2000-01-01T00:00:00+00:00
title: "Cannot connect, retry in 1m0s"
author: bradrydzewski
weight: 1
---

The autoscale server will attempt to establish a connection with your instance. The network may not be immediately available, in which case the autoscale server will wait and attempt to reconnect. It is therefore normal to see this message in your logs.

If this message repeats indefinitely, it could indicate network connectivity issues. It might indicate, for example, your server is blocking inbound TCP connections to port 2376. Please check your security group and network settings.

```
|DEBU| cannot connect, retry in 1m0s error="Cannot connect to the
       Docker daemon. Is the docker daemon running?"
```
