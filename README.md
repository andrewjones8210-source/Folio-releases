# Folio Releases

Public download channel for [Folio](https://github.com/andrewjones8210-source/Folio) — a macOS app that records meetings, transcribes them on-device, and summarizes with your choice of AI provider.

## Download

**[Folio-arm64.dmg](https://github.com/andrewjones8210-source/Folio-releases/releases/latest/download/Folio-arm64.dmg)** — always the latest signed build. Apple Silicon (M1/M2/M3/M4) only. Requires macOS 15.0 Sequoia or later.

## First launch — REQUIRED (don't skip)

Folio is signed with an Apple Development certificate, not a paid Apple Developer ID Application certificate, and is not Apple-notarized. macOS Gatekeeper will quarantine the downloaded DMG and refuse to open the app on first launch — you'll see the icon bounce in the Dock and disappear with no error dialog.

This is normal. You need to clear the quarantine flag **once**, then Folio launches like any other app.

**Fastest fix — one Terminal command:**

```
xattr -dr com.apple.quarantine /Applications/Folio.app && open /Applications/Folio.app
```

Open Terminal (Spotlight → "Terminal"), paste, hit Return. Folio launches.

**GUI alternative if you don't want to use Terminal:**

1. Open **Applications** in Finder.
2. **Right-click** (or Control-click) **Folio.app** → choose **Open**.
3. If macOS says "Folio cannot be opened because it is from an unidentified developer," click **Cancel**, then right-click → **Open** again. (Sometimes Sequoia requires two passes.)
4. On the second prompt, click **Open**.

The DMG also ships with a `READ ME FIRST.rtf` file alongside Folio.app explaining the same step.

## Why this is necessary

Apple charges $99/yr for a Developer ID + notarization, which is the only path to a downloaded macOS app that launches without this manual step. Folio is pre-revenue and doesn't have that yet.

The install is not unsafe — the bundle is correctly signed by Surya's Apple Development certificate. Verify with:

```
codesign --verify --deep --strict /Applications/Folio.app
```

## Auto-update

Once installed and launched, Folio uses [Sparkle](https://sparkle-project.org) to auto-update from `appcast.xml` in this repository. New versions install in place.

## Issue tracking

Public bug tracker: [Folio-releases/issues](https://github.com/andrewjones8210-source/Folio-releases/issues).

## Source code

[andrewjones8210-source/Folio](https://github.com/andrewjones8210-source/Folio).
