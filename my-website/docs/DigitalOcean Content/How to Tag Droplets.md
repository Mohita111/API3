---
title: How to Tag Droplets
description: Organize Droplets with tags to group and filter Droplets by role, automatically include Droplets in firewall or load balancer configurations, or …
product: Droplets
url: https://docs.digitalocean.com/products/droplets/how-to/tag/
last_updated: "2026-04-15"
---

> **For AI agents:** The documentation index is at [https://docs.digitalocean.com/llms.txt](https://docs.digitalocean.com/llms.txt). Markdown versions of pages use the same URL with `index.html.md` in place of the HTML page (for example, append `index.html.md` to the directory path instead of opening the HTML document).
>

# How to Tag Droplets

DigitalOcean Droplets are Linux-based virtual machines (VMs) that run on top of virtualized hardware. Each Droplet you create is a new server you can use, either standalone or as part of a larger, cloud-based infrastructure.

Tags are custom labels you can apply to Droplets and other DigitalOcean resources. You can filter tagged Droplets, automatically include Droplets in [DigitalOcean Firewall](https://docs.digitalocean.com/products/networking/firewalls/index.html.md) or [Load Balancer](https://docs.digitalocean.com/products/networking/load-balancers/index.html.md) configurations by tag, create [monitoring alert policies](https://docs.digitalocean.com/products/monitoring/how-to/manage-alerts/index.html.md#create-control) for groups of tagged Droplets, and use the [DigitalOcean API](https://docs.digitalocean.com/products/droplets/reference/index.html.md) to initiate an action across multiple Droplets with the same tag.

Choosing terms that describe a Droplet’s function can help you locate and administer Droplets that share common roles. For example, you might tag Droplets by:

- **Environment**, like production, staging, or development.
- **Application**, like web servers (Apache) or database servers (MariaDB).
- **Purpose**, like a project name or any other key term that describes the use of the Droplet.
- **Person**, like the individual or team responsible for managing the Droplet.

You can add tags to Droplets during or after creation.

## Limits

- Tags must be a single word containing only letters, numbers, colons, dashes, and underscores.

## Known Issues

- You cannot edit existing tags. Instead, create a new tag, apply it to the appropriate resources, and delete the old one.
- Tag names are case stable, which means the capitalization you use when you first create a tag is canonical.

  - Tagged resources in the Control Panel always display the canonical capitalization. For example, if you create a tag named `PROD`, you can tag resources in the Control Panel by entering `prod`. The tag still displays with its canonical capitalization, `PROD`.
  - When working with [tags in the API](https://docs.digitalocean.com/reference/api/reference/index.html.md), you must use the tag’s canonical capitalization. For example, if you create a tag named `PROD`, the URL to add that tag to a resource would be `https://api.digitalocean.com/v2/tags/PROD/resources` (not `/v2/tags/prod/resources`).

## Tag Existing Droplets

To add or modify tags for an existing Droplet, you can:

- Open the Droplet’s detail page, click the **Settings** tab, scroll to the **Tags** section, and click **Edit**.
- Click **Actions** on the Droplet’s detail page and select **Edit tags** (or **Add tags** if the Droplet has none).
- Click the **More** menu next to the Droplet on the Droplets list and select a tag option.

The **Manage Tags** window opens.

![Manage Tags window with tag chip, search field, Save Tags button, and Cancel link.](https://docs.digitalocean.com/screenshots/droplets/manage-tags-window.63b15949c89aa20093ac614995fac8d1fb393f53ac671fa4e1ba941d693723a3.png)

Add tags by pressing `SPACEBAR` or `ENTER` after each term. Navigate between tags with the arrow keys, and remove the highlighted tag with `DELETE` or the last tag on the list with `BACKSPACE`.

When you’re done, click **Save Tags**.

## Tag Droplets During Creation

To add tags while creating a new Droplet, at the bottom of the [Droplet create page](https://cloud.digitalocean.com/droplets/new), look for the **Finalize Details** section.

![Finalize Details on the create page with quantity, hostname fields, Tags with a tag chip and Enter tag name, project selector, and clear all link.](https://docs.digitalocean.com/screenshots/droplets/create/finalize-details.9bc23460776a82fadd42cb36ec8dde12e121a3d172ff2c47dd527f9bb889784b.png)

In the **Tags** field, enter the tags. Add multiple tags by pressing `SPACEBAR` or `ENTER` after each term. Navigate between tags with the arrow keys, and remove the highlighted tag with `DELETE` or the last tag on the list with `BACKSPACE`.

## Automate Tagging

When tagging a Droplet via API, you need to have already [created a tag](https://docs.digitalocean.com/reference/api/reference/tags/index.html.md#tags_create). This is not necessary when using `doctl`, the CLI.

## How to Add a Tag to a Droplet Using the DigitalOcean CLI

1. [Install `doctl`](https://docs.digitalocean.com/reference/doctl/how-to/install/index.html.md), the official DigitalOcean CLI.
2. [Create a personal access token](https://docs.digitalocean.com/reference/api/create-personal-access-token/index.html.md) and save it for use with `doctl`.
3. Use the token to grant `doctl` access to your DigitalOcean account.```shell
   doctl auth init
   ```

The following example applies the tag `frontend` to a Droplet with the ID `386734086`:

```shell
doctl compute droplet tag 386734086 --tag-name frontend
```

## How to Tag a Resource Using the DigitalOcean API

[Create a personal access token](https://docs.digitalocean.com/reference/api/create-personal-access-token/index.html.md) and save it for use with the API.

### cURL

Send a POST request to [`https://api.digitalocean.com/v2/tags/{tag_id}/resources`](https://docs.digitalocean.com/reference/api/reference/tags/index.html.md#tags_assign_resources).

Using cURL:

```shell
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $DIGITALOCEAN_TOKEN" \
  -d '{"resources":[{"resource_id":"9569411","resource_type":"droplet"},{"resource_id":"7555620","resource_type":"image"},{"resource_id":"3d80cb72-342b-4aaa-b92e-4e4abb24a933","resource_type":"volume"}]}' \
  "https://api.digitalocean.com/v2/tags/awesome/resources"
```

### Go

Using [Godo](https://github.com/digitalocean/godo), the official DigitalOcean API client for Go:

```go
import (
    "context"
    "os"

    "github.com/digitalocean/godo"
)

func main() {
    token := os.Getenv("DIGITALOCEAN_TOKEN")

    client := godo.NewFromToken(token)
    ctx := context.TODO()

    opt := &godo.ListOptions{
        Page:    1,
        PerPage: 200,
    }
    tags, _, err := client.Tags.List(ctx, opt)
}
```

### Ruby

Using [DropletKit](https://github.com/digitalocean/droplet_kit), the official DigitalOcean API client for Ruby:

```ruby
require 'droplet_kit'
token = ENV['DIGITALOCEAN_TOKEN']
client = DropletKit::Client.new(access_token: token)

client.tags.tag_resources(name: 'awesome', resources: [{ resource_id: '9569411', resource_type: 'droplet' },{ resource_id: '7555620', resource_type: 'image' },{ resource_id: '3d80cb72-342b-4aaa-b92e-4e4abb24a933', resource_type: 'volume'}])
```

### Python

Using [PyDo](https://github.com/digitalocean/pydo), the official DigitalOcean API client for Python:

```python
import os
from pydo import Client

client = Client(token=os.environ.get("DIGITALOCEAN_TOKEN"))

req = {
  "resources": [
    {
      "resource_id": "9569411",
      "resource_type": "droplet"
    },
    {
      "resource_id": "7555620",
      "resource_type": "image"
    },
    {
      "resource_id": "3d80cb72-342b-4aaa-b92e-4e4abb24a933",
      "resource_type": "volume"
    }
  ]
}

resp = client.tags.assign_resources(tag_id="awesome", body=req)
```