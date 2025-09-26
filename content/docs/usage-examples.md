+++
title = 'Usage Examples'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

Use Maigret from the command line, through the web interface, or as a Python library.

## CLI scenarios

1. Search the default top 500 sites (ranked by Alexa) for a username:

   ```bash
   maigret machine42
   ```

2. Search **all** sites in the database:

   ```bash
   maigret machine42 -a
   ```

   {{< callout type="info" >}}
   If you see a spike in false positives, install the latest development version and run `maigret --self-check` to disable problematic sites automatically.
   {{< /callout >}}

3. Generate HTML and PDF reports in one go:

   ```bash
   maigret machine42 -a --html --pdf
   ```

4. Focus on a single site entry:

   ```bash
   maigret machine42 --site Facebook
   ```

5. Parse an existing profile and continue the investigation with the discovered username:

   ```bash
   maigret --parse https://steamcommunity.com/profiles/76561199113454789
   ```

6. Limit the search to specific countries:

   ```bash
   maigret machine42 --tags us,jp
   ```

7. Limit the search to certain interests or site types:

   ```bash
   maigret machine42 --tags coding
   ```

8. Limit the search to a predefined engine (for example, uCoz forums):

   ```bash
   maigret machine42 --tags ucoz
   ```

## Web interface

Enable the built-in web UI to browse results visually and download reports:

```bash
maigret --web 5000
```

## Library mode

Integrate Maigret into your own tooling to receive structured JSON results:

```python
from maigret import maigret_api

results = maigret_api.search_username("machine42")
```
