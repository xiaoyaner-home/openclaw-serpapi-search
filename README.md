# SerpApi Search Provider for OpenClaw

An [OpenClaw](https://github.com/openclaw/openclaw) plugin that adds [SerpApi](https://serpapi.com/) as a web search provider with **vertical search routing** — the LLM automatically picks the best search vertical (News, Scholar, Images, Shopping, Maps, etc.) as part of its normal `web_search` tool call.

## Features

- **20+ search verticals** via a single `engine` parameter
- **Zero extra LLM calls** — the model picks the vertical naturally
- **Google + alternative engines** (Bing, Baidu, Yandex, Naver, DuckDuckGo)
- **Structured results** with titles, URLs, descriptions, ratings, prices, citations
- **Freshness filtering** for Google engines (past day/week/month/year)

## Supported Engines

| Engine            | Alias        | What it searches   |
| ----------------- | ------------ | ------------------ |
| `google`          | (default)    | Regular web search |
| `google_news`     | `news`       | News articles      |
| `google_scholar`  | `scholar`    | Academic papers    |
| `google_images`   | `images`     | Image search       |
| `google_shopping` | `shopping`   | Products & prices  |
| `google_maps`     | `maps`       | Local places & POI |
| `google_jobs`     | `jobs`       | Job listings       |
| `google_finance`  | `finance`    | Financial data     |
| `google_patents`  | `patents`    | Patent search      |
| `youtube`         | `youtube`    | YouTube videos     |
| `bing`            | `bing`       | Bing web search    |
| `baidu`           | `baidu`      | Baidu (Chinese)    |
| `yandex`          | `yandex`     | Yandex (Russian)   |
| `naver`           | `naver`      | Naver (Korean)     |
| `duckduckgo`      | `duckduckgo` | DuckDuckGo         |

## Installation

### Via npm (recommended)

```bash
openclaw plugins install @xiaoyaner/openclaw-serpapi-search
```

### Manual (local path)

Clone this repo and add to your OpenClaw config:

```json
{
  "plugins": {
    "load": {
      "paths": ["./path/to/openclaw-serpapi-search"]
    }
  }
}
```

## Configuration

Add to your `openclaw.json`:

```json
{
  "plugins": {
    "entries": {
      "serpapi-search": {
        "enabled": true,
        "config": {
          "apiKey": "your-serpapi-api-key"
        }
      }
    }
  },
  "tools": {
    "web": {
      "search": {
        "provider": "serpapi"
      }
    }
  }
}
```

Or set the environment variable:

```bash
export SERPAPI_API_KEY="your-serpapi-api-key"
```

### Config Options

| Option          | Env Var           | Default    | Description                                    |
| --------------- | ----------------- | ---------- | ---------------------------------------------- |
| `apiKey`        | `SERPAPI_API_KEY`  | —          | Your SerpApi API key ([get one](https://serpapi.com/manage-api-key)) |
| `defaultEngine` | —                 | `google`   | Default engine when LLM doesn't specify one    |

## Usage

Once installed, `web_search` calls are routed through SerpApi. The LLM selects verticals naturally:

- "Search for recent AI news" → LLM picks `engine: "news"`
- "Find papers on transformer architecture" → LLM picks `engine: "scholar"`
- "How much does iPhone 16 cost" → LLM picks `engine: "shopping"`
- "Coffee shops near Times Square" → LLM picks `engine: "maps"`
- General questions → default `engine: "google"`

## Pricing

SerpApi offers a free tier with 100 searches/month. Paid plans start at $50/month for 5,000 searches. See [serpapi.com/pricing](https://serpapi.com/pricing).

## License

MIT
