---
date: 2000-01-01T00:00:00+00:00
title: System Endpoints
author: bradrydzewski
weight: 2
toc: true

description: |
  The system API allows you to access and control system operations.
---

This API allows you to access and control system operations.

# Pause

The Pause endpoint pauses the autoscaling routine. When autoscaling is paused, the system will not automatically provision or terminate any instances.

```
POST /api/pause
```

# Resume

The Resume endpoint resumes the autoscaling routine. When autoscaling is resumed, the system will automatically provision or terminate any instances based on build volume.

```
POST /api/resume
```

# Health

The Health endpoint returns a `200 OK` if the autoscaler is in a healthy state. This endpoint is intended for use with monitoring tools and does not require authentication.

```
GET /healthz
```