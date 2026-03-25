# pi-google-search

Google Search extension for [pi](https://github.com/badlogic/pi-mono) coding agent. Uses Gemini's grounded search to return AI-synthesized answers with source URLs.

Based on [GSD-2](https://github.com/gsd-build/gsd-2)'s google-search extension, adapted for standalone use.

## Install

```bash
pi install npm:pi-google-search
```

## Setup

Two auth options:

### Option 1: API Key (standard pricing)
```bash
export GEMINI_API_KEY=your_key
```
Get one at [Google AI Studio](https://aistudio.google.com/apikey).

### Option 2: Google OAuth (free — uses Cloud Code Assist credits)
Log in to Google in pi. The extension auto-detects the `google-gemini-cli` OAuth token — no API key needed. Uses Google Cloud Code Assist credits which are included free with any Google Cloud account.

## Usage

The extension registers a `google_search` tool that the agent calls automatically when it needs web information.

```
> What's the latest version of Next.js?
```

The agent will use `google_search` behind the scenes and return an answer with cited sources.

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
| `GEMINI_API_KEY` | Gemini API key (option 1) | — |
| `GEMINI_SEARCH_MODEL` | Gemini model to use | `gemini-2.5-flash` |

If neither `GEMINI_API_KEY` nor Google OAuth is configured, the tool will show an error with setup instructions.

The TUI renderer shows which auth method is active: `api_key` or `free` (OAuth).

## License

MIT
