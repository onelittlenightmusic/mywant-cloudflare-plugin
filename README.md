# mywant-cloudflare

A [MyWant](https://github.com/onelittlenightmusic/MyWant) plugin that adds the **Cloudflare Tunnel** want type.

Exposes a local service via a public URL using Cloudflare Tunnel (cloudflared).
Uses the built-in `live_server_management` agent under the hood.

## Requirements

- [MyWant](https://github.com/onelittlenightmusic/MyWant) installed and running
- [cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/) installed and available in `PATH`

## Installation

```sh
git clone https://github.com/onelittlenightmusic/mywant-cloudflare-plugin \
  ~/.mywant/custom-types/mywant-cloudflare-plugin
```

Then restart MyWant (`make restart-all` or `./bin/mywant stop && ./bin/mywant start -D`).

## Usage

```sh
# List available want types (confirm "cloudflare" appears)
mywant types list

# Deploy with default port 8080
mywant wants create -t cloudflare

# Deploy with custom args
mywant wants create -t cloudflare -p args='["tunnel","--url","http://localhost:3000"]'
```

## Parameters

| Name | Default | Description |
|------|---------|-------------|
| `port` | `"8080"` | Local port to expose |
| `args` | `'["tunnel","--url","http://localhost:8080"]'` | CLI arguments (JSON array) |
| `command` | `"cloudflared"` | Path to cloudflared binary |
| `url_regex` | `\|\s+(https://...trycloudflare\.com)\s+` | Regex to extract tunnel URL |
| `max_retries` | `40` | Max retries waiting for URL |
| `log_file` | `""` | Path to capture output (auto if empty) |

## State

After the want is achieved, the tunnel URL is available as:

- `current.server_url` — the tunnel URL
- `final_result` — same value, for use with `using` selectors
