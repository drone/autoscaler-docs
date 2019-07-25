---
date: 2000-01-01T00:00:00+00:00
title: API Overview
author: bradrydzewski
weight: 1
---

The autoscaler API is organized around REST. It accepts JSON-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authorization, and verbs.

Example request:

```
curl -X GET "http://localhost:8080/api/servers" \
  -H "Authorization: Bearer AKIAIOSFODNN7EXAMPLE"
```

# Authentication

The autoscaler API uses access tokens to authorize requests. You can retrieve an access token in the Drone user interface by navigating to your user profile.

{{< alert security >}}
In order to access the autoscaler API you must have a system administrator role in Drone.
{{< / alert >}}

Authentication to the API is performed using the HTTP Authorization header. Provide your token as the bearer token value.

```
Authorization: Bearer AKIAIOSFODNN7EXAMPLE
```
