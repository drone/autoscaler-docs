---
date: 2000-01-01T00:00:00+00:00
title: Configure Logging
author: bradrydzewski
weight: 3
toc: false
---

Logs are written to stderr and are captured by the Docker daemon. You can access the logs by running the following Docker command:

```
docker logs autoscaler
```

The defult log level is `DEBUG`. Over time, once you feel more comfortable with the autoscaler, you can disable debug logging:

```
DRONE_LOGS_DEBUG=false
```

Logs are written to `stderr` in json-format. You can change the default log format to something more human-readable with the following settings:

```
DRONE_LOGS_PRETTY=true
DRONE_LOGS_COLOR=true
```
