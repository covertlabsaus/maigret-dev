+++
title = 'Installation'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

Maigret can be installed from PyPI, built from source, or run inside a Docker container. If you do not want to install anything locally, you can use the official Telegram bot or one of the cloud notebook launchers.

## Windows standalone binaries

Ready-to-run executables are published in the [GitHub releases](https://github.com/soxoj/maigret/releases). A fresh build is produced automatically for every push to the `main` and `dev` branches. A short video walkthrough is available at <https://youtu.be/qIgwTZOmMmM>.

## Cloud shells and notebooks

Launch Maigret directly in the browser by opening one of the prepared environments:

- [Google Cloud Shell](https://console.cloud.google.com/cloudshell/open?git_repo=https://github.com/soxoj/maigret&tutorial=README.md)
- [Replit workspace](https://repl.it/github/soxoj/maigret)
- [Google Colab notebook](https://colab.research.google.com/gist/soxoj/879b51bc3b2f8b695abb054090645000/maigret-collab.ipynb)
- [Binder environment](https://mybinder.org/v2/gist/soxoj/9d65c2f4d3bec5dd25949197ea73cf3a/HEAD)

## Install from PyPI

> **Note**: Python 3.10+ is required (3.11 is recommended). The bundled site database in the PyPI package may lag behind the development version. If you see many false positives, install from GitHub instead.

```bash
# Install from PyPI
pip3 install maigret

# Run a search
maigret username
```

## Install the development version

```bash
# Clone and install locally
git clone https://github.com/soxoj/maigret
cd maigret
pip3 install .

# Or install straight from GitHub
pip3 install git+https://github.com/soxoj/maigret.git

# If you plan to hack on Maigret, install Poetry and use its venv
pip3 install poetry
poetry run maigret
```

## Docker images

```bash
# Pull the official image (tracks the development branch)
docker pull soxoj/maigret

# Mount a local reports directory while running
docker run -v /mydir:/app/reports soxoj/maigret:latest username --html

# Build a local image
docker build -t maigret .
```

## Telegram bot

An officially maintained [Telegram bot](https://t.me/osint_maigret_bot) exposes the latest Maigret features without any local setup. Its source code lives at [soxoj/maigret-tg-bot](https://github.com/soxoj/maigret-tg-bot).
