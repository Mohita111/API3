---
title: Bitwarden
description: A password management tool for individuals, teams, and business organizations.
product: Marketplace
url: https://docs.digitalocean.com/products/marketplace/catalog/bitwarden/
last_updated: "2026-06-11"
---

> **For AI agents:** The documentation index is at [https://docs.digitalocean.com/llms.txt](https://docs.digitalocean.com/llms.txt). Markdown versions of pages use the same URL with `index.html.md` in place of the HTML page (for example, append `index.html.md` to the directory path instead of opening the HTML document).

# Bitwarden

Generated on 11 Jun 2026 from [the Bitwarden catalog page](https://marketplace.digitalocean.com/apps/bitwarden)

Bitwarden is an open source password management tool that allows you to securely store, share, and sync passwords and other senitive data. No matter what platform or environment you use, Bitwarden offers an array of official, high quality client applications that can easily connect to your self-hosted Bitwarden server.

## Software Included

| Package | Version | License |
|---|---|---|
| Bitwarden | [2026.6.0](https://github.com/bitwarden/server/releases) | [AGPL v3](https://github.com/bitwarden/server/blob/master/LICENSE.txt) |

## Creating an App using the Control Panel

Click the **Deploy to DigitalOcean** button to create a Droplet based on this 1-Click App. If you aren’t logged in, this link will prompt you to log in with your DigitalOcean account.

[![Deploy to DO](https://www.deploytodo.com/do-btn-blue.svg)](https://cloud.digitalocean.com/droplets/new?image=bitwarden)

## Creating an App using the API

In addition to creating a Droplet from the Bitwarden 1-Click App using the control panel, you can also use the [DigitalOcean API](https://docs.digitalocean.com/reference/api). As an example, to create a 4GB Bitwarden Droplet in the SFO2 region, you can use the following `curl` command. You need to either save your [API access token](https://docs.digitalocean.com/reference/api/create-personal-access-token/index.html.md) to an environment variable or substitute it in the command below.

```shell
curl -X POST -H 'Content-Type: application/json' \
         -H 'Authorization: Bearer '$TOKEN'' -d \
        '{"name":"choose_a_name","region":"sfo2","size":"s-2vcpu-4gb","image":"bitwarden"}' \
        "https://api.digitalocean.com/v2/droplets"
```

## Getting Started After Deploying Bitwarden

Before you begin with your Bitwarden 1-Click Droplet, you will need to obtain:

1. A hostname (domain or subdomain) where you can create a DNS record pointing to your Droplet’s IP address
2. A Bitwarden installation ID and key from [https://bitwarden.com/host/](https://bitwarden.com/host/). Bitwarden requires at least 2GB of RAM, so make sure to choose a plan with enough memory during creation. After you create your Bitwarden 1-Click Droplet, Bitwarden’s dependencies and installation scripts will be preinstalled and ready for you to use. You will need to connect to the Droplet via SSH to complete the setup.`ssh root@your_droplet_public_ipv4`

Once you connect, you’ll be prompted to complete Bitwarden’s installation. Provide the hostname that you will use (be sure you have setup the DNS record), your installation ID and key, and answer the questions about how you will configure SSL with your Bitwarden installation. Bitwarden requires a secure HTTPS connection to operate. The installer can generate a self-signed certificate for you if you do not have one.

After you have completed the installation, you can visit your Bitwarden domain in a web browser, register a Bitwarden user account, and log in.

Your Bitwarden 1-Click Droplet has also been preconfigured with automatic updates so you won’t need to worry about keeping the Bitwarden server application up to date. Update checks will occur weekly.

Finally, application settings (such as a SMTP mail server) can be configured in `/root/bwdata/env/global.override.env`. If you need to make changes to your server’s installation settings, you can do so in `/root/bitwarden/bwdata/config.yml`.

More information on managing your Bitwarden server can be found at [https://help.bitwarden.com/hosting/](https://help.bitwarden.com/hosting/).