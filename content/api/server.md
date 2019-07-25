---
date: 2000-01-01T00:00:00+00:00
title: Server Endpoints
author: bradrydzewski
weight: 2
toc: true

description: |
  The server API allows you to create, access, and terminate server instances programmatically.
---

The server API allows you to create, access, and terminate server instances programmatically.

# Find a Server

Find a server by name.

```
GET /api/servers/:name
```

Request Parameters:

Parameter | Type        | Description
----------|-------------|------------
`name`    | `string`    | name of the server

200 Response Body:

{{< highlight json >}}
{
    "id": "string",
    "provider": "string",
    "state": "string",
    "name": "string",
    "image": "string",
    "region": "string",
    "size": "string",
    "address": "string",
    "capacity": "number",
    "secret": "string",
    "error": "string",
    "ca_key": "string",
    "ca_cert": "string",
    "ca_cert": "string",
    "tls_key": "string",
    "tls_cert": "string",
    "created": "number",
    "updated": "number",
    "started": "number",
    "stopped": "number"
}
{{< / highlight >}}

# List All Servers

List all servers.

```
GET /api/servers
```

Response Body:

{{< highlight json >}}
[
    {
        "id": "string",
        "provider": "string",
        "state": "string",
        "name": "string",
        "image": "string",
        "region": "string",
        "size": "string",
        "address": "string",
        "capacity": "number",
        "secret": "string",
        "error": "string",
        "ca_key": "string",
        "ca_cert": "string",
        "ca_cert": "string",
        "tls_key": "string",
        "tls_cert": "string",
        "created": "number",
        "updated": "number",
        "started": "number",
        "stopped": "number"
    }
]
{{< / highlight >}}

# Provision a Server

Provision allocates a new server instance.

```
POST /api/servers
```

200 Response Body:

{{< highlight json >}}
{
    "id": "string",
    "provider": "string",
    "state": "string",
    "name": "string",
    "image": "string",
    "region": "string",
    "size": "string",
    "address": "string",
    "capacity": "number",
    "secret": "string",
    "error": "string",
    "ca_key": "string",
    "ca_cert": "string",
    "ca_cert": "string",
    "tls_key": "string",
    "tls_cert": "string",
    "created": "number",
    "updated": "number",
    "started": "number",
    "stopped": "number"
}
{{< / highlight >}}

# Terminate a Server

Terminate stops and terminates a named server instance.

```
DELETE /api/servers/:name
```

Request Parameters:

Parameter | Type        | Description
----------|-------------|------------
`name`    | `string`    | name of the server
`force`   | `boolean`   | force remove the instance


<!-- {{< highlight TypeScript >}}
{
    id: string;
    provider: string;
    state: string;
    name: string;
    image: string;
    region: string;
    size: string;
    address: string;
    capacity: number;
    secret: string;
    error: string;
    ca_key: string;
    ca_cert: string;
    ca_cert: string;
    tls_key: string;
    tls_cert: string;
    created: number;
    updated: number;
    started: number;
    stopped: number;
}
{{< / highlight >}} -->