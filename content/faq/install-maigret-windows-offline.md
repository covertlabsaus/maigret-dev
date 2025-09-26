+++
title = "Install Maigret on Windows Without Internet"
description = "Bundle Maigret dependencies for an offline Windows deployment using virtual environments and wheel caches."
draft = false
+++

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "@id": "https://maigret.dev/faq/install-maigret-windows-offline",
    "name": "How do I install Maigret on Windows when the machine has no internet access?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Download Maigret wheels on an online workstation with pip download, copy them via removable media, and install offline using pip install --no-index --find-links <wheelhouse>."
    }
  }]
}
</script>

Offline environments (lab networks, air-gapped hosts) require staged installation.

## Prepare on an online workstation

```powershell
mkdir C:\maigret-wheelhouse
pip download maigret -d C:\maigret-wheelhouse
```

Include optional extras:

```powershell
pip download "maigret[tor]" -d C:\maigret-wheelhouse
```

Zip the folder and transfer it via approved media.

## Install offline

```powershell
Expand-Archive .\maigret-wheelhouse.zip C:\maigret-wheelhouse
python -m venv C:\maigret
C:\maigret\Scripts\Activate.ps1
pip install --no-index --find-links C:\maigret-wheelhouse maigret
```

## Verify

```powershell
maigret --version
maigret johndoe --top-sites 50 --html
```

## Optional Tor bundle
- Install the [Tor Expert Bundle](https://www.torproject.org/download/tor/) offline by copying the ZIP.
- Configure `torrc` to run a local SOCKS proxy for Maigret usage.

## Diagram

```mermaid
flowchart LR
    A[Online workstation] --> B[pip download wheelhouse]
    B --> C[USB drive]
    C --> D[Air-gapped Windows host]
    D --> E[pip --no-index install]
```

Keep the wheelhouse updated after every Maigret release to patch dependencies promptly.
