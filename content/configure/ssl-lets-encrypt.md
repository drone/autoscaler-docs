---
date: 2000-01-01T00:00:00+00:00
title: Configure SSL with Lets Encrypt
author: bradrydzewski
weight: 2
toc: false
---

The autoscaler supports automated SSL configuration and updates using let’s encrypt. You can enable Let’s encrypt with the following flag:

First, enable Lets Encrypt:

```
DRONE_TLS_AUTOCERT=true
```

Next, ensure the desired hostname is configured:

```
DRONE_HTTP_HOST=domain.com
DRONE_HTTP_PROTO=https
```

Finally, expose the standard http and https ports:

```
docker run \
 -p 80:80 \
 -p 443:443
```
