---
date: 2000-01-01T00:00:00+00:00
title: Configure Agent Logging
author: tphoney
weight: 3
toc: true
---

# debugging agent / build failures in the field

## Introduction

This will walk you through adding further logging to the autoscaler agent to help diagnose issues with a build that is not completeing as expected. This will allow us to upload logs from the agent (drone-runner-docker's docker daemon) to the cloud. The following explains the steps required for AWS, but the same concepts can be applied to other cloud providers.

## AWS changes

We will need to add a new policy and role to the AWS account. The policy will allow the autoscaler agent (docker daemon) to write to cloudwatch logs. The role will be attached to the autoscaler agent instance.

### Create a new Policy

Go to the IAM policies page and create a new policy eg `https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-2#/policies`. The policy should have the following permissions:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogStream",
                "logs:CreateLogGroup",
                "logs:PutLogEvents"
            ],
            "Resource": "*"
        }
    ]
}
```

### Create a new Role

Go to the IAM roles page and create a new role eg `https://us-east-1.console.aws.amazon.com/iamv2/home#/roles`. Then attach the policy created above to the role. You then need to copy the `Instance profile ARN` from the role page eg `https://us-east-1.console.aws.amazon.com/iamv2/home#/roles/details/cloudwatchautoscaler?section=permissions`, The arn should look like `arn:aws:iam::093396591680:instance-profile/cloudwatchautoscaler`.

## Autoscaler changes

This is were we add the IAM profile to the autoscaler agent instance and enable more verbose logging on the Agent(docker daemon).

### .env changes

Add the following options to the `.env` file:

```bash
DRONE_AGENT_ENVIRON=DRONE_DEBUG=true,DRONE_TRACE=true                                         # enable debug and trace logging on the runner
DRONE_AMAZON_IAM_PROFILE_ARN=arn:aws:iam::093396591680:instance-profile/cloudwatchautoscaler  # attach the iam role to the agent instance
```

### cloud-init changes

See the following page for adding custom userdata to the autoscaler agent instance `https://autoscale.drone.io/configure/cloud-init/`. Add the following snippet to the cloud-init to enable uploading logs to amazon cloudwatch:

```yaml
 - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": [ "0.0.0.0:2376", "unix:///var/run/docker.sock" ],
        "tls": true,
        "tlsverify": true,
        "tlscacert": "/etc/docker/ca.pem",
        "tlscert": "/etc/docker/server-cert.pem",
        "tlskey": "/etc/docker/server-key.pem",
        "log-driver": "awslogs",                 # enable cloudwatch logging
        "log-opts": {                            #
          "awslogs-region": "us-east-2",         # set the region
          "awslogs-group":  "autoscaler",        # set the log group
          "awslogs-create-group": "true"         # create the log group if it doesn't exist
        }
      }
```

There are other options for the log driver, see `https://docs.docker.com/config/containers/logging/awslogs/` for more information.

## Viewing the logs

Logs from the agent (docker daemon) will be uploaded to cloudwatch. You can view the logs in the cloudwatch console eg `https://us-east-2.console.aws.amazon.com/cloudwatch/home?region=us-east-2#logsV2:log-groups/log-group/autoscaler`. You can also set up alerts or set the log retention period.
