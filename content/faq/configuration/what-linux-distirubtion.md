---
date: 2000-01-01T00:00:00+00:00
title: Which base image is used?
author: bradrydzewski
weight: 1
---

When Drone creates a server instance it uses the official Ubuntu base image (from your hosting provider). The autoscaler is optimized for Debian and Ubuntu and requires additional configuration when using a custom Linux distribution.