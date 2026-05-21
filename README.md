# Folio — Releases

Public download + auto-update channel for **Folio**, a privacy-first macOS meeting recorder, transcriber, and AI summarizer that runs on-device.

The application source code lives in a separate private repository. This repo hosts only:

- Signed DMG release builds
- The Sparkle `appcast.xml` feed
- The public issue tracker

## Download

**[Download Folio for macOS (Apple Silicon)](https://github.com/andrewjones8210-source/Folio-releases/releases/latest/download/Folio-arm64.dmg)**

Always serves the latest signed build. See the [Releases page](https://github.com/andrewjones8210-source/Folio-releases/releases/latest) for version history and release notes.

System requirements: macOS 15.0 (Sequoia) or later, Apple Silicon.

## Install

1. Click the **Download** link above. Safari/Chrome will save `Folio-arm64.dmg` to your **Downloads** folder.
2. Double-click `Folio-arm64.dmg` to mount it.
3. In the window that opens, drag **Folio.app** onto the **Applications** shortcut.
4. Eject the DMG (right-click the disk in Finder → **Eject**).

## First Launch — Bypass Gatekeeper (One-Time Step)

> **Why this is needed:** Folio is signed with an Apple Development certificate, **not** a paid Apple Developer ID. macOS Gatekeeper treats Development-signed apps as "from an unidentified developer" and blocks the first launch. The bypass below tells macOS you trust this app. You only do it once — subsequent launches are normal.

**Do not double-click Folio.app on first launch.** Double-clicking will show:

> *"Folio cannot be opened because it is from an unidentified developer."*

…with no **Open** button. To bypass:

1. Open **Finder** → **Applications**.
2. **Right-click** (or Control-click) **Folio.app** → choose **Open**.
3. macOS shows a warning dialog: *"macOS cannot verify the developer of 'Folio'. Are you sure you want to open it?"*
4. Click **Open**.

Folio launches. From now on, you can launch it normally from the Dock, Spotlight, or Launchpad.

### If the Right-Click → Open Trick Doesn't Work

On macOS Sequoia (15.x), Apple sometimes hides the **Open** button entirely. If that happens:

1. Try to open Folio (it will be blocked).
2. Open **System Settings** → **Privacy & Security**.
3. Scroll to the **Security** section near the bottom.
4. You'll see *"'Folio' was blocked from use because it is not from an identified developer."*
5. Click **Open Anyway**.
6. Authenticate with your password or Touch ID.

## Privacy Permissions

Folio records audio locally and never sends it off your Mac unless you explicitly share. macOS still requires you to grant permission. On first record, you'll be prompted for:

| Permission | Why Folio Needs It | Required? |
|---|---|---|
| **Microphone** | Records your voice | Yes |
| **Screen & System Audio Recording** | Captures other meeting participants (Zoom, Meet, Teams) via ScreenCaptureKit | Optional — decline if you only want your own voice |
| **Speech Recognition** | (Legacy path only — not used by the default WhisperKit on-device transcription) | No |

Grant each prompt as it appears.

### If You Denied a Permission by Mistake

Open **System Settings** → **Privacy & Security**, then:

- **Microphone** → toggle **Folio** on.
- **Screen & System Audio Recording** → toggle **Folio** on.

You may need to quit and relaunch Folio for the change to take effect.

### What Folio Sends Off Your Mac (and What It Doesn't)

| Data | Leaves Your Mac? |
|---|---|
| Audio recordings | **Never** unless you choose to share/export |
| Transcripts | **Never** unless you choose to share/export |
| Meeting summaries | Only the **prompt text** is sent to the AI provider you configured (Anthropic / OpenAI / Groq / Together.ai / DeepSeek / Ollama / Claude Code subscription). Choose **Ollama** for fully offline. |
| Slack share | Only if you click **Share to Slack** |
| API keys | Stored in your macOS Keychain. Never sent anywhere except the provider you configured. |
| Telemetry / analytics | **None.** Folio has no analytics SDK. |
| Update check | Sparkle requests `appcast.xml` from this GitHub repo once per day. No identifying info. |
| ML model downloads | On first launch, Folio downloads WhisperKit (transcription) + SpeakerKit (diarization) models from Hugging Face. One-time. |

Full install + privacy details: [INSTALL.md](INSTALL.md).

## What Folio Does

- Records meetings (mic + system audio via ScreenCaptureKit).
- Transcribes locally on-device with WhisperKit (no cloud).
- Diarizes speakers locally with SpeakerKit (CoreML / Apple Neural Engine).
- Summarizes with the AI provider of your choice (Anthropic, OpenAI, Groq, Together.ai, DeepSeek, Ollama, or your existing Claude Code subscription).
- Shares meeting summaries to Slack.

## Auto-Update

Folio uses [Sparkle](https://sparkle-project.org) and checks this repository's `appcast.xml` on launch. New versions install in place. You can also trigger a manual check via **Folio → Check for Updates…** in the menu bar.

## Reporting Bugs

Open an issue: <https://github.com/andrewjones8210-source/Folio-releases/issues>

If you've enabled **Settings → Diagnostics**, attach the relevant JSON files from `~/Library/Application Support/Folio/Diagnostics/`. Diagnostics are off by default and stay on your Mac unless you choose to share them.

## License

Distribution of binaries from this repo only. Source license is governed by the private source repository.
