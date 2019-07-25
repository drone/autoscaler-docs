---
date: 2000-01-01T00:00:00+00:00
title: DRONE_TLS_AUTOCERT
author: bradrydzewski
toc: false
---

Automatically generates an SSL certificate using Lets Encrypt,
and configures the API server to accept HTTPS requests.
This configuration parameter is of type `boolean` and is optional,
and is disabled by default.

```
DRONE_TLS_AUTOCERT=false
DRONE_TLS_AUTOCERT=true
```