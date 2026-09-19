<div align="center">

# ChickBeat

**A lightweight, GSI-compliant CS2 custom music kit creator and real-time manager.**

<br />

[![Release](https://img.shields.io/github/v/release/TYFALY/ChickBeat?style=flat-square&color=E63946&label=Release)](https://github.com/TYFALY/ChickBeat/releases/latest)
[![.NET 8](https://img.shields.io/badge/.NET-8.0-512BD4?style=flat-square&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/download/dotnet/8.0)
[![Platform](https://img.shields.io/badge/Platform-Windows_x64-27272A?style=flat-square&logo=windows&logoColor=white)](https://github.com/TYFALY/ChickBeat/releases/latest)
[![VirusTotal](https://img.shields.io/badge/VirusTotal-Scan_Report-394EFF?style=flat-square&logo=virustotal&logoColor=white)](https://www.virustotal.com/gui/file/7ce4c70670894c63b881419da725cc1f104229fd83f90bcc85615f05e1a177ed)

[Features](#core-features) · [Trust & Anti-Cheat](#trust--anti-cheat-compliance) · [Installation](#installation--usage) · [Tech Stack](#tech-stack) · [Feedback](#feedback)

</div>

---

## Core Features

- **GSI Engine:** Powered by Valve's official Game State Integration. It is driven by HTTP payloads from the game, with no memory hooking and no game file modification.
- **Direct URL Importer:** Auto-generate music kits directly from YouTube, Spotify, or audio links, with FFmpeg and yt-dlp handled automatically. RMS energy profiling maps the highest-energy sections (drops, choruses) to high-impact events like the MVP anthem and round start, and lower-energy sections (intros, verses, breakdowns) to events like death and menu ambience.
- **Kit Creator:** Individual stem volume adjustments, an 800 ms smooth audio fade-out engine, and real-time NAudio preview.
- **Minimal Footprint:** Optimized memory management (under 40 MB RAM) for zero FPS impact in-game.
- **Portable Single Binary:** A self-contained executable. No installer needed.

---

## Trust & Anti-Cheat Compliance

### VAC and anti-cheat safety

> [!IMPORTANT]
> ChickBeat uses Valve's official Game State Integration (GSI) `.cfg` HTTP payloads. It does **not** touch `cs2.exe` memory, inject DLLs, or modify game files.

GSI is a [documented Valve feature](https://developer.valvesoftware.com/wiki/Counter-Strike:_Global_Offensive_Game_State_Integration): the game sends match state as HTTP payloads and ChickBeat reacts to them. Nothing runs inside the game process.

```text
CS2  ── GSI HTTP payloads ──▶  ChickBeat  ──▶  NAudio  ──▶  Your audio output
```

ChickBeat is closed source, so this is a statement of how it works, not something you can confirm by reading code. It is also not a guarantee from Valve, who do not review or endorse third-party tools.

### Windows SmartScreen and antivirus false positives

The first launch may show **"Windows protected your PC"**. This is expected for an unsigned binary:

- **No code-signing certificate.** SmartScreen judges executables by download reputation. Signing certificates cost hundreds of dollars a year, which most independent developers do not pay for. A new or rarely downloaded file gets flagged regardless of what it contains.
- **Self-contained single-file .NET binary.** The executable bundles the runtime and extracts parts of itself at launch, a pattern some antivirus heuristics treat with suspicion.
- **Helper tools.** Launching external tools (yt-dlp, FFmpeg) can trigger behavioral heuristics in some products.

**To run it anyway:**

1. Click **More info** in the SmartScreen dialog, then **Run anyway**.
2. If Windows still blocks it, right-click `ChickBeat.exe` → **Properties** → tick **Unblock** → **OK**. Or in PowerShell:

   ```powershell
   Unblock-File -Path .\ChickBeat.exe
   ```

### Verify your download

The [VirusTotal report](https://www.virustotal.com/gui/file/7ce4c70670894c63b881419da725cc1f104229fd83f90bcc85615f05e1a177ed) is for the file with this SHA-256:

```text
7ce4c70670894c63b881419da725cc1f104229fd83f90bcc85615f05e1a177ed
```

Check that your download matches:

```powershell
Get-FileHash .\ChickBeat.exe -Algorithm SHA256
```

---

## Installation & Usage

1. **Download** `ChickBeat.exe` from [GitHub Releases](https://github.com/TYFALY/ChickBeat/releases/latest).
2. **Run** the executable. FFmpeg and yt-dlp dependencies are handled automatically on first use, or via `%AppData%/ChickBeat/tools/`.
3. **Click "Equip"** on a kit, or create custom kits with the Kit Creator.

---

## Tech Stack

- **C# / .NET 8**
- **[Avalonia UI 11](https://avaloniaui.net/):** cross-platform UI framework
- **[NAudio](https://github.com/naudio/NAudio):** audio processing pipeline

---

## Feedback

Bug reports and feature requests: [GitHub Issues](https://github.com/TYFALY/ChickBeat/issues)

---

Counter-Strike, CS2, and Valve are registered trademarks of Valve Corporation. ChickBeat is an independent project and is not affiliated with or endorsed by Valve Corporation.