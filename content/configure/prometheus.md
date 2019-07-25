---
date: 2000-01-01T00:00:00+00:00
title: Configure Prometheus
author: bradrydzewski
weight: 4
toc: false
---

The autoscaler publishes and exposes metrics that can be consumed by Prometheus. Please note that access to the metrics endpoint is restricted and requires an authorization token.

First, create a random token:

```
$ openssl rand -base64 12
  zFuQGzQetpeaSWix
```

Next, register the token with the autoscaler:

```
DRONE_PROMETHEUS_TOKEN=zFuQGzQetpeaSWix
```

Finally, configure the prometheus scraper:

{{< highlight terminal "linenos=table" >}}
global:
    scrape_interval: 60s

    scrape_configs:
    - job_name: 'autoscaler'
        bearer_token: zFuQGzQetpeaSWix

        static_configs:
        - targets: ['domain.com']
{{< / highlight >}}
