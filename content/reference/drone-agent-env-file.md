---
date: 2000-01-01T00:00:00+00:00
title: DRONE_AGENT_ENV_FILE
author: bradrydzewski
toc: false
---

Optional string. Provides a path to an environment file containing environment variables used to configure the agent.

```
DRONE_AGENT_ENV_FILE=/path/to/file.env
```

The environment file is a text file that defines environment variables in key value format. Please see the envfile [documentation](https://github.com/joho/godotenv) for more details about the file format.

```
S3_BUCKET=YOURS3BUCKET
SECRET_KEY=YOURSECRETKEYGOESHERE
```