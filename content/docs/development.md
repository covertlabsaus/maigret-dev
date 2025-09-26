+++
title = 'Development'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

## Frequently asked questions

### Where can I see the supported site list?

- Human-readable: [`sites.md`](https://github.com/soxoj/maigret/blob/main/sites.md)
- Machine-readable: [`maigret/resources/data.json`](https://github.com/soxoj/maigret/blob/main/maigret/resources/data.json)

The Markdown list is generated automatically from the JSON database.

### Which check methods are supported?

`checkType` values in `data.json` describe how Maigret verifies accounts:

- `message` — look for `presenceStrs` and ensure none of the `absenceStrs` appear.
- `status_code` — require a successful HTTP status.
- `response_url` — confirm there is no redirect and the response status is 2xx.

Implementation details live in [`checking.py`](https://github.com/soxoj/maigret/blob/main/maigret/checking.py#L339).

## Test setup

Use Python 3.10 for local development.

```bash
poetry install --with dev

# Static checks
make lint

# Auto-format
make format

# Run tests with coverage report
make test
open htmlcov/index.html

# Inspect startup performance
make speed
```

## Fixing false positives

1. Enable the Git hook that updates statistics: `git config --local core.hooksPath .githooks/`.
2. Identify the problematic site (use a random username such as `laiuhi3h4gi3u4hgt` or the [Telegram bot](https://t.me/osint_maigret_bot)).
3. Inspect the live profile page:
   - If the service is gone, remove it from `data.json`.
   - If the layout changed, update `checkType`, `presenceStrs`, or `absenceStrs`.
   - If authentication is required, set `disabled: true`.
4. Update the entry manually or run the automatic analyser:

   ```bash
   maigret --submit https://my.mail.ru/bk/alex
   ```

5. To disable checks quickly, run:

   ```bash
   maigret --self-check --site My.Mail.ru@bk.ru
   ```

6. Debug responses with:

   ```bash
   maigret soxoj --site My.Mail.ru@bk.ru -d 2> response.txt
   ```

Helpful fields in `data.json`:

- `engine` — predefined behaviour for known platforms (forums, etc.).
- `headers` — extra headers to send.
- `requestHeadOnly` — use HEAD requests when possible.
- `regexCheck` — validate usernames with regular expressions.

## Activation mechanism

Some sites require runtime activation (cookies, JWT tokens, etc.). For example, the Vimeo entry triggers a function that fetches a fresh token when a "Something strange occurred" marker appears. The sequence is:

1. A request to `urlProbe` fails with a known error message.
2. The activation handler defined in [`activation.py`](https://github.com/soxoj/maigret/blob/main/maigret/activation.py) runs.
3. The handler obtains a new token and updates the in-memory headers.
4. The next retry succeeds with the refreshed credentials.

See the Vimeo implementation in the source for a complete pattern.

## Releasing a new version

> Maintainer permissions are required. Contact @soxoj for access.

1. Create a release branch with the next version number (increment the patch component unless there are breaking changes).
2. Update the version in:
   - `pyproject.toml`
   - `maigret/__version__.py`
   - `docs/source/conf.py`
   - `snapcraft.yaml`
3. Update the changelog.
4. Open a GitHub release — the CI pipeline will publish the package to PyPI automatically.

Example branch: <https://github.com/soxoj/maigret/commit/e520418f6a25d7edacde2d73b41a8ae7c80ddf39>

Example release tag: <https://github.com/soxoj/maigret/releases/tag/v0.4.1>
