+++
title = 'Supported Identifier Types'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

Beyond plain usernames, Maigret recognises several identifiers that uniquely map to user profiles on specific platforms:

- `gaia_id` — Google internal numeric identifier (historically exposed in Google+ URLs).
- `steam_id` — Steam numeric account ID.
- `wikimapia_uid` — Wikimapia.org numeric identifier.
- `uidme_uguid` — uID.me numeric identifier.
- `yandex_public_id` — Yandex letter-based public identifier. See also [YaSeeker](https://github.com/HowToFind-bot/YaSeeker).
- `vk_id` — VK.com numeric user ID.
- `ok_id` — Odnoklassniki (ok.ru) numeric user ID.
- `yelp_userid` — Yelp internal identifier.

Where available, Maigret automatically follows those IDs to locate additional accounts and enrich the dossier.
