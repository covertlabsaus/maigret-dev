+++
title = 'Features'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

# Features

This is the list of Maigret features.

## Web Interface

You can run Maigret with a web interface, where you can view the graph with results and download reports of all formats on a single page.

![Web interface: how to start](https://raw.githubusercontent.com/soxoj/maigret/main/static/web_interface_screenshot_start.png)

![Web interface: results](https://raw.githubusercontent.com/soxoj/maigret/main/static/web_interface_screenshot.png)

Instructions:

1. Run Maigret with the `--web` flag and specify the port number.

```console
maigret --web 5000
```

2. Open http://127.0.0.1:5000 in your browser and enter one or more usernames to make a search.

3. Wait a bit for the search to complete and view the graph with results, the table with all accounts found, and download reports of all formats.

## Personal info gathering

Maigret does the [parsing of accounts webpages and extraction](https://github.com/soxoj/socid-extractor) of personal info, links to other profiles, etc.
Extracted info displayed as an additional result in CLI output and as tables in HTML and PDF reports.
Also, Maigret use found ids and usernames from links to start a recursive search.

Enabled by default, can be disabled with `--no extracting`.

```text
$ python3 -m maigret soxoj --timeout 5
    [-] Starting a search on top 500 sites from the Maigret database...
    [!] You can run search by full list of sites with flag `-a`
    [*] Checking username soxoj on:
    [+] Habr: https://habr.com/en/users/soxoj/
    [*] Extracting information from https://habr.com/en/users/soxoj/
    [+] extracted ids: ['albarabanov', 'Alexander Barabanov']
    [+] extracted usernames: ['soxoj']
    [+] Disqus: https://disqus.com/by/soxoj/
    [+] GitHub: https://www.github.com/soxoj
    [+] GitLab: https://gitlab.com/soxoj
    [+] HackerNews: https://news.ycombinator.com/user?id=soxoj
    [+] HackerOne: https://hackerone.com/soxoj
    [+] Reddit: https://reddit.com/user/soxoj
    [+] Telegram: https://t.me/soxoj
    [+] TikTok: https://tiktok.com/@soxoj
    [+] about.me: https://about.me/soxoj
```

## PDF and XMind Reports

Maigret can generate reports in PDF and XMind formats.

```console
# Generate PDF report
maigret username --pdf

# Generate XMind report
maigret username --xmind
```

![PDF report example](https://raw.githubusercontent.com/soxoj/maigret/main/static/report_alexaimephotography_html_screenshot.png)

![XMind report example](https://raw.githubusercontent.com/soxoj/maigret/main/static/report_alexaimephotography_xmind_screenshot.png)

## Tags and filtering

You can filter sites by tags (categories and countries):

```console
# Search only photo and dating sites
maigret username --tags photo,dating

# Search only US-based sites
maigret username --tags us

# Search only social networks
maigret username --tags social
```

## Recursive search

Maigret automatically searches for new usernames and IDs found during the initial search:

```console
# Enable recursive search (may take longer)
maigret username --recursive
```

## Tor and I2P support

Search through Tor and I2P networks:

```console
# Search using Tor proxy
maigret username --proxy socks5://127.0.0.1:9050

# Search I2P sites
maigret username --tags i2p
```

## API integration

Maigret supports API integration for automated workflows:

```python
from maigret import maigret_api

results = maigret_api.search_username("username")
```