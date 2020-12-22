---
date: 2000-01-01T00:00:00+00:00
title: Install for Amazon EC2
author: bradrydzewski
logo: aws_logo.svg
toc: true
---

The goal of this document is to give you enough technical specifics to configure and run the autoscaler. When properly configured, it will automatically provision and terminate EC2 instances based on your Drone server's build volume.

# Prerequisites

## Create a Drone Token

You need to create a Drone user token with administrative privilege that you can provide to the autoscaler. The autoscaler will use this token to remotely access the Drone build queue. If you do not know how to create a token please see [our tutorial](https://docs.drone.io/manage/user/machine/).

## Create a Secret Access Key

You need to create an AWS Secret Access key that you can provide to the autoscaler. The autoscaler will use these credentials to authorize API requests. If you do not know how to create a token please see our tutorial.

## Create an SSH Keypair

You need to create an SSH keypair named `drone` and register with AWS. The autoscaler will add the SSH key to provisioned instances. You can then use the private key for remote SSH access to the instance, for manual debugging purposes. If you do not know how to create and upload a keypair please see our tutorial.

## Create a VPC

You will need a VPC configured with default subnets. You will need to provide the autoscaler with a subnet ID. If you do not know how to find or create subnets please see our tutorial.

## Create a Security Group

You will need a VPC and= security group that enables inbound TCP traffic to `2376` from `0.0.0.0/0`. If you do not know how to create a security group, please see our tutorial.

# Download

The autoscaler is distributed as a lightweight Docker image. The image is self-contained and does not have any external requirements.

```
docker pull drone/autoscaler
```

# Start the Server

The autoscaler container can be started with the below command. The container is configured through environment variables. For a full list of configuration parameters, please see the [configuration reference](/reference).

{{< highlight text "linenos=table" >}}
docker run -d \
  -v /var/lib/autoscaler:/data \
  -e DRONE_POOL_MIN=${DRONE_POOL_MIN} \
  -e DRONE_POOL_MAX=${DRONE_POOL_MAX} \
  -e DRONE_SERVER_PROTO=${DRONE_SERVER_PROTO} \
  -e DRONE_SERVER_HOST=${DRONE_SERVER_HOST} \
  -e DRONE_SERVER_TOKEN=${DRONE_SERVER_TOKEN} \
  -e DRONE_AGENT_TOKEN=${DRONE_AGENT_TOKEN} \
  -e DRONE_AMAZON_INSTANCE=${DRONE_AMAZON_INSTANCE} \
  -e DRONE_AMAZON_REGION=${DRONE_AMAZON_REGION} \
  -e DRONE_AMAZON_SUBNET_ID=${DRONE_AMAZON_SUBNET_ID} \
  -e DRONE_AMAZON_SECURITY_GROUP=${DRONE_AMAZON_SECURITY_GROUP} \
  -e DRONE_AMAZON_SSHKEY=${DRONE_AMAZON_SSHKEY} \
  -e AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID} \
  -e AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY} \
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

### DRONE_AMAZON_REGION

A string containing the region in which new instances are provisioned.

```
DRONE_AMAZON_REGION=us-east-1
```

### DRONE_AMAZON_SUBNET_ID

A string containing the identifier of the subnet used to configure instance networks.

```
DRONE_AMAZON_SUBNET_ID=subnet-0b32177f
```

### DRONE_AMAZON_INSTANCE

A string field, provides the instance type you wish to use when provisioning instances. The default value is `t2.medium`.

```
DRONE_AMAZON_INSTANCE=t2.medium
```

### DRONE_AMAZON_SECURITY_GROUP

A string containing the identifier of the security group used to configure instance networks.

```
DRONE_AMAZON_SECURITY_GROUP=sg-770eabe1
```

### DRONE_AMAZON_SSHKEY

A string containing the name of the registered SSH key that should be added to newly created instances.

```
DRONE_AMAZON_SSHKEY=id_rsa
```

### AWS_ACCESS_KEY_ID

A string containing your amazon secret key ID. You may alternatively use IAM roles for authorization.

### AWS_SECRET_ACCESS_KEY

A string containing your amazon secret access key. You may alternatively use IAM roles for authorization.

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
