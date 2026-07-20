# Changelog

All notable user-facing changes to RMS Threads Assistant are documented in this file.

## [0.1.0] — 2026-07-21

First public desktop release.

### Added

* **Desktop app** for macOS (Apple Silicon), Windows, and Linux (.deb / .rpm / AppImage).
* **Threads accounts** — connect with your own Meta App credentials; OAuth and token custody go through the RMS edge so access tokens never stay on the device.
* **Projects & replies** — find Threads posts by keyword, draft expert replies with LLM providers, and publish through the app.
* **Posts & planner** — schedule original posts and reply slots; publication history with delete support.
* **Media** — image and carousel attachments for posts.
* **Telegram moderation** — optional Telegram integration for review workflows.
* **Licensing** — 5-day local trial, then activate a key from [license.rms-ds.com](https://license.rms-ds.com/dashboard/shop). About and status bar show status, expiry, and Buy / Manage license links. Countdown appears when five or fewer days remain.
* **In-app updates** — check and install updates from About → Updates (macOS, Windows, Linux AppImage). `.deb` / `.rpm` installs update by downloading a newer package.
* **Themes & languages** — light / dark / system theme; English, Russian, German, French, Spanish, Italian, Georgian.
* **System tray** — keep the app in the tray; show or quit from the menu.

### Fixed

* Meta authorization errors when deleting, searching, or discovering profiles (missing OAuth scopes).
* Hide/manage reply failing on posts that are not yours.
* Edge token refresh so connected accounts stay valid longer without re-login.

### Notes

* Downloads: [public releases](https://github.com/max-ramas/rms-threads-assistant-public/releases/latest).
* Purchase / renew: [RMS License shop](https://license.rms-ds.com/dashboard/shop).
* Android and iOS are planned; not included in this release.
