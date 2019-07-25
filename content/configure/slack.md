---
date: 2000-01-01T00:00:00+00:00
title: Configure Slack Alerts
author: bradrydzewski
weight: 8
toc: false
---

Slack alerts notify you and your team when servers are provisioned and terminated. Enable the built-in Slack integration to send alerts to a Slack channel.

First, create a new Slack application. [Click here](https://api.slack.com/apps?new_app=1).

![slack application creation](/images/slack_app_create.png)

Optionally, customize the display information. You can [download](https://github.com/drone/brand/blob/master/logos/) our official logo and upload as your app icon.

![slack application display info](/images/slack_app_display.png)

Next, click the incoming webhooks link and enable webhooks by toggling the switch. Then create a new webhook and click the Copy button to copy the webhook address.

![slack application webhook](/images/slack_app_webhook.png)

Finally, we need to provide the autoscale server with the webhook. The autoscaler server will post
messages to the webhook when servers are created and terminated.

```
DRONE_SLACK_WEBHOOK=https://hooks.slack.com/services/XXX/YYY/ZZZ
```