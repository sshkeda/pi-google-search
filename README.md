# pi-google-search

Google Search extension for [pi](https://github.com/badlogic/pi-mono) coding agent. Uses Gemini's grounded search to return AI-synthesized answers with source URLs.

Based on [GSD-2](https://github.com/gsd-build/gsd-2)'s google-search extension, adapted for standalone use.

## Install

```bash
pi install npm:pi-google-search
```

## Setup

Set your Gemini API key:

```bash
export GEMINI_API_KEY=your_key
```

Get one at [Google AI Studio](https://aistudio.google.com/apikey).

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
| `GEMINI_API_KEY` | **Required.** Your Gemini API key | — |
| `GEMINI_SEARCH_MODEL` | Gemini model to use | `gemini-2.5-flash` |

## License

MIT
