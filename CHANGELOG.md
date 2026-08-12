# Changelog

All notable user-facing changes to RMS Threads Assistant are documented in this file.

## [1.0.3] — 2026-08-12

### Fixed

* **Reply search pacing** — each scheduler tick searches one comma-separated phrase in round-robin order instead of fanning out the full list; daily caps advance the schedule without a 60-second retry loop.
* **Transient Meta throttling** — rate-limit, 502, and 503 responses keep the cadence alive and store a diagnostic note instead of permanently stopping the reply configuration.
* **Telegram polling recovery** — startup clears stale webhooks, unexpected dispatcher exits restart, manual restart lets the old `getUpdates` call release, and up to 20 pending drafts are re-notified.
* **Newer database startup** — a database migrated by a newer build now produces a clear user-facing error and clean exit instead of a Rust panic/macOS crash report; user data is not modified.

### Added

* **Exclude keywords** — reply configurations can filter comma-separated terms from both manual and scheduled search; forward-only migration `20260723000008` and all seven locales are included.
* **Regression coverage** — keyword parsing/rotation, exclude filtering, transient throttling, and safe startup-error messaging.

### Verification

* TypeScript, locale parity (555 keys), IPC contract (75 commands), Vitest 12/12, Rust 43 passed + 1 ignored live test, strict Clippy, and production frontend/Tauri app builds passed.

## [0.1.2] — 2026-07-22

### Fixed

* **Generated-post publish command** — `publish_approved_post` is registered in Tauri's `generate_handler!`, so publishing a generated post from Moderation no longer fails with an unknown command.
* **Media path confinement** — persisted chain media must resolve to a canonical descendant of `app_data/media`; absolute paths, `..`, and symlink escapes are rejected, with JPEG/PNG signature and 1 byte–8 MB size validation before staging and publishing.
* **Duplicate reply publication** — an atomic `pending|approved|failed → publishing` claim prevents concurrent or replayed IPC calls from starting a second publish.
* **Strict Clippy regression** — safety-score parsing uses `rfind`, restoring a clean `cargo clippy --all-targets -- -D warnings` run on current stable Rust.
* **Honest publish feedback** — Planner toasts show the real outcome (`published` / `partial` / `failed` / quota deferred), not “started”.
* **Stuck `publishing` chains** — early publish errors no longer leave a chain frozen; stuck chains can be marked failed and retried; scheduler recovers chains stuck >15 minutes.
* **Planner media IPC** — `filePath`/`sourceUrl` camelCase (and snake_case aliases) so attached images persist correctly.
* **Empty History / Analytics for Planner posts** — published chain segments appear in History and insights refresh.
* **Dashboard zeros after Planner publish** — account overview includes Planner chain status counts separately from the AI reply pipeline; SQLite `SUM` uses `COALESCE` so empty tables do not crash the IPC.
* **Analytics stuck at zeros** — insights refresh runs automatically when Analytics opens; toasts report success/failure; Meta Graph `{data:[…]}` insights JSON is parsed before flat edge JSON so zeros are not silently accepted.
* **LLM score mis-parse** — relevance/safety scores prefer JSON and fail closed (ignore `v2.0` / `Step 1` / `Rule 5` traps that could auto-approve unsafe content).
* **Chain daily limits** — local post/reply counters and Meta quota snapshots increment after each successful segment so a long chain cannot overshoot remaining quota in one run.
* **Telegram approve burns quota on network failure** — daily counters increment only after Meta accepts the publish.
* **Orphan LLM keys** — deleting an account also removes `openrouter` / `ollama` keychain entries.
* **Silent license IPC failure** — failed `get_license_status` shows a toast and an in-app banner.
* **Blocking media upload I/O** — `upload_media` reads files with `tokio::fs::read` instead of sync `std::fs::read` on the async runtime.
* **Publication slot timezone drift** — `slot_at` stored/compared in UTC (one-shot migrate from legacy local wall-clock); Calendar still shows local times.
* **Setup-path SQLite `block_on`** — Keychain warm, Telegram token, and minimize-to-tray load off the Tauri setup path so a slow DB/keychain cannot freeze first paint.
* **Stacked chain numbering** — re-split / numbering toggle no longer piles `(1/3) (1/3)…`; markers are stripped before apply; edit composer opens with a single clean suffix.
* **Locale parity** — de/es/fr/it/ka filled for Planner/Analytics/Dashboard/History/Calendar keys (553 keys match `en.json`).

### Added

* **Frontend/Tauri IPC contract check** — all 75 literal frontend `invoke()` commands are compared with `generate_handler!` in `npm run check` and CI.
* **Security/idempotency regression tests** — traversal, symlink escape, media signature, and reply publish claim coverage.
* **Chain detail view** — open any chain to read full segment text, media counts, media IDs, and errors.
* **Richer Planner cards** — preview, segment/image counts, localized status, error snippet; Recover for stuck publishing.
* **Spoiler grouping** — History and Analytics collapse chain segments into one expandable card.
* **Pagination** — Planner chain list uses server-side pages (50 per page).
* **Account overview IPC** — `get_account_overview` for Dashboard aggregates without loading every reply row.

## [0.1.1] — 2026-07-21

### Fixed

* **Trial expiry enforcement** — when the 5-day trial ends, the app locks to About (buy / enter license key). Search, publish, scheduler, and other features are blocked locally until a license is active.
* **Accounts still visible after trial ends** — connected Threads accounts remain listed in the header; local data is not deleted.
* **License key input** — typing a key no longer clears the field on every status refresh.

### Added

* **Planner images & carousels** — **Add images** per chain segment (local JPEG/PNG via file picker). Multiple files on one segment publish as a carousel (up to 20). Broken HTTPS-URL-only field removed.
* **Planner draft management** — Edit, delete, and cancel unpublished chains (draft / queued / failed). Save updates text, media, schedule, and project.

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
