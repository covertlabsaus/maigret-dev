+++
title = "Export Maigret Reports in Multiple Formats"
description = "Generate PDF, HTML, CSV, and JSON Maigret reports in a single run or automation pipeline."
draft = false
+++

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "@id": "https://maigret.dev/faq/maigret-export-multiple-formats",
    "name": "How can I export Maigret reports to PDF and HTML together?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Use report switches like --html --pdf --csv --json in one Maigret invocation and specify --output ./reports to collect the artifacts."
    }
  }]
}
</script>

Maigret renders reports client-side, so you can request any combination during a single scan.

## Command example

```bash
maigret username --html --pdf --json --csv --output ./reports --folderoutput
```

Resulting files land in `./reports/username/`:

- `username.html`
- `username.pdf`
- `username.json`
- `username.csv`

## Automating with cron

```bash
0 2 * * * /usr/local/bin/maigret userlist.txt \
  --input usernames.txt \
  --html --pdf --json \
  --output /var/reports --folderoutput >> /var/log/maigret.log 2>&1
```

## Python API snippet

```python
from pathlib import Path
from maigret import maigret_api

reports_dir = Path("reports")
results = maigret_api.search_username("username", report_types=["html", "pdf", "json"])
for artifact in results.artifacts:
    artifact.save(reports_dir)
```

## Quality checks
- Use `--no-color` to make terminal logs machine-parsable.
- Pair with `maigret --print-not-found` to reduce clutter before archiving.
- Validate PDFs with `pdfinfo reports/user.pdf` in CI.

Multi-format exports are ideal when stakeholders want human-readable HTML plus machine-readable JSON for pipeline ingestion.
