---
date: 2000-01-01T00:00:00+00:00
title: Configure SSL
author: bradrydzewski
weight: 1
toc: false
---

The autoscaler supports ssl configuration by mounting certificates into the server container. _Note that if your server is public you should also consider using Lets Encrypt._

{{< link "/configure/ssl-lets-encrypt" >}}

First, mount your certificate and key into the autoscaler container:

```
docker run \
 -v /etc/certs/domain.com/server.crt:/etc/certs/domain.com/server.crt \
 -v /etc/certs/domain.com/server.key:/etc/certs/domain.com/server.key
```

Configure the path to your certificate and key:

```
DRONE_TLS_CERT=/etc/certs/domain.com/server.crt
DRONE_TLS_KEY=/etc/certs/domain.com/server.key
```

Expose the standard http and https ports:

```
docker run \
 -p 80:80 \
 -p 443:443
```
