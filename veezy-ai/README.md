# Veezy.ai Studio

Visuals for the culture. Veezy.ai is an AI art studio for independent rap and R&B artists, modeled on what OpenArt offers. It makes cover art, rollout visuals and music video treatments with a modern Afrocentric look and 90s hip-hop grit.

It is a single static `index.html` with no build step and no backend.

## Look and feel

- **Palette:** black, gold and cream, with kente stripes (gold / red / green) and a mudcloth line pattern in the background.
- **Texture and type:** film grain over everything, bold condensed Anton headings, and Permanent Marker tags.
- **Era looks:** the presets capture eras and aesthetics, never a specific real artist. Prompts tell Claude not to imitate anyone's likeness.

## Features

| Veezy.ai | What it does |
|---|---|
| **Create** | Describe the vibe, choose a look and a format, and get 1–4 variations |
| **Formats** | Cover art (1:1), Story / Reel (9:16), YouTube thumbnail (16:9), Show flyer (4:5), Merch graphic |
| **Drop pack** | One click makes a cover, story, thumbnail and flyer from the same vibe and seed, so the whole rollout matches |
| **Looks** | 90s West Coast, Golden Era NYC, Kente Royalty, Mudcloth Earth, Afrofuturism, R&B Velvet, Soul Painting, Street Mural, Y2K Chrome |
| **✨ Art-direct it** | Claude turns a rough idea into a detailed, culturally fluent image prompt |
| **✍ Rollout copy** | Claude writes a release caption, 8–12 hashtags and 3 rollout content ideas |
| **Cover maker** | Adds your artist name and title in real fonts (image models garble text), with an optional kente strip and an "Explicit" tag, then exports a PNG |
| **Artist personas** | Saves your look (skin tone, hair, fit, jewelry) and a fixed seed, so you look like you in every image |
| **Video treatment** | Song title plus concept or hook → Claude writes a treatment with a logline and shot-by-shot direction, and Veezy storyboards each shot starring your persona |
| **Vault** | Everything you make is saved in the browser |

### Engines

- **Flux / Turbo:** free image models from [Pollinations.ai](https://pollinations.ai). No key needed.
- **Vector:** Claude draws an SVG, best for logos and merch graphics. Needs an Anthropic key. The SVG is shown inside an `<img>` tag, so any script in it cannot run.

## Running

Open `index.html` in a browser, or serve the folder (`python3 -m http.server`). Flux and Turbo work right away. For art direction, rollout copy, video treatments and Vector, click **⚙ Settings** and paste an Anthropic API key.

Claude calls use the official `@anthropic-ai/sdk` with `claude-opus-5-5`, adaptive thinking, and a server-side refusal fallback. Treatments and rollout copy use structured outputs.

> The key is kept in browser storage and sent directly to Anthropic. That is fine for personal use. For a public launch, move the Claude calls behind your own backend and add accounts, credits and moderation.

## Content rules

Use only your own likeness or original characters. Don't make images of real artists without their consent, and don't use copyrighted logos or lyrics you don't own.

## Not included yet (compared with OpenArt)

- Video generation, a community gallery, accounts and credits. These need a backend and paid APIs.
- Training a model on your own photos, inpainting, upscaling and background removal.
