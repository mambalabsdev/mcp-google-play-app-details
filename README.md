# Google Play App Details MCP Server

[![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-google-play-app-details/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-google-play-app-details) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-google-play-app-details%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-google-play-app-details&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-google-play-app-details)](https://www.npmjs.com/package/@mambalabsdev/mcp-google-play-app-details) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-google-play-app-details)](https://www.npmjs.com/package/@mambalabsdev/mcp-google-play-app-details) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-google-play-app-details)](https://github.com/mambalabsdev/mcp-google-play-app-details/blob/main/LICENSE)

An MCP server for the Mamba Labs Google Play App Details actor on Apify. Google Play app pages as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes Android package names, Play URLs, or developer names and returns one row per app with its Google Play details: rating, ratings by star, installs, price, category, developer contact links, and update date.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-google-play-app-details": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-google-play-app-details"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `get_google_play_app_details` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Get the Google Play rating, installs, and last update date for com.spotify.music and com.duolingo."
- "List every Google Play app by the developer Spotify AB with its rating and install band."

## Tool

`get_google_play_app_details`. One tool. Example arguments:

```json
{
  "apps": [
    "com.spotify.music"
  ]
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `apps` | array | no | Android package names (com.spotify.music) or Google Play app URLs (https://play.google.com/store/apps/details?id=com.spotify.music). |
| `developers` | array | no | Optional. Developer names exactly as an app page shows them (Spotify AB), numeric developer IDs, or developer page URLs. The developer's apps are read in page order. One developer per item; a name may hold commas. |
| `country` | string | no | 2 letter country code for the store (gl), for example US, GB, DE. Prices, currency, and availability follow it. Default US. |
| `language` | string | no | Page language (hl), for example en, de, pt_BR. Descriptions and labels follow it. Default en. |
| `max_apps_per_developer` | number | no | Apps to read from each developer page, in page order. Default 20, maximum 100. |
| `include_description` | boolean | no | true (default) or false. false leaves the long description empty to keep rows small. The price is the same. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `app-row`, one app with its details | $0.002 | $0.0019 | $0.0018 | $0.0017 |
| `apify-actor-start`, per run start | $0.004 | $0.004 | $0.004 | $0.004 |

Developer summaries, missing apps, refused pages, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/google-play-app-details](https://apify.com/mambalabs/google-play-app-details)

## License

MIT. See [LICENSE](LICENSE).
