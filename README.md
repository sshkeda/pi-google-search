# pi-google-search

[![npm version](https://img.shields.io/npm/v/pi-google-search)](https://www.npmjs.com/package/pi-google-search)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Give your [pi](https://github.com/badlogic/pi-mono) coding agent real-time web search — powered by Gemini's grounded search. Returns AI-synthesized answers with cited source URLs. Free to use with Google OAuth.

## Features

- 🔍 Real-time Google Search via Gemini grounded search
- 📝 AI-synthesized answers with cited source URLs
- 🔑 Two auth options: Gemini API key or free Google OAuth
- ⚡ Per-session result caching — identical queries cost nothing
- 🎨 Custom TUI rendering with search progress and source count
- 🛡️ 30-second timeout protection against hanging requests
- 🔄 Automatic retry on rate limits and server errors (OAuth path)

## Install

```bash
pi install npm:pi-google-search
```

## Setup

### Option 1: Google OAuth (free — recommended)

Run `/login` in pi and select **Google Gemini CLI**. The extension auto-detects the OAuth token — no API key needed. Uses Google Cloud Code Assist credits which are included free with any Google Cloud account.

### Option 2: API Key (standard pricing)

```bash
export GEMINI_API_KEY=your_key
```

Get one at [Google AI Studio](https://aistudio.google.com/apikey).

## Usage

The extension registers a `google_search` tool that the agent calls automatically when it needs web information.

```
> What's the latest version of Next.js?
```

The agent will use `google_search` behind the scenes and return a cited answer:

```
Next.js 16.2 was released in March 2026 with ~400% faster dev server startup
and ~50% faster rendering...

Sources:
[1] nextjs.org - https://nextjs.org/blog/next-16-2
[2] npmjs.com - https://www.npmjs.com/package/next
[3] wikipedia.org - https://en.wikipedia.org/wiki/Next.js

Searches performed: "latest version of Next.js", "Next.js current stable release"
```

### Manual tool call

```
google_search({ query: "Next.js 15 app router changes" })
```

## How it works

1. Sends your query to Gemini Flash with `googleSearch` grounding enabled
2. Gemini performs real Google searches internally
3. Returns an AI-synthesized answer + source URLs from grounding metadata
4. Results are cached per-session — identical queries are free

## Configuration

| Environment Variable | Description | Default |
|---|---|---|
| `GEMINI_API_KEY` | Gemini API key (option 2) | — |
| `GEMINI_SEARCH_MODEL` | Gemini model to use | `gemini-2.5-flash` |

If neither `GEMINI_API_KEY` nor Google OAuth is configured, the tool will show an error with setup instructions.

The TUI renderer shows which auth method is active: `api_key` or `free` (OAuth).

## Requirements

- [pi coding agent](https://github.com/badlogic/pi-mono) (`@mariozechner/pi-coding-agent`)
- Node.js 20+
- A Google account (for OAuth) or Gemini API key

## Credits

Based on [GSD-2](https://github.com/gsd-build/gsd-2)'s google-search extension by [Lex Christopherson](https://github.com/gsd-build), adapted for standalone use as a pi package.

## License

[MIT](LICENSE)
