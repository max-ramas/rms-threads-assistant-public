# RMS Threads Assistant
 
<div align="center">
<p>
  <img alt="Latest release" src="https://img.shields.io/github/v/release/max-ramas/rms-threads-assistant-public?label=release">
  <img alt="Downloads" src="https://img.shields.io/github/downloads/max-ramas/rms-threads-assistant-public/total">
  <img alt="Platform" src="https://img.shields.io/badge/platform-macOS%20%7C%20Windows%20%7C%20Linux%20%7C%20Android-blue">
  <img alt="Built with Tauri" src="https://img.shields.io/badge/built%20with-Tauri%202-24C8DB?logo=tauri&logoColor=white">
  <img alt="Rust" src="https://img.shields.io/badge/backend-Rust-000000?logo=rust&logoColor=white">
  <img alt="React" src="https://img.shields.io/badge/frontend-React%2019-61DAFB?logo=react&logoColor=black">
  <img alt="TypeScript" src="https://img.shields.io/badge/-TypeScript-3178C6?logo=typescript&logoColor=white">
  <img alt="License" src="https://img.shields.io/badge/license-commercial-lightgrey">
</p>
</div>

**A local-first desktop app that helps you show up on Threads consistently — without living in the app.**

RMS Threads Assistant finds conversations relevant to your brand or niche on Threads, drafts on-brand AI replies for your review, and gives you a full planner for scheduling your own original posts and threads — all from a desktop app that keeps your credentials on your machine, not on someone else's server.

> This repository ships **binary releases only** — no source code. See [Releases](../../releases) for downloads.

## Download

| Platform | Download |
|---|---|
| macOS (Apple Silicon) | [.dmg](../../releases/latest) |
| Windows | [.msi, .exe](../../releases/latest) |
| Linux | [.deb](../../releases/latest) / [.rpm](../../releases/latest) / [AppImage](../../releases/latest) |
| Android | coming soon |
| iOS | coming soon |

> **Note on updates:** macOS, Windows, and Linux AppImage builds auto-update in-app. `.deb`/`.rpm` installs need a manual re-download from Releases.

[**→ All releases**](../../releases)

---

**Known issue on macOS:** the app currently launches with an "app is damaged" warning on first run — this isn't a corrupted file, it's Gatekeeper's standard check for apps distributed outside the App Store. We're sorry for the inconvenience — this will be resolved once notarization with Apple is complete. In the meantime, here's how to open it:

**Option 1** — System Settings → Privacy & Security → scroll down to the Security section → click "Open Anyway" next to the RMS Threads Assistant entry, then confirm with your password.

**Option 2** (if Option 1 didn't work or the button isn't there) — open Terminal and run:
```
xattr -r -d com.apple.quarantine /Applications/RMS\ Threads\ Assistant.app
```

---

## Why it exists

Growing a presence on Threads means two things: replying to the right conversations before they go cold, and posting your own content consistently. Both are time sinks if you do them manually, and most "growth" tools either scrape data in ways that risk your account or route your credentials through someone else's backend.

RMS Threads Assistant does neither. It talks to Threads only through the **official Threads API**, and your Meta access token never leaves your device unencrypted — it's stored in your OS keychain.

## What it does

### 🔍 Reply pipeline
- Searches Threads for posts matching keywords you define
- Runs each candidate through a 3-stage pipeline: relevance pre-filter → reply generation → toxicity/safety gate
- Drafts above your confidence threshold can auto-publish; everything else goes to a manual approval queue
- **We recommend keeping full-auto mode off.** It's available, but a human glance before publishing is worth the extra thirty seconds.

### 📅 Planner & Scheduler
- Compose original posts and multi-post threads, with auto-split by sentence and optional (1/5)-style numbering
- Schedule to a specific date and time, or publish instantly — one unified queue, no separate "instant" vs "scheduled" code paths to worry about
- Multi-image carousels (2–20 images per post)
- Full calendar view of what's queued and what's already gone out

### 📱 Telegram remote control
- Approve, edit, reject, publish-now, or reschedule drafts from your phone
- No need to open the desktop app to keep the pipeline moving

### 🧠 Bring your own model
- OpenAI, Anthropic, OpenRouter, and other providers supported (11 total)
- Per-token cost tracking so you know what each reply actually costs you

### 🔒 Local-first, with the fewest possible exceptions
- Meta OAuth token stored only on a minimal edge service, never on your desktop — your device holds an opaque account reference, not the token itself
- LLM requests go straight from your device to your chosen provider
- Rate limits respected automatically: publishing pauses at 80% of Meta's daily caps before you'd hit a block
- Credentials live in your OS keychain only — never exposed in raw form over internal app messaging; outbound requests are timeout- and origin-guarded

### 🌍 Cross-platform
macOS, Windows, and Linux today, with an Android build already available as a direct APK download below (no Play Store required). iOS is in progress, pending Apple Developer Program enrollment. Interface available in English, Russian, German, French, Spanish, Italian, and Georgian.

## Setup

RMS Threads Assistant runs on **your own Meta Developer app**, not a shared one:

1. [Download the latest release](../../releases) for your platform
2. Create a Meta Developer app and get your own `client_id` / `client_secret` (takes a few minutes — guide linked in-app)
3. Enter them in Settings and connect your Threads account
4. Define a search config (or start with the Planner if you just want to post)

Using your own app credentials means you're never sharing rate limits or API quota with anyone else's traffic.

## Licensing

Free 5-day trial, no credit card required. After that:

| Plan | Price |
|---|---|
| 1 month | €19 |
| 3 months | €49 |
| 6 months | €89 |
| 12 months | €159 |

[Get a license →](https://license.rms-ds.com/dashboard/shop)

## Support

Issues and feature requests: use the [Issues](../../issues) tab on this repo.

---

<div align="center">
<sub>Built by <a href="https://ramzaeff.com">Maksim Ramzaev</a> · <a href="https://rms-ds.com">RMS Digital Services</a></sub>
</div>
