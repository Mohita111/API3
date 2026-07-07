---
title: How to Track Performance with Droplet Graphs
description: Monitor Droplet performance in the control panel with default graphs for bandwidth, disk I/O, and disk usage. The metrics agent, enabled by default at …
product: Droplets
url: https://docs.digitalocean.com/products/droplets/how-to/track-performance/
last_updated: "2026-04-15"
---

> **For AI agents:** The documentation index is at [https://docs.digitalocean.com/llms.txt](https://docs.digitalocean.com/llms.txt). Markdown versions of pages use the same URL with `index.html.md` in place of the HTML page (for example, append `index.html.md` to the directory path instead of opening the HTML document).

# How to Track Performance with Droplet Graphs

DigitalOcean Droplets are Linux-based virtual machines (VMs) that run on top of virtualized hardware. Each Droplet you create is a new server you can use, either standalone or as part of a larger, cloud-based infrastructure.

Droplet graphs are up-to-the-minute visualizations of how your server is performing over time. They let you monitor Droplet performance metrics on the **Insights** tab in the control panel.

Droplets come with some graphs available by default, and there are additional graphs available when the [DigitalOcean metrics agent](https://docs.digitalocean.com/products/monitoring/index.html.md#what-is-the-digitalocean-agent) is installed. The metrics agent also enables [DigitalOcean Monitoring](https://docs.digitalocean.com/products/monitoring/index.html.md) and [alert policies](https://docs.digitalocean.com/products/monitoring/how-to/manage-alerts/index.html.md#create-control).

## Default Droplet Graphs

To view a Droplet’s graphs, click its name on the **Droplets** page, then click the **Insights** tab. By default, three graphs are available for any Droplet:

- The **Bandwidth public** chart displays public bandwidth usage in megabits per second. Incoming bandwidth is one color and outgoing bandwidth is another.
- The **Disk I/O** chart displays disk read and write operations in megabytes per second, with read and write called out separately in the legend.
- The **Disk Usage** chart shows the percentage of space being used on the Droplet’s disk.

The times in these graphs are in your local time zone, as determined by your browser.

If you have enabled private networking on the Droplet, you also have access to a **Bandwidth private** chart that displays [VPC network](https://docs.digitalocean.com/products/networking/vpc/index.html.md) bandwidth usage.

## Metrics Agent

The default Droplet graphs use metrics collected by external tools; they require no additional services on the Droplet itself. You can enable additional metrics graphs and alerting with the DigitalOcean metrics agent, which is a small utility that runs on the Droplet.

The **Improved Metrics and monitoring** checkbox on the [Droplet create page](https://docs.digitalocean.com/products/droplets/how-to/create/index.html.md) is enabled by default and installs the metrics agent automatically when you provision a Droplet. If you disabled this option at create time or manage an older Droplet, you can [install the metrics agent later](https://docs.digitalocean.com/products/monitoring/how-to/install-metrics-agent/index.html.md#install).

Once the agent is installed, the following additional graphs are available on the **Insights** tab:

- The **CPU** chart shows the percent of total processing power being used, with distinct colors for user and system processes in the legend.
- The **Load Average** chart measures whether the CPU is keeping up with queued processes. There are three lines representing 1-, 5-, and 15-minute load average calculation time frames. For definitions, see [load average](https://docs.digitalocean.com/products/monitoring/concepts/metrics/index.html.md#load-average) in the metrics reference.
- The **Memory** chart displays the percentage of physical RAM in use.

![Droplet Insights tab with CPU and Load charts, time period selector, Manage Monitoring button, and Monitoring Agent Enabled indicator.](https://docs.digitalocean.com/screenshots/droplets/pages/graphs.822d84740b3cc1562d340fbd454dc6c461a259885c851d44e517b53d9a662c23.png)

The Droplet graph time frame options include 1 hour, 6 hours, 24 hours, 7 days, and 14 days. Data resolution is based on number of points, with a fixed number of points per plot. When you mouse over any of the graphs, a line appears on all of them, pinpointing a moment in time. A graph legend appears along with metrics for that specific point in time.

## Retrieve Performance Data via API

The DigitalOcean API provides monitoring endpoints that cover various performance metrics, like bandwidth, CPU, and memory usage. The following code examples cover CPU usage.

## How to Get Droplet CPU Metrics Using the DigitalOcean API

[Create a personal access token](https://docs.digitalocean.com/reference/api/create-personal-access-token/index.html.md) and save it for use with the API.

### cURL

Send a GET request to [`https://api.digitalocean.com/v2/monitoring/metrics/droplet/cpu`](https://docs.digitalocean.com/reference/api/reference/monitoring/index.html.md#monitoring_get_DropletCpuMetrics).

Using cURL:

```shell
curl -X GET \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $DIGITALOCEAN_TOKEN" \
  "https://api.digitalocean.com/v2/monitoring/metrics/droplet/cpu?host_id=222651441&start=1636051668&end=1636051668"
```

### Python

Using [PyDo](https://github.com/digitalocean/pydo), the official DigitalOcean API client for Python:

```python
import os
from pydo import Client

client = Client(token=os.environ.get("DIGITALOCEAN_TOKEN"))

resp = client.monitoring.get_droplet_cpu_metrics(host_id="17209102", start="1620683817", end="1620705417")
```

To learn more, see [the monitoring endpoint of the DigitalOcean API](https://docs.digitalocean.com/reference/api/reference/monitoring/index.html.md).