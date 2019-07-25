---
date: 2000-01-01T00:00:00+00:00
title: CLI Configuration
author: bradrydzewski
weight: 2
toc: false
---

The command line tools interact with the server and autoscaler using REST endpoints. You will need to provide the CLI tools with the server and autoscale addresses, and your personal authorization token.

Configure your Drone server address:

```
export DRONE_SERVER=http://drone.mycompany.com
```

Configure your Drone personal token:

```
export DRONE_TOKEN=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

Configure your autoscaler address:

```
export DRONE_AUTOSCALER=http://autoscaler.mycompany.com
```
