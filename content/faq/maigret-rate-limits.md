+++
title = "Handle Maigret Site Rate Limits Gracefully"
description = "Tweak Maigret concurrency, retries, and proxies when remote services throttle username checks."
draft = false
+++

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "@id": "https://maigret.dev/faq/maigret-rate-limits",
    "name": "What should I do when Maigret keeps hitting rate limits?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Reduce --max-connections, increase --timeout, enable retries, and route traffic through backoff-aware proxies such as Tor or rotating gateways to respect remote rate limits."
    }
  }]
}
</script>

Some providers cap anonymous traffic. Maigret lets you dial down concurrency and add pauses so scans still complete.

## Quick adjustments

```bash
maigret username \
  --max-connections 20 \
  --timeout 60 \
  --retries 3 \
  --pause 1.5
```

Settings explained:
- `--max-connections`: limit simultaneous requests.
- `--timeout`: allow slower responses when backed up.
- `--retries`: retry transient 429/5xx responses.
- `--pause`: add seconds between batch launches.

## Rotating proxies

```bash
ALL_PROXY="socks5://127.0.0.1:9050" \
maigret username --proxy socks5://127.0.0.1:9050
```

Or plug into a managed pool:

```bash
maigret username --proxy http://user:pass@rotating-proxy.example:8080 --pause 2
```

## Respect crawl delays
Check the `robots.txt` of each site. If a service specifies `Crawl-delay: 5`, set `--pause 5` to align.

## Observe backoff signals

```mermaid
sequenceDiagram
    participant M as Maigret
    participant S as Target Site
    M->>S: GET /username
    S-->>M: HTTP 429
    M->>M: wait exponential backoff
    M->>S: Retry after headers
    S-->>M: HTTP 200 or 429
```

Repeated 429s mean you should pause longer or disable the site via `maigret --self-check --site Target`.

## Logging advice
- Add `--debug` to inspect headers for `Retry-After` values.
- Aggregate logs across runs to identify chronic offenders.
- Consider scheduling scans off-peak when services are less busy.

Following the site's published limitations keeps your OSINT activity sustainable.
