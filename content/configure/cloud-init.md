---
date: 2000-01-01T00:00:00+00:00
title: Using a Custom Cloud-Init
author: bradrydzewski
weight: 12
toc: false
---

In some cases you may need to customize an instance at creation, before the agent is installed and started. 

{{< alert warning >}}
Overriding the default cloud-init file is an advanced feature and should be avoided unless absolutely necessary.
{{</ alert >}}

You can customize your instance configuration by providing a custom cloud-init file. Below is sample cloud-init file that you can use as a baseline and customize.

{{< highlight terminal "linenos=table" >}}
#cloud-config

apt_reboot_if_required: false
package_update: false
package_upgrade: false

apt:
  sources:
    docker.list:
      source: deb [arch=amd64] https://download.docker.com/linux/ubuntu $RELEASE stable
      keyid: 0EBFCD88

packages:
  - docker-ce

write_files:
  - path: /etc/systemd/system/docker.service.d/override.conf
    content: |
      [Service]
      ExecStart=
      ExecStart=/usr/bin/dockerd
  - path: /etc/default/docker
    content: |
      DOCKER_OPTS=""
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": [ "0.0.0.0:2376", "unix:///var/run/docker.sock" ],
        "tls": true,
        "tlsverify": true,
        "tlscacert": "/etc/docker/ca.pem",
        "tlscert": "/etc/docker/server-cert.pem",
        "tlskey": "/etc/docker/server-key.pem"
      }
  - path: /etc/docker/ca.pem
    encoding: b64
    content: {{ .CACert | base64 }}
  - path: /etc/docker/server-cert.pem
    encoding: b64
    content: {{ .TLSCert | base64 }}
  - path: /etc/docker/server-key.pem
    encoding: b64
    content: {{ .TLSKey | base64 }}

runcmd:
  - [ systemctl, daemon-reload ]
  - [ systemctl, restart, docker ]
{{< / highlight >}}

You will need to provide your custom cloud-init file to the autoscale server. You can mount the file as a volume:

```
--volume=/path/on/host/init.yml:/path/in/container/init.yml
```

You will also need to tell the autoscale server where to find the file inside the container. _Please adjust the configuration based on your provider_.

```
DRONE_AMAZON_USERDATA_FILE=/path/inside/container/init.yml
```