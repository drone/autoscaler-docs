---
date: 2000-01-01T00:00:00+00:00
title: DRONE_AGENT_LABELS
author: bradrydzewski
toc: false
---

Optional string map. Provides a set of labels used by the scheduler to assign the pipeline to a specific runner. Note that a pipeline is only assigned to a runner when its configuration exactly matches the pipeline labels.

```
DRONE_AGENT_LABELS=foo:bar,baz:qux
```