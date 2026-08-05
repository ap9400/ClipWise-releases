# ClipWise Changelog

This file is the source of truth for what changed in each release. `release.sh`
extracts the section matching the version being published and ships it as the
Sparkle release notes and the GitHub release body — so what is written here is
what users read in the update dialog. A release cannot be cut without a section.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and
[Semantic Versioning](https://semver.org/). Entries are written for the person
who has to decide whether to install the update, not for the person who wrote
the code: lead with what they will notice, and describe a bug only when someone
lived through it and deserves to know it is gone.

## Unreleased

## 2.9.0 — 2026-08-04

### Added
- Protected Secrets: press Control+Command+P anywhere to search every
  secret you've saved. Type part of a name, pick with the arrow keys, press
  Return, and Touch ID copies it to the clipboard as usual. Once you have
  more than a handful of secrets this replaces having to remember a separate
  shortcut for each one — and before you type anything, it lists what you
  used most recently first. Accents and capitals don't matter, so a secret
  saved for "münchen.de" is found by typing "munchen". The shortcut is
  rebindable in Settings › Secrets.
- Secrets can now carry tags — comma-separated words like "work, vpn,
  login" — so you can find one by what it's for and not only by what you
  called it. Tags are searched alongside the name, are never copied to the
  clipboard, and never leave your Mac.
- You can now bulk-import passwords from a Chrome or Chromium CSV export.
  Chrome, Edge, Brave, Vivaldi and Opera can all save every password you
  have to a CSV file; Settings › Secrets reads that file, shows you what
  it found, and lets you tick off exactly which entries to keep. Passwords
  are never shown on screen during the import. Each one you keep becomes a
  normal Protected Secret in the Keychain behind Touch ID, named after its
  site and account and tagged with its site — so typing the site name in
  the search palette finds it straight away.
- Importing the same export a second time no longer quietly doubles
  everything. Entries you already have are marked "Already saved" and left
  unticked, so re-importing after saving a few new logins in your browser
  adds only what's new.
- Settings › Secrets now has a filter box once you have more than a handful
  of secrets, so a few hundred imported logins are still a list you can find
  one thing in.
- After an import, ClipWise tells you where that CSV file still is and
  offers to move it to the Trash. A browser password export is every
  password you have saved, sitting in plain text in your Downloads folder;
  importing it here doesn't change that, and nothing is deleted unless you
  ask for it. If you don't deal with it there and then, Settings › Secrets
  keeps reminding you until you do — that offer used to disappear the moment
  the window closed.
- Settings › Secrets has a "Delete All Secrets" option, for starting over or
  clearing out a browser import — one confirmation, and it removes the
  Keychain values themselves, not just the list.

### Security
- The list of secret names and tags that ClipWise keeps on disk is now
  readable only by you. It has never held a secret's value — those are in
  the Keychain — but after a browser import it does describe which sites you
  have accounts on and under which username, and it was being written with
  default permissions that let any program running as you read it. Settings ›
  Secrets now says plainly what that file holds.

## 2.8.0 — 2026-08-02

### Added
- Protected Secrets: a new Settings pane for keeping a password or other
  short secret in ClipWise and copying it to the clipboard on demand. Each
  secret gets its own keyboard shortcut; every use requires Touch ID or your
  device password; the copy is wiped from the clipboard automatically after
  a short delay. Secrets never appear in ClipWise's own clipboard history.
  Ships with a few example entries so the Settings pane isn't empty on first
  look — delete them any time.

### Fixed
- Resizing the clipboard popup no longer quits ClipWise. Dragging its edge
  wrote your window size to disk on every step of the drag, and each write
  woke enough of the app to restart the window's layout — so the window could
  be asked to lay itself out again faster than it could finish, until macOS
  gave up and terminated ClipWise. It now records the size once you let go.
  Hovering the divider between the list and the preview also left a stray
  resize cursor behind each time, which contributed to the same pile-up.
- Copying the same thing twice no longer deletes it from your history.
  Whenever a copy matched something already saved, ClipWise removed the old
  entry to replace it — and then immediately deleted the replacement too,
  believing it was over the history limit. It was not: this happened at any
  history size, with a thousand items against a limit of two thousand. Anything
  you copied a second time simply vanished.
- ClipWise no longer disappears without warning while you are copying. The
  entry deleted above was still listed in the index used to spot duplicates,
  so the next time you copied that same text ClipWise went looking for
  something that no longer existed and quit instantly — no error, no dialog,
  nothing on screen. It was most likely to strike text you copy repeatedly,
  which is why it felt random. The same could happen to anything removed by
  the history limit, the storage budget, or Clear History; all of those are
  safe now.
- The Reader's "There is no text to read" error no longer gets stuck on
  screen forever. "Try Again" used to resend the same empty text and
  reproduce the identical error every time, with no way to dismiss it; the
  dialog now offers a way to close it, and the app refuses to open a Reader
  window for empty text in the first place.

## 2.7.1 — 2026-07-27

### Fixed
- The Reader no longer plays a voice sample before your text. The local voice
  engine reports its progress on the same channel it returns audio on, and the
  app only skipped those progress messages when something was listening for
  them — so a preview's audio could be handed to your reading instead.
- Word highlighting follows the words actually being spoken again. It was the
  same fault: the reading received another request's word timings along with
  its audio, so the highlight had nothing to do with what you heard.
- The Reader's buttons take clicks anywhere on the button. They previously
  responded only on the drawn icon, a target a few points across, which made
  the speed − and + look broken and every other control feel unreliable.
- Aiming for a voice's preview button in the voice list no longer selects that
  voice instead, which restarted the reading.

### Changed
- The Reader's toolbar is two rows: what is being read and how it is going on
  top, controls underneath. Everything previously shared one line and had no
  room to be legible.
- Playback speed is a `− 1.25x +` stepper on the player bar rather than buried
  in a popover, and the presets are still one click away on the readout.
- Background generation of voice previews now waits for your reading to finish.
  The voice engine answers one request at a time, so previews generated during
  a reading were not running alongside it — they were running instead of it.
- An available update now shows Sparkle's dialog with the release notes for
  that version, and Install / Remind Me Later / Skip This Version. It appears
  once per version; after that the menu-bar badge carries the signal and
  clicking it reopens the same dialog.

### Added
- Update notes. Each release now carries a description of what changed, shown
  in the update dialog before you install and reachable from there as a full
  history. Previously an update offered a version number and nothing else.
- A "What's New" window the first time a newly installed version runs, so a
  change you notice afterwards has somewhere to be explained. It is silent on a
  first install, where there is nothing to compare against.

## 2.7.0 — 2026-07-27

### Distribution and Updates (new)
- Enabled automatic updates. ClipWise checks for a new version once a day and can be checked on demand from Settings → General; both the toggle and the button existed already but the update feed was empty, so every check silently did nothing.
- Updates are published to a public releases repository and are cryptographically signed — ClipWise installs one only if the signature matches.
- Added `scripts/release.sh` to build, sign, publish, and update the feed in one step.

### Offline Voice Install (new)
- The Kokoro voice can now be installed from inside the app. Open the Reader and choose Set Up Offline Voice; ClipWise downloads the package, checks it against a published checksum, and installs it, with a Remove button in the same window.
- Previously the offline voice could only be set up by hand, and required Homebrew and a matching Python 3.12 on the machine. Copying ClipWise to another Mac left the Reader's Kokoro engine broken with no way to fix it from the app.
- The voice package is downloaded on demand rather than bundled, so the app download stays small and app updates never re-download it. The Reader works immediately with the built-in macOS voices either way.
- The package is fully self-contained — it carries its own Python interpreter and model weights, needs no Homebrew, and never touches the network once installed.
- Added `scripts/build-kokoro-runtime.sh` and `scripts/publish-kokoro-runtime.sh` to build and publish it, and `docs/releasing.md` describing the whole pipeline.

### ClipWise Reader (new)
- Added the Reader: select text anywhere and press ⇧⌃R to have it read aloud, with the spoken word highlighted in a scrolling view that follows along.
- Added two voice engines — Kokoro-82M running locally for exact per-word timing, and the built-in macOS system voices for estimated timing with no install.
- Added a voice picker with per-voice preview, adjustable speed (0.5x–2.0x), text size, highlight colour, auto-scroll, and a keep-on-top pin.
- Added reading history in three places: a popover in the reader window, a Reader tab in the menu-bar popup, and a standalone Audio History window. Any past reading can be replayed or saved as a single audio file.

### Reader Playback
- Audio now starts after the first chunk instead of waiting for the whole reading, and later chunks generate behind the audio already playing.
- Sized the first chunk to roughly one sentence. At the engine's measured ~160 characters/second, the previous uniform 900-character chunk meant about 5.5 seconds of silence before playback began.
- Changing voice or engine mid-reading now resumes from the current sentence in the new voice, instead of restarting the whole reading from the top.
- Clicking anywhere in the text now jumps there, snapping to the start of that sentence. Positions already rendered are a plain seek; positions outside the queued audio generate from that sentence.
- Play/pause intent is tracked separately from playback, so pausing while audio is still generating is no longer overridden when the next chunk arrives.

### Reader Fixes
- Fixed word highlighting drifting out of sync: alignment now trusts the engine's reported offsets when they still spell the token, instead of searching for the token text. A normalized token (a number spoken as words) had no literal match, so the search consumed a later occurrence and dragged every subsequent word off by one.
- Fixed ⇧⌃R stacking a new reader window on every use. The old window kept playing its own audio behind the new one and held the single resident Kokoro server busy, so the new window sat at "Generating…" with dead controls.
- Fixed the reader hanging permanently when the local voice helper stopped responding: reads are now bounded and a wedged helper is restarted or reported as an error.
- Fixed seeking backwards skipping every chunk that had already played, because re-queued audio items were not rewound.
- Stopped stitching every reading into a single file during playback. Merging now happens only when the audio is actually saved; pressing Save mid-reading waits for generation to finish and shows a pending state.

### Documentation
- Reorganized the project documentation around a clearer top-level doc set: `README.md`, `VISION.md`, `ROADMAP.md`, and `CHANGELOG.md`.
- Updated the README to explain repository structure, source layout, and where to find active project docs.
- Promoted roadmap visibility by adding a root-level `ROADMAP.md` instead of relying on hidden planning notes.

### Performance
- Improved menu bar popup hover responsiveness by avoiding repeated full-list lookups during pointer movement.
- Reduced repeated row rendering work by calculating visible pinned and unpinned history items once per popup list render pass.
- Cached generated color swatches and skipped unnecessary hex parsing for normal text entries.

### AI Model Selection
- Synced model selection across the menu bar popup, settings, and prompt/instruct surfaces so provider/model changes stay consistent throughout the app.
- Centralized model-selection writes through the shared AI provider manager.
- Preserved existing CLI thinking configuration when changing CLI models, instead of overwriting it during model switches.

### UI Polish
- Fixed clipped drop-shadow on the floating Transform HUD by enlarging the host panel so the shadow renders within bounds.
- Fixed clipped drop-shadow on the prompt/instruct panel by reserving padding for the shadow around the visible rounded rectangle.

### AI Text Transforms
- Allowed default text transform commands to be deleted from AI settings.
- Replaced the exposed Reset All button with a Manage Defaults menu for resetting default prompts or restoring deleted original transforms.
- Added restore confirmation copy with an optional checkbox to also delete user-created text transform commands.
- Disabled Manage Defaults menu items now spell out why they're unavailable (e.g. "no edits to reset", "none missing").
- Added a confirmation dialog when deleting a built-in default, with a reminder that it can be restored from Manage Defaults.

## v1.0.0-beta — 2026-03-24

Complete rebrand to ClipWise with new onboarding experience and clean identity separation.

### Rebrand
- **Full rename**: Maccy/MaccyPerf/ClipAI references replaced across all source, localization (36+ locales), docs, and Xcode project
- **New bundle ID**: `com.clipwise.app` — clean break from upstream `org.p0deje.Maccy`
- **CLI renamed**: `clipwise`, `clipwise-transform`, `clipwise-keys`
- **Config directory**: `~/.config/clipwise/`
- **Pasteboard type**: `com.clipwise.pasteboard`
- **Automatic migration**: UserDefaults, clipboard database, config directory, keychain entries, and explanation history all migrate from old paths on first launch

### First-Launch Onboarding
- **4-screen wizard**: Welcome, Accessibility, AI Configuration, Ready
- **Live accessibility detection**: Polls for permission grant and shows green checkmark when enabled
- **AI provider picker**: CLI, Anthropic API, OpenAI API, Ollama, LM Studio — with info popovers explaining each option
- **Binary detection**: Automatically detects installed Claude Code and Codex CLI
- **Smart keychain access**: Password prompt only appears when storing API keys, never for CLI-only users
- **Re-runnable**: Available from Settings > Advanced > "Run Setup..."

### AI Provider Improvements
- **Renamed**: "Backend Provider" → "AI Provider" throughout
- **Simplified**: CLI label no longer shows "(ClipWise Transform)"
- **Keychain consent**: Explicit "Secure Keychain Storage" alert before any system password dialog, both in onboarding and settings

## v1.1.0 — 2026-03-22

Pre-release polish: AI settings organization, OAuth login, prompt management, and History UI improvements.

### AI Settings
- **Visual section grouping**: Backend & Model Configuration and Commands & Prompts areas are now clearly separated with styled section headers and icons.
- **Provider config panels**: Each provider's settings (CLI, Anthropic, OpenAI, Ollama, LM Studio) wrapped in styled containers with header icon, title, and live status badge.
- **ChatGPT OAuth login**: Sign in with your ChatGPT Plus/Pro subscription instead of entering an API key. Uses PKCE OAuth flow with browser-based login and automatic token management.
- **Auth method picker**: OpenAI settings now offer a choice between API Key and ChatGPT Login via segmented control.

### Prompt Management
- **Delete any command**: All commands (including built-in defaults) can now be deleted from the active view.
- **Restore Defaults**: Brings back any deleted default commands and resets modified prompts without touching custom commands. Defaults are stored immutably and can always be reinstated.
- **Prompt status indicator**: Edit sheet shows "Default prompt" or "Modified from default" to indicate the current state.

### AI Insights
- **Window design polish**: Improved toolbar button sizing, accent-colored tab selection, copy button feedback, and enhanced loading state.
- **History preview panel**: Hovering an AI Insight entry in the History popup shows its AI response and original source text in the slideout preview panel (same panel used by clipboard items). Includes "Open in AI Insights" button to launch the full window.
- **Inline model selector**: AI Insights tab in the History popup includes a model switcher for changing providers without navigating to Settings.

### Bug Fixes
- **Fix clipboard preview bleeding into AI Insights tab**: Switching tabs now properly clears the other tab's selection so stale clipboard previews don't persist.
- **Fix preview not opening for AI Insights**: The slideout preview panel now correctly opens when hovering AI insight entries (previously only clipboard items could trigger it).

## v1.0.0 — 2026-03-21

First release. Forked from [Maccy](https://github.com/p0deje/Maccy) and rebuilt with performance optimizations, AI-powered text transforms, and a CLI for agent integration.

### Performance
- **Windowed loading**: Only loads 200 items at startup instead of the entire history. Infinite scroll loads more on demand.
- **Full-content search**: Search indexes up to 50K characters per entry (was 1K truncated title). Finds text buried deep in long clipboard entries.
- **Smart search**: Exact substring match always runs first across all search modes (exact, fuzzy, regex, mixed). Fuzzy mode no longer drowns exact matches.
- **Search normalization**: Punctuation tolerance ("dont" finds "don't"), symbol interchangeability (& ↔ and, % ↔ percent), number interchangeability (5 ↔ five).
- **Relevance ranking**: Results sorted by match position — matches near the start of content rank higher.
- **Large entry optimization**: Cached hasImage flag, lazy preview text (2K cap), content size display in preview.
- **Memory leak fixes**: Manual cascade deletion of HistoryItemContent (workaround for SwiftData bug), preview image eviction on popup close.
- **History cap raised**: 999 → 100,000 entries.
- **Database cleanup**: Purged 774MB of orphaned content records from original ClipWise database.

### AI Text Transforms
- **Global hotkeys**: Select text in any app and press a shortcut to transform it inline via Claude or Codex.
- **Built-in commands**: Fix Grammar (⇧⌃G), Make Better (⇧⌃B), Make Digestible (⇧⌃D), Format Markdown (⇧⌃M), Summarize (⇧⌃S), Clean Code (⇧⌃J), Custom Prompt (⇧⌃P).
- **Custom commands**: Add your own commands with custom prompts and key bindings via Settings > AI.
- **Model selection**: Claude Haiku/Sonnet/Opus and Codex (GPT-5.4) supported, switchable in settings.
- **Floating HUD**: Small overlay appears near cursor during transforms with spinner and cancel button.
- **Original text preserved**: Clipboard history captures the original before overwriting with the transform result.
- **Session naming**: Each transform names its Claude session (e.g., "ClipWise: Grammar fix — hey boss just wanted...") for easy browsing.
- **Editable prompts**: All built-in prompts are editable in settings with revert-to-default support.
- **Reset All**: One-click reset of all commands to defaults with confirmation dialog.

### CLI (`clipwise` command)
- `get` / `set` — read/write clipboard
- `history [n]` — show recent entries
- `search <term>` — full-text search across all content
- `entry <id>` — get full content by ID
- `paste-entry <id>` — restore a history entry to clipboard
- `ai <mode>` — AI transforms from the command line
- `format <mode>` — quick formatting (json, trim, upper/lower, strip-html, etc.)
- `stats` — database overview
- `cleanup` — purge orphaned records

### UI Improvements
- **Preview on hover only**: Preview panel no longer auto-opens when popup first appears — only on deliberate hover.
- **First-item hover fix**: Hovering over the pre-selected first item now correctly triggers the preview.
- **Right-click menu**: Right-click the menu bar icon for Settings, About, and Quit.
- **Click responsiveness**: `becomesKeyOnlyIfNeeded` prevents swallowed first-clicks during fast workflows.
- **Preview delay**: Lowered from 1500ms to 300ms for faster preview response.
- **Content size in preview**: Shows byte size of each clipboard entry in the preview panel.
- **Sandbox disabled**: Enables global hotkey registration and CLI process execution.

### Rebranding
- Renamed from ClipWise to **ClipWise**
- Default menu bar icon changed to paperclip
- Bundle ID: `com.clipwise.app` (separate from original ClipWise)
