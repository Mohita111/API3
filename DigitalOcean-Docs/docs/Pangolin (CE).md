---
title: Pangolin (CE)
description: Pangolin is an open-source, identity-based remote access platform built on WireGuard that enables secure, seamless connectivity to private and public …
product: Marketplace
url: https://docs.digitalocean.com/products/marketplace/catalog/pangolin-ce/
last_updated: "2026-03-18"
---

> **For AI agents:** The documentation index is at [https://docs.digitalocean.com/llms.txt](https://docs.digitalocean.com/llms.txt). Markdown versions of pages use the same URL with `index.html.md` in place of the HTML page (for example, append `index.html.md` to the directory path instead of opening the HTML document).

# Pangolin (CE)

Generated on 18 Mar 2026 from [the Pangolin (CE) catalog page](https://marketplace.digitalocean.com/apps/pangolin-ce-1)

Pangolin is an open-source, identity-based remote access platform built on WireGuard that enables secure, seamless connectivity to private and public resources. Pangolin combines reverse proxy and VPN capabilities into one platform, providing browser-based access to web applications and client-based access to any private resources, all with zero-trust security and granular access control.

![](https://github.com/fosrl/pangolin/blob/main/public/screenshots/hero.png?raw=true)

## Software Included

| Package | Version | License |
|---|---|---|
| [Pangolin](https://github.com/fosrl/pangolin) | latest | ALGP-3.0 |
| [Docker CE](https://docs.docker.com/engine/install/ubuntu/) | 28.5.1 | Apache License, Version 2.0 |

## Creating an App using the Control Panel

Click the **Deploy to DigitalOcean** button to create a Droplet based on this 1-Click App. If you aren’t logged in, this link will prompt you to log in with your DigitalOcean account.

[![Deploy to DO](https://www.deploytodo.com/do-btn-blue.svg)](https://cloud.digitalocean.com/droplets/new?image=fossorial-pangolince1)

## Creating an App using the API

In addition to creating a Droplet from the Pangolin (CE) 1-Click App using the control panel, you can also use the [DigitalOcean API](https://docs.digitalocean.com/reference/api). As an example, to create a 4GB Pangolin (CE) Droplet in the SFO2 region, you can use the following `curl` command. You need to either save your [API access token](https://docs.digitalocean.com/reference/api/create-personal-access-token/index.html.md) to an environment variable or substitute it in the command below.

```shell
curl -X POST -H 'Content-Type: application/json' \
         -H 'Authorization: Bearer '$TOKEN'' -d \
        '{"name":"choose_a_name","region":"sfo2","size":"s-2vcpu-4gb","image":"fossorial-pangolince1"}' \
        "https://api.digitalocean.com/v2/droplets"
```

## Getting Started After Deploying Pangolin (CE)

## Pangolin Deployment Guide

This guide walks you through deploying and configuring Pangolin using the DigitalOcean Marketplace 1-Click App.

## Deployment Steps

### 1. Create a Droplet from the Marketplace

1. Log in to your [DigitalOcean account](https://cloud.digitalocean.com/).
2. Navigate to the Marketplace and search for “Pangolin”.
3. Click on the Pangolin 1-Click App.
4. Configure your Droplet:- Choose a plan (recommended: at least 1 CPU and 1GB RAM; it can be deployed on DigitalOcean’s $6 s-1vcpu-1gb)

   - Select a datacenter region
   - Add SSH keys for authentication
   - Choose a hostname (e.g., pangolin-server)
5. Click “Create Droplet”.

### 2. DNS Configuration

Before proceeding with setup, you need to configure your domain to point to your new Droplet:

1. Obtain your Droplet’s IP address from the DigitalOcean control panel.
2. Go to your domain registrar or DNS provider.
3. Create an A record that points your domain or subdomain to your Droplet’s IP address.

```
Type: A
   Name: pangolin (or @ for root domain)
   Value: your_droplet_ip
   TTL: 3600 (or as low as possible for faster propagation)
```

4. Wait for DNS propagation (can take 5 minutes to several hours).

### 3. Initial Setup

1. Once your Droplet is created, connect to it via SSH:

```
ssh root@your_droplet_ip
```

2. The first-login setup script will run automatically, guiding you through the initial configuration:

   - Enter your domain name
   - Provide your email for SSL certificates
   - The script will run the Pangolin installer
   - The script will generate an admin sign-up secret for you to use on your first login
3. After the installer completes, you’ll be able to access the Pangolin dashboard.

### 4. Dashboard Setup

1. Open a web browser and navigate to `https://your-domain.com`.
2. Follow the on-screen instructions to:

   - Create an admin account using the sign-up secret provided during setup
   - Set up your organization
   - Configure your first site and resources

### 5. Security Considerations

- The Pangolin Droplet comes with UFW firewall pre-configured to allow only necessary ports.
- Set up 2FA for your admin account in the Pangolin dashboard.
- Regularly update your Pangolin installation with the latest security patches.

### 6. Maintenance and Updates

To update Pangolin in the future:

1. SSH into your Droplet:

```
ssh root@your_droplet_ip
```

2. Follow the docs for how to update the containers: [https://docs.pangolin.net/self-host/how-to-update](https://docs.pangolin.net/self-host/how-to-update)

## Troubleshooting

### Cannot Access Dashboard

1. Verify DNS configuration with `dig your-domain.com`.
2. Check that your domain points to your Droplet’s IP address.
3. Ensure SSL certificates were issued correctly:

```
cd /opt/pangolin
   docker compose logs traefik
```

4. Check firewall settings on both the Pangolin server and remote site.
5. Verify network connectivity with `ping` or `traceroute`.

## Need Help?

- Documentation: [https://docs.pangolin.net](https://docs.pangolin.net)
- GitHub: [https://github.com/fosrl/pangolin](https://github.com/fosrl/pangolin)
- Discord: [https://pangolin.net/discord](https://pangolin.net/discord)
- Email Support: [support@pangolin.net](mailto:support@pangolin.net)