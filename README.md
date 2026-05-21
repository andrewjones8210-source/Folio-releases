# Folio Releases

Public download channel for [Folio](https://github.com/andrewjones8210-source/Folio) — a macOS app that records meetings, transcribes them on-device, and summarizes with your choice of AI provider.

## Download

**[Folio-arm64.dmg](https://github.com/andrewjones8210-source/Folio-releases/releases/latest/download/Folio-arm64.dmg)** — always the latest signed build. Apple Silicon (M1/M2/M3/M4), macOS 15.0 Sequoia or later.

## First launch

The first time you open Folio, macOS will say "Folio cannot be opened because it is from an unidentified developer." This is the standard one-time step for any independent Mac app.

1. Open **Applications** in Finder.
2. **Right-click** (or Control-click) **Folio.app** → choose **Open**.
3. If Sequoia hides the **Open** button on the first prompt, click **Cancel**, then right-click → **Open** again — the second prompt has the **Open** button.
4. Click **Open**.

Folio launches. From now on, double-click it from the Dock or Applications like any other app.

<details>
<summary>Advanced: Terminal one-liner alternative</summary>

```
xattr -dr com.apple.quarantine /Applications/Folio.app && open /Applications/Folio.app
```

</details>

## Auto-update

Once installed, Folio uses [Sparkle](https://sparkle-project.org) to auto-update from `appcast.xml` in this repository. New versions install in place.

## Issue tracking

[Folio-releases/issues](https://github.com/andrewjones8210-source/Folio-releases/issues).

## Source code

[andrewjones8210-source/Folio](https://github.com/andrewjones8210-source/Folio).
