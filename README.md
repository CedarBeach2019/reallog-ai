<p align="center">
  <img src="https://raw.githubusercontent.com/Lucineer/capitaine/master/docs/capitaine-logo.jpg" alt="Capitaine" width="120">
</p>

<h1 align="center">reallog-ai</h1>

<p align="center">An AI-assisted journal that helps you notice patterns in your own writing over time.</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> ·
  <a href="#features">Features</a> ·
  <a href="#the-fleet">The Fleet</a> ·
  <a href="https://github.com/Lucineer/reallog-ai/issues">Issues</a>
</p>

---

Most journal apps are text boxes with timestamps. You write, it saves. Finding your own long-term patterns is manual work.

reallog-ai is a simple companion that reads your entries and surfaces connections you might have missed—recurring worries, subtle progress, or topics that resurface across weeks.

It doesn't tell you what to think. It quietly shows you what you've been thinking.

## Why this exists

Many AI journals are SaaS products that hold your data on their servers. This is a self-contained agent you deploy and control. Your entries stay within your own Cloudflare Worker, and you choose which LLM provider processes them. There is no middleman service.

## How it works

This is an open-source vessel in the Cocapn fleet. You fork it, deploy it, and it runs independently. It can optionally receive non-breaking updates from the fleet, but you can also disable this and modify any part of the code yourself.

**Live Instance:** [reallog-ai](https://reallog-ai.casey-digennaro.workers.dev) · MIT Licensed · Runs on Cloudflare Workers

Built with [Capitaine](https://github.com/Lucineer/capitaine) · [Cocapn](https://github.com/Lucineer/cocapn)

---

## Quick Start

1.  **Fork this repository.** This becomes your own copy.
2.  Deploy to Cloudflare Workers:
    ```bash
    npx wrangler deploy
    ```
    You will need to set `DEEPSEEK_API_KEY` (or another provider's key) as a secret.

Your journal is now running on your own Worker.

## Features

- **Self-hosted privacy:** Journal data never passes through external servers.
- **Pattern recognition:** Highlights thematic connections across your past entries.
- **Multi-model support:** Works with DeepSeek, OpenAI, Anthropic, or other compatible LLM APIs.
- **Simple deployment:** Single Worker file, no external database or additional services.
- **Configurable updates:** Optionally receive improvements via the Cocapn fleet protocol.

## One Limitation

Pattern recognition depends on the context window and reasoning capabilities of your chosen LLM provider. Deeper insights may require a capable model.

## Architecture

A standard Cocapn vessel. The logic is contained in a readable TypeScript Worker:
- `src/worker.ts` – Handles requests, sessions, and fleet coordination.
- `lib/pattern.ts` – Contains the reflection and connection logic.
- `lib/byok.ts` – Routes prompts to your configured LLM provider.

## The Fleet

reallog-ai is part of the Cocapn Fleet, a collection of specialized autonomous vessels. Fleet members can share non-breaking updates and improvements.

<div align="center">
  <br>
  <a href="https://the-fleet.casey-digennaro.workers.dev">The Fleet</a> · <a href="https://cocapn.ai">Cocapn</a>
  <br><br>
  <sub>Attribution: Superinstance & Lucineer (DiGennaro et al.)</sub>
</div>