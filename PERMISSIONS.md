# Permissions

Snapback asks Chrome for a small set of permissions. Each one is required for a
specific job. Nothing is sent off your machine — the extension talks only to
Google's own servers (to read your library) and writes files only to the local
folder you pick.

## Permissions

### `storage`
Stores your settings (folder format, Live Photo handling, concurrency, etc.)
and migrates older settings out of `chrome.storage.local` on update. Settings
never leave your browser.

### `unlimitedStorage`
Lifts Chrome's default quota on the extension's local database. Snapback keeps
one row per photo in IndexedDB so it can resume where it left off — for a
1M-item library that's tens of MB. Without this permission Chrome would evict
the database mid-backup.

### `sidePanel`
Opens Snapback's UI in Chrome's side panel instead of a popup, so you can keep
it visible alongside Google Photos while it works.

### `alarms`
Wakes the extension's service worker every 25 seconds. Chrome shuts idle
workers down after ~30s; the alarm flushes session progress to disk and keeps
the worker alive while a backup is running. Stops as soon as no backup is
active.

### `scripting`
Injects the scanner script into `photos.google.com` tabs. The scanner is what
walks your library through Google's own API. Snapback only injects into Google
Photos pages — never into any other site.

### `power`
Calls `chrome.power.requestKeepAwake('display')` while a backup, restore, or
delete is running. This stops Chrome from throttling the side panel when the
window isn't focused (which would otherwise stall downloads) and keeps the
display awake so the OS doesn't sleep mid-backup. Released the moment the run
ends.

### `offscreen`
Creates a hidden "offscreen document" that owns the download queue and writes
files to your chosen folder. Chrome's File System Access API can't be used from
service workers or content scripts, so a dedicated offscreen page is the only
way to stream files to disk reliably.

## Host permissions

These are the *only* sites Snapback is allowed to talk to. Every other domain
is off-limits to the extension.

### `https://photos.google.com/*`
The scanner runs here and calls Google's internal `batchexecute` API to list
your library, fetch metadata, request download URLs, and (when you ask) move
items to trash or restore them.

### `https://*.googleusercontent.com/*`
Google serves the actual photo and video bytes from this CDN. Snapback fetches
each file from the URL Google hands back and streams it straight to your
folder.

### `https://*.google.com/*`
Some Google Photos requests redirect through other `google.com` subdomains
(auth, region routing). This permission keeps those redirects from being
blocked.

## Things Snapback does *not* request

- No `<all_urls>` — it cannot read or modify any site outside Google Photos.
- No `tabs` permission — it cannot see your other tabs' URLs or titles.
- No `cookies`, `webRequest`, or `webRequestBlocking` — it does not intercept
  or read cookies, and does not see your normal browsing traffic.
- No `identity` / OAuth — it relies on your existing Google Photos session in
  Chrome. No separate sign-in, no tokens stored anywhere.
- No analytics, telemetry, or remote configuration. The extension never phones
  home.

## Where your data goes

- **Photo and video files**: streamed from Google's CDN directly to the local
  folder you grant via the folder picker. Nothing is uploaded anywhere.
- **Metadata sidecars** (`*.supplemental-metadata.json`): written next to each
  file in the same folder.
- **Session state** (which items are done, which are pending): kept in the
  extension's local IndexedDB so you can pause and resume.
- **Settings**: kept in Chrome's extension storage on your machine.
