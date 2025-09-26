+++
title = 'Command Line Options'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

# Command line options

## Usernames

`maigret username1 username2 ...`

You can specify several usernames separated by space. Usernames are **not** mandatory as there are other operations modes (see below).

## Parsing of account pages and online documents

`maigret --parse URL`

Maigret will try to extract information about the document/account owner (including username and other ids) and will make a search by the extracted username and ids.

## Main options

Options are also configurable through settings files.

### Filtering and Search Options

`--tags` - Filter sites for searching by tags: sites categories and two-letter country codes (**not a language!**). E.g. photo, dating, sport; jp, us, global. Multiple tags can be associated with one site. **Warning**: tags markup is not stable now.

`-n`, `--max-connections` - Allowed number of concurrent connections **(default: 100)**.

`-a`, `--all-sites` - Use all sites for scan **(default: top 500)**.

`--top-sites` - Count of sites for scan ranked by Alexa Top **(default: top 500)**.

`--timeout` - Time (in seconds) to wait for responses from sites **(default: 30)**. A longer timeout will be more likely to get results from slow sites. On the other hand, this may cause a long delay to gather all results.

### Authentication and Cookies

`--cookies-jar-file` - File with custom cookies in Netscape format (aka cookies.txt). You can install an extension to your browser to download own cookies ([Chrome](https://chrome.google.com/webstore/detail/get-cookiestxt/bgaddhkoddajcdgocldbbfleckgcbcid), [Firefox](https://addons.mozilla.org/en-US/firefox/addon/cookies-txt/)).

### Output Options

`--html` - Generate HTML report with results.

`--pdf` - Generate PDF report with results.

`--xmind` - Generate XMind map with results.

`--csv` - Generate CSV file with results.

`--txt` - Generate simple text file with results.

`-o`, `--output` - Output directory for reports **(default: ./reports)**.

`--no-color` - Disable colored output.

`--print-not-found` - Print sites where the username was not found.

### Advanced Options

`--recursive` - Enable recursive search by found usernames and ids.

`--no-extracting` - Disable extraction of personal info from found accounts.

`--proxy` - Proxy server (e.g., socks5://127.0.0.1:9050 for Tor).

`--db` - Path to the Maigret database file.

`--folderoutput` - Create a folder for every username.

## Usage Examples

### Basic search
```bash
maigret johndoe
```

### Search with specific options
```bash
# Search on all sites with 5-second timeout
maigret johndoe -a --timeout 5

# Search only photo and dating sites
maigret johndoe --tags photo,dating

# Generate all report formats
maigret johndoe --html --pdf --csv --txt

# Search multiple users with custom output folder
maigret user1 user2 user3 -o /path/to/reports

# Search using Tor proxy
maigret johndoe --proxy socks5://127.0.0.1:9050
```

### Parse account pages
```bash
# Extract info from social media profile
maigret --parse https://twitter.com/username

# Extract info from any webpage
maigret --parse https://example.com/about
```

### Web interface
```bash
# Start web interface on port 5000
maigret --web 5000
```

## Configuration Files

You can configure default options using JSON configuration files:

```json
{
  "timeout": 10,
  "max_connections": 50,
  "tags": ["photo", "social"],
  "print_not_found": false
}
```

Save as `~/.config/maigret/settings.json` (Linux/Mac) or `%APPDATA%\maigret\settings.json` (Windows).