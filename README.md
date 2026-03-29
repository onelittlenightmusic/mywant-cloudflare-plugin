# mywant-cloudflare

A [MyWant](https://github.com/onelittlenightmusic/mywant) plugin that adds the **Cloudflare Tunnel** recipe.

Exposes a local service via a public URL using Cloudflare Tunnel (cloudflared).
Uses the built-in `managed_process` want type under the hood.

## Requirements

- [MyWant](https://github.com/onelittlenightmusic/mywant) installed and running
- [cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/) installed and available in `PATH`

## Installation

```sh
cd ~/.mywant/recipes
git clone https://github.com/onelittlenightmusic/mywant-cloudflare-plugin
```

The recipe is loaded automatically on next server start, or register it without restart:

```sh
mywant recipes create -f ~/.mywant/recipes/mywant-cloudflare-plugin/cloudflare_tunnel.yaml
```

## Usage

```sh
# List available recipes (confirm "Cloudflare Tunnel" appears)
mywant recipes list

# Deploy with default port 8080
mywant wants create --recipe "Cloudflare Tunnel"

# Deploy with custom port
mywant wants create --recipe "Cloudflare Tunnel" -p port=3000
```

## Update

```sh
cd ~/.mywant/recipes/mywant-cloudflare-plugin && git pull
```

## Parameters

| Name | Default | Description |
|------|---------|-------------|
| `port` | `"8080"` | Local port to expose |
| `protocol` | `"http"` | Protocol for the local service |
| `command` | `"cloudflared"` | Path to cloudflared binary |
| `args` | `'["tunnel","--url","http://localhost:8080"]'` | CLI arguments (JSON array) |
| `max_retries` | `40` | Max retries waiting for URL |
| `log_file` | `""` | Path to capture output (auto if empty) |
