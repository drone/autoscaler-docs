---
date: 2000-01-01T00:00:00+00:00
title: Install for Hetzner Cloud
author: bradrydzewski
logo: hetzner_logo.png
toc: true
---

The goal of this document is to give you enough technical specifics to configure and run the autoscaler. When properly configured, it will automatically provision and terminate Hetzner Cloud instances based on your Drone server's build volume.

# Prerequisites

## Create a Drone Token

You need to create a Drone user token with administrative privilege that you can provide to the autoscaler. The autoscaler will use this token to remotely access the Drone build queue.

## Create a Hetzner Token

You need to create a Hetzner token that you can provide to the autoscaler. The autoscaler will use the token to authorize API requests.

## Create an SSH Keypair

You need to create an SSH keypair and register with Hetzner. The autoscaler will use the SSH private key for remote login and access to your droplets.

# Download

The autoscaler is distributed as a lightweight Docker image. The image is self-contained and does not have any external requirements.

```
docker pull drone/autoscaler
```

# Start the Server

{{< alert warn >}}
This section is missing the hetzner environment variable parameters. Please consider sending a pull request to improve this documentation.
{{</ alert >}}

The autoscaler container can be started with the below command. The container is configured through environment variables. For a full list of configuration parameters, please see the [configuration reference](/reference).

{{< highlight terminal "linenos=table" >}}
docker run -d \
  -e DRONE_POOL_MIN={DRONE_POOL_MIN} \
  -e DRONE_POOL_MAX={DRONE_POOL_MAX} \
  -e DRONE_SERVER_PROTO={DRONE_SERVER_PROTO} \
  -e DRONE_SERVER_HOST={DRONE_SERVER_HOST} \
  -e DRONE_SERVER_TOKEN={DRONE_SERVER_TOKEN} \
  -e DRONE_AGENT_TOKEN={DRONE_AGENT_TOKEN} \
  -p 8080:8080 \
  --restart=always \
  --name=autoscaler \
  drone/autoscaler
{{< / highlight >}}

# Reference

## Environment

Configuration parameters are set using environment variables. This section defines a subset of recommended configuration parameters. For a full list, please see our configuration reference.

### DRONE_POOL_MIN

An integer defining the minimum number of instances the autoscaler should keep alive. The default value is two instances.

```
DRONE_POOL_MIN=2
```

### DRONE_POOL_MAX

An integer defining the maximum number of instances the autoscaler can provision. The default value is four instances.

```
DRONE_POOL_MAX=4
```

### DRONE_SERVER_PROTO

A string containing your Drone server protocol scheme. This value should be set to http or https.

```
DRONE_SERVER_PROTO=https
```

### DRONE_SERVER_HOST

A string containing your Drone server hostname or IP address.

```
DRONE_SERVER_HOST=drone.domain.com
```

### DRONE_SERVER_TOKEN

A string containing your Drone user token. This token must grant administrative access to your Drone server.

### DRONE_AGENT_CONCURRENCY

An integer defining the maximum number of concurrent builds an agent can execute. This value is used to configure new agents.

```
DRONE_AGENT_CONCURRENCY=2
```

### DRONE_AGENT_TOKEN

A string containing the shared secret (DRONE_RPC_SECRET) that authorizes agent to server communication. This value is used to configure new agents.

```
DRONE_AGENT_TOKEN=IiOiIxMjM0NTY3ODkwIiwibmFtZSI6Ikxvb2
```

## Network

The autoscaler exposes REST endpoints so that you can extract runtime information from the system. The autoscaler listens on port 8080 inside the container, and should be published on the host machine:

```
--publish=8080:8080
```

## Volumes

The autoscaler creates a sqlite database and persists to a container volume at `/data`. To prevent dataloss, we recommend mounting the data volume to the host machine.

```
--volume=/var/lib/autoscaler:/data
```
