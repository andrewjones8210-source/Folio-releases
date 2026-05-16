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
   - **Anthropic / OpenAI** — paste your API key.
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

## Reporting Issues

Open an issue at <https://github.com/andrewjones8210-source/Folio-releases/issues> (public tracker). Attach diagnostic JSON if available.
