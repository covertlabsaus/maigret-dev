+++
title = 'Settings'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

{{< callout type="warning" >}}
The settings system is experimental and may change between releases.
{{< /callout >}}

Maigret reads configuration files in the following order (later files override earlier values):

1. `resources/settings.json` — bundled with the installed package.
2. `~/.maigret/settings.json` — per-user configuration.
3. `./settings.json` — project-specific overrides in the current working directory.

Missing files are ignored silently.

Refer to the [default settings template](https://github.com/soxoj/maigret/blob/main/maigret/resources/settings.json) for supported keys. Typical options control concurrency, timeouts, tag filters, report formats, and proxy configuration.
