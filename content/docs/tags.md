+++
title = 'Tags'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

Tags narrow the Maigret site database to a subset that matches your investigation goals.

{{< callout type="warning" >}}
Tag assignments are still evolving. Expect occasional changes while the database matures.
{{< /callout >}}

## Tag types

1. **Country codes** — ISO 3166-1 alpha-2 values such as `us`, `jp`, or `br`. They capture the dominant language or region. Sites that are truly global may omit country tags altogether.
2. **Site engines** — platform identifiers like `uCoz`, `vBulletin`, or `XenForo` help you concentrate on specific communities.
3. **Topics and verticals** — categories for areas of interest (`coding`, `crypto`, `photo`, etc.). The canonical list currently lives in the [source code](https://github.com/soxoj/maigret/blob/main/maigret/sites.py#L13).

## Usage examples

```bash
# Search on US and Japanese sites
maigret username --tags us,jp

# Search across developer-focused destinations
maigret username --tags coding

# Search only uCoz-powered communities
maigret username --tags ucoz
```
