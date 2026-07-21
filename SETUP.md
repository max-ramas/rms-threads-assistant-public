# Setup guide

Quick path from download to your first scheduled post.

## Download

Grab the latest release for your platform from the [Releases page](https://github.com/max-ramas/rms-threads-assistant-public/releases/latest):

| Platform | Download |
|----------|----------|
| macOS (Apple Silicon) | `.dmg` |
| Windows | `.exe` (installer) |
| Linux | `.deb` / `.rpm` / [AppImage](https://github.com/max-ramas/rms-threads-assistant-public/releases/latest) |
| Android / iOS | coming soon |

**macOS (first install):** if macOS says the app is “damaged”, the build is not notarized yet. Remove the quarantine flag, then open:

```bash
xattr -cr "/Applications/RMS Threads Assistant.app"
open "/Applications/RMS Threads Assistant.app"
```

**Updates:** macOS, Windows, and Linux AppImage can update from **About → Updates**. `.deb` / `.rpm` installs must be updated manually from Releases.

---

## Create your Meta Developer app

RMS Threads Assistant runs on **your own** Meta Developer app, not a shared one — this keeps your rate limits and API quota separate from every other user.

```
1. Go to developers.facebook.com → Create app
2. Choose a use case that includes Threads (or add the Threads product)
3. Under App settings → Basic, copy your App ID (Client ID) and App Secret
4. Under Facebook Login / Threads → Settings (or Use cases → Customize),
   add this Valid OAuth Redirect URI exactly:

      https://media.rms-ds.com/auth/callback

5. Under App Review → Permissions and features (or Threads use cases),
   request access to every permission below — the app needs all of them.
```

### Threads permissions to enable

When Meta asks which capabilities you need, include **all** of these:

| Permission | Used for |
|------------|----------|
| `threads_basic` | Profile and account access |
| `threads_content_publish` | Posts, replies, and chains |
| `threads_delete` | Delete posts/replies from History |
| `threads_keyword_search` | Find posts by keyword in Projects |
| `threads_read_replies` | Read replies on threads |
| `threads_manage_replies` | Hide/show replies you own |
| `threads_manage_mentions` | Mention-related features |
| `threads_profile_discovery` | Profile lookup |
| `threads_manage_insights` | Engagement metrics in Analytics |

**Development mode:** add your Threads account as a **Tester** (or Admin/Developer) on the app so OAuth works before App Review is complete.

**After adding permissions:** use **Reconnect** in the app (Settings → Accounts) so the new scopes are granted. OAuth only includes permissions that existed at authorize time.

---

## Connect your account

```
1. Open RMS Threads Assistant → Settings → Accounts
2. Click Add account
3. Enter a display name, your Meta Client ID and Client Secret
   (stored only in your OS keychain — never sent to RMS servers except
    for the OAuth code exchange on the RMS edge)
4. Click Connect and complete authorization in the browser window
5. Select the account in the header dropdown when working with projects
```

If Connect fails, double-check the redirect URI and that your Threads user is a tester on the app.

---

## Activate your license

New installs start a **5-day free trial** automatically — no key required.

```
1. Go to About (or click the license label in the status bar)
2. Click Buy license → choose a plan at license.rms-ds.com
3. Paste your license key in About → License key → Save key
```

---

## Complete Meta “Use case testing” (one button)

Before App Review, Meta’s dashboard asks you to run API calls for each permission. The app can do this for you in one step:

```
1. Settings → Limits & Meta (select your account first)
2. Click Run Meta API use-case tests
3. Confirm — the app publishes a short test post (and reply), exercises
   each permission, then deletes the test content
4. Check results in the panel below the button (green = OK)
5. In Meta App Dashboard → Use case testing, statuses may take up to 24h
   to show Complete
```

If any probe fails, use **Reconnect** on the account (Settings → Accounts) to refresh OAuth scopes, then run the tests again.

---

## Add LLM API keys

Reply and post drafts need an LLM provider:

```
1. Settings → API keys (select your account)
2. Enter the API key for your chosen provider (OpenAI, Anthropic, etc.)
3. Save
```

Keys stay on your device in the OS keychain.

---

## Set up your first reply pipeline

```
1. Projects → New project
2. Set search keywords/topic and a short brand context so replies stay on-voice
3. Choose your LLM provider and model settings
4. Set your auto-approval confidence threshold
```

We recommend leaving auto-publish off at first and reviewing drafts manually until you trust the output.

---

## Or start with the Planner

```
1. Planner → New post
2. Write your post
3. In Chain preview, click **Add images** on each segment (JPEG/PNG, ≤8 MB).
   Multiple images on one segment become a carousel (up to 20)
4. Publish now, or schedule for a specific date and time
```

---

## Optional: Telegram moderation

```
1. Settings → General → Telegram integration
2. Add a bot token (from @BotFather) and your chat ID
3. Drafts can be sent for approval before publish
```

---

## Need help?

* [RMS License shop](https://license.rms-ds.com/dashboard/shop) — purchase / renew
* [Latest downloads](https://github.com/max-ramas/rms-threads-assistant-public/releases/latest)
* Website: [rms-ds.com](https://rms-ds.com/)
