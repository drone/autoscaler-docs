---
date: 2000-01-01T00:00:00+00:00
title: DRONE_PROMETHEUS_TOKEN
author: bradrydzewski
toc: false
---

Restricts access to the prometheus `/metrics` endpoint and
requires authentication using the provided token. If the
token is empty or is not set, the prometheus endpoint allows
guest access. This configuration parameter is of type `string`
and is optional.

```
DRONE_PROMETHEUS_TOKEN=b359e05e8
```

