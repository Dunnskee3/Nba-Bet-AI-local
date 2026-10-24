# Veezy.ai Studio

An AI art studio modeled on what OpenArt offers, with its own branding: turn prompts into images, keep characters consistent, and turn one sentence into an illustrated story. It is a single static `index.html` with no build step and no backend.

## Features

| Veezy.ai | Inspired by (OpenArt) | How it works |
|---|---|---|
| **Create**: prompt → 1–4 images, 9 style presets, 5 aspect ratios, seed, "avoid" list | Text-to-image across many models | Picks from three engines (below) |
| **✨ Enhance with Claude** | Prompt helper | Claude expands a short idea into a detailed image prompt |
| **Characters** | Character Builder | Saves a name, a fixed visual description and a seed. Both are added to every prompt that uses the character, so they look the same each time |
| **One-click story** | One-Click Story | Claude plans a 4–8 scene storyboard (title, narration, a prompt per frame) as structured JSON, then each scene is drawn with the same lead character and seed |
| **Library** | My creations | Every result is saved in the browser. Click to enlarge, reuse the prompt, download or delete |

### Engines

- **Flux / Turbo:** free image models from [Pollinations.ai](https://pollinations.ai). They need no key; images are loaded straight from a URL.
- **Vector:** Claude draws an SVG illustration, best for logos, icons and flat art. Needs an Anthropic key. The SVG is shown inside an `<img>` tag, so any script in it cannot run.

## Running

Open `index.html` in a browser, or serve the folder (`python3 -m http.server`). Flux and Turbo work right away. For Enhance, Story and Vector, click **⚙ Settings** and paste an Anthropic API key.

Claude calls use the official `@anthropic-ai/sdk` with `claude-opus-5-5`, adaptive thinking, and a server-side refusal fallback. Stories use structured outputs.

> The key is kept in browser storage and sent directly to Anthropic. That is fine for personal use. For a public launch, move the Claude calls behind your own backend and add accounts, credits and moderation.

## Not included yet (compared with OpenArt)

- Video generation, a community gallery, accounts and credits. These need a backend and paid video or image APIs.
- Model training on your own photos, inpainting, upscaling and background removal.
