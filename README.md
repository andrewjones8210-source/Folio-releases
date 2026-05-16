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

1. Download the latest `Folio-x.y.z-arm64.dmg`.
2. Open the DMG, drag **Folio.app** into **Applications**.
3. **First launch:** right-click (or Control-click) Folio.app in Applications → **Open** → confirm.

> Folio is signed with an Apple Development certificate, not a paid Apple Developer ID, so macOS Gatekeeper requires the right-click bypass on first launch only. Subsequent launches work normally.

Full instructions: [INSTALL.md](INSTALL.md).

## What Folio Does

- Records meetings (mic + system audio via ScreenCaptureKit).
- Transcribes locally on-device with WhisperKit (no cloud).
- Diarizes speakers locally with SpeakerKit (CoreML / Apple Neural Engine).
- Summarizes with the AI provider of your choice (Anthropic, OpenAI, Ollama, or your existing Claude Code subscription).
- Shares meeting summaries to Slack.

Audio and transcripts never leave your Mac unless you explicitly share them.

## Auto-Update

Folio uses [Sparkle](https://sparkle-project.org) and checks this repository's `appcast.xml` on launch. New versions install in place. You can also trigger a manual check via **Folio → Check for Updates…** in the menu bar.

## Reporting Bugs

Open an issue: <https://github.com/andrewjones8210-source/Folio-releases/issues>

If you've enabled **Settings → Diagnostics**, attach the relevant JSON files from `~/Library/Application Support/Folio/Diagnostics/`. Diagnostics are off by default and stay on your Mac unless you choose to share them.

## Privacy

- Microphone access is used only while you are recording.
- System audio capture (other meeting participants) is opt-in per macOS permission.
- API keys for external AI providers are stored in your system Keychain.
- No telemetry, no analytics, no usage tracking.
- The only outbound network requests Folio makes without your action are: (1) a daily Sparkle update check against this repo and (2) automated download of WhisperKit / SpeakerKit ML models from Hugging Face on first launch.

## License

Distribution of binaries from this repo only. Source license is governed by the private source repository.
