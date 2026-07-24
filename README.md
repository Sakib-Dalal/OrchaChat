<br>
<div align="center">
  <p>
    <img src="./assets/orcha-logo.svg" alt="Orcha Chat" width="140"/>
  </p>

  <h1>Orcha Chat</h1>

  **The confidential AI workspace for public institutions.**

  Encrypted end-to-end · personal data tokenised on-device · zero-retention Ghost sessions

  <p>
    <img src="https://img.shields.io/badge/version-1.0.2-2D2D2D?style=flat-square" alt="Version 1.0.2"/>
    <img src="https://img.shields.io/badge/macOS-10.15%2B-2D2D2D?style=flat-square" alt="macOS 10.15+"/>
    <img src="https://img.shields.io/badge/Windows-10%20%7C%2011%20x64-2D2D2D?style=flat-square" alt="Windows 10 or 11 x64"/>
    <img src="https://img.shields.io/badge/licence-proprietary-2D2D2D?style=flat-square" alt="Proprietary licence"/>
  </p>

  <sub>

  **[www.orchachat.com](https://www.orchachat.com)** · [Download](#download) · [Install](#install)

  </sub>
</div>

---

This repository hosts the **desktop app releases** for Orcha Chat — currently
**version 1.0.2**, for macOS and Windows. The product itself — including the web app,
accounts and subscriptions — lives at **[www.orchachat.com](https://www.orchachat.com)**.

## What is Orcha Chat?

Orcha Chat is a secure AI assistant built for government teams — police stations, revenue
offices, district administration. Every message is encrypted, and personal identifiers
(names, Aadhaar numbers, phones, vehicle plates) are replaced with placeholder tags **on
the device** before any model ever sees them. It speaks 8 Indian languages, and the
desktop app ships the same interface as the web app from a single codebase.

**Three workspaces**

- **Chat** — a streaming assistant with a live *Tagged / Plain / Encrypted* view of every
  message, web grounding (DuckDuckGo + india.gov.in), and a zero-retention **Ghost** mode.
- **Notebook** — a chain board: drop in files, links or gov-portal results, then wire
  action nodes into pipelines — summarise → mind-map → translate — plus office tools like
  **redact PII, official letter, RTI reply, meeting minutes**.
- **Studio** — turn a brief into a finished **PDF / Word / slide deck**, with a
  per-document output language selector.

**Two assistant tiers** — **Orcha Lite** (fast, everyday) and **Orcha Pro** (deeper
reasoning, long documents). Pro members pick their default; Notebook and Studio always use
Orcha Pro.

**Privacy by architecture** — end-to-end encryption, on-device PII tokenisation, Ghost
sessions that store nothing, and account/data deletion controls.

**Made yours** — light/dark themes plus an Arc-style custom colour wheel that tints the
whole UI and the ambient background field, a fully customisable ambient effect, 8
languages, keyboard shortcuts.

## Download

**Version 1.0.2** — released 24 July 2026. The version is in every filename below, so you
can always tell which build you have. To check an installed copy on macOS:

```bash
defaults read "/Applications/Orcha Chat.app/Contents/Info.plist" CFBundleShortVersionString
```

On Windows, right-click the installed `Orcha Chat.exe` → **Properties** → **Details**.

| Platform | File | Size | Notes |
|---|---|---|---|
| macOS (Apple Silicon + Intel) | [`Orcha.Chat_1.0.2_universal.dmg`](Orcha.Chat_1.0.2_universal.dmg) | 10 MB | Recommended installer |
| macOS (archive) | [`Orcha.Chat_universal.app.tar.gz`](Orcha.Chat_universal.app.tar.gz) | 8.9 MB | Plain `.app`, no disk image |
| Windows 10/11 (x64) | [`Orcha.Chat_1.0.2_x64-setup.exe`](Orcha.Chat_1.0.2_x64-setup.exe) | 3.6 MB | Recommended installer |
| Windows 10/11 (x64) | [`Orcha.Chat_1.0.2_x64_en-US.msi`](Orcha.Chat_1.0.2_x64_en-US.msi) | 4.5 MB | For managed / silent deployment |

No Linux build yet — use the web app at [www.orchachat.com](https://www.orchachat.com).

### Requirements

- **macOS 10.15 Catalina** or later, Apple Silicon or Intel (one universal binary).
- **Windows 10 or 11, 64-bit**, with WebView2 (preinstalled on Windows 11 and current
  Windows 10; the installer fetches it if missing).
- An internet connection and an Orcha Chat account.

## Install

### macOS

1. Open the `.dmg` and drag **Orcha Chat** into **Applications**.
2. The build is **not code-signed or notarised yet**, so the first launch is blocked.
   Right-click the app → **Open** → **Open**. Do this once; later launches are normal.

If macOS still refuses to open it, clear the quarantine flag:

```bash
xattr -dr com.apple.quarantine "/Applications/Orcha Chat.app"
```

For the `.tar.gz`: unpack it and move `Orcha Chat.app` into `/Applications` yourself, then
follow the same first-launch step.

### Windows

1. Run `Orcha.Chat_1.0.2_x64-setup.exe` and follow the installer.
2. The build is **not code-signed yet**, so SmartScreen shows a warning. Click
   **More info** → **Run anyway**.

For fleet deployment, use the MSI:

```bash
msiexec /i Orcha.Chat_1.0.2_x64_en-US.msi /quiet /norestart
```

### Verify your download

```bash
shasum -a 256 Orcha.Chat_1.0.2_universal.dmg
```

On Windows:

```bash
certutil -hashfile Orcha.Chat_1.0.2_x64-setup.exe SHA256
```

Expected values:

```
d81f70d3163cb528c93eaadd3e16869c8a89ebc01d763983d10d13ac0b223e83  Orcha.Chat_1.0.2_universal.dmg
0fea3cec48d408cc32dcb97dd9bf00caf94012a722f92ecd9096ffbf13daaa14  Orcha.Chat_universal.app.tar.gz
7e0edb5efa44fffe489bb4e8dd5948e123ebcd95fe8ba86a27b90f4a8aa4f5f0  Orcha.Chat_1.0.2_x64-setup.exe
7860ae918edaa7aa1e3d20c82b171b50c577a85a2cf7a09882a65653552c785a  Orcha.Chat_1.0.2_x64_en-US.msi
```

Because the bundles are unsigned, these checksums are the only way to confirm you have the
files we published. Check them before you install.

## Under the hood

The desktop app is a **[Tauri 2](https://v2.tauri.app)** shell around the Orcha Chat web
frontend — one interface, two products, so desktop and web never drift apart. It carries a
strict content-security policy: the webview may talk to Orcha Chat's own backend and
nothing else.

| | |
|---|---|
| Version | 1.0.2 |
| Bundle identifier | `com.sakibdalal.orchachat` |
| macOS binary | universal (`arm64` + `x86_64`), minimum macOS 10.15 |
| Windows binary | `x64`, NSIS installer + WiX MSI |

## Support

- Product, pricing and sign-up — **[www.orchachat.com](https://www.orchachat.com)**
- Questions, bug reports and licensing — **support@orchachat.com**

## Licence

Orcha Chat is **proprietary software**. Copyright © 2026 Sakib Dalal, all rights reserved.
See [`LICENSE`](LICENSE).

The builds here are distributed for use with an Orcha Chat account; downloading one grants
no right to copy, redistribute, modify or reverse engineer it. Your use of the app and the
hosted service is governed by the Orcha Chat Terms of Service and Privacy Policy.

Bundled third-party components keep their own licences — permissive throughout (MIT,
Apache-2.0, ISC, BSD), with no GPL or AGPL anywhere in the tree, plus the IBM Plex fonts
under the SIL Open Font License 1.1.
