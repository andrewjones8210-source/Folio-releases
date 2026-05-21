# Install Folio

Folio is a macOS app that records meetings, transcribes them on-device, and summarizes with your choice of AI provider. Audio never leaves your Mac unless you choose to share it.

## Requirements

- macOS 15.0 (Sequoia) or later
- Apple Silicon (M1 / M2 / M3 / M4)

## Install

1. [Download Folio](https://github.com/andrewjones8210-source/Folio-releases/releases/latest/download/Folio-arm64.dmg) (always the latest signed build).
2. Open the DMG.
3. Drag **Folio.app** into the **Applications** folder.

## First Launch (Important — Read This)

Folio is signed with an Apple Development certificate, **not** a paid Apple Developer ID. macOS Gatekeeper will block the first launch. This is a one-time step.

1. Open **Applications** in Finder.
2. **Right-click** (or Control-click) **Folio.app** → choose **Open**.
3. A dialog will warn that Folio is from an "unidentified developer." Click **Open**.

After this, Folio launches normally from the Dock or Spotlight.

> Double-clicking the app on first launch will show "Folio cannot be opened" with no Open button. Right-click → Open is the workaround.

## Permissions

On first record, macOS will prompt for:

- **Microphone** — required to record your voice.
- **System Audio Recording** — required to capture other meeting participants' audio (Zoom, Meet, Teams, etc.). Optional. You can decline if you only want your own voice.

If you accidentally denied a permission, fix it in **System Settings → Privacy & Security → Microphone / Screen & System Audio Recording**.

## Configure AI Provider

Folio runs transcription on-device. Summarization requires an AI provider.

1. Open **Folio → Settings** (⌘,).
2. Choose a provider:
   - **Anthropic / OpenAI / Groq / Together.ai / DeepSeek** — paste your API key.
   - **Ollama** — point to your local endpoint (default `http://localhost:11434`).
   - **Claude Code** — uses your existing Claude Code subscription. No key needed. Requires the `claude` CLI installed and authenticated.
3. Click **Save**.

## Auto-Update

Folio checks for updates on launch via Sparkle. New versions install in place. You can also trigger a manual check from **Folio → Check for Updates…** in the menu bar.

## Optional: Diagnostics

If you want to help with bug reports without compromising privacy:

1. **Settings → Diagnostics → Save crash + hang reports locally**.
2. Reports are written to `~/Library/Application Support/Folio/Diagnostics/` as JSON.
3. **Nothing is uploaded.** When you hit a bug, click **Reveal Diagnostics in Finder** and attach the relevant files to a GitHub Issue.

Off by default. Toggle off any time.

## Uninstall

1. Quit Folio.
2. Drag **Folio.app** from Applications to the Trash.
3. Optional, to remove all local data:
   ```
   rm -rf ~/Library/Application\ Support/Folio
   rm -rf ~/Library/Caches/com.suryaamara.folio
   ```
4. API keys are stored in the system Keychain. Delete entries matching `com.folio.provider.*` via Keychain Access if desired.

## Troubleshooting

### The Folio icon bounces in the Dock then disappears

You have **v1.0.1** installed. The Sparkle auto-update framework in that build kept its upstream Team ID, and macOS hardened-runtime library validation refused to load it — the process dies before the main window opens. Symptom: 1–2 Dock bounces, then nothing. No Gatekeeper dialog, no crash report.

Fix: download **v1.0.2 or later** from the [Folio releases page](https://github.com/andrewjones8210-source/Folio-releases/releases/latest) and reinstall. Sparkle auto-update cannot recover v1.0.1 — the failure happens before Sparkle even runs.

### My meetings disappeared after updating Folio

Folio v1.0.x and earlier wrote its SwiftData store to `~/Library/Application Support/default.store`. Newer builds write to `~/Library/Application Support/Folio/Folio.store`. On first launch of a new build, Folio consolidates the two: whichever store has the newer modification time wins; the loser is renamed `*.superseded-<date>` and kept on disk so you can recover manually.

To recover the archived store:
```
ls ~/Library/Application\ Support/Folio/
# look for Folio.store.superseded-YYYYMMDD-HHMMSS
```
Then either quit Folio and rename the archive back to `Folio.store` (after backing up the active one), or open both with [DB Browser for SQLite](https://sqlitebrowser.org/) and export rows.

### Claude Code shows "not found" but `claude` works in Terminal

macOS GUI apps don't inherit your shell's `PATH`, so Folio probes a fixed set of install locations (Anthropic's installer, Homebrew, nvm, Bun, Volta, fnm). If your `claude` lives elsewhere, the path probe in Settings → AI Provider → Claude Code (expand "Why not detected?") lists everything Folio looked for. The easiest fix is to symlink it into one of those locations, e.g.:
```
ln -s /path/to/your/claude /usr/local/bin/claude
```
Then click **Retry detection**.

### Cmd+Q while Folio is still summarizing

Folio holds the quit for up to 10 seconds while AI post-processing finishes writing its results. If it takes longer than 10 s, summary writes may be lost — the transcript and diarized segments are saved earlier in the pipeline and will survive the quit either way.

## Reporting Issues

Open an issue at <https://github.com/andrewjones8210-source/Folio-releases/issues> (public tracker). Attach diagnostic JSON if available.
