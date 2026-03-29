# mywant-cloudflare

A [MyWant](https://github.com/onelittlenightmusic/mywant) plugin that adds the `cloudflare` want type.

Manages a Cloudflare Tunnel (`cloudflared`) lifecycle to expose a local service via a public URL.
Automatically starts the cloudflared process, parses the Quick Tunnel URL from its output, and stores it in state.

## Requirements

- [MyWant](https://github.com/onelittlenightmusic/mywant) installed and running
- [cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/) installed and available in `PATH`

## Installation

```sh
mkdir -p ~/.mywant/custom-types
curl -o ~/.mywant/custom-types/cloudflare_tunnel.yaml \
  https://raw.githubusercontent.com/onelittlenightmusic/mywant-cloudflare-plugin/main/cloudflare_tunnel.yaml
```

Or manually copy `cloudflare_tunnel.yaml` to `~/.mywant/custom-types/`.
The type is loaded automatically on next server start, or register it without restart:

```sh
mywant types create -f ~/.mywant/custom-types/cloudflare_tunnel.yaml
```

## Usage

```yaml
metadata:
  name: my-tunnel
  type: cloudflare
spec:
  params:
    port: "3000"
```

```sh
mywant wants create -f my-tunnel.yaml
```

## Parameters

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `port` | string | `"8080"` | Local port to expose |
| `protocol` | string | `"http"` | Protocol for the local service |
| `command` | string | `"cloudflared"` | Path to cloudflared binary |
| `args` | string | `'["tunnel","--url","http://localhost:8080"]'` | CLI arguments (JSON array) |
| `max_retries` | int | `40` | Max retries waiting for URL |
| `log_file` | string | `""` | Path to capture output (auto if empty) |
