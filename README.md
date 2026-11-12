# bangla-iptv

Auto-updated JSON list of Bangladesh and Indian Bangla IPTV channels (720p and up, including sports).

- `bangla_channels.json` – the generated list (updated automatically)
- `fetch_channels.py` – builds the list from iptv-org playlists and your own repo files
- `.github/workflows/update-channels.yml` – refreshes the JSON every 12 hours

## Use in your app

```
https://raw.githubusercontent.com/<user>/<repo>/main/bangla_channels.json
```

Shape: `{ total, byCountry, channels[] }`. Each channel has `name`, `id`, `country`,
`resolution`, `logo`, `group`, `geoBlocked`, `url`, and optionally `userAgent` / `referrer`.

## Setup

1. Unzip, then push the files to a new GitHub repo (make sure the hidden `.github` folder is included).
2. That's it. The first push starts the workflow, then it runs every 12 hours and commits the updated JSON.
3. (Optional) Add your own playlists to `MY_REPO_SOURCES` in `fetch_channels.py`.

If a run fails with a permission error: **Settings -> Actions -> General -> Workflow permissions** -> *Read and write permissions*.
You can also start a run anytime: **Actions -> Update channels -> Run workflow**.

## Run locally

```
python fetch_channels.py                    # 720p+ (default)
python fetch_channels.py --min-res 1080     # 1080p only
python fetch_channels.py --filter-mine      # also filter your own entries
```

Streams are public and can go offline or be geo-blocked at any time.
