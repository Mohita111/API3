---
title: OpenLIT-----
description: OpenLIT is an open-source observability and monitoring platform for AI and LLM-based applications. It helps developers and data teams track, debug, …
product: Marketplace
url: https://docs.digitalocean.com/products/marketplace/catalog/openlit/
last_updated: "2025-11-13"
---

> **For AI agents:** The documentation index is at [https://docs.digitalocean.com/llms.txt](https://docs.digitalocean.com/llms.txt). Markdown versions of pages use the same URL with `index.html.md` in place of the HTML page (for example, append `index.html.md` to the directory path instead of opening the HTML document).

# OpenLIT

Generated on 13 Nov 2025 from [the OpenLIT catalog page](https://marketplace.digitalocean.com/apps/openlit)

OpenLIT is an open-source observability and monitoring platform for AI Agents and LLMs. It helps developers and data teams track, debug, and optimize their generative AI workloads with real-time visibility into prompts, token usage, latency, cost, and performance.

Every action performed by an AI agent is captured, analyzed, and visualized; helping teams understand how agents reason, make decisions, and interact with models or tools.

## Features

- **AI Agent & LLM Observability**: Collect traces, metrics, and logs across LLMs, vector databases, and APIs.
- **Prompt Management**: Version and organize prompts using the built-in Prompt Hub.
- **Cost & Usage Analytics**: Track tokens, requests, and GPU usage to manage your AI spend effectively.
- **Error & Exception Tracking**: Automatically capture and trace exceptions to improve debugging.
- **Secrets Management**: Securely store API keys and environment variables within the platform.
- **Fleet Hub (powered by OpAMP)**: Manage, update, and monitor all OpenTelemetry collectors and configurations at scale.
- **OpenTelemetry-Native Integration**: Built entirely on the OpenTelemetry standard for consistent data collection and analysis.

## Software Included

| Package | Version | License |
|---|---|---|
| [OpenLIT](https://openlit.io/) | [1.15.0](https://github.com/openlit/openlit) | [Apache License 2.0](https://github.com/openlit/openlit/blob/main/LICENSE) |

## Creating an App using the Control Panel

Click the **Deploy to DigitalOcean** button to install a Kubernetes 1-Click Application. If you aren’t logged in, this link will prompt you to log in with your DigitalOcean account.

[![Deploy to DO](https://www.deploytodo.com/do-btn-blue.svg)](https://cloud.digitalocean.com/kubernetes/clusters?app_id=ecaeee693101174e7c5c6eb9&referrer=https%3A%2F%2Fmarketplace.digitalocean.com&activation_redirect=%2Fkubernetes%2Fclusters%3Fapp_id%3Decaeee693101174e7c5c6eb9%26referrer%3Dhttps%253A%252F%252Fmarketplace.digitalocean.com)

## Creating an App using the API

In addition to creating OpenLIT using the control panel, you can also use the [DigitalOcean API](https://docs.digitalocean.com/reference/api). As an example, to create a 3 node DigitalOcean Kubernetes cluster made up of Basic Droplets in the SFO2 region, you can use the following `doctl` command. You need to authenticate with `doctl` with your [API access token](https://docs.digitalocean.com/reference/api/create-personal-access-token/index.html.md) and replace the `$CLUSTER_NAME` variable with the chosen name for your cluster in the command below.

```shell
doctl kubernetes clusters create --size s-4vcpu-8gb $CLUSTER_NAME --1-clicks openlit
```

## Getting Started After Deploying OpenLIT

## Prerequisites

- A DigitalOcean Kubernetes cluster (1.19+)
- kubectl configured to connect to your cluster
- doctl CLI tool installed and configured
- Helm 3.x installed

## Connect to Your Cluster

Follow the [DigitalOcean Kubernetes connection guide](https://docs.digitalocean.com/products/kubernetes/how-to/connect-to-cluster/index.html.md) to connect to your cluster with kubectl.

## Install OpenLIT Add-on

The OpenLIT add-on will be automatically installed in your cluster through the DigitalOcean Marketplace.

## Verify OpenLIT Installation

### Check Helm Installation Status

First, check if the Helm installation was successful by running the following command:

```
helm ls -n openlit
```

You should see output similar to:

```
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
openlit openlit         1               2025-11-13 13:42:16.68552 +0530 IST     deployed        openlit-1.15.1  1.15.0
```

## Access OpenLIT

## Port Forwarding

To quickly access OpenLIT:

```
kubectl port-forward -n openlit svc/openlit 3000:3000
```

Then open your browser and navigate to `http://localhost:3000`

## LoadBalancer

By default, OpenLIT services are LoadBalancer type.

You can get the external LoadBalancer IP:

```
kubectl get service openlit -n openlit
```

Then open your browser and navigate to `http://<external-lb-ip>:3000`

## Login to OpenLIT

Login to OpenLIT using the default credentials

- Email as ‘[user@openlit.io](mailto:user@openlit.io)’
- Password as ‘openlituser’

## Send Telemetry to OpenLIT

Once you have your OpenLIT URL, you can configure the `openlit` SDK or OpenLIT Operator to automatically send LLM and Agent observability data to OpenLIT at the `4318` port.

You can follow these quickstart guides:

- **Zero Code Observability with OpenLIT Operator**: [https://docs.openlit.io/latest/operator/quickstart](https://docs.openlit.io/latest/operator/quickstart)
- **LLM and Agent Observability**: [https://docs.openlit.io/latest/openlit/quickstart-ai-observability](https://docs.openlit.io/latest/openlit/quickstart-ai-observability)
- **MCP Monitoring**: [https://docs.openlit.io/latest/openlit/quickstart-mcp-observability](https://docs.openlit.io/latest/openlit/quickstart-mcp-observability)
- **AI Evals**: [https://docs.openlit.io/latest/sdk/quickstart-programmatic-evals](https://docs.openlit.io/latest/sdk/quickstart-programmatic-evals)
- **AI Guardrails**: [https://docs.openlit.io/latest/openlit/quickstart-guard](https://docs.openlit.io/latest/openlit/quickstart-guard)
- **GPU Monitoring**: [https://docs.openlit.io/latest/openlit/quickstart-gpu](https://docs.openlit.io/latest/openlit/quickstart-gpu)

## Next Steps

- [Setup Automatic Evaluation of AI responses and actions](https://docs.openlit.io/latest/openlit/quickstart-evals)
- [Manage OpenTelemetry Collectors using Fleet Hub](https://docs.openlit.io/latest/openlit/observability/fleet-hub)
- [Version, edit, deploy prompts collaboratively using Prompt Hub](https://docs.openlit.io/latest/openlit/prompts-experiments/prompt-hub)
- [Compare cost, duration, and response tokens across LLMs to choose the most efficient model for your use case](https://docs.openlit.io/latest/openlit/prompts-experiments/openground)
- [Create powerful, interactive dashboards to monitor AI application performance](https://docs.openlit.io/latest/openlit/dashboards/overview)
- [Centrally store LLM API keys that applications can retrieve remotely without restarts for seamless key rotation](https://docs.openlit.io/latest/openlit/developer-resources/vault)

## Support

- Join OpenLIT’s community Slack - [Invite Link](https://join.slack.com/t/openlit/shared_invite/zt-2etnfttwg-TjP_7BZXfYg84oAukY8QRQ)
- OpenLIT’s Official Documentation - [docs.openlit.io](https://docs.openlit.io/latest/overview)