# Changelog

A user-friendly history of changes to Codex Session Viewer. The version
shown in the top app bar matches the latest entry below — if they don't
match, refresh the page (Cmd/Ctrl + Shift + R) to clear your browser
cache.

## v1.2.1 — 2026-05-30

- Fixed the **stat and inactivity-marker tooltips**, which previously
  relied on flaky browser-native tooltips. They now appear as styled
  popovers on hover, with clearer dotted-underline cues on the stat
  labels so it's obvious what's hoverable.

## v1.2.0 — 2026-05-30

- Added a **Changelog** link in the top app bar so you can see what
  changed in each version without leaving the page.

## v1.1.0 — 2026-05-30

- Added **Total time** and **Active time** to the session header.
  - *Total time* is the wall-clock duration from the first event in the
    session to the last.
  - *Active time* approximates how long you were actually working with
    Codex, by ignoring gaps of more than 5 minutes between events.
  - Hover either label for a tooltip explaining what it measures.
- Added **inline inactivity markers** in the transcript. Wherever there
  was a gap of more than 5 minutes between events, you'll now see a
  divider like `———— INACTIVE · 12m ————`. Hover the marker for an
  explanation.

## v1.0.1 — 2026-05-30

- Added a **Help** link in the top app bar that opens the project
  README in a new tab.
- Added a **"New here?"** link on the drop screen pointing to the same
  guide, for first-time visitors.
- Added a small **version indicator** in the top app bar so you can
  always tell which build you're looking at (helpful for diagnosing
  browser-cache issues).

## v1.0.0 — Initial release

- Drop a Codex CLI `.tar.gz` log archive onto the page to get a clean,
  browsable transcript of every turn, command, patch, plan, and web
  search from your session.
- Everything runs locally in your browser — nothing is uploaded.
- Multi-session archives show a list view; single-session archives go
  straight to the transcript.
- Sidebar table of contents, collapsible terminal/patch cards, and
  toggles for commentary, terminal output, and reasoning.
