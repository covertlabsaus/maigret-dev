+++
title = 'Usage'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

Run Maigret from the command line to search for usernames, parse profile pages, or export structured reports.

## Basic workflow

```bash
# Search for one or more usernames on the default top 500 sites
maigret username1 username2

# Search all sites in the database (slower)
maigret username --all-sites
```

Maigret prints live progress while contacting sites, highlighting confirmed accounts and extracted data points.

## Filtering targets

- `--tags photo,dating` — limit the scan to specific categories or country codes.
- `--site Facebook` — restrict the search to a single site entry.
- `--top-sites 100` — reduce the search scope to the fastest 100 entries.
- `--self-check` — disable sites that currently produce false positives.

A full reference is available in the [command line options](/docs/command-line-options) page.

## Parsing existing profiles

```bash
# Parse a public profile and launch follow-up searches
maigret --parse https://twitter.com/example
```

The parser extracts usernames, IDs, social links, and metadata from known profile formats. Those identifiers are queued automatically for recursive searches when `--recursive` is enabled.

## Reports and exports

```bash
# Generate multiple report formats
maigret username --html --pdf --csv --json

# Store output in a specific folder
maigret username --output ./reports
```

Report formats include HTML, PDF, XMind, CSV, JSON, and plaintext. Use `--folderoutput` to separate results per username.

## Web interface

```bash
# Launch the built-in web UI
maigret --web 5000
```

Navigate to <http://127.0.0.1:5000> to explore results in a graph view, browse extracted metadata, and download reports.

## Automation and APIs

Maigret exposes a lightweight Python API for embedding searches in your own tools:

```python
from maigret import maigret_api

result = maigret_api.search_username("username")
```

See the [development guide](/docs/development) for deeper integration examples and test tooling.
